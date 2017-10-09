---
title: "As operações de indexador (API de REST do serviço de pesquisa do Azure: 2015-02-28-pré-visualização) | Microsoft Docs"
description: "As operações de indexador (API de REST do serviço de pesquisa do Azure: 2015-02-28-pré-visualização)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>As operações de indexador (API de REST do serviço de pesquisa do Azure: 2015-02-28-pré-visualização)
> [!NOTE]
> Este artigo descreve indexadores na Olá [API de REST de pré-visualização 2015-02-28](search-api-2015-02-28-preview.md). Esta versão de API adiciona versões de pré-visualização do indexador de Blob Storage do Azure com a extração do documento e indexador Table Storage do Azure, para além de outros melhoramentos. Olá API também suporta geralmente disponíveis indexadores (DG), incluindo indexadores para a SQL Database do Azure, SQL Server em VMs do Azure e Azure Cosmos DB.
> 
> 

## <a name="overview"></a>Descrição geral
A pesquisa do Azure pode ser integrado diretamente algumas origens de dados comum, remover Olá necessidade toowrite código tooindex os dados. tooset se esta cópia de segurança, pode chamar Olá API da Azure Search toocreate e gerir **indexadores** e **origens de dados**. 

Um **indexador** é um recurso que liga as origens de dados com os índices de pesquisa de destino. Um indexador é utilizado na Olá seguintes formas: 

* Efetue uma cópia única do Olá dados toopopulate um índice.
* Um índice com as alterações da origem de dados de Olá com base numa agenda de sincronização. agenda de Olá faz parte da definição de indexador Olá.
* Invocar a pedido tooupdate um índice conforme necessário. 

