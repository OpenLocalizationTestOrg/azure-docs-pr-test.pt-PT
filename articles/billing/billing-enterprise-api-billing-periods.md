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
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>APIs de relatórios para os clientes empresariais - períodos de faturação

Olá API de períodos de faturação devolve uma lista de faturação períodos que tenham dados de consumo de Olá especificado inscrição por ordem cronológica inversa. Cada período contém uma propriedade apontar toohello rota de API para conjuntos de quatro Olá de dados - BalanceSummary, UsageDetails, Marktplace encargos e folha de preços. Se o período de Olá não tiver dados, a propriedade correspondente Olá é nula. 


##<a name="request"></a>Pedir 
Foram especificadas propriedades de cabeçalho comuns que necessitam de toobe adicionado [aqui](billing-enterprise-api.md). 

|Método | URI do pedido|
|-|-|
|INTRODUÇÃO| https://Consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / billingperiods|

> [!Note]
> versão de pré-visualização de Olá toouse da API, substitua v2 v1 no Olá acima URL.
>

## <a name="response"></a>Resposta
 
    
    
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
    

**Definições de propriedades de resposta**

|Nome da propriedade| Tipo| Descrição
|-|-|-|
|billingPeriodId| Cadeia| Olá Id exclusivo que representa um determinado período de faturação|
|billingStart| DateTime| Cadeia de ISO 8601 que representa a data de início do período de Olá|
|billingEnd| DateTime| Cadeia de ISO 8601 que representa a data de fim do período de Olá|
|balanceSummary| Cadeia| caminho de URL de Olá que encaminha os dados de resumo de saldo toohello deste período|
|usageDetails| Cadeia| caminho de URL de Olá que encaminha toohello dados de detalhes de utilização deste período|
|marketplaceCharges| Cadeia| caminho de URL de Olá que encaminha toohello dados de encargos de Marketplace deste período|
|folha de preços| Cadeia| caminho de URL de Olá que encaminha toohello folha de preços dados para este período|

<br/>
## <a name="see-also"></a>Consultar também

* [API de balanceamento e resumo](billing-enterprise-api-balance-summary.md)

* [Detalhes de utilização API](billing-enterprise-api-usage-detail.md) 

* [Encargos de arquivo de Marketplace API](billing-enterprise-api-marketplace-storecharge.md) 

* [API de folha de preços](billing-enterprise-api-pricesheet.md)