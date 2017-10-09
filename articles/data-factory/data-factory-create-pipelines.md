---
title: aaaCreate/agenda Pipelines, atividades de cadeia em Data Factory | Microsoft Docs
description: "Saiba toocreate um pipeline de dados no Azure Data Factory toomove e transforme dados. Crie um dados orientada por informações do fluxo de trabalho tooproduce toouse pronto."
keywords: pipeline de dados, os dados por fluxo de trabalho
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a>Pipelines e atividades de Azure Data Factory
Este artigo ajuda-o a compreender os pipelines e atividades no Azure Data Factory e utilizá-los fluxos de trabalho do tooconstruct ponto a ponto condicionados por dados para o movimento de dados e cenários de processamento de dados.  

> [!NOTE]
> Este artigo pressupõe que já leu [introdução tooAzure Data Factory](data-factory-introduction.md). Se não tiver hands-on-experiência com criar fábricas de dados, passar [tutorial de transformação de dados](data-factory-build-your-first-pipeline.md) e/ou [tutorial de movimento de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) iria ajudar a compreender melhor neste artigo.  

## <a name="overview"></a>Descrição geral
Uma fábrica de dados pode ter um ou mais pipelines. Os pipelines são agrupamentos lógicos de atividades que, em conjunto, realizam uma tarefa. Atividades de Olá num pipeline definem ações tooperform nos seus dados. Por exemplo, pode utilizar uma cópia atividade toocopy de dados de um tooan do SQL Server no local Blob Storage do Azure. Em seguida, utilize uma atividade do ramo de registo que executa um script de ramo de registo num dados do Azure HDInsight cluster tooprocess/transformação de dados de saída de tooproduce de armazenamento de BLOBs de Olá. Por fim, utilize uma segunda cópia atividade toocopy Olá saída dados tooan Azure SQL Data Warehouse em cima que intelligence (BI) do negócio soluções de relatório são criadas. 

Uma atividade pode ter zero ou mais [conjuntos de dados](data-factory-create-datasets.md) de entrada e produzir um ou mais [conjuntos de dados](data-factory-create-datasets.md) de saída. Olá seguinte diagrama mostra Olá relação entre pipeline, a atividade e o conjunto de dados no Data Factory: 

![Relação entre pipeline, a atividade e o conjunto de dados](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

Um pipeline permite-lhe toomanage atividades como um conjunto em vez de cada um deles individualmente. Por exemplo, pode implementar, agendar, suspender e retomar um pipeline, em vez de lidar com atividades no pipeline de Olá independentemente.

O Data Factory suporta dois tipos de atividades -- atividades de movimento de dados e atividades de transformação de dados. Cada atividade pode ter entrada de zero ou mais [conjuntos de dados](data-factory-create-datasets.md) e produzir uma ou mais conjuntos de dados de saída.

Entrada Olá para uma atividade no pipeline de Olá de representa um conjunto de dados de entrada e saída Olá para a atividade de Olá de representa um conjunto de dados de saída. Os conjuntos de dados identificam dados dentro de diferentes arquivos de dados, como tabelas, ficheiros, pastas e documentos. Depois de criar um conjunto de dados, pode utilizá-lo com atividades num pipeline. Por exemplo, um conjunto de dados pode ser um conjunto de dados de entrada/saída de uma atividade Cópia ou de uma atividade HDInsightHive. Para obter mais informações sobre os conjuntos de dados, veja o artigo [Datasets in Azure Data Factory](data-factory-create-datasets.md) (Conjuntos de Dados no Azure Data Factory).

### <a name="data-movement-activities"></a>Atividades de movimento de dados
Atividade de cópia numa fábrica de dados copia dados a partir de um arquivo de dados de origem dados arquivo tooa sink. Fábrica de dados suporta Olá seguir arquivos de dados. Dados a partir de qualquer origem podem ser escritos tooany sink. Clique num toolearn de arquivo de dados como toocopy dados tooand desse arquivo.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Armazena os dados com * pode estar no local ou no IaaS do Azure e necessitam que tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) numa máquina no local/Azure IaaS.

