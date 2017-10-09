---
title: "aaaAzure métricas de Monitor - métricas suportadas por tipo de recurso | Microsoft Docs"
description: "Lista de haver métricas disponíveis para cada tipo de recurso com a monitorização do Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Métricas suportadas com a monitorização do Azure
Monitor do Azure fornece várias formas toointeract com métricas, incluindo charting-las no portal de Olá, aceder às mesmas através da REST API de Olá ou consultá-los utilizando o PowerShell ou a CLI. Segue-se uma lista completa de todas as métricas atualmente disponíveis no pipeline de métrico do Monitor do Azure.

> [!NOTE]
> Outras métricas poderão estar disponíveis no portal de Olá ou com APIs de legado. Esta lista inclui apenas métricas de pré-visualização pública disponíveis através de Olá pré-visualização pública do pipeline de métrico de Monitor de Azure Olá consolidado.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|qpu_metric|QPU|Contagem|Média|QPU. Intervalo de 0-100 para S1, 0-200 para S2 e 0-400 para S4|
|memory_metric|Memória|Bytes|Média|Memória. No intervalo 0-25 GB para S1, 0 a 50 GB para S2 e 0-100 GB para S4|
|TotalConnectionRequests|Pedidos de ligação total|Contagem|Média|Pedidos de ligação total. Estes são arrivals.|
|SuccessfullConnectionsPerSec|Ligações com êxito por seg|CountPerSecond|Média|Taxa de conclusões de ligação com êxito.|
|TotalConnectionFailures|Falhas de ligação total|Contagem|Média|Total de tentativas de ligação falhadas.|
|CurrentUserSessions|Sessões de utilizador atual|Contagem|Média|Número atual de sessões de utilizador estabelecida.|
|QueryPoolBusyThreads|Threads de ocupado de conjunto de consulta|Contagem|Média|Número de threads ocupados no conjunto de threads de consulta Olá.|
|CommandPoolJobQueueLength|Comprimento de fila de tarefa de conjunto de comandos|Contagem|Média|Número de tarefas numa fila de Olá do conjunto de threads de comando Olá.|
|ProcessingPoolJobQueueLength|Comprimento de fila de tarefa de conjunto de processamento|Contagem|Média|Número de tarefas não-I/O na fila de Olá de Olá conjunto de threads de processamento.|
|CurrentConnections|Ligação: Ligações atuais|Contagem|Média|Número atual de ligações de cliente estabelecido.|
|CleanerCurrentPrice|Memória: Preço atual de limpeza|Contagem|Média|Preço atual de memória, $/ byte/hora, too1000 normalizado.|
|CleanerMemoryShrinkable|Memória: Memória de limpeza que possam ser encolhida|Bytes|Média|Quantidade de memória, em bytes, assunto toopurging por fundo Olá limpeza.|
|CleanerMemoryNonshrinkable|Memória: Memória nonshrinkable de limpeza|Bytes|Média|Quantidade de memória, em bytes, não requerente toopurging por fundo Olá limpeza.|
|MemoryUsage|Memória: Utilização de memória|Bytes|Média|Utilização de memória de processo do servidor Olá como utilizado para calcular preço de memória de limpeza. Igual a toocounter Process\PrivateBytes plus Olá tamanho dos dados de mapeamento de memória, ignorando quaisquer memória que foi mapeada ou atribuída pelo Olá xVelocity análise na memória motor (VertiPaq) que excedam o motor de xVelocity Olá limite de memória.|
|MemoryLimitHard|Memória: Disco rígido de limite de memória|Bytes|Média|Limite de memória de disco rígido, ficheiro de configuração.|
|MemoryLimitHigh|Memória: Limite de memória elevada|Bytes|Média|Limite de memória elevada, ficheiro de configuração.|
|MemoryLimitLow|Memória: Baixa de limite de memória|Bytes|Média|Limite de memória insuficiente, ficheiro de configuração.|
|MemoryLimitVertiPaq|Memória: VertiPaq de limite de memória|Bytes|Média|Limite de memória, ficheiro de configuração.|
|Quota|Memória: Quota|Bytes|Média|Quota atual de memória, em bytes. Quota de memória também é conhecido como uma reserva de memória ou de concessão de memória.|
|QuotaBlocked|Memória: Quota bloqueado|Contagem|Média|Número atual de pedidos de quota são bloqueada até que outros quotas de memória são libertadas.|
|VertiPaqNonpaged|Memória: VertiPaq na memória não paginável|Bytes|Média|Bytes de memória bloqueado no conjunto de trabalho de Olá para utilização por motor dentro da memória de Olá.|
|VertiPaqPaged|Memória: VertiPaq bloco paginado|Bytes|Média|Bytes de memória paginada em utilização para dados em memória.|
|RowsReadPerSec|Processamento: Linhas lidas por seg|CountPerSecond|Média|Taxa de linhas lida todas as bases de dados relacionais.|
|RowsConvertedPerSec|Processamento: Converter o linhas por seg|CountPerSecond|Média|Taxa de linhas converter durante o processamento.|
|RowsWrittenPerSec|Processamento: Linhas escritas por seg|CountPerSecond|Média|Taxa de linhas escritos durante o processamento.|
|CommandPoolBusyThreads|Threads: Threads ocupado do conjunto de comandos|Contagem|Média|Número de threads ocupados no conjunto de threads de comando Olá.|
|CommandPoolIdleThreads|Threads: Threads de inatividade do conjunto de comandos|Contagem|Média|Número de threads Inativos no conjunto de threads de comando Olá.|
|LongParsingBusyThreads|Threads: Análise de threads ocupados de longa|Contagem|Média|Número de threads ocupados no Olá longa analisar o conjunto de threads.|
|LongParsingIdleThreads|Threads: Longa análise threads Inativos|Contagem|Média|Número de threads Inativos no Olá longa analisar o conjunto de threads.|
|LongParsingJobQueueLength|Threads: Análise longa comprimento da fila de tarefas|Contagem|Média|Número de tarefas numa fila de Olá de Olá longa analisar o conjunto de threads.|
|ProcessingPoolBusyIOJobThreads|Threads: Threads de trabalho de e/s ocupados do conjunto de processamento|Contagem|Média|Número de threads em execução tarefas de e/s no conjunto de threads de processamento de Olá.|
|ProcessingPoolBusyNonIOThreads|Threads: Threads de não-I/O ocupado do conjunto de processamento|Contagem|Média|Número de threads em execução de tarefas não-I/O no conjunto de threads de processamento de Olá.|
|ProcessingPoolIOJobQueueLength|Threads: Conjunto de comprimento de fila de trabalho de e/s de processamento|Contagem|Média|Número de tarefas de e/s na fila de Olá de Olá conjunto de threads de processamento.|
|ProcessingPoolIdleIOJobThreads|Threads: Conjunto Inativos threads de trabalho de e/s de processamento|Contagem|Média|Número de threads de inatividade para as tarefas de e/s no conjunto de threads de processamento de Olá.|
|ProcessingPoolIdleNonIOThreads|Threads: Threads de não-I/O inativo do conjunto de processamento|Contagem|Média|Número de threads Inativos no conjunto de threads de processamento de Olá dedicada tarefas toonon-I/O.|
|QueryPoolIdleThreads|Threads: Threads de inatividade do conjunto de consulta|Contagem|Média|Número de threads de inatividade para as tarefas de e/s no conjunto de threads de processamento de Olá.|
|QueryPoolJobQueueLength|Threads: Lengt de fila de tarefa de conjunto de consulta|Contagem|Média|Número de tarefas numa fila de Olá do conjunto de threads de consulta Olá.|
|ShortParsingBusyThreads|Threads: Curto período análise threads ocupados|Contagem|Média|Número de threads ocupados no Olá pequeno conjunto de threads de análise.|
|ShortParsingIdleThreads|Threads: Curto período análise threads Inativos|Contagem|Média|Número de threads Inativos no Olá pequeno conjunto de threads de análise.|
|ShortParsingJobQueueLength|Threads: Curto período comprimento de fila de tarefa de análise|Contagem|Média|Número de tarefas numa fila de Olá de Olá pequeno conjunto de threads de análise.|
|memory_thrashing_metric|Memória Thrashing|Percentagem|Média|Thrashing média da memória.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|TotalRequests|Gateway de total de pedidos|Contagem|Total|Número de pedidos de gateway|
|SuccessfulRequests|Pedidos de Gateway com êxito|Contagem|Total|Número de pedidos de gateway com êxito|
|UnauthorizedRequests|Pedidos de Gateway não autorizado|Contagem|Total|Número de pedidos de gateway não autorizado|
|FailedRequests|Pedidos de Gateway com falhas|Contagem|Total|Número de falhas nos pedidos de gateway|
|OtherRequests|Outros pedidos de Gateway|Contagem|Total|Número de outros pedidos de gateway|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|CoreCount|Contagem de núcleos dedicado|Contagem|Total|Número total de núcleos dedicados na conta do batch Olá|
|TotalNodeCount|Número de nós dedicado|Contagem|Total|Número total de nós dedicada na conta do batch Olá|
|LowPriorityCoreCount|Contagem de núcleos LowPriority|Contagem|Total|Número total de núcleos de prioridade baixa na conta do batch Olá|
|TotalLowPriorityNodeCount|Número de nós de baixa prioridade|Contagem|Total|Número total de nós de prioridade baixa na conta do batch Olá|
|CreatingNodeCount|Criar o número de nós|Contagem|Total|Número de nós ser criada|
|StartingNodeCount|Contagem inicial de nós|Contagem|Total|Número de nós partir de|
|WaitingForStartTaskNodeCount|A aguardar para contagem de nós de tarefa de início|Contagem|Total|Número de nós aguardar Olá iniciar tarefa toocomplete|
|StartTaskFailedNodeCount|Número de nós de falha de tarefa de início|Contagem|Total|Número de nós em que Olá iniciar tarefa falhou|
|IdleNodeCount|Contagem de nó inativo|Contagem|Total|Número de nós Inativos|
|OfflineNodeCount|Número de nós offline|Contagem|Total|Número de nós offline|
|RebootingNodeCount|Contagem de nós de reinício|Contagem|Total|Número de nós a ser reiniciado|
|ReimagingNodeCount|Número de nós de reprocessamento de imagem|Contagem|Total|Número de nós de reprocessamento de imagem|
|RunningNodeCount|Número de nós em execução|Contagem|Total|Número de nós a executar|
|LeavingPoolNodeCount|Abandonar o fileparser número de nós de conjunto|Contagem|Total|Número de nós Olá conjunto abandonar o fileparser.|
|UnusableNodeCount|Número de nós não utilizável|Contagem|Total|Número de nós não utilizáveis|
|PreemptedNodeCount|Número de nós antecipada|Contagem|Total|Número de nós antecipada|
|TaskStartEvent|Eventos de início da tarefa|Contagem|Total|Número total de tarefas que foram iniciadas|
|TaskCompleteEvent|Eventos de conclusão de tarefas|Contagem|Total|Número total de tarefas que foram concluídas|
|TaskFailEvent|Eventos de falha de tarefa|Contagem|Total|Número total de tarefas concluiu em estado de falha|
|PoolCreateEvent|Conjunto criar eventos|Contagem|Total|Número total de agrupamentos que foram criados|
|PoolResizeStartEvent|Eventos de início de redimensionamento de conjunto|Contagem|Total|Número total de redimensiona conjunto que foram iniciadas|
|PoolResizeCompleteEvent|Eventos de conclusão de redimensionamento do agrupamento|Contagem|Total|Número total de redimensiona conjunto que foram concluídas|
|PoolDeleteStartEvent|Eventos de início de eliminação do conjunto|Contagem|Total|Número total de eliminações de conjunto que foram iniciadas|
|PoolDeleteCompleteEvent|Conjunto eliminar eventos concluída|Contagem|Total|Número total de eliminações de conjunto que foram concluídas|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|connectedclients|Clientes ligados|Contagem|Máximo||
|totalcommandsprocessed|Operações totais|Contagem|Total||
|cachehits|Acertos na cache|Contagem|Total||
|cachemisses|Pedidos de sem êxito na cache|Contagem|Total||
|getcommands|Obtém|Contagem|Total||
|setcommands|Conjuntos de|Contagem|Total||
|evictedkeys|Expulsos as chaves|Contagem|Total||
|totalkeys|Chaves totais|Contagem|Máximo||
|expiredkeys|Chaves expiradas|Contagem|Total||
|usedmemory|Memória utilizada|Bytes|Máximo||
|usedmemoryRss|Memória utilizada RSS|Bytes|Máximo||
|serverLoad|Carga de servidor|Percentagem|Máximo||
|cacheWrite|Cache de escrita|BytesPerSecond|Máximo||
|cacheRead|Cache de leitura|BytesPerSecond|Máximo||
|percentProcessorTime|CPU|Percentagem|Máximo||
|connectedclients0|Clientes ligados (ID de partição horizontal 0)|Contagem|Máximo||
|totalcommandsprocessed0|Operações totais (ID de partição horizontal 0)|Contagem|Total||
|cachehits0|Acertos na cache (ID de partição horizontal 0)|Contagem|Total||
|cachemisses0|Pedidos sem êxito de cache (ID de partição horizontal 0)|Contagem|Total||
|getcommands0|Obtém (ID de partição horizontal 0)|Contagem|Total||
|setcommands0|Define (ID de partição horizontal 0)|Contagem|Total||
|evictedkeys0|Expulsos as chaves (ID de partição horizontal 0)|Contagem|Total||
|totalkeys0|Chaves totais (ID de partição horizontal 0)|Contagem|Máximo||
|expiredkeys0|Chaves expiradas (ID de partição horizontal 0)|Contagem|Total||
|usedmemory0|Memória utilizada (ID de partição horizontal 0)|Bytes|Máximo||
|usedmemoryRss0|Memória utilizada RSS (ID de partição horizontal 0)|Bytes|Máximo||
|serverLoad0|Carga de servidor (ID de partição horizontal 0)|Percentagem|Máximo||
|cacheWrite0|Cache de escrita (ID de partição horizontal 0)|BytesPerSecond|Máximo||
|cacheRead0|Cache de leitura (ID de partição horizontal 0)|BytesPerSecond|Máximo||
|percentProcessorTime0|CPU (ID de partição horizontal 0)|Percentagem|Máximo||
|connectedclients1|Clientes ligados (ID de partição horizontal 1)|Contagem|Máximo||
|totalcommandsprocessed1|Operações (ID de partição horizontal 1) do totais|Contagem|Total||
|cachehits1|Acertos na cache (ID de partição horizontal 1)|Contagem|Total||
|cachemisses1|Pedidos sem êxito de cache (ID de partição horizontal 1)|Contagem|Total||
|getcommands1|Obtém (ID de partição horizontal 1)|Contagem|Total||
|setcommands1|Define (ID de partição horizontal 1)|Contagem|Total||
|evictedkeys1|Expulsos as chaves (ID de partição horizontal 1)|Contagem|Total||
|totalkeys1|Chaves totais (ID de partição horizontal 1)|Contagem|Máximo||
|expiredkeys1|Chaves expiradas (ID de partição horizontal 1)|Contagem|Total||
|usedmemory1|Memória utilizada (ID de partição horizontal 1)|Bytes|Máximo||
|usedmemoryRss1|Memória utilizada RSS (ID de partição horizontal 1)|Bytes|Máximo||
|serverLoad1|Carga de servidor (ID de partição horizontal 1)|Percentagem|Máximo||
|cacheWrite1|Cache de escrita (ID de partição horizontal 1)|BytesPerSecond|Máximo||
|cacheRead1|Cache de leitura (ID de partição horizontal 1)|BytesPerSecond|Máximo||
|percentProcessorTime1|CPU (ID de partição horizontal 1)|Percentagem|Máximo||
|connectedclients2|Clientes ligados (ID de partição horizontal 2)|Contagem|Máximo||
|totalcommandsprocessed2|Operações (ID de partição horizontal 2) do totais|Contagem|Total||
|cachehits2|Acertos na cache (ID de partição horizontal 2)|Contagem|Total||
|cachemisses2|Pedidos sem êxito de cache (ID de partição horizontal 2)|Contagem|Total||
|getcommands2|Obtém (ID de partição horizontal 2)|Contagem|Total||
|setcommands2|Define (ID de partição horizontal 2)|Contagem|Total||
|evictedkeys2|Expulsos as chaves (ID de partição horizontal 2)|Contagem|Total||
|totalkeys2|Chaves totais (ID de partição horizontal 2)|Contagem|Máximo||
|expiredkeys2|Chaves expiradas (ID de partição horizontal 2)|Contagem|Total||
|usedmemory2|Memória utilizada (ID de partição horizontal 2)|Bytes|Máximo||
|usedmemoryRss2|Memória utilizada RSS (ID de partição horizontal 2)|Bytes|Máximo||
|serverLoad2|Carga de servidor (ID de partição horizontal 2)|Percentagem|Máximo||
|cacheWrite2|Cache de escrita (ID de partição horizontal 2)|BytesPerSecond|Máximo||
|cacheRead2|Cache de leitura (ID de partição horizontal 2)|BytesPerSecond|Máximo||
|percentProcessorTime2|CPU (ID de partição horizontal 2)|Percentagem|Máximo||
|connectedclients3|Clientes ligados (ID de partição horizontal 3)|Contagem|Máximo||
|totalcommandsprocessed3|Operações (ID de partição horizontal 3) do totais|Contagem|Total||
|cachehits3|Acertos na cache (ID de partição horizontal 3)|Contagem|Total||
|cachemisses3|Pedidos sem êxito de cache (ID de partição horizontal 3)|Contagem|Total||
|getcommands3|Obtém (ID de partição horizontal 3)|Contagem|Total||
|setcommands3|Define (ID de partição horizontal 3)|Contagem|Total||
|evictedkeys3|Expulsos as chaves (ID de partição horizontal 3)|Contagem|Total||
|totalkeys3|Chaves totais (ID de partição horizontal 3)|Contagem|Máximo||
|expiredkeys3|Chaves expiradas (ID de partição horizontal 3)|Contagem|Total||
|usedmemory3|Memória utilizada (ID de partição horizontal 3)|Bytes|Máximo||
|usedmemoryRss3|Memória utilizada RSS (ID de partição horizontal 3)|Bytes|Máximo||
|serverLoad3|Carga de servidor (ID de partição horizontal 3)|Percentagem|Máximo||
|cacheWrite3|Cache de escrita (ID de partição horizontal 3)|BytesPerSecond|Máximo||
|cacheRead3|Cache de leitura (ID de partição horizontal 3)|BytesPerSecond|Máximo||
|percentProcessorTime3|CPU (ID de partição horizontal 3)|Percentagem|Máximo||
|connectedclients4|Clientes ligados (ID de partição horizontal 4)|Contagem|Máximo||
|totalcommandsprocessed4|Operações totais (ID de partição horizontal 4)|Contagem|Total||
|cachehits4|Acertos na cache (ID de partição horizontal 4)|Contagem|Total||
|cachemisses4|Pedidos sem êxito de cache (ID de partição horizontal 4)|Contagem|Total||
|getcommands4|Obtém (ID de partição horizontal 4)|Contagem|Total||
|setcommands4|Define (ID de partição horizontal 4)|Contagem|Total||
|evictedkeys4|Expulsos as chaves (ID de partição horizontal 4)|Contagem|Total||
|totalkeys4|Chaves totais (ID de partição horizontal 4)|Contagem|Máximo||
|expiredkeys4|Chaves expiradas (ID de partição horizontal 4)|Contagem|Total||
|usedmemory4|Memória utilizada (ID de partição horizontal 4)|Bytes|Máximo||
|usedmemoryRss4|Memória utilizada RSS (ID de partição horizontal 4)|Bytes|Máximo||
|serverLoad4|Carga de servidor (ID de partição horizontal 4)|Percentagem|Máximo||
|cacheWrite4|Cache de escrita (ID de partição horizontal 4)|BytesPerSecond|Máximo||
|cacheRead4|Cache de leitura (ID de partição horizontal 4)|BytesPerSecond|Máximo||
|percentProcessorTime4|CPU (ID de partição horizontal 4)|Percentagem|Máximo||
|connectedclients5|Clientes ligados (ID de partição horizontal 5)|Contagem|Máximo||
|totalcommandsprocessed5|Operações totais (ID de partição horizontal 5)|Contagem|Total||
|cachehits5|Acertos na cache (ID de partição horizontal 5)|Contagem|Total||
|cachemisses5|Pedidos sem êxito de cache (ID de partição horizontal 5)|Contagem|Total||
|getcommands5|Obtém (ID de partição horizontal 5)|Contagem|Total||
|setcommands5|Define (ID de partição horizontal 5)|Contagem|Total||
|evictedkeys5|Expulsos as chaves (ID de partição horizontal 5)|Contagem|Total||
|totalkeys5|Chaves totais (ID de partição horizontal 5)|Contagem|Máximo||
|expiredkeys5|Chaves expiradas (ID de partição horizontal 5)|Contagem|Total||
|usedmemory5|Memória utilizada (ID de partição horizontal 5)|Bytes|Máximo||
|usedmemoryRss5|Memória utilizada RSS (ID de partição horizontal 5)|Bytes|Máximo||
|serverLoad5|Carga de servidor (ID de partição horizontal 5)|Percentagem|Máximo||
|cacheWrite5|Cache de escrita (ID de partição horizontal 5)|BytesPerSecond|Máximo||
|cacheRead5|Cache de leitura (ID de partição horizontal 5)|BytesPerSecond|Máximo||
|percentProcessorTime5|CPU (ID de partição horizontal 5)|Percentagem|Máximo||
|connectedclients6|Clientes ligados (ID de partição horizontal 6)|Contagem|Máximo||
|totalcommandsprocessed6|Operações totais (ID de partição horizontal 6)|Contagem|Total||
|cachehits6|Acertos na cache (ID de partição horizontal 6)|Contagem|Total||
|cachemisses6|Pedidos sem êxito de cache (ID de partição horizontal 6)|Contagem|Total||
|getcommands6|Obtém (ID de partição horizontal 6)|Contagem|Total||
|setcommands6|Define (ID de partição horizontal 6)|Contagem|Total||
|evictedkeys6|Expulsos as chaves (ID de partição horizontal 6)|Contagem|Total||
|totalkeys6|Chaves totais (ID de partição horizontal 6)|Contagem|Máximo||
|expiredkeys6|Chaves expiradas (ID de partição horizontal 6)|Contagem|Total||
|usedmemory6|Memória utilizada (ID de partição horizontal 6)|Bytes|Máximo||
|usedmemoryRss6|Memória utilizada RSS (ID de partição horizontal 6)|Bytes|Máximo||
|serverLoad6|Carga de servidor (ID de partição horizontal 6)|Percentagem|Máximo||
|cacheWrite6|Cache de escrita (ID de partição horizontal 6)|BytesPerSecond|Máximo||
|cacheRead6|Cache de leitura (ID de partição horizontal 6)|BytesPerSecond|Máximo||
|percentProcessorTime6|CPU (ID de partição horizontal 6)|Percentagem|Máximo||
|connectedclients7|Clientes ligados (ID de partição horizontal 7)|Contagem|Máximo||
|totalcommandsprocessed7|Operações totais (ID de partição horizontal 7)|Contagem|Total||
|cachehits7|Acertos na cache (ID de partição horizontal 7)|Contagem|Total||
|cachemisses7|Pedidos sem êxito de cache (ID de partição horizontal 7)|Contagem|Total||
|getcommands7|Obtém (ID de partição horizontal 7)|Contagem|Total||
|setcommands7|Define (ID de partição horizontal 7)|Contagem|Total||
|evictedkeys7|Expulsos as chaves (ID de partição horizontal 7)|Contagem|Total||
|totalkeys7|Chaves totais (ID de partição horizontal 7)|Contagem|Máximo||
|expiredkeys7|Chaves expiradas (ID de partição horizontal 7)|Contagem|Total||
|usedmemory7|Memória utilizada (ID de partição horizontal 7)|Bytes|Máximo||
|usedmemoryRss7|Memória utilizada RSS (ID de partição horizontal 7)|Bytes|Máximo||
|serverLoad7|Carga de servidor (ID de partição horizontal 7)|Percentagem|Máximo||
|cacheWrite7|Cache de escrita (ID de partição horizontal 7)|BytesPerSecond|Máximo||
|cacheRead7|Cache de leitura (ID de partição horizontal 7)|BytesPerSecond|Máximo||
|percentProcessorTime7|CPU (ID de partição horizontal 7)|Percentagem|Máximo||
|connectedclients8|Clientes ligados (ID de partição horizontal 8)|Contagem|Máximo||
|totalcommandsprocessed8|Operações totais (ID de partição horizontal 8)|Contagem|Total||
|cachehits8|Acertos na cache (ID de partição horizontal 8)|Contagem|Total||
|cachemisses8|Pedidos sem êxito de cache (ID de partição horizontal 8)|Contagem|Total||
|getcommands8|Obtém (ID de partição horizontal 8)|Contagem|Total||
|setcommands8|Define (ID de partição horizontal 8)|Contagem|Total||
|evictedkeys8|Expulsos as chaves (ID de partição horizontal 8)|Contagem|Total||
|totalkeys8|Chaves totais (ID de partição horizontal 8)|Contagem|Máximo||
|expiredkeys8|Chaves expiradas (ID de partição horizontal 8)|Contagem|Total||
|usedmemory8|Memória utilizada (ID de partição horizontal 8)|Bytes|Máximo||
|usedmemoryRss8|Memória utilizada RSS (ID de partição horizontal 8)|Bytes|Máximo||
|serverLoad8|Carga de servidor (ID de partição horizontal 8)|Percentagem|Máximo||
|cacheWrite8|Cache de escrita (ID de partição horizontal 8)|BytesPerSecond|Máximo||
|cacheRead8|Cache de leitura (ID de partição horizontal 8)|BytesPerSecond|Máximo||
|percentProcessorTime8|CPU (ID de partição horizontal 8)|Percentagem|Máximo||
|connectedclients9|Clientes ligados (ID de partição horizontal 9)|Contagem|Máximo||
|totalcommandsprocessed9|Operações totais (ID de partição horizontal 9)|Contagem|Total||
|cachehits9|Acertos na cache (ID de partição horizontal 9)|Contagem|Total||
|cachemisses9|Pedidos sem êxito de cache (ID de partição horizontal 9)|Contagem|Total||
|getcommands9|Obtém (ID de partição horizontal 9)|Contagem|Total||
|setcommands9|Define (ID de partição horizontal 9)|Contagem|Total||
|evictedkeys9|Expulsos as chaves (ID de partição horizontal 9)|Contagem|Total||
|totalkeys9|Chaves totais (ID de partição horizontal 9)|Contagem|Máximo||
|expiredkeys9|Chaves expiradas (ID de partição horizontal 9)|Contagem|Total||
|usedmemory9|Memória utilizada (ID de partição horizontal 9)|Bytes|Máximo||
|usedmemoryRss9|Memória utilizada RSS (ID de partição horizontal 9)|Bytes|Máximo||
|serverLoad9|Carga de servidor (ID de partição horizontal 9)|Percentagem|Máximo||
|cacheWrite9|Cache de escrita (ID de partição horizontal 9)|BytesPerSecond|Máximo||
|cacheRead9|Cache de leitura (ID de partição horizontal 9)|BytesPerSecond|Máximo||
|percentProcessorTime9|CPU (ID de partição horizontal 9)|Percentagem|Máximo||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|TotalCalls|Totais de chamadas|Contagem|Total|Número total de chamadas.|
|SuccessfulCalls|Chamadas com êxito|Contagem|Total|Número de chamadas com êxito.|
|TotalErrors|Total de erros|Contagem|Total|Número total de chamadas com a resposta de erro (4xx de código de resposta HTTP ou 5xx).|
|BlockedCalls|Chamadas bloqueadas|Contagem|Total|Número de chamadas que taxa excedida ou o limite de quota.|
|ServerErrors|Erros de servidor|Contagem|Total|Número de chamadas com o erro interno do serviço (código de resposta HTTP 5xx).|
|ClientErrors|Erros de cliente|Contagem|Total|Número de chamadas com o erro do lado do cliente (4xx de código de resposta HTTP).|
|DataIn|Dados em|Bytes|Total|Tamanho dos dados de entrada em bytes.|
|DataOut|Dados de saída|Bytes|Total|Tamanho dos dados de saída em bytes.|
|Latência|Latência|Milissegundos|Média|Latência em milissegundos.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|Percentagem de CPU|Percentagem de CPU|Percentagem|Média|percentagem de Olá de unidades de computação alocados que estão atualmente em utilização por Olá ais|
|Rede no|Rede no|Bytes|Total|Olá número de bytes recebidos em todas as interfaces de rede pelo Olá ais (tráfego de entrada)|
|Limite de rede|Limite de rede|Bytes|Total|Olá número de bytes terminar em todas as interfaces de rede por Olá ais (tráfego de saída)|
|Bytes de leitura do disco|Bytes de leitura do disco|Bytes|Total|Total de bytes lidos do disco durante o período de monitorização|
|Bytes de escrita do disco|Bytes de escrita do disco|Bytes|Total|Total de bytes escritos toodisk durante o período de monitorização|
|Disco lidos/seg de operações|Disco lidos/seg de operações|CountPerSecond|Média|Leitura de disco IOPS|
|Operações de escrita de disco/seg|Operações de escrita de disco/seg|CountPerSecond|Média|Escrita de disco IOPS|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|Percentagem de CPU|Percentagem de CPU|Percentagem|Média|percentagem de Olá de unidades de computação alocados que estão atualmente em utilização por Olá ais|
|Rede no|Rede no|Bytes|Total|Olá número de bytes recebidos em todas as interfaces de rede pelo Olá ais (tráfego de entrada)|
|Limite de rede|Limite de rede|Bytes|Total|Olá número de bytes terminar em todas as interfaces de rede por Olá ais (tráfego de saída)|
|Bytes de leitura do disco|Bytes de leitura do disco|Bytes|Total|Total de bytes lidos do disco durante o período de monitorização|
|Bytes de escrita do disco|Bytes de escrita do disco|Bytes|Total|Total de bytes escritos toodisk durante o período de monitorização|
|Disco lidos/seg de operações|Disco lidos/seg de operações|CountPerSecond|Média|Leitura de disco IOPS|
|Operações de escrita de disco/seg|Operações de escrita de disco/seg|CountPerSecond|Média|Escrita de disco IOPS|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|Percentagem de CPU|Percentagem de CPU|Percentagem|Média|percentagem de Olá de unidades de computação alocados que estão atualmente em utilização por Olá ais|
|Rede no|Rede no|Bytes|Total|Olá número de bytes recebidos em todas as interfaces de rede pelo Olá ais (tráfego de entrada)|
|Limite de rede|Limite de rede|Bytes|Total|Olá número de bytes terminar em todas as interfaces de rede por Olá ais (tráfego de saída)|
|Bytes de leitura do disco|Bytes de leitura do disco|Bytes|Total|Total de bytes lidos do disco durante o período de monitorização|
|Bytes de escrita do disco|Bytes de escrita do disco|Bytes|Total|Total de bytes escritos toodisk durante o período de monitorização|
|Disco lidos/seg de operações|Disco lidos/seg de operações|CountPerSecond|Média|Leitura de disco IOPS|
|Operações de escrita de disco/seg|Operações de escrita de disco/seg|CountPerSecond|Média|Escrita de disco IOPS|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|DCIApiCalls|Chamadas de API de informações de cliente|Contagem|Total||
|DCIMappingImportOperationSuccessfulLines|Mapeamento de operação de importação linhas com êxito|Contagem|Total||
|DCIMappingImportOperationFailedLines|Mapeamento de operação de importação falha linhas|Contagem|Total||
|DCIMappingImportOperationTotalLines|Mapeamento de operação de importação linhas Total|Contagem|Total||
|DCIMappingImportOperationRuntimeInSeconds|Runtime de operação de importação de mapeamento em segundos|Segundos|Total||
|DCIOutboundProfileExportSucceeded|Exportação de perfil de saída foi concluída com êxito|Contagem|Total||
|DCIOutboundProfileExportFailed|Falhada de exportação de perfil de saída|Contagem|Total||
|DCIOutboundProfileExportDuration|Duração de exportação de perfil de saída|Segundos|Total||
|DCIOutboundKpiExportSucceeded|Saída de Kpi de exportação com êxito|Contagem|Total||
|DCIOutboundKpiExportFailed|Falha de saída de Kpi de exportação|Contagem|Total||
|DCIOutboundKpiExportDuration|Duração de saída de Kpi de exportação|Segundos|Total||
|DCIOutboundKpiExportStarted|Exportação de Kpi de saída foi iniciada|Segundos|Total||
|DCIOutboundKpiRecordCount|Contagem de registo de Kpi de saída|Segundos|Total||
|DCIOutboundProfileExportCount|Contagem de exportação de perfil de saída|Segundos|Total||
|DCIOutboundInitialProfileExportFailed|Falhada de exportação de saída perfil inicial|Segundos|Total||
|DCIOutboundInitialProfileExportSucceeded|Exportação de saída perfil inicial foi concluída com êxito|Segundos|Total||
|DCIOutboundInitialKpiExportFailed|Exportação de Kpi inicial saída falhou|Segundos|Total||
|DCIOutboundInitialKpiExportSucceeded|Exportação de Kpi inicial saída com êxito|Segundos|Total||
|DCIOutboundInitialProfileExportDurationInSeconds|Duração de exportação de saída perfil inicial em segundos|Segundos|Total||
|AdlaJobForStandardKpiFailed|Tarefa de Adla para Standard Kpi falhada em segundos|Segundos|Total||
|AdlaJobForStandardKpiTimeOut|Tarefa de Adla para padrão de Kpi de tempo limite em segundos|Segundos|Total||
|AdlaJobForStandardKpiCompleted|Tarefa de Adla para Standard Kpi foi concluída em segundos|Segundos|Total||
|ImportASAValuesFailed|Contagem de falha na importação ASA valores|Contagem|Total||
|ImportASAValuesSucceeded|Importar ASA valores êxito contagem|Contagem|Total||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|JobEndedSuccess|Tarefas com êxito|Contagem|Total|Contagem de tarefas com êxito.|
|JobEndedFailure|Tarefas falhadas|Contagem|Total|Contagem de tarefas com falha.|
|JobEndedCancelled|Tarefas canceladas|Contagem|Total|Contagem de tarefas canceladas.|
|JobAUEndedSuccess|Tempo de AU com êxito|Segundos|Total|Tempo de AU total para as tarefas com êxito.|
|JobAUEndedFailure|Falha de AU de tempo|Segundos|Total|Tempo de AU total para as tarefas falhadas.|
|JobAUEndedCancelled|Tempo de AU cancelada|Segundos|Total|Tempo total de AU para tarefas canceladas.|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|cpu_percent|Percentagem de CPU|Percentagem|Média|Percentagem de CPU|
|compute_limit|Limite de unidade de computação|Contagem|Média|Limite de unidade de computação|
|compute_consumption_percent|Percentagem de unidade de computação|Percentagem|Média|Percentagem de unidade de computação|
|memory_percent|Percentagem de memória|Percentagem|Média|Percentagem de memória|
|io_consumption_percent|Percentagem de e/s|Percentagem|Média|Percentagem de e/s|
|storage_percent|Percentagem de armazenamento|Percentagem|Média|Percentagem de armazenamento|
|storage_used|Armazenamento utilizado|Bytes|Média|Armazenamento utilizado|
|storage_limit|Limite de armazenamento|Bytes|Média|Limite de armazenamento|
|active_connections|Totais ligações ativas|Contagem|Média|Totais ligações ativas|
|connections_failed|Totais de ligações com falhas|Contagem|Média|Totais de ligações com falhas|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|cpu_percent|Percentagem de CPU|Percentagem|Média|Percentagem de CPU|
|compute_limit|Limite de unidade de computação|Contagem|Média|Limite de unidade de computação|
|compute_consumption_percent|Percentagem de unidade de computação|Percentagem|Média|Percentagem de unidade de computação|
|memory_percent|Percentagem de memória|Percentagem|Média|Percentagem de memória|
|io_consumption_percent|Percentagem de e/s|Percentagem|Média|Percentagem de e/s|
|storage_percent|Percentagem de armazenamento|Percentagem|Média|Percentagem de armazenamento|
|storage_used|Armazenamento utilizado|Bytes|Média|Armazenamento utilizado|
|storage_limit|Limite de armazenamento|Bytes|Média|Limite de armazenamento|
|active_connections|Totais ligações ativas|Contagem|Média|Totais ligações ativas|
|connections_failed|Totais de ligações com falhas|Contagem|Média|Totais de ligações com falhas|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|d2c.telemetry.Ingress.allProtocol|Tentativas de envio de mensagem de telemetria|Contagem|Total|Número de toobe de tentativa de mensagens de telemetria do dispositivo para nuvem enviados tooyour IoT hub|
|d2c.telemetry.Ingress.Success|Mensagens de telemetria enviadas|Contagem|Total|Número de mensagens de telemetria do dispositivo para nuvem enviados com êxito tooyour IoT hub|
|c2d.Commands.egress.Complete.Success|Comandos concluídos|Contagem|Total|Número de comandos da nuvem para o dispositivo foi concluída com êxito pelo dispositivo Olá|
|c2d.Commands.egress.Abandon.Success|Comandos abandonados|Contagem|Total|Número de comandos da nuvem para o dispositivo abandonadas pelo dispositivo Olá|
|c2d.Commands.egress.Reject.Success|Comandos rejeitados|Contagem|Total|Número de comandos da nuvem para dispositivo rejeitados pelo dispositivo Olá|
|devices.totalDevices|Total de dispositivos|Contagem|Total|Número de dispositivos registados tooyour IoT hub|
|devices.connectedDevices.allProtocol|Dispositivos ligados|Contagem|Total|Número de dispositivos ligados tooyour IoT hub|
|d2c.telemetry.egress.Success|Mensagens de telemetria entregues|Contagem|Total|Número de vezes que as mensagens com êxito foram escritas tooendpoints (total)|
|d2c.telemetry.egress.dropped|Mensagens de ignorados|Contagem|Total|Número de mensagens removida porque o ponto final de entrega de Olá foi Inativos|
|d2c.telemetry.egress.orphaned|Mensagens órfãos|Contagem|Total|Contagem de Olá de mensagens em fila não corresponde a qualquer rotas incluindo rota Olá de contingência|
|d2c.telemetry.egress.Invalid|Mensagens inválidas|Contagem|Total|Olá contagem de mensagens não entregues devido tooincompatibility com o ponto final de Olá|
|d2c.telemetry.egress.fallback|Mensagens de correspondência de condição de contingência|Contagem|Total|Número de mensagens escritas toohello endpoint de contingência|
|d2c.Endpoints.egress.eventHubs|Mensagens entregues tooEvent pontos finais de Hub|Contagem|Total|Número de vezes que as mensagens foram pontos finais de Hub tooEvent escrito com êxito|
|d2c.Endpoints.latency.eventHubs|Latência de mensagem para pontos finais de Hub de eventos|milissegundos|Média|latência média Olá entre mensagem entrada toohello IoT hub e a entrada de mensagem para um ponto final de Hub de eventos, em milissegundos|
|d2c.Endpoints.egress.serviceBusQueues|Mensagens entregues tooService pontos finais de fila de barramento|Contagem|Total|Número de vezes que as mensagens foram pontos finais de fila de barramento tooService escrito com êxito|
|d2c.Endpoints.latency.serviceBusQueues|Latência de mensagem para pontos finais de fila do Service Bus|milissegundos|Média|latência média Olá entre mensagem entrada toohello IoT hub e a entrada de mensagem para um ponto final de fila do Service Bus, em milissegundos|
|d2c.Endpoints.egress.serviceBusTopics|Mensagens entregues tooService pontos finais de tópico de barramento|Contagem|Total|Número de vezes que as mensagens foram pontos finais de tópico de barramento tooService escrito com êxito|
|d2c.Endpoints.latency.serviceBusTopics|Latência de mensagem para pontos finais de tópico de barramento de serviço|milissegundos|Média|latência média Olá entre mensagem entrada toohello IoT hub e a entrada de mensagem para um ponto final de tópico de barramento de serviço, em milissegundos|
|d2c.Endpoints.egress.builtIn.Events|Mensagens entregues ponto final incorporado toohello (mensagens/eventos)|Contagem|Total|Número de vezes que as mensagens foram ponto final incorporado toohello escrito com êxito (mensagens/eventos)|
|d2c.Endpoints.latency.builtIn.Events|Latência de mensagem para o ponto final incorporado de Olá (mensagens/eventos)|milissegundos|Média|latência média Olá entre mensagem entrada toohello IoT hub e a entrada de mensagem em Olá ponto final incorporado (mensagens/eventos), em milissegundos |
|d2c.Twin.Read.Success|Leituras de duplo bem-sucedida dos dispositivos|Contagem|Total|Contagem de Olá de leituras de iniciadas por dispositivo duplo todos os com êxito.|
|d2c.Twin.Read.Failure|Não foi possível duplo leituras dos dispositivos|Contagem|Total|Contagem de Olá de todos os falha leituras iniciadas por dispositivo duplo.|
|d2c.Twin.Read.size|Tamanho da resposta de duplo lê a partir de dispositivos|Bytes|Média|média de Olá, mínimo e máximo de todos os com êxito iniciadas por dispositivo duplo leituras.|
|d2c.Twin.Update.Success|Atualizações de duplo com êxito a partir de dispositivos|Contagem|Total|Contagem de Olá de todos os com êxito atualizações de iniciadas por dispositivo duplo.|
|d2c.Twin.Update.Failure|Falha de atualizações de duplo a partir de dispositivos|Contagem|Total|Contagem de Olá de todos os falha atualizações iniciadas por dispositivo duplo.|
|d2c.Twin.Update.size|Tamanho das atualizações de duplo a partir de dispositivos|Bytes|Média|média de Olá, min e o tamanho máximo de todos os com êxito iniciadas por dispositivo duplo atualizações.|
|c2d.methods.Success|Invocações de método direto com êxito|Contagem|Total|Contagem de Olá de chamadas de método direto todos os com êxito.|
|c2d.methods.Failure|Não foi possível invocações de método direto|Contagem|Total|Contagem de Olá de todos os falha chamadas de método direto.|
|c2d.methods.requestSize|Tamanho do pedido de invocações de método direto|Bytes|Média|média de Olá, min e max de todos os com êxito direcionam os pedidos de método.|
|c2d.methods.responseSize|Tamanho da resposta de invocações de método direto|Bytes|Média|média de Olá, min e max de todas as respostas de método direto com êxito.|
|c2d.Twin.Read.Success|Leituras de duplo com êxito de back-end|Contagem|Total|Contagem de Olá de leituras de back-end-iniciada duplo todos os com êxito.|
|c2d.Twin.Read.Failure|Leituras de duplo falhada de back-end|Contagem|Total|Contagem de Olá de todos os falha leituras duplo iniciada em back-end.|
|c2d.Twin.Read.size|Tamanho da resposta de duplo lê a partir do back-end|Bytes|Média|média de Olá, mínimo e máximo de todos os com êxito iniciada em back-end duplo leituras.|
|c2d.Twin.Update.Success|Atualizações de duplo com êxito a partir de back-end|Contagem|Total|Contagem de Olá de todos os com êxito atualizações de duplo iniciada em back-end.|
|c2d.Twin.Update.Failure|Atualizações de duplo falhada a partir de back-end|Contagem|Total|Contagem de Olá de todos os falha atualizações duplo iniciada em back-end.|
|c2d.Twin.Update.size|Tamanho de atualizações de duplo do back-end|Bytes|Média|média de Olá, min e o tamanho máximo de todos os com êxito iniciada em back-end duplo atualizações.|
|twinQueries.success|Consultas de duplo com êxito|Contagem|Total|Contagem de Olá de todas as consultas de duplo com êxito.|
|twinQueries.failure|Consultas de duplo falhada|Contagem|Total|Contagem de Olá de todas as consultas de duplo falhada.|
|twinQueries.resultSize|Tamanho dos resultados consultas duplo|Bytes|Média|média de Olá, min e max do tamanho dos resultados Olá de todas as consultas de duplo com êxito.|
|jobs.createTwinUpdateJob.success|Criações com êxito das tarefas de atualização de duplo|Contagem|Total|Contagem de Olá de todos os criação com êxito das tarefas de atualização de duplo.|
|jobs.createTwinUpdateJob.failure|Falha de criações de tarefas de atualização de duplo|Contagem|Total|Contagem de Olá de todos os falha na criação de tarefas de atualização de duplo.|
|jobs.createDirectMethodJob.success|Criações com êxito das tarefas de invocação do método|Contagem|Total|Contagem de Olá de todos os criação com êxito das tarefas de invocação do método direto.|
|jobs.createDirectMethodJob.failure|Falha de criações de tarefas de invocação do método|Contagem|Total|Contagem de Olá de todos os falha na criação de tarefas de invocação do método direto.|
|jobs.listJobs.success|Tarefas de toolist de chamadas com êxito|Contagem|Total|Contagem de Olá de todas as tarefas de toolist chamadas bem-sucedidas.|
|jobs.listJobs.failure|Chamadas falhadas toolist tarefas|Contagem|Total|Contagem de Olá de todas as tarefas de toolist chamadas falhadas.|
|jobs.cancelJob.success|Cancelamentos de tarefas com êxito|Contagem|Total|Contagem de Olá de êxito todas as chamadas toocancel uma tarefa.|
|jobs.cancelJob.failure|Cancelamentos de tarefas com falhas|Contagem|Total|Contagem de Olá de todas as chamadas falhadas toocancel uma tarefa.|
|jobs.queryJobs.success|Consultas de tarefa com êxito|Contagem|Total|Contagem de Olá de todas as tarefas de tooquery chamadas bem-sucedidas.|
|jobs.queryJobs.failure|Falha na tarefa consulta|Contagem|Total|Contagem de Olá de todas as tarefas de tooquery chamadas falhadas.|
|Jobs.completed|Tarefas concluídas|Contagem|Total|Contagem de Olá de todas as tarefas de conclusão.|
|Jobs.Failed|Tarefas falhadas|Contagem|Total|Contagem de Olá de todas as tarefas falhadas.|
|d2c.telemetry.Ingress.sendThrottle|Número de erros de limitação|Contagem|Total|Número de erros de limitação devido a limitações de débito toodevice|
|dailyMessageQuotaUsed|Número total de mensagens utilizado|Contagem|Média|Número total de mensagens utilizada hoje em dia|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|INREQS|Receber pedidos de envio|Contagem|Total|Entrada total enviar pedidos para um hub de notificação|
|SUCCREQ|Pedidos com êxito|Contagem|Total|Total de pedidos com êxito para um espaço de nomes|
|FAILREQ|Pedidos falhados|Contagem|Total|Totais de pedidos falhados para um espaço de nomes|
|SVRBSY|Servidor ocupado erros|Contagem|Total|Erros de ocupado total do servidor para um espaço de nomes|
|INTERR|Erros de servidor interno|Contagem|Total|Erros de total de servidor interno para um espaço de nomes|
|MISCERR|Outros erros|Contagem|Total|Totais de pedidos falhados para um espaço de nomes|
|INMSGS|Mensagens a receber|Contagem|Total|Total de mensagens de entrada para um espaço de nomes|
|OUTMSGS|Mensagens de saída|Contagem|Total|Total de envio de mensagens para um espaço de nomes|
|EHINMBS|Bytes recebidos|Bytes|Total|Débito de mensagem de entrada de Hub do evento para um espaço de nomes|
|EHOUTMBS|Bytes enviados|Bytes|Total|Total de envio de mensagens para um espaço de nomes|
|EHABL|Mensagens de registo de segurança de arquivo|Contagem|Total|Mensagens de arquivo de Hub de eventos no registo de segurança para um espaço de nomes|
|EHAMSGS|Arquivar mensagens|Contagem|Total|Hub de eventos arquivados mensagens num espaço de nomes|
|EHAMBS|Débito de mensagem de arquivo|Bytes|Total|Débito de mensagem num espaço de nomes de arquivada de Hub de eventos|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|RunsStarted|Executa iniciada|Contagem|Total|Número de fluxo de trabalho é executado foi iniciado.|
|RunsCompleted|Executa concluída|Contagem|Total|Número de fluxo de trabalho é executado concluído.|
|RunsSucceeded|É executado com êxito|Contagem|Total|Número de fluxo de trabalho é executado com êxito.|
|RunsFailed|Falhada de execução|Contagem|Total|Número de fluxo de trabalho é executado com falhas.|
|RunsCancelled|Execução cancelada|Contagem|Total|Número de fluxo de trabalho é executado cancelado.|
|RunLatency|Executar latência|Segundos|Média|Executa a latência de fluxo de trabalho foi concluída.|
|RunSuccessLatency|Execute a latência de êxito|Segundos|Média|Executa a latência de fluxo de trabalho foi efetuada com êxito.|
|RunThrottledEvents|Executar otimizados de eventos|Contagem|Total|Número de ação de fluxo de trabalho ou acionador limitado eventos.|
|RunFailurePercentage|Percentagem de falha de execução|Percentagem|Total|Percentagem de fluxo de trabalho é executado com falhas.|
|ActionsStarted|Ações iniciadas |Contagem|Total|Número de ações de fluxo de trabalho foi iniciado.|
|ActionsCompleted|Ações concluídas |Contagem|Total|Número de ações de fluxo de trabalho foi concluída.|
|ActionsSucceeded|Ações foi concluída com êxito |Contagem|Total|Número de ações de fluxo de trabalho foi efetuado com êxito.|
|ActionsFailed|Falhada de ações|Contagem|Total|Número de ações de fluxo de trabalho falharam.|
|ActionsSkipped|Ações ignoradas |Contagem|Total|Número de ações de fluxo de trabalho foi ignorada.|
|ActionLatency|Latência de ação |Segundos|Média|Latência das ações de fluxo de trabalho foi concluída.|
|ActionSuccessLatency|Latência de êxito de ação |Segundos|Média|Latência das ações de fluxo de trabalho foi efetuada com êxito.|
|ActionThrottledEvents|Ação limitadas eventos|Contagem|Total|Número de ação de fluxo de trabalho limitadas eventos...|
|TriggersStarted|Acionadores iniciados |Contagem|Total|Número de acionadores de fluxo de trabalho foi iniciado.|
|TriggersCompleted|Acionadores concluídas |Contagem|Total|Número de acionadores de fluxo de trabalho foi concluída.|
|TriggersSucceeded|Acionadores foi concluída com êxito |Contagem|Total|Número de acionadores de fluxo de trabalho foi efetuado com êxito.|
|TriggersFailed|Acionadores falhou |Contagem|Total|Número de acionadores de fluxo de trabalho falharam.|
|TriggersSkipped|Acionadores ignoradas|Contagem|Total|Número de acionadores de fluxo de trabalho foi ignorada.|
|TriggersFired|Acionadores desencadeados |Contagem|Total|É desencadeado o número de acionadores de fluxo de trabalho.|
|TriggerLatency|Latência de Acionador |Segundos|Média|Latência de acionadores de fluxo de trabalho foi concluída.|
|TriggerFireLatency|Latência de Fire do acionador |Segundos|Média|Latência de acionadores de desencadeou o fluxo de trabalho.|
|TriggerSuccessLatency|Latência de êxito de Acionador |Segundos|Média|Latência de acionadores de fluxo de trabalho foi efetuada com êxito.|
|TriggerThrottledEvents|Acionar eventos otimizados|Contagem|Total|Número de Acionador de fluxo de trabalho limitado eventos.|
|BillableActionExecutions|Execuções de ação facturável|Contagem|Total|Número de execuções de ação de fluxo de trabalho obter cobrados.|
|BillableTriggerExecutions|Execuções de Acionador facturável|Contagem|Total|Número de execuções de Acionador de fluxo de trabalho obter cobrados.|
|TotalBillableExecutions|Execuções Faturáveis totais|Contagem|Total|Número de execuções de fluxo de trabalho obter cobrados.|

