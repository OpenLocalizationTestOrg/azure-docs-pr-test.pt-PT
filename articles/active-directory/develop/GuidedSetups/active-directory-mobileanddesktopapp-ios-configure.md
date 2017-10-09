---
title: "Introdução de aaaAzure AD v2 iOS - configurar | Microsoft Docs"
description: "Como as aplicações do iOS (Swift) podem chamar uma API que necessitam de tokens de acesso ao ponto final do Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="9d4f1-103">Criar uma aplicação (rápida)</span><span class="sxs-lookup"><span data-stu-id="9d4f1-103">Create an application (Express)</span></span>
<span data-ttu-id="9d4f1-104">Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="9d4f1-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="9d4f1-105">Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="9d4f1-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="9d4f1-106">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="9d4f1-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="9d4f1-107">Certifique-se a opção de Olá para a configuração orientado está marcada</span><span class="sxs-lookup"><span data-stu-id="9d4f1-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="9d4f1-108">Siga o ID da aplicação Olá instruções tooobtain Olá e cole-o para o seu código</span><span class="sxs-lookup"><span data-stu-id="9d4f1-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="9d4f1-109">Adicionar a sua solução de tooyour de informações de registo de aplicações (avançado)</span><span class="sxs-lookup"><span data-stu-id="9d4f1-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="9d4f1-110">Aceda demasiado[Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="9d4f1-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="9d4f1-111">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="9d4f1-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="9d4f1-112">Certifique-se a opção de Olá para a configuração orientado está desmarcada</span><span class="sxs-lookup"><span data-stu-id="9d4f1-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="9d4f1-113">Clique em `Add Platform`, em seguida, selecione `Native Application` e clique em`Save`</span><span class="sxs-lookup"><span data-stu-id="9d4f1-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="9d4f1-114">Volte tooXcode.</span><span class="sxs-lookup"><span data-stu-id="9d4f1-114">Go back tooXcode.</span></span> <span data-ttu-id="9d4f1-115">No `ViewController.swift`, substitua a linha de Olá que começa por '`let kClientID`' com o ID da aplicação Olá apenas registado:</span><span class="sxs-lookup"><span data-stu-id="9d4f1-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="9d4f1-116">Controlar + clique <code>Info.plist</code> toobring configurar menu contextuais Olá e, em seguida, clique em: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="9d4f1-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="9d4f1-117">Em Olá <code>dict</code> nó raiz, adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9d4f1-117">Under hello <code>dict</code> root node, add hello following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
<span data-ttu-id="9d4f1-118">Substitua <i> <code>[Your_Application_Id_Here]</code> </i> com Olá Id da aplicação que acabou de ser registado</span><span class="sxs-lookup"><span data-stu-id="9d4f1-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
