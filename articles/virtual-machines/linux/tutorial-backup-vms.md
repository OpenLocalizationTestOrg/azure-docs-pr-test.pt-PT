---
title: "Cópia de segurança de VMs com Linux do Azure | Microsoft Docs"
description: "Proteger as VMs com Linux através de cópias de segurança utilizando a cópia de segurança do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Cópia de segurança de computadores virtuais Linux no Azure

Pode criar cópias de segurança em intervalos regulares para manter os seus dados protegidos. Cópia de segurança do Azure cria pontos de recuperação que estão armazenados no cofres de recuperação com redundância geográfica. Quando restaurar a partir de um ponto de recuperação, pode restaurar Olá VM todo ou ficheiros apenas específicos. Este artigo explica como toorestore um único ficheiro tooa nginx em execução de VM com Linux. Se ainda não tiver um toouse VM, pode criar um utilizando Olá [início rápido do Linux](quick-create-cli.md). Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Criar uma cópia de segurança de uma VM
> * Agendar uma cópia de segurança diária
> * Restaurar um ficheiro a partir de uma cópia de segurança



## <a name="backup-overview"></a>Descrição geral da Cópia de Segurança

Quando Olá serviço cópia de segurança do Azure inicia uma cópia de segurança, aciona tootake de extensão de cópia de segurança de Olá um instantâneo de ponto no tempo. Olá serviço de cópia de segurança do Azure utiliza Olá _VMSnapshotLinux_ extensão no Linux. extensão de Olá é instalado durante a cópia de segurança Olá primeira VM se Olá VM está em execução. Se hello VM não está em execução, Olá serviço de cópia de segurança tira um instantâneo de Olá subjacente armazenamento (uma vez que não existem escritas de aplicação ocorrerem ao hello que VM está parada).

