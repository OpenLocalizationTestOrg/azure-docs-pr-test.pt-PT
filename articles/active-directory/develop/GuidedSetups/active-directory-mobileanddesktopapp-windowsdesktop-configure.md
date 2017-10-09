---
title: "aaaAzure AD v2 Windows Desktop introdução - Config | Microsoft Docs"
description: "Como uma aplicação .NET de ambiente de trabalho do Windows (XAML) pode obter um token de acesso e chamar uma API protegida pelo ponto final do Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="4596f-104">Criar uma aplicação (rápida)</span><span class="sxs-lookup"><span data-stu-id="4596f-104">Create an application (Express)</span></span>
<span data-ttu-id="4596f-105">Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="4596f-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="4596f-106">Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="4596f-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="4596f-107">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="4596f-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="4596f-108">Certifique-se a opção de Olá para a configuração orientado está marcada</span><span class="sxs-lookup"><span data-stu-id="4596f-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="4596f-109">Siga o ID da aplicação Olá instruções tooobtain Olá e cole-o para o seu código</span><span class="sxs-lookup"><span data-stu-id="4596f-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="4596f-110">Adicionar a sua solução de tooyour de informações de registo de aplicações (avançado)</span><span class="sxs-lookup"><span data-stu-id="4596f-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="4596f-111">Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="4596f-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="4596f-112">Aceda toohello [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister uma aplicação</span><span class="sxs-lookup"><span data-stu-id="4596f-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="4596f-113">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="4596f-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="4596f-114">Certifique-se a opção de Olá para a configuração orientado está desmarcada</span><span class="sxs-lookup"><span data-stu-id="4596f-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="4596f-115">Clique em `Add Platform`, em seguida, selecione `Native Application` e clique em Guardar</span><span class="sxs-lookup"><span data-stu-id="4596f-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="4596f-116">Copiar Olá GUID no ID da aplicação, volte atrás tooVisual Studio, abra `App.xaml.cs` e substitua `your_client_id_here` com Olá ID da aplicação que acabou de ser registado:</span><span class="sxs-lookup"><span data-stu-id="4596f-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
