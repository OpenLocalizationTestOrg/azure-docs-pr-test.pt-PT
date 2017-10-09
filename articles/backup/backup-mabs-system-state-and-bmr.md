---
title: "aaaAzure cópia de segurança do servidor protege o estado do sistema e restaura toobare metal | Microsoft Docs"
description: "Utilize tooback do servidor de cópia de segurança do Azure se o estado do sistema e fornecer proteção de recuperação bare-metal (BMR)."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>Cópia de segurança do Estado do sistema e restaurar toobare metal. o servidor de cópia de segurança do Azure

Servidor de cópia de segurança do Azure efetua cópias de segurança do Estado do sistema e fornece proteção de recuperação bare-metal (BMR).

*   **Cópia de segurança de estado de sistema**: efetua cópias de segurança de ficheiros do sistema operativo, pelo que pode recuperar quando um computador é iniciado, mas os ficheiros de sistema e registo Olá sejam perdidas. Inclui uma cópia de segurança do Estado do sistema:
    * Membro de domínio: ficheiros, a base de dados de registo de classe COM+, registo de arranque
    * Controlador de domínio: Windows Server Active Directory (NTDS), efetuar o arranque de ficheiros, a base de dados de registo de classe COM+, registo, o volume de sistema (SYSVOL)
    * Computador que executa serviços de cluster: os metadados do servidor de Cluster
    * Computador que executa os serviços de certificados: dados de certificado
* **Cópia de segurança bare-metal**: efetua cópias de segurança de ficheiros do sistema operativo e todos os dados em volumes críticos (exceto os dados de utilizador). Por definição, uma cópia de segurança de BMR inclui uma cópia de segurança do Estado do sistema. Fornece proteção quando um computador não iniciará e tiver toorecover tudo.

Olá, a tabela seguinte resume o que pode fazer cópias de segurança e recuperar. Para obter informações detalhadas sobre as versões da aplicação que podem ser protegidos com o estado do sistema e a BMR, consulte [servidor de cópia de segurança do Azure que faz uma cópia de segurança?](backup-mabs-protection-matrix.md).

