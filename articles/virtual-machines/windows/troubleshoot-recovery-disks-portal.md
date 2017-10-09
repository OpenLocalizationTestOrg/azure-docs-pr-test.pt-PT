---
title: "aaaUse um Windows VM de resolução de problemas no Olá portal do Azure | Microsoft Docs"
description: "Saiba como tootroubleshoot Windows problemas da máquina virtual no Azure utilizando a ligação Olá SO disco tooa recuperação VM Olá portal do Azure"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Resolver problemas de uma VM do Windows ao anexar a VM de recuperação Olá SO disco tooa utilizando Olá portal do Azure
Se a máquina virtual (VM) do Windows no Azure encontra um erro de arranque ou de disco, poderá ser necessário tooperform passos no disco rígido virtual Olá próprio de resolução de problemas. Um exemplo comum seria uma atualização da aplicação com falhas que impede que Olá VM que está a ser capaz de tooboot com êxito. Detalhes deste artigo como toouse Olá tooconnect portal do Azure a virtual rígido disco tooanother VM do Windows toofix quaisquer erros, em seguida, voltar a criar a VM original.

## <a name="recovery-process-overview"></a>Descrição geral do processo de recuperação
Olá, processo de resolução de problemas é o seguinte:

1. Elimine Olá VM encontrar problemas, mantendo Olá os discos rígidos virtuais.
2. Anexe e montar o disco rígido virtual de Olá tooanother VM do Windows para fins de resolução de problemas.
3. Ligar toohello VM de resolução de problemas. Editar ficheiros ou executar quaisquer ferramentas toofix problemas no Olá original disco virtual.
4. Desmonte e desanexar o disco rígido virtual Olá de Olá VM de resolução de problemas.
5. Crie uma VM utilizando Olá original disco virtual.


## <a name="determine-boot-issues"></a>Determinar os problemas de arranque
toodetermine motivo pelo qual a VM não é capaz de tooboot corretamente, examine o diagnóstico de arranque de Olá captura de ecrã da VM. Um exemplo comum teria de ser uma atualização da aplicação que falhou, ou um subjacente disco de rígido virtual que está a ser eliminado ou movido.

Selecione a VM no portal de Olá e, em seguida, desloque para baixo toohello **suporte + resolução de problemas** secção. Clique em **diagnóstico de arranque** captura de ecrã do tooview Olá. Tenha em atenção quaisquer mensagens de erro específicas ou códigos de erro toohelp determinar por que motivo Olá VM verificou um problema. Olá exemplo seguinte mostra uma VM aguardar a resposta de parar os serviços:

![Visualizar VM diagnóstico de arranque consola registos](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

Também pode clicar em **captura de ecrã** toodownload uma captura de captura de ecrã do Olá VM.


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

1. Abra um tooyour de ligação de ambiente de trabalho remoto VM. Selecione a VM no portal de Olá e clique em **Connect**. Transfira e abra o ficheiro de ligação de RDP Olá. Introduza o toolog de credenciais em tooyour VM da seguinte forma:

    ![Inicie sessão no tooyour VM utilizando o ambiente de trabalho remoto](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. Abra **Gestor de servidor**, em seguida, selecione **File and Storage Services**. 

    ![Selecione o ficheiro e serviços de armazenamento no Gestor de servidor](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. disco de dados de Olá é automaticamente detetado e ligado. os discos, selecione de ligados toosee uma lista de Olá **discos**. Pode selecionar as informações de volume de tooview da disco de dados, incluindo a letra de unidade de Olá. Olá seguinte exemplo mostra Olá disco de dados ligado e utilizar **f:**:

    ![Disco ligado e informações de volume no Gestor de servidor](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Resolva os problemas no disco rígido virtual original
Com Olá disco rígido virtual existente montado, agora pode efetuar qualquer manutenção e passos de resolução de problemas, conforme necessário. Assim que tiver resolvido problemas Olá, continue com Olá os seguintes passos.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Desmonte e desanexar o disco rígido virtual original
Depois dos erros serem resolvidos, desligue o disco rígido virtual existente por Olá da sua VM de resolução de problemas. Não é possível utilizar o disco rígido virtual com quaisquer outro VM até que a concessão de Olá anexar toohello de disco rígido virtual Olá VM de resolução de problemas é libertado.

1. A partir do Olá RDP sessão tooyour VM, abra **Gestor de servidor**, em seguida, selecione **File and Storage Services**:

    ![Selecione o ficheiro e serviços de armazenamento no Gestor de servidor](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. Selecione **discos** e, em seguida, selecione o disco de dados. Faça duplo clique no seu disco de dados e selecione **Colocar Offline**:

    ![Definir o disco de dados de Olá como offline no Gestor de servidor](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. Agora anular a exposição do disco rígido virtual Olá de Olá VM. Selecione a VM no Olá portal do Azure e clique em **discos**. Selecione o disco rígido virtual existente e, em seguida, clique em **anulação de exposições**:

    ![Exposição do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Aguarde até que Olá VM tem exposição anulada com êxito o disco de dados de Olá antes de continuar.

## <a name="create-vm-from-original-hard-disk"></a>Criar a VM de disco rígido original
toocreate uma VM a partir do seu disco rígido virtual original, utilize [este modelo Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). modelo de Olá implementa uma VM numa rede virtual existente, utilizando Olá URL de VHD de Olá comando anterior. Clique em Olá **implementar tooAzure** botão da seguinte forma:

![Implementar a VM a partir do modelo a partir do Github](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

modelo de Olá está carregado Olá portal do Azure para a implementação. Introduza os nomes de Olá para a sua nova VM e os recursos do Azure existentes e cole Olá URL tooyour disco rígido virtual existente. implementação de Olá toobegin, clique em **Compra**:

![Implementar a VM a partir do modelo](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Reativar o diagnóstico de arranque
Ao criar a VM de Olá existente disco virtual, diagnóstico de arranque pode não ser ativado automaticamente. toocheck Olá estado de diagnóstico de arranque e ative se for necessário, selecione a VM no portal de Olá. Em **monitorização**, clique em **as definições de diagnóstico**. Certifique-se de estado de Olá **no**, e Olá marca de verificação junto demasiado**diagnóstico de arranque** está selecionada. Se efetuar alterações, clique em **guardar**:

![Atualizar as definições de diagnóstico de arranque](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Passos seguintes
Se estiver a ter problemas em ligar tooyour VM, consulte [RDP de resolução de problemas de ligações tooan VM do Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para problemas com a aceder a aplicações em execução numa VM, consulte [resolver problemas de conectividade de aplicação numa Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para obter mais informações sobre como utilizar o Gestor de recursos, consulte [descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).