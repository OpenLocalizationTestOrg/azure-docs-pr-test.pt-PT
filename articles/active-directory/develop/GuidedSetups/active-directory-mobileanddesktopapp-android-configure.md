---
title: "aaaAzure AD v2 Android introdução - configurar | Microsoft Docs"
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
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="89c7e-103">Criar uma aplicação (rápida)</span><span class="sxs-lookup"><span data-stu-id="89c7e-103">Create an application (Express)</span></span>
<span data-ttu-id="89c7e-104">Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="89c7e-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="89c7e-105">Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="89c7e-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="89c7e-106">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="89c7e-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="89c7e-107">Certifique-se a opção de Olá para a configuração orientado está marcada</span><span class="sxs-lookup"><span data-stu-id="89c7e-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="89c7e-108">Siga o ID da aplicação Olá instruções tooobtain Olá e cole-o para o seu código</span><span class="sxs-lookup"><span data-stu-id="89c7e-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="89c7e-109">Adicionar a sua solução de tooyour de informações de registo de aplicações (avançado)</span><span class="sxs-lookup"><span data-stu-id="89c7e-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="89c7e-110">Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="89c7e-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="89c7e-111">Aceda toohello [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister uma aplicação</span><span class="sxs-lookup"><span data-stu-id="89c7e-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="89c7e-112">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="89c7e-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="89c7e-113">Certifique-se a opção de Olá para a configuração orientado está desmarcada</span><span class="sxs-lookup"><span data-stu-id="89c7e-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="89c7e-114">Clique em `Add Platform`, em seguida, selecione `Native Application` e clique em Guardar</span><span class="sxs-lookup"><span data-stu-id="89c7e-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="89c7e-115">Abra `MainActivity` (em `app`  >  `java`  >   *`{host}.{namespace}`* )</span><span class="sxs-lookup"><span data-stu-id="89c7e-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="89c7e-116">Substitua Olá *[Introduza Olá aplicação Id aqui]* na linha de Olá começadas `final static String CLIENT_ID` com o ID da aplicação Olá apenas registado:</span><span class="sxs-lookup"><span data-stu-id="89c7e-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="89c7e-117">Abra `AndroidManifest.xml` (em `app`  >  `manifests`) Olá adicionar seguir atividade demasiado`manifest\application` nós.</span><span class="sxs-lookup"><span data-stu-id="89c7e-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="89c7e-118">Este procedimento regista um `BrowserTabActivity` tooallow Olá tooresume SO a aplicação depois de concluir a autenticação de Olá:</span><span class="sxs-lookup"><span data-stu-id="89c7e-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
</li>
</ol>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
<span data-ttu-id="89c7e-119">No Olá `BrowserTabActivity`, substitua `[Enter hello application Id here]` com o ID da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="89c7e-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
