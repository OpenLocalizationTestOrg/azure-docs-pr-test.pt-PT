---
title: "a compressão do ficheiro de aaaTroubleshooting na CDN do Azure | Microsoft Docs"
description: "Resolva problemas com a compressão do ficheiro de CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="7a264-103">Resolver problemas de compressão de ficheiros CDN</span><span class="sxs-lookup"><span data-stu-id="7a264-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="7a264-104">Este artigo ajuda-o a resolver problemas com [compressão do ficheiro CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="7a264-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="7a264-105">Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no [Olá MSDN Azure e Olá Stack Overflow fóruns](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="7a264-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="7a264-106">Em alternativa, pode também ficheiro um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a264-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="7a264-107">Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **obter suporte**.</span><span class="sxs-lookup"><span data-stu-id="7a264-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="7a264-108">Sintoma</span><span class="sxs-lookup"><span data-stu-id="7a264-108">Symptom</span></span>
<span data-ttu-id="7a264-109">A compressão para o ponto final está ativada, mas os ficheiros estão a ser devolvidos descomprimidos.</span><span class="sxs-lookup"><span data-stu-id="7a264-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="7a264-110">toocheck se os ficheiros estão a ser devolvidos comprimidos, é preciso toouse uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) ou do seu browser [ferramentas de programador](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="7a264-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="7a264-111">Verificação de cabeçalhos de resposta de Olá HTTP devolveu o CDN em cache conteúdos.</span><span class="sxs-lookup"><span data-stu-id="7a264-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="7a264-112">Se houver um cabeçalho com o nome `Content-Encoding` com um valor de **gzip**, **bzip2**, ou **deflate**, o conteúdo é comprimido.</span><span class="sxs-lookup"><span data-stu-id="7a264-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Cabeçalho de codificação de conteúdo](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="7a264-114">Causa</span><span class="sxs-lookup"><span data-stu-id="7a264-114">Cause</span></span>
<span data-ttu-id="7a264-115">Existem várias causas possíveis, incluindo:</span><span class="sxs-lookup"><span data-stu-id="7a264-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="7a264-116">Olá pedida não é elegível para compressão de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="7a264-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="7a264-117">Compressão não está ativada para Olá ficheiro tipo pedido.</span><span class="sxs-lookup"><span data-stu-id="7a264-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="7a264-118">pedido HTTP Olá não inclui um cabeçalho de pedir um tipo de compressão válido.</span><span class="sxs-lookup"><span data-stu-id="7a264-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="7a264-119">Passos de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="7a264-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="7a264-120">Como implementar novo pontos finais, as alterações de configuração da CDN tomar algumas toopropagate tempo através da rede Olá.</span><span class="sxs-lookup"><span data-stu-id="7a264-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="7a264-121">Normalmente, as alterações sejam aplicadas dentro de 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="7a264-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="7a264-122">Se este for Olá pela primeira vez que tiver configurado a compressão para o ponto final CDN, deve considerar a aguardar toobe 1-2 horas se as definições de compressão Olá terem sido propagados toohello POPs.</span><span class="sxs-lookup"><span data-stu-id="7a264-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="7a264-123">Verifique se o pedido de Olá</span><span class="sxs-lookup"><span data-stu-id="7a264-123">Verify hello request</span></span>
<span data-ttu-id="7a264-124">Em primeiro lugar, iremos deve efetuar uma verificação rápida sanity pedido Olá.</span><span class="sxs-lookup"><span data-stu-id="7a264-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="7a264-125">Pode utilizar o seu browser [ferramentas de programador](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview Olá pedidos efetuados.</span><span class="sxs-lookup"><span data-stu-id="7a264-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="7a264-126">Certifique-se de que está a ser enviado o pedido de Olá URL de ponto final de tooyour `<endpointname>.azureedge.net`e não a sua origem.</span><span class="sxs-lookup"><span data-stu-id="7a264-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="7a264-127">Certifique-se de que o pedido de Olá contém um **codificação de aceitar** cabeçalho e Olá valor para essa cabeçalho contém **gzip**, **deflate**, ou **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="7a264-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="7a264-128">**CDN do Azure da Akamai** perfis suporte apenas **gzip** codificação.</span><span class="sxs-lookup"><span data-stu-id="7a264-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Cabeçalhos de pedido CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="7a264-130">Verifique as definições de compressão (perfil de Standard CDN)</span><span class="sxs-lookup"><span data-stu-id="7a264-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="7a264-131">Este passo aplica-se apenas se o perfil de CDN é uma **CDN do Azure Standard da Verizon** ou **CDN do Azure Standard da Akamai** perfil.</span><span class="sxs-lookup"><span data-stu-id="7a264-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="7a264-132">Navegue tooyour no ponto final em Olá [portal do Azure](https://portal.azure.com) e clique em Olá **configurar** botão.</span><span class="sxs-lookup"><span data-stu-id="7a264-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="7a264-133">Certifique-se de que a compressão está ativada.</span><span class="sxs-lookup"><span data-stu-id="7a264-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="7a264-134">Verifique se o tipo de MIME Olá Olá conteúdo toobe comprimido está incluído na lista de Olá dos formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="7a264-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Definições de compressão de CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="7a264-136">Verifique as definições de compressão (perfil de Premium CDN)</span><span class="sxs-lookup"><span data-stu-id="7a264-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="7a264-137">Este passo aplica-se apenas se o perfil de CDN é uma **CDN do Azure Premium da Verizon** perfil.</span><span class="sxs-lookup"><span data-stu-id="7a264-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="7a264-138">Navegue tooyour no ponto final em Olá [portal do Azure](https://portal.azure.com) e clique em Olá **gerir** botão.</span><span class="sxs-lookup"><span data-stu-id="7a264-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="7a264-139">portal suplementar Olá irá abrir.</span><span class="sxs-lookup"><span data-stu-id="7a264-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="7a264-140">Paire sobre Olá **HTTP grande** separador, em seguida, paire sobre Olá **definições da Cache** flyout.</span><span class="sxs-lookup"><span data-stu-id="7a264-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="7a264-141">Clique em **compressão**.</span><span class="sxs-lookup"><span data-stu-id="7a264-141">Click **Compression**.</span></span> 

* <span data-ttu-id="7a264-142">Certifique-se de que a compressão está ativada.</span><span class="sxs-lookup"><span data-stu-id="7a264-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="7a264-143">Certifique-se Olá **tipos de ficheiro** lista contém uma lista separada por vírgulas (sem espaços) de tipos de MIME.</span><span class="sxs-lookup"><span data-stu-id="7a264-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="7a264-144">Verifique se o tipo de MIME Olá Olá conteúdo toobe comprimido está incluído na lista de Olá dos formatos comprimidos.</span><span class="sxs-lookup"><span data-stu-id="7a264-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Definições de compressão CDN premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="7a264-146">Certifique-se de que o conteúdo de Olá é colocado em cache</span><span class="sxs-lookup"><span data-stu-id="7a264-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="7a264-147">Este passo aplica-se apenas se o perfil de CDN é uma **CDN do Azure da Verizon** perfil (Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="7a264-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="7a264-148">Utilizar ferramentas de programador do seu browser, verifique o ficheiro a Olá da tooensure de cabeçalhos de resposta de Olá é colocado em cache na região de olá onde está a ser pedida.</span><span class="sxs-lookup"><span data-stu-id="7a264-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="7a264-149">Verifique Olá **servidor** cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="7a264-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="7a264-150">cabeçalho de Olá deve ter o formato de Olá **Platform (servidor/POP ID)**, como mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="7a264-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="7a264-151">Verifique Olá **X-Cache** cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="7a264-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="7a264-152">deve ler o cabeçalho de Olá **ACESSOS**.</span><span class="sxs-lookup"><span data-stu-id="7a264-152">hello header should read **HIT**.</span></span>  

![Cabeçalhos de resposta CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="7a264-154">Certifique-se de que o ficheiro de Olá cumpre os requisitos de tamanho de Olá</span><span class="sxs-lookup"><span data-stu-id="7a264-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="7a264-155">Este passo aplica-se apenas se o perfil de CDN é uma **CDN do Azure da Verizon** perfil (Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="7a264-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="7a264-156">toobe elegível para compressão, um ficheiro tem de cumprir os requisitos de tamanho de Olá:</span><span class="sxs-lookup"><span data-stu-id="7a264-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="7a264-157">Maior do que 128 bytes.</span><span class="sxs-lookup"><span data-stu-id="7a264-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="7a264-158">Menor que 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7a264-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="7a264-159">Verificar a solicitação de Olá no servidor de origem Olá para um **através de** cabeçalho</span><span class="sxs-lookup"><span data-stu-id="7a264-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="7a264-160">Olá **através de** cabeçalho de HTTP indica o servidor de web de toohello Olá pedido está a ser transferida por um servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="7a264-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="7a264-161">Os servidores web do Microsoft IIS por predefinição não comprimir respostas quando Olá pedido contém um **através de** cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="7a264-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="7a264-162">toooverride este comportamento, efetue Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="7a264-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="7a264-163">**IIS 6**: [definir HcNoCompressionForProxies = "FALSE" nas propriedades de Metabase do IIS Olá](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="7a264-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="7a264-164">**IIS 7 e até**: [definidas **noCompressionForHttp10** e **noCompressionForProxies** tooFalse numa configuração de servidor Olá](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="7a264-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

