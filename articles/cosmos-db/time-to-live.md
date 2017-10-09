---
title: dados de aaaExpire do BD Azure Cosmos com tempo toolive | Microsoft Docs
description: "Com o TTL, base de dados do Microsoft Azure Cosmos fornece documentos toohave capacidade de Olá automaticamente removidos do sistema de Olá após um período de tempo."
services: cosmos-db
documentationcenter: 
keywords: tempo toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Expirar os dados em coleções de base de dados do Azure Cosmos automaticamente com o tempo toolive
As aplicações podem produzir e armazenar grandes quantidades de dados. Alguns destes dados, incluindo machine gerado dados, os registos e utilizador a sessão do evento informações apenas são útil para um período de tempo finito. Depois dos dados de Olá torna-se às necessidades de surplus toohello da aplicação Olá é seguro toopurge estes dados e reduzir as necessidades de armazenamento Olá de uma aplicação.

Com "tempo toolive" ou TTL, base de dados do Microsoft Azure Cosmos fornece documentos toohave capacidade de Olá removidos automaticamente da base de dados de Olá após um período de tempo. Olá tempo predefinido durante toolive pode ser definido ao nível da coleção de Olá e substituí-lo numa base por documento. Depois do TTL é definido como uma predefinição de coleção ou a um nível de documento, base de dados do Cosmos removerá automaticamente documentos que existem depois desse período de tempo, em segundos, desde que foram modificado pela última vez.

Tempo toolive na base de dados do Cosmos utiliza um desvio em relação ao documento Olá foi modificado pela última vez. toodo este de TI utiliza Olá `_ts` campo de que existe em todos os documentos. campo de _ts Olá é uma unix estilo época timestamp que representa Olá data e hora. Olá `_ts` campo é atualizado sempre que um documento é modificado. 

## <a name="ttl-behavior"></a>Comportamento TTL
funcionalidade TTL Olá é controlada pelas propriedades TTL em dois níveis - Olá coleção Olá documento nível e. valores de Olá estão definidos em segundos e são tratados como um delta de Olá `_ts` esse documento Olá foi modificado pela última vez em.

1. DefaultTTL para a coleção de Olá
   
   * Se em falta (ou conjunto toonull), documentos não são eliminados automaticamente.
   * Se estiver presente, não sendo valor Olá "-1" = infinita – documentos não expirarem por predefinição
   * Se estiver presente e o valor de Olá é algumas número ("n") – documentos expirarem "n" segundos após a última modificação
2. Valor de TTL para documentos Olá: 
   
   * Propriedade só é aplicável se DefaultTTL está presente para a coleção do principal de Olá.
   * Substitui o valor de DefaultTTL Olá para a coleção do principal de Olá.

Assim que o documento de Olá expirou (`ttl`  +  `_ts` > = hora atual do servidor), documento Olá está marcado como "expirado". Nenhuma operação será permitida nestes documentos após esta hora e serão excluídos resultados Olá quaisquer consultas efetuadas. documentos Olá fisicamente são eliminados no sistema de Olá e são eliminados em segundo plano de Olá opportunistically numa altura posterior. Isto não consome qualquer [unidades de pedido (RUs)](request-units.md) do orçamento de coleção de Olá.

pode ser mostrado Olá acima lógica Olá matriz os seguintes:

|  | DefaultTTL em falta/não definido na coleção de Olá | DefaultTTL = -1 na coleção | DefaultTTL = "n" na coleção |
| --- |:--- |:--- |:--- |
| TTL em falta no documento |Nada toooverride ao nível do documento, uma vez que o documento de Olá e coleção não tem nenhum conceito de TTL. |Não existem documentos nesta coleção irão expirar. |documentos Olá nesta coleção irão expirar quando intervalo n decorrida. |
| TTL = -1 no documento |Nada toooverride ao nível do documento Olá, uma vez que não define a coleção de Olá Olá DefaultTTL propriedade que pode substituir um documento. TTL num documento é não interpretado pelo sistema Olá. |Não existem documentos nesta coleção irão expirar. |documento de Olá com TTL =-1 nesta coleção nunca irá expirar. Todos os outros documentos irão expirar após o intervalo de "n". |
| TTL = n no documento |Nada toooverride ao nível do documento Olá. TTL num documento no não interpretado pelo sistema Olá. |documento de Olá com TTL = n irá expirar após n intervalo, em segundos. Outros documentos irão herdar o intervalo de -1 e nunca expirem. |documento de Olá com TTL = n irá expirar após n intervalo, em segundos. Outros documentos serão herdam a coleção de Olá intervalo "n". |

## <a name="configuring-ttl"></a>Configurar o valor de TTL
Por predefinição, o tempo toolive está desativado por predefinição em todas as coleções de BD do Cosmos e em todos os documentos.

