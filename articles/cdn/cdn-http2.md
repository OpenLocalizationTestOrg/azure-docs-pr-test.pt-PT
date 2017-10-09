---
title: suporte de aaaHTTP/2 na CDN do Azure | Microsoft Docs
description: Saiba mais sobre o suporte HTTP/2 e CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="c1c94-103">Suporte HTTP/2 na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="c1c94-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="c1c94-104">HTTP/2 é tooHTTP/1.1\ uma revisão principal.</span><span class="sxs-lookup"><span data-stu-id="c1c94-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="c1c94-105">Fornece mais rapidamente do desempenho da web, tempo de resposta reduzida e melhorada experiência do utilizador, mantendo os métodos HTTP familiares Olá, códigos de estado e semântica.</span><span class="sxs-lookup"><span data-stu-id="c1c94-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="c1c94-106">Apesar de HTTP/2 toowork concebida com HTTP e HTTPS, muitos browsers do cliente suportam apenas HTTP/2 sobre TLS.</span><span class="sxs-lookup"><span data-stu-id="c1c94-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="c1c94-107">Vantagens HTTP/2</span><span class="sxs-lookup"><span data-stu-id="c1c94-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="c1c94-108">benefícios Olá de HTTP/2 incluem:</span><span class="sxs-lookup"><span data-stu-id="c1c94-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="c1c94-109">**Multiplexação e simultaneidade**</span><span class="sxs-lookup"><span data-stu-id="c1c94-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="c1c94-110">Utilizar HTTP 1.1, vários tornar vários pedidos de recursos requer várias ligações TCP e cada ligação tem uma tolerância de desempenho associada ao mesmo.</span><span class="sxs-lookup"><span data-stu-id="c1c94-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="c1c94-111">HTTP/2 permite vários recursos toobe, pedida numa única ligação TCP.</span><span class="sxs-lookup"><span data-stu-id="c1c94-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="c1c94-112">**Compressão de cabeçalho**</span><span class="sxs-lookup"><span data-stu-id="c1c94-112">**Header compression**</span></span>

    <span data-ttu-id="c1c94-113">Através da compressão de cabeçalhos de Olá HTTP servidos recursos, hora de transmissão de Olá é significativamente reduzida.</span><span class="sxs-lookup"><span data-stu-id="c1c94-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="c1c94-114">**Dependências de sequência**</span><span class="sxs-lookup"><span data-stu-id="c1c94-114">**Stream dependencies**</span></span>

    <span data-ttu-id="c1c94-115">Dependências de sequência permitem ao cliente Olá tooindicate toohello servidor que recursos tem prioridade.</span><span class="sxs-lookup"><span data-stu-id="c1c94-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="c1c94-116">Suporte de browsers HTTP/2</span><span class="sxs-lookup"><span data-stu-id="c1c94-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="c1c94-117">Todos os browsers principais Olá tem implementada HTTP/2 suporte das respetivas versões atuais.</span><span class="sxs-lookup"><span data-stu-id="c1c94-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="c1c94-118">Browsers suportados não serão automaticamente contingência tooHTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="c1c94-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="c1c94-119">Browser</span><span class="sxs-lookup"><span data-stu-id="c1c94-119">Browser</span></span>|<span data-ttu-id="c1c94-120">Versão mínima</span><span class="sxs-lookup"><span data-stu-id="c1c94-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="c1c94-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="c1c94-121">Microsoft Edge</span></span>| <span data-ttu-id="c1c94-122">12</span><span class="sxs-lookup"><span data-stu-id="c1c94-122">12</span></span>|
|<span data-ttu-id="c1c94-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="c1c94-123">Google Chrome</span></span>| <span data-ttu-id="c1c94-124">43</span><span class="sxs-lookup"><span data-stu-id="c1c94-124">43</span></span>|
|<span data-ttu-id="c1c94-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="c1c94-125">Mozilla Firefox</span></span>| <span data-ttu-id="c1c94-126">38</span><span class="sxs-lookup"><span data-stu-id="c1c94-126">38</span></span>|
|<span data-ttu-id="c1c94-127">Opera</span><span class="sxs-lookup"><span data-stu-id="c1c94-127">Opera</span></span>| <span data-ttu-id="c1c94-128">32</span><span class="sxs-lookup"><span data-stu-id="c1c94-128">32</span></span>|
|<span data-ttu-id="c1c94-129">Safari</span><span class="sxs-lookup"><span data-stu-id="c1c94-129">Safari</span></span>| <span data-ttu-id="c1c94-130">9</span><span class="sxs-lookup"><span data-stu-id="c1c94-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="c1c94-131">Ativar o suporte HTTP/2 na CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="c1c94-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="c1c94-132">Atualmente está ativo para o suporte HTTP/2 **CDN do Azure da Akamai** e **CDN do Azure da Verizon** perfis.</span><span class="sxs-lookup"><span data-stu-id="c1c94-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="c1c94-133">Nenhuma ação adicional é necessária de clientes.</span><span class="sxs-lookup"><span data-stu-id="c1c94-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="c1c94-134">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="c1c94-134">Next Steps</span></span>

<span data-ttu-id="c1c94-135">vantagens de Olá toosee de HTTP/2 em ação, consulte [esta demonstração da Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="c1c94-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="c1c94-136">toolearn mais informações sobre HTTP/2, visite Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="c1c94-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="c1c94-137">Home page de especificação de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="c1c94-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="c1c94-138">Oficial HTTP/2 FAQ</span><span class="sxs-lookup"><span data-stu-id="c1c94-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="c1c94-139">Informações da Akamai HTTP/2</span><span class="sxs-lookup"><span data-stu-id="c1c94-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="c1c94-140">toolearn mais informações sobre as funcionalidades disponíveis da CDN do Azure, consulte Olá [descrição geral da CDN do Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="c1c94-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