|Cópia de segurança|Problema|Recuperar a partir de cópia de segurança do servidor de cópia de segurança do Azure|Recuperar a partir de cópia de segurança de estado de sistema|BMR|
|----------|---------|---------------------------|------------------------------------|-------|
|**Dados de ficheiro**<br /><br />Cópia de segurança de dados normal<br /><br />Cópia de segurança de estado de sistema/BMR|Dados de ficheiro perdidas|S|N|N|
|**Dados de ficheiro**<br /><br />Cópia de segurança do servidor do Backup do Azure de dados de ficheiro<br /><br />Cópia de segurança de estado de sistema/BMR|Sistema de operativo perdido ou danificado|N|S|S|
|**Dados de ficheiro**<br /><br />Cópia de segurança do servidor do Backup do Azure de dados de ficheiro<br /><br />Cópia de segurança de estado de sistema/BMR|Servidor perdido (volumes de dados intactos)|N|N|S|
|**Dados de ficheiro**<br /><br />Cópia de segurança do servidor do Backup do Azure de dados de ficheiro<br /><br />Cópia de segurança de estado de sistema/BMR|Servidor perdido (volumes de dados perdidos)|S|Não|Sim (BMR, seguida de recuperação normal de dados de ficheiro de cópia de segurança)|
|**Dados do SharePoint**:<br /><br />Cópia de segurança de servidor do Backup do Azure de dados do farm<br /><br />Cópia de segurança de estado de sistema/BMR|Site perdido, listas, itens de lista, documentos|S|N|N|
|**Dados do SharePoint**:<br /><br />Cópia de segurança de servidor do Backup do Azure de dados do farm<br /><br />Cópia de segurança de estado de sistema/BMR|Sistema de operativo perdido ou danificado|N|S|S|
|**Dados do SharePoint**:<br /><br />Cópia de segurança de servidor do Backup do Azure de dados do farm<br /><br />Cópia de segurança de estado de sistema/BMR|Recuperação após desastre|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Cópia de segurança de servidor do Backup do Azure de convidado ou anfitrião Hyper-V<br /><br />Cópia de segurança do sistema/BMR estado do anfitrião|VM perdida|S|N|N|
|Hyper-V<br /><br />Cópia de segurança de servidor do Backup do Azure de convidado ou anfitrião Hyper-V<br /><br />Cópia de segurança do sistema/BMR estado do anfitrião|Sistema de operativo perdido ou danificado|N|S|S|
|Hyper-V<br /><br />Cópia de segurança de servidor do Backup do Azure de convidado ou anfitrião Hyper-V<br /><br />Cópia de segurança do sistema/BMR estado do anfitrião|Anfitrião de Hyper-V perdido (VMs intactas)|N|N|S|
|Hyper-V<br /><br />Cópia de segurança de servidor do Backup do Azure de convidado ou anfitrião Hyper-V<br /><br />Cópia de segurança do sistema/BMR estado do anfitrião|Anfitrião de Hyper-V perdido (VMs perdidas)|N|N|S<br /><br />BMR, seguida de recuperação normal de servidor de cópia de segurança do Azure|
|SQL Server/Exchange<br /><br />Cópia de segurança de aplicação do servidor de cópia de segurança do Azure<br /><br />Cópia de segurança de estado de sistema/BMR|Dados da aplicação perdidas|S|N|N|
|SQL Server/Exchange<br /><br />Cópia de segurança de aplicação do servidor de cópia de segurança do Azure<br /><br />Cópia de segurança de estado de sistema/BMR|Sistema de operativo perdido ou danificado|N|Y|S|
|SQL Server/Exchange<br /><br />Cópia de segurança de aplicação do servidor de cópia de segurança do Azure<br /><br />Cópia de segurança de estado de sistema/BMR|Servidor perdido (base de dados/os registos de transações intactos)|N|N|S|
|SQL Server/Exchange<br /><br />Cópia de segurança de aplicação do servidor de cópia de segurança do Azure<br /><br />Cópia de segurança de estado de sistema/BMR|Servidor perdido (base de dados/os registos de transações perdidos)|N|N|S<br /><br />Recuperação de BMR, seguida de recuperação normal de servidor de cópia de segurança do Azure|

## <a name="how-system-state-backup-works"></a>Como funciona a cópia de segurança de estado de sistema

Quando é executada uma cópia de segurança do Estado do sistema, o servidor de cópia de segurança comunica com toorequest cópia de segurança do Windows Server uma cópia de segurança do servidor de Olá estado do sistema. Por predefinição, o servidor de cópia de segurança e de cópia de segurança do Windows Server utilizam unidade Olá que tenha Olá mais espaço livre. Informações sobre esta unidade são guardadas no ficheiro de PSDataSourceConfig.xml Olá. Esta é a unidade de Olá que utiliza a cópia de segurança do Windows Server para cópias de segurança.

Pode personalizar a unidade de Olá que utiliza o servidor de cópia de segurança para cópia de segurança de estado de sistema de Olá. No servidor de Olá protegido, aceda tooC:\Program Files\Microsoft Manager\MABS\Datasources de proteção de dados. Ficheiro PSDataSourceConfig.xml Olá aberta para edição. Olá alteração \<FilesToProtect\> valor para a letra de unidade de Olá. Guarde e feche o ficheiro de Olá. Se existir que um grupo de proteção definir estado do sistema Olá tooprotect computador Olá, execute uma verificação de consistência. Se for gerado um alerta, selecione **Modificar grupo de proteção** no Assistente de Olá, em seguida, concluir e alerta Olá. Em seguida, execute outra verificação de consistência.

Tenha em atenção que, se o servidor de proteção de Olá está num cluster, é possível que uma unidade de cluster será selecionada como unidade de Olá com Olá mais espaço livre. Se a propriedade dessa unidade tiver sido nó tooanother desativados e executa uma cópia de segurança do Estado do sistema, unidade Olá não está disponível e Olá cópia de segurança falhará. Neste cenário, modificar o ficheiro PSDataSourceConfig.xml tooa de toopoint unidade local.

