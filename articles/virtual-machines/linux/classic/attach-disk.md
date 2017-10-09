---
title: aaaAttach tooa um disco VM com Linux no Azure | Microsoft Docs
description: "Saiba como tooattach dados de um disco tooa VM com Linux utilizando a implementação de clássico Olá modelo e inicializar disco Olá, para que fique pronta para ser utilizado"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>Como tooAttach tooa um disco de dados Máquina Virtual com Linux
> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Veja como demasiado[anexar um disco de dados com o modelo de implementação do Resource Manager Olá](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Pode anexar vazios discos e os discos que contêm dados tooyour VMs do Azure. Ambos os tipos de discos são ficheiros. vhd que residem numa conta de armazenamento do Azure. Como com a adição de qualquer máquina de Linux do disco tooa, depois de ligar o disco de Olá que precisa tooinitialize e formate-o para que fique pronta para ser utilizado. Este detalhes de artigo anexar discos vazios e discos já que contém, bem como dados tooyour VMs, como a forma como toothen inicializar e formatar um novo disco.

> [!NOTE]
> É uma melhor toouse de prática um ou mais discos toostore separam dados de uma máquina virtual. Quando cria uma máquina virtual do Azure, tem um disco de sistema operativo e um disco temporário. **Não utilize dados persistentes do Olá disco temporário toostore.** Como Olá nome indica, fornece apenas armazenamento temporário. Não oferece nenhuma cópia de segurança ou redundância porque esta não reside no armazenamento do Azure.
> disco temporário Olá é, normalmente, gerido pelo Olá agente Linux do Azure e automaticamente montado demasiado**/mnt/recursos** (ou **/mnt** nas imagens Ubuntu). No Olá por outro lado, um disco de dados pode ser denominado pelo kernel de Linux Olá algo semelhante ao seguinte `/dev/sdc`, e terá de toopartition, formatar e monte este recurso. Consulte Olá [guia de utilizador de agente do Azure Linux] [ Agent] para obter mais detalhes.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Inicializar um novo disco de dados no Linux
1. SSH tooyour VM. Para obter mais informações, consulte [como toolog tooa máquina de virtual com Linux][Logon].
2. Em seguida precisa o identificador do dispositivo Olá toofind para tooinitialize de disco de dados de Olá. Existem duas formas toodo que:
   
    a) registos de Grep para dispositivos SCSI Olá, como Olá os seguintes comandos:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Para as distribuições do Ubuntu recentes, poderá ser necessário toouse `sudo grep SCSI /var/log/syslog` porque o registo demasiado`/var/log/messages` podem estar desativados por predefinição.
   
    Pode encontrar o identificador de Olá de Olá último disco de dados que foi adicionado no mensagens hello que são apresentadas.
   
    ![Obter mensagens hello do disco](./media/attach-disk/scsidisklog.png)
   
    OU
   
    b) Olá utilize `lsscsi` toofind comando terminar o id de dispositivo Olá. `lsscsi` podem ser instaladas por um `yum install lsscsi` (no Red Hat com base distribuições) ou `apt-get install lsscsi` (no Debian com base distribuições). Pode encontrar o disco de Olá que está procurando pelo respetivo *lun* ou **número de unidade lógica**. Por exemplo, Olá *lun* para discos de Olá anexou podem ser facilmente vistos a partir de `azure vm disk list <virtual-machine>` como:

    ```azurecli
    azure vm disk list myVM
    ```

    o resultado da Olá é semelhante toohello seguinte:

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Comparar estes dados com o resultado Olá `lsscsi` para Olá mesma máquina virtual de exemplo:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    número da última Olá na cadeia de identificação de Olá em cada linha é Olá *lun*. Consulte `man lsscsi` para obter mais informações.
3. Na linha de Olá, escreva, por exemplo, o dispositivo Olá toocreate de comando a seguir:
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. Quando lhe for pedido, escreva  **n**  toocreate uma partição.

    ![Criar dispositivo](./media/attach-disk/fdisknewpartition.png)

5. Quando lhe for pedido, escreva **p** partição primária do toomake Olá partição Olá. Tipo **1** toomake Olá primeira partição e, em seguida, escreva introduza o valor do tooaccept Olá predefinido para cilindro Olá. Em alguns sistemas, pode mostrar os valores predefinidos de Olá de Olá primeiro e Olá último setores, em vez de cilindro Olá. Pode escolher tooaccept estas predefinições.

    ![Criar a partição](./media/attach-disk/fdisknewpartdetails.png)


6. Tipo **p** toosee Olá detalhes disco Olá que está a ser particionado.

    ![Informações do disco de lista](./media/attach-disk/fdiskpartitiondetails.png)


7. Tipo **w** definições de Olá toowrite para disco Olá.

    ![Escrever Olá alterações de disco](./media/attach-disk/fdiskwritedisk.png)