## <a name="microsoftnetworkapplicationgateways"></a>Network/applicationgateways

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|Débito|Débito|BytesPerSecond|Média||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|BytesIn|BytesIn|Contagem|Total||
|BytesOut|BytesOut|Contagem|Total||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|Registration.all|Operação de registo|Contagem|Total|Contagem de Olá de todas as operações de registo com êxito (consultas do criações atualizações e eliminações). |
|Registration.Create|Registo criar operações|Contagem|Total|Contagem de Olá de todas as criações de registo com êxito.|
|Registration.Update|Operações de atualização de registo|Contagem|Total|Contagem de Olá de todas as atualizações do registo com êxito.|
|Registration.Get|Operações de leitura do registo|Contagem|Total|Contagem de Olá de todas as consultas de registo com êxito.|
|Registration.delete|Operações de eliminação do registo|Contagem|Total|Contagem de Olá de todas as eliminações de registo com êxito.|
|entrada|Mensagens a receber|Contagem|Total|Contagem de Olá de todos os com êxito enviar chamadas da API. |
|incoming.Scheduled|Notificações Push agendada enviadas|Contagem|Total|Notificações de Push agendada canceladas|
|incoming.Scheduled.Cancel|Notificações de Push agendada canceladas|Contagem|Total|Notificações de Push agendada canceladas|
|Scheduled.Pending|Notificações agendadas pendentes|Contagem|Total|Notificações agendadas pendentes|
|Installation.all|Operações de gestão de instalação|Contagem|Total|Operações de gestão de instalação|
|Installation.Get|Obter operações de instalação|Contagem|Total|Obter operações de instalação|
|Installation.upsert|Criar ou atualizar operações de instalação|Contagem|Total|Criar ou atualizar operações de instalação|
|Installation.patch|Operações de instalação de patches|Contagem|Total|Operações de instalação de patches|
|Installation.delete|Eliminar operações de instalação|Contagem|Total|Eliminar operações de instalação|
|Outgoing.allpns.Success|Notificações com êxito|Contagem|Total|Contagem de Olá de todas as notificações com êxito.|
|Outgoing.allpns.invalidpayload|Erros de payload|Contagem|Total|Contagem de Olá de pushes falhou porque hello PNS devolveu um erro de payload incorreto.|
|Outgoing.allpns.pnserror|Erros de sistema externo de notificação|Contagem|Total|Contagem de Olá de pushes falhou porque ocorreu um problema ao comunicar com Olá PNS (exclui a problemas de autenticação).|
|Outgoing.allpns.channelerror|Erros de canal|Contagem|Total|Contagem de Olá de pushes que falhou porque o canal de Olá era inválido não associados a Olá correto aplicação limitadas ou expirou.|
|Outgoing.allpns.badorexpiredchannel|Erros de canal incorretos ou expirados|Contagem|Total|Contagem de Olá de pushes que falhou porque Olá canal/token/registrationId no registo de Olá era inválida ou expirada.|
|Outgoing.WNS.Success|Notificações com êxito do WNS|Contagem|Total|Contagem de Olá de todas as notificações com êxito.|
|Outgoing.WNS.invalidcredentials|Erros de autorização do WNS (credenciais inválidas)|Contagem|Total|Contagem de Olá de pushes que falhou porque Olá PNS não aceitou Olá fornecidas credenciais ou credenciais Olá estão bloqueadas. (Windows Live não reconhece credenciais Olá).|
|Outgoing.WNS.badchannel|Erro de canal de incorretos do WNS|Contagem|Total|Olá, contagem de pushes falhou porque não foi reconhecido Olá ChannelURI no registo de Olá (estado WNS: 404 não encontrado).|
|Outgoing.WNS.expiredchannel|Erro de canal de expirado WNS|Contagem|Total|Olá, contagem de pushes falhou porque hello ChannelURI expirou (estado WNS: 410 Gone).|
|Outgoing.WNS.throttled|WNS limitadas notificações|Contagem|Total|Olá, contagem de pushes falhou porque o WNS é a limitação esta aplicação (estado WNS: 406 Não aceitável).|
|Outgoing.WNS.tokenproviderunreachable|Erros de autorização do WNS (inacessíveis)|Contagem|Total|Windows Live não está acessível.|
|Outgoing.WNS.invalidtoken|Erros de autorização do WNS (Token inválido)|Contagem|Total|Olá token fornecido tooWNS não é válido (estado WNS: não autorizado 401).|
|Outgoing.WNS.wrongtoken|Erros de autorização do WNS (Token incorreto)|Contagem|Total|Olá token fornecido tooWNS é válido, mas para outra aplicação (estado WNS: 403 Proibido). Isto pode acontecer se Olá ChannelURI no registo de Olá estiver associada a outra aplicação. Verifique que as aplicações cliente Olá estão associada a Olá mesma aplicação cujas credenciais são no hub de notificação de Olá.|
|Outgoing.WNS.invalidnotificationformat|Formato de notificação inválido do WNS|Contagem|Total|o formato de notificação de Olá Olá é inválido (estado WNS: 400). Tenha em atenção que o WNS não rejeitar todos os payloads inválidos.|
|Outgoing.WNS.invalidnotificationsize|Erro de tamanho de notificação inválido do WNS|Contagem|Total|payload de notificação de Olá é demasiado grande (estado WNS: 413).|
|Outgoing.WNS.channelthrottled|Canal de WNS limitadas|Contagem|Total|a notificação de Olá foi removida porque está limitada Olá ChannelURI no registo de Olá (cabeçalho de resposta do WNS: X-WNS-NotificationStatus:channelThrottled).|
|Outgoing.WNS.channeldisconnected|Canal de WNS desligado|Contagem|Total|a notificação de Olá foi removida porque está limitada Olá ChannelURI no registo de Olá (cabeçalho de resposta do WNS: X-WNS-DeviceConnectionStatus: desligado).|
|Outgoing.WNS.dropped|Notificações de ignorados do WNS|Contagem|Total|a notificação de Olá foi removida porque está limitada Olá ChannelURI no registo de Olá (X-WNS-NotificationStatus: ignorados, mas não X-WNS-DeviceConnectionStatus: desligado).|
|Outgoing.WNS.pnserror|Erros do WNS|Contagem|Total|Notificação não entregar devido a erros de comunicação ao WNS.|
|Outgoing.WNS.authenticationerror|Erros de autenticação do WNS|Contagem|Total|Notificação não entregar devido a erros de comunicação com o Windows Live credenciais inválidas ou token incorreto.|
|Outgoing.APNs.Success|Notificações com êxito do APNS|Contagem|Total|Contagem de Olá de todas as notificações com êxito.|
|Outgoing.APNs.invalidcredentials|Erros de autorização do APNS|Contagem|Total|Contagem de Olá de pushes que falhou porque Olá PNS não aceitou Olá fornecidas credenciais ou credenciais Olá estão bloqueadas.|
|Outgoing.APNs.badchannel|Erro de canal de incorretos do APNS|Contagem|Total|Olá, contagem de pushes falhou porque o token de Olá é inválido (código de estado do APNS: 8).|
|Outgoing.APNs.expiredchannel|Erro de canal de expirado do APNS|Contagem|Total|Contagem de Olá de token que foram invalidados por canal de comentários do Olá do APNS.|
|Outgoing.APNs.invalidnotificationsize|Erro de tamanho de notificação inválido do APNS|Contagem|Total|Olá, contagem de pushes falhou porque o payload de Olá era demasiado grande (código de estado do APNS: 7).|
|Outgoing.APNs.pnserror|Erros do APNS|Contagem|Total|Contagem de Olá de pushes que falharam devido a erros de comunicação com o APNS.|
|Outgoing.GCM.Success|Notificações com êxito do GCM|Contagem|Total|Contagem de Olá de todas as notificações com êxito.|
|Outgoing.GCM.invalidcredentials|Erros de autorização do GCM (credenciais inválidas)|Contagem|Total|Contagem de Olá de pushes que falhou porque Olá PNS não aceitou Olá fornecidas credenciais ou credenciais Olá estão bloqueadas.|
|Outgoing.GCM.badchannel|Erro de canal de incorretos do GCM|Contagem|Total|Olá, contagem de pushes falhou porque não foi reconhecido Olá registrationId no registo de Olá (resultado do GCM: registo inválido).|
|Outgoing.GCM.expiredchannel|Erro de canal de expirado do GCM|Contagem|Total|Olá, contagem de pushes falhou porque Olá registrationId no registo de Olá expirou (resultado do GCM: NotRegistered).|
|Outgoing.GCM.throttled|GCM limitadas notificações|Contagem|Total|Olá, contagem de pushes falhou porque o GCM limitadas esta aplicação (código de estado do GCM: 501-599 ou resultado: disponível).|
|Outgoing.GCM.invalidnotificationformat|Formato de notificação inválido do GCM|Contagem|Total|Olá, contagem de pushes falhou porque o payload de Olá não foi formatada corretamente (resultado do GCM: InvalidDataKey ou InvalidTtl).|
|Outgoing.GCM.invalidnotificationsize|Erro de tamanho de notificação inválido do GCM|Contagem|Total|Olá, contagem de pushes falhou porque o payload de Olá era demasiado grande (resultado do GCM: MessageTooBig).|
|Outgoing.GCM.wrongchannel|Erro de canal de problema do GCM|Contagem|Total|Contagem de Olá de pushes falhou porque Olá registrationId no registo de Olá não está associado à aplicação atual toohello (resultado do GCM: InvalidPackageName).|
|Outgoing.GCM.pnserror|Erros GCM|Contagem|Total|Contagem de Olá de pushes que falharam devido a erros de comunicação com o GCM.|
|Outgoing.GCM.authenticationerror|Erros de autenticação do GCM|Contagem|Total|Olá, contagem de pushes falhou porque Olá PNS não aceitou Olá fornecidas credenciais de Olá credenciais são bloqueadas ou Olá SenderId não está corretamente configurado na aplicação Olá (resultado do GCM: MismatchedSenderId).|
|Outgoing.mpns.Success|Notificações com êxito do MPNS|Contagem|Total|Contagem de Olá de todas as notificações com êxito.|
|Outgoing.mpns.invalidcredentials|Credenciais inválidas MPNS|Contagem|Total|Contagem de Olá de pushes que falhou porque Olá PNS não aceitou Olá fornecidas credenciais ou credenciais Olá estão bloqueadas.|
|Outgoing.mpns.badchannel|Erro de canal do MPNS incorreta|Contagem|Total|Olá, contagem de pushes falhou porque não foi reconhecido Olá ChannelURI no registo de Olá (estado MPNS: 404 não encontrado).|
|Outgoing.mpns.throttled|MPNS limitadas notificações|Contagem|Total|Olá, contagem de pushes falhou porque o MPNS é a limitação esta aplicação (WNS MPNS: 406 Não aceitável).|
|Outgoing.mpns.invalidnotificationformat|Formato de notificação inválido do MPNS|Contagem|Total|Contagem de Olá de pushes que falhou porque o payload de Olá de notificação de Olá era demasiado grande.|
|Outgoing.mpns.channeldisconnected|Canal de MPNS desligado|Contagem|Total|Olá, contagem de pushes falhou porque foi desligada Olá ChannelURI no registo de Olá (estado MPNS: 412 não encontrado).|
|Outgoing.mpns.dropped|Notificações de ignorados do MPNS|Contagem|Total|Olá, contagem de pushes que foram ignorados pelo MPNS (cabeçalho de resposta do MPNS: X NotificationStatus: QueueFull ou Suppressed).|
|Outgoing.mpns.pnserror|Erros MPNS|Contagem|Total|Contagem de Olá de pushes que falharam devido a erros de comunicação com MPNS.|
|Outgoing.mpns.authenticationerror|Erros de autenticação do MPNS|Contagem|Total|Contagem de Olá de pushes que falhou porque Olá PNS não aceitou Olá fornecidas credenciais ou credenciais Olá estão bloqueadas.|
|notificationhub.pushes|Todas as notificações de saída|Contagem|Total|Todas as notificações de saída do hub de notificação de Olá|
|incoming.all.Requests|Todos os pedidos recebidos|Contagem|Total|Total de pedidos recebidos para um hub de notificação|
|incoming.all.failedrequests|Entrada de todos os pedidos falhados|Contagem|Total|Total de pedidos falhados recebidos para um hub de notificação|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|qpu_metric|QPU|Contagem|Média|QPU. Intervalo de 0-100 para S1, 0-200 para S2 e 0-400 para S4|
|memory_metric|Memória|Bytes|Média|Memória. No intervalo 0-25 GB para S1, 0 a 50 GB para S2 e 0-100 GB para S4|
|TotalConnectionRequests|Pedidos de ligação total|Contagem|Média|Pedidos de ligação total. Estes são arrivals.|
|SuccessfullConnectionsPerSec|Ligações com êxito por seg|CountPerSecond|Média|Taxa de conclusões de ligação com êxito.|
|TotalConnectionFailures|Falhas de ligação total|Contagem|Média|Total de tentativas de ligação falhadas.|
|CurrentUserSessions|Sessões de utilizador atual|Contagem|Média|Número atual de sessões de utilizador estabelecida.|
|QueryPoolBusyThreads|Threads de ocupado de conjunto de consulta|Contagem|Média|Número de threads ocupados no conjunto de threads de consulta Olá.|
|CommandPoolJobQueueLength|Comprimento de fila de tarefa de conjunto de comandos|Contagem|Média|Número de tarefas numa fila de Olá do conjunto de threads de comando Olá.|
|ProcessingPoolJobQueueLength|Comprimento de fila de tarefa de conjunto de processamento|Contagem|Média|Número de tarefas não-I/O na fila de Olá de Olá conjunto de threads de processamento.|
|CurrentConnections|Ligação: Ligações atuais|Contagem|Média|Número atual de ligações de cliente estabelecido.|
|CleanerCurrentPrice|Memória: Preço atual de limpeza|Contagem|Média|Preço atual de memória, $/ byte/hora, too1000 normalizado.|
|CleanerMemoryShrinkable|Memória: Memória de limpeza que possam ser encolhida|Bytes|Média|Quantidade de memória, em bytes, assunto toopurging por fundo Olá limpeza.|
|CleanerMemoryNonshrinkable|Memória: Memória nonshrinkable de limpeza|Bytes|Média|Quantidade de memória, em bytes, não requerente toopurging por fundo Olá limpeza.|
|MemoryUsage|Memória: Utilização de memória|Bytes|Média|Utilização de memória de processo do servidor Olá como utilizado para calcular preço de memória de limpeza. Igual a toocounter Process\PrivateBytes plus Olá tamanho dos dados de mapeamento de memória, ignorando quaisquer memória que foi mapeada ou atribuída pelo Olá xVelocity análise na memória motor (VertiPaq) que excedam o motor de xVelocity Olá limite de memória.|
|MemoryLimitHard|Memória: Disco rígido de limite de memória|Bytes|Média|Limite de memória de disco rígido, ficheiro de configuração.|
|MemoryLimitHigh|Memória: Limite de memória elevada|Bytes|Média|Limite de memória elevada, ficheiro de configuração.|
|MemoryLimitLow|Memória: Baixa de limite de memória|Bytes|Média|Limite de memória insuficiente, ficheiro de configuração.|
|MemoryLimitVertiPaq|Memória: VertiPaq de limite de memória|Bytes|Média|Limite de memória, ficheiro de configuração.|
|Quota|Memória: Quota|Bytes|Média|Quota atual de memória, em bytes. Quota de memória também é conhecido como uma reserva de memória ou de concessão de memória.|
|QuotaBlocked|Memória: Quota bloqueado|Contagem|Média|Número atual de pedidos de quota são bloqueada até que outros quotas de memória são libertadas.|
|VertiPaqNonpaged|Memória: VertiPaq na memória não paginável|Bytes|Média|Bytes de memória bloqueado no conjunto de trabalho de Olá para utilização por motor dentro da memória de Olá.|
|VertiPaqPaged|Memória: VertiPaq bloco paginado|Bytes|Média|Bytes de memória paginada em utilização para dados em memória.|
|RowsReadPerSec|Processamento: Linhas lidas por seg|CountPerSecond|Média|Taxa de linhas lida todas as bases de dados relacionais.|
|RowsConvertedPerSec|Processamento: Converter o linhas por seg|CountPerSecond|Média|Taxa de linhas converter durante o processamento.|
|RowsWrittenPerSec|Processamento: Linhas escritas por seg|CountPerSecond|Média|Taxa de linhas escritos durante o processamento.|
|CommandPoolBusyThreads|Threads: Threads ocupado do conjunto de comandos|Contagem|Média|Número de threads ocupados no conjunto de threads de comando Olá.|
|CommandPoolIdleThreads|Threads: Threads de inatividade do conjunto de comandos|Contagem|Média|Número de threads Inativos no conjunto de threads de comando Olá.|
|LongParsingBusyThreads|Threads: Análise de threads ocupados de longa|Contagem|Média|Número de threads ocupados no Olá longa analisar o conjunto de threads.|
|LongParsingIdleThreads|Threads: Longa análise threads Inativos|Contagem|Média|Número de threads Inativos no Olá longa analisar o conjunto de threads.|
|LongParsingJobQueueLength|Threads: Análise longa comprimento da fila de tarefas|Contagem|Média|Número de tarefas numa fila de Olá de Olá longa analisar o conjunto de threads.|
|ProcessingPoolBusyIOJobThreads|Threads: Threads de trabalho de e/s ocupados do conjunto de processamento|Contagem|Média|Número de threads em execução tarefas de e/s no conjunto de threads de processamento de Olá.|
|ProcessingPoolBusyNonIOThreads|Threads: Threads de não-I/O ocupado do conjunto de processamento|Contagem|Média|Número de threads em execução de tarefas não-I/O no conjunto de threads de processamento de Olá.|
|ProcessingPoolIOJobQueueLength|Threads: Conjunto de comprimento de fila de trabalho de e/s de processamento|Contagem|Média|Número de tarefas de e/s na fila de Olá de Olá conjunto de threads de processamento.|
|ProcessingPoolIdleIOJobThreads|Threads: Conjunto Inativos threads de trabalho de e/s de processamento|Contagem|Média|Número de threads de inatividade para as tarefas de e/s no conjunto de threads de processamento de Olá.|
|ProcessingPoolIdleNonIOThreads|Threads: Threads de não-I/O inativo do conjunto de processamento|Contagem|Média|Número de threads Inativos no conjunto de threads de processamento de Olá dedicada tarefas toonon-I/O.|
|QueryPoolIdleThreads|Threads: Threads de inatividade do conjunto de consulta|Contagem|Média|Número de threads de inatividade para as tarefas de e/s no conjunto de threads de processamento de Olá.|
|QueryPoolJobQueueLength|Threads: Lengt de fila de tarefa de conjunto de consulta|Contagem|Média|Número de tarefas numa fila de Olá do conjunto de threads de consulta Olá.|
|ShortParsingBusyThreads|Threads: Curto período análise threads ocupados|Contagem|Média|Número de threads ocupados no Olá pequeno conjunto de threads de análise.|
|ShortParsingIdleThreads|Threads: Curto período análise threads Inativos|Contagem|Média|Número de threads Inativos no Olá pequeno conjunto de threads de análise.|
|ShortParsingJobQueueLength|Threads: Curto período comprimento de fila de tarefa de análise|Contagem|Média|Número de tarefas numa fila de Olá de Olá pequeno conjunto de threads de análise.|
|memory_thrashing_metric|Memória Thrashing|Percentagem|Média|Thrashing média da memória.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|SearchLatency|Latência de pesquisa|Segundos|Média|Latência média de pesquisa para o serviço de pesquisa de Olá|
|SearchQueriesPerSecond|Consultas de pesquisa por segundo|CountPerSecond|Média|Consultas de pesquisa de serviço de pesquisa de Olá por segundo|
|ThrottledSearchQueriesPercentage|Percentagem de consultas de pesquisa otimizadas|Percentagem|Média|Percentagem de consultas de pesquisa que foram limitadas para o serviço de pesquisa de Olá|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|CPUXNS|Utilização da CPU por espaço de nomes|Percentagem|Máximo|Métrica de utilização de espaço de nomes da CPU do Service bus premium|
|WSXNS|Utilização de tamanho de memória por espaço de nomes|Percentagem|Máximo|Métrica de utilização de memória do Service bus premium espaço de nomes|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|cpu_percent|Percentagem de CPU|Percentagem|Média|Percentagem de CPU|
|physical_data_read_percent|Percentagem de ES de Dados|Percentagem|Média|Percentagem de ES de Dados|
|log_write_percent|Percentagem de es do registo|Percentagem|Média|Percentagem de es do registo|
|dtu_consumption_percent|Percentagem de DTU|Percentagem|Média|Percentagem de DTU|
|Armazenamento|Tamanho total da base de dados|Bytes|Máximo|Tamanho total da base de dados|
|connection_successful|Ligações com êxito|Contagem|Total|Ligações com êxito|
|connection_failed|Falha de ligações|Contagem|Total|Falha de ligações|
|blocked_by_firewall|Bloqueado pela Firewall|Contagem|Total|Bloqueado pela Firewall|
|impasse|Impasses|Contagem|Total|Impasses|
|storage_percent|Percentagem de tamanho da Base de Dados|Percentagem|Máximo|Percentagem de tamanho da Base de Dados|
|xtp_storage_percent|Percentagem de armazenamento do OLTP dentro da memória|Percentagem|Média|Percentagem de armazenamento do OLTP dentro da memória|
|workers_percent|Percentagem de trabalhadores|Percentagem|Média|Percentagem de trabalhadores|
|sessions_percent|Percentagem de sessões|Percentagem|Média|Percentagem de sessões|
|dtu_limit|Limite DTU|Contagem|Média|Limite DTU|
|dtu_used|DTU utilizado|Contagem|Média|DTU utilizado|
|dwu_limit|Limite DWU|Contagem|Máximo|Limite DWU|
|dwu_consumption_percent|Percentagem DWU|Percentagem|Máximo|Percentagem DWU|
|dwu_used|DWU utilizado|Contagem|Máximo|DWU utilizado|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|cpu_percent|Percentagem de CPU|Percentagem|Média|Percentagem de CPU|
|database_cpu_percent|Percentagem de CPU|Percentagem|Média|Percentagem de CPU|
|physical_data_read_percent|Percentagem de ES de Dados|Percentagem|Média|Percentagem de ES de Dados|
|database_physical_data_read_percent|Percentagem de ES de Dados|Percentagem|Média|Percentagem de ES de Dados|
|log_write_percent|Percentagem de es do registo|Percentagem|Média|Percentagem de es do registo|
|database_log_write_percent|Percentagem de es do registo|Percentagem|Média|Percentagem de es do registo|
|dtu_consumption_percent|Percentagem de DTU|Percentagem|Média|Percentagem de DTU|
|database_dtu_consumption_percent|Percentagem de DTU|Percentagem|Média|Percentagem de DTU|
|storage_percent|Percentagem de armazenamento|Percentagem|Média|Percentagem de armazenamento|
|workers_percent|Percentagem de trabalhadores|Percentagem|Média|Percentagem de trabalhadores|
|database_workers_percent|Percentagem de trabalhadores|Percentagem|Média|Percentagem de trabalhadores|
|sessions_percent|Percentagem de sessões|Percentagem|Média|Percentagem de sessões|
|database_sessions_percent|Percentagem de sessões|Percentagem|Média|Percentagem de sessões|
|eDTU_limit|limite de eDTU|Contagem|Média|limite de eDTU|
|storage_limit|Limite de armazenamento|Bytes|Média|Limite de armazenamento|
|eDTU_used|eDTU utilizado|Contagem|Média|eDTU utilizado|
|storage_used|Armazenamento utilizado|Bytes|Média|Armazenamento utilizado|
|database_storage_used|Armazenamento utilizado|Bytes|Média|Armazenamento utilizado|
|xtp_storage_percent|Percentagem de armazenamento do OLTP dentro da memória|Percentagem|Média|Percentagem de armazenamento do OLTP dentro da memória|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|dtu_consumption_percent|Percentagem de DTU|Percentagem|Média|Percentagem de DTU|
|database_dtu_consumption_percent|Percentagem de DTU|Percentagem|Média|Percentagem de DTU|
|storage_used|Armazenamento utilizado|Bytes|Média|Armazenamento utilizado|
|database_storage_used|Armazenamento utilizado|Bytes|Média|Armazenamento utilizado|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|ResourceUtilization|% De utilização de SU|Percentagem|Máximo|% De utilização de SU|
|InputEvents|Eventos de entrada|Contagem|Total|Eventos de entrada|
|InputEventBytes|Bytes do evento de entrada|Bytes|Total|Bytes do evento de entrada|
|LateInputEvents|Eventos de entrada de enlace tardio|Contagem|Total|Eventos de entrada de enlace tardio|
|OutputEvents|Eventos de saída|Contagem|Total|Eventos de saída|
|ConversionErrors|Erros de conversão de dados|Contagem|Total|Erros de conversão de dados|
|Erros|Erros de Runtime|Contagem|Total|Erros de Runtime|
|DroppedOrAdjustedEvents|Eventos fora de ordem|Contagem|Total|Eventos fora de ordem|
|AMLCalloutRequests|Pedidos de função|Contagem|Total|Pedidos de função|
|AMLCalloutFailedRequests|Pedidos de função falhada|Contagem|Total|Pedidos de função falhada|
|AMLCalloutInputEvents|Eventos de função|Contagem|Total|Eventos de função|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|CpuPercentage|Percentagem de CPU|Percentagem|Média|Percentagem de CPU|
|MemoryPercentage|Percentagem de memória|Percentagem|Média|Percentagem de memória|
|DiskQueueLength|Comprimento da fila de disco|Contagem|Total|Comprimento da fila de disco|
|HttpQueueLength|Comprimento da fila de HTTP|Contagem|Total|Comprimento da fila de HTTP|
|BytesReceived|Dados em|Bytes|Total|Dados em|
|BytesSent|Dados de saída|Bytes|Total|Dados de saída|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (excluindo as funções)

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|CpuTime|Tempo de CPU|Segundos|Total|Tempo de CPU|
|Pedidos|Pedidos|Contagem|Total|Pedidos|
|BytesReceived|Dados em|Bytes|Total|Dados em|
|BytesSent|Dados de saída|Bytes|Total|Dados de saída|
|Http101|HTTP 101|Contagem|Total|HTTP 101|
|Http2xx|2xx de HTTP|Contagem|Total|2xx de HTTP|
|Http3xx|3xx de HTTP|Contagem|Total|3xx de HTTP|
|Http401|HTTP 401|Contagem|Total|HTTP 401|
|Http403|HTTP 403|Contagem|Total|HTTP 403|
|Http404|HTTP 404|Contagem|Total|HTTP 404|
|Http406|HTTP 406|Contagem|Total|HTTP 406|
|Http4xx|4xx de HTTP|Contagem|Total|4xx de HTTP|
|Http5xx|Erros de servidor de HTTP|Contagem|Total|Erros de servidor de HTTP|
|MemoryWorkingSet|Conjunto de trabalho de memória|Bytes|Média|Conjunto de trabalho de memória|
|AverageMemoryWorkingSet|Memória média conjunto de trabalho|Bytes|Média|Memória média conjunto de trabalho|
|AverageResponseTime|Tempo de resposta médio|Segundos|Média|Tempo de resposta médio|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (funções)

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|BytesReceived|Dados em|Bytes|Total|Dados em|
|BytesSent|Dados de saída|Bytes|Total|Dados de saída|
|Http5xx|Erros de servidor de HTTP|Contagem|Total|Erros de servidor de HTTP|
|MemoryWorkingSet|Conjunto de trabalho de memória|Bytes|Média|Conjunto de trabalho de memória|
|AverageMemoryWorkingSet|Memória média conjunto de trabalho|Bytes|Média|Memória média conjunto de trabalho|
|FunctionExecutionUnits|Unidades de execução de função|Contagem|Média|Unidades de execução de função|
|FunctionExecutionCount|Contagem de execução de função|Contagem|Média|Contagem de execução de função|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Métrica|Nome a apresentar métrica|Unidade|Tipo de agregação|Descrição|
|---|---|---|---|---|
|CpuTime|Tempo de CPU|Segundos|Total|Tempo de CPU|
|Pedidos|Pedidos|Contagem|Total|Pedidos|
|BytesReceived|Dados em|Bytes|Total|Dados em|
|BytesSent|Dados de saída|Bytes|Total|Dados de saída|
|Http101|HTTP 101|Contagem|Total|HTTP 101|
|Http2xx|2xx de HTTP|Contagem|Total|2xx de HTTP|
|Http3xx|3xx de HTTP|Contagem|Total|3xx de HTTP|
|Http401|HTTP 401|Contagem|Total|HTTP 401|
|Http403|HTTP 403|Contagem|Total|HTTP 403|
|Http404|HTTP 404|Contagem|Total|HTTP 404|
|Http406|HTTP 406|Contagem|Total|HTTP 406|
|Http4xx|4xx de HTTP|Contagem|Total|4xx de HTTP|
|Http5xx|Erros de servidor de HTTP|Contagem|Total|Erros de servidor de HTTP|
|MemoryWorkingSet|Conjunto de trabalho de memória|Bytes|Média|Conjunto de trabalho de memória|
|AverageMemoryWorkingSet|Memória média conjunto de trabalho|Bytes|Média|Memória média conjunto de trabalho|
|AverageResponseTime|Tempo de resposta médio|Segundos|Média|Tempo de resposta médio|
|FunctionExecutionUnits|Unidades de execução de função|Contagem|Média|Unidades de execução de função|
|FunctionExecutionCount|Contagem de execução de função|Contagem|Média|Contagem de execução de função|

## <a name="next-steps"></a>Passos seguintes
* [Leia sobre as métricas no Monitor do Azure](monitoring-overview-metrics.md)
* [Criar alertas nas métricas](insights-receive-alert-notifications.md)
* [Exportar toostorage de métricas, Hub de eventos ou análise de registos](monitoring-overview-of-diagnostic-logs.md)
