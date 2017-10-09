---
title: "autenticação de Account Microsoft tooconfigure aaaHow para a sua aplicação de serviços aplicacionais"
description: "Saiba como autenticação de Account Microsoft tooconfigure para a sua aplicação de serviços de aplicações."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="9835c-103">Como tooconfigure o início de sessão de Account Microsoft de toouse de aplicação do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="9835c-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="9835c-104">Este tópico mostra como tooconfigure App Service do Azure toouse Account Microsoft como um fornecedor de autenticação.</span><span class="sxs-lookup"><span data-stu-id="9835c-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="9835c-105"><a name="register-microsoft-account"></a>Registar a sua aplicação com a conta Microsoft</span><span class="sxs-lookup"><span data-stu-id="9835c-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="9835c-106">Inicie sessão no toohello [portal do Azure]e navegue tooyour aplicação.</span><span class="sxs-lookup"><span data-stu-id="9835c-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="9835c-107">Copiar o **URL**que mais tarde, utiliza tooconfigure a aplicação com Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9835c-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="9835c-108">Navegue toohello [aplicações My] página em Olá Microsoft Account Developer Center e inicie sessão com a sua conta Microsoft, se necessário.</span><span class="sxs-lookup"><span data-stu-id="9835c-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="9835c-109">Clique em **adicionar uma aplicação**, em seguida, escreva um nome de aplicação e, em **Criar aplicação**.</span><span class="sxs-lookup"><span data-stu-id="9835c-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="9835c-110">Tome nota do Olá **ID da aplicação**, uma vez que irá precisar dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9835c-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="9835c-111">Em "Plataformas", clique em **adicionar plataforma** e selecione "Web".</span><span class="sxs-lookup"><span data-stu-id="9835c-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="9835c-112">Em "URI de redirecionamento" alimentação Olá ponto final para a sua aplicação, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="9835c-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9835c-113">O redirecionamento URI é Olá URL da aplicação acrescentada com o caminho de Olá, */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="9835c-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="9835c-114">Por exemplo, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="9835c-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="9835c-115">Certifique-se de que está a utilizar o esquema HTTPS de Olá.</span><span class="sxs-lookup"><span data-stu-id="9835c-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="9835c-116">Em "Segredos de aplicação", clique em **gerar a nova palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="9835c-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="9835c-117">Tome nota do valor de Olá que aparece.</span><span class="sxs-lookup"><span data-stu-id="9835c-117">Make note of hello value that appears.</span></span> <span data-ttu-id="9835c-118">Depois de deixar a página Olá, não será novamente apresentado.</span><span class="sxs-lookup"><span data-stu-id="9835c-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9835c-119">palavra-passe de Olá é uma credencial de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="9835c-119">hello password is an important security credential.</span></span> <span data-ttu-id="9835c-120">Não partilhe palavra-passe de Olá com ninguém e distribui-lo dentro de uma aplicação de cliente.</span><span class="sxs-lookup"><span data-stu-id="9835c-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="9835c-121"><a name="secrets"></a>Tooyour de informações de adicionar a conta do Microsoft aplicação de serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="9835c-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="9835c-122">Novamente no Olá [portal do Azure], navegue até tooyour aplicação, clique em **definições** > **autenticação / autorização**.</span><span class="sxs-lookup"><span data-stu-id="9835c-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="9835c-123">Se Olá autenticação / autorização funcionalidade não está ativada, mude- **no**.</span><span class="sxs-lookup"><span data-stu-id="9835c-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="9835c-124">Clique em **conta Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="9835c-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="9835c-125">Colar Olá ID da aplicação e a palavra-passe os valores que obteve anteriormente e, opcionalmente ativar qualquer âmbitos que requer a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9835c-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="9835c-126">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9835c-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="9835c-127">Por predefinição, o serviço de aplicações fornece autenticação mas não a restringir o conteúdo de site de tooyour acesso autorizado e APIs.</span><span class="sxs-lookup"><span data-stu-id="9835c-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="9835c-128">Tem de autorizar os utilizadores no seu código de aplicação.</span><span class="sxs-lookup"><span data-stu-id="9835c-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="9835c-129">(Opcional) toorestrict acesso tooyour site tooonly, os utilizadores autenticados pelo conta Microsoft, defina **ação tootake quando o pedido não é autenticado** demasiado**Account Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="9835c-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="9835c-130">Isto requer que todos os pedidos de ser autenticados e todos os pedidos não autenticados são direcionados tooMicrosoft conta para autenticação.</span><span class="sxs-lookup"><span data-stu-id="9835c-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="9835c-131">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9835c-131">Click **Save**.</span></span>

<span data-ttu-id="9835c-132">Agora, está pronto toouse Account Microsoft para a autenticação na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9835c-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="9835c-133"><a name="related-content"></a>Relacionados com o conteúdo</span><span class="sxs-lookup"><span data-stu-id="9835c-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[aplicações My]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portal do Azure]: https://portal.azure.com/
