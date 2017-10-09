---
title: "aaaConfigure as definições de aplicação de função do Azure | Microsoft Docs"
description: "Saiba como tooconfigure do Azure funcionar as definições de aplicação."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="af28a-103">Como toomanage uma aplicação de função Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="af28a-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="af28a-104">As funções do Azure, uma aplicação de função fornece o contexto de execução de Olá para as suas funções individuais.</span><span class="sxs-lookup"><span data-stu-id="af28a-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="af28a-105">Comportamentos de aplicação de função aplicam funções tooall alojadas por uma aplicação de função especificada.</span><span class="sxs-lookup"><span data-stu-id="af28a-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="af28a-106">Este tópico descreve como tooconfigure e gerir as suas aplicações de função no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="af28a-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="af28a-107">toobegin, aceda toohello [portal do Azure](http://portal.azure.com) e iniciar sessão tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="af28a-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="af28a-108">Na barra de pesquisa de Olá, Olá parte superior do portal de Olá, escreva o nome de Olá da sua aplicação de função e selecione-o na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="af28a-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="af28a-109">Depois de selecionar a sua aplicação de função, consulte Olá seguinte página:</span><span class="sxs-lookup"><span data-stu-id="af28a-109">After selecting your function app, you see hello following page:</span></span>

![Descrição geral da aplicação de função no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="af28a-111"><a name="manage-app-service-settings"></a>Separador de definições de aplicação de função</span><span class="sxs-lookup"><span data-stu-id="af28a-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Função descrição geral da aplicação no Olá portal do Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="af28a-113">Olá **definições** separador é onde pode atualizar a versão de runtime de funções de Olá utilizado pela sua aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="af28a-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="af28a-114">Também é onde irá gerir Olá anfitrião as chaves utilizadas toorestrict HTTP acesso tooall funções alojadas pelo Olá aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="af28a-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="af28a-115">As funções suporta o alojamento de consumo e planos de alojamento do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="af28a-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="af28a-116">Para obter mais informações, consulte [plano de serviço correto Olá escolha para as funções do Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="af28a-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="af28a-117">Para melhor previsão no plano de consumo Olá, funções permite-lhe limitar a utilização de plataforma, definindo uma quota de utilização diária, em gigabytes segundos.</span><span class="sxs-lookup"><span data-stu-id="af28a-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="af28a-118">Assim que for atingida a quota de utilização diária Olá, a aplicação de função Olá está parada.</span><span class="sxs-lookup"><span data-stu-id="af28a-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="af28a-119">Uma aplicação de função parada devido a atingir Olá gastos quota pode ser reativada da Olá mesmo contexto como estabelecer Olá diariamente gastos quota.</span><span class="sxs-lookup"><span data-stu-id="af28a-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="af28a-120">Consulte Olá [das funções do Azure a página de preços](http://azure.microsoft.com/pricing/details/functions/) para obter detalhes sobre faturação.</span><span class="sxs-lookup"><span data-stu-id="af28a-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="af28a-121">Separador de funcionalidades de plataforma</span><span class="sxs-lookup"><span data-stu-id="af28a-121">Platform features tab</span></span>

![Separador de funcionalidades de plataforma de aplicação de função.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="af28a-123">Aplicações de função executados na e são mantidas, pela plataforma do App Service do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="af28a-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="af28a-124">Como tal, as aplicações de função tem acesso toomost das funcionalidades de Olá da plataforma de alojamento na web principal do Azure.</span><span class="sxs-lookup"><span data-stu-id="af28a-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="af28a-125">Olá **funcionalidades da plataforma** separador é onde o acesso Olá muitas funcionalidades de Olá plataforma de serviço de aplicações que pode utilizar nas suas aplicações de função.</span><span class="sxs-lookup"><span data-stu-id="af28a-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="af28a-126">Nem todas as funcionalidades do serviço de aplicações estão disponíveis quando uma aplicação de função é executada no plano de alojamento de consumo de Olá.</span><span class="sxs-lookup"><span data-stu-id="af28a-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="af28a-127">resto Olá este tópico centra-se nos Olá seguintes funcionalidades do App Service no Olá portal do Azure que são úteis para as funções:</span><span class="sxs-lookup"><span data-stu-id="af28a-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="af28a-128">Editor de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="af28a-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="af28a-129">Definições da aplicação</span><span class="sxs-lookup"><span data-stu-id="af28a-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="af28a-130">Console</span><span class="sxs-lookup"><span data-stu-id="af28a-130">Console</span></span>](#console)
+ [<span data-ttu-id="af28a-131">Ferramentas Avançadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="af28a-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="af28a-132">Opções de implementação</span><span class="sxs-lookup"><span data-stu-id="af28a-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="af28a-133">CORS</span><span class="sxs-lookup"><span data-stu-id="af28a-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="af28a-134">Autenticação</span><span class="sxs-lookup"><span data-stu-id="af28a-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="af28a-135">Definição da API</span><span class="sxs-lookup"><span data-stu-id="af28a-135">API definition</span></span>](#swagger)

<span data-ttu-id="af28a-136">Para obter mais informações sobre como toowork com definições de serviço de aplicações, consulte [configurar definições de serviço de aplicações do Azure](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="af28a-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="af28a-137"><a name="editor"></a>Editor de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="af28a-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Aplicação de função de editor do serviço de aplicações.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="af28a-139">Olá editor do serviço de aplicações é um editor no portal avançado que pode utilizar os ficheiros de configuração do toomodify JSON e ficheiros de código igual.</span><span class="sxs-lookup"><span data-stu-id="af28a-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="af28a-140">Escolha esta opção inicia um separador de browser separados com um editor de básico.</span><span class="sxs-lookup"><span data-stu-id="af28a-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="af28a-141">Isto permite-lhe toointegrate com o código de execução e depuração do repositório de Git do Olá e modificar as definições de aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="af28a-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="af28a-142">Deste editor fornece um ambiente de desenvolvimento avançado para as suas funções comparada ao painel de aplicação de função do Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="af28a-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![Olá editor do serviço de aplicações](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="af28a-144"><a name="settings"></a>Definições da aplicação</span><span class="sxs-lookup"><span data-stu-id="af28a-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Definições de aplicação de aplicação de função.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="af28a-146">Olá do serviço de aplicações **definições da aplicação** painel é onde pode configurar e gerir versões framework, depuração remota, as definições de aplicação e as cadeias de ligação.</span><span class="sxs-lookup"><span data-stu-id="af28a-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="af28a-147">Quando integrar a sua aplicação de função com outros serviços de terceiros e do Azure, pode modificar essas definições aqui.</span><span class="sxs-lookup"><span data-stu-id="af28a-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configurar as definições da aplicação](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="af28a-149"><a name="console"></a>Consola do</span><span class="sxs-lookup"><span data-stu-id="af28a-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Consola de aplicação de função na Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="af28a-151">consola no portal de Olá é uma ferramenta de programador ideal quando preferir toointeract com a sua aplicação de função a partir da linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="af28a-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="af28a-152">Comandos comuns incluem o diretório e criação de ficheiros e navegação, bem como executar scripts e ficheiros batch.</span><span class="sxs-lookup"><span data-stu-id="af28a-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Consola de aplicação de função](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="af28a-154"><a name="kudu"></a>Ferramentas Avançadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="af28a-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Aplicação de função Kudu no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="af28a-156">Olá ferramentas avançadas para o serviço de aplicações (também conhecido como Kudu) fornecem acesso tooadvanced funcionalidades administrativas da sua aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="af28a-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="af28a-157">Do Kudu, gerir as informações do sistema, as definições de aplicação, as variáveis de ambiente, as extensões de site, os cabeçalhos de HTTP e variáveis de servidor.</span><span class="sxs-lookup"><span data-stu-id="af28a-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="af28a-158">Também pode iniciar **Kudu** navegando toohello SCM o ponto final para a aplicação de função, como`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="af28a-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurar o Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="af28a-160"><a name="deployment">Opções de implementação</span><span class="sxs-lookup"><span data-stu-id="af28a-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opções de implementação de aplicação de função no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="af28a-162">As funções permite-lhe desenvolver o seu código de função no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="af28a-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="af28a-163">Em seguida, pode carregar o tooAzure de projeto de aplicação de função local.</span><span class="sxs-lookup"><span data-stu-id="af28a-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="af28a-164">Além disso tootraditional carregamento FTP, as funções permite-lhe implementar a aplicação de função utilizando soluções de integração contínua popular, como o GitHub, VSTS, Dropbox, Bitbucket e outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="af28a-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="af28a-165">Para obter mais informações, consulte [a implementação contínua para as funções do Azure](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="af28a-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="af28a-166">tooupload manualmente utilizando o FTP ou de local Git, terá também [configurar as suas credenciais de implementação](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="af28a-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="af28a-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="af28a-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Aplicação de função CORS no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="af28a-169">execução de código malicioso tooprevent nos seus serviços, blocos de serviço de aplicações chama tooyour função aplicações a partir de origens externas.</span><span class="sxs-lookup"><span data-stu-id="af28a-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="af28a-170">As funções suporta recursos de várias origens de partilha toolet (CORS), definir uma "lista branca" de permitido origens a partir da qual as suas funções podem aceitar pedidos remotos.</span><span class="sxs-lookup"><span data-stu-id="af28a-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configurar a aplicação de função CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="af28a-172"><a name="auth"></a>Autenticação</span><span class="sxs-lookup"><span data-stu-id="af28a-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Autenticação de aplicação de função no Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="af28a-174">Quando as funções de utilizam um acionador HTTP, pode exigir chamadas toofirst ser autenticado.</span><span class="sxs-lookup"><span data-stu-id="af28a-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="af28a-175">Serviço de aplicações suporta a autenticação do Azure Active Directory e inicie sessão com fornecedores de redes sociais, como o Facebook, a Microsoft e o Twitter.</span><span class="sxs-lookup"><span data-stu-id="af28a-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="af28a-176">Para obter detalhes sobre a configuração de fornecedores de autenticação específicas, consulte [descrição geral da autenticação do App Service do Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af28a-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configurar a autenticação para uma aplicação de função](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="af28a-178"><a name="swagger"></a>Definição da API</span><span class="sxs-lookup"><span data-stu-id="af28a-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![API de aplicação de função swagger de definição de Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="af28a-180">As funções suporta Swagger tooallow clientes toomore consumir facilmente as funções acionadas por HTTP.</span><span class="sxs-lookup"><span data-stu-id="af28a-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="af28a-181">Para obter mais informações sobre como criar definições de API com Swagger, visite [introdução à API Apps, ASP.NET e Swagger no Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="af28a-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="af28a-182">Também pode utilizar os Proxies de funções toodefine uma único superfície de API para várias funções.</span><span class="sxs-lookup"><span data-stu-id="af28a-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="af28a-183">Para obter mais informações, consulte [trabalhar com os Proxies de funções do Azure](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="af28a-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configurar a API da aplicação de função](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="af28a-185">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="af28a-185">Next steps</span></span>

+ [<span data-ttu-id="af28a-186">Configurar as definições do App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="af28a-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="af28a-187">Implementação contínua para Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="af28a-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



