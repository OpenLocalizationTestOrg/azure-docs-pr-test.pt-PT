---
title: "aaaAzure ServiceFabric diagnóstico e monitorização | Microsoft Docs"
description: "Este artigo descreve as funcionalidades de monitorização de desempenho de Olá no tempo de execução da ServiceRemoting fiável do Service Fabric Olá, como os contadores de desempenho emitidos pelo-lo."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Diagnóstico e monitorização de desempenho para fiável de serviço de gestão remota
tempo de execução do Olá ServiceRemoting fiável emite [contadores de desempenho](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Estes fornecem informações sobre como Olá ServiceRemoting está a funcionar e ajudam a resolver problemas e monitorização do desempenho.


## <a name="performance-counters"></a>Contadores de desempenho
tempo de execução do Olá ServiceRemoting fiável define Olá seguintes categorias de contador de desempenho:

| Categoria | Descrição |
| --- | --- |
| Serviço de recursos de infraestrutura |Contadores específico tooAzure comunicação remota de serviço de recursos de infraestrutura de serviço, por exemplo, tempo médio necessário tooprocess pedido |
| Método do serviço de recursos de infraestrutura de serviço |Toomethods específico contadores implementada pelo serviço de comunicação remota do serviço de recursos de infraestrutura, por exemplo, com que frequência um método de serviço é invocado |

Cada um dos Olá precedente categorias tem um ou mais contadores.

Olá [Monitor de desempenho do Windows](https://technet.microsoft.com/library/cc749249.aspx) aplicação que está disponível por predefinição no sistema de operativo do Windows hello pode ser utilizados dados de contador de desempenho de toocollect e vista. [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) é outra opção para recolher dados de contador de desempenho e carregá-lo tooAzure tabelas.

### <a name="performance-counter-instance-names"></a>Nomes de instâncias do contador de desempenho
Um cluster com um grande número de partições ou de serviços de ServiceRemoting ter um grande número de instâncias do contador de desempenho. instância do contador de desempenho Olá nomes podem ajudar a identificar partição específica Olá e método do serviço (se aplicável) essa instância de contador de desempenho de Olá está associada.

#### <a name="service-fabric-service-category"></a>Categoria de serviço do Service Fabric
Para a categoria de Olá `Service Fabric Service`, os nomes de instâncias do contador Olá estão em Olá seguinte formato:

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* é Olá representação de cadeia de Olá ID de partição de Service Fabric Olá instância do contador de desempenho está associado. ID de partição Olá é um GUID e respetiva representação de cadeia que é gerada através de Olá [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método com o especificador de formato "D".

*ServiceReplicaOrInstanceId* é Olá representação de cadeia de Olá ID de réplica/instância de recursos de infraestrutura de serviço Olá instância do contador de desempenho está associado.

*ServiceRuntimeInternalID* é Olá representação de um número inteiro de 64 bits que é gerado pelo runtime do serviço de recursos de infraestrutura de Olá a sua utilização interna. Isto está incluído na instância do contador de desempenho de Olá nome tooensure a exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os utilizadores não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de Olá.

Olá segue-se um exemplo de um nome de instância do contador para um contador que pertence toohello `Service Fabric Service` categoria:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

No Olá anterior exemplo, `2740af29-78aa-44bc-a20b-7e60fb783264` é Olá representação de cadeia de ID de partição de Service Fabric Olá, `635650083799324046` é representação de cadeia de réplica/InstanceId e `5008379932` Olá ID de 64 bits que é gerado para o tempo de execução Olá 's interno Utilize.

#### <a name="service-fabric-service-method-category"></a>Categoria de método do serviço de recursos de infraestrutura de serviço
Para a categoria de Olá `Service Fabric Service Method`, os nomes de instâncias do contador Olá estão em Olá seguinte formato:

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* é o nome de Olá do método do serviço de Olá que Olá instância do contador de desempenho está associado. formato de Olá do nome do método Olá é determinado com base em algumas lógica no tempo de execução do serviço de recursos de infraestrutura Olá equilibrar o facilitar a leitura do nome de Olá com restrições de comprimento de máximo de Olá dos nomes de instância de contador de desempenho de Olá no Windows hello.

*ServiceRuntimeMethodId* é Olá representação de um número inteiro de 32 bits que é gerado pelo runtime do serviço de recursos de infraestrutura de Olá a sua utilização interna. Isto está incluído na instância do contador de desempenho de Olá nome tooensure a exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os utilizadores não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de Olá.

*ServiceFabricPartitionID* é Olá representação de cadeia de Olá ID de partição de Service Fabric Olá instância do contador de desempenho está associado. ID de partição Olá é um GUID e respetiva representação de cadeia que é gerada através de Olá [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método com o especificador de formato "D".

*ServiceReplicaOrInstanceId* é Olá representação de cadeia de Olá ID de réplica/instância de recursos de infraestrutura de serviço Olá instância do contador de desempenho está associado.

*ServiceRuntimeInternalID* é Olá representação de um número inteiro de 64 bits que é gerado pelo runtime do serviço de recursos de infraestrutura de Olá a sua utilização interna. Isto está incluído na instância do contador de desempenho de Olá nome tooensure a exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os utilizadores não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de Olá.

Olá segue-se um exemplo de um nome de instância do contador para um contador que pertence toohello `Service Fabric Service Method` categoria:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

No Olá anterior exemplo, `ivoicemailboxservice.leavemessageasync` é o nome do método Olá, `2` é Olá utilizar ID de 32 bits gerado para o tempo de execução Olá 's interno, `89383d32-e57e-4a9b-a6ad-57c6792aa521` é Olá representação de cadeia de ID de partição de Service Fabric Olá,`635650083804480486` é Olá cadeia representação de Olá ID de réplica/instância do serviço de recursos de infraestrutura e `5008380` é utilizar ID de 64 bits de Olá gerado para o tempo de execução Olá 's interno.

## <a name="list-of-performance-counters"></a>Lista de contadores de desempenho
### <a name="service-method-performance-counters"></a>Contadores de desempenho de método do serviço

tempo de execução de serviço fiável de Olá publica Olá seguir execução toohello relacionados de contadores de desempenho dos métodos do serviço.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Método do serviço de recursos de infraestrutura de serviço |Invocações por segundo |Número de vezes que o método do serviço Olá é invocado por segundo |
| Método do serviço de recursos de infraestrutura de serviço |Média em milissegundos por invocação |Tempo decorrido método do serviço tooexecute Olá em milissegundos |
| Método do serviço de recursos de infraestrutura de serviço |Exceções emitidas/seg |Número de vezes que Olá método do serviço emitiu uma exceção por segundo |

### <a name="service-request-processing-performance-counters"></a>Contadores de desempenho de processamento de pedido de serviço
Quando um cliente invoca um método através de um objeto de proxy de serviço, o que resulta numa mensagem de pedido enviada ao longo do serviço de comunicação remota do Olá rede toohello. serviço de Olá processa a mensagem de pedido de saudação e envia um cliente de back-toohello de resposta. tempo de execução do Olá ServiceRemoting fiável publica Olá após o processamento de pedidos de tooservice relacionados de contadores de desempenho.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Serviço de recursos de infraestrutura |n. º de pedidos pendentes |Número de pedidos a ser processado no service Olá |
| Serviço de recursos de infraestrutura |Média em milissegundos por pedido |Tempo decorrido (em milissegundos) por Olá serviço tooprocess um pedido |
| Serviço de recursos de infraestrutura |Média em milissegundos para a desserialização do pedido |Mensagem de pedido de serviço do tempo decorrido (em milissegundos) toodeserialize quando recebido no serviço de Olá |
| Serviço de recursos de infraestrutura |Média em milissegundos para a serialização da resposta |Mensagem de resposta do serviço do tempo decorrido (em milissegundos) tooserialize Olá serviço Olá antes do envio de resposta Olá toohello cliente |

## <a name="next-steps"></a>Passos seguintes
* [Código de exemplo](https://github.com/Azure/servicefabric-samples)
* [Fornecedores de EventSource no PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
