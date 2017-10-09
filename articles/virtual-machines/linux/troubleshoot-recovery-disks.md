---
title: "aaaUse uma VM de resolução de problemas com Olá Azure CLI 2.0 do Linux | Microsoft Docs"
description: "Saiba como tootroubleshoot emite VM com Linux utilizando a ligação Olá SO disco tooa recuperação VM Olá Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a>Resolver problemas de uma VM com Linux ligando Olá SO disco tooa VM de recuperação com Olá Azure CLI 2.0
Se a máquina virtual (VM) do Linux encontra um erro de arranque ou de disco, poderá ser necessário tooperform passos no disco rígido virtual Olá próprio de resolução de problemas. Um exemplo comum é uma entrada inválida no `/etc/fstab` Olá VM que impede de ser capaz de tooboot com êxito. Detalhes deste artigo como toouse Olá, Azure CLI 2.0 tooconnect seu virtual rígido disco tooanother VM com Linux toofix quaisquer erros, em seguida, voltar a criar a VM original. Também pode executar estes passos com Olá [CLI do Azure 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="recovery-process-overview"></a>Descrição geral do processo de recuperação
Olá, processo de resolução de problemas é o seguinte:

1. Elimine Olá VM encontrar problemas, mantendo Olá os discos rígidos virtuais.
2. Anexe e montar o disco rígido virtual de Olá tooanother VM com Linux para fins de resolução de problemas.
3. Ligar toohello VM de resolução de problemas. Editar ficheiros ou executar quaisquer ferramentas toofix problemas no Olá original disco virtual.
4. Desmonte e desanexar o disco rígido virtual Olá de Olá VM de resolução de problemas.
5. Crie uma VM utilizando Olá original disco virtual.

tooperform estes passos, a resolução de problemas precisar de mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).

No Olá exemplos a seguir, substitua os nomes de parâmetros com os seus próprios valores. Os nomes dos parâmetros de exemplo incluem `myResourceGroup`, `mystorageaccount`, e `myVM`.


## <a name="determine-boot-issues"></a>Determinar os problemas de arranque
Examine Olá saída série toodetermine motivo pelo qual a VM não é capaz de tooboot corretamente. Um exemplo comum é uma entrada inválida no `/etc/fstab`, ou Olá subjacente o disco rígido virtual que está a ser eliminado ou movido.