## <a name="enabling-ttl"></a>Ativar o TTL
tooenable TTL de uma coleção ou documentos Olá dentro de uma coleção, é necessário tooset Olá DefaultTTL propriedade tooeither uma coleção -1 ou um número positivo diferente de zero. Definição significa de demasiado-1 para DefaultTTL de Olá que por predefinição todos os documentos na coleção de Olá serão em direto indefinidamente, mas Olá Cosmos DB serviço deverá monitorizar esta coleção para documentos que tenham substituído esta predefinição.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Configurar o TTL predefinido de uma coleção
São tooconfigure capaz de uma hora predefinida toolive um nível da coleção. Olá tooset TTL numa coleção, terá de tooprovide um número positivo diferente de zero, que indica o período de Olá, em segundos, tooexpire todos os documentos na coleção de Olá depois Olá modificado pela última vez timestamp documento Olá (`_ts`). Em alternativa, pode definir Olá predefinido demasiado-1, o que significa que todos os documentos inseridos na coleção de toohello serão live indefinidamente por predefinição.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>Definição TTL de um documento
Além disso toosetting um TTL predefinido de uma coleção pode definir TTL específico a um nível de documento. Fazer isto irá substituir a predefinição de Olá da coleção de Olá.

* Olá tooset TTL num documento, terá de tooprovide um número positivo diferente de zero, que indica Olá período, em segundos, o documento de Olá tooexpire depois Olá modificado pela última vez timestamp documento Olá (`_ts`).
* Se um documento não tem nenhum campo de valor de TTL, em seguida, Olá predefinido da coleção de Olá será aplicada.
* Se o TTL é desativado ao nível da coleção de Olá, campo de valor de TTL Olá no documento de Olá será ignorado enquanto o TTL seja ativada de novo na coleção de Olá.

Eis um fragmento que mostra como tooset Olá expiração de TTL de um documento:

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>Expandir o TTL num documento existente
Só pode repor Olá TTL num documento efetuando qualquer operação de escrita no documento de Olá. Fazê-lo, irá definir Olá `_ts` toohello hora atual e Olá contagem decrescente toohello documentar expiração, conforme definido pela Olá `ttl`, começará novamente. Se desejar toochange Olá `ttl` de um documento, pode atualizar o campo de Olá, como pode fazer com qualquer outro campo pode ser definido.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>Remover o TTL de um documento
Se tiver sido definido um valor de TTL num documento e já não pretender tooexpire esse documento, em seguida, pode obter documento de Olá, remover o campo de valor de TTL Olá e substitua documento Olá no servidor de Olá. Quando o campo de valor de TTL Olá é removido do documento Olá, predefinição Olá da coleção de Olá será aplicada. toostop um documento de expirar e não herda da coleção de Olá, em seguida, terá de tooset Olá TTL Valor demasiado-1.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>Desativar o TTL
toodisable TTL inteiramente num coleção e a paragem Olá fundo processar a partir à procura de documentos expirados propriedade de DefaultTTL Olá na coleção de Olá deve ser eliminada. Eliminar esta propriedade é diferente do defini-la demasiado-1. A definição demasiado-1 significa novos documentos adicionado toohello coleção será permanentemente em direto, mas pode substituir isto em documentos específicos na coleção de Olá. Remover esta propriedade inteiramente da coleção de Olá significa que não existem documentos irão expirar, mesmo existem documentos que tenham explicitamente substituído um predefinido anterior.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>FAQ
**O que irá TTL custo-me?**

Não há nenhum toosetting custos adicionais de um valor de TTL num documento.

**Quanto será necessário toodelete os meus documentos depois Olá TTL está a funcionar?**

documentos Olá expiraram imediatamente depois de Olá TTL está a funcionar e não estará acessível através de CRUD ou APIs de consulta. 

**TTL num documento não terá qualquer impacto em custos de RU?**

Não, existirá nenhum impacto em custos de RU para eliminações de expirada documentos através de TTL na base de dados do Cosmos.

**Funcionalidade TTL Olá só se aplicam tooentire documentos ou posso expirar os valores de propriedade de documento individuais?**

TTL aplica-se toohello todo o documento. Se gostaria de tooexpire apenas uma parte de um documento, é recomendada que extrair parte Olá do documento de principais de Olá tooa separado, documento "ligada" e, em seguida, utilize o TTL nesse documento extraídos.

**A funcionalidade TTL Olá tem quaisquer requisitos específicos de indexação?**

Sim. coleção de Olá tem de ter [conjunto de política de indexação](indexing-policies.md) tooeither Consistent ou Lazy. Tentar tooset DefaultTTL numa coleção com indexação tooNone de conjunto resultará num erro, como irá tentar tooturn desativar indexação numa coleção que tenha um DefaultTTL já definido.

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a BD do Cosmos do Azure, consulte o serviço de toohello [ *documentação* ](https://azure.microsoft.com/documentation/services/cosmos-db/) página.

