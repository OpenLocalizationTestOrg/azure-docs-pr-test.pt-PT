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
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Definir o débito para contentores de base de dados do Azure Cosmos

Pode definir o débito para os contentores de base de dados do Azure Cosmos no Olá portal do Azure ou através da utilização de Olá SDKs do cliente. 

Olá, a tabela seguinte apresenta uma lista de débito Olá disponível para contentores:

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Contentor de partições únicas</strong></p></td>
            <td valign="top"><p><strong>Contentor particionada</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Débito mínimo</p></td>
            <td valign="top"><p>400 unidades de pedido por segundo</p></td>
            <td valign="top"><p>2500 unidades de pedido por segundo</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Débito máximo</p></td>
            <td valign="top"><p>10 000 unidades de pedido por segundo</p></td>
            <td valign="top"><p>Ilimitado</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>débito de Olá tooset utilizando Olá portal do Azure

1. Numa nova janela, abra Olá [portal do Azure](https://portal.azure.com).
2. Na barra de esquerdo Olá, clique em **Azure Cosmos DB**, ou clique em **mais serviços** na parte inferior do Olá, em seguida, desloque-se demasiado**bases de dados**e, em seguida, clique em **Azure Cosmos DB**.
3. Selecione a sua conta de base de dados do Cosmos.
4. Na nova janela Olá, clique em **Explorador de dados (pré-visualização)** no menu de navegação de Olá.
5. Numa janela nova Olá, expanda a base de dados e o contentor e, em seguida, clique em **definições de dimensionamento &**.
6. Numa janela nova Olá, escreva Olá novo débito valor no Olá **débito** caixa e, em seguida, clique em **guardar**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>débito de Olá tooset utilizando Olá DocumentDB API para .NET

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

## <a name="throughput-faq"></a>Débito FAQ

**Pode definir o meu tooless de débito de 400 RU/s?**

400 RU/s é débito mínimos Olá disponível em coleções de partições únicas de BD do Cosmos (2500 RU/s é Olá mínimo para coleções particionadas). O pedido unidades estão definidas em 100 intervalos de RU/s, mas o débito não é possível definir too100 RU/s ou qualquer valor inferior a 400 RU/s. Se estiver à procura de um método económico toodevelop e Cosmos DB de teste, pode utilizar Olá livre [emulador de BD do Azure Cosmos](local-emulator.md), que pode implementar localmente, sem qualquer custo. 

**Como definir a througput Olá API de MongoDB a utilizar?**

Não há nenhum débito de tooset de extensões de API do MongoDB. Olá recomendação é toouse Olá API do DocumentDB, conforme mostrado no [débito de Olá tooset utilizando Olá DocumentDB API para o .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre o aprovisionamento e a escala planet contínuo com Cosmos DB, consulte [divisão em partições e o dimensionamento com Cosmos DB](partition-data.md).
