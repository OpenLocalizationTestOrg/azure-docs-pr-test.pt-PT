---
title: "aaaProvision débito de base de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como tooset aprovisionado débito de base de dados do Azure Cosmos containsers, coleções, gráficos e tabelas."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a><span data-ttu-id="e22f6-103">Definir o débito para contentores de base de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="e22f6-103">Set throughput for Azure Cosmos DB containers</span></span>

<span data-ttu-id="e22f6-104">Pode definir o débito para os contentores de base de dados do Azure Cosmos no Olá portal do Azure ou através da utilização de Olá SDKs do cliente.</span><span class="sxs-lookup"><span data-stu-id="e22f6-104">You can set throughput for your Azure Cosmos DB containers in hello Azure portal or by using hello client SDKs.</span></span> 

<span data-ttu-id="e22f6-105">Olá, a tabela seguinte apresenta uma lista de débito Olá disponível para contentores:</span><span class="sxs-lookup"><span data-stu-id="e22f6-105">hello following table lists hello throughput available for containers:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="e22f6-106"><strong>Contentor de partições únicas</strong></span><span class="sxs-lookup"><span data-stu-id="e22f6-106"><strong>Single Partition Container</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e22f6-107"><strong>Contentor particionada</strong></span><span class="sxs-lookup"><span data-stu-id="e22f6-107"><strong>Partitioned Container</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e22f6-108">Débito mínimo</span><span class="sxs-lookup"><span data-stu-id="e22f6-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e22f6-109">400 unidades de pedido por segundo</span><span class="sxs-lookup"><span data-stu-id="e22f6-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e22f6-110">2500 unidades de pedido por segundo</span><span class="sxs-lookup"><span data-stu-id="e22f6-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="e22f6-111">Débito máximo</span><span class="sxs-lookup"><span data-stu-id="e22f6-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e22f6-112">10 000 unidades de pedido por segundo</span><span class="sxs-lookup"><span data-stu-id="e22f6-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="e22f6-113">Ilimitado</span><span class="sxs-lookup"><span data-stu-id="e22f6-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a><span data-ttu-id="e22f6-114">débito de Olá tooset utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e22f6-114">tooset hello throughput by using hello Azure portal</span></span>

1. <span data-ttu-id="e22f6-115">Numa nova janela, abra Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e22f6-115">In a new window, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e22f6-116">Na barra de esquerdo Olá, clique em **Azure Cosmos DB**, ou clique em **mais serviços** na parte inferior do Olá, em seguida, desloque-se demasiado**bases de dados**e, em seguida, clique em **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="e22f6-116">On hello left bar, click **Azure Cosmos DB**, or click **More Services** at hello bottom, then scroll too**Databases**, and then click **Azure Cosmos DB**.</span></span>
3. <span data-ttu-id="e22f6-117">Selecione a sua conta de base de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e22f6-117">Select your Cosmos DB account.</span></span>
4. <span data-ttu-id="e22f6-118">Na nova janela Olá, clique em **Explorador de dados (pré-visualização)** no menu de navegação de Olá.</span><span class="sxs-lookup"><span data-stu-id="e22f6-118">In hello new window, click **Data Explorer (Preview)** in hello navigation menu.</span></span>
5. <span data-ttu-id="e22f6-119">Numa janela nova Olá, expanda a base de dados e o contentor e, em seguida, clique em **definições de dimensionamento &**.</span><span class="sxs-lookup"><span data-stu-id="e22f6-119">In hello new window, expand your database and container and then click **Scale & Settings**.</span></span>
6. <span data-ttu-id="e22f6-120">Numa janela nova Olá, escreva Olá novo débito valor no Olá **débito** caixa e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e22f6-120">In hello new window, type hello new throughput value in hello **Throughput** box, and then click **Save**.</span></span>

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a><span data-ttu-id="e22f6-121">débito de Olá tooset utilizando Olá DocumentDB API para .NET</span><span class="sxs-lookup"><span data-stu-id="e22f6-121">tooset hello throughput by using hello DocumentDB API for .NET</span></span>

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="e22f6-122">Débito FAQ</span><span class="sxs-lookup"><span data-stu-id="e22f6-122">Throughput FAQ</span></span>

<span data-ttu-id="e22f6-123">**Pode definir o meu tooless de débito de 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="e22f6-123">**Can I set my throughput tooless than 400 RU/s?**</span></span>

<span data-ttu-id="e22f6-124">400 RU/s é débito mínimos Olá disponível em coleções de partições únicas de BD do Cosmos (2500 RU/s é Olá mínimo para coleções particionadas).</span><span class="sxs-lookup"><span data-stu-id="e22f6-124">400 RU/s is hello minimum throughput available on Cosmos DB single partition collections (2500 RU/s is hello minimum for partitioned collections).</span></span> <span data-ttu-id="e22f6-125">O pedido unidades estão definidas em 100 intervalos de RU/s, mas o débito não é possível definir too100 RU/s ou qualquer valor inferior a 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="e22f6-125">Request units are set in 100 RU/s intervals, but throughput cannot be set too100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="e22f6-126">Se estiver à procura de um método económico toodevelop e Cosmos DB de teste, pode utilizar Olá livre [emulador de BD do Azure Cosmos](local-emulator.md), que pode implementar localmente, sem qualquer custo.</span><span class="sxs-lookup"><span data-stu-id="e22f6-126">If you're looking for a cost effective method toodevelop and test Cosmos DB, you can use hello free [Azure Cosmos DB Emulator](local-emulator.md), which you can deploy locally at no cost.</span></span> 

<span data-ttu-id="e22f6-127">**Como definir a througput Olá API de MongoDB a utilizar?**</span><span class="sxs-lookup"><span data-stu-id="e22f6-127">**How do I set througput using hello MongoDB API?**</span></span>

<span data-ttu-id="e22f6-128">Não há nenhum débito de tooset de extensões de API do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e22f6-128">There's no MongoDB API extension tooset throughput.</span></span> <span data-ttu-id="e22f6-129">Olá recomendação é toouse Olá API do DocumentDB, conforme mostrado no [débito de Olá tooset utilizando Olá DocumentDB API para o .NET](#set-throughput-sdk).</span><span class="sxs-lookup"><span data-stu-id="e22f6-129">hello recommendation is toouse hello DocumentDB API, as shown in [tooset hello throughput by using hello DocumentDB API for .NET](#set-throughput-sdk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e22f6-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e22f6-130">Next steps</span></span>

<span data-ttu-id="e22f6-131">toolearn mais informações sobre o aprovisionamento e a escala planet contínuo com Cosmos DB, consulte [divisão em partições e o dimensionamento com Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="e22f6-131">toolearn more about provisioning and going planet-scale with Cosmos DB, see [Partitioning and scaling with Cosmos DB](partition-data.md).</span></span>
