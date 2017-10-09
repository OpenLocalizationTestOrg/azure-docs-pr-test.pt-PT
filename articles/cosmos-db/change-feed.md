---
title: "suporte de feed aaaWorking com alteração de Olá do BD Azure Cosmos | Microsoft Docs"
description: "Utilização do Azure Cosmos DB alterar suporte feed tootrack alterações em documentos e efetuar com base em eventos processamento como acionadores e manter os sistemas de caches e análise atualizado."
keywords: "Alteração do feed"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Trabalhar com suporte de feed de alteração de Olá do BD Azure Cosmos
[BD do Azure do Cosmos](../cosmos-db/introduction.md) são um fast e flexível globalmente replicados serviço de base de dados que é utilizado para armazenar dados de elevado volume transacionais e operacionais com latência previsível dígito milissegundo para leituras e escritas. Isto torna adequada para IoT, revenda, jogos e aplicações de registo operacional. É um padrão de conceção comuns nestas aplicações tootrack alterações efetuadas tooAzure Cosmos DB dados e atualizar as vistas materializadas, efetuar a análise em tempo real, o armazenamento de dados de arquivo toocold e notificações de Acionador em determinados eventos com base nestas alterações. Olá **alteração feed suporte** do BD Azure Cosmos permite-lhe toobuild eficientes e dimensionáveis soluções para cada um desses padrões.

Com alteração de feed de suporte, base de dados do Azure Cosmos fornece uma lista ordenada de documentos dentro de uma coleção de base de dados do Azure Cosmos por ordem de Olá em que foram modificadas. Este feed pode ser utilizado toolisten para modificações toodata dentro da coleção de Olá e realizar ações tais como:

* Acionar um tooan chamada API, quando um documento é inserido ou modificado
* Efetuar o processamento em tempo real (fluxo) sobre atualizações
* Sincronizar dados com uma cache, o motor de busca ou do armazém de dados

Alterações do BD Azure Cosmos são mantidas e podem ser processadas de forma assíncrona e distribuídas por um ou mais consumidores para processamento paralelo. Vamos ver Olá APIs para o feed de alteração e como pode utilizá-los toobuild dimensionável, aplicações em tempo real. Este artigo mostra como toowork com base de dados do Azure Cosmos alterar feed e Olá API do DocumentDB. 