Obter registos de arranque Olá com [az vm diagnóstico de arranque get-arranque-registo](/cli/azure/vm/boot-diagnostics#get-boot-log). Olá exemplo seguinte obtém saída série Olá da VM com o nome de Olá `myVM` no grupo de recursos de Olá designado `myResourceGroup`:

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

Reveja Olá série toodetermine por que motivo está a falhar tooboot Olá VM de saída. Se a saída de série de Olá não está a fornecer qualquer indicação, poderá ser necessário tooreview ficheiros de registo na `/var/log` assim que tiver Olá virtual disco rígido ligado tooa VM de resolução de problemas.


## <a name="view-existing-virtual-hard-disk-details"></a>Ver detalhes de disco rígido virtual existente
Antes de pode anexar o disco rígido virtual (VHD) de tooanother VM, terá de tooidentify Olá URI de disco de SO Olá. 

Ver informações sobre a VM com [mostrar de vm az](/cli/azure/vm#show). Olá utilize `--query` disco de SO de toohello do sinalizador tooextract Olá URI. Olá exemplo seguinte obtém informações do disco para a VM com o nome de Olá `myVM` no grupo de recursos de Olá designado `myResourceGroup`:

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

Olá URI é demasiado semelhante**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.

## <a name="delete-existing-vm"></a>Eliminar VM existente
Os discos rígidos virtuais e as VMs são dois recursos diferentes do Azure. Um disco rígido virtual é onde são armazenadas Olá sistema operativo, as aplicações e configurações. Olá própria VM é apenas metadados, que definem o tamanho de Olá ou localização e referencia recursos, tais como um disco rígido virtual ou o cartão de interface de rede virtual (NIC). Cada disco rígido virtual tem uma concessão atribuída quando ligado tooa VM. Embora os discos de dados podem ser ligados e anular a exposição mesmo enquanto Olá VM está em execução, o disco do SO Olá não pode ser desligado, a menos que Olá recurso VM é eliminado. concessão de Olá continua disco de SO de Olá tooassociate com uma VM, mesmo quando se encontra num estado parado e desalocado essa VM.

Olá primeiro passo toorecover a VM é o recurso VM de Olá toodelete próprio. A eliminar Olá VM deixa Olá os discos rígidos virtuais na sua conta de armazenamento. Depois de Olá que VM é eliminada, anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolva os erros de Olá.

Eliminar Olá VM com [az vm eliminar](/cli/azure/vm#delete). Olá, seguindo as eliminações de exemplo Olá VM com o nome `myVM` do grupo de recursos de Olá designado `myResourceGroup`:

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

Aguarde até que Olá VM terminou a eliminação antes de anexar o disco rígido virtual de Olá tooanother VM. tem de concessão de Olá no disco rígido virtual Olá que associa-Olá VM toobe lançada antes de pode anexar o disco rígido virtual de Olá tooanother VM.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Anexar tooanother de disco rígido virtual existente VM
Para Olá, em seguida alguns passos, utilizar outra VM para fins de resolução de problemas. Anexar Olá toothis do disco rígido virtual existente toobrowse VM de resolução de problemas e editar o conteúdo do disco Olá. Este processo permite-lhe toocorrect quaisquer erros de configuração ou a aplicação adicional de revisão ou o sistema de ficheiros de registo por exemplo. Escolha ou crie outro toouse VM para fins de resolução de problemas.

Anexar o disco rígido virtual existente por Olá com [az unmanaged-disco da vm ligar](/cli/azure/vm/unmanaged-disk#attach). Quando anexa Olá existente disco virtual, especifique o disco de toohello URI de Olá obtido no Olá anterior `az vm show` comando. Olá exemplo seguinte anexa um toohello de disco rígido virtual existente VM com o nome de resolução de problemas `myVMRecovery` no grupo de recursos de Olá designado `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Montar o disco de dados anexados Olá

> [!NOTE]
> Olá exemplos seguintes de detalhe os passos de Olá necessários numa VM com Ubuntu. Se estiver a utilizar um distro diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá localizações de ficheiros de registo e `mount` os comandos podem ser ligeiramente diferentes. Consulte a documentação do toohello para sua distro específico para alterações adequadas do Olá nos comandos.

1. Resolução de problemas de VM com as credenciais adequadas Olá tooyour SSH. Se este disco Olá primeiro dados disco ligado tooyour VM de resolução de problemas, disco de Olá, provavelmente, está ligado demasiado`/dev/sdc`. Utilize `dmseg` tooview discos ligados:

    ```bash
    dmesg | grep SCSI
    ```

    Olá de saída é semelhante toohello seguinte exemplo:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    Olá anterior exemplo, disco de SO de Olá é em `/dev/sda` e disco temporário Olá fornecido para cada VM está em `/dev/sdb`. Se tiver vários discos de dados, devem estar no `/dev/sdd`, `/dev/sde`, e assim sucessivamente.

2. Crie um diretório toomount o disco rígido virtual existente. Olá exemplo seguinte cria um diretório com o nome `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. Se tiver várias partições no seu disco rígido virtual existente, monte partição Olá necessário. Olá exemplo seguinte monta primeira partição primária Olá em `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > Melhor prática é toomount discos de dados em VMs no Azure com Olá Identificador exclusivo universalmente (UUID) do disco rígido virtual do Olá. Para este cenário de resolução de problemas curto, montagem Olá disco rígido virtual utilizando Olá UUID não é necessário. No entanto, na utilização normal, editar `/etc/fstab` toomount os discos rígidos virtuais com o nome de dispositivo em vez de pode provocar um UUID Olá VM toofail tooboot.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Resolva os problemas no disco rígido virtual original
Com Olá disco rígido virtual existente montado, agora pode efetuar qualquer manutenção e passos de resolução de problemas, conforme necessário. Assim que tiver resolvido problemas Olá, continue com Olá os seguintes passos.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Desmonte e desanexar o disco rígido virtual original
Depois dos erros serem resolvidos, desmonte e desanexar Olá existente disco virtual de VM resolução de problemas. Não é possível utilizar o disco rígido virtual com quaisquer outro VM até que a concessão de Olá anexar toohello de disco rígido virtual Olá VM de resolução de problemas é libertado.

1. De Olá tooyour sessão SSH VM de resolução de problemas, desmonte Olá existente disco virtual. Altere primeiro fora do diretório de principal de Olá do ponto de montagem:

    ```bash
    cd /
    ```

    Desmonte agora Olá existente disco virtual. Olá exemplo seguinte unmounts dispositivo Olá em `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Agora anular a exposição do disco rígido virtual Olá de Olá VM. Sair Olá SSH sessão tooyour VM de resolução de problemas. Olá lista ligado tooyour de discos de dados resolução de problemas de VM com [az vm unmanaged-lista de discos](/cli/azure/vm/unmanaged-disk#list). Olá listas Olá discos de dados de exemplo seguinte ligado toohello VM com o nome `myVMRecovery` no grupo de recursos de Olá designado `myResourceGroup`:

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    Tenha em atenção Olá o nome do seu disco rígido virtual existente. Por exemplo, o nome de Olá de um disco com Olá URI de **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** é **myVHD**. 

    Exposição do disco de dados de Olá da sua VM [az unmanaged-disco da vm desanexar](/cli/azure/vm/unmanaged-disk#detach). Olá exemplo seguinte Desanexa disco Olá chamado `myVHD` da VM com o nome de Olá `myVMRecovery` no Olá `myResourceGroup` grupo de recursos:

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a>Criar a VM de disco rígido original
toocreate uma VM a partir do seu disco rígido virtual original, utilize [este modelo Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). modelo JSON Olá está em Olá seguinte hiperligação:

- https://RAW.githubusercontent.com/Azure/Azure-QuickStart-Templates/Master/201-VM-Specialized-VHD/azuredeploy.JSON

Olá modelo implementa uma VM utilizando Olá URI de VHD de Olá comando anterior. Implementar a modelo Olá com [criar a implementação do grupo az](/cli/azure/group/deployment#create). Fornecer Olá URI tooyour original VHD e, em seguida, especifique o tipo de SO de Olá, o tamanho da VM e o nome VM da seguinte forma:

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a>Reativar o diagnóstico de arranque
Ao criar a VM de Olá existente disco virtual, diagnóstico de arranque pode não ser ativado automaticamente. Ativar o diagnóstico de arranque com [ativar o diagnóstico de arranque do vm az](/cli/azure/vm/boot-diagnostics#enable). Olá exemplo seguinte ativa a extensão de diagnóstico de Olá na VM com o nome de Olá `myDeployedVM` no grupo de recursos de Olá designado `myResourceGroup`:

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Passos seguintes
Se estiver a ter problemas em ligar tooyour VM, consulte [resolver problemas de SSH ligações tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Para problemas com a aceder a aplicações em execução numa VM, consulte [resolver problemas de conectividade de aplicação numa VM com Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
