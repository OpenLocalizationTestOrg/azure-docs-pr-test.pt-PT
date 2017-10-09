---
title: "aaaAzure AD v2 ASP.NET Web Server introdução - Config | Microsoft Docs"
description: "Implementar Microsoft início de sessão numa solução ASP.NET com uma aplicação de baseadas no browser web tradicional utilizando o padrão de OpenID Connect"
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="ca0c1-103">Criar uma aplicação (rápida)</span><span class="sxs-lookup"><span data-stu-id="ca0c1-103">Create an application (Express)</span></span>
<span data-ttu-id="ca0c1-104">Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ca0c1-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ca0c1-105">Registar a sua aplicação através de Olá [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="ca0c1-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="ca0c1-106">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="ca0c1-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="ca0c1-107">Certifique-se a opção de Olá para a configuração orientado está marcada</span><span class="sxs-lookup"><span data-stu-id="ca0c1-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="ca0c1-108">Siga as instruções de Olá tooadd uma aplicação de tooyour do URL de redirecionamento</span><span class="sxs-lookup"><span data-stu-id="ca0c1-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="ca0c1-109">Adicionar a sua solução de tooyour de informações de registo de aplicações (avançado)</span><span class="sxs-lookup"><span data-stu-id="ca0c1-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="ca0c1-110">Agora tem tooregister a aplicação no Olá *Portal de registo de aplicações do Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ca0c1-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ca0c1-111">Aceda toohello [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister uma aplicação</span><span class="sxs-lookup"><span data-stu-id="ca0c1-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="ca0c1-112">Introduza um nome para a aplicação e o seu correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="ca0c1-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="ca0c1-113">Certifique-se a opção de Olá para a configuração orientado está desmarcada</span><span class="sxs-lookup"><span data-stu-id="ca0c1-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="ca0c1-114">Clique em `Add Platform`, em seguida, selecione`Web`</span><span class="sxs-lookup"><span data-stu-id="ca0c1-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="ca0c1-115">Voltar atrás tooVisual Studio, no Explorador de soluções, selecione o projeto de Olá e observe a janela de propriedades de Olá (se não for apresentada uma janela de propriedades, prima F4)</span><span class="sxs-lookup"><span data-stu-id="ca0c1-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="ca0c1-116">Alterar demasiado SSL ativado`True`</span><span class="sxs-lookup"><span data-stu-id="ca0c1-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="ca0c1-117">Copie o URL de SSL de Olá e adicionar esta lista de toohello do URL de redirecionamento URLs na lista de Portal de registo a Olá de URLs de redirecionamento:</span><span class="sxs-lookup"><span data-stu-id="ca0c1-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Propriedades do projeto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="ca0c1-119">Adicione o seguinte Olá no `web.config` localizado na pasta raiz de Olá na secção de Olá `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="ca0c1-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="ca0c1-120">Substitua `ClientId` com Olá Id da aplicação que acabou de ser registado</span><span class="sxs-lookup"><span data-stu-id="ca0c1-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="ca0c1-121">Substitua `redirectUri` com Olá SSL URL do seu projeto</span><span class="sxs-lookup"><span data-stu-id="ca0c1-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
