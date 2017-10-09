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
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="1d3c0-103">Controlo do Azure CDN comportamento com cadeias de consulta a colocação em cache</span><span class="sxs-lookup"><span data-stu-id="1d3c0-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d3c0-104">Standard</span><span class="sxs-lookup"><span data-stu-id="1d3c0-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="1d3c0-105">CDN do Azure Premium da Verizon</span><span class="sxs-lookup"><span data-stu-id="1d3c0-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1d3c0-106">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="1d3c0-106">Overview</span></span>
<span data-ttu-id="1d3c0-107">Cadeia de consulta controla como os ficheiros são toobe em cache quando estas contêm cadeias de consulta a colocação em cache.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d3c0-108">Olá produtos Standard e Premium CDN fornecem Olá igual a funcionalidade de colocação em cache de cadeia de consulta, mas difere de interface de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="1d3c0-109">Este documento descreve a interface de Olá **CDN do Azure Standard da Akamai** e **CDN do Azure Standard da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-109">This document describes hello interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="1d3c0-110">Para a cache de cadeia de consulta com **CDN do Azure Premium da Verizon**, consulte [controlar o comportamento de colocação em cache da CDN pedidos com cadeias de consulta - Premium](cdn-query-string-premium.md).</span><span class="sxs-lookup"><span data-stu-id="1d3c0-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="1d3c0-111">Estão disponíveis três modos de:</span><span class="sxs-lookup"><span data-stu-id="1d3c0-111">Three modes are available:</span></span>

* <span data-ttu-id="1d3c0-112">**Ignorar as cadeias de consulta**: Este é o modo predefinido de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-112">**Ignore query strings**:  This is hello default mode.</span></span>  <span data-ttu-id="1d3c0-113">nó de extremidade CDN Olá irá transferir cadeia de consulta Olá de Olá requerente toohello de origem no primeiro pedido efetuado Olá e asset Olá de cache.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="1d3c0-114">Todos os pedidos subsequentes para esse recurso e que são servidos do nó de extremidade Olá irão ignorar a cadeia de consulta Olá até que o elemento em cache Olá expira.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="1d3c0-115">**Ignorar a colocação em cache para URL com cadeias de consulta**: neste modo, os pedidos com cadeias de consulta não estão em cache no nó de extremidade Olá CDN.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="1d3c0-116">nó de extremidade Olá obtém asset Olá diretamente a partir da origem de Olá e passa-toohello requerente com cada pedido.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="1d3c0-117">**Colocar em cache todos os URLs únicos**: neste modo processa cada pedido com uma cadeia de consulta como um recurso com a sua própria cache exclusivo.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="1d3c0-118">Por exemplo, Olá resposta da origem de Olá para um pedido para *foo.ashx?q=bar* seria em cache no nó de extremidade Olá e devolvido para caches subsequentes com essa mesma cadeia de consulta.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="1d3c0-119">Um pedido para *foo.ashx?q=somethingelse* deverá ser colocado em cache como um recurso com o seu próprio tempo toolive separado.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="1d3c0-120">Alterar as definições de perfis da CDN padrão a colocação em cache de cadeia de consulta</span><span class="sxs-lookup"><span data-stu-id="1d3c0-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="1d3c0-121">No painel do perfil da CDN Olá, clique em ponto final de CDN Olá desejar toomanage.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-121">From hello CDN profile blade, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Pontos finais de painel de perfil CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="1d3c0-123">é aberto o painel do ponto final da CDN Olá.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-123">hello CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="1d3c0-124">Clique em Olá **configurar** botão.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-124">Click hello **Configure** button.</span></span>
   
    ![Botão de gerir do painel do perfil da CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="1d3c0-126">é aberto o painel de configuração de CDN Olá.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-126">hello CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="1d3c0-127">Selecione uma definição de Olá **comportamento de colocação em cache de cadeia de consulta** pendente.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-127">Select a setting from hello **Query string caching behavior** dropdown.</span></span>
   
    ![Cadeia de consulta CDN opções a colocação em cache](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="1d3c0-129">Depois de efetuar a seleção, clique em Olá **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-129">After making your selection, click hello **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d3c0-130">as alterações de definições de Olá podem não ser imediatamente visíveis como demora algum tempo para Olá registo toopropagate através de Olá CDN.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-130">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="1d3c0-131">Para os perfis <b>CDN do Azure da Akamai</b>, a propagação normalmente fica concluída num minuto.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="1d3c0-132">Para os perfis <b>CDN do Azure da Verizon</b>, a propagação normalmente fica concluída no prazo de 90 minutos, mas em certos casos pode demorar mais tempo.</span><span class="sxs-lookup"><span data-stu-id="1d3c0-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