Para obter mais informações, veja o artigo [Data Movement Activities (Atividades de Movimento de Dados)](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Atividades de transformação de dados
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Para obter mais informações, veja o artigo [Data Transformation Activities (Atividades de Transformação de Dados)](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Atividades .NET personalizadas 
Se precisa de dados de toomove para/de dados de arquivo Olá atividade de cópia não suportar, ou transformar dados utilizando a sua própria lógica, crie um **atividade personalizada do .NET**. Para obter detalhes sobre criar e utilizar uma atividade personalizada, veja [Use custom activities in an Azure Data Factory pipeline (Utilizar atividades personalizadas num pipeline do Azure Data Factory)](data-factory-use-custom-activities.md).

## <a name="schedule-pipelines"></a>Pipelines de agenda
Um pipeline está ativo apenas entre o **iniciar** tempo e **final** tempo. Não foi executada antes da hora de início de Olá ou depois da hora de fim de Olá. Se o pipeline de Olá está em pausa, não ser executada independentemente da respetiva hora de início e de fim. Para toorun um pipeline, que deve não ser pausado. Consulte [agendamento e execução](data-factory-scheduling-and-execution.md) toounderstand como funciona o agendamento e execução no Azure Data Factory.

## <a name="pipeline-json"></a>JSON dos pipelines
Vamos ver mais de perto a definição dos pipelines no formato JSON. estrutura genérica de Olá para um pipeline de procura da seguinte forma:

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| Etiqueta | Descrição | Necessário |
| --- | --- | --- |
| nome |Nome do pipeline de Olá. Especifique um nome que representa a ação de Olá Olá pipeline efetua. <br/><ul><li>Número máximo de carateres: 260</li><li>Tem de começar com uma letra, um número ou um caráter de sublinhado (_)</li><li>Os seguintes carateres não são permitidos: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Sim |
| descrição | Especifique o texto de Olá que descrevem o pipeline de Olá é utilizado para. |Sim |
| atividades | Olá **atividades** secção pode ter um ou mais atividades definidas dentro do mesmo. Consulte a secção seguinte do Olá para obter detalhes sobre o elemento JSON Olá atividades. | Sim |  
| start | Data-hora de início do pipeline de Olá. Tem de constar [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: `2016-10-14T16:32:41Z`. <br/><br/>É possível toospecify uma hora local, por exemplo um período de tempo EST. Eis um exemplo: `2016-02-27T06:00:00-05:00`", que é 6 AM EST.<br/><br/>Olá propriedades de início e de fim em conjunto especifique período ativo do pipeline de Olá. Setores de saída só são produzidos neste período de Active Directory. |Não<br/><br/>Se especificar um valor para a propriedade de fim de Olá, tem de especificar o valor da propriedade de início de Olá.<br/><br/>Olá tempos de início e de fim podem ambos ser vazio toocreate um pipeline. Tem de especificar ambos os valores tooset um período ativo de Olá pipeline toorun. Se não especificar os tempos de início e de fim quando criar um pipeline, pode configurá-los através do cmdlet Olá AzureRmDataFactoryPipelineActivePeriod conjunto mais tarde. |
| Fim | Data-hora de fim do pipeline de Olá. Se for especificado tem de estar no formato ISO. Por exemplo: `2016-10-14T17:32:41Z` <br/><br/>É possível toospecify uma hora local, por exemplo um período de tempo EST. Eis um exemplo: `2016-02-27T06:00:00-05:00`, que é 6 AM EST.<br/><br/>pipeline de Olá toorun especificar indefinidamente, 9999-09-09 como valor de Olá para a propriedade de fim de Olá. <br/><br/> Um pipeline está ativo apenas entre a hora de início e a hora de fim. Não foi executada antes da hora de início de Olá ou depois da hora de fim de Olá. Se o pipeline de Olá está em pausa, não ser executada independentemente da respetiva hora de início e de fim. Para toorun um pipeline, que deve não ser pausado. Consulte [agendamento e execução](data-factory-scheduling-and-execution.md) toounderstand como funciona o agendamento e execução no Azure Data Factory. |Não <br/><br/>Se especificar um valor para a propriedade de início de Olá, tem de especificar o valor da propriedade de fim de Olá.<br/><br/>Consulte as notas para Olá **iniciar** propriedade. |
| isPaused | Se o conjunto tootrue, pipeline Olá não é executado. Que tem no Olá pausado estado. Valor predefinido = false. Pode utilizar esta propriedade tooenable ou desativar um pipeline. |Não |
| pipelineMode | método de Olá para agendar a execução do pipeline de Olá. Valores permitidos são: agendada (predefinição), onetime.<br/><br/>'Agendada' indica que nesse pipeline Olá é executada num período ativo de tooits (hora de início e fim) de acordo com um intervalo de tempo especificado. 'Onetime' indica que nesse pipeline Olá é executada apenas uma vez. Pipelines onetime depois de criado não podem ser modificado/atualizar atualmente. Consulte [Onetime pipeline](#onetime-pipeline) para obter detalhes sobre a definição onetime. |Não |
| expirationTime | Duração de tempo, após a criação, para que Olá [pipeline Monouso](#onetime-pipeline) é válido e deve permanecer aprovisionado. Se não tem nenhum Active Directory, falha, ou pendentes é executado, o pipeline de Olá é automaticamente uma vez eliminada atingir a hora de expiração Olá. valor predefinido de Olá:`"expirationTime": "3.00:00:00"`|Não |
| Conjuntos de dados |Lista de toobe de conjuntos de dados utilizado por atividades definidas no pipeline de Olá. Esta propriedade pode ser utilizado toodefine conjuntos de dados que são específicas toothis pipeline e não definido no factory de dados de Olá. Conjuntos de dados definidos no âmbito deste pipeline só podem ser utilizados por este pipeline e não podem ser partilhados. Consulte [âmbito conjuntos de dados](data-factory-create-datasets.md#scoped-datasets) para obter mais detalhes. |Não |

## <a name="activity-json"></a>JSON da Atividade
Olá **atividades** secção pode ter um ou mais atividades definidas dentro do mesmo. Cada atividade tem Olá seguir a estrutura de nível superior:

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    },
    "scheduler":
    {
    }
}
```

A tabela seguinte descreve as propriedades na atividade de Olá definição JSON:

| Etiqueta | Descrição | Necessário |
| --- | --- | --- |
| nome | Nome da atividade de Olá. Especifique um nome que representa Olá ação que executa a atividade de Olá. <br/><ul><li>Número máximo de carateres: 260</li><li>Tem de começar com uma letra, um número ou um caráter de sublinhado (_)</li><li>Os seguintes carateres não são permitidos: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</li></ul> |Sim |
| descrição | Texto que descreve o que é utilizado para ou Olá atividade |Sim |
| tipo | Tipo de atividade de Olá. Consulte Olá [atividades de movimentos de dados](#data-movement-activities) e [atividades de transformação de dados](#data-transformation-activities) secções para diferentes tipos de atividades. |Sim |
| Entradas |Tabelas de entrada utilizadas pela atividade Olá<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Sim |
| saídas |Tabelas de saída utilizadas pela atividade Olá.<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |Sim |
| linkedServiceName |Nome do serviço de Olá ligado utilizado pela atividade Olá. <br/><br/>Uma atividade pode exigir que especificou o serviço de Olá ligado que liga o ambiente de computação necessária toohello. |Sim para a atividade do HDInsight e do Azure Machine Learning atividade de classificação de lote <br/><br/>Não para todas as outras. |
| typeProperties |As propriedades no Olá **typeProperties** secção dependem do tipo de atividade de Olá. Propriedades do tipo toosee para uma atividade, clique em atividade de toohello ligações na secção anterior Olá. | Não |
| política |Políticas que afetam o comportamento de tempo de execução de Olá da atividade de Olá. Se não for especificado, políticas predefinidas são utilizadas. |Não |
| Programador | propriedade de "Programador" é utilizado toodefine pretendido de agendamento para a atividade de Olá. Os subproperties são Olá igual ao hello aqueles no Olá [propriedade de disponibilidade de um conjunto de dados](data-factory-create-datasets.md#dataset-availability). |Não |


### <a name="policies"></a>Políticas
As políticas afetam o comportamento de tempo de execução de Olá de uma atividade, especificamente quando o setor de Olá de uma tabela é processado. Olá, a tabela seguinte fornece detalhes de Olá.

| Propriedade | Valores permitidos | Valor predefinido | Descrição |
| --- | --- | --- | --- |
| Simultaneidade |Número inteiro <br/><br/>O valor máximo: 10 |1 |Número de execuções simultâneas da atividade de Olá.<br/><br/>Determina número de Olá de execuções de actividade paralela que pode acontecer em diferentes setores. Por exemplo, se precisar de uma atividade toogo através de um grande conjunto de dados disponíveis, que tenham um valor de concorrência maior acelera Olá o processamento de dados. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Determina a ordenação Olá de setores de dados que estão a ser processados.<br/><br/>Por exemplo, se tiver setores de 2 (uma acontecer em 4 pm e outra nas 17: 00) e ambos são pendentes execução. Se definir Olá executionPriorityOrder toobe NewestFirst, setor Olá nas 17: 00 é processada primeiro. Da mesma forma que defina Olá executionPriorityORder toobe OldestFIrst, em seguida, Olá setor em 4 PM está processado. |
| retry |Número inteiro<br/><br/>O valor máximo possível 10 |0 |Número de tentativas antes do processamento de dados de Olá setor de Olá está marcado como falha. Execução da atividade para um setor de dados é repetida segurança toohello especificado contagem de tentativas. repetição de Olá é feita logo que possível após falha de Olá. |
| tempo limite |TimeSpan |00:00:00 |Tempo limite para a atividade de Olá de mensagens em fila. Exemplo: 00:10:00 (indica o tempo limite de 10 minutos)<br/><br/>Se um valor não for especificado ou for 0, o tempo limite de Olá é infinita.<br/><br/>Se o tempo de processamento de dados de Olá num setor excede o valor de tempo limite de Olá, foi cancelada e sistema Olá tentativas de processamento de Olá tooretry. número de Olá de tentativas depende da propriedade de repetição de Olá. Quando ocorre a tempo limite, o estado de Olá está definido tooTimedOut. |
| Atraso |TimeSpan |00:00:00 |Especificar o atraso de Olá antes do processamento de dados de Olá setor começa.<br/><br/>execução de Olá da atividade para um setor de dados é iniciada depois de Olá atraso é passado Olá esperado tempo de execução.<br/><br/>Exemplo: 00:10:00 (implica atraso de 10 minutos) |
| longRetry |Número inteiro<br/><br/>O valor máximo: 10 |1 |Olá de repetições longa tentativas de falha de execução de setor de Olá.<br/><br/>tentativas de longRetry são espaçamento por longRetryInterval. Por isso, se precisar de toospecify um período de tempo entre as tentativas de repetição, utilize o longRetry. Se repetir e o longRetry forem especificados, cada tentativa de longRetry incluir as tentativas de repetição e número máximo de Olá de tentativas de repetição * longRetry.<br/><br/>Por exemplo, se tivermos Olá definições na política de atividade Olá os seguintes:<br/>Repita: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Partem do princípio de houver apenas um setor tooexecute (estado está a aguardar a) e a execução da atividade Olá falha sempre. Inicialmente seria possível 3 tentativas de execução consecutivos. Após cada tentativa, estado do setor Olá seria repetição. Após o primeiro 3 tentativas são, o estado do setor Olá seria LongRetry.<br/><br/>Depois de uma hora (ou seja, o valor do longRetryInteval), seria possível outro conjunto de 3 tentativas de execução consecutivos. Depois disso, estado do setor Olá seria possível falhou e não iriam ser tentadas nenhuma mais tentativas. Por conseguinte, global 6 foram efetuadas tentativas.<br/><br/>Se qualquer execução for bem sucedida, estado do setor Olá seria preparado e não existem mais tentativas estão tentadas.<br/><br/>longRetry pode ser utilizada em situações onde dados dependentes chega vezes não determinística ou hello ambiente geral flaky em que o processamento de dados ocorre. Nestes casos, não pode ajudar a fazer várias tentativas umas a seguir e se o fizer, depois de um intervalo de tempo de resultados de na Olá pretendido saída.<br/><br/>Palavra de advertência: não definir valores elevados para longRetry ou longRetryInterval. Normalmente, os valores superiores implica outros problemas systemic. |
| longRetryInterval |TimeSpan |00:00:00 |atraso de Olá entre as tentativas de repetição longo |

## <a name="sample-copy-pipeline"></a>Pipeline de cópia de exemplo
No seguinte exemplo de pipeline de Olá, é uma atividade do tipo **cópia** no Olá **atividades** secção. Neste exemplo Olá [atividade de cópia](data-factory-data-movement-activities.md) copia dados a partir de uma base de dados de SQL do Azure de tooan de armazenamento do BLOBs do Azure. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

Tenha em atenção Olá seguintes pontos:

* Na secção de atividades de Olá, é apenas uma atividade cujo **tipo** estiver definido demasiado**cópia**.
* Entrada atividade Olá está definida demasiado**InputDataset** e a saída atividade Olá estiver definida demasiado**OutputDataset**. Veja o artigo [Conjuntos de dados](data-factory-create-datasets.md) para saber como definir conjuntos de dados em JSON. 
* No Olá **typeProperties** secção, **BlobSource** está especificado como tipo de origem Olá e **SqlSink** está especificado como o tipo de sink Olá. No Olá [atividades de movimentos de dados](#data-movement-activities) secção, clique em Olá que pretende toouse como uma origem ou uma toolearn sink mais sobre como mover dados de/para este arquivo de dados do arquivo de dados. 

Para instruções completas de criar este pipeline, consulte [Tutorial: copiar dados do Blob Storage tooSQL da base de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="sample-transformation-pipeline"></a>Pipeline de transformação de exemplos
No seguinte exemplo de pipeline de Olá, é uma atividade do tipo **HDInsightHive** no Olá **atividades** secção. Neste exemplo Olá [atividade do ramo de registo do HDInsight](data-factory-hive-activity.md) transformações de dados a partir de um Blob storage do Azure através da execução de um ficheiro de script de ramo de registo num cluster do Azure HDInsight Hadoop. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

Tenha em atenção Olá seguintes pontos: 

* Na secção de atividades de Olá, é apenas uma atividade cujo **tipo** estiver definido demasiado**HDInsightHive**.
* ficheiro de script de ramo de registo de Olá **partitionweblogs.hql**, é armazenada no Olá conta do storage do Azure (especificado pelo scriptLinkedService Olá, denominado **AzureStorageLinkedService**) e, em  **script** pasta no contentor de Olá **adfgetstarted**.
* Olá `defines` secção é utilizado toospecify Olá runtime as definições que são transmitidas toohello script de ramo de registo como valores de configuração do ramo de registo (por exemplo `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

Olá **typeProperties** secção é diferente para cada atividade de transformação. toolearn sobre as propriedades de tipo suportado para uma atividade de transformação, clique em atividades de transformação de Olá no Olá [atividades de transformação de dados](#data-transformation-activities) tabela. 

Para instruções completas de criar este pipeline, consulte [Tutorial: criar primeiro pipeline tooprocess dados utilizando o cluster de Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="multiple-activities-in-a-pipeline"></a>Múltiplas atividades num pipeline
pipelines de dois exemplos anteriores Olá tem apenas uma atividade. Pode ter mais de uma atividade num pipeline.  

Se tiver várias atividades num pipeline e saída de uma atividade não é uma entrada de outra atividade, atividades Olá poderão ser executadas em paralelo se setores de dados de entrada para atividades Olá estão prontos. 

Pode encadeiam duas atividades, fazendo com que o conjunto de dados de saída de Olá de uma atividade como conjunto de dados de entrada Olá de Olá outra atividade. atividade segundo Olá executa apenas ao hello primeiro um for concluída com êxito.

![Encadeamento de atividades no Olá mesmo pipeline](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

Neste exemplo, o pipeline de Olá com duas atividades: Activity1 e Activity2. Olá Activity1 demora Dataset1 como entrada e produz uma saída Dataset2. Olá atividade demora Dataset2 como entrada e produz uma saída Dataset3. Dado que o resultado Olá Activity1 (Dataset2) seja a entrada de Olá de Activity2, Olá Activity2 é executado apenas após Olá atividade seja concluída com êxito e produz Olá Dataset2 setor. Se Olá Activity1 falha por alguma razão e não produz o setor de Olá Dataset2, Olá atividade 2 não é executado para esse setor (por exemplo: 9 AM too10 ESTOU). 

Também pode encadeiam atividades que estão em diferentes pipelines.

![Encadeamento de atividades em duas pipelines](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

Neste exemplo, Pipeline1 tem apenas uma atividade que demora Dataset1 como entrada e produz Dataset2 como resultado. Olá Pipeline2 também tem apenas uma atividade que aceita Dataset2 como uma entrada e Dataset3 como resultado. 

Para obter mais informações, consulte [agendamento e execução](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="create-and-monitor-pipelines"></a>Criar e monitorizar pipelines
Pode criar pipelines utilizando um destas ferramentas ou SDKs. 

- Assistente para copiar. 
- Portal do Azure
- Visual Studio
- Azure PowerShell
- Modelo Azure Resource Manager
- API REST
- API .NET

Consulte Olá seguintes tutoriais para obter instruções passo a passo para criar pipelines utilizando um destas ferramentas ou SDKs.
 
- [Build a pipeline with a data transformation activity](data-factory-build-your-first-pipeline.md) (Criar um pipeline cum uma atividade de transformação de dados)
- [Criar um pipeline com uma atividade de movimento de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

Depois de um pipeline criado/implementada, pode gerir e monitorizar os pipelines utilizando Olá os painéis do portal do Azure ou monitorizar e gerir aplicações. Consulte Olá os seguintes tópicos para obter instruções passo a passo. 

- [Monitorizar e gerir pipelines com os painéis do portal do Azure](data-factory-monitor-manage-pipelines.md).
- [Monitorizar e gerir pipelines com a monitorizar e gerir aplicações](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a>Onetime pipeline
Pode criar e agendar uma toorun pipeline periodicamente (por exemplo: hora a hora ou diariamente) dentro de Olá início e de fim que especifica na definição do pipeline de Olá. Consulte [agendamento atividades](#scheduling-and-execution) para obter mais detalhes. Também pode criar um pipeline que é executada apenas uma vez. toodo por isso, definir Olá **pipelineMode** propriedade no Olá pipeline definição demasiado**onetime** conforme mostrado no Olá amostra JSON a seguir. valor predefinido de Olá para esta propriedade é **agendada**.

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

Tenha em atenção o seguinte Olá:

* **Iniciar** e **final** vezes para o pipeline de Olá não foram especificados.
* **Disponibilidade** especificado conjuntos de dados de entrada e saída (**frequência** e **intervalo**), apesar de fábrica de dados não utiliza valores de Olá.  
* Vista de diagrama mostra pipelines única. Este comportamento é propositado.
* Não não possível atualizar o uso pipelines. Pode clonar um único pipeline, mude o nome, atualizar propriedades e implementá-la toocreate outro.


## <a name="next-steps"></a>Passos Seguintes
- Para mais informações sobre conjuntos de dados, consulte [criar conjuntos de dados](data-factory-create-datasets.md) artigo. 
- Para obter mais informações sobre como pipelines são agendadas e executadas, consulte [agendamento e execução no Azure Data Factory](data-factory-scheduling-and-execution.md) artigo. 
  

