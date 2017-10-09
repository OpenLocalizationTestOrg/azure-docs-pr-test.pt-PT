---
title: "aaaProblems início de sessão na aplicação de galeria tooa configurada para Federado de sessão único-| Microsoft Docs"
description: "Orientações para erros específicos de Olá quando iniciar sessão uma aplicação que configurou para baseados em SAML federado-início de sessão único com o Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: ba20a4904860cf063967029cad33fb80f16e4956
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooa-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="d21c2-103">Problemas de início de sessão na aplicação de galeria tooa configurada para federado-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d21c2-103">Problems signing in tooa gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="d21c2-104">tootroubleshoot o problema, tem de configuração da aplicação Olá tooverify no Azure AD como seguir:</span><span class="sxs-lookup"><span data-stu-id="d21c2-104">tootroubleshoot your problem, you need tooverify hello application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="d21c2-105">Seguiu todos os passos de configuração de Olá de Olá aplicação de galeria do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d21c2-105">You have followed all hello configuration steps for hello Azure AD gallery application.</span></span>

-   <span data-ttu-id="d21c2-106">corresponder estes valores esperados na aplicação Olá Olá identificador e o URL de resposta configurado no AAD</span><span class="sxs-lookup"><span data-stu-id="d21c2-106">hello Identifier and Reply URL configured in AAD match they expected values in hello application</span></span>

-   <span data-ttu-id="d21c2-107">Atribuiu utilizadores toohello aplicação</span><span class="sxs-lookup"><span data-stu-id="d21c2-107">You have assigned users toohello application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="d21c2-108">Não foi encontrada no diretório de aplicação</span><span class="sxs-lookup"><span data-stu-id="d21c2-108">Application not found in directory</span></span>

<span data-ttu-id="d21c2-109">*AADSTS70001 de erro: A aplicação com o identificador 'https://contoso.com' não foi encontrada no diretório de Olá*.</span><span class="sxs-lookup"><span data-stu-id="d21c2-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in hello directory*.</span></span>

<span data-ttu-id="d21c2-110">**Uma causa possível**</span><span class="sxs-lookup"><span data-stu-id="d21c2-110">**Possible cause**</span></span>

<span data-ttu-id="d21c2-111">atributo de emissor Olá envia de Olá aplicação tooAzure que AD no pedido SAML Olá não corresponde ao valor do identificador de Olá configurado na aplicação Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d21c2-111">hello Issuer attribute sends from hello application tooAzure AD in hello SAML request doesn’t match hello Identifier value configured in hello application Azure AD.</span></span>

<span data-ttu-id="d21c2-112">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="d21c2-112">**Resolution**</span></span>

<span data-ttu-id="d21c2-113">Certifique-se esse atributo de emissor Olá no pedido SAML Olá correspondência Olá valor do identificador configurado no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d21c2-113">Ensure that hello Issuer attribute in hello SAML request it’s matching hello Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="d21c2-114">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-114">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d21c2-115">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-115">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d21c2-116">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="d21c2-116">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d21c2-117">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d21c2-117">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d21c2-118">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="d21c2-118">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d21c2-119">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-119">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d21c2-120">Selecionar aplicação Olá pretende tooconfigure-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d21c2-120">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="d21c2-121">Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-121">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d21c2-122">Aceda demasiado**domínios e URLs** secção.</span><span class="sxs-lookup"><span data-stu-id="d21c2-122">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="d21c2-123">Certifique-se de que o valor na caixa de texto valor Olá para o valor do identificador de Olá apresentado no registo de erros Olá correspondência de identificador de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-123">Verify that hello value in hello Identifier textbox is matching hello value for hello identifier value displayed in hello error.</span></span>

<span data-ttu-id="d21c2-124">Depois de ter atualizado o valor do identificador de Olá no Azure AD e de Olá valor correspondente envia pela aplicação Olá no pedido SAML Olá, deve ser capaz de toosign na aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="d21c2-124">After you have updated hello Identifier value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="hello-reply-address-does-not-match-hello-reply-addresses-configured-for-hello-application"></a><span data-ttu-id="d21c2-125">endereço de resposta de Olá não correspondem aos endereços de resposta de Olá configurados para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-125">hello reply address does not match hello reply addresses configured for hello application.</span></span>

