---
title: "aaaMove dados da tabela da Web através do Azure Data Factory | Microsoft Docs"
description: "Saiba mais sobre como toomove dados de uma tabela de uma Web página utilizando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Mover dados de uma origem de tabela Web utilizando o Azure Data Factory
Este artigo descreve como toouse Olá atividade de cópia em dados do Azure Data Factory toomove a partir de uma tabela na tooa página Web suportado o arquivo de dados do sink. Este artigo baseia-se Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo que apresenta uma descrição geral do movimento de dados com a lista de atividade e Olá de cópia de arquivos de dados suportados como sinks/origens.

Fábrica de dados suporta atualmente só armazena mover dados a partir de um tooother de dados de tabela da Web, mas não mover dados de outros dados armazena o destino de tabela tooa Web.

> [!IMPORTANT]
> Este conector Web atualmente suporta apenas extrair conteúdo da tabela de uma página HTML. utilizar tooretrieve dados a partir de um ponto final de HTTP/s, [conetor HTTP](data-factory-http-connector.md) em vez disso.

## <a name="getting-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados de um arquivo de dados no local Cassandra utilizando ferramentas diferentes/APIs. 

- Olá toocreate da forma mais fácil um pipeline está toouse Olá **Assistente para copiar**. Consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md) para obter instruções sobre como criar um pipeline com o Assistente de cópia de dados Olá rápida. 
- Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:

1. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. 
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. 

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para um exemplo com definições de JSON para entidades do Data Factory que são utilizados toocopy dados de uma tabela de web, consulte [exemplo JSON: copiar dados da tabela de Web tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) secção deste artigo. 

Olá seguintes secções fornece detalhes sobre as propriedades JSON que estão a tabela de Web do toodefine utilizados Data Factory entidades tooa específico:

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Olá, a tabela seguinte fornece uma descrição do serviço do JSON elementos específicos tooWeb ligado.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| tipo |a propriedade de tipo Olá tem de ser definida: **Web** |Sim |
| Url |Origem do URL toohello Web |Sim |
| authenticationType |Anónimo. |Sim |

