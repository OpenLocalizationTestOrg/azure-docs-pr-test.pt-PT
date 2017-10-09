---
title: "aaaClient e o servidor SDK controlo de versões em aplicações móveis e dos Mobile Services | Microsoft Docs"
description: "Lista de SDKs de cliente e a compatibilidade com versões do SDK do Mobile Services e as Mobile Apps do Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="baeb0-103">Controlo de versões de cliente e servidor de aplicações móveis e dos Mobile Services</span><span class="sxs-lookup"><span data-stu-id="baeb0-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="baeb0-104">versão mais recente do Olá dos Mobile Services do Azure é Olá **Mobile Apps** funcionalidade do App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="baeb0-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="baeb0-105">Hello do cliente de aplicações móveis e SDKs de servidor são originalmente com base nos Mobile Services, mas são *não* compatíveis entre si.</span><span class="sxs-lookup"><span data-stu-id="baeb0-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="baeb0-106">Ou seja, tem de utilizar um *Mobile Apps* SDK cliente com um *Mobile Apps* SDK do servidor e da mesma forma para *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="baeb0-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="baeb0-107">Este contrato é imposto através de um valor de cabeçalho especial utilizado pelo cliente de Olá e servidor SDKs, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="baeb0-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="baeb0-108">Nota: sempre que este documento refere-se tooa *Mobile Services* back-end, não é necessariamente necessário toobe alojada nos Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="baeb0-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="baeb0-109">É agora possível toomigrate toorun um serviço móvel no serviço de aplicações sem quaisquer alterações de código, mas ainda seria utilizar o serviço Olá *Mobile Services* versões do SDK.</span><span class="sxs-lookup"><span data-stu-id="baeb0-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="baeb0-110">toolearn mais informações sobre como migrar tooApp serviço sem quaisquer alterações de código, consulte o artigo de Olá [migrar tooAzure um serviço móvel do serviço de aplicações].</span><span class="sxs-lookup"><span data-stu-id="baeb0-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="baeb0-111">Especificação de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="baeb0-111">Header specification</span></span>
<span data-ttu-id="baeb0-112">chave de Olá `ZUMO-API-VERSION` pode ser especificado no cabeçalho HTTP de Olá ou cadeia de consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="baeb0-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="baeb0-113">valor de Olá é uma cadeia de versão no formulário de Olá **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="baeb0-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="baeb0-114">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="baeb0-114">For example:</span></span>

