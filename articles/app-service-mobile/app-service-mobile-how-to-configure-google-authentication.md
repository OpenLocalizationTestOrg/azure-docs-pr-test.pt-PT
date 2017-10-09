---
title: "aaaHow tooconfigure Google autenticação para a sua aplicação de serviços aplicacionais"
description: "Saiba como tooconfigure Google autenticação para a sua aplicação de serviços de aplicações."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="d7045-103">Como tooconfigure o início de sessão de Google de toouse de aplicação do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="d7045-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="d7045-104">Este tópico mostra como tooconfigure App Service do Azure toouse Google como um fornecedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="d7045-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="d7045-105">procedimento de Olá toocomplete neste tópico, tem de ter uma conta do Google que tenha um endereço de correio eletrónico verificado.</span><span class="sxs-lookup"><span data-stu-id="d7045-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="d7045-106">toocreate uma nova conta do Google, aceda demasiado[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="d7045-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="d7045-107"><a name="register"></a>Registar a aplicação com o Google</span><span class="sxs-lookup"><span data-stu-id="d7045-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="d7045-108">Inicie sessão no toohello [portal do Azure]e navegue tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="d7045-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="d7045-109">Copiar o **URL**, que utiliza a aplicação do Google tooconfigure posterior.</span><span class="sxs-lookup"><span data-stu-id="d7045-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="d7045-110">Navegue toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) Web site, inicie sessão com as credenciais da conta Google, clique em **criar projeto**, forneça um **nome do projeto**, em seguida, clique em  **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d7045-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="d7045-111">Em **APIs sociais** clique **Google + API** e, em seguida, **ativar**.</span><span class="sxs-lookup"><span data-stu-id="d7045-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="d7045-112">No Olá à esquerda de navegação, **credenciais** > **ecrã de consentimento do OAuth**, em seguida, selecione o **endereço de correio eletrónico**, introduza um **denomedeproduto**e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="d7045-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="d7045-113">No Olá **credenciais** separador, clique em **criar credenciais** > **ID de cliente OAuth**, em seguida, selecione **aplicação Web**.</span><span class="sxs-lookup"><span data-stu-id="d7045-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="d7045-114">Colar hello do serviço de aplicações **URL** que copiou anteriormente para **autorizado origens de JavaScript**, em seguida, cole o redirecionamento URI para **autorizado o URI de redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="d7045-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="d7045-115">Olá redirecionamento URI é Olá URL da aplicação acrescentada com o caminho de Olá, */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="d7045-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="d7045-116">Por exemplo, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="d7045-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="d7045-117">Certifique-se de que está a utilizar o esquema HTTPS de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7045-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="d7045-118">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d7045-118">Then click **Create**.</span></span>
7. <span data-ttu-id="d7045-119">No seguinte ecrã de Olá, tome nota dos valores de hello do cliente de Olá segredo de cliente e o ID.</span><span class="sxs-lookup"><span data-stu-id="d7045-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d7045-120">segredo do cliente Olá é uma credencial de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="d7045-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="d7045-121">Não partilhe este segredo com ninguém e distribui-lo dentro de uma aplicação de cliente.</span><span class="sxs-lookup"><span data-stu-id="d7045-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="d7045-122"><a name="secrets"></a>Aplicação do Google adicionar informações tooyour</span><span class="sxs-lookup"><span data-stu-id="d7045-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="d7045-123">Novamente no Olá [portal do Azure], navegue até tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="d7045-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="d7045-124">Clique em **definições**e, em seguida, **autenticação / autorização**.</span><span class="sxs-lookup"><span data-stu-id="d7045-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="d7045-125">Se Olá autenticação / autorização funcionalidade não está ativada, ative o comutador de Olá demasiado**no**.</span><span class="sxs-lookup"><span data-stu-id="d7045-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="d7045-126">Clique em **Google**.</span><span class="sxs-lookup"><span data-stu-id="d7045-126">Click **Google**.</span></span> <span data-ttu-id="d7045-127">Cole valores de ID de aplicação e o segredo de aplicação Olá que obteve anteriormente e, opcionalmente ativar qualquer âmbitos que requer a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d7045-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="d7045-128">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7045-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="d7045-129">Por predefinição, o serviço de aplicações fornece autenticação mas não a restringir o conteúdo de site de tooyour acesso autorizado e APIs.</span><span class="sxs-lookup"><span data-stu-id="d7045-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="d7045-130">Tem de autorizar os utilizadores no seu código de aplicação.</span><span class="sxs-lookup"><span data-stu-id="d7045-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="d7045-131">(Opcional) toorestrict acesso tooyour site tooonly, os utilizadores autenticados pelo Google, defina **ação tootake quando o pedido não é autenticado** demasiado**Google**.</span><span class="sxs-lookup"><span data-stu-id="d7045-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="d7045-132">Isto requer que todos os pedidos de ser autenticados e todos os pedidos não autenticados são tooGoogle redirecionado para a autenticação.</span><span class="sxs-lookup"><span data-stu-id="d7045-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="d7045-133">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d7045-133">Click **Save**.</span></span>

<span data-ttu-id="d7045-134">Agora, está pronto toouse Google para autenticação na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d7045-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="d7045-135"><a name="related-content"></a>Relacionados com o conteúdo</span><span class="sxs-lookup"><span data-stu-id="d7045-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portal do Azure]: https://portal.azure.com/

