---
title: aaaGet iniciado com o Azure Active Directory Identity Protection e o Microsoft Graph | Microsoft Docs
description: "Fornece uma introdução tooquery Microsoft Graph para obter uma lista de eventos de risco e informações associadas do Azure Active Directory."
services: active-directory
keywords: "eventos de risco, proteção de identidade do Azure Active Directory, a política de segurança, o Microsoft Graph e vulnerabilidade"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="53e76-104">Introdução ao Azure Active Directory Identity Protection e o Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="53e76-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="53e76-105">Microsoft Graph é Olá Microsoft unified ponto final de API e Olá inicial de [do Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span><span class="sxs-lookup"><span data-stu-id="53e76-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="53e76-106">Olá primeira API, **identityRiskEvents**, permite-lhe tooquery Microsoft Graph para obter uma lista de [eventos de risco](active-directory-identityprotection-risk-events-types.md) e informações de associados.</span><span class="sxs-lookup"><span data-stu-id="53e76-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="53e76-107">Este artigo obtém a começar a consultar esta API.</span><span class="sxs-lookup"><span data-stu-id="53e76-107">This article gets you started querying this API.</span></span> <span data-ttu-id="53e76-108">Para uma introdução aprofundada, documentação completa e acesso toohello gráfico Explorer, consulte Olá [site Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="53e76-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53e76-109">A Microsoft recomenda que gere o Azure AD através de Olá [Centro de administração do Azure AD](https://aad.portal.azure.com) no Olá portal do Azure em vez de utilizar Olá portal clássico do Azure referenciado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="53e76-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="53e76-110">Existem três passos tooaccessing identidade dados da proteção através do Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="53e76-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="53e76-111">Adicione uma aplicação com um segredo do cliente.</span><span class="sxs-lookup"><span data-stu-id="53e76-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="53e76-112">Utilize este segredo e alguns outros tipos de informações tooauthenticate tooMicrosoft gráfico, onde recebe um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="53e76-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="53e76-113">Utilizar este ponto final do token toomake pedidos toohello API e voltar a dados da proteção de identidade.</span><span class="sxs-lookup"><span data-stu-id="53e76-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="53e76-114">Antes de começar, terá de:</span><span class="sxs-lookup"><span data-stu-id="53e76-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="53e76-115">Aplicação da Olá de toocreate de privilégios de administrador no Azure AD</span><span class="sxs-lookup"><span data-stu-id="53e76-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="53e76-116">nome de Olá de domínio do inquilino (por exemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="53e76-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="53e76-117">Adicionar uma aplicação com um segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="53e76-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="53e76-118">[Inicie sessão no](https://manage.windowsazure.com) tooyour portal clássico do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="53e76-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="53e76-119">No painel de navegação esquerdo Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53e76-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="53e76-121">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="53e76-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="53e76-122">No menu de Olá na parte superior do Olá, clique em **aplicações**.</span><span class="sxs-lookup"><span data-stu-id="53e76-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="53e76-124">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="53e76-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="53e76-126">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação que a minha organização está a desenvolver**.</span><span class="sxs-lookup"><span data-stu-id="53e76-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="53e76-128">No Olá **conte-na sua aplicação** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="53e76-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="53e76-130">a.</span><span class="sxs-lookup"><span data-stu-id="53e76-130">a.</span></span> <span data-ttu-id="53e76-131">No Olá **nome** caixa de texto, escreva um nome para a sua aplicação (por ex.: aplicação de API de eventos de risco AADIP).</span><span class="sxs-lookup"><span data-stu-id="53e76-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="53e76-132">b.</span><span class="sxs-lookup"><span data-stu-id="53e76-132">b.</span></span> <span data-ttu-id="53e76-133">Como **tipo**, selecione **aplicação Web e / ou Web API**.</span><span class="sxs-lookup"><span data-stu-id="53e76-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="53e76-134">c.</span><span class="sxs-lookup"><span data-stu-id="53e76-134">c.</span></span> <span data-ttu-id="53e76-135">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="53e76-135">Click **Next**.</span></span>
8. <span data-ttu-id="53e76-136">No Olá **as propriedades da aplicação** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="53e76-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="53e76-138">a.</span><span class="sxs-lookup"><span data-stu-id="53e76-138">a.</span></span> <span data-ttu-id="53e76-139">No Olá **URL de início de sessão** caixa de texto, tipo `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="53e76-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="53e76-140">b.</span><span class="sxs-lookup"><span data-stu-id="53e76-140">b.</span></span> <span data-ttu-id="53e76-141">No Olá **URI de ID de aplicação** caixa de texto, tipo `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="53e76-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="53e76-142">c.</span><span class="sxs-lookup"><span data-stu-id="53e76-142">c.</span></span> <span data-ttu-id="53e76-143">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="53e76-143">Click **Complete**.</span></span>

<span data-ttu-id="53e76-144">Agora pode configurar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="53e76-144">Your can now configure your application.</span></span>

![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="53e76-146">Conceder a Olá de toouse de permissão de aplicação API</span><span class="sxs-lookup"><span data-stu-id="53e76-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="53e76-147">Na página da aplicação, no menu de Olá na parte superior do Olá, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="53e76-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="53e76-149">No Olá **aplicações de tooother permissões** secção, clique em **Adicionar aplicação**.</span><span class="sxs-lookup"><span data-stu-id="53e76-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="53e76-151">No Olá **aplicações de tooother permissões** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="53e76-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="53e76-153">a.</span><span class="sxs-lookup"><span data-stu-id="53e76-153">a.</span></span> <span data-ttu-id="53e76-154">Selecione **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="53e76-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="53e76-155">b.</span><span class="sxs-lookup"><span data-stu-id="53e76-155">b.</span></span> <span data-ttu-id="53e76-156">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="53e76-156">Click **Complete**.</span></span>
4. <span data-ttu-id="53e76-157">Clique em **permissões de aplicação: 0**e, em seguida, selecione **ler todas as informações de eventos de risco de identidade**.</span><span class="sxs-lookup"><span data-stu-id="53e76-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="53e76-159">Clique em **guardar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="53e76-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="53e76-161">Obter uma chave de acesso</span><span class="sxs-lookup"><span data-stu-id="53e76-161">Get an access key</span></span>
1. <span data-ttu-id="53e76-162">Na página da aplicação, na Olá **chaves** secção, selecione de 1 ano como duração.</span><span class="sxs-lookup"><span data-stu-id="53e76-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="53e76-164">Clique em **guardar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="53e76-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="53e76-166">na secção de chaves de Olá, copie o valor de Olá da sua chave recentemente criada e, em seguida, cole-o numa localização segura.</span><span class="sxs-lookup"><span data-stu-id="53e76-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Criar uma aplicação](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="53e76-168">Se perder a esta chave, irá ter tooreturn toothis secção e crie uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="53e76-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="53e76-169">Manter esta chave de segredo: qualquer pessoa que tenha pode aceder aos seus dados.</span><span class="sxs-lookup"><span data-stu-id="53e76-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="53e76-170">No Olá **propriedades** secção, Olá cópia **ID de cliente**e, em seguida, cole-o numa localização segura.</span><span class="sxs-lookup"><span data-stu-id="53e76-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="53e76-171">Autenticar tooMicrosoft gráfico e Olá de consulta API de eventos de risco de identidade</span><span class="sxs-lookup"><span data-stu-id="53e76-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="53e76-172">Neste momento, é necessário:</span><span class="sxs-lookup"><span data-stu-id="53e76-172">At this point, you should have:</span></span>

* <span data-ttu-id="53e76-173">ID de cliente Olá copiou acima</span><span class="sxs-lookup"><span data-stu-id="53e76-173">hello client ID you copied above</span></span>
* <span data-ttu-id="53e76-174">chave de Olá que copiou acima</span><span class="sxs-lookup"><span data-stu-id="53e76-174">hello key you copied above</span></span>
* <span data-ttu-id="53e76-175">nome de Olá do domínio do seu inquilino</span><span class="sxs-lookup"><span data-stu-id="53e76-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="53e76-176">tooauthenticate, envie uma mensagem de pedido demasiado`https://login.microsoft.com` com Olá seguir os parâmetros no corpo de Olá:</span><span class="sxs-lookup"><span data-stu-id="53e76-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="53e76-177">grant_type: "**client_credentials**"</span><span class="sxs-lookup"><span data-stu-id="53e76-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="53e76-178">recurso: "**https://graph.microsoft.com**"</span><span class="sxs-lookup"><span data-stu-id="53e76-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="53e76-179">client_id:<your client ID></span><span class="sxs-lookup"><span data-stu-id="53e76-179">client_id: <your client ID></span></span>
* <span data-ttu-id="53e76-180">client_secret:<your key></span><span class="sxs-lookup"><span data-stu-id="53e76-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="53e76-181">Precisa de valores de tooprovide para Olá **client_id** e Olá **client_secret** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="53e76-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="53e76-182">Se tiver êxito, esta ação devolve um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="53e76-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="53e76-183">Olá toocall API, criar um cabeçalho com Olá seguinte parâmetro:</span><span class="sxs-lookup"><span data-stu-id="53e76-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="53e76-184">Quando a autenticação, pode encontrar o tipo de token de Olá e o token de acesso no Olá devolvida um token.</span><span class="sxs-lookup"><span data-stu-id="53e76-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="53e76-185">Envie este cabeçalho como um toohello pedido seguinte URL de API:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="53e76-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="53e76-186">resposta de Olá, se tiver êxito, é uma coleção de identidade eventos de risco e dados no formato JSON de OData, que pode ser analisado e processado como julgar de Olá associados.</span><span class="sxs-lookup"><span data-stu-id="53e76-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="53e76-187">Eis o código de exemplo para autenticar e chamar a API de Olá através do Powershell.</span><span class="sxs-lookup"><span data-stu-id="53e76-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="53e76-188">Basta adicionar o seu ID de cliente, a chave e domínio de inquilino.</span><span class="sxs-lookup"><span data-stu-id="53e76-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="53e76-189">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="53e76-189">Next steps</span></span>
<span data-ttu-id="53e76-190">Parabéns, efetuadas apenas o primeiro tooMicrosoft de chamada gráfico!</span><span class="sxs-lookup"><span data-stu-id="53e76-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="53e76-191">Agora pode consultar eventos de risco de identidade e utilizar dados Olá, no entanto, julgar.</span><span class="sxs-lookup"><span data-stu-id="53e76-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="53e76-192">toolearn mais informações sobre o Microsoft Graph e como aplicações toobuild utilizando Olá Graph API, consulte Olá [documentação](https://graph.microsoft.io/docs) e muito mais no Olá [site Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="53e76-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="53e76-193">Além disso, certifique-se de que toobookmark Olá [API do Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) página que lista todos os Olá APIs de proteção de identidade disponíveis no gráfico.</span><span class="sxs-lookup"><span data-stu-id="53e76-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="53e76-194">À medida que adiciona novas formas toowork com proteção de identidade através de API, irá vê-los nessa página.</span><span class="sxs-lookup"><span data-stu-id="53e76-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53e76-195">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="53e76-195">Additional resources</span></span>
* [<span data-ttu-id="53e76-196">Proteção de identidade do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53e76-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="53e76-197">Tipos de eventos de risco detetados pelo Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="53e76-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="53e76-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="53e76-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="53e76-199">Descrição geral do Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="53e76-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="53e76-200">Raiz do serviço do Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="53e76-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