![Utilizar base de dados do Azure Cosmos alteração feed toopower de análise em tempo real e condicionada por eventos cenários de computação](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Alteração de suporte de feed só é fornecida para Olá DocumentDB API nesta altura; Olá Graph API e a API de tabela não são atualmente suportadas.

## <a name="use-cases-and-scenarios"></a>Cenários e casos de utilização
Alteração feed permite processamento eficiente de grandes conjuntos de dados com um grande volume de escritas e oferece uma tooidentify de conjuntos de dados completo tooquerying alternativo que tenha sido alterado. Por exemplo, pode efetuar Olá eficazmente os seguintes tarefas:

* Atualize uma cache, o índice de pesquisa ou um armazém de dados com dados armazenados na base de dados do Azure Cosmos.
* Implementar dados ao nível da aplicação e o arquivo de camadas, ou seja, armazenar "dados" na base de dados do Azure Cosmos e expira "dados amovíveis" demasiado[Blob Storage do Azure](../storage/common/storage-introduction.md) ou [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).
* Implementar a análise de lote em dados utilizando [do Apache Hadoop](run-hadoop-with-hdinsight.md).
* Implementar [pipelines de lambda no Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) com base de dados do Azure Cosmos. BD do Cosmos do Azure fornece uma solução de bases de dados dimensionável que pode processar ingestão e consulta e implementa arquiteturas de lambda com TCO baixa. 
* Efetue zero tooanother migrações de tempo inferior a conta de base de dados do Azure Cosmos com um esquema de partições diferente.

**Lambda Pipelines com a BD do Cosmos do Azure para ingestão e a consulta:**

![Pipeline de lambda de BD do Cosmos com base do Azure para ingestão e consulta](./media/change-feed/lambda.png)

Pode utilizar a base de dados do Azure Cosmos tooreceive e armazenar dados de eventos de dispositivos, sensores, infraestrutura e de aplicações e processar estes eventos em tempo real com [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), ou [do Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

Dentro do seu [sem servidor](http://azure.com/serverless) web apps e móveis, pode controlar eventos como tootrigger de perfil, as preferências ou localização do cliente tooyour alterações determinadas ações, como o envio de push dispositivos tootheir de notificações utilizando [As funções do azure](../azure-functions/functions-bindings-documentdb.md) ou [serviços aplicacionais](https://azure.microsoft.com/services/app-service/). Se estiver a utilizar a base de dados do Azure Cosmos toobuild um jogo, por exemplo, pode utilizar alteração feed tooimplement leaderboards em tempo real com base no pontuações de jogos concluídas.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Como funciona o feed de alteração do BD Azure Cosmos
BD do Azure do Cosmos fornece Olá capacidade tooincrementally ler atualizações efetuadas tooan coleção da base de dados do Azure Cosmos. Este feed de alteração tem Olá seguintes propriedades:

* As alterações sejam persistentes na base de dados do Azure Cosmos e podem ser processadas de forma assíncrona.
* As alterações toodocuments dentro de uma coleção estão disponíveis imediatamente no feed de alteração de Olá.
* Cada documento de tooa alteração aparece exatamente uma vez no feed de alteração de Olá e clientes gerir os respetivos lógica de pontos de verificação. biblioteca de processador de feed de alteração de Olá fornece pontos de verificação automático e ", pelo menos, uma vez" semântica.
* Apenas alteração mais recente de Olá para um determinado documento está incluída no registo de alterações de Olá. Alterações intermédias poderão não estar disponíveis.
* Olá alteração feed é ordenada by order of modificação dentro de cada valor de chave de partição. Não há nenhuma ordem garantida entre os valores de chave de partição.
* As alterações podem ser sincronizadas a partir de qualquer ponto no tempo, ou seja, não existe nenhum período de retenção de dados fixa para o qual as alterações estão disponíveis.
* As alterações estão disponíveis em segmentos de intervalos de chaves de partição. Esta capacidade permite alterações de toobe de coleções de grandes dimensões processados em paralelo por vários consumidores/servidores.
* As aplicações podem o pedido de alteração vários feeds em simultâneo no Olá mesma coleção.

Feed de alteração da BD Cosmos do Azure está ativada por predefinição para todas as contas. Pode utilizar o [débito aprovisionado](request-units.md) na sua região de escrita ou qualquer [ler região](distribute-data-globally.md) tooread de Olá alterar feed, tal como qualquer outra operação da base de dados do Azure Cosmos. Olá alteração feed inclui as operações de atualização efetuadas toodocuments dentro da coleção de Olá e inserções. Pode capturar eliminações ao definir um sinalizador de "eliminar de forma recuperável" dentro os documentos em vez de eliminações. Em alternativa, pode definir um período de expiração finita para os documentos através de Olá [capacidade TTL](time-to-live.md), para o exemplo, 24 horas e a utilização Olá valor da propriedade toocapture elimina. Com esta solução, tem alterações tooprocess dentro de um intervalo de tempo mais curto que o período de expiração do Olá TTL. Olá alteração feed está disponível para cada intervalo de chave de partição dentro da coleção de documentos Olá e, por conseguinte, pode ser distribuído por um ou mais consumidores para processamento paralelo. 

![Feed de processamento distribuído de alteração de base de dados do Azure Cosmos](./media/change-feed/changefeedvisual.png)

Tem algumas opções como implementar uma alteração do feed no seu código de cliente. Olá secções que imediatamente a seguir descrevem como tooimplement Olá utilizando Olá API REST da Azure Cosmos DB de feed de alteração e Olá SDKs do DocumentDB. No entanto, para aplicações de .NET, recomendamos que utilize Olá novo [alteração feed biblioteca processador](#change-feed-processor) para eventos de processamento de Olá alteração feed como simplifica as alterações de leitura em partições e permite que vários threads a funcionar no paralelo. 

## <a id="rest-apis"></a>Trabalhar com Olá REST API e SDKs do DocumentDB
BD do Azure do Cosmos fornece elásticos contentores de armazenamento e débito chamado **coleções**. Os dados dentro de coleções são logicamente agrupados utilizando [chaves de partição](partition-data.md) para escalabilidade e desempenho. BD do Azure do Cosmos fornece diversas APIs para aceder a estes dados, incluindo a pesquisa por ID (leitura/Get), consulta e feeds de leitura (análises). Olá feed de alteração pode ser obtido ao preencher dois novos pedido cabeçalhos toohello DocumentDB `ReadDocumentFeed` API e podem ser processados em paralelo em intervalos de chaves de partição.

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
Vamos observe breve como ReadDocumentFeed funciona. BD do Azure do Cosmos suporta a leitura de um feed de documentos numa coleção através de Olá `ReadDocumentFeed` API. Por exemplo, hello pedido seguinte devolve uma página de documentos no interior Olá `serverlogs` coleção. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Os resultados podem ser limitados utilizando Olá `x-ms-max-item-count` cabeçalho e leituras podem ser retomado por voltar a submeter pedido Olá com um `x-ms-continuation` cabeçalho devolvido na resposta anterior Olá. Durante a execução de um único cliente, `ReadDocumentFeed` itera através de resultados em partições serialmente. 

**Série ler o feed do documento**

Também pode obter o feed Olá de documentos através de um dos Olá suportado [SDKs de BD do Azure Cosmos](documentdb-sdk-dotnet.md). Por exemplo, Olá seguinte fragmento mostra como toouse Olá [ReadDocumentFeedAsync método](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) no .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Execução distribuída do ReadDocumentFeed
Para coleções que contêm terabytes de dados ou mais, ou um grande volume de atualizações de inserção, execução de série do feed de leitura de um único computador cliente poderá não ser prática. Na ordem toosupport nestes cenários de macrodados, Azure Cosmos DB fornece APIs toodistribute `ReadDocumentFeed` chamadas de forma transparente entre vários cliente de leitores de consumidores. 

**Feed do documento de leitura distribuída**

tooprovide processamento dimensionável de alterações incrementais, Cosmos BD do Azure suporta um modelo de escalamento horizontal para alteração Olá feed API com base nos intervalos de chaves de partição.

* Pode obter uma lista de partição intervalos de chaves para uma coleção efetuar um `ReadPartitionKeyRanges` chamada. 
* Para cada intervalo de chave de partição, pode realizar uma `ReadDocumentFeed` tooread documentos com chaves de partição dentro desse intervalo.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Obter intervalos de chaves de partição para uma coleção
Pode obter intervalos de chaves de partição de Olá pelo requerente Olá `pkranges` recursos numa coleção. Por exemplo Olá pedido seguinte obtém Olá lista de intervalos de chaves de partição para Olá `serverlogs` coleção:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Este pedido devolve Olá resposta que contém metadados sobre intervalos de chaves de partição de Olá os seguintes:

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**Propriedades de intervalo de chaves de partição**: cada intervalo de chave de partição inclui as propriedades de metadados de Olá Olá a tabela seguinte:

<table>
    <tr>
        <th>Nome do cabeçalho</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>ID</td>
        <td>
            <p>ID de Olá de intervalo de chave de partição de Olá. Este é um ID exclusivo e estável dentro de cada coleção.</p>
            <p>Tem de ser utilizado no Olá seguir chamada tooread alterações ao intervalo de chaves de partição.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>valor de hash de chave de partição máximo de Olá para o intervalo de chave de partição de Olá. Para utilização interna.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>valor de hash de chave de partição mínima de Olá para o intervalo de chaves de partição do Olá. Para utilização interna.</td>
    </tr>       
</table>

Isto pode ser feito utilizando um dos Olá suportado [SDKs de BD do Azure Cosmos](documentdb-sdk-dotnet.md). Por exemplo, hello fragmento seguinte mostra como a chave de partição tooretrieve intervalos no .NET utilizando Olá [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) método.

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

BD do Cosmos do Azure suporta a obtenção de documentos por intervalo de chaves de partição, definição Olá opcional `x-ms-documentdb-partitionkeyrangeid` cabeçalho. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Efetuar uma ReadDocumentFeed incremental
ReadDocumentFeed suporta Olá cenários/tarefas para processamento incremental das alterações de coleções de base de dados do Azure Cosmos os seguintes:

* Ler todas as alterações toodocuments desde o início de Olá, ou seja, da criação de coleção.
* Ler todas as alterações toofuture atualizações toodocuments da hora atual, ou todas as alterações desde um período de tempo de utilizador especificado.
* Ler todas as alterações toodocuments a partir de uma versão lógica da coleção de Olá (ETag). Pode os consumidores com base no Olá devolvido ETag de pedidos de leitura feed incrementais de ponto de verificação.

alterações de Olá incluem toodocuments inserções e atualizações. Elimina toocapture, tem de utilizar uma propriedade de "eliminação de forma recuperável" dentro os documentos ou utilizar Olá [propriedade incorporada do TTL](time-to-live.md) toosignal uma eliminação pendente no Olá alterar feed.

Olá seguinte tabela apresenta uma lista de Olá [pedido](/rest/api/documentdb/common-documentdb-rest-request-headers.md) e [cabeçalhos de resposta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) para operações de ReadDocumentFeed.

**Cabeçalhos de pedido para incremental ReadDocumentFeed**:

<table>
    <tr>
        <th>Nome do cabeçalho</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>A MI</td>
        <td>Tem de ser definido demasiado "Incremental feed", ou omitido caso contrário</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Não existe um cabeçalho: devolve todas as alterações de Olá a partir da (criação de coleção)</p>
            <p>"*": devolve todas as novas alterações toodata dentro da coleção de Olá</p>         
            <p>&lt;ETag&gt;: Se definir tooa coleção ETag, devolve todas as alterações efetuadas desde que timestamp lógica</p>
        </td>
    </tr>
    <tr>    
        <td>Se-modificado-Since</td> 
        <td>Formato de hora RFC 1123; ignorado se If-None-Match foi especificado</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>ID de intervalo de chaves de partição de Olá para a leitura de dados.</td>
    </tr>
</table>

**Cabeçalhos de resposta para incremental ReadDocumentFeed**:

<table> <tr>
        <th>Nome do cabeçalho</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>ETag</td>
        <td>
            <p>Olá lógica número de sequência (LSN) da última documento devolvido na resposta Olá.</p>
            <p>É possível retomar incremental ReadDocumentFeed ao voltar a submeter este valor na If-None-Match.</p>
        </td>
    </tr>
</table>

Eis um tooreturn de pedido de exemplo todas as alterações incrementais numa coleção de Olá lógica versão/ETag `28535` e o intervalo de chaves de partição = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

As alterações são ordenadas por tempo dentro de cada valor de chave de partição dentro do intervalo de chave de partição de Olá. Não há nenhuma ordem garantida entre os valores de chave de partição. Se não existirem resultados mais que o se podem ajustar numa única página, pode ler página seguinte do Olá de resultados ao voltar a submeter pedido Olá com Olá `If-None-Match` cabeçalho com o valor de toohello igual `etag` da resposta anterior Olá. Se vários documentos foram inseridos ou atualizados uma forma dentro de um procedimento armazenado ou acionador, serão todas devolvidos dentro Olá mesmo página de resposta.

> [!NOTE]
> Com o feed de alteração, poderá obter mais itens devolvidas uma página de início especificada no `x-ms-max-item-count` no caso de Olá de vários documentos inseridas ou atualizadas dentro de um procedimentos armazenados ou acionadores. 

Quando utilizar Olá SDK do .NET (1.17.0), defina o campo de Olá `StartTime` no `ChangeFeedOptions` documentos toodirectly retorno mudou desde `StartTime` ao chamar `CreateDocumentChangeFeedQuery`. Ao especificar `If-Modified-Since` utilizar Olá REST API, o pedido irá devolver não documentos de Olá próprios, mas em vez do token de continuação Olá ou `etag` no cabeçalho de resposta de Olá. documentos de Olá tooreturn Olá modificado especificado tempo, o token de continuação Olá `etag` , em seguida, devem ser utilizadas no próximo pedido de Olá com `If-None-Match` tooreturn Olá documentos reais. 

Olá .NET SDK fornece Olá [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) e [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) classes de programa auxiliar tooaccess alterações tooa coleção. Olá fragmento seguinte mostra como tooretrieve todas as alterações desde início Olá utilizando Olá .NET SDK a partir de um único cliente.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
E hello fragmento seguinte mostra como tooprocess alterações em tempo real com base de dados do Azure Cosmos através da utilização de alteração de Olá feed suporte e Olá anterior a função. chamada primeiro Olá devolve todos os documentos de Olá na coleção de Olá e Olá segundo só devolve Olá dois documentos criados que foram criados desde o último ponto de verificação Olá.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

Também pode filtrar o feed de alteração de Olá com eventos de processo de tooselectively de lógica do lado do cliente. Por exemplo, eis um fragmento que utiliza o cliente lado LINQ tooprocess apenas eventos de alteração de temperatura de sensores de dispositivo.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Biblioteca de processador de Feed de alteração
Outra opção consiste toouse Olá [biblioteca do Azure Cosmos DB alterar Feed processador](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), que podem ajudar a distribuir facilmente o processamento de uma alteração do feed em vários consumidores de eventos. biblioteca de Olá é excelente para a criação de alteração feed leitores na plataforma de .NET Olá. Alguns fluxos de trabalho que seriam simplificados, utilizando a biblioteca de processador de Feed de alteração de Olá através de métodos de Olá incluídos no Olá outros SDKs de BD do Cosmos incluem: 

* Quando os dados são armazenados em várias partições de feed de solicitação de atualizações de alteração
* Mover ou replicar dados a partir de uma coleção tooanother
* Execução paralela de ações acionadas por atualizações toodata e alteração feed 

Enquanto a utilização de Olá APIs no Olá Cosmos SDKs fornece acesso preciso toochange feed atualizações em cada partição, utilizando a biblioteca de processador de Feed de alteração de Olá simplifica as alterações de leitura em partições e de vários threads funcionam em paralelo. Em vez de manualmente ao ler as alterações de cada contentor e guardar um token de continuação para cada partição, Olá alteração Feed processador gere automaticamente as alterações de leitura em partições utilizando um mecanismo de concessão.

biblioteca de Olá está disponível como um pacote NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) e a partir do código de origem como uma Github [exemplo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Biblioteca de processador de Feed de alteração de compreender 

Existem quatro componentes principais de implementação Olá processador de Feed de alteração: Olá monitorizado coleção, a recolha de concessão de Olá, anfitrião do processador Olá e consumidores de Olá. 

**Coleção de monitorizado:** Olá monitorizado coleção encontra-se dados Olá partir do qual Olá o feed de alteração é gerada. Uma coleção de toohello monitorizado inserções e as alterações são refletidas no feed de alteração de Olá da coleção de Olá. 

**Coleção de concessão:** Olá coordenadas de coleção de concessão processar a alteração de Olá feed entre vários workers. Uma coleção separada é concessões de Olá toostore utilizada com uma concessão por partição. É vantajoso toostore esta coleção de concessão numa conta diferente com Olá escrever Olá região próximo toowhere está a executar o processador de Feed de alteração. Um objeto de concessão contém Olá seguintes atributos: 
* Proprietário: Especifica o anfitrião de Olá que é proprietário de concessão de Olá
* Continuação: Especifica a posição de Olá (token de continuação) em alteração Olá feed para uma determinada partição
* Timestamp: Hora da última concessão foi atualizada; Olá timestamp pode ser utilizado toocheck se concessão Olá é considerado expirou 

**Anfitrião do processador:** cada anfitrião determina quantos tooprocess de partições com base em quantos outras instâncias dos anfitriões têm concessões ativas são. 
1.  Quando um anfitrião é iniciado, adquire carga de trabalho do concessões toobalance Olá em todos os anfitriões. Um anfitrião periodicamente é renovada de concessões de, pelo que concessões permanecem ativos. 
2.  Ler uma anfitrião pontos de verificação Olá último continuação token tooits concessão para cada. segurança de concorrência tooensure, um anfitrião verifica Olá ETag para cada atualização de concessão. Também são suportadas outras estratégias de ponto de verificação.  
3.  Após encerramento, um anfitrião versões concessões de todos os mas mantém Olá informações de continuação, para que possa retomar ler a partir do ponto de verificação armazenado hello mais tarde. 

Neste momento, número de Olá de anfitriões não pode ser superior ao número de Olá de partições (concessões).

**Os consumidores:** consumidores ou técnicos, existem threads que efetuar a alteração de Olá feed processamento iniciado por cada anfitrião. Cada anfitrião do processador pode ter vários consumidores. Cada consumidor lê Olá alteração feed Olá partição está atribuído tooand notifica o respetivo anfitrião de alterações e expirado concessões.

toofurther compreender como estes quatro elementos do processador de Feed de alteração de trabalham em conjunto, vamos ver um exemplo Olá diagrama a seguir. Olá monitorizado documentos de arquivos de coleção e utiliza cidade"Olá" como chave de partição Olá. Vemos que a partição de Olá azul contém documentos com o campo de "Cidade" Olá da "A E" e assim sucessivamente. Existem dois anfitriões, cada um com dois os consumidores de ler a partir de partições de Olá quatro em paralelo. Olá setas mostram o consumidores Olá ler a partir de um lugar para cima específico no Olá alterar feed. Na primeira partição Olá, azul darker Olá representa alterações unread enquanto blue leve Olá representa Olá já ler as alterações no feed de alteração de Olá. os anfitriões de Olá utilizam Olá concessão coleção toostore um registo de tookeep de valor de "continuação" da Olá atual de leitura de posição para cada consumidor. 

![Utilizar a alteração de base de dados do Azure Cosmos Olá feed anfitrião do processador](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Utilizar a alteração de Feed de biblioteca de processador 
Olá seguinte secção explica como toouse Olá biblioteca de processador de Feed de alteração do contexto de Olá de replicar as alterações a partir de uma coleção de destino de tooa de coleção de origem. Aqui, a coleção de origem Olá é coleção Olá monitorizado no processador de Feed de alteração. 

**Instalar e incluir o pacote NuGet de processador de Feed de alteração de Olá** 

Antes de instalar pacotes de NuGet processador de Feed de alteração, instale primeiro: 
* Microsoft.Azure.DocumentDB, versão 1.13.1 ou superior 
* Newtonsoft, versão 9.0.1 ou acima instalação `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e incluí-la como uma referência.

**Criar uma coleção de destino e de concessão monitorizada,** 

No toouse Olá da ordem biblioteca de processador de Feeds de alteração, Olá concessão necessita toobe criado antes de executar um ou mais anfitriões de processador de Olá. Novamente, recomendamos o armazenamento de uma coleção de concessão numa conta diferente com uma Olá escrita região próximo toowhere que está a executar o processador de Feed de alteração. Neste exemplo de movimento de dados, precisamos de coleção de destino Olá toocreate antes de executar o anfitrião do processador de Feed de alteração de Olá. No código de exemplo de Olá chamamos um Olá toocreate do método de programa auxiliar monitorizado, nos concessionados e coleções de destino, caso ainda não existam. 

> [!WARNING]
> Criar uma coleção tem implicações, de preços são reservar o débito para Olá toocommunicate de aplicação com a base de dados do Azure Cosmos. Para obter mais detalhes, visite Olá [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Criar um anfitrião do processador*

Olá `ChangeFeedProcessorHost` classe fornece um ambiente de tempo de execução seguro para thread com vários processos, segura para as implementações do processador de eventos que também fornece a gestão de concessão de pontos de verificação e partição. Olá toouse `ChangeFeedProcessorHost` classe, pode implementar `IChangeFeedObserver`. Esta interface contém três métodos:

* `OpenAsync`: Esta função é chamada quando observador de feed de alteração é aberto. Pode ser modificado tooperform uma ação específica quando consumidor/observador é aberto.  
* `CloseAsync`: Esta função é chamada quando observador de feed de alteração foi terminada. Pode ser modificado tooperform uma ação específica ao consumidor/observador está fechado.  
* `ProcessChangesAsync`: Esta função é chamada quando novas alterações de documento estão disponíveis no feed de alteração. Pode ser modificado tooperform uma ação específica após todas as atualizações de alteração do feed.  

No nosso exemplo, vamos implementa a interface de Olá `IChangeFeedObserver` através de Olá `DocumentFeedObserver` classe. Aqui, Olá `ProcessChangesAsync` upserts (atualizações) na coleção de destino Olá de feed de um documento de alteração de função. Neste exemplo é útil para mover dados de uma coleção tooanother na ordem toochange Olá a chave de partição de um conjunto de dados. 

*Executar Olá anfitrião do processador*

Antes de iniciar o processamento de eventos, ambos alterar opções de feed e opções de anfitrião de feed de alteração podem ser personalizadas. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
campos específicos Olá que podem ser personalizados estão resumidos na Olá tabelas a seguir. 

**Alterar as opções de Feed**:
<table>
    <tr>
        <th>Nome da propriedade</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Obtém ou define o número máximo de Olá de toobe itens devolvido numa operação de enumeração de Olá no Olá serviço de base de dados de base de dados do Azure Cosmos.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Obtém ou define o id de intervalo de chaves de partição Olá para o pedido atual Olá no serviço de base de dados de base de dados do Azure Cosmos Olá.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Obtém ou define o token de continuação de pedido de Olá no serviço de base de dados de base de dados do Azure Cosmos Olá.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Obtém ou define o token da sessão Olá para utilização com consistência de sessão no Olá serviço de base de dados de base de dados do Azure Cosmos.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Obtém ou define se deve iniciar a alteração do feed no serviço de base de dados de base de dados do Azure Cosmos Olá Olá a partir da (true) ou a atual (false). Por predefinição, este inicia a partir do atual (false).</td>
    </tr>
</table>

**Alterar as opções de anfitrião Feed**:
<table>
    <tr>
        <th>Nome da propriedade</th>
        <th>Tipo</th>
        <th>Descrição</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>intervalo de Olá para todas as concessões para partições atualmente retido por instância de ChangeFeedEventHost Olá.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Olá intervalo tookick desativar uma tarefa toocompute se as partições são distribuídas uniformemente entre instâncias de anfitrião conhecido.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>intervalo de Olá para que Olá concessão é criada numa concessão que representa uma partição. Se a concessão de Olá não for renovado dentro deste intervalo, expirar e a propriedade da partição Olá move tooanother ChangeFeedEventHost instância.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>atraso de Olá entre consulta uma partição para novas alterações no Olá feed, depois de todas as alterações atuais são drained.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Olá concessões de toocheckpoint frequência.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>Int</td>
        <td>Olá mínimo partições para o anfitrião de Olá.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>Int</td>
        <td>pode servir o número máximo de Olá de anfitrião de Olá partições.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>bool</td>
        <td>Se no Olá início do anfitrião Olá todas as concessões existentes deve ser eliminado e anfitrião Olá deve começar do zero.</td>
    </tr>
</table>


processamento de eventos de toostart instanciar `ChangeFeedProcessorHost`, fornecendo os parâmetros adequados Olá para a coleção de BD do Cosmos do Azure. Em seguida, chame `RegisterObserverAsync` tooregister sua `IChangeFeedObserver` implementação (DocumentFeedObserver neste exemplo) com Olá tempo de execução. Neste momento, o anfitrião de Olá tenta tooacquire uma concessão em cada intervalo de chaves de partição na coleção de base de dados do Azure Cosmos Olá utilizando um algoritmo "abrangente". Estas concessões última para um determinado período de tempo e, em seguida, tem de ser renovados. Como novos nós, instâncias de trabalho, neste caso, fique online, colocam reservas de concessões e ao longo do tempo carga Olá desvia entre nós, cada anfitrião tenta tooacquire mais concessões. 

Código de exemplo de Olá, utilizamos uma toocreate de classe (DocumentFeedObserverFactory.cs) fábrica um observador e Olá `RegistObserverFactoryAsync` observador de Olá tooregister. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
Ao longo do tempo, é estabelecido um equilíbrio. Esta capacidade dinâmica permite baseado em CPU dimensionamento automático tooconsumers de toobe aplicada para ambos aumentar verticalmente e horizontalmente. Se as alterações disponíveis do BD Azure Cosmos rapidamente do que os consumidores podem processar, Olá aumento de CPU nos consumidores pode ser utilizado toocause um dimensionamento automático na contagem de instâncias de trabalho.

## <a name="next-steps"></a>Passos seguintes
* Tente Olá [Azure Cosmos DB altere feed exemplos de código no GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Introdução à programação com Olá [SDKs de BD do Azure Cosmos](documentdb-sdk-dotnet.md) ou Olá [REST API](/rest/api/documentdb/).
