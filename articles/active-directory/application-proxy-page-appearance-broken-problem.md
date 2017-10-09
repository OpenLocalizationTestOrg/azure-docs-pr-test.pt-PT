---
title: "página aaaApplication não ser apresentados corretamente para uma aplicação de Proxy de aplicações | Microsoft Docs"
description: "Documentação de orientação durante a página Olá não está corretamente apresentação de uma aplicação de Proxy de aplicação ter integrado com o Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="52599-103">Página da aplicação não é apresentado corretamente para uma aplicação de Proxy de aplicações</span><span class="sxs-lookup"><span data-stu-id="52599-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="52599-104">Este artigo ajuda-o tootroubleshoot problemas com aplicações de Proxy de aplicações do Azure Active Directory quando navegar toohello página, mas algo na página Olá não ter um aspeto correto.</span><span class="sxs-lookup"><span data-stu-id="52599-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="52599-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="52599-105">Overview</span></span>
<span data-ttu-id="52599-106">Quando publica uma aplicação de Proxy de aplicações, apenas páginas na sua raiz estão acessíveis quando aceder à aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="52599-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="52599-107">Se a página Olá não apresentar corretamente, Olá raiz URL interno utilizado para a aplicação Olá poderá estar em falta alguns recursos de página.</span><span class="sxs-lookup"><span data-stu-id="52599-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="52599-108">tooresolve, certifique-se tiver publicado *todos os* Olá recursos para a página Olá como parte da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="52599-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="52599-109">Pode verificar este é o problema de Olá abrindo o controlador de rede (tais como o Fiddler ou F12 ferramentas no Internet Explorer/Edge), a carregar a página Olá e está à procura de 404 erros.</span><span class="sxs-lookup"><span data-stu-id="52599-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="52599-110">Indica que as páginas de Olá que atualmente não não possível localizar e ainda poderão ter toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="52599-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="52599-111">Como um exemplo de neste caso, partem do princípio de ter publicado uma aplicação de despesas utilizando um URL interno de <http://myapps/expenses>, mas a folha de estilos Olá utiliza a aplicação Olá <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="52599-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="52599-112">Neste caso, Olá folha de estilos não está publicada na sua aplicação, para carregar a aplicação de despesas Olá gerar um erro ao tentar tooload style.css 404.</span><span class="sxs-lookup"><span data-stu-id="52599-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="52599-113">Neste exemplo, seria possível resolver o problema de Olá através da publicação de aplicação Olá com um URL interno de <http://myapp/> em vez disso.</span><span class="sxs-lookup"><span data-stu-id="52599-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="52599-114">Problemas com a publicação como uma aplicação</span><span class="sxs-lookup"><span data-stu-id="52599-114">Problems with publishing as one application</span></span>

<span data-ttu-id="52599-115">Se não for possível toopublish Olá, todos os recursos dentro da mesma aplicação, terá toopublish várias aplicações e ativar as ligações entre eles.</span><span class="sxs-lookup"><span data-stu-id="52599-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="52599-116">toodo por isso, recomendamos a utilização Olá [domínios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solução.</span><span class="sxs-lookup"><span data-stu-id="52599-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="52599-117">No entanto, esta solução requer que detém o certificado de Olá para o seu domínio e as suas aplicações utilizam nomes de domínio completamente qualificado (FQDN).</span><span class="sxs-lookup"><span data-stu-id="52599-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="52599-118">Para outras opções, consulte Olá [resolver problemas de ligações quebrada documentação](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="52599-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52599-119">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="52599-119">Next steps</span></span>
[<span data-ttu-id="52599-120">Publicar aplicações através do Proxy de aplicações do Azure AD</span><span class="sxs-lookup"><span data-stu-id="52599-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