Por predefinição, cópia de segurança do Azure assume uma sistema consistente cópia de segurança para a VM com Linux, mas pode ser configurado tootake [aplicação cópia de segurança consistente utilizando o pré- script de e script pós-implementação framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Depois de Olá serviço de cópia de segurança do Azure tira instantâneos Olá, dados de Olá são transferidos toohello cofre. eficiência toomaximize, o serviço de Olá identifica e transfere apenas os blocos de Olá dos dados que foram alterados desde a cópia de segurança anterior Olá.

Quando a transferência de dados de Olá estiver concluída, o instantâneo de Olá é removido e é criado um ponto de recuperação.


## <a name="create-a-backup"></a>Criar uma cópia de segurança
Crie uma simple agendada diária cópia de segurança tooa cofre dos serviços de recuperação. 

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. No menu de Olá Olá esquerda, selecione **máquinas virtuais**. 
3. Na lista de Olá, selecione uma VM tooback cópias de segurança.
4. No painel VM Olá, no Olá **definições** secção, clique em **cópia de segurança**. Olá **ativar cópia de segurança** abre o painel.
5. No **cofre dos serviços de recuperação**, clique em **criar nova** e forneça o nome de Olá para novo cofre de Olá. Um novo cofre é criado na Olá mesmo grupo de recursos e localização da máquina virtual de Olá.
6. Clique em **política de cópia de segurança**. Neste exemplo, mantenha as predefinições de Olá e clique em **OK**.
7. No Olá **ativar cópia de segurança** painel, clique em **ativar a cópia de segurança**. Esta ação cria uma cópia de segurança diária, com base numa agenda predefinida de Olá.
10. toocreate um ponto de recuperação inicial, no Olá **cópia de segurança** painel clique **cópia de segurança agora**.
11. No Olá **cópia de segurança agora** painel, clique em ícone de calendário Olá, utilize Olá de tooselect de controlo do Olá calendário último dia deste ponto de recuperação é mantido e clique em **cópia de segurança**.
12. No Olá **cópia de segurança** painel para a VM, irá ver o número de Olá de pontos de recuperação que estão concluídos.

    ![Pontos de recuperação](./media/tutorial-backup-vms/backup-complete.png)

primeira cópia de segurança Olá demora cerca de 20 minutos. Continuar a parte seguinte do toohello deste tutorial depois de concluída a cópia de segurança.

## <a name="restore-a-file"></a>Restaurar um ficheiro

Se acidentalmente eliminar ou se o ficheiro de tooa de alterações, pode utilizar o ficheiro de Olá toorecover de recuperação de ficheiros do seu Cofre de cópia de segurança. Recuperação de ficheiros utiliza um script que é executado no Olá VM, ponto de recuperação de Olá toomount como unidade local. Estas unidades permanecerá montadas para 12 horas para que possa copiar os ficheiros do ponto de recuperação Olá e restaurá-las toohello VM.  

Neste exemplo, mostramos como toorecover Olá predefinido nginx página web /var/www/html/index.nginx-debian.html. endereço IP público de Olá do nosso VM neste exemplo é *13.69.75.209*. Pode encontrar o endereço IP Olá da sua utilização de vm:

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. No computador local, abra um browser e o tipo de endereço IP público Olá da VM toosee Olá predefinido nginx página web.

    ![Nginx predefinido de página web](./media/tutorial-backup-vms/nginx-working.png)

1. SSH para a VM.

    ```bash
    ssh 13.69.75.209
    ```
2. Elimine /var/www/html/index.nginx-debian.html.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. No computador local, atualize o browser de Olá por atingir CTRL + F5 toosee que nginx página predefinida é removido.

    ![Nginx predefinido de página web](./media/tutorial-backup-vms/nginx-broken.png)
    
1. No seu computador local, inicie sessão toohello [portal do Azure](https://portal.azure.com/).
6. No menu de Olá Olá esquerda, selecione **máquinas virtuais**. 
7. Na lista de Olá, selecione Olá VM.
8. No painel VM Olá, no Olá **definições** secção, clique em **cópia de segurança**. Olá **cópia de segurança** abre o painel. 
9. No menu de Olá, Olá parte superior do painel de Olá, selecione **recuperação de ficheiros**. Olá **recuperação de ficheiros** abre o painel.
10. No **passo 1: selecione o ponto de recuperação**, selecione um ponto de recuperação da Olá lista pendente.
11. No **passo 2: Transferir o script toobrowse e recuperar ficheiros**, clique em Olá **transferir executável** botão. Guarde o computador local do Olá ficheiro transferido tooyour.
7. Clique em **transferir o script** toodownload Olá ficheiro de script do localmente.
8. Abra um Bash linha de comandos e escreva Olá a seguir, substituindo *Linux_myVM_05-05-2017.sh* com Olá corrija o caminho e nome de ficheiro de script de Olá que transferiu, *azureuser* com o nome de utilizador de Olá para Olá VM e *13.69.75.209* com endereço IP público Olá para a VM.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. No seu computador local, abra uma toohello de ligação SSH VM.

    ```bash
    ssh 13.69.75.209
    ```
    
10. Na sua VM, adicione executar o ficheiro de script de toohello de permissões.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. Na VM a executar o ponto de recuperação do Olá script toomount Olá como um sistema de ficheiros.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. Olá o resultado da Olá script fornecem que Olá caminho para o ponto de montagem Olá. saída de Olá procura toothis semelhante:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. Na sua VM, copie Olá nginx predefinido de página web do Olá ponto de montagem toowhere back-lhe eliminar ficheiro Olá.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. No computador local, abra o separador do browser Olá qual estão ligados toohello o endereço IP do Olá VM que mostra Olá nginx predefinido de página. Prima CTRL + F5 página de browser de Olá toorefresh. Deverá ver que Olá página predefinida está a funcionar novamente.

    ![Nginx predefinido de página web](./media/tutorial-backup-vms/nginx-working.png)

18. No computador local, volte atrás toohello separador do browser para Olá portal do Azure e no **passo 3: desmonte discos Olá após a recuperação** clique Olá **desmonte discos** botão. Caso se esqueça toodo neste passo, Olá ligação toohello pontodemontagem é fechar automaticamente após 12 horas. Depois dessas 12 horas, terá de toodownload um toocreate script novo pontodemontagem uma novo.


## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Criar uma cópia de segurança de uma VM
> * Agendar uma cópia de segurança diária
> * Restaurar um ficheiro a partir de uma cópia de segurança

Produzir toohello seguinte toolearn tutorial sobre a monitorização de máquinas virtuais.

> [!div class="nextstepaction"]
> [Monitorizar máquinas virtuais](tutorial-monitoring.md)

