---
title: "aaaUse uma VM de resolução de problemas no portal do Azure de Olá do Linux | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas da máquina virtual Linux utilizando a ligação Olá SO disco tooa recuperação VM Olá portal do Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Resolver problemas de uma VM com Linux ao anexar a VM de recuperação Olá SO disco tooa utilizando Olá portal do Azure
Se a máquina virtual (VM) do Linux encontra um erro de arranque ou de disco, poderá ser necessário tooperform passos no disco rígido virtual Olá próprio de resolução de problemas. Um exemplo comum é uma entrada inválida no `/etc/fstab` Olá VM que impede de ser capaz de tooboot com êxito. Detalhes deste artigo como toouse Olá tooconnect portal do Azure a virtual rígido disco tooanother VM com Linux toofix quaisquer erros, em seguida, voltar a criar a VM original.

## <a name="recovery-process-overview"></a>Descrição geral do processo de recuperação
Olá, processo de resolução de problemas é o seguinte:

1. Elimine Olá VM encontrar problemas, mantendo Olá os discos rígidos virtuais.
2. Anexe e montar o disco rígido virtual de Olá tooanother VM com Linux para fins de resolução de problemas.
3. Ligar toohello VM de resolução de problemas. Editar ficheiros ou executar quaisquer ferramentas toofix problemas no Olá original disco virtual.
4. Desmonte e desanexar o disco rígido virtual Olá de Olá VM de resolução de problemas.
5. Crie uma VM utilizando Olá original disco virtual.


## <a name="determine-boot-issues"></a>Determinar os problemas de arranque
Examine o diagnóstico de arranque Olá e toodetermine de captura de ecrã VM por que razão a VM não é possível tooboot corretamente. Um exemplo comum é uma entrada inválida no `/etc/fstab`, ou um subjacente disco de rígido virtual que está a ser eliminado ou movido.

Selecione a VM no portal de Olá e, em seguida, desloque para baixo toohello **suporte + resolução de problemas** secção. Clique em **diagnóstico de arranque** mensagens de consola tooview hello transmissão em fluxo da VM. Consola de Olá revisão regista toosee se pode determinar o motivo pelo qual hello VM verificou um problema. Olá exemplo seguinte mostra que uma VM bloqueada no modo de manutenção que necessite de interação manual:

