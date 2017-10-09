---
title: "ferramenta de migração de aaaDatabase para a base de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como toouse Olá abrir origem Azure Cosmos DB dados migração ferramentas tooimport dados tooAzure Cosmos DB de várias origens, incluindo ficheiros MongoDB, SQL Server, Table storage, Amazon DynamoDB, CSV e JSON. Conversão de tooJSON CSV."
keywords: "toojson csv, as ferramentas de migração de base de dados, converter csv toojson"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>Como tooimport dados na base de dados do Azure Cosmos para Olá API do DocumentDB?

Este tutorial fornece instruções sobre como utilizar Olá BD do Azure Cosmos: ferramenta de migração de dados de API do DocumentDB, que pode importar dados a partir de várias origens, incluindo ficheiros JSON, CSV ficheiros, SQL Server, o MongoDB, o Table storage do Azure, Amazon DynamoDB e DocumentDB do Azure Cosmos DB Coleções de API para coleções para utilizam com a base de dados do Azure Cosmos e Olá API do DocumentDB. Também pode ser utilizada a ferramenta de migração de dados de Olá quando migrar a partir de uma única partição coleção tooa partição multi coleção Olá API do DocumentDB.

ferramenta de migração de dados de Olá só funciona quando a importação de dados na base de dados do Azure Cosmos para utilizam com Olá API do DocumentDB. Importar dados para utilização com Olá API de tabela ou Graph API não é suportado neste momento. 

dados de tooimport para utilização com Olá API do MongoDB, consulte [BD do Azure Cosmos: como dados de toomigrate para Olá MongoDB API?](mongodb-migrate.md).

Este tutorial abrange Olá seguintes tarefas:

> [!div class="checklist"]
> * Instalar a ferramenta de migração de dados de Olá
> * Importar dados a partir de origens de dados diferentes
> * Exportação de base de dados do Azure Cosmos tooJSON

## <a id="Prerequisites"></a>Pré-requisitos
Antes de seguir as instruções de Olá neste artigo, certifique-se de que tem o seguinte Olá instalado:

* [O Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) ou superior.

## <a id="Overviewl"></a>Descrição geral da ferramenta de migração de dados de Olá
ferramenta de migração de dados de Olá é uma solução de código aberto que importa dados tooAzure Cosmos BD a partir de uma variedade de origens, incluindo:

* Ficheiros JSON
* MongoDB
* SQL Server
* Ficheiros CSV
* Armazenamento de Tabelas do Azure
* Amazon DynamoDB
* HBase
* Coleções do Cosmos BD do Azure

Enquanto a ferramenta de importação de Olá inclui uma interface gráfica (dtui.exe), também pode ser controlada Olá linha de comandos (dt.exe). Na verdade, há um comando de Olá associado toooutput opção depois de configurar uma importação através de Olá IU. Pode ser transformadas a tabela de origem de dados (por exemplo, SQL Server ou ficheiros CSV) que podem ser criadas relações hierárquicas (subdocuments) durante a importação. Manter toolearn de ler mais sobre as opções de origem, tooimport de linhas de comandos de exemplo de cada origem, as opções de destino e visualizar os resultados de importar.

