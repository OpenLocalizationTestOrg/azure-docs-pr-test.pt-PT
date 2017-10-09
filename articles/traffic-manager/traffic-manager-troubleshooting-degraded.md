---
title: "aaaTroubleshooting degradado Estado no Gestor de tráfego do Azure"
description: "Como os perfis do Gestor de tráfego de tootroubleshoot quando mostra como degradada estado."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="a8e05-103">Resolução de problemas degradado Estado no Gestor de tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e05-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="a8e05-104">Este artigo descreve como tootroubleshoot um perfil do Traffic Manager do Azure que aparece um Estado degradado.</span><span class="sxs-lookup"><span data-stu-id="a8e05-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="a8e05-105">Para este cenário, considere que tiver configurado um perfil do Traffic Manager apontar toosome dos seus serviços cloudapp.net alojado.</span><span class="sxs-lookup"><span data-stu-id="a8e05-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="a8e05-106">Se o estado de funcionamento Olá do Gestor de tráfego apresenta um **Degraded** estado e estado de Olá de um ou mais pontos finais poderá **Degraded**:</span><span class="sxs-lookup"><span data-stu-id="a8e05-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![Estado de degradada ponto final](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="a8e05-108">Se apresenta o estado de funcionamento Olá do Gestor de tráfego um **inativo** Estado, em seguida, ambos os pontos finais poderá **desativado**:</span><span class="sxs-lookup"><span data-stu-id="a8e05-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Estado inativo do Gestor de tráfego](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="a8e05-110">Compreender o Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="a8e05-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="a8e05-111">Gestor de tráfego considera um toobe de ponto final ONLINE apenas quando a pesquisa de Olá recebe uma resposta HTTP 200 fazer uma cópia do caminho de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e05-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="a8e05-112">Quaisquer outra resposta 200 não é uma falha.</span><span class="sxs-lookup"><span data-stu-id="a8e05-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="a8e05-113">Falha um redirecionamento 30 x, mesmo se Olá redirecionado URL devolve um 200.</span><span class="sxs-lookup"><span data-stu-id="a8e05-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="a8e05-114">Para as pesquisas de HTTPs, erros de certificado são ignorados.</span><span class="sxs-lookup"><span data-stu-id="a8e05-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="a8e05-115">conteúdo do real Olá do caminho de pesquisa de Olá irrelevante, desde que é devolvido um 200.</span><span class="sxs-lookup"><span data-stu-id="a8e05-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="a8e05-116">Pesquisar um tipo de conteúdo estático do URL toosome "/ favicon.ico" é uma técnica comuns.</span><span class="sxs-lookup"><span data-stu-id="a8e05-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="a8e05-117">Conteúdo dinâmico, como as páginas ASP de Olá, poderá não sempre devolver 200, mesmo quando a aplicação Olá está em bom estada.</span><span class="sxs-lookup"><span data-stu-id="a8e05-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="a8e05-118">Uma melhor prática é tooset Olá sonda toosomething de caminho que tem suficiente toodetermine de lógica Olá site é cima ou para baixo.</span><span class="sxs-lookup"><span data-stu-id="a8e05-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="a8e05-119">No Olá anterior exemplo, definindo Olá caminho too"/favicon.ico", só são testar essa w3wp.exe está a responder.</span><span class="sxs-lookup"><span data-stu-id="a8e05-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="a8e05-120">Esta pesquisa não pode indicar que a sua aplicação web está em bom estada.</span><span class="sxs-lookup"><span data-stu-id="a8e05-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="a8e05-121">Uma opção melhor seria tooset tooa um caminho algo como "/ Probe.aspx" que tem o estado de funcionamento do lógica toodetermine Olá do site de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e05-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="a8e05-122">Por exemplo, pode utilizar utilização de tooCPU de contadores de desempenho ou medidas Olá número de pedidos falhados.</span><span class="sxs-lookup"><span data-stu-id="a8e05-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="a8e05-123">Ou pode tentar tooaccess recursos de base de dados ou toomake de estado de sessão se a aplicação web de Olá está a funcionar.</span><span class="sxs-lookup"><span data-stu-id="a8e05-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="a8e05-124">Se todos os pontos finais num perfil estão degradados, em seguida, o Gestor de tráfego processa todos os pontos finais como bom estado de funcionamento e pontos finais de tooall de tráfego de rotas.</span><span class="sxs-lookup"><span data-stu-id="a8e05-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="a8e05-125">Este comportamento garante que problemas com Olá pesquisar mecanismo resulta numa falha completa do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="a8e05-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a8e05-126">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="a8e05-126">Troubleshooting</span></span>

<span data-ttu-id="a8e05-127">tootroubleshoot uma falha de pesquisa, precisa de uma ferramenta que mostra o código de estado HTTP Olá retorno do URL de sonda de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e05-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="a8e05-128">Existem várias ferramentas disponíveis que mostram Olá resposta HTTP não processada.</span><span class="sxs-lookup"><span data-stu-id="a8e05-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="a8e05-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="a8e05-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="a8e05-130">curl</span><span class="sxs-lookup"><span data-stu-id="a8e05-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="a8e05-131">wget</span><span class="sxs-lookup"><span data-stu-id="a8e05-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="a8e05-132">Além disso, pode utilizar o separador de rede Olá de Olá ferramentas de depuração F12 nas respostas HTTP do Internet Explorer tooview Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e05-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="a8e05-133">Para este exemplo queremos resposta de Olá toosee do nosso URL de sonda: http://watestsdp2008r2.cloudapp.net:80/sonda.</span><span class="sxs-lookup"><span data-stu-id="a8e05-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="a8e05-134">Olá PowerShell de exemplo a seguir ilustra o problema de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e05-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="a8e05-135">Exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="a8e05-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="a8e05-136">Tenha em atenção que recebemos uma resposta de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="a8e05-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="a8e05-137">Conforme indicado anteriormente, qualquer StatusCode diferente de 200 é considerado uma falha.</span><span class="sxs-lookup"><span data-stu-id="a8e05-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="a8e05-138">Alterações do Traffic Manager Olá tooOffline de estado do ponto final.</span><span class="sxs-lookup"><span data-stu-id="a8e05-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="a8e05-139">problema de Olá tooresolve, tooensure configuração de Web site de Olá de verificação que Olá StatusCode adequada pode ser devolvido a partir do caminho de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8e05-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="a8e05-140">Reconfigure Olá Gestor de tráfego sonda toopoint tooa caminho que devolva uma 200.</span><span class="sxs-lookup"><span data-stu-id="a8e05-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="a8e05-141">Se a sua pesquisa utilizar Olá protocolo HTTPS, poderá ser necessário certificado toodisable verificar erros SSL/TLS tooavoid durante o teste.</span><span class="sxs-lookup"><span data-stu-id="a8e05-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="a8e05-142">Olá seguintes declarações de PowerShell desativar a validação de certificado para a sessão atual do PowerShell Olá:</span><span class="sxs-lookup"><span data-stu-id="a8e05-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="a8e05-143">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="a8e05-143">Next Steps</span></span>

[<span data-ttu-id="a8e05-144">Sobre os métodos de encaminhamento de tráfego do Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="a8e05-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="a8e05-145">O que é o Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="a8e05-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="a8e05-146">Serviços Cloud</span><span class="sxs-lookup"><span data-stu-id="a8e05-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="a8e05-147">Aplicações Web do Azure</span><span class="sxs-lookup"><span data-stu-id="a8e05-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="a8e05-148">Operações do Gestor de Tráfego (Referência da API REST)</span><span class="sxs-lookup"><span data-stu-id="a8e05-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="a8e05-149">[Cmdlets do Gestor de tráfego do Azure][1]</span><span class="sxs-lookup"><span data-stu-id="a8e05-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
