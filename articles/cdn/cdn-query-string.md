---
title: aaaControl comportamento da cache com cadeias de consulta do Azure CDN | Microsoft Docs
description: "Cadeia de consulta do Azure CDN controla como os ficheiros são toobe em cache quando estas contêm cadeias de consulta a colocação em cache."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Controlo do Azure CDN comportamento com cadeias de consulta a colocação em cache
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [CDN do Azure Premium da Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Descrição geral
Cadeia de consulta controla como os ficheiros são toobe em cache quando estas contêm cadeias de consulta a colocação em cache.

> [!IMPORTANT]
> Olá produtos Standard e Premium CDN fornecem Olá igual a funcionalidade de colocação em cache de cadeia de consulta, mas difere de interface de utilizador Olá.  Este documento descreve a interface de Olá **CDN do Azure Standard da Akamai** e **CDN do Azure Standard da Verizon**.  Para a cache de cadeia de consulta com **CDN do Azure Premium da Verizon**, consulte [controlar o comportamento de colocação em cache da CDN pedidos com cadeias de consulta - Premium](cdn-query-string-premium.md).
> 
> 

Estão disponíveis três modos de:

* **Ignorar as cadeias de consulta**: Este é o modo predefinido de Olá.  nó de extremidade CDN Olá irá transferir cadeia de consulta Olá de Olá requerente toohello de origem no primeiro pedido efetuado Olá e asset Olá de cache.  Todos os pedidos subsequentes para esse recurso e que são servidos do nó de extremidade Olá irão ignorar a cadeia de consulta Olá até que o elemento em cache Olá expira.
* **Ignorar a colocação em cache para URL com cadeias de consulta**: neste modo, os pedidos com cadeias de consulta não estão em cache no nó de extremidade Olá CDN.  nó de extremidade Olá obtém asset Olá diretamente a partir da origem de Olá e passa-toohello requerente com cada pedido.
* **Colocar em cache todos os URLs únicos**: neste modo processa cada pedido com uma cadeia de consulta como um recurso com a sua própria cache exclusivo.  Por exemplo, Olá resposta da origem de Olá para um pedido para *foo.ashx?q=bar* seria em cache no nó de extremidade Olá e devolvido para caches subsequentes com essa mesma cadeia de consulta.  Um pedido para *foo.ashx?q=somethingelse* deverá ser colocado em cache como um recurso com o seu próprio tempo toolive separado.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Alterar as definições de perfis da CDN padrão a colocação em cache de cadeia de consulta
1. No painel do perfil da CDN Olá, clique em ponto final de CDN Olá desejar toomanage.
   
    ![Pontos finais de painel de perfil CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    é aberto o painel do ponto final da CDN Olá.
2. Clique em Olá **configurar** botão.
   
    ![Botão de gerir do painel do perfil da CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    é aberto o painel de configuração de CDN Olá.
3. Selecione uma definição de Olá **comportamento de colocação em cache de cadeia de consulta** pendente.
   
    ![Cadeia de consulta CDN opções a colocação em cache](./media/cdn-query-string/cdn-query-string.png)
4. Depois de efetuar a seleção, clique em Olá **guardar** botão.

> [!IMPORTANT]
> as alterações de definições de Olá podem não ser imediatamente visíveis como demora algum tempo para Olá registo toopropagate através de Olá CDN.  Para os perfis <b>CDN do Azure da Akamai</b>, a propagação normalmente fica concluída num minuto.  Para os perfis <b>CDN do Azure da Verizon</b>, a propagação normalmente fica concluída no prazo de 90 minutos, mas em certos casos pode demorar mais tempo.
> 
> 