## <a id="Install"></a>Instalar a ferramenta de migração de dados de Olá
código de origem da ferramenta de migração de Olá está disponível no GitHub em [este repositório](https://github.com/azure/azure-documentdb-datamigrationtool) e está disponível a partir de uma versão de compilados [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d). Pode compilar solução Olá ou simplesmente transferir e extrair o diretório de tooa versão compilada Olá à sua escolha. Em seguida, execute um:

* **Dtui.exe**: versão de interface gráfica da ferramenta de Olá
* **DT.exe**: versão de linha de comandos da ferramenta de Olá

## <a name="import-data"></a>Importar dados

Assim que instalou a ferramenta de Olá, é tooimport tempo os dados. Que tipo de dados pretende tooimport?

* [Ficheiros JSON](#JSON)
* [MongoDB](#MongoDB)
* [Ficheiros de exportação do MongoDB](#MongoDBExport)
* [SQL Server](#SQL)
* [Ficheiros CSV](#CSV)
* [Armazenamento de tabelas do Azure](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [Blob](#BlobImport)
* [Coleções do Cosmos BD do Azure](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Importação de em massa do Cosmos BD do Azure](#DocumentDBBulkImport)
* [Importação de registo sequenciais Cosmos BD do Azure](#DocumentDSeqTarget)


## <a id="JSON"></a>ficheiros JSON tooimport
Olá opção de importador de origem de ficheiro JSON permite-lhe tooimport um ou mais ficheiros JSON único documento ou ficheiros JSON que contém cada uma matriz de documentos JSON. Ao adicionar pastas que contêm tooimport de ficheiros JSON, tiver opção Olá recursivamente a procurar ficheiros em subpastas.

![Opções de origem de ficheiro de captura de ecrã de JSON - ferramentas de migração de bases de dados](./media/import-data/jsonsource.png)

Seguem-se alguns ficheiros JSON de tooimport de amostras de linha de comandos:

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <a id="MongoDB"></a>tooimport do MongoDB

> [!IMPORTANT]
> Se estiver a importar conta de base de dados do Azure Cosmos tooan com suporte para o MongoDB, siga estes [instruções](mongodb-migrate.md).
> 
> 

Olá opção de importador de origem do MongoDB permite-lhe tooimport de uma coleção de MongoDB individuais e, opcionalmente, filtrar documentos através de uma consulta e/ou modificar a estrutura de documento Olá através da utilização de uma projecção.  

![Opções de origem de captura de ecrã do MongoDB](./media/import-data/mongodbsource.png)

cadeia de ligação de Olá está no formato de MongoDB padrão Olá:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Utilize Olá verifique comando tooensure que Olá instância do MongoDB especificada no campo de cadeia de ligação de Olá pode ser acedido.
> 
> 

Introduza o nome de Olá da coleção de Olá partir da qual os dados serão importados. Opcionalmente, pode especificar ou fornecer um ficheiro para uma consulta (por exemplo, {pop: {$gt: 5000}}) e/ou projecção (por exemplo, {loc:0}) tooboth filtro e forma Olá dados toobe importado.

Seguem-se algumas tooimport de amostras de linha de comandos do MongoDB:

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>ficheiros de exportação do MongoDB tooimport

> [!IMPORTANT]
> Se estiver a importar conta de base de dados do Azure Cosmos tooan com suporte para o MongoDB, siga estes [instruções](mongodb-migrate.md).
> 
> 

Olá os opção do importador de origem do ficheiro JSON do MongoDB exportação permite-lhe tooimport um ou mais ficheiros JSON produzidos do utilitário de mongoexport Olá.  

![Opções de origem de exportação de captura de ecrã do MongoDB](./media/import-data/mongodbexportsource.png)

Ao adicionar pastas que contêm ficheiros JSON de exportação de MongoDB para importação, terá de opção de Olá de recursivamente a procurar ficheiros em subpastas.

Eis um tooimport de exemplo de linha de comandos da exportação do MongoDB ficheiros JSON:

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>tooimport do SQL Server
Olá opção de importador de origem SQL permite-lhe tooimport de uma base de dados individuais do SQL Server e, opcionalmente, filtrar Olá registos toobe importado utilizando uma consulta. Além disso, pode modificar a estrutura de documento Olá, especificando um separador de aninhamento (mais informações sobre as que dentro de momentos).  

![Opções de origem de captura de ecrã do SQL Server - as ferramentas de migração de base de dados](./media/import-data/sqlexportsource.png)

formato de Olá Olá da cadeia de ligação é o formato de cadeia de ligação do Olá padrão SQL.

> [!NOTE]
> Utilize Olá verifique comando tooensure que Olá instância do SQL Server especificada no campo de cadeia de ligação de Olá pode ser acedido.
> 
> 

Olá aninhamento de propriedade de separador é utilizado toocreate hierárquica relações (secundárias documentos) durante a importação. Considere Olá seguinte consulta SQL:

*Selecione CAST (BusinessEntityID AS varchar) como Id, o nome, AddressType como [Address.AddressType], AddressLine1 como [Address.AddressLine1], cidade como [Address.Location.City], StateProvinceName como [Address.Location.StateProvinceName], PostalCode como [ Address.PostalCode] CountryRegionName como [Address.CountryRegionName] do Sales.vStoreWithAddresses onde AddressType = 'Sede'*

Que devolve Olá os seguintes resultados (parciais):

![Resultados da consulta de captura de ecrã do SQL Server](./media/import-data/sqlqueryresults.png)

Tenha em atenção os aliases de Olá como Address.AddressType e Address.Location.StateProvinceName. Ao especificar um separador de aninhamento de '.', ferramenta de importação de Olá cria endereço e Address.Location subdocuments durante Olá importar. Eis um exemplo de um documento do BD Azure Cosmos resultante:

*{"id": "956", "Name": "Melhorar vendas e serviço de", "Endereço": {"AddressType": "Main Office", "AddressLine1": "#500 75 O'Connor Rua", "Localização": {"Cidade": "Ottawa", "StateProvinceName": "Ontario"}, "PostalCode": "K4B 1S2", "CountryRegionName": " Canadá"}}*

Seguem-se algumas tooimport de amostras de linha de comandos do SQL Server:

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>ficheiros CSV tooimport e converter CSV tooJSON
Olá opção de importador de origem de ficheiro CSV permite-lhe tooimport um ou mais ficheiros CSV. Ao adicionar pastas que contêm ficheiros CSV para importar, tiver opção Olá recursivamente a procurar ficheiros em subpastas.

![Opções de origem de captura de ecrã do CSV - tooJSON CSV](media/import-data/csvsource.png)

Origem SQL toohello semelhante, Olá aninhamento propriedade separador estar toocreate utilizados hierárquica relações (secundárias documentos) durante a importação. Considere Olá seguinte linha de cabeçalho CSV e linhas de dados:

![Registos de exemplo de captura de ecrã do CSV - tooJSON CSV](./media/import-data/csvsample.png)

Tenha em atenção os aliases de Olá como DomainInfo.Domain_Name e RedirectInfo.Redirecting. Ao especificar um separador de aninhamento de '.', a ferramenta de importação de Olá criará DomainInfo e RedirectInfo subdocuments durante Olá importar. Eis um exemplo de um documento do BD Azure Cosmos resultante:

*{"DomainInfo": {"Nome_domínio": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Agência Federal":"Conferência administrativa de Olá dos Estados Unidos","RedirectInfo": {"Redirecionar":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*

ferramenta de importação de Olá tentará informações de tipo tooinfer por valores unquoted ficheiros CSV (delimitado por aspas valores sempre são tratados como cadeias).  Tipos são identificados num Olá seguinte ordem: número, datetime, booleano.  

Existem dois outro toonote coisas sobre importação de CSV:

1. Por predefinição, valores unquoted sempre são recortados para separadores e espaços, enquanto os valores entre aspas são preservados como-é. Este comportamento pode ser substituído por Olá que cortar quoted valores caixa de verificação ou Olá /s.TrimQuoted linha de comandos opção.
2. Por predefinição, um nulo unquoted é tratado como um valor nulo. Este comportamento pode ser substituído (ou seja, processe um unquoted nulo como uma cadeia "null") com Olá Treat unquoted nulo como caixa de verificação ou Olá /s.NoUnquotedNulls linha de comandos a opção de cadeia.

Eis um exemplo de linha de comandos para importação de CSV:

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>tooimport do Table storage do Azure
Olá opção do importador de origem de armazenamento de tabelas do Azure permite-lhe tooimport de uma tabela de armazenamento de tabelas do Azure individual e, opcionalmente, filtrar Olá tabela entidades toobe importado. Tenha em atenção que não é possível utilizar dados de armazenamento de Azure Table ferramenta tooimport Olá migração de dados na base de dados do Azure Cosmos para utilização com Olá API de tabela. Importar apenas tooAzure Cosmos DB para utilização com Olá API do DocumentDB é suportado neste momento.

![Opções de origem do armazenamento de captura de ecrã de tabelas do Azure](./media/import-data/azuretablesource.png)

formato de Olá do Olá cadeia de ligação de armazenamento de tabelas do Azure é:

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Utilize Olá verifique comando tooensure que Olá instância de armazenamento de tabelas do Azure especificada no campo de cadeia de ligação de Olá pode ser acedido.
> 
> 

Introduza o nome de Olá de Olá Azure tabela a partir da qual os dados serão importados. Opcionalmente, pode especificar um [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).

Olá opção do importador de origem de armazenamento de tabelas do Azure tem Olá seguintes opções adicionais:

1. Incluir campos internos
   1. -Incluem todos os campos internos (PartitionKey, RowKey e Timestamp)
   2. Nenhum - excluir todos os campos internos
   3. RowKey - incluir apenas o campo de RowKey Olá
2. Selecionar colunas
   1. Os filtros de armazenamento do Azure tabela não suportam projeções. Se pretender que as propriedades de entidade de Azure Table específicas do tooonly importação, adicioná-los toohello lista de colunas selecionadas. Todas as outras propriedades de entidade serão ignoradas.

Eis um tooimport de exemplo de linha de comandos do Table storage do Azure:

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>tooimport da Amazon DynamoDB
Olá opção de importador de origem do Amazon DynamoDB permite-lhe tooimport de uma tabela de Amazon DynamoDB individuais e, opcionalmente, filtrar Olá entidades toobe importado. Vários modelos são fornecidos para que configurar uma importação é tão simples quanto possível.

![Opções de origem de captura de ecrã da Amazon DynamoDB - ferramentas de migração de bases de dados](./media/import-data/dynamodbsource1.png)

![Opções de origem de captura de ecrã da Amazon DynamoDB - ferramentas de migração de bases de dados](./media/import-data/dynamodbsource2.png)

formato de Olá do Olá Amazon DynamoDB cadeia de ligação é:

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Utilize Olá verifique comando tooensure que Olá instância Amazon DynamoDB especificada no campo de cadeia de ligação de Olá pode ser acedido.
> 
> 

Eis um tooimport de exemplo de linha de comandos do Amazon DynamoDB:

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>ficheiros de tooimport do Blob storage do Azure
Olá ficheiro JSON, ficheiro de exportação do MongoDB e as opções do importador de origem de ficheiro do CSV permitem-lhe tooimport um ou mais ficheiros do Blob storage do Azure. Depois de especificar um URL do contentor de Blob e a chave da conta, forneça uma expressão regular tooselect Olá ficheiros tooimport.

![Opções de origem do ficheiro de captura de ecrã do Blob](./media/import-data/blobsource.png)

Segue-se a linha de comandos exemplo tooimport JSON os ficheiros do armazenamento de Blobs do Azure:

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>tooimport de uma coleção de API de DocumentDB do Azure Cosmos DB
Olá opção de importador de origem de BD do Cosmos Azure permite-lhe tooimport dados a partir de uma ou mais coleções da base de dados do Azure Cosmos e, opcionalmente, filtrar documentos através de uma consulta.  

![Opções de origem de BD do Cosmos captura de ecrã do Azure](./media/import-data/documentdbsource.png)

formato de Olá do Olá cadeia de ligação de base de dados do Azure Cosmos é:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Olá cadeia de ligação de conta de base de dados do Azure Cosmos pode ser obtido a partir do painel de chaves de Olá de Olá portal do Azure, conforme descrito em [como toomanage uma conta de base de dados do Azure Cosmos](manage-account.md); no entanto, o nome de Olá da base de dados de Olá tem toohello toobe anexado cadeia de ligação no Olá seguinte formato:

    Database=<CosmosDB Database>;

> [!NOTE]
> Utilize Olá verifique comando tooensure que Olá instância de base de dados do Azure Cosmos especificada no campo de cadeia de ligação de Olá pode ser acedido.
> 
> 

tooimport de uma única coleção da base de dados do Azure Cosmos, introduza o nome de Olá da coleção de Olá partir da qual os dados serão importados. tooimport de várias coleções de BD do Cosmos do Azure, forneça uma expressão regular toomatch um ou mais nomes de coleção (por exemplo, collection01 | collection02 | collection03). Opcionalmente, pode especificar, ou fornecer um ficheiro para um filtro de tooboth de consulta e formam Olá dados toobe importado.

> [!NOTE]
> Uma vez que o campo de coleção de Olá aceita expressões regulares, se estiver a importar a partir de uma única coleção cujo nome contém carateres de expressão regular, em seguida, esses carateres tem de ser escape em conformidade.
> 
> 

Olá opção de importador de origem de base de dados do Azure Cosmos tem seguinte Olá opções avançadas:

1. Incluir campos internos: Especifica se pretende ou não tooinclude Azure Cosmos DB documento das propriedades do sistema no Olá exportar (por exemplo, _ts, _rid).
2. Número de tentativas em caso de falha: Especifica Olá diversas vezes tooretry Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).
3. Intervalo de repetição: Especifica quanto toowait entre repetir Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).
4. Modo de ligação: Especifica toouse de modo de ligação de Olá com base de dados do Azure Cosmos. opções disponíveis Olá são DirectTcp, DirectHttps e Gateway. modos de ligação direta Olá são mais rápida, enquanto o modo de gateway de Olá é firewall mais amigável como o utiliza apenas a porta 443.

![Origem de captura de ecrã da BD do Cosmos Azure opções avançadas](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> modo de tooconnection de predefinições de ferramenta DirectTcp de importação de Olá. Se ocorrerem problemas de firewall, alternar modo tooconnection Gateway, porque requer apenas a porta 443.
> 
> 

Seguem-se algumas tooimport de amostras de linha de comandos da base de dados do Azure Cosmos:

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> Olá ferramenta de importação de dados do Azure Cosmos DB também suporta a importação de dados de Olá [emulador de BD do Azure Cosmos](local-emulator.md). Ao importar dados a partir de um emulador local, definir ponto final de Olá demasiado`https://localhost:<port>`. 
> 
> 

## <a id="HBaseSource"></a>tooimport do HBase
Olá opção de importador de origem do HBase permite-lhe tooimport dados a partir de uma tabela de HBase e, opcionalmente, filtrar dados Olá. Vários modelos são fornecidos para que configurar uma importação é tão simples quanto possível.

![Opções de origem de captura de ecrã do HBase](./media/import-data/hbasesource1.png)

![Opções de origem de captura de ecrã do HBase](./media/import-data/hbasesource2.png)

formato de Olá do Olá HBase Stargate cadeia de ligação é:

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Utilize Olá verifique comando tooensure que Olá instância HBase especificada no campo de cadeia de ligação de Olá pode ser acedido.
> 
> 

Eis um tooimport de exemplo de linha de comandos do HBase:

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (importar em massa)
importador de em massa de BD do Azure Cosmos Olá permite-lhe tooimport de qualquer uma das opções de origem disponível Olá, utilizando um procedimento de BD do Cosmos Azure armazenados para uma eficiência. Olá ferramenta suporta a importação tooone particionado em único base de dados do Azure Cosmos coleção, bem como a importação na qual os dados estão particionados em várias coleções de base de dados do Azure Cosmos particionado em único. Para obter mais informações sobre a criação de partições de dados, consulte [divisão em partições e o dimensionamento do BD Azure Cosmos](partition-data.md). ferramenta de Olá irá criar, executar e, em seguida, elimine o procedimento armazenado de Olá do Olá destino collection(s).  

![Opções de em massa de BD do Cosmos captura de ecrã do Azure](./media/import-data/documentdbbulk.png)

formato de Olá do Olá cadeia de ligação de base de dados do Azure Cosmos é:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Olá cadeia de ligação de conta de base de dados do Azure Cosmos pode ser obtido a partir do painel de chaves de Olá de Olá portal do Azure, conforme descrito em [como toomanage uma conta de base de dados do Azure Cosmos](manage-account.md); no entanto, o nome de Olá da base de dados de Olá tem toohello toobe anexado cadeia de ligação no Olá seguinte formato:

    Database=<CosmosDB Database>;

> [!NOTE]
> Utilize Olá verifique comando tooensure que Olá instância de base de dados do Azure Cosmos especificada no campo de cadeia de ligação de Olá pode ser acedido.
> 
> 

tooimport tooa única coleção, introduza o nome de Olá de Olá coleção toowhich dados serão importados e clique no botão Adicionar de Olá. tooimport toomultiple coleções, introduza o nome de cada coleção individualmente ou utilizar Olá seguindo a sintaxe toospecify várias coleções: *collection_prefix*[iniciar índice - índice de fim]. Ao especificar várias coleções através da sintaxe acima mencionados Olá, tenha em atenção Olá seguinte:

1. São suportados apenas número inteiro intervalo padrões de nome. Por exemplo, especificar a coleção [0-3] irá produzir Olá seguintes coleções: collection0, collection1, collection2, collection3.
2. Pode utilizar uma sintaxe abreviada: recolha [3] irá emitir o mesmo conjunto de coleções mencionado no passo 1.
3. Pode ser fornecida mais do que uma substituição. Por exemplo, a coleção [0-1], [0-9] irá gerar 20 nomes de colecção com líderes zeros (collection01,.. 02,... 03).

Depois de Olá coleção nomes foram especificadas, escolhe o débito pretendido Olá Olá collection(s) (400 RUs too10 000 RUs). Para melhor desempenho de importação, escolha um maior débito. Para obter mais informações sobre os níveis de desempenho, consulte [níveis de desempenho na base de dados do Azure Cosmos](performance-levels.md).

> [!NOTE]
> definição de débito de desempenho de Olá só se aplica toocollection criação. Se Olá especificado coleção já existe, o débito não será modificado.
> 
> 

Quando importar coleções toomultiple, a ferramenta de importação de Olá suporta fragmentação de hash com base. Neste cenário, especifique a propriedade de documento Olá desejar toouse como Olá chave de partição (se a chave de partição for deixada em branco, documentos será a aleatoriamente em coleções de destino Olá).

Opcionalmente, pode especificar o campo na origem de importação de Olá deve ser utilizado como Olá propriedade de id do documento de base de dados do Azure Cosmos durante a importação de Olá (tenha em atenção que se documentos não contêm esta propriedade, em seguida, Olá importação ferramenta irá gerar um GUID como valor de propriedade de id de Olá).

Existem várias opções avançadas de disponíveis durante a importação. Em primeiro lugar, enquanto a ferramenta de Olá inclui um volume de predefinição importar procedimento armazenado (BulkInsert.js), pode optar por toospecify seu próprio procedimento de importação armazenado:

 ![Opção de sproc de inserção de em massa de BD do Cosmos captura de ecrã do Azure](./media/import-data/bulkinsertsp.png)

Além disso, ao importar os tipos de data (por exemplo, a partir de SQL Server ou o MongoDB), pode escolher entre três opções de importação:

 ![Opções de importação do BD do Cosmos captura de ecrã do Azure data hora](./media/import-data/datetimeoptions.png)

* Cadeia: Manter como um valor de cadeia
* Época: Manter como um valor de número de época
* Ambas: Manter a cadeia e valores numéricos época. Esta opção irá criar um subdocument, por exemplo: "date_joined": {"Valor": "2013-10-21T21:17:25.2410000Z", "época": 1382390245}

importador de em massa de BD do Azure Cosmos Olá tem seguinte de Olá adicionais opções avançadas:

1. Tamanho do lote: Olá ferramenta predefinições tooa tamanho do lote de 50.  Se Olá documentos toobe importado é grande, considere reduzir o tamanho do lote Olá. Por outro lado, se Olá documentos toobe importado é pequeno, considere aumentar o tamanho do lote Olá.
2. Tamanho máximo de Script (bytes): a ferramenta de Olá predefinições tooa tamanho de script máximo de 512KB
3. Desative a geração de Id automática: Se toobe cada documento importada contém um campo de id, em seguida, selecionar esta opção pode aumentar o desempenho. Falta um campo de id exclusivo de documentos não serão importados.
4. Atualização existente documentos: Olá ferramenta predefinições toonot substituir os documentos existentes com conflitos de id. A seleção desta opção permitirá a substituir os documentos existentes com ID correspondentes. Esta funcionalidade é útil para migrações de dados agendada que atualizam documentos existentes.
5. Número de tentativas em caso de falha: Especifica Olá diversas vezes tooretry Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).
6. Intervalo de repetição: Especifica quanto toowait entre repetir Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).
7. Modo de ligação: Especifica toouse de modo de ligação de Olá com base de dados do Azure Cosmos. opções disponíveis Olá são DirectTcp, DirectHttps e Gateway. modos de ligação direta Olá são mais rápida, enquanto o modo de gateway de Olá é firewall mais amigável como o utiliza apenas a porta 443.

![Importação em volume de captura de ecrã da BD do Cosmos Azure opções avançadas](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> modo de tooconnection de predefinições de ferramenta DirectTcp de importação de Olá. Se ocorrerem problemas de firewall, alternar modo tooconnection Gateway, porque requer apenas a porta 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (sequencial de registo de importação)
importador de sequencial de registo de base de dados do Azure Cosmos Olá permite-lhe tooimport de qualquer uma das opções de origem disponível Olá numa base de registo ao registo. Poderá escolher esta opção se estiver a importar tooan coleção existente que atingiu a quota de procedimentos armazenados. Olá ferramenta suporta a importação tooa única coleção de base de dados do Azure Cosmos (partição única e várias partição), bem como a importação em dados estão particionados em várias coleções de partição única e/ou partição multi da BD do Cosmos do Azure. Para obter mais informações sobre a criação de partições de dados, consulte [divisão em partições e o dimensionamento do BD Azure Cosmos](partition-data.md).

![Opções de importação de registos sequencial de BD do Cosmos captura de ecrã do Azure](./media/import-data/documentdbsequential.png)

formato de Olá do Olá cadeia de ligação de base de dados do Azure Cosmos é:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Olá cadeia de ligação de conta de base de dados do Azure Cosmos pode ser obtido a partir do painel de chaves de Olá de Olá portal do Azure, conforme descrito em [como toomanage uma conta de base de dados do Azure Cosmos](manage-account.md); no entanto, o nome de Olá da base de dados de Olá tem toohello toobe anexado cadeia de ligação no Olá seguinte formato:

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Utilize Olá verifique comando tooensure que Olá instância de base de dados do Azure Cosmos especificada no campo de cadeia de ligação de Olá pode ser acedido.
> 
> 

tooimport tooa única coleção, introduza o nome de Olá de Olá coleção toowhich dados serão importados e clique no botão Adicionar de Olá. tooimport toomultiple coleções, introduza o nome de cada coleção individualmente ou utilizar Olá seguindo a sintaxe toospecify várias coleções: *collection_prefix*[iniciar índice - índice de fim]. Ao especificar várias coleções através da sintaxe acima mencionados Olá, tenha em atenção Olá seguinte:

1. São suportados apenas número inteiro intervalo padrões de nome. Por exemplo, especificar a coleção [0-3] irá produzir Olá seguintes coleções: collection0, collection1, collection2, collection3.
2. Pode utilizar uma sintaxe abreviada: recolha [3] irá emitir o mesmo conjunto de coleções mencionado no passo 1.
3. Pode ser fornecida mais do que uma substituição. Por exemplo, a coleção [0-1], [0-9] irá gerar 20 nomes de colecção com líderes zeros (collection01,.. 02,... 03).

Depois de Olá coleção nomes foram especificadas, escolhe o débito pretendido Olá Olá collection(s) (400 RUs too250 000 RUs). Para melhor desempenho de importação, escolha um maior débito. Para obter mais informações sobre os níveis de desempenho, consulte [níveis de desempenho na base de dados do Azure Cosmos](performance-levels.md). Importar qualquer toocollections com débito > 10 000 RUs necessitarão de uma chave de partição. Se optar por toohave mais do que 250 000 RUs, terá de toofile um pedido no toohave portal Olá aumenta a sua conta.

> [!NOTE]
> definição de débito de Olá só se aplica toocollection criação. Se Olá especificado coleção já existe, o débito não será modificado.
> 
> 

Quando importar coleções toomultiple, a ferramenta de importação de Olá suporta fragmentação de hash com base. Neste cenário, especifique a propriedade de documento Olá desejar toouse como Olá chave de partição (se a chave de partição for deixada em branco, documentos será a aleatoriamente em coleções de destino Olá).

Opcionalmente, pode especificar o campo na origem de importação de Olá deve ser utilizado como Olá propriedade de id do documento de base de dados do Azure Cosmos durante a importação de Olá (tenha em atenção que se documentos não contêm esta propriedade, em seguida, Olá importação ferramenta irá gerar um GUID como valor de propriedade de id de Olá).

Existem várias opções avançadas de disponíveis durante a importação. Em primeiro lugar, ao importar os tipos de data (por exemplo, a partir de SQL Server ou o MongoDB), pode escolher entre três opções de importação:

 ![Opções de importação do BD do Cosmos captura de ecrã do Azure data hora](./media/import-data/datetimeoptions.png)

* Cadeia: Manter como um valor de cadeia
* Época: Manter como um valor de número de época
* Ambas: Manter a cadeia e valores numéricos época. Esta opção irá criar um subdocument, por exemplo: "date_joined": {"Valor": "2013-10-21T21:17:25.2410000Z", "época": 1382390245}

Olá Azure Cosmos DB - importador sequencial de registo tem o seguinte de Olá adicionais opções avançadas:

1. Número de pedidos paralelos: ferramenta Olá predefinições pedidos paralelas too2. Se Olá documentos toobe importado é pequeno, considere aumentar o número de Olá de pedidos paralelos. Tenha em atenção que o se este número é gerado muito, Olá importação pode ter a limitação.
2. Desative a geração de Id automática: Se toobe cada documento importada contém um campo de id, em seguida, selecionar esta opção pode aumentar o desempenho. Falta um campo de id exclusivo de documentos não serão importados.
3. Atualização existente documentos: Olá ferramenta predefinições toonot substituir os documentos existentes com conflitos de id. A seleção desta opção permitirá a substituir os documentos existentes com ID correspondentes. Esta funcionalidade é útil para migrações de dados agendada que atualizam documentos existentes.
4. Número de tentativas em caso de falha: Especifica Olá diversas vezes tooretry Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).
5. Intervalo de repetição: Especifica quanto toowait entre repetir Olá ligação tooAzure Cosmos DB em caso de falhas transitórias (por exemplo, interrupção de conectividade de rede).
6. Modo de ligação: Especifica toouse de modo de ligação de Olá com base de dados do Azure Cosmos. opções disponíveis Olá são DirectTcp, DirectHttps e Gateway. modos de ligação direta Olá são mais rápida, enquanto o modo de gateway de Olá é firewall mais amigável como o utiliza apenas a porta 443.

![Importação de registo sequencial de captura de ecrã da BD do Cosmos Azure opções avançadas](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> modo de tooconnection de predefinições de ferramenta DirectTcp de importação de Olá. Se ocorrerem problemas de firewall, alternar modo tooconnection Gateway, porque requer apenas a porta 443.
> 
> 

## <a id="IndexingPolicy"></a>Especificar uma política de indexação ao criar a base de dados do Azure Cosmos coleções
Ao permitir a migração de Olá coleções de toocreate ferramenta durante a importação, pode especificar a política de indexação Olá de coleções de Olá. No Olá avançadas secção Opções de importação de em massa de BD do Azure Cosmos Olá e opções de registo do Azure Cosmos DB sequenciais, navegue até toohello secção de política de indexação.

![Captura de ecrã do Cosmos DB indexação política Azure opções avançadas](./media/import-data/indexingpolicy1.png)

Utilizar Olá opção da política de indexação avançada, pode selecionar um ficheiro de política de indexação, manualmente introduza uma política de indexação ou selecione um conjunto de modelos predefinidos (clicando com o botão direito na caixa de texto de política de indexação de Olá).

os modelos de política de Olá Olá ferramenta fornece são:

* A predefinição. Esta política é melhor quando estiver a efetuar consultas de igualdade em relação a cadeias e utilizar ORDER BY, intervalo e consultas de igualdade para números. Esta política tem uma tolerância de armazenamento de índice inferior ao intervalo.
* Intervalo. Esta política é melhor que utilizar consultas de ORDER BY, intervalo e igualdade no ambos números e scripts. Esta política tem uma tolerância de armazenamento de índice mais alta que predefinido ou Hash.

![Captura de ecrã do Cosmos DB indexação política Azure opções avançadas](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> Se não especificar uma política de indexação, em seguida, Olá predefinido política será aplicada. Para obter mais informações sobre as políticas de indexação, consulte [Azure Cosmos DB indexação políticas](indexing-policies.md).
> 
> 

## <a name="export-toojson-file"></a>Ficheiro de exportação de tooJSON
exportador de JSON de BD do Azure Cosmos Olá permite-lhe tooexport qualquer um dos Olá origem disponível opções tooa ficheiro JSON que contém uma matriz de documentos JSON. ferramenta de Olá irá processar a exportação de Olá para si, ou pode escolher o comando de migração do tooview Olá resultante e execute o comando de Olá por si. ficheiro JSON resultante Olá pode ser armazenado localmente ou no Blob storage do Azure.

![Opção de exportação de ficheiros local de captura de ecrã do Azure Cosmos DB JSON](./media/import-data/jsontarget.png)

![Opção de exportação de armazenamento de captura de ecrã do Blob do Azure Cosmos DB JSON do Azure](./media/import-data/jsontarget2.png)

Pode optar por Olá tooprettify resultante JSON, que irá aumentar o tamanho de Olá documento resultante Olá enquanto efetuar Olá contents humanos mais legível.

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a>Configuração avançada
No ecrã de configuração avançada de Olá, especifique a localização de Olá dos toowhich de ficheiro de registo de Olá que gostaria de quaisquer erros de escrita. Olá seguintes regras aplicam-se a página de toothis:

1. Se não for fornecido um nome de ficheiro, serão devolvidos todos os erros na página de resultados de Olá.
2. Se não for fornecido um nome de ficheiro sem um diretório, em seguida, o ficheiro de Olá será criado (ou substituído) no diretório de ambiente atual Olá.
3. Se selecionar um existente ficheiro, em seguida, o ficheiro de Olá serão substituídas, não existe nenhuma opção de acréscimo.

Em seguida, escolha se todos os toolog, crítico, ou não existem mensagens de erro. Por fim, decida frequência Olá na mensagem de transferência de ecrã será atualizada com o progresso da mesma.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>Confirme as definições de importação e a linha de comandos de vista
1. Depois de especificar as informações da origem, informações de destino e configuração avançada, reveja o resumo de migração de Olá e, opcionalmente, vista/copiar Olá resultante comandos de migração (copiar comandos de Olá é útil tooautomate operações de importação):
   
    ![Captura de ecrã do ecrã de resumo](./media/import-data/summary.png)
   
    ![Captura de ecrã do ecrã de resumo](./media/import-data/summarycommand.png)
2. Quando estiver satisfeito com as opções de origem e de destino, clique em **importação**. tempo decorrido de Olá, contagem transferida e informações da falha (se não fornecer um nome de ficheiro na configuração avançada Olá) irão atualizar como importar Olá está em curso. Depois de concluído, pode exportar resultados de Olá (por exemplo, toodeal com eventuais falhas de importação).
   
    ![Opção de exportação de captura de ecrã do Azure Cosmos DB JSON](./media/import-data/viewresults.png)
3. Também pode iniciar uma importação novo, mantendo Olá as definições existentes (por exemplo, escolha de informações, de origem e de destino de cadeia de ligação, etc.) ou repor todos os valores.
   
    ![Opção de exportação de captura de ecrã do Azure Cosmos DB JSON](./media/import-data/newimport.png)

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, fez seguinte Olá:

> [!div class="checklist"]
> * Instalar ferramenta de migração de dados de Olá
> * Dados importados a partir de origens de dados diferentes
> * Exportado a partir da base de dados do Azure Cosmos tooJSON

Agora pode prosseguir toohello próximo tutorial e obter informações como dados de tooquery utilizando a BD do Cosmos do Azure. 

> [!div class="nextstepaction"]
>[Como tooquery dados?](../cosmos-db/tutorial-query-documentdb.md)
