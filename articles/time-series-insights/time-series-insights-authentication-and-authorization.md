---
title: "aaaConfigure autenticação e autorização para uma aplicação personalizada que chama Olá Azure tempo série Insights API | Microsoft Docs"
description: "Este tutorial explica como tooconfigure autenticação e autorização para uma aplicação personalizada que chama Olá API de Insights de série de tempo do Azure"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="48bc4-103">Autenticação e autorização para API de Insights de série de tempo do Azure</span><span class="sxs-lookup"><span data-stu-id="48bc4-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="48bc4-104">Este artigo explica como tooconfigure uma aplicação personalizada que chama Olá API de Insights de série de tempo do Azure.</span><span class="sxs-lookup"><span data-stu-id="48bc4-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="48bc4-105">Principal de serviço</span><span class="sxs-lookup"><span data-stu-id="48bc4-105">Service principal</span></span>

<span data-ttu-id="48bc4-106">Esta secção explica como tooconfigure tooaccess uma aplicação Olá tempo série Insights API em nome da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="48bc4-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="48bc4-107">aplicação Olá, em seguida, pode consultar dados ou publicar dados de referência no ambiente de informações de séries de tempo de Olá com credenciais de aplicação e credenciais de utilizador não Olá.</span><span class="sxs-lookup"><span data-stu-id="48bc4-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="48bc4-108">Quando tiver uma aplicação que necessita de tooaccess Insights de séries de tempo, tem de configurar uma aplicação do Azure Active Directory e atribuir políticas de acesso de dados Olá no ambiente do Olá Insights de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="48bc4-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="48bc4-109">Esta abordagem é preferível toorunning Olá aplicação com as suas próprias credenciais porque:</span><span class="sxs-lookup"><span data-stu-id="48bc4-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="48bc4-110">Pode atribuir permissões de identidade de aplicação toohello que são diferentes das suas permissões.</span><span class="sxs-lookup"><span data-stu-id="48bc4-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="48bc4-111">Normalmente, estas permissões são tooexactly restrito tem de aplicação que Olá toodo.</span><span class="sxs-lookup"><span data-stu-id="48bc4-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="48bc4-112">Por exemplo, pode permitir Olá aplicação tooonly ler os dados num ambiente Insights de séries de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="48bc4-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="48bc4-113">Não tem credenciais da aplicação Olá toochange se alterar as suas responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="48bc4-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="48bc4-114">Pode utilizar um certificado ou uma autenticação de chave tooautomate aplicação quando estiver a executar um script automático.</span><span class="sxs-lookup"><span data-stu-id="48bc4-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="48bc4-115">Este artigo mostra como tooperform os passos através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="48bc4-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="48bc4-116">Concentra-se uma aplicação do inquilino único em que a aplicação Olá é toorun pretendido na organização apenas um.</span><span class="sxs-lookup"><span data-stu-id="48bc4-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="48bc4-117">Normalmente utiliza aplicações de inquilino único para aplicações de linha de negócio que são executadas na sua organização.</span><span class="sxs-lookup"><span data-stu-id="48bc4-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="48bc4-118">fluxo de configuração de Olá consiste em três passos de alto nível:</span><span class="sxs-lookup"><span data-stu-id="48bc4-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="48bc4-119">Crie uma aplicação no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="48bc4-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="48bc4-120">Autorize o ambiente do Insights de séries de tempo tooaccess Olá esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="48bc4-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="48bc4-121">Utilizar o ID da aplicação Olá e chave tooacquire um token toohello `"https://api.timeseries.azure.com/"` audiência ou recurso.</span><span class="sxs-lookup"><span data-stu-id="48bc4-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="48bc4-122">token de Olá, em seguida, pode ser utilizados toocall Olá API de informações de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="48bc4-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="48bc4-123">Eis os passos detalhados de hello:</span><span class="sxs-lookup"><span data-stu-id="48bc4-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="48bc4-124">No portal do Azure Olá, selecione **do Azure Active Directory** > **registos de aplicação** > **novo registo de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="48bc4-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Novo registo de aplicação no Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="48bc4-126">Dar um toobe de tipo Olá nome, selecione a aplicação Olá **aplicação Web / API**, selecione qualquer URI válido para **URL de início de sessão**e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="48bc4-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Criar aplicação Olá no Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="48bc4-128">Selecione a aplicação criada recentemente e copie o editor de texto favorito de tooyour de ID de aplicação.</span><span class="sxs-lookup"><span data-stu-id="48bc4-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Copie o ID da aplicação Olá](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="48bc4-130">Selecione **chaves**, introduza o nome da chave Olá, expiração selecione Olá e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="48bc4-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![Selecione as chaves de aplicação](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Introduza o nome da chave Olá e expiração e clique em Guardar](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="48bc4-133">Copie o editor de texto favorito Olá tooyour chave.</span><span class="sxs-lookup"><span data-stu-id="48bc4-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Copie a chave da aplicação Olá](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="48bc4-135">Para o ambiente de informações de séries de tempo de Olá, selecione **políticas de acesso de dados** e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="48bc4-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Adicionar novo dados acesso política toohello Insights de séries de tempo ambiente](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="48bc4-137">No Olá **selecionar utilizador** caixa de diálogo, o nome da aplicação Olá Colar (a partir do passo 2) ou o ID da aplicação (a partir do passo 3).</span><span class="sxs-lookup"><span data-stu-id="48bc4-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Localizar uma aplicação na caixa de diálogo Selecionar utilizador Olá](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="48bc4-139">Função de Olá selecione (**leitor** para consultar os dados, **contribuinte** para consultar os dados e a alteração de dados de referência) e clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="48bc4-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Escolher o leitor ou contribuinte na caixa de diálogo Selecionar função Olá](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="48bc4-141">Guardar política de Olá clicando **Ok**.</span><span class="sxs-lookup"><span data-stu-id="48bc4-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="48bc4-142">Utilize o ID da aplicação Olá (a partir do passo 3) e chave (a partir do passo 5) tooacquire Olá o token de aplicações em nome da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="48bc4-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="48bc4-143">Olá token pode, em seguida, ser transmitido no Olá `Authorization` cabeçalho quando chamadas de aplicação Olá Olá API de informações de séries de tempo.</span><span class="sxs-lookup"><span data-stu-id="48bc4-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="48bc4-144">Se estiver a utilizar c#, pode utilizar Olá token de Olá tooacquire código em nome da aplicação Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="48bc4-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="48bc4-145">Para um exemplo completo, consulte [consultar dados com c#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="48bc4-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="48bc4-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="48bc4-146">Next steps</span></span>

<span data-ttu-id="48bc4-147">Utilizar o ID da aplicação Olá e chave na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="48bc4-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="48bc4-148">Para o código de exemplo que chama a API de informações de séries de tempo de Olá, consulte [consultar dados com c#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="48bc4-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="48bc4-149">Consultar também</span><span class="sxs-lookup"><span data-stu-id="48bc4-149">See also</span></span>

* <span data-ttu-id="48bc4-150">[API de consulta](/rest/api/time-series-insights/time-series-insights-reference-queryapi) para referência da API de consulta completa Olá</span><span class="sxs-lookup"><span data-stu-id="48bc4-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="48bc4-151">Criar um serviço principal no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="48bc4-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