<span data-ttu-id="d21c2-126">*AADSTS50011 de erro: o endereço de resposta de Olá 'https://contoso.com' não correspondem aos endereços de resposta de Olá configurados para a aplicação Olá*</span><span class="sxs-lookup"><span data-stu-id="d21c2-126">*Error AADSTS50011: hello reply address ‘https://contoso.com’ does not match hello reply addresses configured for hello application*</span></span>

<span data-ttu-id="d21c2-127">**Uma causa possível**</span><span class="sxs-lookup"><span data-stu-id="d21c2-127">**Possible cause**</span></span>

<span data-ttu-id="d21c2-128">Olá AssertionConsumerServiceURL valor no pedido SAML Olá não corresponde ao valor de URL de resposta de Olá ou padrão configurado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d21c2-128">hello AssertionConsumerServiceURL value in hello SAML request doesn't match hello Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="d21c2-129">Olá AssertionConsumerServiceURL valor no pedido SAML Olá é URL Olá, consulte o erro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-129">hello AssertionConsumerServiceURL value in hello SAML request is hello URL you see in hello error.</span></span>

<span data-ttu-id="d21c2-130">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="d21c2-130">**Resolution**</span></span>

<span data-ttu-id="d21c2-131">Certifique-se de que o valor AssertionConsumerServiceURL Olá no pedido SAML Olá de correspondente Olá valor do URL de resposta configurado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d21c2-131">Ensure that hello AssertionConsumerServiceURL value in hello SAML request it's matching hello Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="d21c2-132">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-132">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d21c2-133">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-133">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d21c2-134">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="d21c2-134">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d21c2-135">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d21c2-135">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d21c2-136">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="d21c2-136">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d21c2-137">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-137">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d21c2-138">Selecionar aplicação Olá pretende tooconfigure-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d21c2-138">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="d21c2-139">Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-139">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d21c2-140">Aceda demasiado**domínios e URLs** secção.</span><span class="sxs-lookup"><span data-stu-id="d21c2-140">Go too**Domain and URLs** section.</span></span> <span data-ttu-id="d21c2-141">Certifique-se ou Atualize o valor Olá Olá de toomatch AssertionConsumerServiceURL valor no pedido SAML Olá do Olá URL de resposta caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d21c2-141">Verify or update hello value in hello Reply URL textbox toomatch hello AssertionConsumerServiceURL value in hello SAML request.</span></span>  
    * <span data-ttu-id="d21c2-142">Se não vir a caixa de texto de URL de resposta de Olá, selecione Olá **Mostrar avançadas definições de URL** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="d21c2-142">If you don't see hello Reply URL textbox, select hello **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="d21c2-143">Depois de ter atualizado o valor do URL de resposta de Olá no Azure AD e tem de correspondência do valor de Olá envia pela aplicação Olá em Olá pedido SAML, deve ser capaz de toosign na aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="d21c2-143">After you have updated hello Reply URL value in Azure AD and it’s matching hello value sends by hello application in hello SAML request, you should be able toosign in toohello application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="d21c2-144">Não atribuído uma função de utilizador</span><span class="sxs-lookup"><span data-stu-id="d21c2-144">User not assigned a role</span></span>

<span data-ttu-id="d21c2-145">*Erro AADSTS50105: Olá com sessão iniciada utilizador 'brian@contoso.com' não está atribuído a função de tooa para aplicação Olá*.</span><span class="sxs-lookup"><span data-stu-id="d21c2-145">*Error AADSTS50105: hello signed in user 'brian@contoso.com' is not assigned tooa role for hello application*.</span></span>

<span data-ttu-id="d21c2-146">**Uma causa possível**</span><span class="sxs-lookup"><span data-stu-id="d21c2-146">**Possible cause**</span></span>

<span data-ttu-id="d21c2-147">Olá tem não foi concedido ao utilizador acesso toohello aplicação no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d21c2-147">hello user has not been granted access toohello application in Azure AD.</span></span>

<span data-ttu-id="d21c2-148">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="d21c2-148">**Resolution**</span></span>