Em seguida, a cópia de segurança do Windows Server cria uma pasta designada WindowsImageBackup na raiz de Olá da pasta de restauro de Olá. Como a cópia de segurança do Windows Server cria a cópia de segurança de Olá, todos os dados de Olá são colocados nesta pasta. Quando a cópia de segurança de Olá estiver concluída, o ficheiro de Olá é computador do servidor de cópia de segurança de toohello transferidos. Tenha em atenção Olá seguintes informações:

* Esta pasta e respetivo conteúdo não sejam limpos quando a cópia de segurança de Olá ou transferência for concluída. Olá melhor forma toothink desta situação é que o espaço de Olá está a ser reservado para Olá próxima vez que uma cópia de segurança estiver concluída.
* pasta de Olá é criada sempre que é efetuada uma cópia de segurança. carimbo de data e hora Olá reflete a hora de Olá da sua última cópia de segurança de estado de sistema.

## <a name="bmr-backup"></a>Cópia de segurança de BMR

Para a BMR (incluindo uma cópia de segurança do Estado do sistema), tarefas de cópia de segurança de Olá é guardada diretamente tooa partilha no computador do servidor de cópia de segurança de Olá. -Não é guardado tooa pasta no servidor de Olá protegido.

Servidor de cópia de segurança chama a cópia de segurança do Windows Server e partilha o volume de réplica Olá para essa cópia de segurança de BMR. Neste caso, não, não indica a cópia de segurança do Windows Server toouse Olá unidade Olá mais espaço livre. Em vez disso, utiliza partilha Olá que foi criada para a tarefa de Olá.

Quando a cópia de segurança de Olá estiver concluída, o ficheiro de Olá é computador do servidor de cópia de segurança de toohello transferidos. Os registos são armazenados em c:\windows\logs\windowsserverbackup..

## <a name="prerequisites-and-limitations"></a>Pré-requisitos e limitações

-   BMR não é suportada para computadores que executam o Windows Server 2003 ou computadores que executam um sistema operativo cliente.

-   Não é possível proteger a BMR e estado de sistema para Olá mesmo computador em grupos de proteção diferentes.

-   Um computador do servidor de cópia de segurança não é possível proteger a próprio para a BMR.

-   Curta duração tootape de proteção (disco para banda ou D2T) não é suportada para a BMR. Longa duração tootape de armazenamento (disco para disco para banda ou D2D2T) é suportada.

-   Para a proteção de BMR, a cópia de segurança do Windows Server tem de estar instalada no computador de Olá protegido.

-   Para a proteção de BMR, ao contrário para proteção do Estado do sistema, o servidor de cópia de segurança não tem quaisquer requisitos de espaço no computador de Olá protegido. Cópia de segurança do Windows Server transfere diretamente o computador do servidor de cópia de segurança de toohello de cópias de segurança. tarefa de transferência de cópia de segurança de Olá não aparece na hello do servidor de cópia de segurança **tarefas** vista.

-   Servidor de cópia de segurança reserva 30 GB de espaço no volume de réplica Olá para a BMR. Pode alterar isto na Olá **alocação do disco** página no assistente Modificar grupo de proteção de Olá ou utilizando os cmdlets Get-DatasourceDiskAllocation e Set-DatasourceDiskAllocation PowerShell de Olá. No volume de pontos de recuperação Olá, a proteção BMR requer cerca de 6 GB para uma retenção de cinco dias.
    * Tenha em atenção que não é possível reduzir tooless tamanho de volume de réplica do Olá de 15 GB.
    * Servidor de cópia de segurança não calcula o tamanho de Olá Olá BMR da origem de dados. Parte do pressuposto de 30 GB para todos os servidores. Altere o valor de Olá com base no tamanho Olá de cópias de segurança de BMR que pretende no seu ambiente. tamanho de Olá de uma cópia de segurança de BMR pode ser aproximadamente calculado como soma de Olá de espaço utilizado em todos os volumes críticos. Volumes críticos = volume de arranque + volume de sistema + volume que aloja os dados de estado do sistema, como o Active Directory.

