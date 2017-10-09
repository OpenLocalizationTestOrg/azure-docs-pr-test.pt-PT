---
title: "aaaUse tooback de servidor de cópia de segurança do Azure se um tooAzure de farm do SharePoint | Microsoft Docs"
description: "Utilizar o servidor de cópia de segurança do Azure tooback cópias de segurança e restaurar os dados do SharePoint. Este artigo fornece Olá informações tooconfigure farm do SharePoint para que os dados pretendido podem ser armazenados no Azure. Pode restaurar dados de SharePoint protegidos do disco ou a partir do Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Criar cópias de segurança uma tooAzure de farm do SharePoint
A cópia de segurança SharePoint do farm tooMicrosoft do Azure utilizando o servidor de cópia de segurança do Azure (MABS) da Microsoft no muito Olá mesma maneira que a cópia de segurança de outras origens de dados. Cópia de segurança do Azure fornece flexibilidade na Olá agenda de cópia de segurança toocreate pontos de cópia de segurança diários, semanais, mensais ou anuais e dá-lhe opções de política de retenção para vários pontos de cópia de segurança. Também proporciona uma capacidade de Olá toostore cópias de disco local rápidos objetivos de tempo de recuperação (RTO) e toostore copia tooAzure para a retenção de longo prazo, económica.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Versões suportadas e relacionadas com cenários de proteção do SharePoint
O Backup do Azure para o DPM suporta Olá os seguintes cenários:

| Carga de trabalho | Versão | Implementação de SharePoint | Proteção e recuperação |
| --- | --- | --- | --- | --- | --- |
| SharePoint |O SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0 |SharePoint implementado como um servidor físico ou máquina virtual Hyper-V/VMware <br> -------------- <br> AlwaysOn SQL | Opções de recuperação do Farm do SharePoint de proteger: farm de recuperação, a base de dados e o ficheiro ou item de lista de pontos de recuperação do disco.  Base de dados e de farm de recuperação pontos de recuperação do Azure. |

## <a name="before-you-start"></a>Antes de começar
Existem algumas coisas que precisa de tooconfirm antes de criar cópias de segurança uma tooAzure de farm do SharePoint.

### <a name="prerequisites"></a>Pré-requisitos
Antes de continuar, certifique-se de que tem [instalado e preparado hello do servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md) tooprotect cargas de trabalho.

