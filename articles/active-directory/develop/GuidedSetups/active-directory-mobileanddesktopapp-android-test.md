---
title: "aaaAzure AD v2 Android introdução - teste | Microsoft Docs"
description: "Como uma aplicação Android pode obter um token de acesso e chamar Graph API do Microsoft ou de APIs que necessitam de tokens de acesso a partir do ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="f8d10-103">Testar o seu código</span><span class="sxs-lookup"><span data-stu-id="f8d10-103">Test your code</span></span>

1. <span data-ttu-id="f8d10-104">Implemente o código tooyour dispositivos/emulador.</span><span class="sxs-lookup"><span data-stu-id="f8d10-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="f8d10-105">Quando estiver pronto tootest, utilize (conta institucional) um Microsoft Azure Active Directory ou uma toosign de conta Account Microsoft (live.com, outlook.com) no.</span><span class="sxs-lookup"><span data-stu-id="f8d10-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="f8d10-106">![Captura de ecrã de exemplo](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="f8d10-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="f8d10-107">
![Início de sessão](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="f8d10-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="f8d10-108">Consentimento</span><span class="sxs-lookup"><span data-stu-id="f8d10-108">Consent</span></span>
<span data-ttu-id="f8d10-109">Olá pela primeira vez que um utilizador inicia sessão numa aplicação tooyour, estes serão apresentados com um ecrã consentimento com semelhante toohello de abaixo, onde têm de aceitar tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="f8d10-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Consentimento](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="f8d10-111">Resultados esperados</span><span class="sxs-lookup"><span data-stu-id="f8d10-111">Expected results</span></span>
<span data-ttu-id="f8d10-112">Deverá ver resultados de Olá de uma chamada de tooMicrosoft Graph API 'me' ponto final utilizado o perfil de utilizador de Olá tootooobtain - https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="f8d10-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="f8d10-113">Para obter uma lista de pontos finais de Microsoft Graph comuns, consulte este [artigo](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="f8d10-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="f8d10-114">Mais informações sobre âmbitos e as permissões delegadas</span><span class="sxs-lookup"><span data-stu-id="f8d10-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="f8d10-115">Olá Microsoft Graph API requer Olá `user.read` âmbito tooread Olá perfil.</span><span class="sxs-lookup"><span data-stu-id="f8d10-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="f8d10-116">Este âmbito é adicionado automaticamente por predefinição em todas as aplicações que está a ser registada no nosso portal de registo.</span><span class="sxs-lookup"><span data-stu-id="f8d10-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="f8d10-117">Algumas outras APIs para o Microsoft Graph, bem como APIs personalizadas para o servidor de back-end poderá exigir âmbitos adicionais.</span><span class="sxs-lookup"><span data-stu-id="f8d10-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="f8d10-118">Por exemplo, para o Microsoft Graph, Olá âmbito `Calendars.Read` é calendários do utilizador Olá toolist necessária.</span><span class="sxs-lookup"><span data-stu-id="f8d10-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="f8d10-119">Ordem tooaccess Olá calendário do utilizador num contexto de uma aplicação, terá de tooadd Olá `Calendars.Read` delegados informações do registo de permissão, toohello aplicação e, em seguida, adicionar Olá `Calendars.Read` âmbito toohello `acquireTokenSilentAsync` chamada.</span><span class="sxs-lookup"><span data-stu-id="f8d10-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="f8d10-120">Olá poderá ser solicitado ao utilizador consents adicionais como aumentar o número de Olá de âmbitos.</span><span class="sxs-lookup"><span data-stu-id="f8d10-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
