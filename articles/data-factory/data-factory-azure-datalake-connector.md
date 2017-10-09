---
title: aaaCopy tooand de dados do Azure Data Lake Store | Microsoft Docs
description: Saiba como toocopy tooand dados do Data Lake Store utilizando o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a>Copiar tooand de dados do Data Lake Store utilizando o Data Factory
Este artigo explica como toouse atividade de cópia no Azure Data Factory toomove dados tooand do Azure Data Lake Store. Baseia-se no Olá [atividades de movimentos de dados](data-factory-data-movement-activities.md) artigo, uma descrição geral do movimento de dados com a atividade de cópia.

## <a name="supported-scenarios"></a>Cenários suportados
Pode copiar dados **do Azure Data Lake Store** toohello seguir arquivos de dados:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Pode copiar dados de Olá seguir arquivos de dados **tooAzure Data Lake Store**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> Crie uma conta de Data Lake Store antes de criar um pipeline com atividade de cópia. Para obter mais informações, consulte [introdução ao Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="supported-authentication-types"></a>Tipos de autenticação suportados
conector do Data Lake Store Olá suporta estes tipos de autenticação:
* Autenticação do principal de serviço
* Autenticação de credencial (OAuth) do utilizador 

Recomendamos que utilize autenticação principal de serviço, especialmente para uma cópia de dados agendada. Comportamento de expiração do token pode ocorrer com autenticação de credenciais do utilizador. Para detalhes de configuração, consulte Olá [ligado propriedades do serviço](#linked-service-properties) secção.

## <a name="get-started"></a>Introdução
Pode criar um pipeline com uma atividade de cópia move os dados para/de um Azure Data Lake Store utilizando APIs/ferramentas diferentes.

Olá toocreate da forma mais fácil um dados toocopy do pipeline está toouse Olá **Assistente para copiar**. Para um tutorial sobre como criar um pipeline utilizando Olá Assistente para copiar, consulte [Tutorial: criar um pipeline com o Assistente para copiar](data-factory-copy-data-wizard-tutorial.md).

Também pode utilizar Olá seguintes ferramentas toocreate um pipeline: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo Azure Resource Manager** , **.NET API**, e **REST API**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.

Se utilizar ferramentas de Olá ou APIs, execute Olá os seguintes passos toocreate um pipeline que move o arquivo de dados do tooa sink do arquivo de dados de uma origem de dados:

1. Criar um **fábrica de dados**. Uma fábrica de dados pode conter um ou mais pipelines. 
2. Criar **serviços ligados** fábrica de dados de tooyour de arquivos de dados de entrada e saída de toolink. Por exemplo, se estiver a copiar dados de um tooan de armazenamento de Blobs do Azure do Azure Data Lake Store, criar dois serviços ligados toolink a conta de armazenamento do Azure e a fábrica de dados do Azure Data Lake store tooyour. As propriedades de serviço ligado que são específica tooAzure Data Lake Store, consulte [ligado propriedades do serviço](#linked-service-properties) secção. 
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para Olá. Exemplo de Olá mencionado no passo último Olá, criar um contentor de blob do conjunto de dados toospecify Olá e a pasta que contém dados de entrada Olá. Além disso, crie outro conjunto de dados toospecify Olá ficheiros e pastas caminho no Olá Data Lake store que contém dados Olá copiados Olá do armazenamento de Blobs. As propriedades do conjunto de dados que são específica tooAzure Data Lake Store, consulte [propriedades do dataset](#dataset-properties) secção.
3. Criar um **pipeline** com uma atividade de cópia executa um conjunto de dados como entrada e um conjunto de dados como resultado. Exemplo de Olá mencionado anteriormente, que utilizar BlobSource como uma origem e AzureDataLakeStoreSink como um sink para atividade de cópia de Olá. Da mesma forma, se estiver a copiar no Blob Storage do Azure Data Lake Store tooAzure, utilizar AzureDataLakeStoreSource e BlobSink na atividade de cópia de Olá. Para as propriedades da atividade de cópia que são específica tooAzure Data Lake Store, consulte [copiar propriedades da atividade](#copy-activity-properties) secção. Para obter detalhes sobre como toouse um arquivo de dados como uma origem ou de um receptor de mensagens em fila, clique em ligação Olá na secção anterior do Olá para o arquivo de dados.  

Quando utiliza o Assistente de Olá, definições de JSON para estas entidades do Data Factory (serviços ligados, conjuntos de dados e pipeline Olá) são criadas automaticamente para si. Ao utilizar ferramentas/APIs (exceto .NET API), é possível definir estas entidades do Data Factory utilizando o formato JSON Olá.  Para exemplos com definições de JSON para entidades do Data Factory que são utilizados toocopy dados para/de um Azure Data Lake Store, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-data-lake-store) secção deste artigo.

Olá seguintes secções fornece detalhes sobre as propriedades JSON que são utilizado toodefine Data Factory entidades específicas tooData Lake Store.

## <a name="linked-service-properties"></a>Propriedades de serviço ligado
Um serviço ligado liga uma fábrica de dados de tooa de arquivo de dados. Criar um serviço ligado do tipo **AzureDataLakeStore** toolink a fábrica de dados de tooyour de dados do Data Lake Store. Olá, a tabela seguinte descreve JSON elementos específicos tooData Lake Store ligado serviços. Pode escolher entre o principal de serviço e a autenticação de credenciais do utilizador.

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| **tipo** | a propriedade de tipo Olá tem de ser definida demasiado**AzureDataLakeStore**. | Sim |
| **dataLakeStoreUri** | Informações sobre Olá conta do Azure Data Lake Store. Estas informações demora um dos seguintes formatos de Olá: `https://[accountname].azuredatalakestore.net/webhdfs/v1` ou `adl://[accountname].azuredatalakestore.net/`. | Sim |
| **subscriptionId** | Olá de toowhich de ID de subscrição do Azure conta do Data Lake Store pertence. | Obrigatório para sink |
| **resourceGroupName** | Olá de toowhich de nome do recurso do Azure grupo conta de Data Lake Store pertence. | Obrigatório para sink |

### <a name="service-principal-authentication-recommended"></a>Autenticação principal de serviço (recomendada)
toouse a autenticação principal de serviço, registar uma entidade de aplicação no Azure Active Directory (Azure AD) e conceda-Olá aceder tooData Lake Store. Para obter passos detalhados, consulte [autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Tome nota dos Olá valores, que utiliza os seguintes toodefine Olá serviço ligado:
* ID da aplicação
* Chave da aplicação 
* ID do inquilino

> [!IMPORTANT]
> Se estiver a utilizar pipelines de dados do Olá Assistente para copiar tooauthor, certifique-se de que conceda principal de serviço Olá, pelo menos, um **leitor** função no controlo de acesso (gestão de identidades e acessos) para a conta de Data Lake Store Olá. Além disso, conceder, pelo menos, o principal de serviço Olá **leitura + executar** raiz de Data Lake Store para tooyour de permissão ("/") e os respectivos valores secundários. Caso contrário, poderá ver a mensagem de saudação "Olá credenciais fornecidas são inválidas."<br/><br/>
Depois de criar ou atualizar um principal de serviço no Azure AD, pode demorar alguns minutos para Olá alterações tootake efeito. Certifique-se de principal de serviço Olá e configurações de lista (ACL) de controlo de acesso de Data Lake Store. Se continuar a ver a mensagem de saudação "Olá credenciais fornecidas são inválidas", aguarde e tente novamente.

Utilize autenticação principal de serviço, especificando Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| **servicePrincipalId** | Especifique o ID de cliente. da aplicação Olá | Sim |
| **servicePrincipalKey** | Especifique a chave da aplicação Olá. | Sim |
| **inquilino** | Especifique as informações de inquilinos Olá (nome ou o inquilino ID de domínio) em que reside a aplicação. Pode obtê-lo por hovering rato Olá no canto superior direito de Olá de Olá portal do Azure. | Sim |

**Exemplo: Autenticação principal do serviço**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticação de credenciais de utilizador
Em alternativa, pode utilizar toocopy de autenticação de credenciais de utilizador do ou tooData Lake Store, especificando Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| **autorização** | Clique em Olá **autorizar** clique no botão no Olá Editor do Data Factory e introduza as credenciais que atribui a propriedade de toothis do URL de autorização do Olá gerado automaticamente. | Sim |
| **ID de sessão** | ID de sessão OAuth a partir de sessão de autorização do OAuth Olá. Cada ID de sessão é exclusivo e pode ser utilizado apenas uma vez. Esta definição é gerada automaticamente quando utiliza Olá Editor do Data Factory. | Sim |

**Exemplo: Autenticação de credenciais de utilizador**
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiração do token
Olá, código de autorização que geram utilizando Olá **autorizar** botão expira após um determinado período de tempo. Olá seguir mensagem significa que esse token de autenticação Olá expirou:

Erro de operação de credencial: invalid_grant - AADSTS70002: erro ao validar as credenciais. AADSTS70008: Olá fornecido a concessão de acesso expirado ou revogado. ID de rastreio: ID de correlação d18629e8-af88-43c5-88e3-d8419eb1fca1: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.

Olá tabela seguinte mostra tempos de expiração de Olá de diferentes tipos de contas de utilizador:


| Tipo de utilizador | Expira após |
|:--- |:--- |
| Contas de utilizador *não* geridas pelo Azure Active Directory (por exemplo, @hotmail.com ou @live.com) |12 horas |
| Contas de utilizadores geridas pelo Azure Active Directory |nos últimos 14 dias após o último setor de Olá executar <br/><br/>90 dias, se um setor com base num serviço ligado com base em OAuth é executado, pelo menos, uma vez a cada 14 dias |

Se alterar a palavra-passe antes da hora de expiração do token de Olá, token Olá expira imediatamente. Verá a mensagem de saudação mencionada anteriormente nesta secção.

Pode voltar a autorizar a conta de Olá utilizando Olá **autorizar** botão quando o token de Olá expira tooredeploy Olá serviço ligado. Também pode gerar valores para Olá **sessionId** e **autorização** Olá propriedades através de programação utilizando o seguinte código:


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
Para obter detalhes sobre as classes de fábrica de dados de Olá utilizados no código Olá, consulte Olá [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [ Classe de AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tópicos. Adicionar uma referência tooversion `2.9.10826.1824` de `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` para Olá `WindowsFormsWebAuthenticationDialog` classe utilizado no código Olá.

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
toospecify dados de entrada de toorepresent um conjunto de dados num arquivo Data Lake, definir Olá **tipo** propriedade de conjunto de dados de Olá demasiado**AzureDataLakeStore**. Conjunto Olá **linkedServiceName** serviço ligado de propriedade do Olá dataset toohello nome Olá Data Lake Store. Para obter uma lista completa de secções JSON e propriedades disponíveis para definir os conjuntos de dados, consulte Olá [criar conjuntos de dados](data-factory-create-datasets.md) artigo. Secções de um conjunto de dados em JSON, tais como **estrutura**, **disponibilidade**, e **política**, são semelhantes para todos os tipos de conjunto de dados (SQL database do Azure, BLOBs do Azure e a tabela do Azure, para exemplo). Olá **typeProperties** secção é diferente para cada tipo de conjunto de dados e fornece informações como a localização e o formato dos dados de Olá no arquivo de dados de Olá. 

Olá **typeProperties** secção para um conjunto de dados do tipo **AzureDataLakeStore** contém Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| **folderPath** |Contentor de toohello caminho e a pasta no Data Lake Store. |Sim |
| **nome de ficheiro** |Nome do ficheiro de Olá no Azure Data Lake Store. Olá **fileName** propriedade é opcional e maiúsculas e minúsculas. <br/><br/>Se especificar **fileName**, atividade Olá (incluindo cópia) funciona num ficheiro específico Olá.<br/><br/>Quando **fileName** não for especificado, cópia inclui todos os ficheiros no **folderPath** no conjunto de dados de entrada Olá.<br/><br/>Quando **fileName** não está especificado para um conjunto de dados de saída e **preserveHierarchy** não foram especificadas no receptor de atividade, nome de Olá do ficheiro de Olá gerado está num formato de Olá dados. _GUID_. txt '. Por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt. |Não |
| **partitionedBy** |Olá **partitionedBy** propriedade é opcional. Pode utilizá-lo toospecify um dinâmico caminho e nome de ficheiro de dados de séries de tempo. Por exemplo, **folderPath** podem ser parametrizadas para cada hora dos dados. Para obter detalhes e exemplos, consulte [Olá partitionedBy propriedade](#using-partitionedby-property). |Não |
| **formato** | é suportado os seguintes tipos de formato de Olá: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, e  **ParquetFormat**. Conjunto Olá **tipo** propriedade **formato** tooone destes valores. Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato ORC](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) secções Olá [formatos de ficheiro e compressão suportados pelo Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo. <br><br> Se pretender que os ficheiros de toocopy "como-é" entre arquivos baseados em ficheiros (cópia binário), ignorar Olá `format` secção em ambas as definições do conjunto de dados de entrada e de saída. |Não |
| **compressão** | Especifique o tipo de Olá e nível de compressão de dados de Olá. Tipos suportados são **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**. Níveis suportados são **Optimal** e **Fastest**. Para obter mais informações, consulte [formatos de ficheiro e compressão suportados pelo Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Não |

### <a name="hello-partitionedby-property"></a>propriedade de partitionedBy Olá
Pode especificar dinâmica **folderPath** e **fileName** propriedades para dados de séries de tempo com Olá **partitionedBy** propriedade, funções de fábrica de dados e do sistema variáveis. Para obter mais informações, consulte Olá [do Azure Data Factory - as funções e variáveis do sistema](data-factory-functions-variables.md) artigo.


No seguinte exemplo, de Olá `{Slice}` é substituído pelo valor Olá da variável de sistema do Data Factory Olá `SliceStart` no formato de Olá especificado (`yyyyMMddHH`). nome de Olá `SliceStart` refere-se a hora de início do setor Olá toohello. Olá `folderPath` propriedade é diferente para cada setor, como em `wikidatagateway/wikisampledataout/2014100103` ou `wikidatagateway/wikisampledataout/2014100104`.

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

No Olá seguinte exemplo, Olá ano, mês, dia e tempo de `SliceStart` são extraídos em separado variáveis que são utilizadas por Olá `folderPath` e `fileName` propriedades:
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Para obter mais detalhes sobre conjuntos de dados de séries de tempo, agendar e setores, consulte Olá [conjuntos de dados no Azure Data Factory](data-factory-create-datasets.md) e [Data Factory agendamento e execução](data-factory-scheduling-and-execution.md) artigos. 


## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para uma lista completa das secções e propriedades disponíveis para definir as atividades, consulte Olá [Criar pipelines](data-factory-create-pipelines.md) artigo. Propriedades, tais como o nome, descrição e de saída, tabelas e política estão disponíveis para todos os tipos de atividades.

Olá propriedades disponíveis nos Olá **typeProperties** secção de uma atividade variar de acordo com cada tipo de atividade. Para uma atividade de cópia, podem variam consoante os tipos de origens e sinks Olá.

**AzureDataLakeStoreSource** suporta Olá seguinte propriedade no Olá **typeProperties** secção:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| **recursiva** |Indica se Olá é ler dados recursivamente subpastas Olá ou apenas a pasta especificada Olá. |TRUE (valor predefinido), False |Não |


**AzureDataLakeStoreSink** suporta Olá seguintes propriedades no Olá **typeProperties** secção:

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| **copyBehavior** |Especifica o comportamento de cópia de Olá. |<b>PreserveHierarchy</b>: preserva a hierarquia de ficheiros de Olá na pasta de destino Olá. o caminho relativo Olá da pasta de toosource do ficheiro de origem é idêntico toohello caminho relativo de tootarget da pasta do ficheiro de destino.<br/><br/><b>FlattenHierarchy</b>: todos os ficheiros da pasta de origem Olá são criados no nível de primeiro Olá da pasta de destino Olá. ficheiros do destino de Olá são criados com nomes gerado automaticamente.<br/><br/><b>MergeFiles</b>: une todos os ficheiros a partir do ficheiro de tooone da pasta de origem de Olá. Se hello nome de ficheiro ou blob for especificado, Olá ficheiro intercalado é Olá especificado nome. Caso contrário, o nome de ficheiro Olá é gerado automaticamente. |Não |

### <a name="recursive-and-copybehavior-examples"></a>Exemplos de recursiva e copyBehavior
Esta secção descreve o comportamento resultante de Olá de operação de cópia de Olá para diferentes combinações de valores recursiva e copyBehavior.

| Recursiva | copyBehavior | Comportamento resultante |
| --- | --- | --- |
| VERDADEIRO |preserveHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá mesmo estrutura como origem Olá<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| VERDADEIRO |flattenHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>destino de Olá Pasta1 é criado com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File5 |
| VERDADEIRO |mergeFiles |Para uma pasta de origem Pasta1 com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>destino de Olá Pasta1 é criado com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + ficheiro 5 é intercalado conteúdo para um ficheiro com nome de ficheiro gerado automaticamente |
| FALSO |preserveHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura: <br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |
| FALSO |flattenHierarchy |Para uma pasta de origem Pasta1 com Olá seguir a estrutura:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para File2<br/><br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |
| FALSO |mergeFiles |Para uma pasta de origem Pasta1 com Olá seguir a estrutura:<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>pasta de destino Olá Pasta1 é criada com Olá seguir a estrutura<br/><br/>Pasta1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 conteúdos são intercalados para um ficheiro com nome de ficheiro gerada automaticamente. nome gerado automaticamente para File1<br/><br/>Não Subfolder1 com File3, File4 e File5 captado. |

## <a name="supported-file-and-compression-formats"></a>Formatos de ficheiro e compressão suportados
Para obter mais informações, consulte Olá [formatos de ficheiro e compressão no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artigo.

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a>Exemplos JSON para copiar dados tooand do Data Lake Store
Olá exemplos a seguir fornece definições JSON de exemplo. Pode utilizar estes toocreate de definições de exemplo um pipeline com Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Olá exemplos mostram como toocopy tooand de dados do armazenamento do Data Lake Store e BLOBs do Azure. No entanto, os dados podem ser copiados _diretamente_ de qualquer um dos Olá origens tooany de sinks Olá suportado. Para obter mais informações, consulte a secção de Olá "arquivos de dados suportadas e formatos" em Olá [mover dados utilizando a atividade de cópia](data-factory-data-movement-activities.md) artigo.  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a>Exemplo: Copiar dados de tooAzure do Blob Storage do Azure Data Lake Store
Mostra o código de exemplo de Olá nesta secção:

* Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Um serviço ligado do tipo [AzureDataLakeStore](#linked-service-properties).
* Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureDataLakeStore](#dataset-properties).
* A [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que utiliza [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureDataLakeStoreSink](#copy-activity-properties).

Olá exemplos mostram como séries de tempo dados a partir do Blob Storage do Azure são copiado tooData Lake Store a cada hora. 

**Serviço ligado do Armazenamento do Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**Serviço ligado do Azure Data Lake Store**

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> Para detalhes de configuração, consulte Olá [ligado propriedades do serviço](#linked-service-properties) secção.
>

**Conjunto de dados de entrada do blobs do Azure**

No seguinte exemplo de Olá, dados são captados um blob de novo a cada hora (`"frequency": "Hour", "interval": 1`). Olá pasta caminho e nome de ficheiro para o blob Olá dinamicamente são avaliados com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza Olá ano, mês e parte do dia Olá da hora de início. nome de ficheiro Olá utiliza hora Olá parte Olá a hora de início. Olá `"external": true` definição informa o serviço do Data Factory Olá nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

**Conjunto de dados de saída do Azure Data Lake Store**

Olá arquivo de Lake de tooData de dados de cópias de exemplo a seguir. Novos dados são copiados tooData Lake Store a cada hora.

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


**Atividade de cópia de um pipeline com uma origem de blob e um receptor de Data Lake Store**

No seguinte exemplo de Olá, pipeline Olá contém uma atividade de cópia está configurada toouse Olá conjuntos de dados de entrada e de saída. atividade de cópia de Olá é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá `source` tipo está definido demasiado`BlobSource`e Olá `sink` tipo está definido demasiado`AzureDataLakeStoreSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a>Exemplo: Copiar dados do Azure Data Lake Store tooan BLOBs do Azure
Mostra o código de exemplo de Olá nesta secção:

* Um serviço ligado do tipo [AzureDataLakeStore](#linked-service-properties).
* Um serviço ligado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Uma entrada [dataset](data-factory-create-datasets.md) do tipo [AzureDataLakeStore](#dataset-properties).
* Uma saída [dataset](data-factory-create-datasets.md) do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* A [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que utiliza [AzureDataLakeStoreSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

código de Olá copia dados de séries de tempo da Data Lake Store tooan BLOBs do Azure a cada hora. 

**Serviço ligado do Azure Data Lake Store**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> Para detalhes de configuração, consulte Olá [ligado propriedades do serviço](#linked-service-properties) secção.
>

**Serviço ligado do Armazenamento do Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Conjunto de dados de entrada do Azure Data Lake**

Neste exemplo, definição `"external"` demasiado`true` informa o serviço do Data Factory Olá nessa tabela Olá é toohello externo fábrica de dados e não é produzida por uma atividade no factory de dados de Olá.

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
        "policy": {
              "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
              }
        }
      }
}
```
**Conjunto de dados de saída do blob do Azure**

No seguinte exemplo de Olá, são escritos dados no blob tooa de novo a cada hora (`"frequency": "Hour", "interval": 1`). caminho da pasta Olá para BLOBs Olá dinamicamente é avaliado com base na hora de início de Olá do setor de Olá que está a ser processado. caminho da pasta Olá utiliza Olá ano, mês, dia e parte horas Olá da hora de início.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Uma atividade de cópia num pipeline com uma origem de Azure Data Lake Store e um receptor de blob**

No seguinte exemplo de Olá, pipeline Olá contém uma atividade de cópia está configurada toouse Olá conjuntos de dados de entrada e de saída. atividade de cópia de Olá é agendada toorun a cada hora. No pipeline de Olá definição JSON, Olá `source` tipo está definido demasiado`AzureDataLakeStoreSource`e Olá `sink` tipo está definido demasiado`BlobSink`.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

Na definição de atividade de cópia de Olá, também pode mapear colunas de Olá toocolumns de conjunto de dados de origem no conjunto de dados do Olá sink. Para obter mais informações, consulte [mapeamento de colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e otimização
toolearn sobre fatores Olá que afetam o desempenho de atividade de cópia e como toooptimize-lo, consulte Olá [guia Otimização e de desempenho de atividade de cópia](data-factory-copy-activity-performance.md) artigo.