<span data-ttu-id="d21c2-149">tooassign um ou mais aplicações de tooan utilizadores diretamente, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="d21c2-149">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="d21c2-150">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-150">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="d21c2-151">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-151">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d21c2-152">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="d21c2-152">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d21c2-153">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d21c2-153">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d21c2-154">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="d21c2-154">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d21c2-155">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-155">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d21c2-156">Selecione aplicação Olá pretende tooassign uma lista de Olá de toofrom do utilizador.</span><span class="sxs-lookup"><span data-stu-id="d21c2-156">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="d21c2-157">Quando carrega a aplicação Olá, clique em **utilizadores e grupos** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-157">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d21c2-158">Clique em Olá **adicionar** botão por cima Olá **utilizadores e grupos** Olá de tooopen lista **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="d21c2-158">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="d21c2-159">Clique em Olá **utilizadores e grupos** Seletor de Olá **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="d21c2-159">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="d21c2-160">Tipo de Olá **nome completo** ou **endereço de correio eletrónico** do utilizador Olá estiver interessado em atribuir para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d21c2-160">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="d21c2-161">Coloque o cursor sobre Olá **utilizador** no Olá lista tooreveal um **caixa de verificação**.</span><span class="sxs-lookup"><span data-stu-id="d21c2-161">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="d21c2-162">Clique em tooadd de fotografias ou logótipo do perfil do Olá caixa de verificação seguinte toohello utilizador seu utilizador toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="d21c2-162">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="d21c2-163">**Opcional:** se gostaria demasiado**adicionar mais do que um utilizador**, tipo noutra **nome completo** ou **endereço de correio eletrónico** para Olá **pesquisar por nome ou o endereço de correio eletrónico** caixa de pesquisa e clique em Olá caixa de verificação tooadd toohello este utilizador **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="d21c2-163">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="d21c2-164">Quando tiver terminado de selecionar utilizadores, clique em Olá **selecione** botão tooadd-los toohello lista de utilizadores e grupos toobe atribuído toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="d21c2-164">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="d21c2-165">**Opcional:** clique Olá **selecionar função** Seletor no Olá **adicionar atribuição** painel tooselect uma função tooassign toohello utilizadores que selecionou.</span><span class="sxs-lookup"><span data-stu-id="d21c2-165">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="d21c2-166">Clique em Olá **atribuir** botão tooassign Olá aplicação toohello utilizadores selecionados.</span><span class="sxs-lookup"><span data-stu-id="d21c2-166">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="d21c2-167">Após um curto período de tempo, os utilizadores Olá que selecionou de ser capaz de toolaunch estas aplicações utilizando Olá métodos descritos na secção de descrição de solução Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-167">After a short period of time, hello users you have selected be able toolaunch these applications using hello methods described in hello solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="d21c2-168">Não um pedido de SAML válido</span><span class="sxs-lookup"><span data-stu-id="d21c2-168">Not a valid SAML Request</span></span>

<span data-ttu-id="d21c2-169">*Erro AADSTS75005: Olá do pedido não é uma mensagem de protocolo Saml2 válida.*</span><span class="sxs-lookup"><span data-stu-id="d21c2-169">*Error AADSTS75005: hello request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="d21c2-170">**Uma causa possível**</span><span class="sxs-lookup"><span data-stu-id="d21c2-170">**Possible cause**</span></span>

<span data-ttu-id="d21c2-171">Azure AD não suporta Olá SAML do pedido enviados pela aplicação Olá para o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="d21c2-171">Azure AD doesn’t support hello SAML Request sent by hello application for Single Sign-on.</span></span> <span data-ttu-id="d21c2-172">Alguns problemas comuns são:</span><span class="sxs-lookup"><span data-stu-id="d21c2-172">Some common issues are:</span></span>

-   <span data-ttu-id="d21c2-173">Campos necessários no pedido SAML Olá em falta</span><span class="sxs-lookup"><span data-stu-id="d21c2-173">Missing required fields in hello SAML request</span></span>

-   <span data-ttu-id="d21c2-174">Método de pedido codificado de SAML</span><span class="sxs-lookup"><span data-stu-id="d21c2-174">SAML request encoded method</span></span>

<span data-ttu-id="d21c2-175">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="d21c2-175">**Resolution**</span></span>