### <a name="protection-agent"></a>Agente de proteção
agente de proteção de Olá tem de estar instalado no servidor de Olá que está a executar o SharePoint, servidores de Olá que estejam a executar o SQL Server e todos os outros servidores que fazem parte do farm do SharePoint Olá. Para obter mais informações sobre como tooset se o agente de proteção de Olá, consulte [a configuração do agente de proteção](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  uma exceção de Olá é que instalar o agente de Olá apenas no servidor web único front-end (WFE). O DPM precisa agente Olá um WFE server apenas tooserve como ponto de entrada de Olá para proteção.

### <a name="sharepoint-farm"></a>Farm do SharePoint
Para cada 10 milhões de itens no farm de Olá, tem de existir pelo menos 2 GB de espaço no volume de olá onde está localizada a pasta MABS Olá. Este espaço é necessário para a geração do catálogo. Para MABS toorecover itens específicos (coleções de sites, sites, listas, bibliotecas de documentos, pastas, documentos individuais e itens de lista), a geração do catálogo cria uma lista dos URLs de Olá que estão contidas dentro de cada base de dados de conteúdo. Pode ver a lista Olá de URLs no painel de itens recuperáveis Olá no Olá **recuperação** área da consola do administrador MABS de tarefas.

### <a name="sql-server"></a>SQL Server
MABS é executado como uma conta LocalSystem. tooback segurança de bases de dados do SQL Server, MABS necessita de privilégios sysadmin nessa conta para o servidor de Olá que está a executar o SQL Server. Definir NT AUTHORITY\SYSTEM demasiado*sysadmin* no servidor de Olá que está a executar o SQL Server antes de faça uma cópia de.

Se o farm do SharePoint Olá tem bases de dados do SQL Server configuradas com aliases do SQL Server, instale os componentes de cliente do SQL Server Olá no servidor Web front-end Olá que irá proteger MABS.

### <a name="sharepoint-server"></a>SharePoint Server
Enquanto o desempenho depende de vários fatores, tais como o tamanho do farm do SharePoint, um MABS pode proteger um farm do SharePoint 25 TB como orientação geral.

### <a name="whats-not-supported"></a>O que não é suportado
* MABS que protege um farm do SharePoint não protege os índices de pesquisa ou bases de dados de serviço de aplicações. Terá de proteção de Olá tooconfigure destas bases de dados em separado.
* MABS não fornece cópia de segurança das bases de dados do SQL Server do SharePoint que estão alojados em partilhas de servidor (SOFS) de ficheiros de escalamento horizontal.

## <a name="configure-sharepoint-protection"></a>Configurar a proteção do SharePoint
Antes de poder utilizar MABS tooprotect SharePoint, tem de configurar o serviço de escritor de VSS do SharePoint de Olá (serviço WSS Writer) utilizando **ConfigureSharePoint.exe**.

Pode encontrar **ConfigureSharePoint.exe** na pasta \bin de Olá [caminho de instalação MABS] no servidor web front-end de Olá. Esta ferramenta fornece o agente de proteção de Olá com credenciais de Olá para farm do SharePoint Olá. Executá-la num único servidor WFE. Se tiver múltiplos servidores WFE, selecione apenas um quando configurar um grupo de proteção.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>Olá tooconfigure serviço de escritor de VSS do SharePoint
1. No servidor WFE de Olá, numa linha de comandos, vá demasiado [localização da instalação MABS] \bin\.
2. Introduza o comando ConfigureSharePoint - EnableSharePointProtection.
3. Introduza as credenciais de administrador do farm Olá. Esta conta deve ser um membro de Olá grupo de administrador local no servidor WFE de Olá. Se o administrador do farm Olá não é um Olá de concessão de administrador local as seguintes permissões no servidor WFE de Olá:
   * Conceda Olá WSS_Admin_WPG controlo total toohello DPM pasta grupo (% programa Files%\Microsoft Azure Backup\DPM).
   * Conceda Olá WSS_Admin_WPG grupo acesso de leitura toohello DPM chave de registo (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Terá toorerun ConfigureSharePoint.exe sempre que exista uma alteração de credenciais de administrador de farm do Olá SharePoint.
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a>Fazer cópias de segurança de um farm do SharePoint utilizando MABS
Depois de ter configurado MABS e Olá farm do SharePoint, conforme explicado anteriormente, o SharePoint pode ser protegido por MABS.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect um farm do SharePoint
1. De Olá **proteção** separador de Olá consola do administrador MABS, clique em **novo**.
    ![Novo separador de proteção](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. No Olá **selecionar tipo de grupo de proteção** página do Olá **criar novo grupo de proteção** assistente, selecione **servidores**e, em seguida, clique em **seguinte** .

    ![Tipo de selecionar o grupo de proteção](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. No Olá **selecionar membros do grupo** ecrã, Olá selecione a caixa de verificação para Olá SharePoint server que pretende tooprotect e clique em **seguinte**.

    ![Selecionar Membros do grupo](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > Com o agente de proteção de Olá instalado, pode ver servidor Olá no Assistente de Olá. MABS também mostra a estrutura. Uma vez que executou o ConfigureSharePoint.exe, MABS comunica com o serviço de escritor de VSS do SharePoint de Olá e respetivas bases de dados do SQL Server correspondentes e reconhece a estrutura de farm do SharePoint Olá, Olá associados a bases de dados de conteúdos e quaisquer itens correspondentes.
   >
   >
4. No Olá **selecionar método de proteção de dados** página, introduza o nome de Olá de Olá **grupo de proteção**e selecione o preferencial *métodos de proteção*. Clique em **Seguinte**.

    ![Selecione o método de proteção de dados](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > método de proteção de disco Olá ajuda toomeet objetivos de recuperação-tempo curto.
   >
   >
5. No Olá **especificar objetivos a curto prazo** página, selecione o preferencial **período de retenção** e identificar quando quiser toooccur de cópias de segurança.

    ![Especificar objetivos a curto prazo](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > Uma vez recuperação é frequentemente necessária para dados é inferior a cinco dias, é selecionado um período de retenção de cinco dias no disco e certificar-se de que essa cópia de segurança Olá ocorre durante o horário de não produção, para este exemplo.
   >
   >
6. Reveja Olá armazenamento conjunto espaço em disco atribuído para o grupo de proteção de Olá e, em seguida, clique **seguinte**.
7. Para cada grupo de proteção, MABS aloca toostore de espaço em disco e gerir réplicas. Neste momento, MABS tem de criar uma cópia dos dados de Olá selecionado. Selecione como e quando pretende réplica Olá criada e, em seguida, clique em **seguinte**.

    ![Escolher método de criação de réplica](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > toomake certificar-se de que o tráfego de rede não é afetado, selecione uma hora fora do horário de produção.
   >
   >
8. MABS assegura a integridade dos dados, efetuando as verificações de consistência na réplica de Olá. Existem duas opções disponíveis. Pode definir verificações de consistência de toorun uma agenda ou o DPM pode executar verificações de consistência automaticamente na réplica de Olá sempre que o se tornar inconsistente. Selecione a sua opção preferida e, em seguida, clique em **seguinte**.

    ![Verificação de consistência](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. No Olá **especificar dados da proteção Online** página, selecione o farm do SharePoint Olá que pretende tooprotect e, em seguida, clique em **seguinte**.

    ![O DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. No Olá **Especificar agenda de cópia de segurança Online** página, selecione o horário da sua preferência e, em seguida, clique em **seguinte**.

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > MABS fornece um máximo de dois tooAzure de cópias de segurança diária de Olá, em seguida, disponíveis ponto de cópia de segurança de disco mais recente. Cópia de segurança do Azure também pode controlar a quantidade de Olá de largura de banda WAN, que pode ser utilizada para cópias de segurança no pico e horas de ponta utilizando [limitação de rede de cópia de segurança do Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).
    >
    >
11. Consoante a agenda de cópia de segurança de Olá que selecionou no Olá **especificar política de retenção Online** página de política de retenção de Olá Selecione para pontos de cópia de segurança diárias, semanais, mensais e anuais.

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > MABS utiliza um esquema de retenção do avô-pai-filho na qual pode ser selecionada uma política de retenção diferentes para diferentes pontos de cópia de segurança.
    >
    >
12. Toodisk semelhante, necessita de uma réplica de ponto de referência inicial toobe criada no Azure. Selecione toocreate sua opção preferida tooAzure uma cópia de segurança inicial e, em seguida, clique em **seguinte**.

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Reveja as definições selecionadas no Olá **resumo** página e, em seguida, clique em **criar grupo**. Verá uma mensagem de êxito depois do grupo de proteção de Olá foi criado.

    ![Resumo](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a>Restaurar um item do SharePoint do disco utilizando MABS
No seguinte exemplo de Olá, Olá *SharePoint recuperar item* foi eliminado acidentalmente e tem de toobe recuperada.
![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Abra Olá **consola de administrador do DPM**. São apresentados todos os farms do SharePoint que estão protegidos pelo DPM Olá **proteção** separador.

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. item de Olá de toorecover toobegin, selecione de Olá **recuperação** separador.

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. Pode pesquisar o SharePoint para *SharePoint recuperar item* utilizando uma pesquisa com base no caráter universal dentro de uma recuperação do ponto de intervalo.

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Selecionar ponto de recuperação adequadas Olá de resultados da pesquisa Olá, clique no item de Olá e, em seguida, selecione **recuperar**.
5. Também pode procurar através de vários pontos de recuperação e selecione uma base de dados ou item toorecover. Selecione **data > hora da recuperação**e, em seguida, selecione Olá correto **base de dados > farm do SharePoint > ponto de recuperação > Item**.

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Clique no item de Olá e, em seguida, selecione **recuperar** tooopen Olá **Assistente de recuperação**. Clique em **Seguinte**.

    ![Rever seleção de recuperação](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Selecione o tipo de Olá de recuperação que pretende tooperform e, em seguida, clique em **seguinte**.

    ![Tipo de recuperação](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > Olá, seleção de **recuperar toooriginal** no Olá exemplo recupera o site do SharePoint Olá item toohello original.
   >
   >
8. Selecione Olá **processo de recuperação** que pretende que o toouse.

   * Selecione **recuperar sem utilizar um farm de recuperação** se o farm do SharePoint Olá não foi alterado e é Olá igual à recuperação Olá ponto que seja restaurado.
   * Selecione **recuperar um farm de recuperação a utilizar** se o farm do SharePoint Olá foi alterada desde a criação do ponto de recuperação Olá.

     ![Processo de recuperação](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Forneça temporariamente uma transição do SQL Server instância localização toorecover Olá base de dados e fornecer uma partilha de ficheiros de teste no MABS e Olá no servidor que está a executar o item do SharePoint toorecover Olá.

    ![Transição Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    MABS anexa Olá conteúdo da base de dados que está a alojar Olá SharePoint item toohello temporária instância do SQL Server. Da base de dados conteúdo de Olá, recupera item Olá e coloca-o no Olá localização do ficheiro no MABS de transição. Olá recuperar o item que se encontra agora a localização de transição de Olá necessidades toobe exportado toohello localização no farm do SharePoint Olá de transição.

    ![Transição Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Selecione **especificar opções de recuperação**e aplicar definições de segurança toohello farm do SharePoint ou aplicar definições de segurança de Olá Olá do ponto de recuperação. Clique em **Seguinte**.

    ![Opções de recuperação](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > Pode escolher a utilização de largura de banda de rede de Olá toothrottle. Isto minimiza o servidor de produção do impacto toohello durante as horas de produção.
    >
    >
11. Reveja as informações de resumo de Olá e, em seguida, clique em **recuperar** toobegin recuperação de ficheiros de Olá.

    ![Resumo de recuperação](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Agora selecionar Olá **monitorização** separador Olá **consola do administrador MABS** tooview Olá **estado** de recuperação de Olá.

    ![Estado de recuperação](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > ficheiro de Olá agora é restaurado. Pode atualizar o ficheiro do Olá SharePoint site toocheck Olá restaurada.
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Restaurar uma base de dados do SharePoint a partir do Azure utilizando o DPM
1. toorecover uma base de conteúdos do SharePoint, navegue através de vários pontos de recuperação (conforme mostrado anteriormente) e selecione Olá ponto de recuperação que pretende que o toorestore.

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Faça duplo clique Olá SharePoint ponto tooshow Olá disponíveis SharePoint catálogo as informações de recuperação.

   > [!NOTE]
   > Porque o farm do SharePoint Olá é protegido para a retenção de longa duração no Azure, não existem informações de catálogo (metadados) estão disponíveis no MABS. Como resultado, sempre que uma base de dados ponto no tempo do conteúdo do SharePoint tem toobe recuperada, terá de farm do SharePoint toocatalog Olá novamente.
   >
   >
3. Clique em **recatalogação**.

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    Olá **nuvem Recatalogar** é aberta a janela de estado.

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    Depois de concluída a cataloging, o estado de Olá mudar demasiado*êxito*. Clique em **Fechar**.

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Clique em objetos de SharePoint Olá mostrado na Olá MABS **recuperação** separador Estrutura de base de dados de conteúdo de Olá tooget. Clique no item de Olá e, em seguida, clique em **recuperar**.

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. Neste momento, siga Olá [passos de recuperação anteriores no artigo](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover SharePoint conteúdo bases de dados de disco.

## <a name="faqs"></a>Perguntas mais frequentes
P: posso recuperar uma localização original do SharePoint item toohello se SharePoint estiver configurado utilizando o SQL Server AlwaysOn (com a proteção no disco)?<br>
R: Sim, o item de Olá pode ser recuperado toohello original site do SharePoint.

P: posso recuperar uma localização original do SharePoint da base de dados toohello se SharePoint estiver configurado utilizando o SQL Server AlwaysOn?<br>
R: porque as bases de dados do SharePoint são configuradas no SQL Server AlwaysOn, não pode ser modificados a menos que o grupo de disponibilidade de Olá é removido. Como resultado, MABS não é possível restaurar uma base de dados toohello a localização original. Pode recuperar uma instância de SQL Server de tooanother de base de dados do SQL Server.

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre MABS proteção do SharePoint - consulte [vídeo série - DPM proteção do SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