<span data-ttu-id="baeb0-115">OBTER https://service.azurewebsites.net/tables/TodoItem</span><span class="sxs-lookup"><span data-stu-id="baeb0-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="baeb0-116">CABEÇALHOS: ZUMO-API-VERSION: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="baeb0-117">PUBLIQUE https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="baeb0-118">Aceitar fora de verificação da versão</span><span class="sxs-lookup"><span data-stu-id="baeb0-118">Opting out of version checking</span></span>
<span data-ttu-id="baeb0-119">Pode ativamente a verificação, definindo um valor de versão **verdadeiro** para definição de aplicação Olá **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="baeb0-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="baeb0-120">Especifique isto no seu Web. config ou no Olá secção definições da aplicação Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="baeb0-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="baeb0-121">Existem várias das alterações de comportamento entre os Mobile Services e as Mobile Apps, especialmente nas áreas de Olá da sincronização offline, a autenticação e notificações push.</span><span class="sxs-lookup"><span data-stu-id="baeb0-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="baeb0-122">Só deve ativamente versão verificação depois de concluída tooensure de teste que estas alterações comportamentais não interromper a funcionalidade da aplicação.</span><span class="sxs-lookup"><span data-stu-id="baeb0-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="baeb0-123">Resumo de compatibilidade para todas as versões</span><span class="sxs-lookup"><span data-stu-id="baeb0-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="baeb0-124">gráfico de Olá abaixo mostra a compatibilidade de Olá entre todos os tipos de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="baeb0-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="baeb0-125">Um back-end é classificado como qualquer uma das Mobile **serviços** ou Mobile **aplicações** com base no servidor de Olá SDK que utiliza.</span><span class="sxs-lookup"><span data-stu-id="baeb0-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="baeb0-126">**Serviços móveis** Node.js ou .NET</span><span class="sxs-lookup"><span data-stu-id="baeb0-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="baeb0-127">**As aplicações móveis** Node.js ou .NET</span><span class="sxs-lookup"><span data-stu-id="baeb0-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baeb0-128">[Clientes de Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="baeb0-128">[Mobile Services clients]</span></span> |<span data-ttu-id="baeb0-129">OK</span><span class="sxs-lookup"><span data-stu-id="baeb0-129">Ok</span></span> |<span data-ttu-id="baeb0-130">Erro\*</span><span class="sxs-lookup"><span data-stu-id="baeb0-130">Error\*</span></span> |
| <span data-ttu-id="baeb0-131">[Clientes de aplicações móveis]</span><span class="sxs-lookup"><span data-stu-id="baeb0-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="baeb0-132">Erro\*</span><span class="sxs-lookup"><span data-stu-id="baeb0-132">Error\*</span></span> |<span data-ttu-id="baeb0-133">OK</span><span class="sxs-lookup"><span data-stu-id="baeb0-133">Ok</span></span> |

<span data-ttu-id="baeb0-134">\*Isto pode ser controlado através da especificação **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="baeb0-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="baeb0-135"><a name="1.0.0"></a>Cliente de Mobile Services e o servidor</span><span class="sxs-lookup"><span data-stu-id="baeb0-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="baeb0-136">o cliente de Olá SDKs na tabela de Olá abaixo são compatíveis com **Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="baeb0-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="baeb0-137">Nota: Olá SDKs do cliente de Mobile Services *não* enviar um valor de cabeçalho `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="baeb0-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="baeb0-138">Se o serviço de Olá receber este cabeçalho ou o valor da cadeia de consulta, será devolvido um erro, a menos que explicitamente optou por terminar, tal como descrito acima.</span><span class="sxs-lookup"><span data-stu-id="baeb0-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="baeb0-139"><a name="MobileServicesClients"></a>Mobile *serviços* SDKs de cliente</span><span class="sxs-lookup"><span data-stu-id="baeb0-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="baeb0-140">Plataforma de cliente</span><span class="sxs-lookup"><span data-stu-id="baeb0-140">Client platform</span></span> | <span data-ttu-id="baeb0-141">Versão</span><span class="sxs-lookup"><span data-stu-id="baeb0-141">Version</span></span> | <span data-ttu-id="baeb0-142">Valor de cabeçalho de versão</span><span class="sxs-lookup"><span data-stu-id="baeb0-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baeb0-143">Cliente gerido (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="baeb0-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="baeb0-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="baeb0-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="baeb0-145">n/d</span><span class="sxs-lookup"><span data-stu-id="baeb0-145">n/a</span></span> |
| <span data-ttu-id="baeb0-146">iOS</span><span class="sxs-lookup"><span data-stu-id="baeb0-146">iOS</span></span> |[<span data-ttu-id="baeb0-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="baeb0-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="baeb0-148">n/d</span><span class="sxs-lookup"><span data-stu-id="baeb0-148">n/a</span></span> |
| <span data-ttu-id="baeb0-149">Android</span><span class="sxs-lookup"><span data-stu-id="baeb0-149">Android</span></span> |[<span data-ttu-id="baeb0-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="baeb0-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="baeb0-151">n/d</span><span class="sxs-lookup"><span data-stu-id="baeb0-151">n/a</span></span> |
| <span data-ttu-id="baeb0-152">HTML</span><span class="sxs-lookup"><span data-stu-id="baeb0-152">HTML</span></span> |[<span data-ttu-id="baeb0-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="baeb0-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="baeb0-154">n/d</span><span class="sxs-lookup"><span data-stu-id="baeb0-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="baeb0-155">Mobile *serviços* SDKs do servidor</span><span class="sxs-lookup"><span data-stu-id="baeb0-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="baeb0-156">Plataforma de servidor</span><span class="sxs-lookup"><span data-stu-id="baeb0-156">Server platform</span></span> | <span data-ttu-id="baeb0-157">Versão</span><span class="sxs-lookup"><span data-stu-id="baeb0-157">Version</span></span> | <span data-ttu-id="baeb0-158">Cabeçalho de versão aceite</span><span class="sxs-lookup"><span data-stu-id="baeb0-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baeb0-159">.NET</span><span class="sxs-lookup"><span data-stu-id="baeb0-159">.NET</span></span> |[<span data-ttu-id="baeb0-160">Versão WindowsAzure.MobileServices.Backend.* 1.0.x</span><span class="sxs-lookup"><span data-stu-id="baeb0-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="baeb0-161">* * Nenhum cabeçalho de versão * *</span><span class="sxs-lookup"><span data-stu-id="baeb0-161">**No version header **</span></span> |
| <span data-ttu-id="baeb0-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="baeb0-162">Node.js</span></span> |<span data-ttu-id="baeb0-163">(brevemente)</span><span class="sxs-lookup"><span data-stu-id="baeb0-163">(coming soon)</span></span> |<span data-ttu-id="baeb0-164">**Não existe um cabeçalho de versão**</span><span class="sxs-lookup"><span data-stu-id="baeb0-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="baeb0-165">Comportamento de back-ends de Mobile Services</span><span class="sxs-lookup"><span data-stu-id="baeb0-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="baeb0-166">VERSÃO DA API DE ZUMO</span><span class="sxs-lookup"><span data-stu-id="baeb0-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="baeb0-167">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="baeb0-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="baeb0-168">Resposta</span><span class="sxs-lookup"><span data-stu-id="baeb0-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baeb0-169">Não foi especificado</span><span class="sxs-lookup"><span data-stu-id="baeb0-169">Not specified</span></span> |<span data-ttu-id="baeb0-170">Qualquer</span><span class="sxs-lookup"><span data-stu-id="baeb0-170">Any</span></span> |<span data-ttu-id="baeb0-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="baeb0-171">200 - OK</span></span> |
| <span data-ttu-id="baeb0-172">Qualquer valor</span><span class="sxs-lookup"><span data-stu-id="baeb0-172">Any value</span></span> |<span data-ttu-id="baeb0-173">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="baeb0-173">True</span></span> |<span data-ttu-id="baeb0-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="baeb0-174">200 - OK</span></span> |
| <span data-ttu-id="baeb0-175">Qualquer valor</span><span class="sxs-lookup"><span data-stu-id="baeb0-175">Any value</span></span> |<span data-ttu-id="baeb0-176">FALSO/não especificado</span><span class="sxs-lookup"><span data-stu-id="baeb0-176">False/Not Specified</span></span> |<span data-ttu-id="baeb0-177">400 - pedido de incorreto</span><span class="sxs-lookup"><span data-stu-id="baeb0-177">400 - Bad Request</span></span> |

## <span data-ttu-id="baeb0-178"><a name="2.0.0"></a>Cliente de Mobile Apps do Azure e do servidor</span><span class="sxs-lookup"><span data-stu-id="baeb0-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="baeb0-179"><a name="MobileAppsClients"></a>Mobile *aplicações* SDKs de cliente</span><span class="sxs-lookup"><span data-stu-id="baeb0-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="baeb0-180">A verificar a versão foi introduzida começadas Olá seguintes versões do SDK do cliente de Olá para **Mobile Apps do Azure**:</span><span class="sxs-lookup"><span data-stu-id="baeb0-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="baeb0-181">Plataforma de cliente</span><span class="sxs-lookup"><span data-stu-id="baeb0-181">Client platform</span></span> | <span data-ttu-id="baeb0-182">Versão</span><span class="sxs-lookup"><span data-stu-id="baeb0-182">Version</span></span> | <span data-ttu-id="baeb0-183">Valor de cabeçalho de versão</span><span class="sxs-lookup"><span data-stu-id="baeb0-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baeb0-184">Cliente gerido (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="baeb0-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="baeb0-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="baeb0-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-186">2.0.0</span></span> |
| <span data-ttu-id="baeb0-187">iOS</span><span class="sxs-lookup"><span data-stu-id="baeb0-187">iOS</span></span> |[<span data-ttu-id="baeb0-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="baeb0-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-189">2.0.0</span></span> |
| <span data-ttu-id="baeb0-190">Android</span><span class="sxs-lookup"><span data-stu-id="baeb0-190">Android</span></span> |[<span data-ttu-id="baeb0-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="baeb0-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="baeb0-193">Mobile *aplicações* SDKs do servidor</span><span class="sxs-lookup"><span data-stu-id="baeb0-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="baeb0-194">A verificar a versão está incluída nos seguintes versões do SDK de servidor:</span><span class="sxs-lookup"><span data-stu-id="baeb0-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="baeb0-195">Plataforma de servidor</span><span class="sxs-lookup"><span data-stu-id="baeb0-195">Server platform</span></span> | <span data-ttu-id="baeb0-196">SDK</span><span class="sxs-lookup"><span data-stu-id="baeb0-196">SDK</span></span> | <span data-ttu-id="baeb0-197">Cabeçalho de versão aceite</span><span class="sxs-lookup"><span data-stu-id="baeb0-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baeb0-198">.NET</span><span class="sxs-lookup"><span data-stu-id="baeb0-198">.NET</span></span> |[<span data-ttu-id="baeb0-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="baeb0-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="baeb0-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-200">2.0.0</span></span> |
| <span data-ttu-id="baeb0-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="baeb0-201">Node.js</span></span> |[<span data-ttu-id="baeb0-202">Azure--aplicações móveis)</span><span class="sxs-lookup"><span data-stu-id="baeb0-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="baeb0-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="baeb0-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="baeb0-204">Comportamento de back-ends de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="baeb0-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="baeb0-205">VERSÃO DA API DE ZUMO</span><span class="sxs-lookup"><span data-stu-id="baeb0-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="baeb0-206">Valor de MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="baeb0-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="baeb0-207">Resposta</span><span class="sxs-lookup"><span data-stu-id="baeb0-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="baeb0-208">x.y.z ou nulo</span><span class="sxs-lookup"><span data-stu-id="baeb0-208">x.y.z or Null</span></span> |<span data-ttu-id="baeb0-209">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="baeb0-209">True</span></span> |<span data-ttu-id="baeb0-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="baeb0-210">200 - OK</span></span> |
| <span data-ttu-id="baeb0-211">Valor nulo</span><span class="sxs-lookup"><span data-stu-id="baeb0-211">Null</span></span> |<span data-ttu-id="baeb0-212">FALSO/não especificado</span><span class="sxs-lookup"><span data-stu-id="baeb0-212">False/Not Specified</span></span> |<span data-ttu-id="baeb0-213">400 - pedido de incorreto</span><span class="sxs-lookup"><span data-stu-id="baeb0-213">400 - Bad Request</span></span> |
| <span data-ttu-id="baeb0-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="baeb0-214">1.x.y</span></span> |<span data-ttu-id="baeb0-215">FALSO/não especificado</span><span class="sxs-lookup"><span data-stu-id="baeb0-215">False/Not Specified</span></span> |<span data-ttu-id="baeb0-216">400 - pedido de incorreto</span><span class="sxs-lookup"><span data-stu-id="baeb0-216">400 - Bad Request</span></span> |
| <span data-ttu-id="baeb0-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="baeb0-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="baeb0-218">FALSO/não especificado</span><span class="sxs-lookup"><span data-stu-id="baeb0-218">False/Not Specified</span></span> |<span data-ttu-id="baeb0-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="baeb0-219">200 - OK</span></span> |
| <span data-ttu-id="baeb0-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="baeb0-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="baeb0-221">FALSO/não especificado</span><span class="sxs-lookup"><span data-stu-id="baeb0-221">False/Not Specified</span></span> |<span data-ttu-id="baeb0-222">400 - pedido de incorreto</span><span class="sxs-lookup"><span data-stu-id="baeb0-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="baeb0-223">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="baeb0-223">Next Steps</span></span>
* <span data-ttu-id="baeb0-224">[migrar tooAzure um serviço móvel do serviço de aplicações]</span><span class="sxs-lookup"><span data-stu-id="baeb0-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Clientes de Mobile Services]: #MobileServicesClients
[Clientes de aplicações móveis]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migrar tooAzure um serviço móvel do serviço de aplicações]: app-service-mobile-migrating-from-mobile-services.md
