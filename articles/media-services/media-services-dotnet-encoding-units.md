---
title: "suporte de dados de aaaScale processamento através da adição de unidades de codificação - Azure |  Microsoft Docs"
description: "Saiba como unidades de codificação tooadd toohow com o .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>Como tooscale codificação com o .NET SDK
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Descrição geral
> [!IMPORTANT]
> Certifique-se de que tooreview Olá [descrição geral](media-services-scale-media-processing-overview.md) tópico tooget mais informações sobre dimensionamento processamento tópico de suporte de dados.
> 
> 

toochange Olá reservado unidade tipo e Olá número de unidades codificação reservada com o .NET SDK, Olá seguintes:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Abrir um pedido de suporte
Por predefinição, cada conta de Media Services pode dimensionar tooup too25 codificação e 5 a pedido de transmissão em fluxo unidades reservadas. Pode pedir um limite superior ao abrir um pedido de suporte.

### <a name="open-a-support-ticket"></a>Abra um pedido de suporte
um pedido de suporte de tooopen Olá seguintes:

1. Clique em [obter suporte](https://manage.windowsazure.com/?getsupport=true). Se não tiver sessão iniciada, terá de ser pedido tooenter as suas credenciais.
2. Selecione a sua subscrição.
3. Em tipo de suporte, selecione "Técnica".
4. Clique em "Criar pedido de".
5. Selecione "Media Services do Azure" na lista de produto Olá apresentados na página seguinte Olá.
6. Selecione um "tipo de problema" que é adequado para o seu problema.
7. Clique em continuar.
8. Siga as instruções na página seguinte e, em seguida, introduza os detalhes sobre o problema.
9. Clique em submeter o pedido de suporte do tooopen Olá.

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

