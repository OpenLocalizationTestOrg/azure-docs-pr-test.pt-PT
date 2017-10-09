---
title: "Cópia de segurança do Azure: Tooa de restauro do Estado do sistema do Windows Server | Microsoft Docs"
description: "Passo por explicação passo para restaurar o estado do sistema do Windows Server a partir de uma cópia de segurança no Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>Restaurar estado do sistema tooWindows servidor

Este artigo explica como toorestore cópias de segurança de estado do sistema do Windows Server um serviços de recuperação do Azure do cofre. toorestore estado do sistema, tem de ter uma cópia de segurança do Estado do sistema (criadas com instruções Olá [cópia de segurança do Estado do sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) e certifique-se de que instalou Olá [versão mais recente do Olá recuperação do Microsoft Azure Agente de serviços (MARS)](http://aka.ms/azurebackup_agent). Recuperar dados de estado do sistema do Windows Server a partir de um cofre dos serviços de recuperação do Azure é um processo de dois passos:

1. Restaure estado do sistema como ficheiros de cópia de segurança do Azure. Ao restaurar o estado do sistema de ficheiros de cópia de segurança do Azure, pode:
  * Restaurar estado do sistema toohello mesmo servidor em que foram executadas cópias de segurança hello, ou
  * Restaurar estado do sistema tooan alternativo servidor de ficheiros.

2. Aplica Olá restaurada estado do sistema ficheiros tooa do Windows Server.


## <a name="recover-system-state-files-toohello-same-server"></a>Estado do sistema de recuperar ficheiros toohello mesmo servidor
Olá, os passos seguintes explica como tooroll fazer uma cópia do estado anterior do Windows Server configuração tooa. A anular o servidor de configuração tooa back conhecida, estado estável, pode ser extremamente valiosa. Olá seguintes estado do sistema do servidor de passos, restauro Olá de um cofre dos serviços de recuperação. 

1. Abra Olá **cópia de segurança do Microsoft Azure** snap-in. Se não souber qual o snap-in do Olá foi instalado, pesquisar computador Olá ou um servidor para **cópia de segurança do Microsoft Azure**.

    aplicação de ambiente de trabalho Olá deve aparecer nos resultados de pesquisa de Olá.

2. Clique em **recuperar dados** Assistente de Olá toostart.

    ![Recuperar dados](./media/backup-azure-restore-windows-server/recover.png)

3. No Olá **introdução** painel, toorestore Olá dados toohello mesmo servidor ou computador, selecione **neste servidor (`<server name>`)** e clique em **seguinte**.

    ![Escolha esta toohello de dados do servidor opção toorestore Olá mesma máquina](./media/backup-azure-restore-system-state/samemachine.png)

4. No Olá **selecionar modo de recuperação** painel, escolha **estado do sistema** e, em seguida, clique em **seguinte**.

    ![Procurar ficheiros](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. No calendário Olá no **data e selecione o Volume** painel, selecione uma recuperação do ponto. 

    Pode restaurar a partir de qualquer ponto de recuperação no tempo. As datas em **negrito** indicar disponibilidade Olá de, pelo menos, um ponto de recuperação. Depois de selecionar uma data, se não estiverem disponíveis vários pontos de recuperação, escolha o ponto de recuperação específico Olá de Olá **tempo** menu pendente.

    ![Data e de volume](./media/backup-azure-restore-system-state/select-date.png)

6. Assim que tiver optado por toorestore de ponto de recuperação Olá, clique em **seguinte**.

    Cópia de segurança do Azure monta o ponto de recuperação do local de Olá e utiliza-o como um volume de recuperação.

7. No painel seguinte da Olá, especifique o destino de Olá para Olá recuperar ficheiros de estado do sistema e clique em **procurar** tooopen Explorador do Windows e localizar Olá ficheiros e pastas que pretende. Olá opção, **criar cópias de modo a que ambas as versões**, cria cópias dos ficheiros individuais num arquivo de ficheiros de estado do sistema existente em vez de criar a cópia de Olá do arquivo de estado do sistema completo Olá.

    ![Opções de recuperação](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Verifique os detalhes de Olá de recuperação no Olá **confirmação** painel e clique em **recuperar**.

   ![Clique em ação de recuperação do recuperar tooacknowledge Olá](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Olá cópia *WindowsImageBackup* diretório no Olá volume não críticas do tooa de destino de recuperação do servidor de Olá. Normalmente, Olá volume de sistema operativo Windows é o volume crítico Olá.

10. Assim que a recuperação de Olá for bem sucedida, siga os passos de Olá na secção de Olá, [aplicar restaurada toohello de ficheiros de estado do sistema do Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete Olá processo de recuperação do Estado do sistema.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Servidor do Estado do sistema de recuperar ficheiros tooan alternativo

Se o servidor do Windows está danificada ou estiver inacessível e pretender toorestore-tooa estado estável por recuperar Olá estado do sistema do Windows Server, pode restaurar estado do sistema do servidor Olá danificada a partir de outro servidor. Utilize Olá os seguintes passos toohello restaurar estado do sistema num servidor separado.  

terminologia de Olá utilizada estes passos incluem:

- *Máquina de origem* – máquina original Olá a partir de cópia de segurança que Olá foi executada e que não está atualmente disponível.
- *A máquina de destino* – dados de Olá Olá máquina toowhich está a ser recuperados.
- *Cofre do exemplo* – Olá do Olá dos serviços de recuperação cofre toowhich *máquina de origem* e *máquina de destino* estão registados. <br/>

> [!NOTE]
> As cópias de segurança obtidas a partir de uma máquina não podem ser máquina tooa restaurados com uma versão anterior do sistema de operativo Olá. Por exemplo, as cópias de segurança obtidas a partir da máquina não pode ser um Windows Server 2016 restaurada tooWindows Server 2012 R2. No entanto, inverso Olá é possível. Pode utilizar cópias de segurança do Windows Server 2012 R2 toorestore Windows Server 2016.
>

1. Abra Olá **cópia de segurança do Microsoft Azure** snap-in no Olá *máquina de destino*.
2. Certifique-se de que Olá *máquina de destino* e Olá *máquina de origem* são registado toohello dos serviços de recuperação mesmo cofre.
3. Clique em **recuperar dados** o fluxo de trabalho do tooinitiate Olá.

    ![Recuperar dados](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Selecione **outro servidor**

    ![Outro servidor](./media/backup-azure-restore-system-state/anotherserver.png)

5. Forneça o ficheiro de credenciais de cofre Olá corresponde toohello *Cofre de exemplo*. Se o ficheiro de credenciais do cofre Olá (expirou ou era inválida), transfira um novo ficheiro de credenciais do Cofre de Olá *Cofre de exemplo* no Olá portal do Azure. Depois do ficheiro de credenciais do cofre Olá for fornecido, é apresentado o Cofre de serviços de recuperação de Olá associada ao ficheiro de credenciais de cofre Olá.

6. No painel de selecionar o servidor de cópia de segurança de Olá, selecione Olá *máquina de origem* da lista de Olá máquinas apresentados.

    ![Lista de máquinas](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. No painel de selecionar o modo de recuperação Olá, escolha **estado do sistema** e clique em **seguinte**. 

    ![Pesquisa](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. No Olá calendário no Olá **data e selecione o Volume** painel, selecione uma recuperação do ponto. Pode restaurar a partir de qualquer ponto de recuperação no tempo. As datas em **negrito** indicar disponibilidade Olá de, pelo menos, um ponto de recuperação. Depois de selecionar uma data, se não estiverem disponíveis vários pontos de recuperação, escolha o ponto de recuperação específico Olá de Olá **tempo** menu pendente. 

    ![Itens de procura](./media/backup-azure-restore-system-state/select-date.png)

9. Assim que tiver optado por toorestore de ponto de recuperação Olá, clique em **seguinte**.

10. No Olá **selecionar modo de recuperação de estado de sistema** painel, especifique onde pretende toobe recuperar ficheiros de estado do sistema de destino de Olá, em seguida, clique em **seguinte**.

    ![Encriptação](./media/backup-azure-restore-system-state/recover-as-files.png)

    Olá opção, **criar cópias de modo a que ambas as versões**, cria cópias dos ficheiros individuais num arquivo de ficheiros de estado do sistema existente em vez de criar a cópia de Olá do arquivo de estado do sistema completo Olá.

11. Verifique os detalhes de Olá de recuperação no painel de confirmação de Olá e clique em **recuperar**. 

    ![Clique em processo de recuperação de Olá botão tooconfirm Olá recuperar](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Olá cópia *WindowsImageBackup* volume de não críticos tooa directory do servidor de Olá (por exemplo D:\). Normalmente, Olá volume de sistema operativo Windows é o volume crítico Olá.

13. processo de recuperação do toocomplete Olá, utilize seguinte de Olá secção demasiado[aplicam-se os ficheiros de estado do sistema de Olá restaurado num servidor Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Aplicar o restauro do Estado do sistema no Windows Server

Assim que tiver recuperado o estado do sistema de ficheiros utilizando o Azure Recovery Services Agent, utilize Olá cópia de segurança do Windows Server utilitário tooapply Olá recuperar o estado do sistema tooWindows servidor. já se encontra disponível no servidor de Olá Olá utilitário de cópia de segurança do Windows Server. Olá, os passos seguintes explica como tooapply Olá recuperar o estado do sistema.

1. Seguinte de Olá utilize comandos tooreboot o servidor no *modo de reparação de serviços de diretório*. Na linha de comandos elevada:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Após o reinício de Olá, abra o snap-in cópia de segurança do Windows Server de Olá. Se não souber qual o snap-in do Olá foi instalado, pesquisar computador Olá ou um servidor para **cópia de segurança do Windows Server**.

    aplicação de ambiente de trabalho de Olá aparece nos resultados de pesquisa de Olá.

3. No snap-in Olá, selecione **cópia de segurança Local**.

    ![Selecione toorestore de cópia de segurança Local a partir daí](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Na consola de cópia de segurança Local Olá, no Olá **painel ações**, clique em **recuperar** tooopen Olá Assistente de recuperação.

5. Selecione a opção de Olá, **uma cópia de segurança armazenada noutra localização**e clique em **seguinte**.

   ![Escolha toorecover tooa outro servidor](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Quando especificar o tipo de localização de Olá, selecione **remoto pasta partilhada** se a cópia de segurança do Estado do sistema foi recuperada tooanother servidor. Se o estado do sistema foi recuperado localmente, em seguida, selecione **unidades locais**. 

    ![Selecione se toorecovery do servidor local ou outro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Introduza Olá caminho toohello *WindowsImageBackup* diretório, ou escolha a unidade local Olá que contém este diretório (por exemplo, D:\WindowsImageBackup) recuperado como parte da recuperação de ficheiros de estado do sistema de Olá utilizando o Azure Recovery Serviços de agente e clique em **seguinte**.

    ![ficheiro partilhado do caminho toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Versão de estado do sistema de Olá Selecione se pretende toorestore e clique em **seguinte**.

9. No painel do Olá selecionar tipo de recuperação, selecione **estado do sistema** e clique em **seguinte**.

10. Para a localização de Olá de Olá recuperação do Estado do sistema, selecione **localização Original**e clique em **seguinte**.

11. Reveja os detalhes de confirmação de Olá, verifique as definições de reinício de Olá e clique em **recuperar** tooapplly Olá restaurar ficheiros de estado do sistema.

    ![Iniciar Olá restaurar ficheiros de estado do sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Considerações especiais sobre a recuperação de estado do sistema no servidor do Active Directory

Cópia de segurança do Estado do sistema inclui dados do Active Directory. Utilize Olá seguintes passos toorestore os serviços de domínio do Active Directory (AD DS) de estado tooa anterior estado atual.

1. Reinicie o controlador de domínio de Olá no serviços restaurar modo diretório (DSRM).
2. Siga os passos de Olá [aqui](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover do AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Resolver problemas de restauro de estado do sistema com falhas

Se o processo anterior de Olá de aplicar o estado do sistema não for concluída com êxito, utilize o Windows Server Olá toorecover de ambiente de recuperação do Windows (Win RE). Olá passos seguintes explicam como toorecover utilizando Win RE. Utilize esta opção apenas se o Windows Server não se inicie normalmente após um restauro do Estado do sistema. seguir o processo de Olá apague dados não pertencente ao sistema, tenha cuidado. 

1. Arrancar o servidor do Windows hello ambiente de recuperação do Windows (Win RE).

2. Selecione as opções de disponíveis três Olá resolução de problemas.

    ![menu abrir](./media/backup-azure-restore-system-state/winre-1.png)

3. De Olá **opções avançadas** ecrã, selecione **linha de comandos** e forneça o nome de utilizador de administrador de servidor de Olá e a palavra-passe.

   ![menu abrir](./media/backup-azure-restore-system-state/winre-2.png)

4. Forneça o nome de utilizador de administrador de servidor de Olá e a palavra-passe.

    ![menu abrir](./media/backup-azure-restore-system-state/winre-3.png)

5. Quando abrir Olá linha de comandos no modo de administrador, execute os seguintes versões cópia de segurança do comando tooget Olá estado do sistema.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![obter versões de cópia de segurança do Estado do sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. Execute todos os volumes disponíveis na cópia de segurança de Olá de Olá tooget de comando a seguir.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![obter versões de cópia de segurança do Estado do sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. Olá seguinte comando recupera todos os volumes que fazem parte do Olá cópia de segurança de estado de sistema. Tenha em atenção que este passo recupera apenas Olá volumes críticos que fazem parte Olá do Estado do sistema. Todos os dados de sistema não é eliminada.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![obter versões de cópia de segurança do Estado do sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Passos seguintes
* Agora que recuperar os seus ficheiros e pastas, pode [gerir as cópias de segurança](backup-azure-manage-windows-server.md).