8. Agora pode criar o sistema de ficheiros de Olá na partição Olá de novo. Acrescentar Olá partição número toohello ID do dispositivo (no seguinte exemplo de Olá `/dev/sdc1`). Olá exemplo seguinte cria uma partição ext4 no /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Criar o sistema de ficheiros](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > Sistemas SuSE Linux Enterprise 11 só suportam acesso só de leitura ext4 sistemas de ficheiros. Para estes sistemas, recomenda-se tooformat Olá novo sistema de ficheiros como ext3 em vez de ext4.

9. Efetue um diretório toomount Olá novo sistema de ficheiros, da seguinte forma:
   
    ```bash
    sudo mkdir /datadrive
    ```

10. Por fim, pode montar unidade Olá, da seguinte forma:
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    disco de dados de Olá está agora pronto toouse como **/datadrive**.
   
    ![Criar disco de Olá de diretório e montagem Olá](./media/attach-disk/mkdirandmount.png)

11. Adicione Olá nova unidade demasiado/etc/fstab:
   
    unidade de Olá tooensure é remontadas da automaticamente depois de reiniciar o computador tem de ser adicionado toohello /etc/fstab ficheiro. Além disso, recomenda-se vivamente que Olá UUID (universalmente Unique IDentifier) é utilizada na unidade de toohello /etc/fstab toorefer em vez de apenas Olá nome do dispositivo (ou seja, /dev/sdc1). Utilizar Olá UUID evita a ser montado tooa fornecido localização se Olá SO Deteta um erro de disco durante o arranque e de quaisquer discos de dados restantes, em seguida, que está a ser atribuído aos IDs de dispositivo de disco incorreta Olá. toofind Olá UUID da nova unidade de Olá, pode utilizar Olá **blkid** utilitário:
   
    ```bash
    sudo -i blkid
    ```
   
    saída de Olá procura toohello semelhante seguinte exemplo:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Editar incorretamente Olá **etc/fstab** ficheiros poderia resultar num sistema de arranque. Se não souber, consulte a documentação da distribuição toohello para obter informações sobre como tooproperly editar este ficheiro. Também é recomendável que uma cópia de segurança do ficheiro de /etc/fstab Olá foi criada antes de editar.

    Em seguida, abra Olá **etc/fstab** ficheiro num editor de texto:

    ```bash
    sudo vi /etc/fstab
    ```

    Neste exemplo, vamos utilizar Olá UUID valor para Olá novo **/dev/sdc1** dispositivo que foi criado nos passos anteriores Olá e Olá pontodemontagem **/datadrive**. Adicionar Olá seguir final toohello linha Olá **etc/fstab** ficheiro:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    Ou, em sistemas com base no SuSE Linux poderá ser necessário toouse formato ligeiramente diferente:

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Olá `nofail` opção garante que Olá VM entrar, mesmo se o sistema de ficheiros de Olá está danificado ou disco Olá não existe no momento do arranque. Sem esta opção, pode encontrar o comportamento, conforme descrito em [não é possível SSH tooLinux VM devido a erros de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    Pode agora testar que o sistema de ficheiros de Olá está montado corretamente pela desmontagem e remontar, em seguida, o sistema de ficheiros hello, ou seja, utilizando o ponto de montagem de exemplo de Olá `/datadrive` criado no Olá anteriormente os passos:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Se hello `mount` comando produz erro, verifique Olá ficheiro etc/fstab para a sintaxe correta. Se as unidades de dados adicionais ou partições são criadas, introduzi-las em etc/fstab separadamente bem.

    Faz com que Olá unidade gravável utilizando este comando:

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Posteriormente, remover um disco de dados sem necessitar de editar fstab causam Olá VM toofail tooboot. Se se tratar de uma ocorrência comum, a maioria das distribuições fornecem o Olá `nofail` e/ou `nobootwait` fstab opções que permitem uma tooboot de sistema, mesmo que o disco de Olá falha toomount no momento do arranque. Consulte a documentação de sua distribuição para obter mais informações sobre estes parâmetros.

### <a name="trimunmap-support-for-linux-in-azure"></a>Suporte de cortar/UNMAP para Linux no Azure
Alguns kernels Linux suportam toodiscard de operações de cortar/UNMAP blocos não utilizados no disco Olá. Estas operações são principalmente útil para armazenamento standard tooinform Azure eliminado páginas já não são válidos e pode ser eliminada. Rejeitar páginas pode guardar o custo, se criar ficheiros grandes e, em seguida, elimine-os.

Existem duas formas tooenable cortar suportar na sua VM com Linux. Normalmente, consulte a distribuição para Olá abordagem recomendada:

* Olá utilize `discard` montar opção na `/etc/fstab`, por exemplo:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* Em alguns Olá casos `discard` opção pode ter implicações de desempenho. Em alternativa, pode executar Olá `fstrim` comando manualmente a partir da linha de comandos hello, ou adicione-tooyour crontab toorun regularmente:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Resolução de problemas
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Passos Seguintes
Pode ler mais sobre como utilizar a VM com Linux no Olá seguintes artigos:

* [Como toolog tooa máquina de virtual com Linux][Logon]
* [Como toodetach um disco de uma máquina virtual Linux](detach-disk.md)
* [Utilizar Olá CLI do Azure com o modelo de implementação clássica Olá](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Configurar o RAID numa VM com Linux no Azure](../configure-raid.md)
* [Configurar LVM numa VM com Linux no Azure](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
