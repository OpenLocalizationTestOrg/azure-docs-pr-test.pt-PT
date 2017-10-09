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
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="983ab-104">Expirar os dados em coleções de base de dados do Azure Cosmos automaticamente com o tempo toolive</span><span class="sxs-lookup"><span data-stu-id="983ab-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="983ab-105">As aplicações podem produzir e armazenar grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="983ab-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="983ab-106">Alguns destes dados, incluindo machine gerado dados, os registos e utilizador a sessão do evento informações apenas são útil para um período de tempo finito.</span><span class="sxs-lookup"><span data-stu-id="983ab-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="983ab-107">Depois dos dados de Olá torna-se às necessidades de surplus toohello da aplicação Olá é seguro toopurge estes dados e reduzir as necessidades de armazenamento Olá de uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="983ab-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="983ab-108">Com "tempo toolive" ou TTL, base de dados do Microsoft Azure Cosmos fornece documentos toohave capacidade de Olá removidos automaticamente da base de dados de Olá após um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="983ab-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="983ab-109">Olá tempo predefinido durante toolive pode ser definido ao nível da coleção de Olá e substituí-lo numa base por documento.</span><span class="sxs-lookup"><span data-stu-id="983ab-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="983ab-110">Depois do TTL é definido como uma predefinição de coleção ou a um nível de documento, base de dados do Cosmos removerá automaticamente documentos que existem depois desse período de tempo, em segundos, desde que foram modificado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="983ab-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="983ab-111">Tempo toolive na base de dados do Cosmos utiliza um desvio em relação ao documento Olá foi modificado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="983ab-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="983ab-112">toodo este de TI utiliza Olá `_ts` campo de que existe em todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="983ab-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="983ab-113">campo de _ts Olá é uma unix estilo época timestamp que representa Olá data e hora.</span><span class="sxs-lookup"><span data-stu-id="983ab-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="983ab-114">Olá `_ts` campo é atualizado sempre que um documento é modificado.</span><span class="sxs-lookup"><span data-stu-id="983ab-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="983ab-115">Comportamento TTL</span><span class="sxs-lookup"><span data-stu-id="983ab-115">TTL behavior</span></span>
<span data-ttu-id="983ab-116">funcionalidade TTL Olá é controlada pelas propriedades TTL em dois níveis - Olá coleção Olá documento nível e.</span><span class="sxs-lookup"><span data-stu-id="983ab-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="983ab-117">valores de Olá estão definidos em segundos e são tratados como um delta de Olá `_ts` esse documento Olá foi modificado pela última vez em.</span><span class="sxs-lookup"><span data-stu-id="983ab-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="983ab-118">DefaultTTL para a coleção de Olá</span><span class="sxs-lookup"><span data-stu-id="983ab-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="983ab-119">Se em falta (ou conjunto toonull), documentos não são eliminados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="983ab-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="983ab-120">Se estiver presente, não sendo valor Olá "-1" = infinita – documentos não expirarem por predefinição</span><span class="sxs-lookup"><span data-stu-id="983ab-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="983ab-121">Se estiver presente e o valor de Olá é algumas número ("n") – documentos expirarem "n" segundos após a última modificação</span><span class="sxs-lookup"><span data-stu-id="983ab-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="983ab-122">Valor de TTL para documentos Olá:</span><span class="sxs-lookup"><span data-stu-id="983ab-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="983ab-123">Propriedade só é aplicável se DefaultTTL está presente para a coleção do principal de Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="983ab-124">Substitui o valor de DefaultTTL Olá para a coleção do principal de Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="983ab-125">Assim que o documento de Olá expirou (`ttl`  +  `_ts` > = hora atual do servidor), documento Olá está marcado como "expirado".</span><span class="sxs-lookup"><span data-stu-id="983ab-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="983ab-126">Nenhuma operação será permitida nestes documentos após esta hora e serão excluídos resultados Olá quaisquer consultas efetuadas.</span><span class="sxs-lookup"><span data-stu-id="983ab-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="983ab-127">documentos Olá fisicamente são eliminados no sistema de Olá e são eliminados em segundo plano de Olá opportunistically numa altura posterior.</span><span class="sxs-lookup"><span data-stu-id="983ab-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="983ab-128">Isto não consome qualquer [unidades de pedido (RUs)](request-units.md) do orçamento de coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="983ab-129">pode ser mostrado Olá acima lógica Olá matriz os seguintes:</span><span class="sxs-lookup"><span data-stu-id="983ab-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="983ab-130">DefaultTTL em falta/não definido na coleção de Olá</span><span class="sxs-lookup"><span data-stu-id="983ab-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="983ab-131">DefaultTTL = -1 na coleção</span><span class="sxs-lookup"><span data-stu-id="983ab-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="983ab-132">DefaultTTL = "n" na coleção</span><span class="sxs-lookup"><span data-stu-id="983ab-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="983ab-133">TTL em falta no documento</span><span class="sxs-lookup"><span data-stu-id="983ab-133">TTL Missing on document</span></span> |<span data-ttu-id="983ab-134">Nada toooverride ao nível do documento, uma vez que o documento de Olá e coleção não tem nenhum conceito de TTL.</span><span class="sxs-lookup"><span data-stu-id="983ab-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="983ab-135">Não existem documentos nesta coleção irão expirar.</span><span class="sxs-lookup"><span data-stu-id="983ab-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="983ab-136">documentos Olá nesta coleção irão expirar quando intervalo n decorrida.</span><span class="sxs-lookup"><span data-stu-id="983ab-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="983ab-137">TTL = -1 no documento</span><span class="sxs-lookup"><span data-stu-id="983ab-137">TTL = -1 on document</span></span> |<span data-ttu-id="983ab-138">Nada toooverride ao nível do documento Olá, uma vez que não define a coleção de Olá Olá DefaultTTL propriedade que pode substituir um documento.</span><span class="sxs-lookup"><span data-stu-id="983ab-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="983ab-139">TTL num documento é não interpretado pelo sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="983ab-140">Não existem documentos nesta coleção irão expirar.</span><span class="sxs-lookup"><span data-stu-id="983ab-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="983ab-141">documento de Olá com TTL =-1 nesta coleção nunca irá expirar.</span><span class="sxs-lookup"><span data-stu-id="983ab-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="983ab-142">Todos os outros documentos irão expirar após o intervalo de "n".</span><span class="sxs-lookup"><span data-stu-id="983ab-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="983ab-143">TTL = n no documento</span><span class="sxs-lookup"><span data-stu-id="983ab-143">TTL = n on document</span></span> |<span data-ttu-id="983ab-144">Nada toooverride ao nível do documento Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="983ab-145">TTL num documento no não interpretado pelo sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="983ab-146">documento de Olá com TTL = n irá expirar após n intervalo, em segundos.</span><span class="sxs-lookup"><span data-stu-id="983ab-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="983ab-147">Outros documentos irão herdar o intervalo de -1 e nunca expirem.</span><span class="sxs-lookup"><span data-stu-id="983ab-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="983ab-148">documento de Olá com TTL = n irá expirar após n intervalo, em segundos.</span><span class="sxs-lookup"><span data-stu-id="983ab-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="983ab-149">Outros documentos serão herdam a coleção de Olá intervalo "n".</span><span class="sxs-lookup"><span data-stu-id="983ab-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="983ab-150">Configurar o valor de TTL</span><span class="sxs-lookup"><span data-stu-id="983ab-150">Configuring TTL</span></span>
<span data-ttu-id="983ab-151">Por predefinição, o tempo toolive está desativado por predefinição em todas as coleções de BD do Cosmos e em todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="983ab-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="983ab-152">Ativar o TTL</span><span class="sxs-lookup"><span data-stu-id="983ab-152">Enabling TTL</span></span>
<span data-ttu-id="983ab-153">tooenable TTL de uma coleção ou documentos Olá dentro de uma coleção, é necessário tooset Olá DefaultTTL propriedade tooeither uma coleção -1 ou um número positivo diferente de zero.</span><span class="sxs-lookup"><span data-stu-id="983ab-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="983ab-154">Definição significa de demasiado-1 para DefaultTTL de Olá que por predefinição todos os documentos na coleção de Olá serão em direto indefinidamente, mas Olá Cosmos DB serviço deverá monitorizar esta coleção para documentos que tenham substituído esta predefinição.</span><span class="sxs-lookup"><span data-stu-id="983ab-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="983ab-155">Configurar o TTL predefinido de uma coleção</span><span class="sxs-lookup"><span data-stu-id="983ab-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="983ab-156">São tooconfigure capaz de uma hora predefinida toolive um nível da coleção.</span><span class="sxs-lookup"><span data-stu-id="983ab-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="983ab-157">Olá tooset TTL numa coleção, terá de tooprovide um número positivo diferente de zero, que indica o período de Olá, em segundos, tooexpire todos os documentos na coleção de Olá depois Olá modificado pela última vez timestamp documento Olá (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="983ab-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="983ab-158">Em alternativa, pode definir Olá predefinido demasiado-1, o que significa que todos os documentos inseridos na coleção de toohello serão live indefinidamente por predefinição.</span><span class="sxs-lookup"><span data-stu-id="983ab-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="983ab-159">Definição TTL de um documento</span><span class="sxs-lookup"><span data-stu-id="983ab-159">Setting TTL on a document</span></span>
<span data-ttu-id="983ab-160">Além disso toosetting um TTL predefinido de uma coleção pode definir TTL específico a um nível de documento.</span><span class="sxs-lookup"><span data-stu-id="983ab-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="983ab-161">Fazer isto irá substituir a predefinição de Olá da coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="983ab-162">Olá tooset TTL num documento, terá de tooprovide um número positivo diferente de zero, que indica Olá período, em segundos, o documento de Olá tooexpire depois Olá modificado pela última vez timestamp documento Olá (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="983ab-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="983ab-163">Se um documento não tem nenhum campo de valor de TTL, em seguida, Olá predefinido da coleção de Olá será aplicada.</span><span class="sxs-lookup"><span data-stu-id="983ab-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="983ab-164">Se o TTL é desativado ao nível da coleção de Olá, campo de valor de TTL Olá no documento de Olá será ignorado enquanto o TTL seja ativada de novo na coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="983ab-165">Eis um fragmento que mostra como tooset Olá expiração de TTL de um documento:</span><span class="sxs-lookup"><span data-stu-id="983ab-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

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


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="983ab-166">Expandir o TTL num documento existente</span><span class="sxs-lookup"><span data-stu-id="983ab-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="983ab-167">Só pode repor Olá TTL num documento efetuando qualquer operação de escrita no documento de Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="983ab-168">Fazê-lo, irá definir Olá `_ts` toohello hora atual e Olá contagem decrescente toohello documentar expiração, conforme definido pela Olá `ttl`, começará novamente.</span><span class="sxs-lookup"><span data-stu-id="983ab-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="983ab-169">Se desejar toochange Olá `ttl` de um documento, pode atualizar o campo de Olá, como pode fazer com qualquer outro campo pode ser definido.</span><span class="sxs-lookup"><span data-stu-id="983ab-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="983ab-170">Remover o TTL de um documento</span><span class="sxs-lookup"><span data-stu-id="983ab-170">Removing TTL from a document</span></span>
<span data-ttu-id="983ab-171">Se tiver sido definido um valor de TTL num documento e já não pretender tooexpire esse documento, em seguida, pode obter documento de Olá, remover o campo de valor de TTL Olá e substitua documento Olá no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="983ab-172">Quando o campo de valor de TTL Olá é removido do documento Olá, predefinição Olá da coleção de Olá será aplicada.</span><span class="sxs-lookup"><span data-stu-id="983ab-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="983ab-173">toostop um documento de expirar e não herda da coleção de Olá, em seguida, terá de tooset Olá TTL Valor demasiado-1.</span><span class="sxs-lookup"><span data-stu-id="983ab-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="983ab-174">Desativar o TTL</span><span class="sxs-lookup"><span data-stu-id="983ab-174">Disabling TTL</span></span>
<span data-ttu-id="983ab-175">toodisable TTL inteiramente num coleção e a paragem Olá fundo processar a partir à procura de documentos expirados propriedade de DefaultTTL Olá na coleção de Olá deve ser eliminada.</span><span class="sxs-lookup"><span data-stu-id="983ab-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="983ab-176">Eliminar esta propriedade é diferente do defini-la demasiado-1.</span><span class="sxs-lookup"><span data-stu-id="983ab-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="983ab-177">A definição demasiado-1 significa novos documentos adicionado toohello coleção será permanentemente em direto, mas pode substituir isto em documentos específicos na coleção de Olá.</span><span class="sxs-lookup"><span data-stu-id="983ab-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="983ab-178">Remover esta propriedade inteiramente da coleção de Olá significa que não existem documentos irão expirar, mesmo existem documentos que tenham explicitamente substituído um predefinido anterior.</span><span class="sxs-lookup"><span data-stu-id="983ab-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="983ab-179">FAQ</span><span class="sxs-lookup"><span data-stu-id="983ab-179">FAQ</span></span>
<span data-ttu-id="983ab-180">**O que irá TTL custo-me?**</span><span class="sxs-lookup"><span data-stu-id="983ab-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="983ab-181">Não há nenhum toosetting custos adicionais de um valor de TTL num documento.</span><span class="sxs-lookup"><span data-stu-id="983ab-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="983ab-182">**Quanto será necessário toodelete os meus documentos depois Olá TTL está a funcionar?**</span><span class="sxs-lookup"><span data-stu-id="983ab-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="983ab-183">documentos Olá expiraram imediatamente depois de Olá TTL está a funcionar e não estará acessível através de CRUD ou APIs de consulta.</span><span class="sxs-lookup"><span data-stu-id="983ab-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="983ab-184">**TTL num documento não terá qualquer impacto em custos de RU?**</span><span class="sxs-lookup"><span data-stu-id="983ab-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="983ab-185">Não, existirá nenhum impacto em custos de RU para eliminações de expirada documentos através de TTL na base de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="983ab-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="983ab-186">**Funcionalidade TTL Olá só se aplicam tooentire documentos ou posso expirar os valores de propriedade de documento individuais?**</span><span class="sxs-lookup"><span data-stu-id="983ab-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="983ab-187">TTL aplica-se toohello todo o documento.</span><span class="sxs-lookup"><span data-stu-id="983ab-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="983ab-188">Se gostaria de tooexpire apenas uma parte de um documento, é recomendada que extrair parte Olá do documento de principais de Olá tooa separado, documento "ligada" e, em seguida, utilize o TTL nesse documento extraídos.</span><span class="sxs-lookup"><span data-stu-id="983ab-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="983ab-189">**A funcionalidade TTL Olá tem quaisquer requisitos específicos de indexação?**</span><span class="sxs-lookup"><span data-stu-id="983ab-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="983ab-190">Sim.</span><span class="sxs-lookup"><span data-stu-id="983ab-190">Yes.</span></span> <span data-ttu-id="983ab-191">coleção de Olá tem de ter [conjunto de política de indexação](indexing-policies.md) tooeither Consistent ou Lazy.</span><span class="sxs-lookup"><span data-stu-id="983ab-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="983ab-192">Tentar tooset DefaultTTL numa coleção com indexação tooNone de conjunto resultará num erro, como irá tentar tooturn desativar indexação numa coleção que tenha um DefaultTTL já definido.</span><span class="sxs-lookup"><span data-stu-id="983ab-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="983ab-193">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="983ab-193">Next steps</span></span>
<span data-ttu-id="983ab-194">toolearn mais informações sobre a BD do Cosmos do Azure, consulte o serviço de toohello [ *documentação* ](https://azure.microsoft.com/documentation/services/cosmos-db/) página.</span><span class="sxs-lookup"><span data-stu-id="983ab-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

