---
title: aaaMap um DNS personalizado existente nome tooAzure Web Apps | Microsoft Docs
description: "Saiba como o nome de tooadd um domínio DNS personalizado existente (domínio intuitivos) tooa web app, back-end da aplicação móvel ou aplicação API no App Service do Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="3ad2e-103">Mapear um existente personalizado DNS nome tooAzure aplicações Web</span><span class="sxs-lookup"><span data-stu-id="3ad2e-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="3ad2e-104">[As Aplicações Web do Azure](app-service-web-overview.md) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="3ad2e-105">Este tutorial mostra como toomap um DNS personalizado existente nome tooAzure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="3ad2e-107">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="3ad2e-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ad2e-108">Mapear um subdomínio (por exemplo, `www.contoso.com`) através da utilização de um registo CNAME</span><span class="sxs-lookup"><span data-stu-id="3ad2e-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="3ad2e-109">Mapear um domínio de raiz (por exemplo, `contoso.com`) através da utilização de um registo</span><span class="sxs-lookup"><span data-stu-id="3ad2e-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="3ad2e-110">Mapear um domínio de caráter universal (por exemplo, `*.contoso.com`) através da utilização de um registo CNAME</span><span class="sxs-lookup"><span data-stu-id="3ad2e-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="3ad2e-111">Mapeamento de domínio com scripts de automatizar</span><span class="sxs-lookup"><span data-stu-id="3ad2e-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="3ad2e-112">Pode utilizar tanto um **registo CNAME** ou um **um registo** toomap um DNS personalizado nome tooApp serviço.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="3ad2e-113">Recomendamos que utilize um CNAME para todos os nomes DNS personalizados, exceto um domínio de raiz (por exemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="3ad2e-114">toomigrate um site em direto e o respetivo tooApp de nome de domínio DNS serviço, consulte o artigo [migrar um Active Directory tooAzure de nome DNS do serviço de aplicações](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ad2e-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3ad2e-115">Prerequisites</span></span>

<span data-ttu-id="3ad2e-116">toocomplete neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="3ad2e-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="3ad2e-117">[Criar uma aplicação do app Service](/azure/app-service/), ou utilizar uma aplicação que criou para outro tutorial.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="3ad2e-118">Adquira um nome de domínio e certifique-se de que tem registo DNS toohello de acesso para o seu fornecedor de domínio (por exemplo, a GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="3ad2e-119">Por exemplo, tooadd as entradas de DNS para `contoso.com` e `www.contoso.com`, tem de ser capaz de tooconfigure definições de DNS de Olá para Olá `contoso.com` domínio de raiz.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3ad2e-120">Se não tiver um domínio existente, nome, considere [aquisição de um domínio utilizando Olá portal do Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="3ad2e-121">Preparar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="3ad2e-121">Prepare hello app</span></span>

<span data-ttu-id="3ad2e-122">toomap um personalizado DNS nome tooa da aplicação web, aplicação web de Olá [plano do App Service](https://azure.microsoft.com/pricing/details/app-service/) tem de ser uma camada paga (**partilhados**, **básico**, **padrão**, ou  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="3ad2e-123">Neste passo, certifique-se de que Olá aplicação fica no Olá do serviço de aplicações suportadas escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="3ad2e-124">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="3ad2e-124">Sign in tooAzure</span></span>

<span data-ttu-id="3ad2e-125">Abra Olá [portal do Azure](https://portal.azure.com) e inicie sessão com a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="3ad2e-126">Navegue até a aplicação de toohello no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3ad2e-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="3ad2e-127">No menu à esquerda de Olá, selecione **serviços aplicacionais**e, em seguida, selecione o nome de Olá da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="3ad2e-129">Pode ver a página de gestão de Olá de Olá aplicação do app Service.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="3ad2e-130">Verifique Olá escalão de preço</span><span class="sxs-lookup"><span data-stu-id="3ad2e-130">Check hello pricing tier</span></span>

<span data-ttu-id="3ad2e-131">No Olá deixado de navegação da página da aplicação Olá, desloque toohello **definições** secção e selecione **aumentar verticalmente (plano do App Service)**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu de dimensionamento](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="3ad2e-133">escalão atual da aplicação Olá é realçado por um limite azul.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="3ad2e-134">Verifique se essa aplicação Olá não está a ser Olá toomake **livres** camada.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="3ad2e-135">DNS personalizado não é suportado no Olá **livres** camada.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Verifique o escalão de preço](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="3ad2e-137">Se hello plano do App Service não está **livres**, fechar Olá **escolher o escalão de preço** página e ignorar demasiado[mapear um registo CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="3ad2e-138">Aumentar verticalmente Olá plano do App Service</span><span class="sxs-lookup"><span data-stu-id="3ad2e-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="3ad2e-139">Selecione qualquer uma das camadas de não livre Olá (**partilhados**, **básico**, **padrão**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="3ad2e-140">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-140">Click **Select**.</span></span>

![Verifique o escalão de preço](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="3ad2e-142">Quando vir Olá seguir notificação, a operação de dimensionamento de Olá está concluída.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Confirmação de operação de escala](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="3ad2e-144">Mapear um registo CNAME</span><span class="sxs-lookup"><span data-stu-id="3ad2e-144">Map a CNAME record</span></span>

<span data-ttu-id="3ad2e-145">Exemplo de tutorial Olá, adicione um registo CNAME para Olá `www` subdomínio (por exemplo, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="3ad2e-146">Criar registo CNAME de Olá</span><span class="sxs-lookup"><span data-stu-id="3ad2e-146">Create hello CNAME record</span></span>

<span data-ttu-id="3ad2e-147">Adicionar um toomap de registo CNAME hostname predefinido de um subdomínio toohello aplicação (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="3ad2e-148">Para Olá `www.contoso.com` exemplo de domínio, adicione um registo CNAME, que mapeia o nome de Olá `www` demasiado`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="3ad2e-149">Depois de adicionar Olá CNAME, página de registos DNS Olá aspeto Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ad2e-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="3ad2e-151">Ativar mapeamento de registo CNAME Olá no Azure</span><span class="sxs-lookup"><span data-stu-id="3ad2e-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="3ad2e-152">No Olá deixada de navegação da página da aplicação Olá num Olá portal do Azure, selecione **domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="3ad2e-154">No Olá **domínios personalizados** página da aplicação Olá, adicionar Olá personalizado nome de DNS completamente qualificado (`www.contoso.com`) toohello lista.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="3ad2e-155">Selecione Olá  **+**  ícone seguinte demasiado**adicionar hostname**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Adicione o nome de anfitrião](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="3ad2e-157">Nome de domínio completamente qualificado do tipo Olá que adicionou um registo CNAME, tais como `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="3ad2e-158">Selecione **validar**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-158">Select **Validate**.</span></span>

<span data-ttu-id="3ad2e-159">Olá **adicionar hostname** botão está ativado.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="3ad2e-160">Certifique-se de que **tipo de registo de nome de anfitrião** estiver definido demasiado**CNAME (www.example.com ou qualquer subdomínio)**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="3ad2e-161">Selecione **adicionar hostname**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-161">Select **Add hostname**.</span></span>

![Adicionar a aplicação de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="3ad2e-163">Poderá demorar algum tempo para toobe Olá novo nome do anfitrião serão refletida da aplicação Olá **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="3ad2e-164">Tente atualizar Olá browser tooupdate Olá dados.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-164">Try refreshing hello browser tooupdate hello data.</span></span>

![Registo CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="3ad2e-166">Se em falta um passo ou enganou algures anteriormente, verá um erro de verificação em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="3ad2e-168">Mapear um registo</span><span class="sxs-lookup"><span data-stu-id="3ad2e-168">Map an A record</span></span>

<span data-ttu-id="3ad2e-169">Exemplo de tutorial Olá, adicione um registo para o domínio de raiz de Olá (por exemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="3ad2e-170">Copie o endereço IP da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="3ad2e-170">Copy hello app's IP address</span></span>

<span data-ttu-id="3ad2e-171">toomap um um registo, terá de endereço IP externo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="3ad2e-172">Pode encontrar este endereço IP da aplicação Olá **domínios personalizados** página Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="3ad2e-173">No Olá deixada de navegação da página da aplicação Olá num Olá portal do Azure, selecione **domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="3ad2e-175">No Olá **domínios personalizados** página, copie o endereço IP da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="3ad2e-177">Criar registo Olá</span><span class="sxs-lookup"><span data-stu-id="3ad2e-177">Create hello A record</span></span>

<span data-ttu-id="3ad2e-178">toomap um um registo tooan aplicação, serviço de aplicações requer **dois** registos DNS:</span><span class="sxs-lookup"><span data-stu-id="3ad2e-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="3ad2e-179">Um **A** registar o endereço IP da aplicação toohello toomap.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="3ad2e-180">A **TXT** registe o nome de anfitrião da aplicação toohello toomap predefinido `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="3ad2e-181">Serviço de aplicações utiliza este registo apenas no momento da configuração, tooverify que é seu domínio personalizado Olá.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="3ad2e-182">Depois do domínio personalizado é validado e configurado no App Service, pode eliminar este registo TXT.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="3ad2e-183">Para Olá `contoso.com` exemplo de domínio, criar registos de A e TXT de Olá toohello a tabela seguinte de acordo com (`@` normalmente representa Olá domínio de raiz).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="3ad2e-184">Tipo de registo</span><span class="sxs-lookup"><span data-stu-id="3ad2e-184">Record type</span></span> | <span data-ttu-id="3ad2e-185">Anfitrião</span><span class="sxs-lookup"><span data-stu-id="3ad2e-185">Host</span></span> | <span data-ttu-id="3ad2e-186">Valor</span><span class="sxs-lookup"><span data-stu-id="3ad2e-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="3ad2e-187">A</span><span class="sxs-lookup"><span data-stu-id="3ad2e-187">A</span></span> | `@` | <span data-ttu-id="3ad2e-188">Endereço IP de [endereço IP da aplicação Olá cópia](#info)</span><span class="sxs-lookup"><span data-stu-id="3ad2e-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="3ad2e-189">TXT</span><span class="sxs-lookup"><span data-stu-id="3ad2e-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="3ad2e-190">Quando são adicionados registos Olá, Olá página de registos DNS aspeto Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ad2e-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![Página de registos DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="3ad2e-192">Ativar Olá um mapeamento de registo na aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="3ad2e-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="3ad2e-193">Novamente da aplicação Olá **domínios personalizados** página no portal do Azure de Olá, adicione Olá personalizado nome de DNS completamente qualificado (por exemplo, `contoso.com`) toohello lista.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="3ad2e-194">Selecione Olá  **+**  ícone seguinte demasiado**adicionar hostname**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Adicione o nome de anfitrião](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="3ad2e-196">Nome de domínio completamente qualificado do tipo Olá que configurou Olá um registo, tais como `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="3ad2e-197">Selecione **validar**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-197">Select **Validate**.</span></span>

<span data-ttu-id="3ad2e-198">Olá **adicionar hostname** botão está ativado.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="3ad2e-199">Certifique-se de que **tipo de registo de nome de anfitrião** estiver definido demasiado**um registo (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="3ad2e-200">Selecione **adicionar hostname**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-200">Select **Add hostname**.</span></span>

![Adicionar a aplicação de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="3ad2e-202">Poderá demorar algum tempo para toobe Olá novo nome do anfitrião serão refletida da aplicação Olá **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="3ad2e-203">Tente atualizar Olá browser tooupdate Olá dados.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Um registo adicionado](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="3ad2e-205">Se em falta um passo ou enganou algures anteriormente, verá um erro de verificação em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="3ad2e-207">Mapear um domínio de caráter universal</span><span class="sxs-lookup"><span data-stu-id="3ad2e-207">Map a wildcard domain</span></span>

<span data-ttu-id="3ad2e-208">Exemplo de tutorial Olá, mapear uma [nome DNS com carateres universais](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (por exemplo, `*.contoso.com`) toohello aplicação do app Service ao adicionar um registo CNAME.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="3ad2e-209">Criar registo CNAME de Olá</span><span class="sxs-lookup"><span data-stu-id="3ad2e-209">Create hello CNAME record</span></span>

<span data-ttu-id="3ad2e-210">Adicionar um toomap de registo CNAME hostname de predefinida da aplicação um caráter universal nome toohello (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="3ad2e-211">Para Olá `*.contoso.com` exemplo de domínio, Olá registo CNAME será mapear o nome de Olá `*` demasiado`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="3ad2e-212">Quando é adicionado Olá CNAME, Olá página de registos DNS aspeto Olá seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ad2e-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="3ad2e-214">Ativar mapeamento de registo CNAME Olá na aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="3ad2e-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="3ad2e-215">Agora pode adicionar qualquer subdomínio que corresponda à aplicação de toohello de nome de caráter universal Olá (por exemplo, `sub1.contoso.com` e `sub2.contoso.com` corresponder `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="3ad2e-216">No Olá deixada de navegação da página da aplicação Olá num Olá portal do Azure, selecione **domínios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="3ad2e-218">Selecione Olá  **+**  ícone seguinte demasiado**adicionar hostname**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Adicione o nome de anfitrião](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="3ad2e-220">Escreva um nome de domínio completamente qualificado que corresponde ao domínio de caráter universal Olá (por exemplo, `sub1.contoso.com`) e, em seguida, selecione **validar**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="3ad2e-221">Olá **adicionar hostname** botão está ativado.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="3ad2e-222">Certifique-se de que **tipo de registo de nome de anfitrião** estiver definido demasiado**registo CNAME (www.example.com ou qualquer subdomínio)**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="3ad2e-223">Selecione **adicionar hostname**.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-223">Select **Add hostname**.</span></span>

![Adicionar a aplicação de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="3ad2e-225">Poderá demorar algum tempo para toobe Olá novo nome do anfitrião serão refletida da aplicação Olá **domínios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="3ad2e-226">Tente atualizar Olá browser tooupdate Olá dados.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="3ad2e-227">Selecione Olá  **+**  ícone novamente tooadd outro nome de anfitrião, que corresponde ao domínio de caráter universal Olá.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="3ad2e-228">Por exemplo, adicionar `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-228">For example, add `sub2.contoso.com`.</span></span>

![Registo CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="3ad2e-230">Teste no browser</span><span class="sxs-lookup"><span data-stu-id="3ad2e-230">Test in browser</span></span>

<span data-ttu-id="3ad2e-231">Procurar toohello nomes DNS que configurou anteriormente (por exemplo, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, e `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="3ad2e-233">Automatizar com scripts</span><span class="sxs-lookup"><span data-stu-id="3ad2e-233">Automate with scripts</span></span>

<span data-ttu-id="3ad2e-234">Pode automatizar a gestão de domínios personalizados com scripts, utilizando Olá [CLI do Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="3ad2e-235">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3ad2e-235">Azure CLI</span></span> 

<span data-ttu-id="3ad2e-236">Olá comando a seguir adiciona um configurado personalizado DNS nome tooan aplicação do app Service.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="3ad2e-237">Para obter mais informações, consulte [mapear uma aplicação de web do domínio personalizado tooa](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="3ad2e-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ad2e-238">Azure PowerShell</span></span> 

<span data-ttu-id="3ad2e-239">Olá comando a seguir adiciona um configurado personalizado DNS nome tooan aplicação do app Service.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="3ad2e-240">Para obter mais informações, consulte [atribuir uma aplicação de web do domínio personalizado tooa](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3ad2e-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ad2e-241">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3ad2e-241">Next steps</span></span>

<span data-ttu-id="3ad2e-242">Neste tutorial, ficou a saber como:</span><span class="sxs-lookup"><span data-stu-id="3ad2e-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3ad2e-243">Mapear um subdomínio através da utilização de um registo CNAME</span><span class="sxs-lookup"><span data-stu-id="3ad2e-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="3ad2e-244">Mapear um domínio de raiz utilizando um registo</span><span class="sxs-lookup"><span data-stu-id="3ad2e-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="3ad2e-245">Mapear um domínio de caráter universal, utilizando um registo CNAME</span><span class="sxs-lookup"><span data-stu-id="3ad2e-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="3ad2e-246">Mapeamento de domínio com scripts de automatizar</span><span class="sxs-lookup"><span data-stu-id="3ad2e-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="3ad2e-247">Avançar toohello toolearn de tutorial seguinte como toobind um SSL personalizado certificado tooa web app.</span><span class="sxs-lookup"><span data-stu-id="3ad2e-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ad2e-248">Vincular um existente personalizado SSL certificado tooAzure aplicações Web</span><span class="sxs-lookup"><span data-stu-id="3ad2e-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
