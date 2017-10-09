---
title: "aaaBuild a primeira fábrica de dados (REST) | Microsoft Docs"
description: Neste tutorial, vai criar um exemplo de pipeline do Azure Data Factory com a API REST do Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Tutorial: Criar a primeira fábrica de dados do Azure com a API REST do Data Factory
> [!div class="op_single_selector"]
> * [Descrição geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


Neste artigo, utilize toocreate de API de REST de fábrica de dados a primeira fábrica de dados do Azure. toodo Olá tutorial, utilizando outras ferramentas/SDKs, selecione uma das opções de Olá Olá na lista pendente.

pipeline de Olá neste tutorial tem uma atividade: **atividade do ramo de registo do HDInsight**. Esta atividade executa um script de ramo de registo num cluster do Azure HDInsight transformações dados de saída de tooproduce de dados de entrada. pipeline de Olá é agendada toorun depois de um mês entre Olá especificado tempos de início e de fim.

> [!NOTE]
> Este artigo não abrange todos os Olá REST API. Para obter a documentação completa sobre a API REST, veja [Data Factory REST API Reference](/rest/api/datafactory/) (Referência da API REST do Data Factory).
> 
> Um pipeline pode ter mais de uma atividade. Além disso, pode encadeiam duas atividades (executadas uma atividade após outro) definindo o conjunto de dados de saída de Olá de uma atividade como Olá de entrada de conjunto de dados de Olá outra atividade. Para obter mais informações, veja [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) (agendamento e execução no Data Factory).


## <a name="prerequisites"></a>Pré-requisitos
* Leia [descrição geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e Olá concluída **pré-requisito** passos.
* Instale o [Curl](https://curl.haxx.se/dlwiz/) no seu computador. É utilizar a ferramenta CURL Olá com REST comandos toocreate uma fábrica de dados.
* Siga as instruções [neste artigo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para:
  1. Criar uma aplicação Web com o nome **ADFGetStartedApp** no Azure Active Directory.
  2. Obter o **ID de cliente** e a **chave secreta**.
  3. Obter o **ID de inquilino**.
  4. Atribuir Olá **ADFGetStartedApp** aplicação toohello **contribuinte da fábrica de dados** função.
* Instale o [Azure PowerShell](/powershell/azure/overview).
* Iniciar **PowerShell** e Olá execute os seguintes comandos. Mantenha o Azure PowerShell aberto até Olá fim deste tutorial. Se fechar e reabrir, terá de comandos de Olá toorun novamente.
  1. Executar **Login-AzureRmAccount** e introduza o nome de utilizador de Olá e a palavra-passe que utilizam toosign no toohello portal do Azure.
  2. Executar **Get-AzureRmSubscription** tooview Olá todas as subscrições para esta conta.
  3. Executar **Get-AzureRmSubscription - SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** subscrição de Olá tooselect que pretende que sejam toowork com. Substitua **NameOfAzureSubscription** com o nome de Olá da sua subscrição do Azure.
* Criar um grupo de recursos do Azure com o nome **ADFTutorialResourceGroup** executando Olá seguinte comando na Olá do PowerShell:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   Alguns dos passos de Olá neste tutorial partem do princípio de que utiliza o grupo de recursos de Olá com o nome ADFTutorialResourceGroup. Se utilizar um grupo de recursos diferente, terá de nome de Olá toouse do seu grupo de recursos em vez de ADFTutorialResourceGroup neste tutorial.

## <a name="create-json-definitions"></a>Criar definições JSON
Crie os seguintes ficheiros JSON na pasta de olá onde curl.exe está localizado.

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Nome deve ser globalmente exclusivo, pelo que poderá ser útil tooprefix/sufixo ADFCopyTutorialDF toomake-um nome exclusivo.
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Substitua **accountname** e **accountkey** pelo nome e chave da sua conta de armazenamento do Azure. toolearn como tooget o armazenamento de acesso da chave, consulte Olá obter informações sobre como tooview, copiar e voltar a gerar armazenamento aceder às chaves na [gerir a sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

Olá tabela que se segue fornece descrições para as propriedades JSON de Olá utilizadas no fragmento de Olá:

| Propriedade | Descrição |
|:--- |:--- |
| ClusterSize |Tamanho do cluster do HDInsight Olá. |
| TimeToLive |Especifica esse tempo de inatividade Olá para o cluster do HDInsight Olá, antes de ser eliminado. |
| linkedServiceName |Especifica a conta de armazenamento Olá, que é utilizado toostore os registos de Olá que são gerados pelo HDInsight |

Tenha em atenção Olá seguintes pontos:

* Olá Data Factory cria um **baseado em Linux** cluster do HDInsight com Olá acima JSON. Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
* Também pode utilizar o **seu próprio cluster do HDInsight** em vez de utilizar um cluster do HDInsight a pedido. Veja [HDInsight Linked Service (Serviço Ligado do HDInsight)](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.
* cluster do HDInsight Olá cria um **contentor predefinido** no armazenamento de BLOBs de Olá especificado na Olá JSON (**linkedServiceName**). HDInsight não é eliminado deste contentor quando cluster Olá é eliminado. Este comportamento é propositado. Com o serviço de ligado de HDInsight a pedido, é criado um cluster de HDInsight sempre que um setor é processado, exceto se houver um cluster existente em direto (**timeToLive**) e é eliminado quando o processamento de Olá terminar.

    À medida que são processados mais setores, verá muitos contentores no armazenamento de blobs do Azure. Se não precisar deles para resolução de problemas de tarefas Olá, poderá ser útil toodelete-los armazenamento de Olá tooreduce custo. os nomes de Olá destes contentores seguem um padrão: "adf**nomedafábricadedados**-**linkedservicename**- datetimestamp". Utilize ferramentas como [Explorador de armazenamento do Microsoft](http://storageexplorer.com/) toodelete contentores no seu Azure armazenamento de Blobs.

Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

Olá JSON define um conjunto de dados com o nome **AzureBlobInput**, que representa dados de entrada para uma atividade no pipeline de Olá. Além disso, especifica que os dados de entrada de Olá estão localizados no contentor de blob Olá denominado **adfgetstarted** e pasta Olá **inputdata**.

Olá tabela que se segue fornece descrições para as propriedades JSON de Olá utilizadas no fragmento de Olá:

| Propriedade | Descrição |
|:--- |:--- |
| tipo |propriedade de tipo de Olá está definida tooAzureBlob porque os dados que residem no armazenamento de Blobs do Azure. |
| linkedServiceName |refere-se toohello StorageLinkedService que criou anteriormente. |
| fileName |Esta propriedade é opcional. Se omitir esta propriedade, serão escolhidos todos os ficheiros de Olá de Olá folderPath. Neste caso, apenas Olá input.log é processado. |
| tipo |ficheiros de registo de Olá estão no formato de texto, pelo que iremos utilizar TextFormat. |
| columnDelimiter |colunas nos ficheiros de registo Olá são delimitadas por vírgula () |
| frequência/intervalo |a frequência definida tooMonth e o intervalo é 1, o que significa que os setores de entrada Olá estão disponíveis mensalmente. |
| externo |Esta propriedade é definida tootrue se os dados de entrada de Olá não forem gerados pelo serviço do Data Factory Olá. |

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

Olá JSON define um conjunto de dados com o nome **AzureBlobOutput**, que representa dados de saída para uma atividade no pipeline de Olá. Além disso, especifica que os resultados de Olá são armazenados no contentor de blob Olá denominado **adfgetstarted** e pasta Olá **partitioneddata**. Olá **disponibilidade** secção especifica o conjunto de dados de saída que Olá é produzido mensalmente.

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> Substitua **storageaccountname** pelo nome da sua conta de armazenamento do Azure.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

No fragmento JSON de Olá, está a criar um pipeline que consiste numa única atividade que utiliza o ramo de registo tooprocess dados num cluster do HDInsight.

ficheiro de script de ramo de registo de Olá **partitionweblogs.hql**, é armazenada no Olá conta do storage do Azure (especificado pelo scriptLinkedService Olá, denominado **StorageLinkedService**) e, em **script**  pasta no contentor de Olá **adfgetstarted**.

Olá **define** secção especifica as definições de tempo de execução que são transmitidas toohello script de ramo de registo como valores de configuração do ramo de registo (por exemplo ${hiveconf: inputtable}, ${hiveconf}).

Olá **iniciar** e **final** propriedades de pipeline de Olá Especifica o período ativo de Olá de pipeline de Olá.

No JSON de atividade de Olá, especifique esse Olá script de ramo de registo é executado na computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.

> [!NOTE]
> Consulte "JSON do Pipeline" em [Pipelines e atividades no Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON utilizadas no Olá anterior exemplo.
>
>

## <a name="set-global-variables"></a>Definir variáveis globais
No Azure PowerShell, execute Olá depois de substituir os valores de Olá com os seus próprios os seguintes comandos:

> [!IMPORTANT]
> Consulte a secção [Pré-requisitos](#prerequisites) para instruções sobre como obter o ID de cliente, o segredo do cliente, o ID de inquilino e o ID da subscrição.
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>Autenticar com o AAD

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Criar fábrica de dados
Neste passo, irá criar uma fábrica de dados do Azure com o nome **FirstDataFactoryREST**. Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline pode conter uma atividade ou mais. Por exemplo, um atividade de cópia toocopy dados de um arquivo de dados de destino de tooa de origem e um toorun de atividade do ramo de registo do HDInsight tootransform dados de script de ramo de registo. Execute Olá fábrica de dados do comandos toocreate Olá os seguintes:

1. Atribuir Olá comando toovariable denominado **cmd**.

    Confirme que o nome da fábrica de dados de Olá que especificar aqui (ADFCopyTutorialDF) correspondências Olá nome especificado no Olá Olá **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Execute o comando de Olá utilizando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver os resultados de Olá. Se Olá a fábrica de dados foi criada com êxito, verá Olá JSON Olá fábrica de dados no Olá **resultados**; caso contrário, verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

Tenha em atenção Olá seguintes pontos:

* nome de Olá de Olá do Azure Data Factory deve ser globalmente exclusivo. Se vir Olá erro nos resultados: **nome da fábrica de dados "FirstDataFactoryREST" não está disponível**, Olá os seguintes passos:
  1. O nome de Olá alteração (por exemplo, yournameFirstDataFactoryREST) no Olá **datafactory.json** ficheiro. Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.
  2. No comando primeiro olá onde Olá **$cmd** variável é atribuída um valor, substitua o novo nome de Olá FirstDataFactoryREST e execute o comando de Olá.
  3. Execute Olá dois comandos tooinvoke Olá REST API toocreate Olá data factory e de impressão Olá resultados da operação de Olá.
* instâncias do Data Factory toocreate, terá de toobe um Contribuidor/administrador da Olá subscrição do Azure
* nome de Olá da fábrica de dados de Olá pode ser registado como um nome DNS no futuro Olá e, por conseguinte, ficar publicamente visível.
* Se receber o erro de Olá: "**esta subscrição não está registado toouse espaço de nomes Microsoft. DataFactory**", efetue um dos seguintes Olá e tente publicar novamente:

  * No Azure PowerShell, execute Olá fornecedor do Data Factory comando tooregister Olá os seguintes:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      Pode executar Olá tooconfirm de comando a seguir que Olá é registado o fornecedor do Data Factory:
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Utilizar o início de sessão Olá a subscrição do Azure no Olá [portal do Azure](https://portal.azure.com) e navegue até o painel do Data Factory tooa (ou) crie uma fábrica de dados no Olá portal do Azure. Esta ação regista automaticamente o fornecedor de Olá por si.

Antes de criar um pipeline, terá de toocreate algumas entidades do Data Factory primeiro. Primeiro criar serviços ligados toolink dados arquivos/computações tooyour armazenar, definir a entrada e saída de dados de toorepresent de conjuntos de dados nos arquivos de dados ligados.

## <a name="create-linked-services"></a>Criar serviços ligados
Neste passo, pode liga a sua conta do Storage do Azure e uma fábrica de dados a pedido do Azure HDInsight cluster tooyour. Olá contém Olá dados de entrada e de saída do pipeline de Olá neste exemplo de conta de armazenamento do Azure. Olá serviço ligado do HDInsight é toorun utilizado um script de ramo de registo especificado na atividade de Olá de pipeline de Olá neste exemplo.

### <a name="create-azure-storage-linked-service"></a>Criar o serviço ligado do Storage do Azure
Neste passo, ligar a fábrica de dados de tooyour de conta do Storage do Azure. Com este tutorial utiliza Olá mesma conta de armazenamento do Azure ficheiro de script de dados de entrada/saída toostore e Olá HQL.

1. Atribuir Olá comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Execute o comando de Olá utilizando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver os resultados de Olá. Se ligado Olá o serviço foi criado com êxito, verá Olá JSON para o serviço de Olá ligado no Olá **resultados**; caso contrário, verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Criar o serviço ligado do Azure HDInsight
Neste passo, pode liga a uma fábrica de dados a pedido HDInsight cluster tooyour. cluster do HDInsight Olá é automaticamente criada no tempo de execução e eliminado depois de ter é processado e ficado inativo para o período de tempo especificado Olá. Também pode utilizar o seu próprio cluster do HDInsight em vez de utilizar um cluster do HDInsight a pedido. Veja [Compute Linked Services (Serviços Ligados de Computação)](data-factory-compute-linked-services.md) para obter detalhes.

1. Atribuir Olá comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. Execute o comando de Olá utilizando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver os resultados de Olá. Se ligado Olá o serviço foi criado com êxito, verá Olá JSON para o serviço de Olá ligado no Olá **resultados**; caso contrário, verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Criar conjuntos de dados
Neste passo, poderá criar conjuntos de dados toorepresent Olá entrada e saída dados para o processamento do ramo de registo. Estes conjuntos de dados Consulte toohello **StorageLinkedService** que criou anteriormente neste tutorial. Olá tooan de pontos de serviço ligado conta de armazenamento do Azure e os conjuntos de dados especificam um contentor, pasta, nome de ficheiro no armazenamento de Olá que contém a entrada e saída de dados.

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
Neste passo, vai criar Olá conjunto de dados de entrada toorepresent entrada dados armazenados no Olá Blob storage do Azure.

1. Atribuir Olá comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Execute o comando de Olá utilizando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver os resultados de Olá. Se Olá conjunto de dados foi criado com êxito, verá Olá JSON para Olá conjunto de dados Olá **resultados**; caso contrário, verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Neste passo, crie as dados de saída conjunto de dados de saída do Olá toorepresent armazenados no Olá Blob storage do Azure.

1. Atribuir Olá comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. Execute o comando de Olá utilizando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver os resultados de Olá. Se Olá conjunto de dados foi criado com êxito, verá Olá JSON para Olá conjunto de dados Olá **resultados**; caso contrário, verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a>Criar pipeline
Neste passo, irá criar o seu primeiro pipeline com uma atividade **HDInsightHive**. Setor de entrada está disponível mensalmente (frequência: mês, intervalo: 1), o setor de saída é produzido mensalmente e propriedade do agendador Olá atividade Olá seja também definida toomonthly. Olá as definições de conjunto de dados de saída de Olá e agendador de atividade Olá têm de corresponder. Atualmente, o conjunto de dados de saída é que unidades Olá agenda, pelo que deve criar um conjunto de dados de saída, mesmo se Olá atividade não produzir qualquer saída. Se a atividade de Olá não incluir entradas, pode ignorar o conjunto de dados de entrada Olá criar.

Confirme que vê Olá **input.log** ficheiro Olá **adfgetstarted/inputdata** pasta Olá blob storage do Azure e execute Olá pipeline de Olá toodeploy de comando a seguir. Desde Olá **iniciar** e **final** são definidas no passado Olá e **isPaused** é conjunto toofalse, pipeline Olá executa (atividade no pipeline de Olá) imediatamente depois da implementação.

1. Atribuir Olá comando toovariable denominado **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Execute o comando de Olá utilizando **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Ver os resultados de Olá. Se Olá conjunto de dados foi criado com êxito, verá Olá JSON para Olá conjunto de dados Olá **resultados**; caso contrário, verá uma mensagem de erro.

    ```PowerShell
    Write-Host $results
    ```
4. Parabéns, criou com êxito o seu primeiro pipeline com o Azure PowerShell!

## <a name="monitor-pipeline"></a>Monitorizar o pipeline
Neste passo, utiliza o setores de toomonitor de API de REST de fábrica de dados que está a ser produzidos pelo pipeline Olá.

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> A criação de um cluster do HDInsight a pedido demora, por norma, algum tempo (cerca de 20 minutos). Por conseguinte, esperar Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá setor.
>
>

Executar Olá Invoke-Command e Olá seguinte até verá o setor de Olá no **pronto** Estado ou **falha** estado. Quando o setor Olá está no estado pronto, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contentor de armazenamento de BLOBs para Olá.  criação de Olá de um cluster do HDInsight a pedido demora, normalmente, algum tempo.

![dados de saída](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> ficheiro de entrada Olá é eliminado quando o setor de Olá é processado com êxito. Por conseguinte, se pretender setor de Olá toorerun ou Olá novamente o tutorial, carregue Olá ficheiro de entrada (input.log) toohello na pasta inputdata do contentor adfgetstarted de Olá.
>
>

Também pode utilizar os setores de toomonitor portal do Azure e resolva quaisquer problemas. Consulte os detalhes em [Monitorizar pipelines com o portal do Azure](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).

## <a name="summary"></a>Resumo
Neste tutorial, criou um dados de tooprocess da fábrica de dados do Azure executando o script de ramo de registo num cluster de hadoop do HDInsight. Utilizou Olá Editor do Data Factory no Olá toodo portal do Azure de Olá os seguintes passos:

1. Criou uma **fábrica de dados** do Azure.
2. Criar dois **serviços ligados**:
   1. **Armazenamento do Azure** ligado serviço toolink o armazenamento de Blobs do Azure que contém a fábrica de dados de toohello de ficheiros de entrada/saída.
   2. **O Azure HDInsight** a pedido ligado serviço toolink uma fábrica de dados a pedido do HDInsight Hadoop cluster toohello. O Azure Data Factory cria do HDInsight Hadoop, dados de entrada do cluster just-in-time tooprocess e produzir dados de saída.
3. Criar dois **conjuntos de dados**, que descrevem dados de entrada e de saída para a atividade do ramo de registo do HDInsight no pipeline de Olá.
4. Criar um **pipeline** com uma atividade do **Ramo de Registo do HDInsight**.

## <a name="next-steps"></a>Passos seguintes
Neste artigo, criou um pipeline com uma atividade de transformação (Atividade do HDInsight) que executa um Script de ramo de registo num cluster do Azure HDInsight a pedido. toosee como toouse um toocopy de dados de atividade de cópia de tooAzure um Blob do Azure SQL, consulte [Tutorial: copiar dados de tooAzure um Blob do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Veja Também
| Tópico | Descrição |
|:--- |:--- |
| [Referência da API REST do Data Factory](/rest/api/datafactory/) |Consulte a documentação abrangente sobre os cmdlets do Data Factory |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda-o a compreender os pipelines e atividades no Azure Data Factory e como toouse-los tooconstruct ponto a ponto condicionados por dados fluxos de trabalho para o seu cenário ou empresa. |
| [Conjuntos de dados](data-factory-create-datasets.md) |Este artigo ajuda-o a compreender os conjuntos de dados no Azure Data Factory. |
| [Agendamento e Execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspetos de agendamento e execução de Olá do modelo de aplicação do Azure Data Factory. |
| [Monitorizar e gerir pipelines com a Aplicação de Monitorização](data-factory-monitor-manage-app.md) |Este artigo descreve como toomonitor, gerir e depurar pipelines utilizando Olá de monitorização e gestão de aplicações. |