1.  <span data-ttu-id="d21c2-176">Capture pedido SAML.</span><span class="sxs-lookup"><span data-stu-id="d21c2-176">Capture SAML request.</span></span> <span data-ttu-id="d21c2-177">Siga o tutorial Olá [como toodebug baseados em SAML único início de sessão tooapplications no Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn como toocapture Olá SAML do pedido.</span><span class="sxs-lookup"><span data-stu-id="d21c2-177">follow hello tutorial [How toodebug SAML-based single sign-on tooapplications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) toolearn how toocapture hello SAML request.</span></span>

2.  <span data-ttu-id="d21c2-178">Contacte o fabricante da aplicação Olá e partilha:</span><span class="sxs-lookup"><span data-stu-id="d21c2-178">Contact hello application vendor and share:</span></span>

   -   <span data-ttu-id="d21c2-179">Pedido SAML</span><span class="sxs-lookup"><span data-stu-id="d21c2-179">SAML request</span></span>

   -   [<span data-ttu-id="d21c2-180">Requisitos de protocolo do Azure AD único início de sessão SAML</span><span class="sxs-lookup"><span data-stu-id="d21c2-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="d21c2-181">Eles devem validar que suportam a implementação do Azure AD SAML Olá para o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="d21c2-181">They should validate they support hello Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="d21c2-182">Nenhum recurso na lista de requiredResourceAccess</span><span class="sxs-lookup"><span data-stu-id="d21c2-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="d21c2-183">*Aplicação de cliente do erro AADSTS65005:hello pediu acesso tooresource ' 00000002-0000-0000-c000-000000000000'. Este pedido falhou porque o cliente de Olá não especificou este recurso na lista de requiredResourceAccess*.</span><span class="sxs-lookup"><span data-stu-id="d21c2-183">*Error AADSTS65005:hello client application has requested access tooresource '00000002-0000-0000-c000-000000000000'. This request has failed because hello client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="d21c2-184">**Uma causa possível**</span><span class="sxs-lookup"><span data-stu-id="d21c2-184">**Possible cause**</span></span>

<span data-ttu-id="d21c2-185">objeto da aplicação Olá está danificado.</span><span class="sxs-lookup"><span data-stu-id="d21c2-185">hello application object is corrupted.</span></span>

<span data-ttu-id="d21c2-186">**Resolução: opção 1**</span><span class="sxs-lookup"><span data-stu-id="d21c2-186">**Resolution: option 1**</span></span>

<span data-ttu-id="d21c2-187">problema de Olá toosolve, adicione o valor do identificador exclusivo Olá na configuração de Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d21c2-187">toosolve hello problem, add hello unique Identifier value in hello Azure AD configuration.</span></span> <span data-ttu-id="d21c2-188">tooadd um valor de identificador, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="d21c2-188">tooadd a Identifier value, follow hello steps below:</span></span>

1.  <span data-ttu-id="d21c2-189">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-189">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d21c2-190">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-190">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d21c2-191">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="d21c2-191">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d21c2-192">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d21c2-192">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d21c2-193">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="d21c2-193">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d21c2-194">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-194">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d21c2-195">Selecione aplicação Olá tiver configurado o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="d21c2-195">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="d21c2-196">Depois de o carregamento da aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="d21c2-196">Once hello application loads, click on hello **Single sign-on** from hello application’s left hand navigation menu</span></span>

8.  <span data-ttu-id="d21c2-197">Em Olá **domínio e o URL** secção, verifique no Olá **Mostrar avançadas definições de URL**.</span><span class="sxs-lookup"><span data-stu-id="d21c2-197">Under hello **Domain and URL** section, check on hello **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="d21c2-198">no Olá **identificador** um identificador exclusivo para a aplicação Olá do tipo de caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d21c2-198">in hello **Identifier** textbox type a unique identifier for hello application.</span></span>

10. <span data-ttu-id="d21c2-199">**Guardar** configuração Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-199">**Save** hello configuration.</span></span>


<span data-ttu-id="d21c2-200">**Opção de resolução de 2**</span><span class="sxs-lookup"><span data-stu-id="d21c2-200">**Resolution option 2**</span></span>

<span data-ttu-id="d21c2-201">Se a opção 1 acima não resolver o problema, tente remover aplicação Olá do diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-201">If option 1 above did not work for you, try removing hello application from hello directory.</span></span> <span data-ttu-id="d21c2-202">Em seguida, adicionar e reconfigurar aplicação Olá, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="d21c2-202">Then, add and reconfigure hello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="d21c2-203">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-203">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d21c2-204">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-204">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d21c2-205">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="d21c2-205">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d21c2-206">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d21c2-206">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d21c2-207">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="d21c2-207">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="d21c2-208">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-208">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d21c2-209">Selecionar aplicação Olá pretende tooconfigure-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d21c2-209">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="d21c2-210">Clique em **eliminar** em Olá superior esquerdo da aplicação Olá **descrição geral** painel.</span><span class="sxs-lookup"><span data-stu-id="d21c2-210">Click **Delete** at hello top-left of hello application **Overview** blade.</span></span>

8.  <span data-ttu-id="d21c2-211">Atualizar do Azure AD e adicionar aplicação Olá da galeria do Azure AD Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-211">Refresh Azure AD and Add hello application from hello Azure AD gallery.</span></span> <span data-ttu-id="d21c2-212">Em seguida, Configure a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="d21c2-212">Then, Configure hello application</span></span>

<span data-ttu-id="d21c2-213"><span id="_Hlk477190176" class="anchor"></span>Após a reconfiguração da aplicação Olá, deve ser capaz de toosign na aplicação toohello.</span><span class="sxs-lookup"><span data-stu-id="d21c2-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring hello application, you should be able toosign in toohello application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="d21c2-214">Certificado ou chave não configurado</span><span class="sxs-lookup"><span data-stu-id="d21c2-214">Certificate or key not configured</span></span>

<span data-ttu-id="d21c2-215">*Erro AADSTS50003: Nenhuma chave de assinatura configurado.*</span><span class="sxs-lookup"><span data-stu-id="d21c2-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="d21c2-216">**Uma causa possível**</span><span class="sxs-lookup"><span data-stu-id="d21c2-216">**Possible cause**</span></span>

<span data-ttu-id="d21c2-217">objeto da aplicação Olá está danificado e do Azure AD não reconhece o certificado de Olá configurado para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-217">hello application object is corrupted and Azure AD doesn’t recognize hello certificate configured for hello application.</span></span>

<span data-ttu-id="d21c2-218">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="d21c2-218">**Resolution**</span></span>

<span data-ttu-id="d21c2-219">toodelete e criar um novo certificado, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="d21c2-219">toodelete and create a new certificate, follow hello steps below:</span></span>

1.  <span data-ttu-id="d21c2-220">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-220">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d21c2-221">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-221">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d21c2-222">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="d21c2-222">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d21c2-223">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d21c2-223">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d21c2-224">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="d21c2-224">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="d21c2-225">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-225">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d21c2-226">Selecionar aplicação Olá pretende tooconfigure-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d21c2-226">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="d21c2-227">Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="d21c2-227">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="d21c2-228">Clique em **criar novo certificado** em Olá **SAML certificado de assinatura** secção.</span><span class="sxs-lookup"><span data-stu-id="d21c2-228">click **Create new certificate** under hello **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="d21c2-229">Selecione a data de expiração.</span><span class="sxs-lookup"><span data-stu-id="d21c2-229">Select Expiration date.</span></span> <span data-ttu-id="d21c2-230">Em seguida, clique em **guardar.**</span><span class="sxs-lookup"><span data-stu-id="d21c2-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="d21c2-231">Verifique **tornar o novo certificado ativa** certificado do toooverride Olá Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d21c2-231">Check **Make new certificate active** toooverride hello active certificate.</span></span> <span data-ttu-id="d21c2-232">Em seguida, clique em **guardar** , Olá parte superior do painel de Olá e aceitar o certificado de rollover de Olá tooactivate.</span><span class="sxs-lookup"><span data-stu-id="d21c2-232">Then, click **Save** at hello top of hello blade and accept tooactivate hello rollover certificate.</span></span>

11. <span data-ttu-id="d21c2-233">Em Olá **certificado de assinatura de SAML** secção, clique em **remover** tooremove Olá **não utilizados** certificado.</span><span class="sxs-lookup"><span data-stu-id="d21c2-233">Under hello **SAML Signing Certificate** section, click **remove** tooremove hello **Unused** certificate.</span></span>

## <a name="problem-when-customizing-hello-saml-claims-sent-tooan-application"></a><span data-ttu-id="d21c2-234">Problema ao personalizar Olá SAML afirmações enviadas tooan aplicação</span><span class="sxs-lookup"><span data-stu-id="d21c2-234">Problem when customizing hello SAML claims sent tooan application</span></span>

<span data-ttu-id="d21c2-235">toolearn como afirmações de atributo do toocustomize Olá SAML enviada tooyour aplicação, consulte [afirmações mapeamento no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d21c2-235">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d21c2-236">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d21c2-236">Next steps</span></span>
[<span data-ttu-id="d21c2-237">Como toodebug baseados em SAML único início de sessão tooapplications no Azure AD</span><span class="sxs-lookup"><span data-stu-id="d21c2-237">How toodebug SAML-based single sign-on tooapplications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