Um **indexador** é útil quando pretender que o índice de tooan atualizações regulares. Pode configurar uma agenda de inline como parte da definição de um indexador ou executá-la a pedido utilizando [executar o indexador](#RunIndexer). 

A **origem de dados** Especifica os dados que precisam de toobe indexada, credenciais tooaccess Olá dados e políticas tooenable da Azure Search tooefficiently identificar as alterações nos dados de Olá (tais como modificadas ou eliminadas linhas numa tabela da base de dados). Está definido como um recurso independente para que possa ser utilizado por vários indexadores.

Olá, as seguintes origens de dados atualmente é suportada:

* **Base de dados SQL do Azure** e **SQL Server em VMs do Azure**. Para uma passagem de destino, consulte [neste artigo](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Azure Cosmos DB**. Para uma passagem de destino, consulte [neste artigo](search-howto-index-documentdb.md). 
* **Armazenamento de Blobs do Azure**, incluindo formatos de documento seguinte Olá: ficheiros PDF, Microsoft Office (DOCX/DOC, XSLX/XLS, PPTX/PPT, tarifas de mensagens), HTML, XML, ZIP e texto simples (incluindo JSON). Para uma passagem de destino, consulte [neste artigo](search-howto-indexing-azure-blob-storage.md).
* **Table Storage do Azure**. Para uma passagem de destino, consulte [neste artigo](search-howto-indexing-azure-tables.md).

Iremos está a considerar adicionar suporte para origens de dados adicionais no Olá futura. toohelp-na atribuir prioridades a estas decisões, introduza os seus comentários no Olá [fórum de comentários da Azure Search](http://feedback.azure.com/forums/263029-azure-search).

Consulte [limites de serviço](search-limits-quotas-capacity.md) para máximo limites de recursos de origem de dados e tooindexer relacionados.

## <a name="typical-usage-flow"></a>Fluxo típico de utilização
Pode criar e gerir indexadores e origens de dados através de pedidos de HTTP simples (POST, GET, PUT, DELETE) em relação a um determinado `data source` ou `indexer` recursos.

Configurar a indexação automática, normalmente, é um processo de quatro passos:

1. Identifica a origem de dados de Olá que contém dados Olá que necessita de toobe indexada. Tenha em atenção que o Azure Search não podem suportar todos os tipos de dados de Olá presentes na sua origem de dados. Consulte [tipos de dados suportados](https://msdn.microsoft.com/library/azure/dn798938.aspx) para lista de Olá.
2. Crie um índice da Azure Search cuja esquema é compatível com a origem de dados.
3. Crie uma origem de dados de pesquisa do Azure, conforme descrito em [criar origem de dados](#CreateDataSource).
4. Criar um indexador de Azure Search, conforme descrito [criar indexador](#CreateIndexer).

Deve planear a criação de um indexador para cada combinação de origem de dados e índice de destino. Pode ter vários indexadores respetiva escrita no Olá mesmo índice e pode reutilizar Olá mesma origem de dados para vários indexadores. No entanto, um indexador só pode consumir uma origem de dados num momento e só pode escrever o índice único tooa. 

Depois de criar um indexador, pode obter o estado de execução utilizando Olá [obter estado do indexador](#GetIndexerStatus) operação. Também pode executar um indexador em qualquer altura (em vez de ou na adição toorunning-lo periodicamente com base numa agenda) utilizando Olá [executar o indexador](#RunIndexer) operação.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Criar origem de dados
Na Azure Search, uma origem de dados é utilizada com indexadores, fornecer informações de ligação de Olá atualização de dados do ad hoc ou agendada de um índice de destino. Pode criar uma nova origem de dados dentro de um serviço da Azure Search utilizando um pedido POST de HTTP.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Em alternativa, pode utilizar PUT e especificar o nome de origem de dados de Olá no Olá URI. Se a origem de dados de Olá não existir, será criado.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> Olá número máximo permitido de origens de dados varia consoante o escalão de preço. serviço gratuito Olá permite configurar origens de dados de too3. O serviço padrão permite 50 origens de dados. Consulte [limites de serviço](search-limits-quotas-capacity.md) para obter mais detalhes.
> 
> 

**Pedido**

HTTPS é necessário para todos os pedidos de serviço. Olá **criar origem de dados** pedido pode ser construído com um método POST ou PUT. Quando utilizar POST, tem de fornecer um nome de origem de dados no corpo do pedido de Olá, juntamente com a definição de origem de dados de Olá. Com PUT, o nome Olá faz parte do URL de Olá. Se a origem de dados de Olá não existir, será criado. Se já existir, é atualizado toohello nova definição. 

nome da origem de dados Olá tem de ter minúsculas, começar com uma letra ou número, ter nenhum barras ou pontos e de ter menos de 128 carateres. Depois de iniciar o nome da origem de dados Olá com uma letra ou número, rest Olá do nome de Olá pode incluir qualquer letra, o número e travessões, desde que os traços Olá não estão consecutivos. Consulte [regras de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx) para obter mais detalhes.

Olá `api-version` é necessária. a versão atual do Olá `2015-02-28`.

**Cabeçalhos de pedido**

Olá lista a seguir descreve Olá necessário e cabeçalhos de pedido opcional. 

* `Content-Type`: Necessário. Defina esta opção demasiado`application/json`
* `api-key`: Necessário. Olá `api-key` é utilizado tooauthenticate Olá pedido tooyour serviço de pesquisa. É um valor de cadeia, o serviço tooyour exclusivo. Olá **criar origem de dados** pedido tem de incluir um `api-key` cabeçalho definir a chave de administrador tooyour (como chave de consulta tooa oposição ao). 

Também terá de Olá serviço nome tooconstruct Olá URL do pedido. Pode obter o nome de serviço Olá e `api-key` a partir do seu dashboard de serviço no Olá [Portal do Azure](https://portal.azure.com/). Consulte [criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) para obter ajuda na navegação página.

<a name="CreateDataSourceRequestSyntax"></a>
**Sintaxe de corpo do pedido**

corpo de Olá de pedido de Olá contém uma definição de origem de dados, que inclui o tipo de origem de dados de Olá, dados de Olá tooread de credenciais, bem como uma deteção de alteração de dados opcionais e deteção de eliminação de dados políticas que são utilizado tooefficiently identificam alterado ou dados eliminados na origem de dados de Olá quando utilizado com um indexador periodicamente agendada. 

sintaxe de Olá para structuring payload de pedido de Olá é a seguinte. Um exemplo de pedido é fornecido mais neste tópico.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

O pedido contém Olá seguintes propriedades: 

* `name`: Necessário. nome de Olá Olá da origem de dados. Um nome de origem de dados pode apenas conter letras minúsculas, dígitos ou traços, não é possível iniciar ou terminar com travessões e carateres de too128 limitado.
* `description`: Uma descrição opcional. 
* `type`: Necessário. Tem de ser um dos tipos de origens de dados de Olá suportado:
  * `azuresql`-Base de dados SQL as do azure ou SQL Server em VMs do Azure
  * `documentdb`-BD do Cosmos as do azure
  * `azureblob`-Armazenamento de BLOBs azure
  * `azuretable`-Table Storage as do azure
* `credentials`:
  * Olá necessário `connectionString` propriedade especifica a cadeia de ligação de Olá Olá origem de dados. formato de Olá Olá da cadeia de ligação depende do tipo de origem de dados de Olá: 
    * Para o Azure SQL, esta é a cadeia de ligação do SQL Server de Olá habitual. Se estiver a utilizar a cadeia de ligação do Olá tooretrieve portal do Azure Olá, utilize Olá `ADO.NET connection string` opção.
    * Para a base de dados do Azure Cosmos, cadeia de ligação de Olá tem de constar Olá seguinte formato: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Todos os valores de Olá são necessários. Pode encontrá-los no Olá [portal do Azure](https://portal.azure.com/).  
    * Para o Blob do Azure e o Table Storage, o que é cadeia de ligação da conta de armazenamento de Olá. formato de Olá é descrito [aqui](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). Protocolo de ponto final HTTPS é necessário.  
* `container`, necessário: Especifica Olá dados tooindex utilizando Olá `name` e `query` propriedades: 
  * `name`, necessário:
    * SQL do Azure: Especifica Olá tabela ou vista. Pode utilizar nomes qualificados de esquema, tal como `[dbo].[mytable]`.
    * O DocumentDB: Especifica a coleção de Olá. 
    * Armazenamento de Blobs do Azure: Especifica o contentor de armazenamento Olá.
    * Table Storage do Azure: Especifica o nome de Olá da tabela de Olá. 
  * `query`, opcional:
    * O DocumentDB: permite-lhe toospecify uma consulta que flattens um esquema de documentos JSON arbitrário para um esquema simples que pode índice da Azure Search.  
    * Armazenamento de Blobs do Azure: permite-lhe toospecify uma pasta dentro do contentor do blob Olá virtual. Por exemplo, para o caminho do blob `mycontainer/documents/blob.pdf`, `documents` pode ser utilizada como pasta virtual Olá.
    * Table Storage do Azure: permite-lhe toospecify uma consulta que filtros Olá conjunto de toobe linhas importado.
    * SQL do Azure: a consulta não é suportada. Se precisar desta funcionalidade, votar para [este sugestão](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* Olá opcional `dataChangeDetectionPolicy` e `dataDeletionDetectionPolicy` propriedades são descritas abaixo.

<a name="DataChangeDetectionPolicies"></a>
**Políticas de deteção de alteração de dados**

objetivo Olá de um dado de alterar a política de deteção é tooefficiently identificar itens de dados alterados. Políticas suportadas variam com base no tipo de origem de dados de Olá. Secções abaixo descrevem cada política. 

***Política de deteção de alteração marca d'água alta*** 

Utilize esta política quando a origem de dados contém uma coluna ou uma propriedade que cumpra Olá os seguintes critérios:

* Inserções de todos os especificar um valor para a coluna de Olá. 
* Item de tooan todas as atualizações também alterar o valor de Olá da coluna de Olá. 
* valor de Olá desta coluna aumenta com cada alteração.
* As consultas que utilizam um filtro cláusula semelhante toohello seguinte `WHERE [High Water Mark Column] > [Current High Water Mark Value]` podem ser executadas de forma eficiente.

Por exemplo, quando utilizar origens de dados SQL do Azure, uma indexada `rowversion` coluna é candidatos ideais de Olá para utilização com a política de nível máximo de Olá. 

Esta política pode ser especificada da seguinte forma:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Quando utilizar a base de dados do Azure Cosmos origens de dados, tem de utilizar Olá `_ts` propriedade fornecida pelo Azure Cosmos DB. 

Quando utilizar automaticamente a origens de dados de Blobs do Azure, Azure Search utiliza uma marca d'água alta alterar a política de deteção com base no timestamp da última modificação de um blob; não precisa de toospecify tal política por si.   

***Política de deteção de alterações integrado do SQL***

Se a base de dados do SQL Server suporta [alterações](https://msdn.microsoft.com/library/bb933875.aspx), recomendamos que utilize SQL integrada Alterar controlo política. Esta política permite Olá mais eficiente alterações e permite que as linhas de tooidentify eliminado de pesquisa do Azure sem precisar de toohave uma coluna de explícita "eliminação de forma recuperável" no seu esquema.

Registo de alterações integrado é suportada ao iniciar com Olá seguintes versões do SQL Server da base de dados: 

* SQL Server 2008 R2, se estiver a utilizar o SQL Server em VMs do Azure.
* Azure SQL Database V12, se estiver a utilizar a SQL Database do Azure.  

Quando utilizar a política de SQL integrada controlo de alterações, não especifique uma política de deteção de eliminação de dados separada - esta política tem suporte incorporado para identificar o eliminar linhas. 

Esta política só pode ser utilizada com tabelas; não pode ser utilizado com vistas. É necessário tooenable alterações para a tabela de Olá que estiver a utilizar antes de poder utilizar esta política. Consulte [ativar e desativar o registo de alterações](https://msdn.microsoft.com/library/bb964713.aspx) para obter instruções.    

Quando structuring Olá **criar origem de dados** pedido SQL política de controlo de alterações integrado podem ser especificada da seguinte forma:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Políticas de deteção de eliminação de dados**

objetivo Olá uma política de deteção de eliminação de dados é tooefficiently identificar itens de dados eliminadas. Atualmente, a política de Olá só suportada é Olá `Soft Delete` política, que permite identificar eliminou itens com base no valor Olá um `soft delete` coluna ou propriedade da origem de dados de Olá. Esta política pode ser especificada da seguinte forma:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> São suportadas apenas colunas com valores de cadeia, número inteiro ou booleanos. Olá utilizado como valor `softDeleteMarkerValue` tem de ser uma cadeia, mesmo se a coluna correspondente Olá contém os números inteiros ou em booleanos. Por exemplo, se o valor de Olá que aparece na sua origem de dados for 1, utilizar `"1"` como Olá `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**Exemplos de corpo do pedido**

Se tenciona origem de dados de Olá toouse com um indexador que é executada com base numa agenda, este exemplo mostra como toospecify alteração e eliminação as políticas de Deteção: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Se tenciona apenas origem de dados de Olá toouse para uma única cópia dos dados de Olá, podem ser omitidas políticas Olá:

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Resposta**

Para um pedido com êxito: 201 criado. 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Atualizar a origem de dados
Pode atualizar uma origem de dados existente, utilizando um pedido HTTP PUT. Especifique o nome Olá tooupdate de origem de dados de Olá no URI do pedido de Olá:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Olá `api-version` é necessária. a versão atual do Olá `2015-02-28`. [Versões de API de pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn864560.aspx) tem detalhes e mais informações sobre versões alternativas.

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Pedido**

Olá sintaxe de corpo do pedido é Olá mesmos que para [criar origem de dados de pedidos](#CreateDataSourceRequestSyntax).

Algumas propriedades não não possível atualizar uma origem de dados existente. Por exemplo, não é possível alterar o tipo de Olá de uma origem de dados existente.  

Se não quiser a cadeia de ligação de Olá toochange para uma origem de dados existente, pode especificar Olá literal `<unchanged>` para a cadeia de ligação de Olá. Isto é útil em situações em que tem tooupdate uma origem de dados, mas não tem a cadeia de ligação do acesso prático toohello porque se trata de dados de segurança confidenciais.

**Resposta**

Para um pedido com êxito: 201 criado se uma nova origem de dados foi criado e 204 não conteúdo se uma origem de dados existente tiver sido atualizada.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Origens de dados de lista
Olá **origens de dados de lista** operação devolve uma lista de origens de dados de Olá no seu serviço da Azure Search. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. a versão atual do Olá `2015-02-28`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Para um pedido com êxito: 200 OK.

Eis um corpo de resposta de exemplo:

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

Tenha em atenção que pode filtrar resposta Olá baixo propriedades de Olá toojust que estiver interessado em. Por exemplo, se pretender que apenas uma lista de nomes de origem de dados, utilize Olá OData `$select` opção de consulta:

    GET /datasources?api-version=205-02-28&$select=name

Neste caso, resposta de Olá do Olá acima exemplo deverá aparecer da seguinte forma: 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Esta é uma largura de banda de toosave técnica útil se tiver um grande número de origens de dados no serviço de pesquisa.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Obter a origem de dados
Olá **obter a origem de dados** operação obtém a definição de origem de dados de Olá da Azure Search.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. a versão atual do Olá `2015-02-28`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

resposta Olá é semelhante tooexamples no [pedidos de exemplo da origem de dados criar](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Não defina Olá `Accept` cabeçalho de pedido demasiado`application/json;odata.metadata=none` quando chamar esta API como se o fizer, irá fazer com que `@odata.type` toobe atributo omitido da resposta Olá e não será capaz de toodifferentiate entre a alteração de dados e deteção de eliminação de dados políticas de diferentes tipos de mensagens em fila. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Eliminar a origem de dados
Olá **Eliminar origem de dados** operação remove uma origem de dados do serviço da Azure Search.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Se qualquer indexadores referenciem a origem de dados de Olá que está a eliminar, operação de eliminação de Olá ainda irá continuar. No entanto, essas indexadores irão transitar para um Estado de erro após a respetiva execução seguinte.  
> 
> 

Olá `api-version` é necessária. a versão atual do Olá `2015-02-28`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Código de estado: 204 conteúdo não é devolvido para uma resposta com êxito.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Criar indexador
Pode criar um indexador novo dentro de um serviço da Azure Search utilizando um pedido POST de HTTP.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Em alternativa, pode utilizar PUT e especificar o nome de origem de dados de Olá no Olá URI. Se a origem de dados de Olá não existir, será criado.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> número máximo de Olá de indexadores permitido varia consoante o escalão de preço. serviço gratuito Olá permite cópias de segurança too3 indexadores. O serviço padrão permite 50 indexadores. Consulte [limites de serviço](search-limits-quotas-capacity.md) para obter mais detalhes.
> 
> 

Olá `api-version` é necessária. a versão atual do Olá `2015-02-28`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

<a name="CreateIndexerRequestSyntax"></a>
**Sintaxe de corpo do pedido**

corpo de Olá de pedido de Olá contém uma definição de indexador que especifica a origem de dados de Olá e Olá de índice de destino para indexação, bem como indexação de agenda opcional e os parâmetros. 

sintaxe de Olá para structuring payload de pedido de Olá é a seguinte. Um exemplo de pedido é fornecido mais neste tópico.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Agendamento do indexador**

Um indexador, opcionalmente, pode especificar uma agenda. Se estiver presente uma agenda, indexador Olá é executada periodicamente de acordo com a agenda. Agenda tem Olá seguintes atributos:

* `interval`: Necessário. Um valor de duração que especifica um intervalo ou o período de indexador é executado. Olá menor permitido intervalo é de 5 minutos; Olá mais longo é um dia. Tem de ser formatado como um valor de "dayTimeDuration" XSD (um subconjunto restrito de um [duração ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) valor). Olá padrão para isto é: `"P[nD][T[nH][nM]]"`. Exemplos: `PT15M` para a cada 15 minutos, `PT2H` para cada 2 horas. 
* `startTime`: Necessário. Datetime de UTC quando o indexador Olá deve iniciar a execução. 

**Parâmetros do indexador**

Um indexador, opcionalmente, pode especificar vários parâmetros que afetam o respetivo comportamento. Todos os parâmetros de Olá são opcionais.  

* `maxFailedItems`: número de Olá de itens que pode falhar toobe indexados antes de um indexador é considerado uma falha. Predefinição é 0. São devolvidas informações sobre itens falhados por Olá [obter estado do indexador](#GetIndexerStatus) operação. 
* `maxFailedItemsPerBatch`: número de Olá de itens que pode falhar toobe indexados em cada lote antes de um indexador é considerado uma falha. Predefinição é 0.
* `base64EncodeKeys`: Especifica se pretende ou não as chaves de documento será com codificação base 64. A pesquisa do Azure impõe restrições de carateres que podem constar de uma chave de documento. No entanto, Olá valores existentes na sua origem de dados podem conter carateres inválidos. Se for necessário tooindex de valores, tais como chaves de documento, pode definir este sinalizador tootrue. Predefinição é `false`.
* `batchSize`: Especifica o número de Olá dos itens que são lidos a partir da origem de dados de Olá e indexada como um único lote do desempenho de tooimprove de ordem. predefinição de Olá depende do tipo de origem de dados de Olá: é 1000 para o SQL do Azure e a base de dados do Azure Cosmos e 10 para armazenamento de Blobs do Azure.

**Mapeamentos de campo**

Pode utilizar toomap de mapeamentos campo um nome de campo nome diferente para o campo tooa de origem de dados de Olá no índice de destino Olá. Por exemplo, considere uma tabela de origem com um campo `_id`. A pesquisa do Azure não permite um nome de campo começado por um caráter de sublinhado, pelo que deve ser mudar o nome de campo Olá. Isto pode ser feito utilizando Olá `fieldMappings` propriedade do indexador Olá da seguinte forma: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

Pode especificar mapeamentos campo: 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

Os nomes de campo de origem e de destino são sensível.

<a name="FieldMappingFunctions"></a>
***Campo mapeamento de funções***

Mapeamentos de campo também podem ser utilizados tootransform valores de campo de origem utilizando *mapeamento de funções*.

Apenas um desse função é atualmente suportada: `jsonArrayToStringCollection`. -Analisa um campo que contém uma cadeia formatada como uma matriz JSON para um campo de Collection(Edm.String) no índice de destino Olá. Destina-se para utilização com o indexador de SQL do Azure em particular, uma vez que o SQL Server não tem um tipo de dados de coleção nativo. Podem ser utilizada da seguinte forma: 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Por exemplo, se hello o campo de origem contém uma cadeia Olá `["red", "white", "blue"]`, em seguida, no campo de destino Olá do tipo `Collection(Edm.String)` irá ser preenchida com valores de Olá três `"red"`, `"white"` e `"blue"`.

Tenha em atenção que Olá `targetFieldName` propriedade é opcional; se for deixado, Olá `sourceFieldName` valor é utilizado. 

<a name="CreateIndexerRequestExamples"></a>
**Exemplos de corpo do pedido**

Olá exemplo seguinte cria um indexador que copia dados da tabela de Olá referenciada pela Olá `ordersds` toohello da origem de dados `orders` índice com base numa agenda que inicia no 1 de Janeiro de 2015 UTC e é executada hora a hora. Cada invocação de indexador será bem sucedida se não mais de 5 itens falharem toobe indexado em cada lote e não mais do que 10 itens falharem toobe indexada no total. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Resposta**

201 criado para um pedido com êxito.

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Atualizar o indexador
Pode atualizar um indexador existente utilizando um pedido HTTP PUT. Especifique o nome Olá Olá indexador tooupdate no URI do pedido de Olá:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Olá `api-version` é necessária. a versão atual do Olá `2015-02-28`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Pedido**

Olá sintaxe de corpo do pedido é Olá mesmos que para [indexador criar pedidos](#CreateIndexerRequestSyntax).

**Resposta**

Para um pedido com êxito: 201 criado se um indexador nova foi criada e 204 não conteúdo se tiver sido atualizado um indexador existente.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Indexadores de lista
Olá **lista indexadores** operação devolve a lista de Olá de indexadores no serviço da Azure Search. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Olá `api-version` é necessária. versão de pré-visualização Olá é `2015-02-28-Preview`. [Controlo de versões de pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn864560.aspx) tem detalhes e mais informações sobre versões alternativas.

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Para um pedido com êxito: 200 OK.

Eis um corpo de resposta de exemplo:

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

Tenha em atenção que pode filtrar resposta Olá baixo propriedades de Olá toojust que estiver interessado em. Por exemplo, se pretender que apenas uma lista de nomes de indexador, utilizar Olá OData `$select` opção de consulta:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

Neste caso, resposta de Olá do Olá acima exemplo deverá aparecer da seguinte forma: 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Esta é uma largura de banda de toosave técnica útil se tiver um grande número de indexadores no serviço de pesquisa.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Obter o indexador
Olá **obter indexador** operação obtém a definição de indexador Olá da Azure Search.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. versão de pré-visualização Olá é `2015-02-28-Preview`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Código de estado: 200 OK é devolvido para uma resposta com êxito.

resposta Olá é semelhante tooexamples no [indexador criar pedidos de exemplo](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Eliminar o indexador
Olá **eliminar o indexador** operação remove um indexador do serviço da Azure Search.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Quando um indexador é eliminado, execuções de indexador Olá em curso a essa hora serão executado toocompletion, mas não existem execuções mais serão agendadas. Não foi encontrado toouse tentativas que um indexador inexistente irá resultar num código de estado HTTP 404. 

Olá `api-version` é necessária. versão de pré-visualização Olá é `2015-02-28-Preview`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Código de estado: 204 conteúdo não é devolvido para uma resposta com êxito.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>Executar o indexador
Na adição toorunning periodicamente com base numa agenda, também é possível invocar um indexador a pedido através de Olá **executar o indexador** operação: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. versão de pré-visualização Olá é `2015-02-28-Preview`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Código de estado: 202 aceites é devolvido para uma resposta com êxito.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>Obter o estado do indexador
Olá **obter estado do indexador** operação obtém Olá atual estado e a execução do histórico de um indexador: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Olá `api-version` é necessária. versão de pré-visualização Olá é `2015-02-28-Preview`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Código de estado: 200 OK para uma resposta com êxito.

corpo da resposta Olá contém informações sobre o estado de funcionamento geral do indexador, invocação de indexador último Olá, bem como o histórico de Olá de invocações de indexador recentes (caso exista). 

Um corpo de resposta de exemplo tem o seguinte aspeto: 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**Estado do indexador**

Estado de indexador pode ser um dos seguintes valores de Olá:

* `running`indica que esse indexador Olá está a funcionar normalmente. Tenha em atenção que algumas das execuções de indexador Olá ainda poderão falhar, pelo que é um Olá de toocheck boa ideia `lastResult` propriedade bem. 
* `error`indica que esse indexador Olá teve um erro que não pode ser corrigido sem qualquer intervenção humana. Por exemplo, as credenciais de origem de dados de Olá podem ter expirado ou esquema Olá Olá da origem de dados ou do índice de destino Olá foi alterada numa quebra forma. 

**Resultado de execução do indexador**

Um resultado de execução do indexador contém informações sobre uma execução do indexador único. resultados mais recente Olá é anexados como Olá `lastResult` propriedade de estado de indexador Olá. Outros resultados recentes, se estiver presente, são devolvidos como Olá `executionHistory` propriedade de estado de indexador Olá. 

Resultado da execução de indexador contém Olá seguintes propriedades: 

* `status`: Olá estado de uma execução. Consulte [estado de execução do indexador](#IndexerExecutionStatus) abaixo para obter mais detalhes. 
* `errorMessage`: mensagem de erro para uma execução falhou. 
* `startTime`: tempo Olá em UTC quando iniciou a execução.
* `endTime`: tempo Olá em UTC quando terminou a execução. Este valor não é definido se a execução de Olá ainda está em curso.
* `errors`: uma matriz de erros ao nível do item, se aplicável. Cada entrada contém uma chave de documento (`key` propriedade) e uma mensagem de erro (`errorMessage` propriedade). 
* `itemsProcessed`: Olá número de itens de origem de dados (por exemplo, linhas de tabela) que Olá indexador tentada tooindex durante a execução. 
* `itemsFailed`: Olá número de itens que falhou durante a execução.  
* `initialTrackingState`: sempre `null` para execução do indexador primeiro hello, ou se os dados de Olá alterar a política de controlo não está ativado na origem de dados de Olá utilizada. Se tal política estiver ativada, nas execuções subsequentes, este valor indica Olá primeiro (mais baixa) registo de alterações valor processado por esta execução. 
* `finalTrackingState`: sempre `null` se dados Olá alterar a política de controlo não está ativado na origem de dados de Olá utilizada. Caso contrário, indica Olá mais recente (mais alta) registo de alterações valor processada com êxito, a execução. 

<a name="IndexerExecutionStatus"></a>
**Estado de execução do indexador**

Estado de execução do indexador captura o estado de Olá da execução do indexador único. Pode ter Olá os seguintes valores:

* `success`indica que a execução do indexador de Olá foi concluída com êxito.
* `inProgress`indica que a execução do indexador de Olá está em curso. 
* `transientFailure`indica que um indexador falha na execução. Consulte `errorMessage` propriedade para obter mais detalhes. Falha de Olá pode ou não precisar de intervenção do homem toofix - por exemplo, corrigir uma incompatibilidade de esquema entre a origem de dados de Olá e o índice de destino Olá necessita de ação do utilizador, enquanto um período de indisponibilidade de origem de dados temporário não. Invocações de indexador continuará por agenda, se estiver presente. 
* `persistentFailure`indica que esse indexador Olá falha de uma forma que requer intervenção do homem. Parar de execuções do indexador agendada. Depois de corrigir o problema de Olá, utilize execuções do repor o indexador API toorestart Olá agendada. 
* `reset`indica que esse indexador Olá foi reposta por um tooReset de chamada de API de indexador (ver abaixo). 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Repor o indexador
Olá **repor o indexador** operação repõe o Estado associado indexador Olá do registo de alterações de Olá. Isto permite-lhe tootrigger da-zero reindexação (por exemplo, se tiver alterado o esquema de origem de dados) ou a política de deteção de toochange Olá dados alteração para uma origem de dados associada indexador Olá.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. versão de pré-visualização Olá é `2015-02-28-Preview`. 

Olá `api-key` tem de ser uma chave de administração (como chave de consulta tooa oposição ao). Consulte a secção autenticação toohello [API de REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais informações sobre chaves. [Criar um serviço de pesquisa no portal de Olá](search-create-service-portal.md) explica como o URL do serviço tooget Olá e propriedades chave utilizada no pedido Olá.

**Resposta**

Código de estado: 204 não conteúdo de uma resposta com êxito.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>Mapeamento entre tipos de dados do SQL Server e os tipos de dados de pesquisa do Azure
<table style="font-size:12">
<tr>
<td>Tipo de dados do SQL Server</td>    
<td>Permitido tipos de campo de índice de destino</td>
<td>Notas</td>
</tr>
<tr>
<td>bits</td>
<td>Boolean, EDM</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>EDM Edm.Int32, Edm.Int64,</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, EDM</td>
<td></td>
</tr>
<tr>
<td>número de vírgula flutuante real,</td>
<td>Edm.Double, EDM</td>
<td></td>
</tr>
<tr>
<td>em smallmoney, dinheiro<br>Decimal<br>um valor numérico
</td>
<td>Edm.String</td>
<td>A pesquisa do Azure não suporta a conversão de tipos decimais numa Edm.Double porque este perderia precisão
</td>
</tr>
<tr>
<td>char, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Coleção (Edm.String)</td>
<td>Consulte [campo mapeamento de funções](#FieldMappingFunctions) neste documento para obter detalhes sobre como tootransform uma coluna de cadeia para um Collection(Edm.String)</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, EDM</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Geografia</td>
<td>Edm.GeographyPoint</td>
<td>Apenas as instâncias de geografia de tipo de ponto de 4326 SRID (que é a predefinição de Olá) são suportadas</td>
</tr>
<tr>
<td>ROWVERSION</td>
<td>N/D</td>
<td>Colunas de versão de linha não podem ser armazenadas no índice de pesquisa de Olá, mas podem ser utilizadas para controlo de alterações</td>
</tr>
<tr>
<td>tempo, timespan<br>Binary, varbinary, imagem,<br>XML, geometria, os tipos CLR</td>
<td>N/D</td>
<td>Não suportado</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapeamento entre tipos de dados JSON e tipos de dados de pesquisa do Azure
<table style="font-size:12">
<tr>
<td>Tipo de dados JSON</td>    
<td>Permitido tipos de campo de índice de destino</td>
<td>Notas</td>
</tr>
<tr>
<td>bool</td>
<td>Boolean, EDM</td>
<td></td>
</tr>
<tr>
<td>Número inteiro</td>
<td>EDM Edm.Int32, Edm.Int64,</td>
<td></td>
</tr>
<tr>
<td>Números de vírgula flutuante</td>
<td>Edm.Double, EDM</td>
<td></td>
</tr>
<tr>
<td>Cadeia</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>tipos de matrizes de primitivos, por exemplo, ["a", "b", "c"]</td>
<td>Coleção (Edm.String)</td>
<td></td>
</tr>
<tr>
<td>Cadeias de aspeto de datas</td>
<td>Edm.DateTimeOffset, EDM</td>
<td></td>
</tr>
<tr>
<td>Objetos de ponto de GeoJSON</td>
<td>Edm.GeographyPoint</td>
<td>GeoJSON pontos são objetos JSON no Olá seguinte formato: {"type": "Ponto", "coordenadas": [lat longo]} </td>
</tr>
<tr>
<td>Outros objetos JSON</td>
<td>N/D</td>
<td>Não suportado; A pesquisa do Azure atualmente suporta apenas tipos primitivos e coleções de cadeia</td>
</tr>
</table>
