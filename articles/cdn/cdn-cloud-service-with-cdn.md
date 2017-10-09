---
title: "aaaIntegrate um serviço em nuvem do Azure com o Azure CDN | Microsoft Docs"
description: "Saiba como toodeploy um serviço em nuvem que serve conteúdo a partir de um ponto de final de CDN do Azure integrado"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="ceb28-103"><a name="intro"></a>Integrar um serviço em nuvem a CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ceb28-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="ceb28-104">Um serviço em nuvem pode ser integrado com a CDN do Azure, que serve qualquer conteúdo da localização do serviço de nuvem a Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="ceb28-105">Este oferece abordagem Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="ceb28-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="ceb28-106">Fácil de implementar e atualizar imagens, scripts e tramas nos diretórios de projeto do seu serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="ceb28-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="ceb28-107">Atualizar facilmente os pacotes de NuGet Olá no seu serviço de nuvem, tais como jQuery ou versões de arranque de configuração</span><span class="sxs-lookup"><span data-stu-id="ceb28-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="ceb28-108">Gerir a sua aplicação Web e o servido CDN conteúdo tudo a partir de Olá mesmo interface de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ceb28-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="ceb28-109">Fluxo de trabalho de implementação unificada para a sua aplicação Web e o conteúdo servido de CDN</span><span class="sxs-lookup"><span data-stu-id="ceb28-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="ceb28-110">Integrar o agrupamento do ASP.NET e minification com CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ceb28-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ceb28-111">O que aprenderá</span><span class="sxs-lookup"><span data-stu-id="ceb28-111">What you will learn</span></span>
<span data-ttu-id="ceb28-112">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="ceb28-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="ceb28-113">Integrar um ponto final de CDN do Azure com o serviço de nuvem e a servir conteúdo estático nas suas páginas Web da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ceb28-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="ceb28-114">Configurar definições da cache de conteúdo estático no seu serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="ceb28-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="ceb28-115">Servir conteúdo das ações de controlador através da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ceb28-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="ceb28-116">Personalizada incluídas e minified conteúdo através da CDN do Azure, mantendo o script de Olá depuração experiência no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ceb28-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="ceb28-117">Configurar a contingência os scripts e CSS quando a CDN do Azure está offline</span><span class="sxs-lookup"><span data-stu-id="ceb28-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="ceb28-118">O que irá criar</span><span class="sxs-lookup"><span data-stu-id="ceb28-118">What you will build</span></span>
<span data-ttu-id="ceb28-119">Irá implementar uma função de Web do serviço de nuvem utilizar a predefinição de Olá modelo MVC do ASP.NET, adicionar conteúdo de tooserve código a partir de uma CDN do Azure integrada, como uma imagem, resultados de ação de controlador e Olá predefinido JavaScript e CSS ficheiros e também escrever Olá tooconfigure de código mecanismo de contingência para pacotes servidos no evento Olá esse Olá CDN está offline.</span><span class="sxs-lookup"><span data-stu-id="ceb28-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="ceb28-120">O que precisa</span><span class="sxs-lookup"><span data-stu-id="ceb28-120">What you will need</span></span>
<span data-ttu-id="ceb28-121">Este tutorial tem Olá os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="ceb28-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="ceb28-122">Um Active Directory [conta do Microsoft Azure](/account/)</span><span class="sxs-lookup"><span data-stu-id="ceb28-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="ceb28-123">Visual Studio 2015 com [SDK do Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="ceb28-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="ceb28-124">Precisa de uma conta do Azure toocomplete neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="ceb28-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="ceb28-125">Pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) -receberá créditos pode utilizar tootry saída paga serviços do Azure e, mesmo depois, pode manter Olá conta e utilizar os serviços do Azure, tais como Web sites gratuitos.</span><span class="sxs-lookup"><span data-stu-id="ceb28-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="ceb28-126">Pode [ativar os benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -sua subscrição do MSDN dá-lhe créditos todos os meses que pode utilizar para serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="ceb28-127">Implementar um serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="ceb28-127">Deploy a cloud service</span></span>
<span data-ttu-id="ceb28-128">Nesta secção, irá implementar predefinido Olá modelo de aplicação de ASP.NET MVC na função de Web do serviço de nuvem do Visual Studio 2015 tooa e, em seguida, integrá-lo com um novo ponto final da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="ceb28-129">Siga as instruções de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="ceb28-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="ceb28-130">No Visual Studio 2015, criar um novo serviço em nuvem do Azure a partir da barra de menu Olá acedendo demasiado**ficheiro > novo > projeto > nuvem > serviço de nuvem do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="ceb28-131">Atribua um nome e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="ceb28-132">Selecione **função da Web ASP.NET** e clique em Olá  **>**  botão.</span><span class="sxs-lookup"><span data-stu-id="ceb28-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="ceb28-133">Clique em OK.</span><span class="sxs-lookup"><span data-stu-id="ceb28-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="ceb28-134">Selecione **MVC** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="ceb28-135">Agora, publica este tooan de função da Web serviço em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="ceb28-136">Clique no projeto de serviço em nuvem Olá e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="ceb28-137">Se ainda não tiver iniciado no Microsoft Azure, clique em Olá **adicionar uma conta...**  Olá pendente e clique em **adicionar uma conta** item de menu.</span><span class="sxs-lookup"><span data-stu-id="ceb28-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="ceb28-138">No início de sessão página Olá, inicie sessão com Olá conta Microsoft que utilizou tooactivate sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="ceb28-139">Assim que tem sessão iniciada, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="ceb28-140">Partindo do princípio que ainda não criou uma conta de armazenamento ou de serviço de nuvem, o Visual Studio irão ajudá-lo a criar ambos.</span><span class="sxs-lookup"><span data-stu-id="ceb28-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="ceb28-141">No Olá **criar serviço de nuvem e de conta** caixa de diálogo, o nome do tipo Olá serviço pretendido e região pretendida Olá selecione.</span><span class="sxs-lookup"><span data-stu-id="ceb28-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="ceb28-142">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="ceb28-143">No Olá publicar a página de definições, verifique a configuração de Olá e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="ceb28-144">processo de publicação Olá para serviços em nuvem demora muito tempo.</span><span class="sxs-lookup"><span data-stu-id="ceb28-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="ceb28-145">Olá ativar Web Deploy para a opção de funções todos os pode tornar a depuração do seu serviço em nuvem muito mais rápido, fornecendo atualizações rápida (mas temporário) tooyour funções da Web.</span><span class="sxs-lookup"><span data-stu-id="ceb28-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="ceb28-146">Para obter mais informações sobre esta opção, consulte [publicação de um serviço em nuvem com as ferramentas do Azure de Olá](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="ceb28-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="ceb28-147">Quando Olá **registo de atividade do Microsoft Azure** mostra que a publicação de estado é **concluído**, irá criar um ponto final da CDN que está integrado com este serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ceb28-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="ceb28-148">Se, após a publicação, o serviço em nuvem Olá implementado apresenta um ecrã de erro, é provável porque está a utilizar o serviço em nuvem Olá implementou um [convidado SO que não inclua a .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="ceb28-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="ceb28-149">Pode contornar este problema por [implementar .NET 4.5.2 como uma tarefa de arranque](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ceb28-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="ceb28-150">Criar um novo perfil da CDN</span><span class="sxs-lookup"><span data-stu-id="ceb28-150">Create a new CDN profile</span></span>
<span data-ttu-id="ceb28-151">Um perfil da CDN é uma coleção de pontos finais da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="ceb28-152">Cada perfil contém um ou mais pontos finais da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="ceb28-153">Pode ser útil toouse vários perfis tooorganize os pontos finais da CDN por domínio de internet, aplicação web ou alguns outros critérios.</span><span class="sxs-lookup"><span data-stu-id="ceb28-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="ceb28-154">Se já tiver um perfil da CDN que pretende que toouse para este tutorial, avance demasiado[criar um novo ponto final da CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="ceb28-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="ceb28-155">Criar um novo ponto final da CDN</span><span class="sxs-lookup"><span data-stu-id="ceb28-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="ceb28-156">**toocreate um novo ponto final da CDN para a sua conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="ceb28-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="ceb28-157">No Olá [Azure Management Portal](https://portal.azure.com), navegue até tooyour perfil da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="ceb28-158">Poderá ter afixou-toohello dashboard no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="ceb28-159">Se não, pode encontrá-lo ao clicar em **procurar**, em seguida, **perfis da CDN**, e clicar no perfil de Olá planear tooadd seu ponto final.</span><span class="sxs-lookup"><span data-stu-id="ceb28-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="ceb28-160">é apresentado o painel do perfil da CDN Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-160">hello CDN profile blade appears.</span></span>
   
    ![Perfil da CDN][cdn-profile-settings]
2. <span data-ttu-id="ceb28-162">Clique em Olá **adicionar ponto final** botão.</span><span class="sxs-lookup"><span data-stu-id="ceb28-162">Click hello **Add Endpoint** button.</span></span>
   
    ![Botão Adicionar ponto final][cdn-new-endpoint-button]
   
    <span data-ttu-id="ceb28-164">Olá **adicionar um ponto final** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="ceb28-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![Painel Adicionar ponto final][cdn-add-endpoint]
3. <span data-ttu-id="ceb28-166">Introduza um **Nome** para este ponto final da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="ceb28-167">Este nome será utilizado tooaccess os recursos em cache no domínio Olá `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="ceb28-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="ceb28-168">No Olá **tipo de origem** lista pendente, selecione *serviço em nuvem*.</span><span class="sxs-lookup"><span data-stu-id="ceb28-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="ceb28-169">No Olá **nome de anfitrião de origem** lista pendente, selecione o seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ceb28-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="ceb28-170">Deixe as predefinições de Olá para **caminho de origem**, **cabeçalho de anfitrião de origem**, e **porta de protocolo/origem**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="ceb28-171">Tem de especificar, pelo menos, um protocolo (HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="ceb28-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="ceb28-172">Clique em Olá **adicionar** botão toocreate Olá novo ponto final.</span><span class="sxs-lookup"><span data-stu-id="ceb28-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="ceb28-173">Assim que for criado o ponto final de Olá, aparece uma lista de pontos finais para Olá perfil.</span><span class="sxs-lookup"><span data-stu-id="ceb28-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="ceb28-174">Vista de lista de Olá mostra Olá URL toouse tooaccess colocados em cache conteúdo, bem como o domínio de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![Ponto final da CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="ceb28-176">Olá ponto final não imediatamente estará disponível para utilização.</span><span class="sxs-lookup"><span data-stu-id="ceb28-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="ceb28-177">Pode demorar até too90 minutos para Olá registo toopropagate através da rede CDN Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="ceb28-178">Os utilizadores que tente imediatamente o nome de domínio do toouse Olá CDN poderão receber o código de estado 404 até que o conteúdo de Olá está disponível através de Olá CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="ceb28-179">Olá teste ponto final de CDN</span><span class="sxs-lookup"><span data-stu-id="ceb28-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="ceb28-180">Quando o estado da publicação de Olá é **concluído**, abra uma janela do browser e navegue até demasiado**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="ceb28-181">Na minha configuração, este URL é:</span><span class="sxs-lookup"><span data-stu-id="ceb28-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="ceb28-182">Que corresponde ao toohello URL de origem no ponto final de CDN Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ceb28-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="ceb28-183">Quando navegar demasiado**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, dependendo do seu browser, será pedido toodownload ou abra Olá bootstrap.css que veio da sua aplicação Web publicada.</span><span class="sxs-lookup"><span data-stu-id="ceb28-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="ceb28-184">Da mesma forma pode aceder a qualquer URL acessível publicamente em  **http://*&lt;serviceName >*.cloudapp.net/**, diretamente a partir do ponto final de CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="ceb28-185">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ceb28-185">For example:</span></span>

* <span data-ttu-id="ceb28-186">Um ficheiro. js a partir do caminho de /Script Olá</span><span class="sxs-lookup"><span data-stu-id="ceb28-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="ceb28-187">Qualquer ficheiro de conteúdo de Olá /Content caminho</span><span class="sxs-lookup"><span data-stu-id="ceb28-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="ceb28-188">Qualquer controlador/ação</span><span class="sxs-lookup"><span data-stu-id="ceb28-188">Any controller/action</span></span>
* <span data-ttu-id="ceb28-189">Se a cadeia de consulta Olá está ativada no ponto final de CDN, qualquer URL com cadeias de consulta</span><span class="sxs-lookup"><span data-stu-id="ceb28-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="ceb28-190">Na verdade, com Olá acima configuração, pode alojar serviço integralmente na nuvem Olá  **http://*&lt;cdnName >*.azureedge.net/**. Se posso navegue demasiado**http://camservice.azureedge.net/ * *, receber resultado da ação de Olá de Home/Index.</span><span class="sxs-lookup"><span data-stu-id="ceb28-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="ceb28-191">Isto não significa que, no entanto, que é sempre tooserve uma boa ideia um serviço integralmente na nuvem através da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="ceb28-192">Uma CDN com otimização de entrega estático não necessariamente acelerar a entrega de elementos dinâmicos que não se destinam toobe em cache ou atualizado muito frequentemente, uma vez que Olá CDN tem de solicitar uma nova versão do recurso de Olá do servidor de origem Olá muito frequentemente.</span><span class="sxs-lookup"><span data-stu-id="ceb28-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="ceb28-193">Para este cenário, pode ativar [aceleração dinâmico do Site](cdn-dynamic-site-acceleration.md) otimização (DSA) no ponto final de CDN que utiliza várias técnicas toospeed segurança entrega de elementos dinâmicos não colocáveis.</span><span class="sxs-lookup"><span data-stu-id="ceb28-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="ceb28-194">Se tiver um site com uma combinação de conteúdo estático e dinâmico, pode escolher tooserve o conteúdo estático de CDN com um tipo de otimização estático (por exemplo, entrega web geral) e o conteúdo dinâmico tooserve diretamente a partir do servidor de origem Olá ou através de uma CDN ponto final com otimização de DSA ativado numa base de maiúsculas e minúsculas, maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ceb28-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="ceb28-195">fim de toothat, já constatou como conteúdo individuais tooaccess ficheiros do ponto final de CDN Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="ceb28-196">Posso irá mostrar como tooserve uma ação de um controlador específico através de um ponto final de CDN específico no servir conteúdo das ações de controlador através da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="ceb28-197">alternativa Olá é toodetermine que conteúdo tooserve da CDN do Azure numa base caso a caso, o serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ceb28-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="ceb28-198">fim de toothat, já constatou como conteúdo individuais tooaccess ficheiros do ponto final de CDN Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="ceb28-199">Posso irá mostrar como tooserve através de uma ação de um controlador específico Olá ponto final de CDN no [servir conteúdo das ações de controlador através do Azure CDN](#controller).</span><span class="sxs-lookup"><span data-stu-id="ceb28-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="ceb28-200">Configurar opções de colocação em cache para ficheiros estáticos no seu serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="ceb28-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="ceb28-201">Com a integração da CDN do Azure no seu serviço em nuvem, pode especificar a forma como pretende estático toobe conteúdo em cache no ponto final de CDN Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="ceb28-202">toodo, abra *Web. config* da função da Web do projeto (por exemplo, WebRole1) e adicione um `<staticContent>` elemento demasiado`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="ceb28-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="ceb28-203">Olá XML abaixo configura Olá cache tooexpire em 3 dias.</span><span class="sxs-lookup"><span data-stu-id="ceb28-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="ceb28-204">Depois de fazê-lo, todos os ficheiros estáticos no seu serviço de nuvem serão observar Olá mesmo regra na sua cache da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="ceb28-205">Para um controlo mais granular das definições da cache, adicione um *Web. config* para uma pasta de ficheiros e adicionar as definições não existe.</span><span class="sxs-lookup"><span data-stu-id="ceb28-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="ceb28-206">Por exemplo, adicionar um *Web. config* ficheiro toohello *\Content* pasta e substitua Olá conteúdo com Olá XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="ceb28-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="ceb28-207">Esta definição faz com que todos os ficheiros estáticos de Olá *\Content* toobe pasta em cache para 15 dias.</span><span class="sxs-lookup"><span data-stu-id="ceb28-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="ceb28-208">Para obter mais informações sobre como tooconfigure Olá `<clientCache>` elemento, consulte [Cache do cliente &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="ceb28-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="ceb28-209">No [servir conteúdo das ações de controlador através do Azure CDN](#controller), posso também irão mostrar como pode configurar definições de cache para resultados de ação de controlador na Olá cache da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="ceb28-210">Servir conteúdo das ações de controlador através da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ceb28-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="ceb28-211">Ao integrar uma função de Web do serviço de nuvem com o CDN do Azure, é relativamente fácil tooserve conteúdo das ações de controlador através de Olá CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="ceb28-212">Que não seja a servir a sua nuvem service diretamente através da CDN do Azure (demonstrados acima), [Maarten Balliauw](https://twitter.com/maartenballiauw) mostra-lhe como toodo-o com um diversão MemeGenerator controlador no [reduzindo a latência na web Olá com Olá CDN do Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="ceb28-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="ceb28-213">Posso irá simplesmente reproduzi-la aqui.</span><span class="sxs-lookup"><span data-stu-id="ceb28-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="ceb28-214">Suponhamos no seu serviço em nuvem que pretende memes toogenerate com base numa imagem Chuck Norris mais novo / (fotografia por [João leve](http://www.flickr.com/photos/alan-light/218493788/)) como esta:</span><span class="sxs-lookup"><span data-stu-id="ceb28-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="ceb28-215">Tiver uma simples `Index` ação que permite que os clientes de Olá superlatives de Olá toospecify na imagem de Olá, em seguida, gera Olá meme depois de serem publique toohello ação.</span><span class="sxs-lookup"><span data-stu-id="ceb28-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="ceb28-216">Uma vez que for Chuck Norris, que seria de esperar toobecome esta página wildly populares global.</span><span class="sxs-lookup"><span data-stu-id="ceb28-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="ceb28-217">Este é um bom exemplo servir conteúdo por dinâmico com CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="ceb28-218">Siga os passos de Olá acima toosetup esta ação de controlador:</span><span class="sxs-lookup"><span data-stu-id="ceb28-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="ceb28-219">No Olá *\Controllers* pasta, crie um novo ficheiro de CS chamado *MemeGeneratorController.cs* e substituir Olá conteúdo com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="ceb28-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="ceb28-220">Ser se tooreplace Olá realçado parte com o nome do CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="ceb28-221">Clique com o botão direito na predefinição Olá `Index()` ação e selecione **Adicionar vista**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="ceb28-222">Aceite as definições de Olá abaixo e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ceb28-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="ceb28-223">Abra Olá novo *Views\MemeGenerator\Index.cshtml* e substitua o conteúdo de Olá Olá seguir simple HTML para submeter superlatives Olá:</span><span class="sxs-lookup"><span data-stu-id="ceb28-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="ceb28-224">Publicar o serviço de nuvem de Olá novamente e navegue demasiado**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** no seu browser.</span><span class="sxs-lookup"><span data-stu-id="ceb28-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="ceb28-225">Quando submete valores de formulário Olá demasiado`/MemeGenerator/Index`, Olá `Index_Post` método da ação devolve uma ligação toohello `Show` método da ação com o identificador de entrada respetivos Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="ceb28-226">Ao clicar em ligação Olá, chegar Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="ceb28-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="ceb28-227">Se está ligado o depurador local, em seguida, irá obter experiência de depuração regular Olá com um local de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="ceb28-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="ceb28-228">Se estiver em execução no serviço de nuvem Olá, em seguida, irá redirecionar para:</span><span class="sxs-lookup"><span data-stu-id="ceb28-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="ceb28-229">Que corresponde ao toohello URL de origem no ponto final de CDN os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ceb28-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="ceb28-230">Em seguida, pode utilizar Olá `OutputCacheAttribute` atributo em Olá `Generate` toospecify método como resultado da ação de Olá deve ser colocados em cache, que irão honrar CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="ceb28-231">código de Olá abaixo especificar uma expiração de cache de 1 hora (3.600 segundos).</span><span class="sxs-lookup"><span data-stu-id="ceb28-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="ceb28-232">Da mesma forma, poderá pode servir segurança conteúdo a partir de qualquer ação do controlador no seu serviço em nuvem através da CDN do Azure, com a opção de colocação em cache Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="ceb28-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="ceb28-233">Na secção seguinte, Olá, posso irá mostrar como tooserve Olá incluídas e minified scripts e CSS através da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="ceb28-234">Integrar o agrupamento do ASP.NET e minification com CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ceb28-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="ceb28-235">Scripts e CSS tramas alterar com pouca frequência e prime candidatos para Olá cache da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="ceb28-236">Servir Olá toda função da Web através da CDN do Azure é toointegrate de forma mais fácil Olá agrupamento e minification com CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="ceb28-237">No entanto, poderá não quiser toodo isto, posso irá mostrar como toodo-preservando Olá pretendido develper experiência de agrupamento do ASP.NET e minification, tal como:</span><span class="sxs-lookup"><span data-stu-id="ceb28-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="ceb28-238">Experiência de modo de depuração excelente</span><span class="sxs-lookup"><span data-stu-id="ceb28-238">Great debug mode experience</span></span>
* <span data-ttu-id="ceb28-239">Implementação simplificada</span><span class="sxs-lookup"><span data-stu-id="ceb28-239">Streamlined deployment</span></span>
* <span data-ttu-id="ceb28-240">Tooclients imediata de atualizações para as atualizações de versão do script/CSS</span><span class="sxs-lookup"><span data-stu-id="ceb28-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="ceb28-241">Mecanismo de contingência quando ocorre uma falha de ponto final de CDN</span><span class="sxs-lookup"><span data-stu-id="ceb28-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="ceb28-242">Minimizar a modificação do código</span><span class="sxs-lookup"><span data-stu-id="ceb28-242">Minimize code modification</span></span>

<span data-ttu-id="ceb28-243">No Olá **WebRole1** projeto que criou no [integrar um ponto final de CDN do Azure com o seu Web site do Azure e a servir conteúdo estático nas suas páginas Web do Azure CDN](#deploy), abra *App_Start\ BundleConfig.cs* e observe Olá `bundles.Add()` chamadas de método.</span><span class="sxs-lookup"><span data-stu-id="ceb28-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="ceb28-244">Olá primeiro `bundles.Add()` instrução adiciona um pacote de scripts no diretório virtual Olá `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="ceb28-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="ceb28-245">Em seguida, abra *Views\Shared\_layout. cshtml* toosee como tag de pacote Olá script é composto.</span><span class="sxs-lookup"><span data-stu-id="ceb28-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="ceb28-246">Deve ser Olá toofind capaz de linha de código Razor os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ceb28-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="ceb28-247">Quando este código Razor é executado na função da Web do Azure de Olá, irá compor um `<script>` etiqueta Olá script seguinte toohello semelhante do pacote:</span><span class="sxs-lookup"><span data-stu-id="ceb28-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="ceb28-248">No entanto, quando for executada no Visual Studio, escrevendo `F5`, irá compor cada ficheiro de script no pacote de Olá individualmente (no caso de Olá acima, apenas um ficheiro de script está no pacote de Olá):</span><span class="sxs-lookup"><span data-stu-id="ceb28-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="ceb28-249">Isto permite-lhe toodebug Olá no código JavaScript no seu ambiente de desenvolvimento ao reduzir as ligações de cliente simultâneas (agrupamento) e melhorando o ficheiro transferir desempenho (minification) na produção.</span><span class="sxs-lookup"><span data-stu-id="ceb28-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="ceb28-250">É um toopreserve funcionalidade excelente com a integração da CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="ceb28-251">Além disso, uma vez que o pacote de Olá composto já contém uma cadeia de versão gerado automaticamente, pretende tooreplicate funcionalidade Olá, por isso, sempre que atualizar a versão de jQuery através do NuGet, pode ser atualizada no lado do cliente de Olá, assim como possíveis.</span><span class="sxs-lookup"><span data-stu-id="ceb28-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="ceb28-252">Siga os passos de Olá abaixo toointegration ASP.NET agrupamento e minification com o ponto final de CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="ceb28-253">Novamente no *App_Start\BundleConfig.cs*, modificar Olá `bundles.Add()` métodos toouse outro [construtor do pacote](http://msdn.microsoft.com/library/jj646464.aspx), que especifica um endereço CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="ceb28-254">toodo Olá, substituir `RegisterBundles` definição de método com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="ceb28-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="ceb28-255">Ser tooreplace se `<yourCDNName>` com nome Olá a CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="ceb28-256">No palavras simples, que define `bundles.UseCdn = true` e adicionar um pacote de tooeach cuidadosamente crafted do URL da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="ceb28-257">Por exemplo, Olá primeiro construtor no código Olá:</span><span class="sxs-lookup"><span data-stu-id="ceb28-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="ceb28-258">é Olá igual ao:</span><span class="sxs-lookup"><span data-stu-id="ceb28-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="ceb28-259">Este construtor indica ao ASP.NET agrupamento e minification toorender ficheiros de script individuais quando debugged localmente, mas utilize Olá especificado CDN endereço tooaccess Olá script em questão.</span><span class="sxs-lookup"><span data-stu-id="ceb28-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="ceb28-260">No entanto, tenha em atenção dois características importantes com este URL CDN cuidadosamente crafted:</span><span class="sxs-lookup"><span data-stu-id="ceb28-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="ceb28-261">Olá origem para este URL CDN é `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, que é realmente Olá diretório virtual do pacote de script de Olá no seu serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ceb28-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="ceb28-262">Uma vez que estiver a utilizar o construtor CDN, Olá tag de script da CDN para pacote Olá já não contém cadeia de versão Olá gerado automaticamente no Olá composto URL.</span><span class="sxs-lookup"><span data-stu-id="ceb28-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="ceb28-263">Tem de gerar manualmente uma cadeia de versão exclusivo sempre que o pacote de script de Olá é modificado tooforce uma cache de perder a sua CDN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="ceb28-264">AT Olá mesmo tempo, esta cadeia de versão exclusivo têm de permanecer constante através de vida de Olá de Olá implementação toomaximize acertos na cache na sua CDN do Azure após a implementação do pacote de Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="ceb28-265">Olá, cadeia de consulta v = < W.X.Y.Z > obtém do *Properties\AssemblyInfo.cs* no seu projeto de função da Web.</span><span class="sxs-lookup"><span data-stu-id="ceb28-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="ceb28-266">Pode ter um fluxo de trabalho de implementação que inclua incrementando versão da assemblagem Olá sempre publicar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ceb28-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="ceb28-267">Em alternativa, pode modificar apenas *Properties\AssemblyInfo.cs* a cadeia de versão do projeto tooautomatically incremento Olá sempre que criar, utilizar o caráter universal de Olá ' *'.</span><span class="sxs-lookup"><span data-stu-id="ceb28-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="ceb28-268">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ceb28-268">For example:</span></span>
     
        <span data-ttu-id="ceb28-269">[assemblagem: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="ceb28-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="ceb28-270">Outro toostreamline estratégia gerar uma cadeia exclusiva de vida de Olá de uma implementação irá funcionar aqui.</span><span class="sxs-lookup"><span data-stu-id="ceb28-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="ceb28-271">Voltar a publicar Olá cloud e acesso de serviço Olá página inicial.</span><span class="sxs-lookup"><span data-stu-id="ceb28-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="ceb28-272">Olá Vista código HTML da página Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="ceb28-273">Deve ser capaz de toosee Olá URL CDN composto, com uma cadeia de versão exclusivo sempre voltar a publicar o serviço de nuvem tooyour de alterações.</span><span class="sxs-lookup"><span data-stu-id="ceb28-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="ceb28-274">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ceb28-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="ceb28-275">No Visual Studio, depurar o serviço em nuvem Olá no Visual Studio, escrevendo `F5`.,</span><span class="sxs-lookup"><span data-stu-id="ceb28-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="ceb28-276">Olá Vista código HTML da página Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="ceb28-277">Verão ainda cada ficheiro de script composto individualmente, para que pode ter uma depuração consistente experiência no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ceb28-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="ceb28-278">Mecanismo de contingência para o URL de CDN</span><span class="sxs-lookup"><span data-stu-id="ceb28-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="ceb28-279">Quando o ponto final de CDN do Azure falha por algum motivo, quer toobe sua página Web smart suficiente tooaccess o servidor de Web de origem como opção de contingência Olá para carregar o JavaScript ou o arranque de configuração.</span><span class="sxs-lookup"><span data-stu-id="ceb28-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="ceb28-280">É suficientemente grave toolose imagens no seu Web site devido a indisponibilidade de tooCDN, mas muito mais grave toolose página fundamental a funcionalidade fornecida pelo seu scripts e tramas.</span><span class="sxs-lookup"><span data-stu-id="ceb28-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="ceb28-281">Olá [pacote](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) classe contém uma propriedade denominada [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) que lhe permitem mecanismo de contingência Olá tooconfigure falha da CDN.</span><span class="sxs-lookup"><span data-stu-id="ceb28-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="ceb28-282">toouse esta propriedade, siga Olá passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="ceb28-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="ceb28-283">No seu projeto de função da Web, abra *App_Start\BundleConfig.cs*, onde adicionou um URL de CDN em cada [construtor do pacote](http://msdn.microsoft.com/library/jj646464.aspx)e efetue o seguinte Olá realçado alterações tooadd mecanismo contingência toohello pacotes de predefinição:</span><span class="sxs-lookup"><span data-stu-id="ceb28-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="ceb28-284">Quando `CdnFallbackExpression` é não nula, script é injetado Olá HTML tootest se o pacote de Olá carregada com êxito e, se não, aceder ao mesmo pacote Olá diretamente a partir do servidor de Web de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="ceb28-285">Esta propriedade tem de toobe conjunto tooa JavaScript expressão que testa se o pacote CDN respetivo Olá é carregado corretamente.</span><span class="sxs-lookup"><span data-stu-id="ceb28-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="ceb28-286">expressão de Olá necessário tootest cada pacote difere de acordo com o toohello conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ceb28-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="ceb28-287">Para pacotes de predefinição Olá acima:</span><span class="sxs-lookup"><span data-stu-id="ceb28-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="ceb28-288">`window.jquery`está definido no jquery-{version}. js</span><span class="sxs-lookup"><span data-stu-id="ceb28-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="ceb28-289">`$.validator`está definido no jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="ceb28-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="ceb28-290">`window.Modernizr`está definido no modernizer-{version}. js</span><span class="sxs-lookup"><span data-stu-id="ceb28-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="ceb28-291">`$.fn.modal`está definido no bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="ceb28-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="ceb28-292">Poderá ter reparado que posso não definido CdnFallbackExpression para Olá `~/Cointent/css` pacote.</span><span class="sxs-lookup"><span data-stu-id="ceb28-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="ceb28-293">Isto acontece porque atualmente não há um [erros nas System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) que injects um `<script>` etiqueta Olá CSS contingência em vez de Olá esperado `<link>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="ceb28-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="ceb28-294">No entanto, há um bom [estilo pacote contingência](https://github.com/EmberConsultingGroup/StyleBundleFallback) oferecidas pelo [Ember consultadoria grupo](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="ceb28-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="ceb28-295">solução de Olá toouse para CSS, crie um novo ficheiro de CS no seu projeto de função de Web *App_Start* pasta denominada *StyleBundleExtensions.cs*e substitua o respetivo conteúdo Olá [código a partir de GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="ceb28-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="ceb28-296">No *App_Start\StyleFundleExtensions.cs*, mudar o nome Olá espaço de nomes tooyour Web nome de função (por exemplo, **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="ceb28-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="ceb28-297">Voltar atrás demasiado`App_Start\BundleConfig.cs` e modificar Olá pela última vez `bundles.Add` instrução com Olá seguir o código realçado:</span><span class="sxs-lookup"><span data-stu-id="ceb28-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="ceb28-298">Este novo método de extensão utiliza Olá ideia mesma tooinject script no Olá HTML toocheck Olá DOM para Olá um nome de classe correspondente, o nome da regra e o valor de regra definido no pacote CSS Olá e o servidor de Web de origem do recai toohello back-se falhar de correspondência de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="ceb28-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="ceb28-299">Publica novamente o serviço de nuvem Olá e Olá home page do acesso.</span><span class="sxs-lookup"><span data-stu-id="ceb28-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="ceb28-300">Olá Vista código HTML da página Olá.</span><span class="sxs-lookup"><span data-stu-id="ceb28-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="ceb28-301">Encontrará scripts injetado semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="ceb28-301">You should find injected scripts similar toohello following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="ceb28-302">Tenha em atenção que o script injetado para Olá CSS pacote contém ainda remnant errant de Olá de Olá `CdnFallbackExpression` propriedade na linha de Olá:</span><span class="sxs-lookup"><span data-stu-id="ceb28-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="ceb28-303">Mas desde Olá primeira parte Olá | | expressão será sempre devolver verdadeira (na linha de Olá diretamente acima que), a função de document.write() Olá nunca irá executar.</span><span class="sxs-lookup"><span data-stu-id="ceb28-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="ceb28-304">Mais Informações</span><span class="sxs-lookup"><span data-stu-id="ceb28-304">More Information</span></span>
* [<span data-ttu-id="ceb28-305">Descrição geral do Olá Azure rede de entrega de conteúdos (CDN)</span><span class="sxs-lookup"><span data-stu-id="ceb28-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="ceb28-306">Utilizar a CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="ceb28-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="ceb28-307">Agrupamento do ASP.NET e Minification</span><span class="sxs-lookup"><span data-stu-id="ceb28-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
