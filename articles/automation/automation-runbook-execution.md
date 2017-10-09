---
title: "execução de aaaRunbook na automatização do Azure | Microsoft Docs"
description: "Descreve os detalhes de Olá da forma como é processado um runbook na automatização do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Execução do Runbook na automatização do Azure
Quando inicia um runbook na automatização do Azure, é criada uma tarefa. Uma tarefa é uma instância de execução individual de um runbook. Uma automatização do Azure é de trabalho atribuídos toorun cada tarefa. Enquanto trabalhadores são partilhados por várias contas do Azure, a diferentes contas de automatização de tarefas estão isoladas entre si. Não têm controlo sobre o pedido de Olá de serviços de trabalho para a tarefa.  Um único runbook pode ter várias tarefas em execução em simultâneo. Quando visualiza lista Olá de runbooks no portal do Azure de Olá, lista Estado Olá de todas as tarefas que foram iniciadas para cada runbook. Pode ver a lista de Olá de tarefas para cada runbook ordem tootrack Olá do Estado de cada. Para uma descrição dos Estados de tarefa diferente Olá, consulte [Estados das tarefas](#job-statuses).

Olá diagrama seguinte mostra Olá ciclo de vida de uma tarefa de runbook para [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) e [runbooks do fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).

![Estados - tarefa do fluxo de trabalho do PowerShell](./media/automation-runbook-execution/job-statuses.png)

Olá diagrama seguinte mostra Olá ciclo de vida de uma tarefa de runbook para [runbooks do PowerShell](automation-runbook-types.md#powershell-runbooks).

![Estados de tarefa - o Script do PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

As tarefas têm acesso tooyour Azure recursos ao tornar um tooyour ligação de subscrição do Azure. Apenas têm acesso tooresources no seu centro de dados se não estiverem acessíveis a partir da nuvem pública Olá esses recursos.

## <a name="job-statuses"></a>Estados das tarefas
Olá tabela seguinte descreve Olá diferentes Estados possíveis das tarefas.

| Estado | Descrição |
|:--- |:--- |
| Foi concluída |tarefa de Olá foi concluída com êxito. |
| Falha |Para [runbooks gráfico e o fluxo de trabalho do PowerShell](automation-runbook-types.md), Olá runbook falha toocompile.  Para [runbooks de Script do PowerShell](automation-runbook-types.md), Olá runbook falha toostart ou tarefa de Olá encontrou uma exceção. |
| Falha ao aguardar a recursos |Falha na tarefa de Olá porque atingiu Olá [fração justa](#fairshare) limitar três vezes e iniciado a partir do Olá mesmo ponto de verificação ou de Olá hora de início do runbook Olá cada. |
| Em fila |Olá tarefa está aguardar recursos num toocome de trabalho de automatização disponível para que as que possa ser iniciado. |
| A Iniciar |Olá tarefa foi atribuída tooa worker e sistema de Olá está no processo de Olá de iniciá-lo. |
| A retomar |sistema de Olá está no processo de Olá de retomar a tarefa de Olá depois foi suspenso. |
| A Executar |tarefa de Olá está em execução. |
| Aguardar execução, dos recursos |Olá tarefa foi descarregada porque atingiu Olá [fração justa](#fairshare) limite. Retoma em breve a partir do último ponto de verificação. |
| Parada |tarefa de Olá foi interrompida pelo utilizador Olá antes de estar concluído. |
| A Parar |sistema de Olá está no processo de Olá de parar a tarefa de Olá. |
| Suspenso |tarefa de Olá foi suspensa pelo utilizador Olá, pelo sistema Olá ou por um comando no runbook Olá. Uma tarefa suspensa pode ser iniciada novamente e retomar a partir do último ponto de verificação ou de Olá a partir do runbook Olá se não tem pontos de verificação. Olá runbook apenas será suspenso pelo sistema Olá quando ocorre uma exceção. Por predefinição, ErrorActionPreference estiver definido demasiado**continuar**, que significa que essa tarefa Olá mantém em execução no erro. Se esta variável de preferência estiver definido demasiado**parar**, em seguida, a tarefa de Olá suspende a um erro.  Aplica-se demasiado[runbooks gráfico e o fluxo de trabalho do PowerShell](automation-runbook-types.md) apenas. |
| A suspensão |sistema de Olá está a tentar tarefa de Olá toosuspend no pedido de Olá do utilizador Olá. Olá runbook tem de atingir o próximo ponto de verificação antes de poder ser suspenso. Se já passado o último ponto de verificação, em seguida, concluir antes de poder ser suspenso.  Aplica-se demasiado[runbooks gráfico e o fluxo de trabalho do PowerShell](automation-runbook-types.md) apenas. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Visualizar o estado da tarefa de Olá portal do Azure
Pode ver um Estado de todas as tarefas de runbook resumido ou explorar detalhes de uma tarefa de runbook específico Olá portal do Azure ou ao configurar a integração com o estado de tarefa runbook de tooforward de área de trabalho de análise de registos do Microsoft Operations Management Suite (OMS) e fluxos de trabalho.  Para obter mais informações sobre a integração com a análise de registos do OMS, consulte [reencaminhar o estado da tarefa e fluxos de trabalho de automatização tooLog análise (OMS)](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Tarefas de runbook de automatização resumidas
No Olá direito da sua conta de automatização selecionada, pode ver um resumo de todas as tarefas de runbook Olá para uma conta de automatização selecionada em **estatísticas de tarefa** mosaico.<br><br> ![Mosaico de estatísticas de tarefa](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Este mosaico mostra uma contagem e a representação gráfica do Estado da tarefa Olá para todas as tarefas executadas.  

Clicar num mosaico Olá apresenta Olá **tarefas** painel, que inclui uma lista resumida de todas as tarefas executadas, com estado, execução da tarefa e os tempos de início e de conclusão.<br><br> ![Painel de tarefas de conta de automatização](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  Pode filtrar a lista de Olá de tarefas, selecionando **filtre as tarefas** e filtrar por um runbook específico, o estado da tarefa, ou de Olá na lista pendente, Olá toosearch de intervalo de data/hora dentro do.<br><br> ![Estado da tarefa de filtro](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Em alternativa, pode ver detalhes de resumo da tarefa para um runbook específico, selecionando esse runbook Olá **Runbooks** painel na sua conta de automatização e, em seguida, selecione de Olá **tarefas** mosaico.  Isto apresenta Olá **tarefas** painel, e a partir daí pode clicar em Olá tarefa registo tooview os detalhes e saída.<br><br> ![Painel de tarefas de conta de automatização](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Resumo da Tarefa
Pode ver uma lista de todas as tarefas de Olá que foram criadas para um determinado runbook e o respetivo estado mais recente. Pode filtrar esta lista por Estado da tarefa e intervalo de Olá de datas para Olá última alteração toohello tarefa. tooview respetivo informações detalhadas e de saída, clique no nome de Olá de uma tarefa. Olá vista detalhada da tarefa de Olá inclui Olá os valores de parâmetros do runbook Olá fornecidas toothat tarefa.

Pode utilizar Olá seguintes tarefas de Olá tooview passos de um runbook.

1. No portal do Azure Olá, selecione **automatização** e, em seguida, selecione o nome de Olá de uma conta de automatização.
2. A partir do hub de Olá, selecione **Runbooks** e, em seguida, no Olá **Runbooks** painel selecionar um runbook Olá lista.
3. No painel Olá runbook Olá selecionado, clique em Olá **tarefas** mosaico.
4. Clique dos trabalhos de Olá na lista de Olá e no painel de detalhes da tarefa de runbook de Olá pode ver os detalhes e saída.

## <a name="retrieving-job-status-using-windows-powershell"></a>Obter o estado da tarefa com o Windows PowerShell
Pode utilizar Olá [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) tarefas de Olá tooretrieve criadas para um runbook e Olá obter detalhes sobre uma tarefa específica. Se iniciar um runbook do Windows PowerShell com [início AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx), em seguida, devolve tarefa resultante Olá. Utilize [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)tooget de saída de uma tarefa de saída do.

Olá comandos de exemplo seguintes obter a última tarefa de Olá para um runbook de exemplo e apresenta o respetivo estado, os valores de Olá fornecidos para os parâmetros do runbook de Olá e Olá o resultado da tarefa de Olá.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>Fração justa
Ordem tooshare recursos entre todos os runbooks na nuvem de Olá o automatização do Azure descarregará temporariamente todas as tarefas depois tem estado em execução para a três horas.  Durante este tempo, as tarefas de [runbooks baseados em PowerShell](automation-runbook-types.md#powershell-runbooks) estão parados e não será reiniciado.  Olá, estado de tarefa mostrar **parado**.  Este tipo de runbook é sempre reiniciado desde o início de Olá, uma vez que não suportam a pontos de verificação.  

[Os runbooks do PowerShell fluxo de trabalho baseada em](automation-runbook-types.md#powershell-workflow-runbooks) será possível retomar a partir da sua última [ponto de verificação](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Depois de executar a três horas, será possível suspender a tarefa de runbook Olá pelo serviço de Olá e o respetivo estado mostra **em execução, aguardar recursos**.  Quando uma sandbox fica disponível, Olá runbook será reiniciado automaticamente pelo serviço de automatização de Olá e retoma a partir do último ponto de verificação Olá.  Este é o comportamento normal do fluxo de trabalho do PowerShell para suspender/reinício.  Se Olá runbook novo exceder três horas do tempo de execução, repete o processo de Olá, cópia de segurança toothree vezes.  Após o reinício terceiro Olá, se o runbook Olá ainda não foi concluída em três horas, em seguida, falha na tarefa de runbook Olá e mostra o estado da tarefa Olá **falha, aguardar recursos**.  Neste caso, receberá Olá seguinte exceção com falha de Olá.

*tarefa de Olá não é possível continuar a ser executada porque este foi expulso repetidamente de Olá mesmo ponto de verificação. Certifique-se que o Runbook não efetua operações demoradas sem a persistência de estado.*

Este é o serviço de Olá de tooprotect a execução de runbooks indefinidamente sem concluir, dado que não fazem toomake consegue-toohello próximo ponto de verificação sem a ser descarregado novamente.

Se o runbook de Olá possui sem pontos de verificação ou tarefa Olá tinha não aceder ao ponto de verificação primeiro Olá antes de a ser descarregado, em seguida, esta reiniciar desde o início de Olá.  

Quando criar um runbook, deve garantir que toorun de tempo de Olá quaisquer atividades entre dois pontos de verificação não pode exceder a três horas. Poderá ser necessário tooadd pontos de verificação tooyour runbook tooensure que não atingiu o limite de três horas ou dividir longa executar operações. Por exemplo, o runbook pode executar um reindex numa grande base de dados do SQL Server. Se esta operação única não for concluída dentro do Olá justa partilha limite, em seguida, a tarefa de Olá é descarregado e reiniciar a partir do início de Olá. Neste caso, deve dividir operação de reindex Olá em vários passos, tais como reindexing uma tabela de cada vez e, em seguida, insira um ponto de verificação após cada operação de modo a que hello tarefa foi retomada após Olá última operação toocomplete.

## <a name="next-steps"></a>Passos seguintes
* toolearn mais informações sobre os diferentes métodos de Olá que podem ser utilizado toostart um runbook na automatização do Azure, consulte [iniciar um runbook na automatização do Azure](automation-starting-a-runbook.md)

