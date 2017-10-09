---
title: "aplicações com suporte para aaaClaims - Proxy de aplicações do Azure AD | Microsoft Docs"
description: "Como toopublish no local as aplicações de ASP.NET que aceitam afirmações do ADFS para acesso remoto seguro pelos seus utilizadores."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="cbbbe-103">Trabalhar com aplicações com suporte para afirmações no Proxy de aplicações</span><span class="sxs-lookup"><span data-stu-id="cbbbe-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="cbbbe-104">[Aplicações com suporte para afirmações](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) efetuar um toohello redirecionamento serviço de Token de segurança (STS).</span><span class="sxs-lookup"><span data-stu-id="cbbbe-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="cbbbe-105">Olá STS os pedidos de credenciais de utilizador de Olá in exchange for um token e redireciona, em seguida, a aplicação de toohello Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="cbbbe-106">Existem algumas formas tooenable Proxy de aplicações toowork com estes redirecionamentos.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="cbbbe-107">Utilize este artigo tooconfigure a implementação para aplicações com suporte para afirmações.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cbbbe-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cbbbe-108">Prerequisites</span></span>
<span data-ttu-id="cbbbe-109">Certifique-se de que Olá STS Olá aplicação com suporte para afirmações redireciona toois disponíveis fora da rede no local.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="cbbbe-110">É possível disponibilizar Olá STS pela sua exposição através de um proxy ou permitindo fora ligações.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="cbbbe-111">Publicar a aplicação</span><span class="sxs-lookup"><span data-stu-id="cbbbe-111">Publish your application</span></span>

1. <span data-ttu-id="cbbbe-112">Publicar a aplicação de acordo com as instruções de toohello descritas em [publicar aplicações com o Proxy de aplicações](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cbbbe-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="cbbbe-113">Navegue até a página de aplicação toohello no Olá portal e selecione **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="cbbbe-114">Se tiver escolhido **do Azure Active Directory** como seu **método de pré-autenticação**, selecione **do Azure AD-início de sessão único desativada** como o **método de autenticação interno**.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="cbbbe-115">Se tiver escolhido **Passthrough** como seu **método de pré-autenticação**, não precisa de toochange qualquer caráter.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="cbbbe-116">A configuração do ADFS</span><span class="sxs-lookup"><span data-stu-id="cbbbe-116">Configure ADFS</span></span>

<span data-ttu-id="cbbbe-117">Pode configurar o AD FS para aplicações com suporte para afirmações de uma das duas formas.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="cbbbe-118">Olá pela primeira vez é através da utilização de domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-118">hello first is by using custom domains.</span></span> <span data-ttu-id="cbbbe-119">segundo é Olá com WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="cbbbe-120">Opção 1: Domínios personalizados</span><span class="sxs-lookup"><span data-stu-id="cbbbe-120">Option 1: Custom domains</span></span>

<span data-ttu-id="cbbbe-121">Se todos os URLs internos de Olá para as aplicações são completamente qualificadas (FQDN) de nomes de domínio, em seguida, pode configurar [domínios personalizados](active-directory-application-proxy-custom-domains.md) para as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="cbbbe-122">Utilize Olá domínios personalizados toocreate URLs externos que são Olá igual ao hello URLs internos.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="cbbbe-123">Quando os URLs externos corresponder ao seu URLs internos, em seguida, redirecionamentos de STS Olá funcionam se os seus utilizadores estão no local ou remoto.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="cbbbe-124">Opção 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="cbbbe-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="cbbbe-125">Abra a gestão do AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="cbbbe-126">Aceda demasiado**confianças da entidade Confiadora**, faça duplo clique na aplicação Olá com o Proxy da aplicação que está a publicar e escolha **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Confianças da entidade confiadora faça duplo clique no nome da aplicação – captura de ecrã](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="cbbbe-128">No Olá **pontos finais** separador em **tipo de ponto final**, selecione **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="cbbbe-129">Em **fidedigna URL**, introduza o URL de Olá que introduziu no Olá Proxy de aplicações em **URL externo** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cbbbe-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Adicionar um ponto final - defina o valor do URL fidedigna - captura de ecrã](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="cbbbe-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cbbbe-131">Next steps</span></span>
* <span data-ttu-id="cbbbe-132">[Ativar o início de sessão único em](application-proxy-sso-overview.md) para aplicações que não suporte para afirmações</span><span class="sxs-lookup"><span data-stu-id="cbbbe-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="cbbbe-133">Ativar aplicações de cliente nativo toointeract com aplicações de proxy</span><span class="sxs-lookup"><span data-stu-id="cbbbe-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


