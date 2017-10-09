---
title: "aaaStart/parar VMs durante a solução de off-hours [pré-visualização] | Microsoft Docs"
description: "soluções de gestão de VM de Olá inicia, interrompe as Virtual Machines do Azure Resource Manager com base numa agenda e monitorizar proactivamente da análise de registos."
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Solução Iniciar/Parar VMs fora do horário comercial [Preview] na Automatização

Olá VMs de início/paragem durante a solução de off-hours [pré-visualização] inicia e interrompe as máquinas virtuais do Azure Resource Manager num agendamento definido pelo utilizador e fornece informações sobre o sucesso de Olá das tarefas de automatização de Olá que iniciar e parar as máquinas virtuais com o OMS Análise de registos.  

## <a name="prerequisites"></a>Pré-requisitos

- Olá runbooks trabalhar com um [conta Run As do Azure](automation-offering-get-started.md#authentication-methods).  Olá conta Run As é o método de autenticação de Olá preferido, uma vez que utiliza a autenticação de certificado em vez de uma palavra-passe que pode expirar ou alterado frequentemente.  

- Esta solução só pode gerir VMs no olá onde reside a conta de automatização de Olá mesma subscrição.  

- Esta solução implementa apenas toohello seguintes regiões do Azure - Sudeste da Austrália, EUA leste, Sudeste asiático e Europa Ocidental.  Olá runbooks que gerem a agenda VM Olá pode visar VMs em qualquer região.  

- notificações de correio eletrónico toosend quando Olá iniciar e parar runbooks VM completa, uma subscrição de classe empresarial do Office 365, é necessária.  

## <a name="solution-components"></a>Componentes da solução

Esta solução é constituído por Olá recursos que serão importados e adicionar a conta de automatização tooyour a seguir.

### <a name="runbooks"></a>Runbooks

Runbook | Descrição|
--------|------------|
CleanSolution-MS-Mgmt-VM | Este runbook removerá contidos todos os recursos e agendas quando acede a solução de Olá toodelete da sua subscrição.|  
SendMailO365-MS-Mgmt | Este runbook envia um e-mail através do Office 365 Exchange.|
StartByResourceGroup-MS-Mgmt-VM | Este runbook está toostart pretendido VMs (ambas as clássica e VMs de baseadas em ARM) que reside numa determinada lista de grupos de recursos do Azure.
StopByResourceGroup-MS-Mgmt-VM | Este runbook está toostop pretendido VMs (ambas as clássica e VMs de baseadas em ARM) que reside numa determinada lista de grupos de recursos do Azure.|
<br>

### <a name="variables"></a>Variáveis

Variável | Descrição|
---------|------------|
Runbook **SendMailO365-MS-Mgmt** ||
SendMailO365-IsSendEmail-MS-Mgmt | Especifica se os runbooks StartByResourceGroup-MS-Mgmt-VM e StopByResourceGroup-MS-Mgmt-VM podem enviar notificações por e-mail após a conclusão.  Selecione **verdadeiro** tooenable e **falso** toodisable alertas de e-mail. O valor predefinido é **Falso**.| 
**StartByResourceGroup-MS-Mgmt-VM** Runbook ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | Introduza VM nomes toobe excluído da operação de gestão Separe os nomes utilizando semi-colon(;) sem espaços. Os valores são sensíveis a maiúsculas e minúsculas e é suportado o caráter universal (asterisco).|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Texto que pode ser anexado toohello início do corpo de mensagem de correio eletrónico Olá.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Especifica o nome de Olá de Olá conta de automatização que contém Olá E-Mail runbook.  <seg>
  **Não modifique esta variável..**</seg>|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Especifica o nome de Olá de Olá e-mail runbook.  Isto é utilizado por Olá StartByResourceGroup-MS-Mgmt-VM e o e-mail de toosend StopByResourceGroup-MS-Mgmt-VM runbooks.  <seg>
  **Não modifique esta variável..**</seg>|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Especifica o nome de Olá Olá do grupo de recursos que contém Olá E-Mail runbook.  <seg>
  **Não modifique esta variável..**</seg>|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Especifica o texto de Olá de linha de assunto Olá de e-mail Olá.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Especifica Olá destinatários de e-mail Olá.  Introduza os nomes separados utilizando semi-colon(;) sem espaços.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Introduza VM nomes toobe excluído da operação de gestão Separe os nomes utilizando semi-colon(;) sem espaços. Os valores são sensíveis a maiúsculas e minúsculas e é suportado o caráter universal (asterisco).  Valor predefinido (asterisco) irá incluir todos os grupos de recursos na subscrição Olá.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Especifica a subscrição de Olá que contém toobe de VMs gerida por esta solução.  Tem de ser Olá mesma subscrição onde reside Olá conta de automatização desta solução.|
Runbook **StopByResourceGroup-MS-Mgmt-VM** ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Introduza VM nomes toobe excluído da operação de gestão Separe os nomes utilizando semi-colon(;) sem espaços. Os valores são sensíveis a maiúsculas e minúsculas e é suportado o caráter universal (asterisco).|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Texto que pode ser anexado toohello início do corpo de mensagem de correio eletrónico Olá.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Especifica o nome de Olá de Olá conta de automatização que contém Olá E-Mail runbook.  <seg>
  **Não modifique esta variável..**</seg>|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Especifica o nome de Olá Olá do grupo de recursos que contém Olá E-Mail runbook.  <seg>
  **Não modifique esta variável..**</seg>|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Especifica o texto de Olá de linha de assunto Olá de e-mail Olá.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Especifica Olá destinatários de e-mail Olá.  Introduza os nomes separados utilizando semi-colon(;) sem espaços.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Introduza VM nomes toobe excluído da operação de gestão Separe os nomes utilizando semi-colon(;) sem espaços. Os valores são sensíveis a maiúsculas e minúsculas e é suportado o caráter universal (asterisco).  Valor predefinido (asterisco) irá incluir todos os grupos de recursos na subscrição Olá.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Especifica a subscrição de Olá que contém toobe de VMs gerida por esta solução.  Tem de ser Olá mesma subscrição onde reside Olá conta de automatização desta solução.|  
<br>

### <a name="schedules"></a>Agendas

Agenda | Descrição|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | Agendamento do runbook StartByResourceGroup, que efetua o arranque de Olá de VMs geridas por esta solução. Quando criada, será assumida tooUTC fuso horário.|
StopByResourceGroup-Schedule-MS-Mgmt | Agendamento do runbook StopByResourceGroup, que executa o encerramento de Olá de VMs geridas por esta solução. Quando criada, será assumida tooUTC fuso horário.|

### <a name="credentials"></a>Credenciais

Credencial | Descrição|
-----------|------------|
O365Credential | Especifica um e-mail de toosend conta de utilizador do válido do Office 365.  Apenas necessário se variável SendMailO365-IsSendEmail-MS-Mgmt estiver definido demasiado**verdadeiro**.

## <a name="configuration"></a>Configuração

Execute os seguintes passos tooadd Olá iniciar/parar VMs durante off-hours [pré-visualização] solução tooyour conta de automatização de Olá e, em seguida, configurar a solução de Olá Olá variáveis toocustomize.

1. A partir da Olá home ecrã no Olá portal do Azure, selecione Olá **Marketplace** mosaico.  Se o mosaico Olá já não consta tooyour afixado home ecrã, a partir do painel de navegação esquerdo Olá, selecione **novo**.  
2. No painel de Marketplace Olá, escreva **iniciar VM** na caixa de pesquisa de Olá e a solução de Olá, em seguida, selecione **VMs de início/paragem durante off-hours [pré-visualização]** de resultados da pesquisa Olá.  
3. No Olá **VMs de início/paragem durante off-hours [pré-visualização]** painel Olá selecionado solução, reveja as informações de resumo de Olá e, em seguida, clique em **criar**.  
4. Olá **Adicionar solução** é apresentado o painel onde são tooconfigure pedido Olá solução antes de importá-lo na sua subscrição de automatização.<br><br> ![Painel Adicionar Solução de Gestão de VMs](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  No Olá **Adicionar solução** painel, selecione **área de trabalho** e aqui selecionou uma área de trabalho do OMS toohello ligado Olá conta de automatização mesma subscrição do Azure está a ser ou criar uma nova área de trabalho do OMS.  Se não tiver uma área de trabalho do OMS, pode selecionar **criar nova área de trabalho** e no Olá **área de trabalho OMS** painel efetuar o seguinte Olá: 
   - Especifique um nome para o novo Olá **área de trabalho OMS**.
   - Selecione um **subscrição** toolink tooby selecionando Olá na lista pendente se predefinido Olá selecionado não é adequado.
   - Em **Grupo de Recursos**, pode criar um grupo de recursos novos ou selecionar um já existente.  
   - Selecione uma **Localização**.  Atualmente são localizações apenas Olá fornecidas para a seleção **Sudeste da Austrália**, **EUA Leste**, **Sudeste asiático**, e **Europa Ocidental**.
   - Selecione um **Escalão de preço**.  solução Olá é oferecida na duas camadas: livre e OMS paga camada.  escalão gratuito Olá tem um limite na quantidade de Olá dos dados recolhidos por dia, o período de retenção e minutos de tempo de execução de tarefa de runbook.  Olá OMS paga camada não tem um limite na quantidade de Olá dos dados recolhidos diariamente.  

        > [!NOTE]
        > Enquanto Olá autónomo paga camada é apresentado como uma opção, não é aplicável.  Se selecioná-lo e continuar com a criação de Olá desta solução na sua subscrição, irá falhar.  Esta opção será contemplada quando a solução for lançada oficialmente.<br>Se utilizar esta solução, a mesma só vai utilizar minutos de trabalhos de automatização e ingestão de registos.  solução Olá não adiciona o ambiente de tooyour de nós OMS adicional.  

6. Depois de fornecer informações de Olá necessário no Olá **área de trabalho OMS** painel, clique em **criar**.  Enquanto as informações de Olá são verificadas e área de trabalho Olá é criada, pode controlar o progresso em **notificações** menu Olá.  Vai ser devolvido toohello **Adicionar solução** painel.  
7. No Olá **Adicionar solução** painel, selecione **conta de automatização**.  Se estiver a criar uma nova área de trabalho do OMS, será necessário tooalso criar uma nova conta de automatização que será associada Olá nova área de trabalho OMS especificada anteriormente, incluindo a sua subscrição do Azure, o grupo de recursos e a região.  Pode selecionar **criar uma conta de automatização** e no Olá **conta de automatização adicionar** painel, fornece Olá seguinte: 
  - No Olá **nome** campo, introduza o nome de Olá de Olá conta de automatização.

    Todas as outras opções são preenchidas automaticamente com base na área de trabalho do OMS Olá selecionada e estas opções não podem ser modificadas.  Uma conta Run As do Azure é o método de autenticação predefinido Olá para runbooks Olá incluídos nesta solução.  Assim que clicar em **OK**, opções de configuração de Olá são validadas e Olá conta de automatização é criada.  Pode controlar o progresso em **notificações** menu Olá. 

    Caso contrário, pode selecionar uma conta Run As de Automatização existente.  Tenha em atenção que a conta Olá que selecionar já não pode ser ligado tooanother área de trabalho do OMS, caso contrário, uma mensagem será apresentada no Olá painel tooinform.  Se já estiver ligado, será necessário tooselect uma conta Run As de automatização diferente ou crie um novo.<br><br> ![Automatização conta já ligado tooOMS área de trabalho](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Por fim no Olá **Adicionar solução** painel, selecione **configuração** e Olá **parâmetros** é apresentado o painel.  No Olá **parâmetros** painel, precisará de:  
   - Especifique Olá **nomes ResourceGroup de destino**, que é um nome de grupo de recursos que contém toobe de VMs gerida por esta solução.  Pode introduzir mais de um nome e separá-los por ponto e vírgula (os valores são sensíveis a maiúsculas e minúsculas).  Utilizar um caráter universal é suportado se quiser tootarget VMs em todos os grupos de recursos na subscrição Olá.
   - Selecione um **agenda** que é uma periódica data e hora para iniciar e parar Olá da VM no Olá os grupos de recursos de destino.  Por predefinição, o agendamento de Olá está configurado toohello UTC fuso horário e selecionar uma região diferente não está disponível.  Se desejar tooconfigure Olá tooyour específico fuso horário de agenda depois de configurar a solução de Olá, consulte [Modifying de agendamento de arranque e encerramento de Olá](#modifying-the-startup-and-shutdown-schedule) abaixo.    

10. Depois de Concluir configuração Olá inicial de definições necessárias para a solução de Olá, selecione **criar**.  Todas as definições serão validadas e, em seguida, a tentativa de solução de Olá toodeploy na sua subscrição.  Este processo pode demorar vários segundos toocomplete e pode controlar o progresso em **notificações** menu Olá. 

## <a name="collection-frequency"></a>Frequência da recolha

Automatização registo e a tarefa de fluxo dados da tarefa é ingeridos no repositório OMS Olá a cada cinco minutos.  

## <a name="using-hello-solution"></a>Utilizar a solução de Olá

Quando adiciona a solução de gestão de VM de Olá, no seu Olá de área de trabalho do OMS **StartStopVM vista** mosaico será adicionado tooyour dashboard do OMS.  Este mosaico mostra uma contagem e a representação gráfica de tarefas de runbooks Olá para a solução de Olá que foram iniciadas e concluiu com êxito.<br><br> ![Mosaico Vista StartStopVM da Gestão de VMs](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

Na sua conta de automatização, pode aceder e gerir soluções de Olá selecionando Olá **soluções** mosaico e, em seguida, Olá **soluções** painel, selecionar solução Olá **[início-Stop-VM Área de trabalho]** da lista de Olá.<br><br> ![Lista de Soluções de Automatização](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Selecionar solução Olá apresentará Olá **Start-Stop-VM [área de trabalho]** painel de solução, onde poderá consultar detalhes importantes, tais como Olá **StartStopVM** na peça de mosaico, como a área de trabalho do OMS, que Mostra uma contagem e a representação gráfica de tarefas de runbooks Olá para a solução de Olá que foram iniciadas e concluiu com êxito.<br><br> ![Painel de Solução de VM de Automatização](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

Aqui pode também abrir a área de trabalho do OMS e efetuar a análise de registos de tarefa Olá.  Basta clicar **todas as definições**e em Olá **definições** painel, selecione **início rápido** e, em seguida, no Olá **início rápido** selecione painel  **Portal do OMS**.   Isto vai abrir um novo separador ou nova sessão do browser e apresentar a área de trabalho OMS associada à sua conta de automatização e subscrição.  


### <a name="configuring-e-mail-notifications"></a>Configurar as notificações por e-mail

notificações de correio eletrónico tooenable quando hello iniciar e parar runbooks VM concluída, terá de toomodify Olá **O365Credential** de credenciais e, no mínimo, Olá seguintes variáveis:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

Olá tooconfigure **O365Credential** credencial, execute Olá os seguintes passos:

1. Da sua conta de automatização, clique em **todas as definições** em Olá parte superior da janela de Olá. 
2. No Olá **definições** painel na secção de Olá **recursos de automatização**, selecione **ativos**. 
3. No Olá **ativos** painel, selecione de Olá **credencial** mosaico e Olá **credencial** painel, selecione de Olá **O365Credential**.  
4. Introduza um nome de utilizador válido do Office 365 e a palavra-passe e, em seguida, clique em **guardar** toosave as suas alterações.  

variáveis de Olá tooconfigure realçadas anteriormente, execute Olá os seguintes passos:

1. Da sua conta de automatização, clique em **todas as definições** em Olá parte superior da janela de Olá. 
2. No Olá **definições** painel na secção de Olá **recursos de automatização**, selecione **ativos**. 
3. No Olá **ativos** painel, selecione de Olá **variáveis** mosaico e Olá **variáveis** painel, selecione de variável Olá listado acima e, em seguida, modifique o valor seguinte Olá descrição para o mesmo especificado no Olá [variável](##variables) secção anterior.  
4. Clique em **guardar** variável de toohello toosave Olá alterações.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Agenda modificação de arranque e encerramento de Olá

Gestão Olá arranque e encerramento agenda nesta solução segue Olá mesmos passos conforme descritos em [agendar um runbook na automatização do Azure](automation-schedules.md).  Lembre-se de que não é possível modificar a configuração de agenda de Olá.  Terá de toodisable Olá agenda existente e, em seguida, crie um novo e, em seguida, ligue toohello **StartByResourceGroup-MS-Mgmt-VM** ou **StopByResourceGroup-MS-Mgmt-VM** runbook que pretende que o Olá Agende tooapply para.   

## <a name="log-analytics-records"></a>Registos do Log Analytics

Automatização cria dois tipos de registos no repositório do Olá OMS.

### <a name="job-logs"></a>Registos de trabalhos

Propriedade | Descrição|
----------|----------|
Autor da chamada |  Quem iniciou a operação de Olá.  Os valores possíveis são um endereço de e-mail ou o sistema para trabalhos agendados.|
Categoria | Classificação do tipo de Olá de dados.  Para automatização, o valor de Olá é JobLogs.|
CorrelationId | GUID que é Olá Id de correlação da tarefa de runbook Olá.|
JobId | GUID que é Olá Id da tarefa de runbook Olá.|
operationName | Especifica o tipo de Olá da operação efetuada no Azure.  Para automatização, o valor de Olá será tarefa.|
resourceId | Especifica o tipo de recurso Olá no Azure.  Para automatização, o valor de Olá é a conta de automatização de Olá associada Olá runbook.|
ResourceGroup | Especifica o nome do grupo de recursos Olá da tarefa de runbook Olá.|
ResourceProvider | Especifica Olá serviço Azure que fornece recursos de Olá, pode implementar e gerir.  Para automatização, o valor de Olá é automatização do Azure.|
ResourceType | Especifica o tipo de recurso Olá no Azure.  Para automatização, o valor de Olá é a conta de automatização de Olá associada Olá runbook.|
resultType | Estado da tarefa de runbook Olá Olá.  Os valores possíveis são:<br>- Iniciado<br>- Parado<br>- Suspenso<br>- Falhado<br>- Bem-sucedido|
resultDescription | Descreve o estado de resultado da tarefa de runbook de Olá.  Os valores possíveis são:<br>- Trabalho iniciado<br>- Trabalho falhado<br>- Trabalho Concluído|
RunbookName | Especifica o nome de Olá de Olá runbook.|
SourceSystem | Especifica o sistema de origem Olá para dados de Olá submetidos.  Para automatização, o valor de Olá será: OpsManager|
StreamType | Especifica o tipo de Olá de evento. Os valores possíveis são:<br>- Verboso<br>- Saída<br>- Erro<br>- Aviso|
SubscriptionId | Especifica o ID de subscrição de Olá da tarefa de Olá.
Hora | Data e hora quando executar a tarefa de runbook Olá.|


### <a name="job-streams"></a>Fluxos de trabalho

Propriedade | Descrição|
----------|----------|
Autor da chamada |  Quem iniciou a operação de Olá.  Os valores possíveis são um endereço de e-mail ou o sistema para trabalhos agendados.|
Categoria | Classificação do tipo de Olá de dados.  Para automatização, o valor de Olá é JobStreams.|
JobId | GUID que é Olá Id da tarefa de runbook Olá.|
operationName | Especifica o tipo de Olá da operação efetuada no Azure.  Para automatização, o valor de Olá será tarefa.|
ResourceGroup | Especifica o nome do grupo de recursos Olá da tarefa de runbook Olá.|
resourceId | Especifica o Id do recurso Olá no Azure.  Para automatização, o valor de Olá é a conta de automatização de Olá associada Olá runbook.|
ResourceProvider | Especifica Olá serviço Azure que fornece recursos de Olá, pode implementar e gerir.  Para automatização, o valor de Olá é automatização do Azure.|
ResourceType | Especifica o tipo de recurso Olá no Azure.  Para automatização, o valor de Olá é a conta de automatização de Olá associada Olá runbook.|
resultType | resultado de Olá da tarefa de runbook Olá no evento do Olá tempo Olá foi gerado.  Os valores possíveis são:<br>- InProgress|
resultDescription | Inclui o fluxo de saída de Olá do runbook Olá.|
RunbookName | nome de Olá de Olá runbook.|
SourceSystem | Especifica o sistema de origem Olá para dados de Olá submetidos.  Para automatização, o valor de Olá será OpsManager|
StreamType | tipo de Olá do fluxo de trabalho. Os valores possíveis são:<br>- Em Curso<br>- Saída<br>- Aviso<br>- Erro<br>- Depuração<br>- Verboso|
Hora | Data e hora quando executar a tarefa de runbook Olá.|

Quando efetuar qualquer pesquisa de registo que devolve os registos da categoria de **JobLogs** ou **JobStreams**, pode selecionar Olá **JobLogs** ou **JobStreams** vista que apresenta um conjunto de mosaicos resumir atualizações Olá devolvidas pela pesquisa de Olá.

## <a name="sample-log-searches"></a>Pesquisas de registo de exemplo

Olá tabela seguinte fornece pesquisas de registo de exemplo para registos de tarefa recolhidos por esta solução. 

Consulta | Descrição|
----------|----------|
Localizar trabalhos para o runbook StartVM que foram concluídos com êxito | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
Localizar trabalhos para o runbook StopVM que foram concluídos com êxito | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
Mostrar estado do trabalho ao longo do tempo para runbooks StartVM e StopVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Remover solução Olá

Se decidir que deixar de precisar solução de Olá toouse qualquer mais, podem eliminá-la Olá conta de automatização.  A eliminar a solução de Olá só irá remover runbooks Olá, não eliminará as agendas de Olá ou variáveis que foram criadas quando solução Olá foi adicionada.  Esses recursos, terá de toodelete manualmente se não estiver a utilizá-los com outros runbooks.  

toodelete Olá solução, execute Olá os seguintes passos:

1.  A partir da sua conta de automatização, selecione Olá **soluções** mosaico.  
2.  No Olá **soluções** painel, solução de Olá selecione **Start-Stop-VM [área de trabalho]**.  No Olá **VMManagementSolution [área de trabalho]** painel, de Olá menu clique **eliminar**.<br><br> ![Eliminar a solução de gestão VM](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  No Olá **Eliminar solução** janela, confirme que pretende que a solução de Olá toodelete.
4.  Enquanto as informações de Olá são verificadas e solução Olá é eliminada, pode controlar o progresso em **notificações** menu Olá.  Vai ser devolvido toohello **VMManagementSolution [área de trabalho]** painel depois do início da solução de tooremove Olá processo.  

conta de automatização Olá e área de trabalho OMS não são eliminados como parte deste processo.  Se não pretender que a área de trabalho OMS de Olá tooretain, terá de toomanually eliminá-lo.  Isto pode ser conseguido também de Olá portal do Azure.   A partir da Olá home ecrã no Olá portal do Azure, selecione **Log Analytics** e, em seguida, no Olá **Log Analytics** painel, área de trabalho Olá selecione e clique em **eliminar** no menu Olá Painel de definições da área de trabalho de Olá.  
      
## <a name="next-steps"></a>Passos seguintes

- toolearn mais informações sobre como consultas de pesquisa diferentes tooconstruct e revisão Olá automatização tarefa registos de análise de registos, consulte [pesquisas de registo na análise de registos](../log-analytics/log-analytics-log-searches.md)
- mais sobre a execução do runbook, como as tarefas de runbook toomonitor e outros detalhes técnicos, consulte toolearn [controlar uma tarefa de runbook](automation-runbook-execution.md)
- toolearn mais informações sobre a análise de registos do OMS e origens de recolha de dados, consulte [dados de armazenamento do Azure recolha na descrição geral da análise de registos](../log-analytics/log-analytics-azure-storage.md)






   