### <a name="using-anonymous-authentication"></a>Autenticação anónima

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para uma lista completa das secções & Propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. As secções, tais como a estrutura, a disponibilidade e a política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL do Azure, Azure blob, tabela do Azure, etc.).

Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização de Olá dos dados de Olá no arquivo de dados de Olá. Olá typeProperties secção para o conjunto de dados do tipo **WebTable** tem Olá seguintes propriedades

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| tipo |Tipo de conjunto de dados de Olá. tem de ser definido demasiado**WebTable** |Sim |
| Caminho |Um relativo recurso de toohello do URL, que contém Olá tabela. |Não. Quando o caminho não for especificado, é utilizada apenas Olá URL especificado na definição de serviço Olá ligado. |
| Índice |índice de Olá da tabela de Olá no recurso de Olá. Consulte [Get índice de uma tabela numa página HTML](#get-index-of-a-table-in-an-html-page) secção para o índice de toogetting passos de uma tabela numa página HTML. |Sim |

**Exemplo:**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções & Propriedades disponíveis para definir as atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, tabelas e política estão disponíveis para todos os tipos de atividades.

Enquanto, propriedades disponíveis na secção de typeProperties Olá da atividade de Olá variar de acordo com cada tipo de atividade. Para a atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

Atualmente, quando a origem de Olá na atividade de cópia é do tipo **WebSource**, sem propriedades adicionais são suportadas.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>Exemplo JSON: copiar dados da tabela de Web tooAzure Blob
Olá seguinte exemplo mostra:

1. Um serviço ligado do tipo [Web](#linked-service-properties).
2. Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Uma entrada [dataset](data-factory-create-datasets.md) do tipo [WebTable](#dataset-properties).
4. Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. A [pipeline](data-factory-create-pipelines.md) com atividade de cópia que utiliza [WebSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo de Olá copia dados a partir um tooan de tabela Web BLOBs do Azure a cada hora. Propriedades JSON de Olá utilizadas nestes exemplos são descritas nas secções seguintes exemplos de Olá.

Olá seguinte exemplo mostra como os dados de toocopy de um tooan de tabela de Web do Azure blob. No entanto, é possível copiar dados diretamente tooany de Olá sinks Olá declarado no [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo utilizando Olá atividade de cópia no Azure Data Factory.

**Serviço ligado do Web** este exemplo utiliza Olá Web ligado serviço com a autenticação anónima. Consulte [Web serviço ligado](#linked-service-properties) secção para diferentes tipos de autenticação, pode utilizar.

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

**Serviço ligado do Armazenamento do Azure**

```json
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

**Conjunto de dados de entrada WebTable** definição **externo** demasiado**verdadeiro** informa o serviço do Data Factory Olá esse conjunto de dados de Olá é toohello externo fábrica de dados e não é produzido por uma atividade no Olá fábrica de dados.

> [!NOTE]
> Consulte [Get índice de uma tabela numa página HTML](#get-index-of-a-table-in-an-html-page) secção para o índice de toogetting passos de uma tabela numa página HTML.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Conjunto de dados de saída de Blobs do Azure**

São escritos dados no blob tooa de novo a cada hora (frequência: hora, intervalo: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



**Pipeline com atividade de cópia**

Olá pipeline contém uma atividade de cópia é configurado toouse Olá conjuntos de dados de entrada e de saída e é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá **origem** tipo está definido demasiado**WebSource** e **sink** tipo está definido demasiado**BlobSink**.

Consulte [propriedades do tipo WebSource](#copy-activity-type-properties) para Olá obter lista de propriedades suportadas por Olá WebSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="get-index-of-a-table-in-an-html-page"></a>Obter o índice de uma tabela de uma página HTML
1. Iniciar **Excel 2016** e um comutador toohello **dados** separador.  
2. Clique em **nova consulta** na barra de ferramentas Olá, ponto demasiado**de outras origens** e clique em **da Web**.

    ![Menu de consulta de energia](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. No Olá **da Web** caixa de diálogo, introduza **URL** que pretende utilizar no ligado JSON do serviço (por exemplo: https://en.wikipedia.org/wiki/), juntamente com o caminho tem de especificar Olá conjunto de dados (por exemplo: AFI % 27s_100_Years... 100_Movies) e clique em **OK**.

    ![Caixa de diálogo Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    URL utilizado neste exemplo: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. Se vir **conteúdo acesso Web** caixa de diálogo, o direito de Olá selecione **URL**, **autenticação**e clique em **Connect**.

   ![Aceder à caixa de diálogo de conteúdo Web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. Clique num **tabela** item no conteúdo toosee de vista de árvore do Olá da tabela de Olá e, em seguida, clique em **editar** botão na parte inferior de Olá.  

   ![Caixa de diálogo do navegador](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. No Olá **Editor de consultas** janela, clique em **avançadas Editor** botão na barra de ferramentas Olá.

    ![Botão Avançadas do Editor](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. Na caixa de diálogo Editor avançadas de Olá, Olá número junto demasiado "Origem" é o índice de Olá.

    ![Avançadas Editor - índice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Se estiver a utilizar o Excel 2013, utilize [Microsoft Power Query para Excel](https://www.microsoft.com/download/details.aspx?id=39379) índice de Olá tooget. Consulte [Connect tooa web página](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artigo para obter detalhes. passos de Olá são semelhantes, se estiver a utilizar [Microsoft Power BI para ambiente de trabalho](https://powerbi.microsoft.com/desktop/).

> [!NOTE]
> colunas de toomap toocolumns de conjunto de dados de origem do conjunto de dados dependente, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e a otimização
Consulte [desempenho de atividade de cópia & otimização guia](data-factory-copy-activity-performance.md) toolearn sobre chave factors desse desempenho impacto de movimento de dados (atividade de cópia) no Azure Data Factory e várias formas toooptimize-lo.