-   Se mudar de estado proteção tooBMR da proteção do sistema, a proteção BMR requer menos espaço no Olá *volume de pontos de recuperação*. No entanto, hello espaço extra no volume de Olá não será recuperado. Manualmente pode diminuir o tamanho do volume Olá no Olá **modificar alocação do disco** página do Assistente para modificar grupo de proteção de Olá ou utilizando os cmdlets Get-DatasourceDiskAllocation e Set-DatasourceDiskAllocation PowerShell de Olá.

    Se mudar de estado proteção tooBMR da proteção do sistema, a proteção BMR requer mais espaço no Olá *volume de réplica*. volume de Olá é automaticamente expandido. Se quiser alocações de espaço predefinidas toochange Olá, utilize o cmdlet do PowerShell de Modify-DiskAllocation Olá.

-   Se alterar a partir da proteção do Estado de toosystem de proteção de BMR, é necessário mais espaço no volume de pontos de recuperação Olá. Servidor de cópia de segurança pode experimentar o volume de Olá tooautomatically aumento. Se não houver espaço insuficiente no agrupamento de armazenamento Olá, ocorre um erro.

    Se alterar da proteção de estado de toosystem de proteção de BMR, necessita de espaço disponível no computador de Olá protegido. Isto acontece porque a proteção do Estado do sistema guarda primeiro computador do Olá réplica toohello local e, em seguida, transfere-o computador do servidor de cópia de segurança de toohello.

## <a name="before-you-begin"></a>Antes de começar

