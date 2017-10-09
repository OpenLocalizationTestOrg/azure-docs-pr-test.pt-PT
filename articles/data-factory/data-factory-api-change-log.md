---
title: "aaaData fábrica - registo de alterações de API do .NET | Microsoft Docs"
description: "Descreve as alterações, adições de funcionalidade, correções de erros etc... numa versão específica do .NET API para Olá do Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8208271b-7f4c-4214-b665-d2ff503c4470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: spelluru
ms.openlocfilehash: 1d44b45c3dc8f9d483d1f1cef7068edacc610932
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---net-api-change-log"></a>O Azure Data Factory - registo de alterações de .NET API
Este artigo fornece informações sobre alterações tooAzure SDK de fábrica de dados numa versão específica. Pode encontrar o pacote NuGet mais recente do Olá para o Azure Data Factory [aqui](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories)

## <a name="version-4110"></a>Versão 4.11.0
Funcionalidade adições:

* Olá seguintes tipos de serviço ligado foram adicionados:
  * [OnPremisesMongoDbLinkedService](https://msdn.microsoft.com/library/mt765129.aspx)
  * [AmazonRedshiftLinkedService](https://msdn.microsoft.com/library/mt765121.aspx)
  * [AwsAccessKeyLinkedService](https://msdn.microsoft.com/library/mt765144.aspx)
* Olá tipos de conjunto de dados seguintes foram adicionado:
  * [MongoDbCollectionDataset](https://msdn.microsoft.com/library/mt765145.aspx)
  * [AmazonS3Dataset](https://msdn.microsoft.com/library/mt765112.aspx)
* seguinte Olá copiar a origem tipos foram adicionados:
  * [MongoDbSource](https://msdn.microsoft.com/library/mt765123.aspx)

## <a name="version-4100"></a>Versão 4.10.0
* foram adicionada Olá seguintes propriedades opcionais tooTextFormat:
  * [SkipLineCount](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.skiplinecount.aspx)
  * [FirstRowAsHeader](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.firstrowasheader.aspx)
  * [TreatEmptyAsNull](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.textformat.treatemptyasnull.aspx)
* Olá seguintes tipos de serviço ligado foram adicionados:
  * [OnPremisesCassandraLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandralinkedservice.aspx)
  * [SalesforceLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.salesforcelinkedservice.aspx)
* Olá tipos de conjunto de dados seguintes foram adicionado:
  * [OnPremisesCassandraTableDataset](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisescassandratabledataset.aspx)
* seguinte Olá copiar a origem tipos foram adicionados:
  * [CassandraSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.cassandrasource.aspx)
* Adicionar [WebServiceInputs](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azuremlbatchexecutionactivity.webserviceinputs.aspx) tooAzureMLBatchExecutionActivity de propriedade
  * Ative a transmissão de várias entradas de serviço web tooan experimentação de Azure Machine Learning

## <a name="version-491"></a>Versão 4.9.1
### <a name="bug-fix"></a>Correção de erro
* Preterir a autenticação baseada em End WebApi para [WebLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.weblinkedservice.authenticationtype.aspx).

## <a name="version-490"></a>Versão 4.9.0
### <a name="feature-additions"></a>Adições de funcionalidade
* Adicionar [EnableStaging](https://msdn.microsoft.com/library/mt767916.aspx) e [StagingSettings](https://msdn.microsoft.com/library/mt767918.aspx) tooCopyActivity de propriedades. Consulte [testado cópia](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes sobre a funcionalidade de Olá.

### <a name="bug-fix"></a>Correção de erro
* Introduzir uma sobrecarga de [ActivityWindowOperationExtensions.List](https://msdn.microsoft.com/library/mt767915.aspx) método, que demora um [ActivityWindowsByActivityListParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.activitywindowsbyactivitylistparameters.aspx) instância.
* Marca [WriteBatchSize](https://msdn.microsoft.com/library/dn884293.aspx) e [WriteBatchTimeout](https://msdn.microsoft.com/library/dn884245.aspx) como opcional na CopySink.

## <a name="version-480"></a>Versão 4.8.0
### <a name="feature-additions"></a>Adições de funcionalidade
* Olá propriedades opcionais a seguir foram adicionado tooCopy atividade escreva tooenable Otimização do desempenho de cópia:
  * [ParallelCopies](https://msdn.microsoft.com/library/mt767910.aspx)
  * [CloudDataMovementUnits](https://msdn.microsoft.com/library/mt767912.aspx)

## <a name="version-470"></a>Versão 4.7.0
### <a name="feature-additions"></a>Adições de funcionalidade
* Adicionar novo tipo de StorageFormat [OrcFormat](https://msdn.microsoft.com/library/mt723391.aspx) escreva toocopy ficheiros otimizados linha columnar (ORC) formato.
* Adicionar [AllowPolyBase](https://msdn.microsoft.com/library/mt723396.aspx) e PolyBaseSettings tooSqlDWSink de propriedades.
  * Permite a utilização de Olá dos dados de toocopy do PolyBase no SQL Data Warehouse.

## <a name="version-461"></a>Versão 4.6.1
### <a name="bug-fixes"></a>Correções de erros
* Correções de pedido HTTP para listar windows de atividade.
  * Remove o nome do grupo de recursos de Olá e nome da fábrica de dados Olá Olá do payload de pedidos.

## <a name="version-460"></a>Versão 4.6.0
### <a name="feature-additions"></a>Adições de funcionalidade
* Olá propriedades seguintes foram adicionadas demasiado[PipelineProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties_properties.aspx):
  * [PipelineMode](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.pipelinemode.aspx)
  * [ExpirationTime](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.expirationtime.aspx)
  * [Conjuntos de dados](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.pipelineproperties.datasets.aspx)
* Olá propriedades seguintes foram adicionadas demasiado[PipelineRuntimeInfo](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.aspx):
  * [PipelineState](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.common.models.pipelineruntimeinfo.pipelinestate.aspx)
* Adicionar novo [StorageFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.storageformat.aspx) tipo [JsonFormat](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.jsonformat.aspx) escreva conjuntos de dados de toodefine cujos dados estão no formato JSON.

## <a name="version-450"></a>Versão 4.5.0
### <a name="feature-additions"></a>Adições de funcionalidade
* Adicionar [listar operações para a janela de atividade](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.activitywindowoperationsextensions.aspx).
  * Adicionar windows de atividade de tooretrieve de métodos com filtros de com base nos tipos de entidade hello (ou seja, fábricas de dados, os conjuntos de dados, pipelines e atividades).
* Olá seguintes tipos de serviço ligado foram adicionados:
  * [ODataLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odatalinkedservice.aspx), [WebLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.weblinkedservice.aspx)
* Olá tipos de conjunto de dados seguintes foram adicionado:
  * [ODataResourceDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.odataresourcedataset.aspx), [WebTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.webtabledataset.aspx)
* seguinte Olá copiar a origem tipos foram adicionados:     
  * [WebSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.websource.aspx)

## <a name="version-440"></a>Versão 4.4.0
### <a name="feature-additions"></a>Adições de funcionalidade
* Olá seguinte tipo de serviço ligado foi adicionado como origens de dados e sinks para atividades de cópia:
  * [AzureStorageSasLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.azurestoragesaslinkedservice.aspx). Consulte [serviço ligado do Azure Storage SAS](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) para obter exemplos e informações conceptuais.

## <a name="version-430"></a>Versão 4.3.0
### <a name="feature-additions"></a>Adições de funcionalidade
* Olá seguintes haven de tipos de serviço ligado foi adicionado como origens de dados para atividades de cópia:
  * [HdfsLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.hdfslinkedservice.aspx). Consulte [mover dados do HDFS utilizando o Data Factory](data-factory-hdfs-connector.md) para obter exemplos e informações conceptuais.
  * [OnPremisesOdbcLinkedService](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.onpremisesodbclinkedservice.aspx). Consulte [mover dados de ODBC os arquivos de dados utilizando o Azure Data Factory](data-factory-odbc-connector.md) para obter exemplos e informações conceptuais.

## <a name="version-420"></a>Versão 4.2.0
### <a name="feature-additions"></a>Adições de funcionalidade
* foi adicionado Olá seguir o novo tipo de atividade: [AzureMLUpdateResourceActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremlupdateresourceactivity.aspx). Para obter detalhes sobre a atividade de Olá, consulte [modelos do Azure ML/atualizar utilizando Olá atividade do recurso da atualização](data-factory-azure-ml-batch-execution-activity.md).
* Uma nova propriedade opcional [updateResourceEndpoint](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.updateresourceendpoint.aspx) foi adicionado toohello [AzureMLLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuremllinkedservice.aspx).
* [LongRunningOperationInitialTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationinitialtimeout.aspx) e [LongRunningOperationRetryTimeout](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.longrunningoperationretrytimeout.aspx) propriedades foram adicionadas toohello [DataFactoryManagementClient](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.datafactorymanagementclient.aspx) classe.
* Permitir a configuração de tempos limite de Olá para chamadas de cliente toohello serviço Data Factory.

## <a name="version-410"></a>Versão 4.1.0
### <a name="feature-additions"></a>Adições de funcionalidade
* Olá seguintes tipos de serviço ligado foram adicionados:
  * [AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx)
  * [AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx)
* foram adicionada Olá os seguintes tipos de atividades:
  * [DataLakeAnalyticsUSQLActivity](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datalakeanalyticsusqlactivity.aspx)
* Olá tipos de conjunto de dados seguintes foram adicionado:
  * [AzureDataLakeStoreDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoredataset.aspx)
* Olá seguintes tipos de origem e dependente para a atividade de cópia foi adicionados:
  * [AzureDataLakeStoreSource](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresource.aspx)
  * [AzureDataLakeStoreSink](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestoresink.aspx)

## <a name="version-401"></a>Versão 4.0.1
### <a name="breaking-changes"></a>As alterações de última hora
Olá seguintes classes de mudança de nome. os nomes dos novos Olá foram nomes original de Olá de classes antes 4.0.0 de versão.

| Nome no 4.0.0 | Nome no 4.0.1 |
|:--- |:--- |
| AzureSqlDataWarehouseDataset |[AzureSqlDataWarehouseTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqldatawarehousetabledataset.aspx) |
| AzureSqlDataset |[AzureSqlTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuresqltabledataset.aspx) |
| AzureDataset |[AzureTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuretabledataset.aspx) |
| OracleDataset |[OracleTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.oracletabledataset.aspx) |
| RelationalDataset |[RelationalTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.relationaltabledataset.aspx) |
| SqlServerDataset |[SqlServerTableDataset](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.sqlservertabledataset.aspx) |

## <a name="version-400"></a>Versão 4.0.0
### <a name="breaking-changes"></a>As alterações de última hora
* cujo nome foi mudado Olá seguintes classes/interfaces.

| Nome antigo | Novo nome |
|:--- |:--- |
| ITableOperations |[IDatasetOperations](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.idatasetoperations.aspx) |
| Tabela |[Conjunto de dados](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.dataset.aspx) |
| TableProperties |[DatasetProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetproperties.aspx) |
| TableTypeProprerties |[DatasetTypeProperties](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasettypeproperties.aspx) |
| TableCreateOrUpdateParameters |[DatasetCreateOrUpdateParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateparameters.aspx) |
| TableCreateOrUpdateResponse |[DatasetCreateOrUpdateResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdateresponse.aspx) |
| TableGetResponse |[DatasetGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetgetresponse.aspx) |
| TableListResponse |[DatasetListResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetlistresponse.aspx) |
| CreateOrUpdateWithRawJsonContentParameters |[DatasetCreateOrUpdateWithRawJsonContentParameters](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.datasetcreateorupdatewithrawjsoncontentparameters.aspx) |

* Olá **lista** métodos devolvem resultados paginados agora. Se a resposta Olá contém um vazios **NextLink** propriedade, aplicações de cliente Olá tem toocontinue obter Olá página seguinte até que todas as páginas são devolvidas.  Segue-se um exemplo:

    ```csharp
    PipelineListResponse response = client.Pipelines.List("ResourceGroupName", "DataFactoryName");
    var pipelines = new List<Pipeline>(response.Pipelines);

    string nextLink = response.NextLink;
    while (!string.IsNullOrEmpty(nextLink))
    {
        PipelineListResponse nextResponse = client.Pipelines.ListNext(nextLink);
        pipelines.AddRange(nextResponse.Pipelines);

        nextLink = nextResponse.NextLink;
    }
    ```
* **Lista** pipeline API devolve apenas Olá resumo de um pipeline, em vez de detalhes completos. Por exemplo, as atividades num resumo de pipeline só contenham nome e tipo.

### <a name="feature-additions"></a>Adições de funcionalidade
* Olá [SqlDWSink](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsink.aspx) classe suporta duas novas propriedades **SliceIdentifierColumnName** e **SqlWriterCleanupScript**, toosupport idempotent cópia tooAzure dados do SQL Server Armazém. Consulte Olá [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md) artigo para obter detalhes sobre estas propriedades.
* Agora suportamos a executar o procedimento armazenado em relação a SQL Database do Azure e Azure SQL Data Warehouse origens como parte da atividade de cópia de Olá. Olá [SqlSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqlsource.aspx) e [SqlDWSource](https://msdn.microsoft.com/library/azure/microsoft.azure.management.datafactories.models.sqldwsource.aspx) as classes têm Olá seguintes propriedades: **SqlReaderStoredProcedureName** e **StoredProcedureParameters** . Consulte Olá [SQL Database do Azure](data-factory-azure-sql-connector.md#sqlsource) e [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#sqldwsource) artigos no Azure.com para obter detalhes sobre estas propriedades.  
