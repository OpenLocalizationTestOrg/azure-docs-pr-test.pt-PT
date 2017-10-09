---
title: "aaaAzure APIs Enterprise de faturação - períodos de faturação | Microsoft Docs"
description: "Saiba mais sobre Olá relatórios APIs que permitem dados de consumo do Enterprise Azure clientes toopull através de programação."
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="e0907-103">APIs de relatórios para os clientes empresariais - períodos de faturação</span><span class="sxs-lookup"><span data-stu-id="e0907-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="e0907-104">Olá API de períodos de faturação devolve uma lista de faturação períodos que tenham dados de consumo de Olá especificado inscrição por ordem cronológica inversa.</span><span class="sxs-lookup"><span data-stu-id="e0907-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="e0907-105">Cada período contém uma propriedade apontar toohello rota de API para conjuntos de quatro Olá de dados - BalanceSummary, UsageDetails, Marktplace encargos e folha de preços.</span><span class="sxs-lookup"><span data-stu-id="e0907-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="e0907-106">Se o período de Olá não tiver dados, a propriedade correspondente Olá é nula.</span><span class="sxs-lookup"><span data-stu-id="e0907-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="e0907-107">Pedir</span><span class="sxs-lookup"><span data-stu-id="e0907-107">Request</span></span> 
<span data-ttu-id="e0907-108">Foram especificadas propriedades de cabeçalho comuns que necessitam de toobe adicionado [aqui](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="e0907-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="e0907-109">Método</span><span class="sxs-lookup"><span data-stu-id="e0907-109">Method</span></span> | <span data-ttu-id="e0907-110">URI do pedido</span><span class="sxs-lookup"><span data-stu-id="e0907-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="e0907-111">INTRODUÇÃO</span><span class="sxs-lookup"><span data-stu-id="e0907-111">GET</span></span>| <span data-ttu-id="e0907-112">https://Consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / billingperiods</span><span class="sxs-lookup"><span data-stu-id="e0907-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="e0907-113">versão de pré-visualização de Olá toouse da API, substitua v2 v1 no Olá acima URL.</span><span class="sxs-lookup"><span data-stu-id="e0907-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="e0907-114">Resposta</span><span class="sxs-lookup"><span data-stu-id="e0907-114">Response</span></span>
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

<span data-ttu-id="e0907-115">**Definições de propriedades de resposta**</span><span class="sxs-lookup"><span data-stu-id="e0907-115">**Response property definitions**</span></span>

|<span data-ttu-id="e0907-116">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="e0907-116">Property Name</span></span>| <span data-ttu-id="e0907-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="e0907-117">Type</span></span>| <span data-ttu-id="e0907-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="e0907-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="e0907-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="e0907-119">billingPeriodId</span></span>| <span data-ttu-id="e0907-120">Cadeia</span><span class="sxs-lookup"><span data-stu-id="e0907-120">string</span></span>| <span data-ttu-id="e0907-121">Olá Id exclusivo que representa um determinado período de faturação</span><span class="sxs-lookup"><span data-stu-id="e0907-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="e0907-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="e0907-122">billingStart</span></span>| <span data-ttu-id="e0907-123">DateTime</span><span class="sxs-lookup"><span data-stu-id="e0907-123">datetime</span></span>| <span data-ttu-id="e0907-124">Cadeia de ISO 8601 que representa a data de início do período de Olá</span><span class="sxs-lookup"><span data-stu-id="e0907-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="e0907-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="e0907-125">billingEnd</span></span>| <span data-ttu-id="e0907-126">DateTime</span><span class="sxs-lookup"><span data-stu-id="e0907-126">datetime</span></span>| <span data-ttu-id="e0907-127">Cadeia de ISO 8601 que representa a data de fim do período de Olá</span><span class="sxs-lookup"><span data-stu-id="e0907-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="e0907-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="e0907-128">balanceSummary</span></span>| <span data-ttu-id="e0907-129">Cadeia</span><span class="sxs-lookup"><span data-stu-id="e0907-129">string</span></span>| <span data-ttu-id="e0907-130">caminho de URL de Olá que encaminha os dados de resumo de saldo toohello deste período</span><span class="sxs-lookup"><span data-stu-id="e0907-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="e0907-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="e0907-131">usageDetails</span></span>| <span data-ttu-id="e0907-132">Cadeia</span><span class="sxs-lookup"><span data-stu-id="e0907-132">string</span></span>| <span data-ttu-id="e0907-133">caminho de URL de Olá que encaminha toohello dados de detalhes de utilização deste período</span><span class="sxs-lookup"><span data-stu-id="e0907-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="e0907-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="e0907-134">marketplaceCharges</span></span>| <span data-ttu-id="e0907-135">Cadeia</span><span class="sxs-lookup"><span data-stu-id="e0907-135">string</span></span>| <span data-ttu-id="e0907-136">caminho de URL de Olá que encaminha toohello dados de encargos de Marketplace deste período</span><span class="sxs-lookup"><span data-stu-id="e0907-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="e0907-137">folha de preços</span><span class="sxs-lookup"><span data-stu-id="e0907-137">priceSheet</span></span>| <span data-ttu-id="e0907-138">Cadeia</span><span class="sxs-lookup"><span data-stu-id="e0907-138">string</span></span>| <span data-ttu-id="e0907-139">caminho de URL de Olá que encaminha toohello folha de preços dados para este período</span><span class="sxs-lookup"><span data-stu-id="e0907-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="e0907-140">Consultar também</span><span class="sxs-lookup"><span data-stu-id="e0907-140">See also</span></span>

* [<span data-ttu-id="e0907-141">API de balanceamento e resumo</span><span class="sxs-lookup"><span data-stu-id="e0907-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="e0907-142">Detalhes de utilização API</span><span class="sxs-lookup"><span data-stu-id="e0907-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="e0907-143">Encargos de arquivo de Marketplace API</span><span class="sxs-lookup"><span data-stu-id="e0907-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="e0907-144">API de folha de preços</span><span class="sxs-lookup"><span data-stu-id="e0907-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)