1.  **Implementar o servidor de cópia de segurança do Azure**. Certifique-se de que o servidor de cópia de segurança é corretamente implementado. Para obter mais informações, consulte:
    * [Requisitos de sistema do servidor de cópia de segurança do Azure](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [Matriz de proteção do servidor de cópia de segurança](backup-mabs-protection-matrix.md)

2.  **Configurar o armazenamento**. Pode armazenar dados de cópia de segurança em disco, banda e na nuvem de Olá com o Azure. Para obter mais informações, consulte [preparar o armazenamento de dados](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage).

3.  **Configurar o agente de proteção de Olá**. Instale o agente de proteção de Olá Olá no computador no qual pretende tooback cópias de segurança. Para obter mais informações, consulte [agente de proteção DPM implementar Olá](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent).

## <a name="back-up-system-state-and-bare-metal"></a>Criar cópias de segurança do Estado do sistema e bare-metal
Configurar um grupo de proteção, conforme descrito em [implementar grupos de proteção](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups). Tenha em atenção que não as poderá proteger a BMR e estado de sistema para Olá mesmo computador em diferentes grupos. Além disso, ao selecionar a BMR, estado do sistema é ativado automaticamente.


1.  Assistente de criação de novo grupo de proteção de Olá tooopen na consola do administrador do servidor de cópia de segurança, selecione de Olá **proteção** > **ações** > **criar proteção Grupo**.

2.  No Olá **selecionar tipo de grupo de proteção** página, selecione **servidores**e, em seguida, selecione **seguinte**.

3.  No Olá **selecionar membros do grupo** página, expanda o computador de Olá e, em seguida, selecione **BMR** ou **estado do sistema**.

    Lembre-se de que não é possível proteger a BMR e o sistema de estado para Olá mesmo computador em diferentes grupos. Além disso, ao selecionar a BMR, estado do sistema é ativado automaticamente. Para obter mais informações, consulte [implementar grupos de proteção](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups).

4.  No Olá **selecionar método de proteção de dados** página, selecione a forma como pretende toohandle cópia de segurança de curta e longa duração. Cópia de segurança de curta duração é sempre toodisk pela primeira vez, com a opção de Olá de cópia de segurança do disco de Olá toohello do Azure na nuvem utilizando o Backup do Azure (curta ou longa duração). Uma nuvem de cópia de segurança toohello toolong-duração alternativa é tooset segurança de longo prazo tooa cópia de segurança autónomo dispositivo ou a banda biblioteca de banda que tenha ligado tooBackup servidor.

5.  No Olá **selecionar objetivos a curto prazo** página, selecione a forma como pretende tooback armazenamento tooshort prazo em disco:
    1. Para **período de retenção**, selecione de tempo durante o qual pretende que os dados de Olá tookeep no disco. 
    2. Para **frequência de sincronização**, selecione a frequência pretende toorun um toodisk de cópia de segurança incremental. Se não quiser tooset um intervalo de cópia de segurança, pode verificar Olá **apenas antes de um ponto de recuperação** opção. Servidor de cópia de segurança será executada uma cópia de segurança rápida completa imediatamente antes de cada ponto de recuperação está agendado.

6.  Se quiser toostore dados na banda para armazenamento de longa duração, em Olá **especificar objetivos de longo prazo** página, selecione de tempo durante o qual pretende que os dados de bandas tookeep (1 a 99 anos). 
    1. Para **frequência da cópia de segurança**, selecione frequência tootape cópia de segurança deve ser executada. frequência de Olá é baseada no período de retenção de Olá que selecionou:
        * Quando o período de retenção de Olá for de 1 a 99 anos, pode selecionar as cópias de segurança toooccur diária, semanal, bissemanal, mensal, trimestral, semestral ou anual.
        * Quando o período de retenção de Olá for de 1 a 11 meses, pode selecionar as cópias de segurança toooccur diária, semanal, bissemanal ou mensal.
        * Quando o período de retenção de Olá for de 1 a 4 semanas, pode selecionar toooccur de cópias de segurança diária ou semanal.

    2. No Olá **selecionar da banda e os detalhes da biblioteca** página, selecione Olá toouse de banda e da biblioteca, e se os dados devem ser comprimidos e encriptados.

7.  No Olá **rever alocação do disco** , reveja o espaço disco de agrupamento de armazenamento de Olá atribuída Olá grupo de proteção.

    1. **Tamanho de dados total** é Olá tamanho dos dados de Olá pretende tooback cópias de segurança.
    2. **Toobe de espaço em disco aprovisionado no servidor de cópia de segurança do Azure** espaço Olá que recomenda a cópia de segurança do servidor para o grupo de proteção de Olá. Servidor de cópia de segurança escolhe Olá ideal cópia de segurança volume de com base nas definições de Olá. No entanto, pode editar opções de cópia de segurança do volume de Olá no **detalhes de alocação de disco**. 
    3. Para cargas de trabalho, no menu pendente de Olá, selecione armazenamento Olá preferido. As edições que efectuou alterar valores Olá para **armazenamento Total** e **armazenamento livre** no Olá **armazenamento em disco disponível** painel. Espaço underprovisioned é a quantidade de Olá de armazenamento que a cópia de segurança do servidor sugere que adicionar volume toohello, uniforme tooensure de cópias de segurança.

8.  No Olá **escolher método de criação de réplica** página, selecione como pretende que a replicação de dados completa inicial toohandle Olá. Se escolher tooreplicate rede Olá, recomendamos que escolha uma hora de ponta. Para grandes quantidades de dados ou para condições de rede que são ideais, considere replicar dados Olá offline utilizando suportes de dados amovível.

9. No Olá **escolher opções de verificação de consistência** página, selecione como pretende que as verificações de consistência tooautomate. Pode escolher toorun uma verificação apenas quando os dados de réplica se tornar inconsistente, ou com base numa agenda. Se não quiser verificação de consistência automática tooconfigure, pode executar uma verificação manual em qualquer altura. toorun uma verificação manual, no Olá **proteção** área da Olá consola do administrador do servidor de cópia de segurança, faça duplo clique em proteção Olá grupo e, em seguida, selecione **efetuar verificação de consistência**.

10. Se selecionou tooback segurança toohello nuvem utilizando a cópia de segurança do Azure, no Olá **especificar dados da proteção Online** página, certifique-se de que seleciona as cargas de trabalho de Olá pretende tooback segurança tooAzure.

11. No Olá **Especificar agenda de cópia de segurança Online** página, selecione a frequência incrementais tooAzure irá ocorrer. Pode agendar cópias de segurança toorun cada dia, semana, mês e ano e selecione Olá data e a hora em que deve executar. As cópias de segurança podem ocorrer se tootwice por dia. Sempre que executa uma cópia de segurança, um ponto de recuperação de dados é criado no Azure a partir de cópia de Olá dos dados de cópia de segurança Olá armazenados no disco do servidor de cópia de segurança de Olá.

12. No Olá **especificar política de retenção Online** página, selecione a forma como pontos de recuperação de Olá criados a partir de cópias de segurança de Olá, diária, semanal, mensal e anual são mantidos no Azure.

13. No Olá **escolher Online replicação** página, selecione a forma como ocorre Olá completa a replicação inicial dos dados. Pode replicar rede Olá ou Efetue uma offline (offline seeding) de cópia de segurança. Cópia de segurança offline utiliza Olá funcionalidade Importar do Azure. Para obter mais informações, consulte [Offline fluxo de trabalho de cópia de segurança na cópia de segurança do Azure](backup-azure-backup-import-export.md).

14. No Olá **resumo** , reveja as suas definições. Depois de selecionar **criar grupo**, ocorre a replicação inicial dos dados de Olá. Quando a replicação de dados estiver concluído, no Olá **estado** página, é de estado do grupo de proteção de Olá **OK**. Cópia de segurança, em seguida, ocorre por proteção Olá definições do grupo.

## <a name="recover-system-state-or-bmr"></a>Recuperar o estado do sistema ou da BMR
Pode recuperar a BMR ou o sistema de localização de rede de tooa de estado. Se tiver criado cópias de segurança de BMR, utilize toostart de ambiente de recuperação do Windows (WinRE) do sistema e ligá-lo toohello rede. Em seguida, utilize toorecover de cópia de segurança do Windows Server a partir da localização de rede Olá. Se tiver uma cópia de segurança do Estado do sistema, utilize apenas toorecover de cópia de segurança do Windows Server de localização de rede Olá.

### <a name="restore-bmr"></a>Restaurar BMR
Execute uma recuperação no computador do servidor de cópia de segurança de Olá:

1.  No Olá **recuperação** painel, encontrar o computador de Olá pretende toorecover e, em seguida, selecione **recuperação bare-Metal**.

2.  Pontos de recuperação disponíveis são indicados a negrito no calendário Olá. Selecione Olá data e hora para ponto de recuperação de Olá que pretende que o toouse.

3.  No Olá **selecionar tipo de recuperação** página, selecione **copiar tooa pasta de rede.**

4.  No Olá **especificar destino** página, selecione onde pretende que toocopy Olá dados. Lembre-se de que destino selecionado de Olá tem toohave tenha espaço suficiente. Recomendamos que crie uma nova pasta.

5.  No Olá **especificar opções de recuperação** página, tooapply de definições de segurança de Olá selecione. Em seguida, selecione se pretende que a rede de área de armazenamento (SAN) de toouse-com base em instantâneos de hardware, para acelerar a recuperação. (Esta é uma opção apenas se tiver uma SAN com esta funcionalidade disponível e Olá toocreate de capacidade e dividir um toomake clone-gravável. In addition, hello computador protegido e o computador do servidor de cópia de segurança tem de ser ligado toohello mesma rede.)

6.  Configure opções de notificação. No Olá **confirmação** página, selecione **recuperar**.

Configure a localização da partilha Olá:

1.  Na localização do restauro Olá, aceda a pasta de toohello que tenha a cópia de segurança de Olá.

2.  Partilhe a pasta de Olá que é um nível acima de WindowsImageBackup para que hello raiz da pasta partilhada Olá seja a pasta WindowsImageBackup de Olá. Se não fizer isto, o restauro não irá localizar cópia de segurança de Olá. tooconnect utilizando o ambiente de recuperação do Windows (WinRE), precisa de uma partilha que pode aceder no WinRE com o endereço IP correto do Olá e as credenciais.

Restaure o sistema de Olá:

1.  Inicie computador Olá no qual pretende que toorestore Olá imagem utilizando Olá DVD do Windows para o sistema de Olá que está a restaurar.

2.  Na primeira página Olá, verifique as definições de idioma e região. No Olá **instalar** página, selecione **reparar o seu computador**.

3.  No Olá **opções de recuperação de sistema** página, selecione **restaurar o computador utilizando uma imagem do sistema que criou anteriormente**.

4.  No Olá **selecionar uma cópia de segurança de imagem de sistema** página, selecione **selecionar uma imagem de sistema** > **avançadas** > **pesquisa para um sistema imagem na rede de Olá**. Se aparecer um aviso, selecione **Sim**. Aceda toohello caminho de partilha, introduza as credenciais de Olá e, em seguida, selecione o ponto de recuperação de Olá. Esta ação procura cópias de segurança específicas que estão disponíveis nesse ponto de recuperação. Selecione o ponto de recuperação de Olá que pretende que o toouse.

5.  No Olá **escolha como toorestore Olá cópia de segurança** página, selecione **formatar e dividir discos**. Na página seguinte do Olá, verifique as definições. 

6.  Restauro do toobegin Olá, selecione **concluir**. É necessário um reinício.

### <a name="restore-system-state"></a>Restaurar estado do sistema

Execute recuperação no servidor de cópia de segurança:

1.  No Olá **recuperação** painel, localizar Olá computador que pretende toorecover e, em seguida, selecione **recuperação bare-Metal**.

2.  Pontos de recuperação disponíveis são indicados a negrito no calendário Olá. Selecione Olá data e hora para ponto de recuperação de Olá que pretende que o toouse.

3.  No Olá **selecionar tipo de recuperação** página, selecione **pasta de rede de tooa cópia**.

4.  No Olá **especificar destino** página, selecione onde pretende que toocopy Olá dados. Lembre-se de que destino selecionado de Olá tem espaço suficiente. Recomendamos que crie uma nova pasta.

5.  No Olá **especificar opções de recuperação** página, tooapply de definições de segurança de Olá selecione. Em seguida, selecione se pretende toouse instantâneos de hardware baseados em SAN para acelerar a recuperação. (Esta é uma opção apenas se tiver uma SAN com esta funcionalidade e Olá toocreate de capacidade e dividir um toomake clone-gravável. In addition, Olá computador protegido e o servidor de cópia de segurança tem de ser ligado toohello mesma rede.)

6.  Configure opções de notificação. No Olá **confirmação** página, selecione **recuperar**.

Execute cópia de segurança do Windows Server:

1.  Selecione **ações** > **recuperar** > **neste servidor** > **seguinte**.

2.  Selecione **outro servidor**, selecione Olá **especificar tipo de localização** página e, em seguida, selecione **remoto pasta partilhada**. Introduza Olá caminho toohello pasta que contém o ponto de recuperação Olá.

3.  No Olá **selecionar tipo de recuperação** página, selecione **estado do sistema**. 

4. No Olá **selecionar localização para recuperação do Estado do sistema** página, selecione **localização Original**.

5.  No Olá **confirmação** página, selecione **recuperar**. Após o restauro de Olá, reinicie o servidor de Olá.

6.  Também pode executar Olá restauro do Estado do sistema numa linha de comandos. toodo, iniciar a cópia de segurança do Windows Server no computador de Olá pretende toorecover. Identificador de versão Olá tooget, numa linha de comandos, introduza:```wbadmin get versions -backuptarget \<servername\sharename\>```

    Utilize Olá versão identificador toostart Olá Estado restauro do sistema. Na linha de comandos Olá, introduza:```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    Certifique-se de que pretende que a recuperação de Olá toostart. Pode ver que processo Olá na janela de linha de comandos Olá. É criado um registo do restauro. Após o restauro de Olá, reinicie o servidor de Olá.

