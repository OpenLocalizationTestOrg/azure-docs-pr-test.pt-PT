---
title: "aaaAzure cópia de segurança para cargas de trabalho do SQL Server utilizando o servidor de cópia de segurança do Azure | Microsoft Docs"
description: "Um toobacking de introdução de segurança de bases de dados do SQL Server utilizando o servidor de cópia de segurança do Azure"
services: backup
documentationcenter: 
author: pvrk
manager: Shivamg
editor: 
ms.assetid: c8b1f7ec-26b1-4ef0-a3f2-91aec959daea
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3a94338e8aca3f9d8611a72bcd223397ffb96f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-with-azure-backup-server"></a>Criar cópias de segurança do SQL Server tooAzure com o servidor de cópia de segurança do Azure
Este artigo orienta-o pelos passos de configuração de Olá para cópia de segurança das bases de dados do SQL Server utilizando o servidor de cópia de segurança do Azure do Microsoft (MABS).

gestão de Olá de tooAzure de cópia de segurança de base de dados do SQL Server e a recuperação a partir do Azure envolve três passos:

1. Crie um tooAzure de bases de dados do SQL Server de tooprotect política de cópia de segurança.
2. Crie cópias de segurança a pedido tooAzure.
3. Recupere a base de dados de Olá a partir do Azure.

## <a name="before-you-start"></a>Antes de começar
Antes de começar, certifique-se de que tem [instalado e preparado hello do servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md).

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>Criar uma política de cópia de segurança tooprotect do SQL Server bases de dados tooAzure
1. Olá da IU do servidor de cópia de segurança do Azure, clique em Olá **proteção** área de trabalho.
2. No Friso de ferramentas Olá, clique em **novo** toocreate um novo grupo de proteção.

    ![Criar grupo de proteção](./media/backup-azure-backup-sql/protection-group.png)
3. MABS mostra o ecrã de início de Olá com orientação Olá sobre a criação de um **grupo de proteção**. Clique em **Seguinte**.
4. Selecione **servidores**.

    ![Selecione o tipo de grupo de proteção - 'Servidores'](./media/backup-azure-backup-sql/pg-servers.png)
5. Expanda a máquina do SQL Server olá onde toobe de bases de dados de Olá uma cópia de segurança estão presentes. MABS mostra várias origens de dados que podem ser uma cópia de segurança a partir desse servidor. Expanda Olá **todas as partilhas de SQL** e selecione Olá bases de dados (neste caso, iremos selecionadas ReportServer$ MSDPM2012 e ReportServer$ MSDPM2012TempDB) toobe uma cópia de segurança. Clique em **Seguinte**.

    ![Selecione a base de dados SQL](./media/backup-azure-backup-sql/pg-databases.png)
6. Forneça um nome para o grupo de proteção de Olá e selecione Olá **pretendo proteção online** caixa de verificação.

    ![Método de proteção de dados - disco de curto prazo e Online do Azure](./media/backup-azure-backup-sql/pg-name.png)
