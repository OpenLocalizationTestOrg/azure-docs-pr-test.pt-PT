---
title: aaaCreate um novo recurso do Azure Application Insights | Microsoft Docs
description: "Configure manualmente monitorização do Application Insights para uma nova aplicação em direto."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="4228f-103">Criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="4228f-103">Create an Application Insights resource</span></span>
<span data-ttu-id="4228f-104">Azure Application Insights apresenta dados sobre a sua aplicação num Microsoft Azure *recursos*.</span><span class="sxs-lookup"><span data-stu-id="4228f-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="4228f-105">Criar um novo recurso, por conseguinte, faz parte de [como configurar o Application Insights toomonitor uma nova aplicação][start].</span><span class="sxs-lookup"><span data-stu-id="4228f-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="4228f-106">Em muitos casos, criação de um recurso pode ser efetuado automaticamente Olá IDE.</span><span class="sxs-lookup"><span data-stu-id="4228f-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="4228f-107">Mas em alguns casos, crie um recurso manualmente - por exemplo, toohave recursos separados para programação e produção baseia-se da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="4228f-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="4228f-108">Depois de ter criado os recursos de Olá, obter a chave de instrumentação e utilizar essa Olá tooconfigure SDK na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="4228f-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="4228f-109">ligações de chaves de recurso de Olá Olá recursos toohello de telemetria.</span><span class="sxs-lookup"><span data-stu-id="4228f-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="4228f-110">Inscrever-se tooMicrosoft do Azure</span><span class="sxs-lookup"><span data-stu-id="4228f-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="4228f-111">Se ainda não recebeu um [Microsoft conta, crie uma agora](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="4228f-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="4228f-112">(Se utilizar serviços como o Outlook.com, OneDrive, Windows Phone ou XBox Live, já tiver uma conta Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="4228f-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="4228f-113">Também precisa de uma subscrição demasiado[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="4228f-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="4228f-114">Se a sua equipa ou organização tiver uma subscrição do Azure, Olá proprietário pode adicioná-tooit, utilizando o ID do Windows em direto.</span><span class="sxs-lookup"><span data-stu-id="4228f-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="4228f-115">Apenas a cobrado o que utiliza.</span><span class="sxs-lookup"><span data-stu-id="4228f-115">You're only charged for what you use.</span></span> <span data-ttu-id="4228f-116">plano de básico Olá predefinido permite a uma determinada quantidade de utilização experimental gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="4228f-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="4228f-117">Quando já tem acesso tooa subscrição, inicie sessão no tooApplication Insights em [http://portal.azure.com](https://portal.azure.com)e utilizar o toologin Live ID.</span><span class="sxs-lookup"><span data-stu-id="4228f-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="4228f-118">Criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="4228f-118">Create an Application Insights resource</span></span>
<span data-ttu-id="4228f-119">No Olá [portal.azure.com](https://portal.azure.com), adicione um recurso do Application Insights:</span><span class="sxs-lookup"><span data-stu-id="4228f-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Clicar em Novo, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="4228f-121">**Tipo de aplicação** afeta o que vê no painel de descrição geral de Olá e propriedades de Olá disponíveis no [explorer métrica][metrics].</span><span class="sxs-lookup"><span data-stu-id="4228f-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="4228f-122">Se não vir o seu tipo de aplicação, escolha geral.</span><span class="sxs-lookup"><span data-stu-id="4228f-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="4228f-123">**Subscrição** é a sua conta de pagamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="4228f-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="4228f-124">**Grupo de recursos** está para efeitos práticos para a gestão de propriedades, como o controlo de acesso.</span><span class="sxs-lookup"><span data-stu-id="4228f-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="4228f-125">Se já tiver criado outros recursos do Azure, pode escolher tooput este novo recurso Olá mesmo grupo.</span><span class="sxs-lookup"><span data-stu-id="4228f-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="4228f-126">**Localização** é onde iremos manter os seus dados.</span><span class="sxs-lookup"><span data-stu-id="4228f-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="4228f-127">**PIN toodashboard** coloca um mosaico de acesso de leitura rápida para o seu recurso na sua página de home page do Azure.</span><span class="sxs-lookup"><span data-stu-id="4228f-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="4228f-128">Recomendado.</span><span class="sxs-lookup"><span data-stu-id="4228f-128">Recommended.</span></span>

<span data-ttu-id="4228f-129">Quando a aplicação tiver sido criada, um novo painel abre.</span><span class="sxs-lookup"><span data-stu-id="4228f-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="4228f-130">Este painel é onde ver os dados de utilização de desempenho e sobre a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="4228f-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="4228f-131">tooget back tooit próxima vez que iniciar sessão na tooAzure, procure o mosaico de início rápido da sua aplicação no Olá Iniciar quadro (home ecrã).</span><span class="sxs-lookup"><span data-stu-id="4228f-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="4228f-132">Ou clique em Procurar toofind-lo.</span><span class="sxs-lookup"><span data-stu-id="4228f-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="4228f-133">Copie a chave de instrumentação Olá</span><span class="sxs-lookup"><span data-stu-id="4228f-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="4228f-134">chave de instrumentação Olá identifica recursos de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="4228f-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="4228f-135">Precisa toogive toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="4228f-135">You need it toogive toohello SDK.</span></span>

![Clique em Essentials, clique em Olá chave de instrumentação, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="4228f-137">Instalar Olá SDK na sua aplicação</span><span class="sxs-lookup"><span data-stu-id="4228f-137">Install hello SDK in your app</span></span>
<span data-ttu-id="4228f-138">Instale Olá Application Insights SDK na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="4228f-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="4228f-139">Este passo depende descontos elevados Olá tipo da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="4228f-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="4228f-140">Utilizar tooconfigure de chave de instrumentação Olá [Olá SDK que instalou na sua aplicação][start].</span><span class="sxs-lookup"><span data-stu-id="4228f-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="4228f-141">Olá SDK inclui módulos padrão que enviam telemetria sem ter toowrite qualquer código.</span><span class="sxs-lookup"><span data-stu-id="4228f-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="4228f-142">as ações do utilizador tootrack ou diagnosticar problemas em mais detalhe, [utilizar Olá API] [ api] toosend sua própria telemetria.</span><span class="sxs-lookup"><span data-stu-id="4228f-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="4228f-143"><a name="monitor"></a>Ver dados de telemetria</span><span class="sxs-lookup"><span data-stu-id="4228f-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="4228f-144">Fechar Olá rápido iniciar o painel de aplicações do painel tooreturn tooyour Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4228f-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="4228f-145">Clique em Olá pesquisa mosaico toosee [pesquisa de diagnóstico][diagnostic], onde são apresentados eventos primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="4228f-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="4228f-146">Se está à espera de mais dados, clique em **atualizar** após alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="4228f-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="4228f-147">Criação de um recurso automaticamente</span><span class="sxs-lookup"><span data-stu-id="4228f-147">Creating a resource automatically</span></span>
<span data-ttu-id="4228f-148">Pode escrever um [script do PowerShell](app-insights-powershell.md) toocreate um recurso automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4228f-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4228f-149">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4228f-149">Next steps</span></span>
* [<span data-ttu-id="4228f-150">Criar um dashboard</span><span class="sxs-lookup"><span data-stu-id="4228f-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="4228f-151">Pesquisa de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4228f-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="4228f-152">Explorar métricas</span><span class="sxs-lookup"><span data-stu-id="4228f-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="4228f-153">Escrever consultas da Análise</span><span class="sxs-lookup"><span data-stu-id="4228f-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

