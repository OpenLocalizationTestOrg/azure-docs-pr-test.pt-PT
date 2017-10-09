---
title: "aaaTest VM oferecem para Olá Marketplace | Microsoft Docs"
description: "Compreenda como tootest a VM de imagem para Olá Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>Testar a sua oferta VM para Olá Azure Marketplace em transição
Significa que implementar o SKU no privado "sandbox", onde pode testar e validar a sua funcionalidade antes de o implementar toohello Marketplace de teste. Olá SKU é apresentado no teste, tal como qualquer cliente de tooa que tenha implementado. A imagem VM tem de ser certificadas toobe enviadas por push toostaging.

## <a name="step-1-push-your-offer-toostaging"></a>Passo 1: Push toostaging sua oferta
1. No Olá **publicar** separador, clique em **Push tooStaging**.
   
    ![desenho](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. Se o Portal de publicação de Olá notifica-o de erros, corrija-os.
3. No Olá **quem pode aceder à sua oferta testada?** caixa de diálogo, introduza a lista de Olá de subscrições do Azure que irá utilizar toopreview oferta no Olá [portal de pré-visualização do Azure](https://portal.azure.com).
   
   > [!NOTE]
   > Em caso de máquinas virtuais e modelos de solução,. **não** subscrições da lista branca do tipo CSP, DreamSpark ou do Azure no Open.
   > 
   > 

    > Em caso de máquinas virtuais, ao clicar no botão de Olá **PUSH tooSTAGING**, Olá os seguintes passos é efetuado por trás de cenas Olá. Será progresso de Olá tooview capaz de cada passo no separador de publicar Olá no Olá portal de publicação. Tem de verificar esta página num intervalo regular (até que o estado de Olá mostra teste) para qualquer informação de falha que precisam de correção da sua end.

    > - Em primeiro lugar, o pedido de teste passa toohello equipa de certificação que validar Olá vhd. No entanto, se o pedido tem tem apenas alterações de marketing, em seguida, Olá certificação passo é ignorado.
    > - Após a conclusão da certificação Olá, replicação de início de oferta Olá em todos os Olá centros de dados do Azure. Geralmente, demora 24-48hours para Olá replicação toocomplete mas poderá demorar até tooa semana, consoante o tamanho do vhd Olá Olá. No entanto, se o pedido tem tem apenas alterações de marketing, em seguida, replicação de Olá é mais rápida.
    > - Quando a replicação de Olá estiver concluída, em seguida, oferta Olá estará disponível no Olá [portal do Azure](http:/portal.azure.com). Em Olá esse tempo Estado ficar TESTADO no Olá portal de publicação. Uma oferta pré-configurada está visível no Olá [portal do Azure](http:/portal.azure.com) apenas utilizando Olá indicados de correio eletrónico associados à subscrição Olá preparada com que Olá oferta.

1. Inicie sessão no toohello [portal de pré-visualização do Azure](https://portal.azure.com) utilizando um dos Olá subscrições Azure listadas no passo anterior Olá.
2. Localizar a sua oferta e validar os pontos de imagem VM:
   
   * Certifique-se de que marketing conteúdo apresentado corretamente no Olá Marketplace.
   * Implementação da imagem VM Olá ponto-a-ponto.
     
      ![portal de mapa img](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> A oferta irá permanecer na transição até notificar a Microsoft através do Portal de publicação de Olá [**publicar** separador > clique no botão de Olá **"" pedido de aprovação tooPush tooProduction**] que é toopush pronto tooproduction. Este é um toohave tempo ideal todos os membros da sua equipa de verificação sobre tudo em preparação para a sua oferta vai listadas.
> 
> Olá plataforma de teste foi concebida para teste Olá oferta no modo de pré-visualização por fabricante Olá. É vivamente desencorajar-se utilizar esta platofrm para fins de commerical.
> 
> 

## <a name="next-steps"></a>Passos seguintes
Agora que a oferta é "teste" e testado a sua funcionalidade e conteúdo de marketing, pode avançar publicação final toohello fase, **passo 4**: [implementar toohello sua oferta Marketplace](marketplace-publishing-push-to-production.md).

## <a name="see-also"></a>Consultar também
* [Introdução: como toopublish toohello uma oferta Azure Marketplace](marketplace-publishing-getting-started.md)