7. No Olá **especificar objetivos a curto prazo** ecrã, incluir entradas necessário de Olá toocreate toodisk de pontos de cópia de segurança.

    Aqui Vemos que **período de retenção** estiver definido demasiado*5 dias*, **frequência de sincronização** está definido tooonce cada *15 minutos* que é Olá frequência com que foi efetuada a cópia de segurança. **Cópia de segurança completa rápida** estiver definido demasiado*8:00 P.M*.

    ![Objetivos de curto prazo](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > Às 8:00 PM (entrada de ecrã toohello de acordo com) cópia de segurança é criado um ponto diariamente por transferência de dados de Olá que tem sido modificados de Olá ponto de cópia de segurança de 8:00 PM do dia anterior. Este processo é denominado **cópia de segurança completa rápida**. Enquanto os registos de transações Olá são sincronizados a cada 15 minutos, se existir uma base de dados necessário toorecover Olá em 9:00 PM –, é criado o ponto de Olá por replaying Olá os registos de Olá express última cópia de segurança completa ponto (de 8 horas neste caso).
   >
   >

8. Clique em **Seguinte**

    Mostra MABS Olá geral espaço de armazenamento disponível e a utilização do espaço em disco potencial Olá.

    ![Alocação de disco](./media/backup-azure-backup-sql/pg-storage.png)

    Por predefinição, MABS cria um volume por origem de dados (SQL Server da base de dados) que é utilizado para cópia de segurança inicial Olá. Através desta abordagem, Olá Gestor de discos lógicos (LDM) limita MABS proteção too300 as origens de dados (bases de dados do SQL Server). toowork em torno esta limitação, selecione de Olá **colocalizar dados no agrupamento de armazenamento do DPM**, opção. Se utilizar esta opção, MABS utiliza um único volume de várias origens de dados, que permite MABS tooprotect segurança too2000 bases de dados do SQL.

    Se **aumentar automaticamente os volumes de Olá** opção estiver selecionada, MABS pode conta para o volume de cópia de segurança de Olá aumentado à medida que aumenta de dados de produção Olá. Se **aumentar automaticamente os volumes de Olá** opção não estiver selecionada, MABS limita Olá armazenamento de cópia de segurança utilizado toohello origens de dados no grupo de proteção de Olá.
9. Os administradores são dada a opção de Olá de transferência este congestionamento de largura de banda tooavoid inicial de cópia de segurança manualmente (desativado rede) ou de rede de Olá. Pode também configurar tempo Olá no qual Olá pode acontecer transferência inicial. Clique em **Seguinte**.

    ![Método de replicação inicial](./media/backup-azure-backup-sql/pg-manual.png)

    cópia de segurança inicial Olá requer transferência Olá completa da origem de dados (SQL Server da base de dados) a partir de tooMABS (máquina do SQL Server) do servidor de produção. Estes dados poderão ser grandes e transferir dados Olá rede Olá poderá exceder a largura de banda. Por este motivo, os administradores podem optar cópia de segurança inicial tootransfer Olá: **manualmente** (utilizando o suporte de dados amovível) tooavoid congestionamento de largura de banda, ou **automaticamente através da rede Olá** (a uma determinada hora).

    Após a conclusão da cópia de segurança inicial Olá, rest Olá de cópias de segurança de Olá são cópias de segurança incrementais em cópia de segurança inicial Olá. Cópias de segurança incrementais tendem toobe pequena e são facilmente transferidas pela rede Olá.
10. Escolha a quando pretende toorun de verificação de consistência Olá e clique em **seguinte**.

    ![Verificação de consistência](./media/backup-azure-backup-sql/pg-consistent.png)

    MABS podem executar de consistência verificação toocheck Olá a integridade do ponto de cópia de segurança de Olá. Calcula a soma de verificação Olá Olá cópia de segurança do ficheiro de no servidor de produção Olá (máquina do SQL Server neste cenário) e os dados de cópia de segurança de Olá do que o ficheiro em MABS. No caso de Olá de um conflito, presume-se que Olá MABS ficheiro de cópia de segurança está danificado. MABS rectifies dados de cópia de segurança de Olá enviando blocos Olá correspondente toohello discrepância de soma de verificação. Como a verificação de consistência Olá é uma operação de intensivos em termos de desempenho, os administradores têm a opção Olá de agendamento da verificação de consistência Olá ou executar automaticamente.
11. a proteção online toospecify das origens de dados de Olá, selecione Olá toobe de bases de dados protegida tooAzure e clique em **seguinte**.

    ![Selecione as origens de dados](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. Os administradores podem optar agendas de cópia de segurança e as políticas de retenção que melhor corresponda às respetivas políticas da organização.

    ![Agenda e retenção](./media/backup-azure-backup-sql/pg-schedule.png)

    Neste exemplo, as cópias de segurança são efetuadas uma vez por dia às 12:00 PM e 8 PM (parte inferior do ecrã de Olá)

    > [!NOTE]
    > É uma boa prática toohave alguns pontos de recuperação de curta duração em disco para a recuperação rápida. Estes pontos de recuperação são utilizados para "recuperação operacional". Azure funciona como uma localização de boa retirada do local com SLAs superiores e garantida disponibilidade.
    >
    >

    **Melhor prática**: Certifique-se de que estão agendadas de cópias de segurança do Azure após a conclusão de Olá de cópias de segurança de disco local utilizando o DPM. Isto permite Olá tooAzure de cópia de segurança toobe copiado de disco mais recente.

13. Escolha o agendamento de política de retenção de Olá. Olá obter detalhes sobre como funciona a política de retenção de Olá são fornecidos ao [tooreplace do Backup do Azure de utilização do artigo de infraestrutura da banda](backup-azure-backup-cloud-as-tape.md).

    ![Política de retenção](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    Neste exemplo:

    * As cópias de segurança são efetuadas uma vez por dia às 12:00 PM e 8 PM (parte inferior do ecrã de Olá) e são mantidas durante 180 dias.
    * cópia de segurança de Olá no Sábado às 12:00 são mantidas durante 104 semanas
    * cópia de segurança de Olá no último Sábado às 12:00 são mantidas durante 60 meses
    * cópia de segurança de Olá no último Sábado de Março às 12:00 é mantido para 10 anos
14. Clique em **seguinte** e Olá, selecione a opção adequada para transferir Olá tooAzure de cópia de segurança inicial. Pode escolher **automaticamente através da rede Olá** ou **cópia de segurança Offline**.

    * **Através da rede Olá** transferências Olá tooAzure de dados de cópia de segurança de acordo com a agenda de Olá escolhida para cópia de segurança.
    * Como **cópia de segurança Offline** funciona é explicada no [fluxo de trabalho de cópia de segurança Offline no Backup do Azure](backup-azure-backup-import-export.md).

    Escolha transferência relevantes Olá mecanismo toosend Olá cópia de segurança inicial tooAzure e clique em **seguinte**.
15. Depois de rever os detalhes da política de Olá no Olá **resumo** ecrã, clique em Olá **criar grupo** o fluxo de trabalho do botão toocomplete Olá. Pode clicar em Olá **fechar** botão e monitor Olá progresso da tarefa na área de trabalho de monitorização.

    ![Criação do grupo de proteção em curso](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>Cópia de segurança a pedido de uma base de dados do SQL Server
Enquanto passos anteriores Olá criada uma política de cópia de segurança, é criado um "ponto de recuperação" apenas quando ocorre a primeira cópia de segurança Olá. Em vez de aguardar Olá programador tookick no, passos Olá abaixo criação de Olá de Acionador de uma recuperação ponto manualmente.

1. Aguarde até que mostra o estado do grupo de proteção de Olá **OK** da base de dados de Olá antes de criar o ponto de recuperação Olá.

    ![Membros do grupo de proteção](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Faça duplo clique na base de dados de Olá e selecione **criar ponto de recuperação**.

    ![Criar ponto de recuperação Online](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. Escolha **proteção Online** no menu pendente de Olá e clique em **OK**. Esta ação inicia a criação de Olá de um ponto de recuperação no Azure.

    ![Criar ponto de recuperação](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. Pode ver o progresso da tarefa Olá no Olá **monitorização** onde poderá encontrar um em curso da área de trabalho da tarefa como Olá um descrito na figura seguinte Olá.

    ![Consola de monitorização](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>Recuperar uma base de dados do SQL Server a partir do Azure
Olá passos seguintes são necessário toorecover uma entidade protegida (base de dados do SQL Server) a partir do Azure.

1. Abra a consola de gestão do servidor DPM Olá. Navegue demasiado**recuperação** área de trabalho onde pode ver os servidores de Olá cópias de segurança do DPM. Procure Olá necessárias da base de dados (por este cenário ReportServer$ MSDPM2012). Selecione um **recuperação a partir de** tempo que termina com **Online**.

    ![Selecione o ponto de recuperação](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Clique no nome da base de dados de Olá e clique em **recuperar**.

    ![Recuperar a partir do Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. O DPM apresenta detalhes de Olá Olá do ponto de recuperação. Clique em **Seguinte**. toooverwrite Olá base de dados, tipo de recuperação Olá selecione **recuperar toooriginal instância do SQL Server**. Clique em **Seguinte**.

    ![Recuperar tooOriginal localização](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    Neste exemplo, o DPM permite a recuperação de instância do SQL Server do Olá da base de dados tooanother ou pasta de rede tooa autónomo.
4. No Olá **opções especificar recuperação** ecrã, pode selecionar as opções de recuperação de Olá como toothrottle Olá da largura de banda utilizada pela recuperação de limitação de utilização de largura de banda de rede. Clique em **Seguinte**.
5. No Olá **resumo** ecrã, pode ver todas as configurações de recuperação de Olá fornecidas até ao momento. Clique em **recuperar**.

    Olá estado de recuperação mostra a base de dados de Olá que está a ser recuperada. Pode clicar em **fechar** tooclose Olá assistente e vista Olá progresso na Olá **monitorização** área de trabalho.

    ![Iniciar o processo de recuperação](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Depois de concluir a recuperação de Olá, base de dados de Olá restaurada é consistente da aplicação.

### <a name="next-steps"></a>Passos Seguintes:
• [FAQ sobre a cópia de segurança do azure](backup-azure-backup-faq.md)
