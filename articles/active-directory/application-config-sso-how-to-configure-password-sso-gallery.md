---
title: "aaaHow tooconfigure palavra-passe-início de sessão único para uma aplicação de galeria do Azure AD | Microsoft Docs"
description: "Como tooconfigure uma aplicação para proteger com base em palavra-passe de início de sessão quando já está listado no Olá Galeria de aplicações do Azure AD"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="cbb4f-103">Como a palavra-passe de tooconfigure único início de sessão para uma aplicação de galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbb4f-103">How tooconfigure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="cbb4f-104">Quando adiciona uma aplicação Olá [Galeria de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), tem de escolher Olá como pretende que o seu toosign de utilizadores na aplicação toothat.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-104">When you add an application from hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have hello choice of how you want your users toosign in toothat application.</span></span> <span data-ttu-id="cbb4f-105">Pode configurar esta opção em qualquer altura, selecionando Olá **Single Sign-on** item de navegação numa aplicação empresarial no Olá [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cbb4f-105">You can configure this choice at any time by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="cbb4f-106">Uma das Olá métodos de início de sessão único disponíveis tooyou é Olá [baseada em palavra-passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opção.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-106">One of hello single sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="cbb4f-107">Esta é uma excelente forma de tooget iniciado integrar aplicações com o Azure AD rapidamente e permite-lhe:</span><span class="sxs-lookup"><span data-stu-id="cbb4f-107">This is a great way tooget started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="cbb4f-108">Ativar **-início de sessão único para os seus utilizadores** em segurança, armazenar e replaying nomes de utilizador e palavras-passe para a aplicação Olá tiver integrado com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="cbb4f-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="cbb4f-109">**Suporta aplicações que necessitam de vários campos de início de sessão** para aplicações que necessitam de mais do que apenas nome de utilizador e palavra-passe campos toosign no</span><span class="sxs-lookup"><span data-stu-id="cbb4f-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="cbb4f-110">**Personalizar etiquetas Olá** dos campos de entrada nome de utilizador e palavra-passe Olá os seus utilizadores verão no Olá [painel de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando ele introduzir as respetivas credenciais</span><span class="sxs-lookup"><span data-stu-id="cbb4f-110">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="cbb4f-111">Permitir o **utilizadores** tooprovide os seus próprios nomes de utilizador e palavras-passe para as contas de aplicação existentes que são escrever manualmente no Olá [painel de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="cbb4f-111">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="cbb4f-112">Permitir que um **membro do grupo de empresas Olá** nomes de utilizador do toospecify Olá e palavras-passe tooa utilizador atribuído utilizando Olá [Self-Service de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funcionalidade</span><span class="sxs-lookup"><span data-stu-id="cbb4f-112">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="cbb4f-113">Permitir que um **administrador** nomes de utilizador do toospecify Olá e palavras-passe atribuídas tooa utilizador com credenciais de atualização de Olá funcionalidade quando [atribuir uma aplicação de tooan do utilizador](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="cbb4f-113">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="cbb4f-114">Permitir que um **administrador** funcionalidade quando o nome de utilizador do toospecify Olá partilhado ou palavra-passe utilizada por um grupo de pessoas com as credenciais de atualização de Olá [atribuir uma aplicação de tooan de grupo](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="cbb4f-114">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="cbb4f-115">A seguir descreve como pode permitir [baseada em palavra-passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan aplicação que já está a ser Olá [Galeria de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="cbb4f-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan application that is already in hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="cbb4f-116">Descrição geral dos passos necessários</span><span class="sxs-lookup"><span data-stu-id="cbb4f-116">Overview of steps required</span></span>
<span data-ttu-id="cbb4f-117">tooconfigure uma aplicação na galeria do Azure AD de Olá tem de:</span><span class="sxs-lookup"><span data-stu-id="cbb4f-117">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="cbb4f-118">Adicionar uma aplicação a partir da galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="cbb4f-118">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="cbb4f-119">Configurar aplicação Olá para palavra-passe-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="cbb4f-119">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="cbb4f-120">Atribuir Olá aplicação tooa utilizador ou um grupo</span><span class="sxs-lookup"><span data-stu-id="cbb4f-120">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="cbb4f-121">Atribuir diretamente uma aplicação de tooan do utilizador</span><span class="sxs-lookup"><span data-stu-id="cbb4f-121">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="cbb4f-122">Atribuir diretamente o grupo de tooa uma aplicação</span><span class="sxs-lookup"><span data-stu-id="cbb4f-122">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="cbb4f-123">Adicionar uma aplicação a partir da galeria do Azure AD Olá</span><span class="sxs-lookup"><span data-stu-id="cbb4f-123">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="cbb4f-124">tooadd uma aplicação Olá Galeria AD do Azure, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbb4f-124">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="cbb4f-125">Abra Olá [Portal do Azure](https://portal.azure.com) e inicie sessão como um **Administrador Global** ou **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="cbb4f-125">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="cbb4f-126">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-126">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cbb4f-127">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-127">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cbb4f-128">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-128">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cbb4f-129">Clique em Olá **adicionar** botão no canto superior direito de Olá no Olá **aplicações empresariais** painel</span><span class="sxs-lookup"><span data-stu-id="cbb4f-129">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="cbb4f-130">No Olá **introduza um nome** caixa de texto de Olá **adicionar da Galeria de Olá** secção, o nome do tipo Olá da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="cbb4f-130">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="cbb4f-131">Selecionar aplicação Olá pretende tooconfigure para o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="cbb4f-131">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="cbb4f-132">Antes de adicionar aplicação Olá, pode alterar o respetivo nome de Olá **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-132">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="cbb4f-133">Clique em **adicionar** botão, a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-133">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="cbb4f-134">Após um curto período de tempo, ser painel de configuração da aplicação Olá toosee possível.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-134">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="cbb4f-135">Configurar aplicação Olá para palavra-passe-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="cbb4f-135">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="cbb4f-136">tooconfigure-início de sessão único para uma aplicação, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbb4f-136">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="cbb4f-137">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="cbb4f-137">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cbb4f-138">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-138">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cbb4f-139">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-139">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cbb4f-140">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-140">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cbb4f-141">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-141">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="cbb4f-142">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="cbb4f-142">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cbb4f-143">Selecionar aplicação Olá pretende tooconfigure-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="cbb4f-143">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="cbb4f-144">Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-144">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cbb4f-145">Modo de Olá selecione **baseada em palavra-passe de início de sessão.**</span><span class="sxs-lookup"><span data-stu-id="cbb4f-145">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="cbb4f-146">[Atribuir utilizadores toohello aplicação](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="cbb4f-146">[Assign users toohello application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="cbb4f-147">Além disso, também pode fornecer as credenciais em nome de utilizador de Olá, selecionar linhas Olá de utilizadores de Olá e clicando na **credenciais de atualização** e introduzindo Olá nome de utilizador e palavra-passe em nome dos utilizadores de Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-147">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="cbb4f-148">Caso contrário, os utilizadores ser tooenter pedido Olá credenciais próprios após iniciar.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-148">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="cbb4f-149">Atribuir diretamente uma aplicação de tooan do utilizador</span><span class="sxs-lookup"><span data-stu-id="cbb4f-149">Assign a user tooan application directly</span></span>

<span data-ttu-id="cbb4f-150">tooassign um ou mais aplicações de tooan utilizadores diretamente, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbb4f-150">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="cbb4f-151">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="cbb4f-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="cbb4f-152">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cbb4f-153">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cbb4f-154">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cbb4f-155">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="cbb4f-156">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="cbb4f-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cbb4f-157">Selecione aplicação Olá pretende tooassign uma lista de Olá de toofrom do utilizador.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-157">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="cbb4f-158">Quando carrega a aplicação Olá, clique em **utilizadores e grupos** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-158">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cbb4f-159">Clique em Olá **adicionar** botão por cima Olá **utilizadores e grupos** Olá de tooopen lista **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-159">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="cbb4f-160">Clique em Olá **utilizadores e grupos** Seletor de Olá **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-160">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="cbb4f-161">Tipo de Olá **nome completo** ou **endereço de correio eletrónico** do utilizador Olá estiver interessado em atribuir para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-161">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="cbb4f-162">Coloque o cursor sobre Olá **utilizador** no Olá lista tooreveal um **caixa de verificação**.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-162">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="cbb4f-163">Clique em tooadd de fotografias ou logótipo do perfil do Olá caixa de verificação seguinte toohello utilizador seu utilizador toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-163">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="cbb4f-164">**Opcional:** se gostaria demasiado**adicionar mais do que um utilizador**, tipo noutra **nome completo** ou **endereço de correio eletrónico** para Olá **pesquisar por nome ou o endereço de correio eletrónico** caixa de pesquisa e clique em Olá caixa de verificação tooadd toohello este utilizador **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-164">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="cbb4f-165">Quando tiver terminado de selecionar utilizadores, clique em Olá **selecione** botão tooadd-los toohello lista de utilizadores e grupos toobe atribuído toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-165">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="cbb4f-166">**Opcional:** clique Olá **selecionar função** Seletor no Olá **adicionar atribuição** painel tooselect uma função tooassign toohello utilizadores que selecionou.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-166">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="cbb4f-167">Clique em Olá **atribuir** botão tooassign Olá aplicação toohello utilizadores selecionados.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-167">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="cbb4f-168">Atribuir diretamente o grupo de tooa uma aplicação</span><span class="sxs-lookup"><span data-stu-id="cbb4f-168">Assign an application tooa group directly</span></span>

<span data-ttu-id="cbb4f-169">tooassign um ou mais grupos de aplicações de tooan diretamente, siga Olá passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbb4f-169">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="cbb4f-170">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="cbb4f-170">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="cbb4f-171">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-171">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cbb4f-172">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-172">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cbb4f-173">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-173">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cbb4f-174">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-174">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="cbb4f-175">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="cbb4f-175">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cbb4f-176">Selecione aplicação Olá pretende tooassign uma lista de Olá de toofrom do utilizador.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-176">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="cbb4f-177">Quando carrega a aplicação Olá, clique em **utilizadores e grupos** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-177">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cbb4f-178">Clique em Olá **adicionar** botão por cima Olá **utilizadores e grupos** Olá de tooopen lista **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-178">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="cbb4f-179">Clique em Olá **utilizadores e grupos** Seletor de Olá **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-179">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="cbb4f-180">Tipo de Olá **nome do grupo completa** do grupo de Olá estiver interessado em atribuir para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-180">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="cbb4f-181">Coloque o cursor sobre Olá **grupo** no Olá lista tooreveal um **caixa de verificação**.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-181">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="cbb4f-182">Clique em tooadd de fotografias ou logótipo do perfil do Olá caixa de verificação seguinte toohello grupo seu utilizador toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-182">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="cbb4f-183">**Opcional:** se gostaria demasiado**adicionar mais de um grupo**, tipo noutra **nome do grupo completo de** para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa e clique em Olá caixa de verificação tooadd toohello este grupo **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-183">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="cbb4f-184">Quando tiver terminado de selecionar grupos, clique em Olá **selecione** botão tooadd-los toohello lista de utilizadores e grupos toobe atribuído toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-184">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="cbb4f-185">**Opcional:** clique Olá **selecionar função** Seletor no Olá **adicionar atribuição** painel tooselect toohello de tooassign uma função de grupos selecionou.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-185">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="cbb4f-186">Clique em Olá **atribuir** botão tooassign Olá aplicação toohello grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-186">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="cbb4f-187">Após um curto período de tempo, os utilizadores Olá que selecionou ser capaz de toolaunch estas aplicações em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="cbb4f-187">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbb4f-188">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cbb4f-188">Next steps</span></span>
[<span data-ttu-id="cbb4f-189">Fornecer aplicações de tooyour de início de sessão único com o Proxy da aplicação</span><span class="sxs-lookup"><span data-stu-id="cbb4f-189">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
