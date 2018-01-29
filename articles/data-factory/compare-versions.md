---
title: "Compare as versões do Azure Data Factory 1 e 2 | Microsoft Docs"
description: Este artigo compara o Azure Data Factory V1 e o Azure Data Factory V2.
services: data-factory
documentationcenter: 
author: kromerm
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/24/2018
ms.author: makromer
ms.openlocfilehash: 83065e6cacd784a3914cfac3ff2552a712688366
ms.sourcegitcommit: 79683e67911c3ab14bcae668f7551e57f3095425
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/25/2018
---
# <a name="compare-azure-data-factory-v1-and-v2"></a>Comparar Azure Data Factory V1 e V2
Este artigo compara a V2 e a V1 do Azure Data Factory. Para uma introdução ao V1, veja [Introdução ao Azure Data Factory](v1/data-factory-introduction.md). Para uma introdução ao V2, veja [Introdução ao Azure Data Factory (V2 – pré-visualização)](introduction.md).

## <a name="feature-comparison"></a>Comparação de funcionalidades
A tabela seguinte compara as funcionalidades do V1 e do V2. 

| Funcionalidade | Versão 1 | Versão 2 | 
| ------- | --------- | --------- | 
| Conjuntos de dados | Uma vista com o nome dos dados que fazem referência aos dados que pretende utilizar nas suas atividades como entradas e saídas. Os conjuntos de dados identificam dados dentro de diferentes arquivos de dados, como tabelas, ficheiros, pastas e documentos. Por exemplo, um conjunto de dados de Blobs do Azure especifica o contentor de blobs e a pasta no armazenamento de Blobs do Azure a partir dos quais a atividade deve ler os dados.<br/><br/>A **Disponibilidade** define o modelo de fragmentação da janela de processamento para o conjunto de dados (por exemplo, hora a hora, diária e assim sucessivamente). | Os conjuntos de dados são os mesmos no V2. No entanto, não terá de definir agendas de **disponibilidade** para conjuntos de dados. Pode definir um recurso de acionador que agende os pipelines a partir de um paradigma de programador de relógio. Para obter mais informações, veja [Acionadores](concepts-pipeline-execution-triggers.md#triggers) e [Conjuntos de dados](concepts-datasets-linked-services.md). | 
| Serviços ligados | Os serviços ligados são muito semelhantes às cadeias de ligação, que definem as informações de ligação necessárias para que o Data Factory se possa ligar a recursos externos. | Os serviços ligados são os mesmo que no Data Factory V1, mas com uma nova propriedade **connectVia** para utilizar o ambiente de computação do Data Factory V2 Integration Runtime. Para obter mais informações, consulte [Runtimes de integração no Azure Data Factory](concepts-integration-runtime.md) e [Propriedades de serviço ligado para o armazenamento de Blobs do Azure](connector-azure-blob-storage.md#linked-service-properties). |
| Pipelines | Uma fábrica de dados pode ter um ou mais pipelines. Os pipelines são agrupamentos lógicos de atividades que, em conjunto, realizam uma tarefa. Vai utilizar StartTime, endTime e isPaused para agendar e executar pipelines. | Os pipelines são grupos de atividades que são executados nos dados. No entanto, o agendamento de atividades no pipeline foi separado em novos recursos de acionador. Pode considerar os pipelines V2 no Data Factory como "unidades de fluxo de trabalho" que agenda em separado através de acionadores. <br/><br/>Os pipelines não dispõem de "janelas" da execução de tempo no Data Factory V2. Os conceitos startTime, endTime e isPaused do Data Factory V1 já não estão presentes no Data Factory V2. Para obter mais informações, veja o artigo [Execuções de pipelines e acionadores](concepts-pipeline-execution-triggers.md) e [Pipelines e atividades](concepts-pipelines-activities.md). |
| Atividades | As atividades definem ações a realizar nos seus dados, dentro de um pipeline. O movimento de dados (atividade de cópia) e as atividades de transformação de dados (tais como o Hive, Pig e MapReduce) são suportadas. | No Data Factory V2, as atividades ainda são ações definidas dentro de um pipeline. O V2 apresenta novas [atividades de fluxo de controlo](concepts-pipelines-activities.md#control-activities). Vai utilizar estas atividades no fluxo de controlo (ciclo e ramificação). As atividades de movimento de dados e transformação de dados que eram suportadas no V1 são suportadas no V2. Pode definir as atividades de transformação sem utilizar os conjuntos de dados no V2. |
| Movimento de dados híbridos e distribuição de atividades | Agora conhecido como Integration Runtime, o [Gateway de Gestão de Dados](v1/data-factory-data-management-gateway.md) suportava movimentar dados entre o local e a cloud.| O Gateway de Gestão de Dados agora chama-se Integration Runtime Autoalojado. Fornece a mesma capacidade que no V1. <br/><br/> O Azure-SSIS Integration Runtime no V2 também suporta a implementação e execução de pacotes do SQL Server Integration Services (SSIS) na cloud. Para obter mais informações, veja [Integration runtime no Azure Data Factory](concepts-integration-runtime.md).|
| Parâmetros | ND | Os parâmetros são pares chave-valor das definições de configuração só de leitura que estão definidas em pipelines. Pode passar os argumentos para os parâmetros quando está a executar manualmente o pipeline. Se estiver a utilizar um acionador de agendador, o acionador também pode passar valores para os parâmetros. As atividades dentro do pipeline consomem os valores dos parâmetros.  |
| Expressões | O Data Factory V1 permite-lhe utilizar funções e variáveis de sistema em consultas de seleção de dados e propriedades de atividade/conjuntos de dados. | No Data Factory V2, pode utilizar expressões em qualquer parte de um valor de cadeia de carateres JSON. Para mais informações, consulte [Expressões e funções no V2](control-flow-expression-language-functions.md).|
| Execuções de pipeline | ND | Uma única instância de uma execução de pipeline. Por exemplo, imagine que tem um pipeline que é executado às 08:00, às 09: 00 e às 10:00. Neste caso, existem três execuções separadas do pipeline (execuções de pipeline). Cada execução de pipeline tem um ID de execução de pipeline exclusivo. A execução de pipeline é um GUID que define exclusivamente essa execução em particular. Normalmente, as execuções de pipeline são instanciadas pela transmissão de argumentos a parâmetros que são definidos nos pipelines. |
| Execuções de atividade | ND | Uma instância de uma execução de atividade dentro de um pipeline. | 
| Execuções de acionador | ND | Uma instância de uma execução do acionador. Para obter mais informações, consulte [Acionadores](concepts-pipeline-execution-triggers.md). |
| Agendamento | O agendamento baseia-se nas horas de início/fim do pipeline e na disponibilidade do conjunto de dados. | Acionador de agendador ou execução através de agendador externo. Para mais informações, consulte [Execuções de pipelines e acionadores](concepts-pipeline-execution-triggers.md). |

As secções seguintes fornecem mais informações sobre as capacidades da V2. 

## <a name="control-flow"></a>Fluxo de controlo  
Para suportar os diversos fluxos e padrões de integração nos armazéns de dados modernos, o Data Factory V2 disponibiliza um novo modelo de pipeline de dados flexível, que já não está associado a dados de séries de tempo. Alguns fluxos comuns que anteriormente não era possíveis, agora são possíveis. Estes modelos são descritos nas secções seguintes.   

### <a name="chaining-activities"></a>Encadeamento de atividades
Na V1, tinha que configurar a saída de uma atividade como a entrada de outra atividade para as encadear. No V2, pode encadear atividades numa sequência dentro de um pipeline. Pode utilizar a propriedade **dependsOn** numa definição de atividade para encadeá-la com uma atividade de origem. Para obter mais informações e um exemplo, consulte [Pipelines e atividades](concepts-pipelines-activities.md#multiple-activities-in-a-pipeline) e [Ramificar e encadear atividades](tutorial-control-flow.md). 

### <a name="branching-activities"></a>Ramificar atividades
Na V2, pode ramificar atividades dentro de um pipeline. A [atividade condição-If](control-flow-if-condition-activity.md) disponibiliza a mesma funcionalidade que as instruções `if` fornecem nas linguagens de programação. Avalia um conjunto de atividades quando a condição é avaliada como `true` e outro conjunto de atividades quando é avaliada como `false`. Para obter um exemplo de ramificação de atividades, consulte o tutorial [Ramificar e encadear atividades](tutorial-control-flow.md).

### <a name="parameters"></a>Parâmetros 
Pode definir parâmetros ao nível do pipeline e passar argumentos quando é invocado o pipeline a pedido ou a partir de um acionador. As atividades podem consumir os argumentos transmitidos para o pipeline Para mais informações, consulte [Pipelines e acionadores](concepts-pipeline-execution-triggers.md). 

### <a name="custom-state-passing"></a>Transmissão de estado personalizado
Os resultados das atividades, incluindo o estado, podem ser consumidos por uma atividade subsequente no pipeline. Por exemplo, na definição de JSON de uma atividade, pode aceder à saída da atividade anterior com a seguinte sintaxe: `@activity('NameofPreviousActivity').output.value`. Ao utilizar esta funcionalidade, pode criar fluxos de trabalho em que os valores podem passar por atividades.

### <a name="looping-containers"></a>Contentores de ciclo
A [atividade ForEach](control-flow-for-each-activity.md) define um fluxo de controlo de repetição no seu pipeline. Esta atividade itera uma coleção e executa atividades especificadas em ciclo. A implementação de ciclo desta atividade é semelhante à estrutura de ciclo Foreach nas linguagens de programação. 

A atividade [Until](control-flow-until-activity.md) disponibiliza a mesma funcionalidade que uma estrutura de ciclos do-until fornecem nas linguagens de programação. Executa um conjunto de atividades num ciclo até que a condição associada às atividades seja avaliada como `true`. Pode especificar um valor de tempo limite para a atividade Until no Data Factory.  

### <a name="trigger-based-flows"></a>Fluxos baseados em acionadores
Os pipelines podem ser adicionados a pedido ou com base no tempo total de execução. O artigo [pipelines e acionadores](concepts-pipeline-execution-triggers.md) tem informações detalhadas sobre acionadores. 

### <a name="invoking-a-pipeline-from-another-pipeline"></a>Invocar um pipeline de outro pipeline
A [atividade Executar Pipeline](control-flow-execute-pipeline-activity.md) permite que um pipeline do Data Factory invoque outro pipeline.

### <a name="delta-flows"></a>Fluxos delta
Um caso de utilização-chave em padrões ETL é "cargas-delta", na qual apenas os dados que foram alterados desde a última iteração de um pipeline são carregados. As novas funcionalidades na V2, tais como [atividade de pesquisa](control-flow-lookup-activity.md), agendamento flexível e fluxo de controlo permitem este caso de utilização de forma natural. Para um tutorial com instruções passo a passo, consulte [Tutorial: Cópia incremental](tutorial-incremental-copy-powershell.md).

### <a name="other-control-flow-activities"></a>Outras atividades de fluxo de controlo
Seguem-se mais algumas atividades de fluxo de controlo suportadas pelo Data Factory V2. 

Atividade de controlo | Descrição
---------------- | -----------
[Atividade ForEach](control-flow-for-each-activity.md) | Define um fluxo de controlo de repetição no seu pipeline. Esta atividade é utilizada para iterar uma coleção e executa atividades especificadas em ciclo. A implementação de ciclo desta atividade é semelhante à estrutura de ciclo Foreach nas linguagens de programação.
[Atividade Web](control-flow-web-activity.md) | Chama um ponto final REST personalizado a partir de um pipeline do Data Factory. Pode transmitir conjuntos de dados e serviços ligados aos quais a atividade tem acesso e que pode consumir. 
[Atividade de Pesquisa](control-flow-lookup-activity.md) | Lê ou procura um valor de nome de registo ou tabela a partir de qualquer origem externa. Este resultado pode ser ainda referenciado por atividades subsequentes. 
[Atividade Obter metadados](control-flow-get-metadata-activity.md) | Obtém os metadados de quaisquer dados no Azure Data Factory. 
[Atividade Aguardar](control-flow-wait-activity.md) | Coloca em pausa o pipeline durante um período de tempo especificado.

## <a name="deploy-ssis-packages-to-azure"></a>Implementar pacotes do SSIS no Azure 
Vai utilizar o Azure-SSIS se quiser mover as cargas de trabalho SSIS para a cloud, criar uma fábrica de dados com a V2 e aprovisionar um Runtime de Integração Azure-SSIS.

O Integration Runtime do Azure-SSIS é um cluster totalmente gerido de VMs do Azure (nós) dedicadas à execução dos pacotes do SSIS na cloud. Depois de aprovisionar o Integration Runtime do Azure-SSIS, tem as mesmas ferramentas que tem estado a utilizar para implementar pacotes do SSIS num ambiente SSIS local. 

Por exemplo, pode utilizar o SQL Server Data Tools ou o SQL Server Management Studio para implementar pacotes do SSIS neste runtime no Azure. Para obter instruções passo a passo, veja o tutorial [Implementar pacotes de serviços de integração do SQL Server no Azure](tutorial-deploy-ssis-packages-azure.md). 

## <a name="flexible-scheduling"></a>Agendamento flexível
No Data Factory V2, não terá de definir agendas de disponibilidade para conjuntos de dados. Pode definir um recurso de acionador que agende os pipelines a partir de um paradigma de programador de relógio. Pode também passar parâmetros para os pipelines a partir de um acionador para um modelo de agendamento e execução flexível. 

Os pipelines não dispõem de "janelas" da execução de tempo no Data Factory V2. Os conceitos startTime, endTime e isPaused do Data Factory V1 já não existem no Data Factory V2. Para mais informações sobre criação e agendamento de um pipeline no Data Factory V2, veja [Execução e acionadores de pipelines](concepts-pipeline-execution-triggers.md).

## <a name="support-for-more-data-stores"></a>Suporte para mais arquivos de dados
O V2 suporta a cópia de dados de e para mais arquivos de dados que V1. Para obter uma lista dos arquivos de dados suportados, consulte os artigos seguintes:

- [V1 - arquivos de dados suportados](v1/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
- [V2 - arquivos de dados suportados](copy-activity-overview.md#supported-data-stores-and-formats)

## <a name="support-for-on-demand-spark-cluster"></a>Suporte para cluster do Spark a pedido
O V2 suporta a criação de um cluster do Apache Spark do HDInsight do Azure a pedido. Para criar um cluster do Apache Spark a pedido, especifique o tipo de cluster como Spark no seu HDInsight a pedido associado à definição de serviço. Em seguida, pode configurar a atividade do Apache Spark no seu pipeline para utilizar este serviço ligado. 

No runtime, quando a atividade é executada, o serviço Data Factory cria automaticamente o cluster do Spark para si. Para obter mais informações, veja os artigos seguintes:

- [Atividade do Spark no V2](transform-data-using-spark.md)
- [Serviço ligado do Azure HDInsight a pedido](compute-linked-services.md#azure-hdinsight-on-demand-linked-service)

## <a name="custom-activities"></a>Atividades personalizadas
No V1, implementa códigos de atividade DotNet (personalizado) ao criar um projeto de biblioteca de classe .NET com uma classe que implemente o método Execute da interface IDotNetActivity. Portanto, tem de escrever o seu código personalizado no .NET Framework 4.5.2 e executá-lo em nós do Azure Batch Pool baseados em Windows. 

Numa atividade personalizada V2, não tem de implementar uma interface de .NET. Pode executar diretamente comandos de scripts e o seu próprio código personalizado compilado como um executável. 

Para mais informações, consulte [Diferença entre a atividade personalizada no V1 e V2](transform-data-using-dotnet-custom-activity.md#difference-between-custom-activity-in-azure-data-factory-v2-and-custom-dotnet-activity-in-azure-data-factory-v1).

## <a name="sdks"></a>SDKs
 O Data Factory V2 fornece um melhor conjunto de SDKs que podem ser utilizados para criar, gerir e monitorizar pipelines.

- **.NET SDK**: o SDK .NET está atualizado para V2.

- **PowerShell**: os cmdlets do PowerShell estão atualizados para V2. Os cmdlets V2 têm **DataFactoryV2** no nome, por exemplo: Get-AzureRmDataFactoryV2. 

- **Python SDK**: este SDK é novo no V2.

- **REST API**: a API REST está atualizada para V2. 

Os SDKs que são atualizados para a V2 não são compatíveis com versões anteriores com clientes V1. 

## <a name="authoring-experience"></a>Experiência de criação

| &nbsp; | V2 | V1 |
| ------ | -- | -- | 
| Portal do Azure | [Sim](quickstart-create-data-factory-portal.md) | [Sim](data-factory-build-your-first-pipeline-using-editor.md) |
| Azure PowerShell | [Sim](quickstart-create-data-factory-powershell.md) | [Sim](data-factory-build-your-first-pipeline-using-powershell.md) |
| SDK .NET | [Sim](quickstart-create-data-factory-dot-net.md) | [Sim](data-factory-build-your-first-pipeline-using-vs.md) |
| API REST | [Sim](quickstart-create-data-factory-rest-api.md) | [Sim](data-factory-build-your-first-pipeline-using-rest-api.md) |
| SDK Python | [Sim](quickstart-create-data-factory-python.md) | Não |
| Modelo do Resource Manager | [Sim](quickstart-create-data-factory-resource-manager-template.md) | [Sim](data-factory-build-your-first-pipeline-using-arm.md) | 


## <a name="monitoring-experience"></a>Experiência de monitorização
No V2, também pode monitorizar fábricas de dados ao utilizar o [Azure Monitor](monitor-using-azure-monitor.md). Os novos cmdlets do PowerShell suportam a monitorização de [tempos de execução de integração](monitor-integration-runtime.md). Ambos o V1 e V2 suportam monitorização visual através de uma aplicação de monitorização que pode ser aberta a partir do portal do Azure.


## <a name="next-steps"></a>Passos seguintes
Saiba como criar uma fábrica de dados com as instruções passo a passo nos inícios rápidos: [PowerShell](quickstart-create-data-factory-powershell.md), [.NET](quickstart-create-data-factory-dot-net.md), [Python](quickstart-create-data-factory-python.md), [REST API](quickstart-create-data-factory-rest-api.md). 
