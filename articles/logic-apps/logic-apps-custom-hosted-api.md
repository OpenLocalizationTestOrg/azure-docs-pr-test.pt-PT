---
title: aaaDeploy, chamar e autenticar as APIs web e REST APIs de Azure Logic Apps | Microsoft Docs
description: "Implementar, autenticar e chamar web APIs e REST APIs em fluxos de trabalho para integrações de sistema com Azure Logic Apps"
keywords: "Web APIs, REST APIs, conectores, fluxos de trabalho, integrações de sistema, autenticar"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="68f93-104">Implementar, chamar e autenticar APIs personalizadas que os conectores para aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="68f93-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="68f93-105">Depois de [criar APIs personalizadas](./logic-apps-create-api-app.md) que fornecer ações ou acionadores toouse na lógica de fluxos de trabalho de aplicações, tem de implementar as suas APIs antes de poder chamá-los.</span><span class="sxs-lookup"><span data-stu-id="68f93-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="68f93-106">E embora pode chamar qualquer API a partir de uma aplicação lógica, para melhor experiência de Olá, adicione [metadados do Swagger](http://swagger.io/specification/) que descreve a API operações e parâmetros.</span><span class="sxs-lookup"><span data-stu-id="68f93-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="68f93-107">Este ficheiro Swagger ajuda a sua API funcionar melhor e mais facilmente integrar com logic apps.</span><span class="sxs-lookup"><span data-stu-id="68f93-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="68f93-108">Pode implementar as suas APIs como [aplicações web](../app-service-web/app-service-web-overview.md), mas a considerar implementar as suas APIs como [das API apps](../app-service-api/app-service-api-apps-why-best-platform.md), que pode fazer com que a tarefa mais fácil quando criar, alojar e consumir APIs na nuvem de Olá e no local.</span><span class="sxs-lookup"><span data-stu-id="68f93-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="68f93-109">Toochange não tem qualquer código na sua APIs – basta implementar a aplicação de API de tooan de código.</span><span class="sxs-lookup"><span data-stu-id="68f93-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="68f93-110">Pode alojar as suas APIs em [App Service do Azure](../app-service/app-service-value-prop-what-is.md), um plataforma-como-um-serviço (PaaS) que fornece uma das formas mais dimensionáveis, mais fácil e prática de Olá para alojar a API da oferta.</span><span class="sxs-lookup"><span data-stu-id="68f93-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="68f93-111">tooauthenticate chamadas de logic apps tooyour APIs, pode definir cópias de segurança do Azure Active Directory no Olá portal do Azure, para que não tenha tooupdate seu código.</span><span class="sxs-lookup"><span data-stu-id="68f93-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="68f93-112">Em alternativa, pode exigir e impor a autenticação através de código da API.</span><span class="sxs-lookup"><span data-stu-id="68f93-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="68f93-113">Implementar a sua API como uma aplicação web ou aplicação API</span><span class="sxs-lookup"><span data-stu-id="68f93-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="68f93-114">Antes de poder chamar a API personalizada a partir de uma aplicação lógica, implemente a sua API como uma aplicação web ou tooAzure de aplicação de API do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="68f93-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="68f93-115">Além disso, toomake o documento Swagger ser lido pelo Olá Designer de aplicação lógica, definir as propriedades da definição Olá API e ative [recursos de várias origens (CORS) de partilha](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) para a sua aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="68f93-116">No portal do Azure Olá, selecione a aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="68f93-117">No painel de Olá que abre-se, em **API**, escolha **definição da API**.</span><span class="sxs-lookup"><span data-stu-id="68f93-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="68f93-118">Conjunto Olá **localização de definição de API** toohello URL para o ficheiro swagger.json.</span><span class="sxs-lookup"><span data-stu-id="68f93-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="68f93-119">Normalmente, o URL de Olá aparece neste formato:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="68f93-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Ficheiro de tooSwagger de ligação para a API personalizada](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="68f93-121">Em **API**, escolha **CORS**.</span><span class="sxs-lookup"><span data-stu-id="68f93-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="68f93-122">Definir políticas CORS Olá para **permitido origens** demasiado**'*'** (permitir todos os).</span><span class="sxs-lookup"><span data-stu-id="68f93-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="68f93-123">Esta definição permite pedidos a partir do Designer de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="68f93-123">This setting permits requests from Logic App Designer.</span></span>

   ![Permitir pedidos de API do Designer de aplicação lógica tooyour personalizada](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="68f93-125">Para obter mais informações, consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="68f93-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="68f93-126">Adicionar metadados do Swagger para as APIs de web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="68f93-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="68f93-127">Implementar o ASP.NET web APIs tooAzure do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="68f93-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="68f93-128">Chamar a API personalizada da lógica de fluxos de trabalho da aplicação</span><span class="sxs-lookup"><span data-stu-id="68f93-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="68f93-129">Depois de configurar as propriedades da definição Olá API e CORS, acionadores e ações a API personalizada devem ficar disponíveis para tooinclude no seu fluxo de trabalho de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="68f93-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="68f93-130">tooview Olá Web sites que tenham Swagger URLs, pode procurar os Web sites subscrição Olá Designer de aplicações lógicas.</span><span class="sxs-lookup"><span data-stu-id="68f93-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="68f93-131">ações disponíveis tooview e entradas por apontar um documento Swagger, utilize Olá [HTTP + Swagger ação](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="68f93-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="68f93-132">toocall qualquer API, incluindo as APIs que não têm ou expor um documento Swagger, pode criar um pedido sempre com Olá [ação HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="68f93-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="68f93-133">Autenticar chamadas tooyour personalizado API</span><span class="sxs-lookup"><span data-stu-id="68f93-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="68f93-134">Pode proteger chamadas tooyour API personalizada nas seguintes formas:</span><span class="sxs-lookup"><span data-stu-id="68f93-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="68f93-135">[Sem alterações de código](#no-code): proteger a sua API com [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) através do portal do Azure Olá, por isso, não tem tooupdate código ou Reimplementar a sua API.</span><span class="sxs-lookup"><span data-stu-id="68f93-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="68f93-136">Por predefinição, a autenticação do Azure AD Olá ativassem no portal do Azure de Olá não fornece autorização detalhada.</span><span class="sxs-lookup"><span data-stu-id="68f93-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="68f93-137">Por exemplo, esta autenticação bloqueia toojust sua API, um inquilino específico, não tooa utilizador específico ou aplicação.</span><span class="sxs-lookup"><span data-stu-id="68f93-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="68f93-138">[Atualizar o código da API](#update-code): proteger a sua API através da imposição [autenticação de certificado](#certificate), [autenticação básica](#basic), ou [autenticação do Azure AD](#azure-ad-code) através de código.</span><span class="sxs-lookup"><span data-stu-id="68f93-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="68f93-139">Autenticar chamadas tooyour API sem alterar o código</span><span class="sxs-lookup"><span data-stu-id="68f93-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="68f93-140">Eis os passos gerais de Olá para que este método:</span><span class="sxs-lookup"><span data-stu-id="68f93-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="68f93-141">Criar dois [identidades de aplicação do Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): um para a sua aplicação lógica e um para a sua aplicação web (ou a aplicação API).</span><span class="sxs-lookup"><span data-stu-id="68f93-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="68f93-142">tooauthenticate chamadas tooyour API, utilizar credenciais de Olá (ID de cliente e segredo) para Olá [principal de serviço](../app-service-api/app-service-api-dotnet-service-principal-auth.md) que está associada a Olá identidade da aplicação do Azure AD para a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="68f93-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="68f93-143">Inclua aplicação Olá IDs na sua definição de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="68f93-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="68f93-144">Parte 1: Criar uma identidade de aplicação do Azure AD para a sua aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="68f93-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="68f93-145">A aplicação lógica utiliza este tooauthenticate de identidade de aplicação do Azure AD no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68f93-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="68f93-146">Só tem tooset se esta identidade de uma vez para o seu diretório.</span><span class="sxs-lookup"><span data-stu-id="68f93-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="68f93-147">Por exemplo, pode escolher toouse Olá a mesma identidade para todas as suas logic apps, mesmo que pode criar identidades únicas de cada aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="68f93-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="68f93-148">Pode configurar estas identidades no portal do Azure, de Olá [portal clássico do Azure](#app-identity-logic-classic), ou utilize [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="68f93-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="68f93-149">**Criar a identidade da aplicação Olá para a sua aplicação lógica no Olá portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="68f93-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="68f93-150">No Olá [portal do Azure](https://portal.azure.com "https://portal.azure.com"), escolha **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68f93-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="68f93-151">Confirme que é no Olá mesmo diretório que a sua aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="68f93-152">tooswitch diretórios, clique em seu perfil e selecione outro diretório.</span><span class="sxs-lookup"><span data-stu-id="68f93-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="68f93-153">Em alternativa, escolha **descrição geral** > **diretório comutador**.</span><span class="sxs-lookup"><span data-stu-id="68f93-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="68f93-154">No menu de diretório Olá, sob **gerir**, escolha **registos de aplicação** > **novo registo de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="68f93-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="68f93-155">Por predefinição, a lista de registos de aplicações de Olá mostra todos os registos de aplicação no seu diretório.</span><span class="sxs-lookup"><span data-stu-id="68f93-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="68f93-156">tooview apenas seja os registos de aplicações, caixa de pesquisa de toohello seguinte, selecione **as minhas aplicações**.</span><span class="sxs-lookup"><span data-stu-id="68f93-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Criar novo registo de aplicação](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="68f93-158">Dê um nome a sua identidade de aplicação, deixe **tipo de aplicação** definido demasiado**aplicação Web / API**, forneça um exclusivo cadeia formatada como um domínio para **URL de início de sessão**e escolha  **Criar**.</span><span class="sxs-lookup"><span data-stu-id="68f93-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Forneça um nome e início de sessão no URL para a identidade da aplicação](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="68f93-160">a identidade da aplicação Olá que criou para a sua aplicação lógica agora é apresentado na lista de registos de aplicações de Olá.</span><span class="sxs-lookup"><span data-stu-id="68f93-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Identidade da aplicação para a sua aplicação lógica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="68f93-162">Na lista de registos de aplicação Olá, selecione a sua identidade de aplicação nova.</span><span class="sxs-lookup"><span data-stu-id="68f93-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="68f93-163">Copie e guarde Olá **ID da aplicação** toouse como Olá "ID de cliente" para a sua aplicação lógica na parte 3.</span><span class="sxs-lookup"><span data-stu-id="68f93-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Copie e guarde o ID da aplicação para a aplicação lógica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="68f93-165">Se as definições de identidade da aplicação não estão visíveis, escolha **definições** ou **todas as definições**.</span><span class="sxs-lookup"><span data-stu-id="68f93-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="68f93-166">Em **acesso à API**, escolha **chaves**.</span><span class="sxs-lookup"><span data-stu-id="68f93-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="68f93-167">Em **Descrição**, forneça um nome para a sua chave.</span><span class="sxs-lookup"><span data-stu-id="68f93-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="68f93-168">Em **expira**, selecione uma duração para a sua chave.</span><span class="sxs-lookup"><span data-stu-id="68f93-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="68f93-169">chave de Olá que estiver a criar atua como da identidade da aplicação Olá "secreta" ou palavra-passe para a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="68f93-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Crie uma chave para a identidade de aplicação lógica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="68f93-171">Na barra de ferramentas Olá, escolha **guardar**.</span><span class="sxs-lookup"><span data-stu-id="68f93-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="68f93-172">Em **valor**, agora é apresentada a sua chave.</span><span class="sxs-lookup"><span data-stu-id="68f93-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="68f93-173">**Certifique-se de que toocopy e guardar a chave de** para utilização posterior porque a chave de Olá está oculto quando deixar painel chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="68f93-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="68f93-174">Quando configura a sua aplicação lógica em parte 3, especifique esta chave como Olá "secreta" ou a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="68f93-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Copie e guarde a chave para utilizar mais tarde](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="68f93-176">**Criar a identidade da aplicação Olá para a sua aplicação lógica no Olá portal clássico do Azure**</span><span class="sxs-lookup"><span data-stu-id="68f93-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="68f93-177">No portal clássico do Azure de Olá, escolha [ **do Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="68f93-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="68f93-178">Selecione Olá mesmo diretório que utiliza para a sua aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="68f93-179">No Olá **aplicações** separador, escolha **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="68f93-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="68f93-180">Dê um nome a sua identidade da aplicação e escolha **seguinte** (seta para a direita).</span><span class="sxs-lookup"><span data-stu-id="68f93-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="68f93-181">Em **as propriedades da aplicação**, forneça um exclusivo cadeia formatada como um domínio para **URL de início de sessão** e **URI de ID de aplicação**e escolha **concluída** (marca de verificação).</span><span class="sxs-lookup"><span data-stu-id="68f93-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="68f93-182">No Olá **configurar** separador, copie e guarde Olá **ID de cliente** para sua toouse de aplicação lógica na parte 3.</span><span class="sxs-lookup"><span data-stu-id="68f93-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="68f93-183">Em **chaves**, abra Olá **selecione duração** lista.</span><span class="sxs-lookup"><span data-stu-id="68f93-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="68f93-184">Selecione uma duração para a sua chave.</span><span class="sxs-lookup"><span data-stu-id="68f93-184">Select a duration for your key.</span></span>

   <span data-ttu-id="68f93-185">chave de Olá que estiver a criar atua como da identidade da aplicação Olá "secreta" ou palavra-passe para a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="68f93-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="68f93-186">Em Olá parte inferior da página Olá, escolha **guardar**.</span><span class="sxs-lookup"><span data-stu-id="68f93-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="68f93-187">Poderá ter toowait alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="68f93-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="68f93-188">Em **chaves**, certifique-se de que toocopy e guardar a chave de Olá que aparece.</span><span class="sxs-lookup"><span data-stu-id="68f93-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="68f93-189">Quando configura a sua aplicação lógica em parte 3, especifique esta chave como Olá "secreta" ou a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="68f93-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="68f93-190">Para obter mais informações, saiba como demasiado [configurar o início de sessão de Azure Active Directory de toouse de aplicação do serviço de aplicações](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="68f93-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="68f93-191">**Criar a identidade da aplicação Olá para a sua aplicação lógica no PowerShell**</span><span class="sxs-lookup"><span data-stu-id="68f93-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="68f93-192">Pode efetuar esta tarefa através do Azure Resource Manager com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68f93-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="68f93-193">No PowerShell, execute estes comandos:</span><span class="sxs-lookup"><span data-stu-id="68f93-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="68f93-194">Certifique-se de que toocopy Olá **ID do inquilino** Olá GUID para o seu inquilino do Azure AD, **ID da aplicação**e Olá palavra-passe que utilizou.</span><span class="sxs-lookup"><span data-stu-id="68f93-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="68f93-195">Para obter mais informações, saiba como demasiado [criar um principal de serviço com o PowerShell tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="68f93-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="68f93-196">Parte 2: Criar uma identidade de aplicação do Azure AD para a sua aplicação web ou aplicação API</span><span class="sxs-lookup"><span data-stu-id="68f93-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="68f93-197">Se já estiver implementada a sua aplicação web ou aplicação API, pode ativar a autenticação e criar a identidade da aplicação Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="68f93-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="68f93-198">Caso contrário, pode [ativar a autenticação quando implementar com um modelo Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="68f93-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="68f93-199">**Criar a identidade da aplicação Olá e ativar a autenticação no Olá portal do Azure para as aplicações implementadas**</span><span class="sxs-lookup"><span data-stu-id="68f93-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="68f93-200">No Olá [portal do Azure](https://portal.azure.com "https://portal.azure.com"), localize e selecione a sua aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="68f93-201">Em **definições**, escolha **autenticação/autorização**.</span><span class="sxs-lookup"><span data-stu-id="68f93-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="68f93-202">Em **autenticação do serviço de aplicações**, ativar a autenticação **no**.</span><span class="sxs-lookup"><span data-stu-id="68f93-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="68f93-203">Em **fornecedores de autenticação**, escolha **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68f93-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Ativar a autenticação](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="68f93-205">Agora crie uma identidade de aplicação para a sua aplicação web ou aplicação API, conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="68f93-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="68f93-206">No Olá **definições do Azure Active Directory** painel, defina **modo de gestão** demasiado**Express**.</span><span class="sxs-lookup"><span data-stu-id="68f93-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="68f93-207">Escolha **criar nova aplicação AD**.</span><span class="sxs-lookup"><span data-stu-id="68f93-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="68f93-208">Dê um nome a sua identidade da aplicação e escolha **OK**.</span><span class="sxs-lookup"><span data-stu-id="68f93-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Criar a identidade da aplicação para a sua aplicação web ou aplicação API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="68f93-210">No Olá **autenticação / painel autorização**, escolha **guardar**.</span><span class="sxs-lookup"><span data-stu-id="68f93-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="68f93-211">Agora tem de localizar o ID de cliente Olá e ID de inquilino para a identidade da aplicação Olá associado à sua aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="68f93-212">Utilize estes IDs de parte 3.</span><span class="sxs-lookup"><span data-stu-id="68f93-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="68f93-213">Para continuar com estes passos para Olá portal do Azure ou [portal clássico do Azure](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="68f93-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="68f93-214">**Encontrar o ID de cliente da identidade da aplicação e ID de inquilino para a sua aplicação web ou aplicação API no Olá portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="68f93-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="68f93-215">Em **fornecedores de autenticação**, escolha **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68f93-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Escolha "Do Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="68f93-217">No Olá **definições do Azure Active Directory** painel, defina **modo de gestão** demasiado**avançadas**.</span><span class="sxs-lookup"><span data-stu-id="68f93-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="68f93-218">Olá cópia **ID de cliente**e guarde este GUID para utilização na parte 3.</span><span class="sxs-lookup"><span data-stu-id="68f93-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="68f93-219">Se **ID de cliente** e **Url do emissor** não aparecer, tente atualizar Olá portal do Azure e repita o passo 1.</span><span class="sxs-lookup"><span data-stu-id="68f93-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="68f93-220">Em **Url do emissor**, copie e guarde hello apenas o GUID para parte 3.</span><span class="sxs-lookup"><span data-stu-id="68f93-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="68f93-221">Também pode utilizar este GUID na sua aplicação web ou modelo de implementação da aplicação API, se necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="68f93-222">Este GUID é o GUID do seu inquilino específico ("ID do inquilino") e deve aparecer neste URL:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="68f93-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="68f93-223">Sem guardar as alterações, feche Olá **definições do Azure Active Directory** painel.</span><span class="sxs-lookup"><span data-stu-id="68f93-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="68f93-224">**Encontrar o ID de cliente da identidade da aplicação e ID de inquilino para a sua aplicação web ou aplicação API no Olá portal clássico do Azure**</span><span class="sxs-lookup"><span data-stu-id="68f93-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="68f93-225">No portal clássico do Azure de Olá, escolha [ **do Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="68f93-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="68f93-226">Selecione o diretório de Olá que utiliza para a sua aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="68f93-227">No Olá **pesquisa** caixa, localize e selecione a identidade da aplicação Olá para a sua aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="68f93-228">No Olá **configurar** separador, Olá cópia **ID de cliente**e guarde este GUID para utilização na parte 3.</span><span class="sxs-lookup"><span data-stu-id="68f93-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="68f93-229">Depois de obter o ID de cliente Olá, na parte inferior de Olá de Olá **configurar** separador, escolha **ver pontos finais**.</span><span class="sxs-lookup"><span data-stu-id="68f93-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="68f93-230">Copie o URL de Olá para **documento de metadados de Federação**e procure toothat URL.</span><span class="sxs-lookup"><span data-stu-id="68f93-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="68f93-231">No documento de metadados de Olá que se abre, determinar a raiz de Olá **EntityDescriptor ID** elemento, que tem um **entityID** atributo neste formulário:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="68f93-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="68f93-232">Olá GUID neste atributo é o GUID do seu inquilino específico (ID de inquilino).</span><span class="sxs-lookup"><span data-stu-id="68f93-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="68f93-233">Copie o ID do inquilino Olá e guarde este ID para utilização na parte 3 e também toouse na sua aplicação web ou modelo de implementação da aplicação API, se necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="68f93-234">Para obter mais informações, consulte estes tópicos:</span><span class="sxs-lookup"><span data-stu-id="68f93-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="68f93-235">Autenticação de utilizador para API apps no App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="68f93-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="68f93-236">Autenticação e autorização no serviço de aplicações do Azure</span><span class="sxs-lookup"><span data-stu-id="68f93-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="68f93-237">**Ativar a autenticação quando implementar com um modelo Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="68f93-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="68f93-238">Tem ainda de criar uma identidade de aplicação do Azure AD para a sua aplicação web ou aplicação API que difere da identidade de aplicação Olá para a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="68f93-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="68f93-239">passos seguintes toocreate Olá a identidade da aplicação, siga Olá anterior na parte 2 de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="68f93-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="68f93-240">Também pode seguir passos Olá parte 1, mas certifique-se de que toouse a aplicação web ou da aplicação API real `https://{URL}` para **URL de início de sessão** e **URI de ID de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="68f93-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="68f93-241">A partir destes passos, tem toosave ambos os cliente Olá ID e o ID de inquilino para utilizar no modelo de implementação da aplicação e também para parte 3.</span><span class="sxs-lookup"><span data-stu-id="68f93-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="68f93-242">Quando cria a identidade da aplicação Olá do Azure AD para a sua aplicação web ou aplicação API, tem de utilizar Olá portal do Azure ou portal clássico do Azure, em vez do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68f93-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="68f93-243">Olá PowerShell commandlet não configurar permissões de Olá necessário toosign utilizadores para um Web site.</span><span class="sxs-lookup"><span data-stu-id="68f93-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="68f93-244">Depois de obter o ID de cliente de Olá e ID do inquilino, inclua estes IDs como um subresource da sua aplicação web ou aplicação API no seu modelo de implementação:</span><span class="sxs-lookup"><span data-stu-id="68f93-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="68f93-245">tooautomatically implementar uma aplicação web em branco e uma aplicação lógica, juntamente com a autenticação do Azure Active Directory, [vista Olá modelo completo aqui](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), ou clique em **implementar tooAzure** aqui:</span><span class="sxs-lookup"><span data-stu-id="68f93-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="68f93-246">[![Implementar tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="68f93-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="68f93-247">Parte 3: Preencher a secção de autorização de Olá na sua aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="68f93-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="68f93-248">modelo anterior Olá já tem esta secção de autorização, configurar, mas se estiver a criar diretamente aplicação de lógica de Olá, tem de incluir secção de autorização completa Olá.</span><span class="sxs-lookup"><span data-stu-id="68f93-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="68f93-249">Abra a definição da aplicação lógica na vista de código, aceda toohello **HTTP** secção de ação, localizar Olá **autorização** secção e incluir esta linha:</span><span class="sxs-lookup"><span data-stu-id="68f93-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="68f93-250">Elemento</span><span class="sxs-lookup"><span data-stu-id="68f93-250">Element</span></span> | <span data-ttu-id="68f93-251">Descrição</span><span class="sxs-lookup"><span data-stu-id="68f93-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="68f93-252">Inquilino</span><span class="sxs-lookup"><span data-stu-id="68f93-252">tenant</span></span> |<span data-ttu-id="68f93-253">Olá GUID para o inquilino Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="68f93-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="68f93-254">público-alvo</span><span class="sxs-lookup"><span data-stu-id="68f93-254">audience</span></span> |<span data-ttu-id="68f93-255">Necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-255">Required.</span></span> <span data-ttu-id="68f93-256">Olá GUID para o recurso de destino Olá que pretende que o tooaccess - Olá ID de cliente de identidade da aplicação Olá para a sua aplicação web ou aplicação API</span><span class="sxs-lookup"><span data-stu-id="68f93-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="68f93-257">ID de cliente</span><span class="sxs-lookup"><span data-stu-id="68f93-257">clientId</span></span> |<span data-ttu-id="68f93-258">Olá GUID para o cliente de Olá que pedem acesso - Olá ID de cliente de identidade da aplicação Olá para a sua aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="68f93-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="68f93-259">segredo</span><span class="sxs-lookup"><span data-stu-id="68f93-259">secret</span></span> |<span data-ttu-id="68f93-260">Necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-260">Required.</span></span> <span data-ttu-id="68f93-261">chave de Olá ou palavra-passe de identidade da aplicação Olá para cliente Olá que está a solicitar o token de acesso de Olá</span><span class="sxs-lookup"><span data-stu-id="68f93-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="68f93-262">tipo</span><span class="sxs-lookup"><span data-stu-id="68f93-262">type</span></span> |<span data-ttu-id="68f93-263">tipo de autenticação de Olá.</span><span class="sxs-lookup"><span data-stu-id="68f93-263">hello authentication type.</span></span> <span data-ttu-id="68f93-264">Para a autenticação de ActiveDirectoryOAuth, o valor de Olá é `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="68f93-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="68f93-265">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="68f93-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="68f93-266">Chamadas de API seguras através de código</span><span class="sxs-lookup"><span data-stu-id="68f93-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="68f93-267">Autenticação de certificados</span><span class="sxs-lookup"><span data-stu-id="68f93-267">Certificate authentication</span></span>

<span data-ttu-id="68f93-268">toovalidate Olá os pedidos recebidos da sua aplicação de lógica tooyour aplicação de web ou aplicação API, pode utilizar certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="68f93-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="68f93-269">Saiba tooset se o seu código [como autenticação mútua do TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="68f93-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="68f93-270">No Olá **autorização** secção, incluir esta linha:</span><span class="sxs-lookup"><span data-stu-id="68f93-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="68f93-271">Elemento</span><span class="sxs-lookup"><span data-stu-id="68f93-271">Element</span></span> | <span data-ttu-id="68f93-272">Descrição</span><span class="sxs-lookup"><span data-stu-id="68f93-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="68f93-273">tipo</span><span class="sxs-lookup"><span data-stu-id="68f93-273">type</span></span> |<span data-ttu-id="68f93-274">Necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-274">Required.</span></span> <span data-ttu-id="68f93-275">tipo de autenticação de Olá.</span><span class="sxs-lookup"><span data-stu-id="68f93-275">hello authentication type.</span></span> <span data-ttu-id="68f93-276">Para certificados de cliente SSL, Olá valor tem de ser `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="68f93-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="68f93-277">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="68f93-277">password</span></span> |<span data-ttu-id="68f93-278">Necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-278">Required.</span></span> <span data-ttu-id="68f93-279">Olá palavra-passe para aceder ao certificado de cliente Olá (ficheiro PFX)</span><span class="sxs-lookup"><span data-stu-id="68f93-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="68f93-280">PFX</span><span class="sxs-lookup"><span data-stu-id="68f93-280">pfx</span></span> |<span data-ttu-id="68f93-281">Necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-281">Required.</span></span> <span data-ttu-id="68f93-282">Com codificação Base64 conteúdo de certificado de cliente Olá (ficheiro PFX)</span><span class="sxs-lookup"><span data-stu-id="68f93-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="68f93-283">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="68f93-283">Basic authentication</span></span>

<span data-ttu-id="68f93-284">toovalidate pedidos recebidos da sua aplicação de lógica tooyour aplicação de web ou aplicação API, pode utilizar a autenticação básica, tais como um nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="68f93-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="68f93-285">Autenticação básica é um padrão comum e pode utilizar esta autenticação em qualquer toobuild idioma utilizado a aplicação web ou aplicação API.</span><span class="sxs-lookup"><span data-stu-id="68f93-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="68f93-286">No Olá **autorização** secção, incluir esta linha:</span><span class="sxs-lookup"><span data-stu-id="68f93-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="68f93-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="68f93-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="68f93-288">Elemento</span><span class="sxs-lookup"><span data-stu-id="68f93-288">Element</span></span> | <span data-ttu-id="68f93-289">Descrição</span><span class="sxs-lookup"><span data-stu-id="68f93-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="68f93-290">tipo</span><span class="sxs-lookup"><span data-stu-id="68f93-290">type</span></span> |<span data-ttu-id="68f93-291">Necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-291">Required.</span></span> <span data-ttu-id="68f93-292">tipo de autenticação de Olá.</span><span class="sxs-lookup"><span data-stu-id="68f93-292">hello authentication type.</span></span> <span data-ttu-id="68f93-293">Para a autenticação básica, Olá valor tem de ser `Basic`.</span><span class="sxs-lookup"><span data-stu-id="68f93-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="68f93-294">o nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="68f93-294">username</span></span> |<span data-ttu-id="68f93-295">Necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-295">Required.</span></span> <span data-ttu-id="68f93-296">Olá nome de utilizador para autenticação</span><span class="sxs-lookup"><span data-stu-id="68f93-296">hello username for authentication</span></span> |
| <span data-ttu-id="68f93-297">palavra-passe</span><span class="sxs-lookup"><span data-stu-id="68f93-297">password</span></span> |<span data-ttu-id="68f93-298">Necessário.</span><span class="sxs-lookup"><span data-stu-id="68f93-298">Required.</span></span> <span data-ttu-id="68f93-299">Olá palavra-passe para autenticação</span><span class="sxs-lookup"><span data-stu-id="68f93-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="68f93-300">Autenticação do Active Directory do Azure através de código</span><span class="sxs-lookup"><span data-stu-id="68f93-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="68f93-301">Por predefinição, a autenticação do Azure AD Olá ativassem no portal do Azure de Olá não fornece autorização detalhada.</span><span class="sxs-lookup"><span data-stu-id="68f93-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="68f93-302">Por exemplo, esta autenticação bloqueia toojust sua API, um inquilino específico, não tooa utilizador específico ou aplicação.</span><span class="sxs-lookup"><span data-stu-id="68f93-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="68f93-303">aplicação de lógica toorestrict API acesso tooyour através de código, extraia o cabeçalho de Olá que tem Olá um token web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="68f93-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="68f93-304">Verificar a identidade do emissor Olá e rejeitar pedidos que não correspondem.</span><span class="sxs-lookup"><span data-stu-id="68f93-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="68f93-305">Além disso, vai tooimplement esta autenticação inteiramente no seu próprio código e não utilize Olá portal do Azure, saiba como demasiado [autenticar com o Active Directory no local na sua aplicação do Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="68f93-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="68f93-306">toocreate uma identidade de aplicação para a sua aplicação lógica e utilizar essa identidade toocall sua API, tem de seguir passos anteriores Olá.</span><span class="sxs-lookup"><span data-stu-id="68f93-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68f93-307">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="68f93-307">Next steps</span></span>

* [<span data-ttu-id="68f93-308">Verificar o desempenho da aplicação lógica com alertas e registos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="68f93-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)