![Visualizar VM diagnóstico de arranque consola registos](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

Também pode clicar em **captura de ecrã** em Olá parte superior do Olá arranque diagnóstico registo toodownload uma captura de captura de ecrã do Olá VM.


## <a name="view-existing-virtual-hard-disk-details"></a>Ver detalhes de disco rígido virtual existente
Antes de pode anexar o disco rígido virtual de tooanother VM, terá de nome de Olá tooidentify de Olá de disco rígido virtual (VHD). 

Selecione o grupo de recursos a partir do portal de Olá, em seguida, selecione a sua conta de armazenamento. Clique em **Blobs**, como no seguinte exemplo de Olá:

![Selecione os blobs de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

Normalmente, tem um contentor com o nome **vhds** que armazena os discos rígidos virtuais. Selecione o contentor de Olá tooview uma lista de discos rígidos virtuais. Nome de Olá nota do seu VHD (prefixo Olá é normalmente nome Olá da sua VM):

![Identificar o VHD no contentor de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Selecione o disco rígido virtual existente na lista de Olá e copie o URL de Olá para utilização no Olá os seguintes passos:

![Copie o URL de disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>Eliminar VM existente
Os discos rígidos virtuais e as VMs são dois recursos diferentes do Azure. Um disco rígido virtual é onde são armazenadas Olá sistema operativo, as aplicações e configurações. Olá própria VM é apenas metadados, que definem o tamanho de Olá ou localização e referencia recursos, tais como um disco rígido virtual ou o cartão de interface de rede virtual (NIC). Cada disco rígido virtual tem uma concessão atribuída quando ligado tooa VM. Embora os discos de dados podem ser ligados e anular a exposição mesmo enquanto Olá VM está em execução, o disco do SO Olá não pode ser desligado, a menos que Olá recurso VM é eliminado. concessão de Olá continua disco de SO de Olá tooassociate com uma VM, mesmo quando se encontra num estado parado e desalocado essa VM.

Olá primeiro passo toorecover a VM é o recurso VM de Olá toodelete próprio. A eliminar Olá VM deixa Olá os discos rígidos virtuais na sua conta de armazenamento. Depois de Olá que VM é eliminada, anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolva os erros de Olá.

Selecione a VM no portal de Olá, em seguida, clique em **eliminar**:

![VM arranque diagnóstico captura de ecrã com erro de arranque](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Aguarde até que Olá VM terminou a eliminação antes de anexar o disco rígido virtual de Olá tooanother VM. tem de concessão de Olá no disco rígido virtual Olá que associa-Olá VM toobe lançada antes de pode anexar o disco rígido virtual de Olá tooanother VM.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Anexar tooanother de disco rígido virtual existente VM
Para Olá, em seguida alguns passos, utilizar outra VM para fins de resolução de problemas. Anexar Olá toothis do disco rígido virtual existente VM toobe capaz de toobrowse de resolução de problemas e editar o conteúdo do disco Olá. Este processo permite-lhe toocorrect quaisquer erros de configuração ou a aplicação adicional de revisão ou o sistema de ficheiros de registo por exemplo. Escolha ou crie outro toouse VM para fins de resolução de problemas.

1. Selecione o grupo de recursos a partir do portal de Olá, em seguida, selecione a VM de resolução de problemas. Selecione **discos** e, em seguida, clique em **anexar existente**:

    ![Anexar o disco existente no portal de Olá](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect o disco rígido virtual existente, clique em **ficheiro VHD**:

    ![Procurar o VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. Selecionar a sua conta do storage e um contentor, em seguida, clique o VHD existente. Clique em Olá **selecione** botão tooconfirm à sua escolha:

    ![Selecionar o seu VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. Com o VHD selecionado agora, clique em **OK** tooattach Olá disco rígido virtual existente:

    ![Confirme a anexar o disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. Após alguns segundos, Olá **discos** painel para a VM lista o disco rígido virtual ligado como um disco de dados:

    ![Disco rígido virtual já existente anexado como disco de dados](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Montar o disco de dados anexados Olá

> [!NOTE]
> Olá exemplos seguintes de detalhe os passos de Olá necessários numa VM com Ubuntu. Se estiver a utilizar um distro diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá localizações de ficheiros de registo e `mount` os comandos podem ser ligeiramente diferentes. Consulte a documentação do toohello para sua distro específico para alterações adequadas do Olá nos comandos.

1. Resolução de problemas de VM com as credenciais adequadas Olá tooyour SSH. Se este disco Olá primeiro dados disco ligado tooyour VM de resolução de problemas, provavelmente, está a ligado demasiado`/dev/sdc`. Utilize `dmseg` toolist discos ligados:

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
Depois dos erros serem resolvidos, desligue o disco rígido virtual existente por Olá da sua VM de resolução de problemas. Não é possível utilizar o disco rígido virtual com quaisquer outro VM até que a concessão de Olá anexar toohello de disco rígido virtual Olá VM de resolução de problemas é libertado.

1. De Olá tooyour sessão SSH VM de resolução de problemas, desmonte Olá existente disco virtual. Altere primeiro fora do diretório de principal de Olá do ponto de montagem:

    ```bash
    cd /
    ```

    Desmonte agora Olá existente disco virtual. Olá exemplo seguinte unmounts dispositivo Olá em `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Agora anular a exposição do disco rígido virtual Olá de Olá VM. Selecione a VM no portal de Olá e clique em **discos**. Selecione o disco rígido virtual existente e, em seguida, clique em **anulação de exposições**:

    ![Exposição do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Aguarde até que Olá VM tem exposição anulada com êxito o disco de dados de Olá antes de continuar.

## <a name="create-vm-from-original-hard-disk"></a>Criar a VM de disco rígido original
toocreate uma VM a partir do seu disco rígido virtual original, utilize [este modelo Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). modelo de Olá implementa uma VM numa rede virtual existente, utilizando Olá URL de VHD de Olá comando anterior. Clique em Olá **implementar tooAzure** botão da seguinte forma:

![Implementar a VM a partir do modelo a partir do GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

modelo de Olá está carregado Olá portal do Azure para a implementação. Introduza os nomes de Olá para a sua nova VM e os recursos do Azure existentes e cole Olá URL tooyour disco rígido virtual existente. implementação de Olá toobegin, clique em **Compra**:

![Implementar a VM a partir do modelo](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Reativar o diagnóstico de arranque
Ao criar a VM de Olá existente disco virtual, diagnóstico de arranque pode não ser ativado automaticamente. toocheck Olá estado de diagnóstico de arranque e ative se for necessário, selecione a VM no portal de Olá. Em **monitorização**, clique em **as definições de diagnóstico**. Certifique-se de estado de Olá **no**, e Olá marca de verificação junto demasiado**diagnóstico de arranque** está selecionada. Se efetuar alterações, clique em **guardar**:

![Atualizar as definições de diagnóstico de arranque](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Passos seguintes
Se estiver a ter problemas em ligar tooyour VM, consulte [resolver problemas de SSH ligações tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Para problemas com a aceder a aplicações em execução numa VM, consulte [resolver problemas de conectividade de aplicação numa VM com Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Para obter mais informações sobre como utilizar o Gestor de recursos, consulte [descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
