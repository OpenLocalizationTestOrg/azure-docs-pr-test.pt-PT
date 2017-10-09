---
title: "aaaHow tooconfigure palavra-passe-início de sessão único para um applicationn não Galeria | Microsoft Docs"
description: "Como tooconfigure uma aplicação não Galeria personalizada para proteger com base em palavra-passe de início de sessão quando não está listado no Olá Galeria de aplicações do Azure AD"
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
ms.openlocfilehash: e3d0e658f792a0a63110a198811edc66acd6ccf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="5ab67-103">Como a palavra-passe de tooconfigure único início de sessão para uma aplicação não Galeria</span><span class="sxs-lookup"><span data-stu-id="5ab67-103">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="5ab67-104">Além disso toohello escolhas encontrados Olá do Azure AD Galeria de aplicações, tem também de Olá opção tooadd um **não Galeria aplicação** quando aplicação Olá pretende não estiver indicada não existe.</span><span class="sxs-lookup"><span data-stu-id="5ab67-104">In addition toohello choices found within hello Azure AD Application Gallery, you also have hello option tooadd a **non-gallery application** when hello application you want is not listed there.</span></span> <span data-ttu-id="5ab67-105">Através desta funcionalidade, pode adicionar qualquer aplicação que já existe na sua organização ou as aplicações de terceiros que poderá utilizar de um fornecedor que já não faz parte de Olá [Galeria de aplicações do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="5ab67-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="5ab67-106">Depois de adicionar uma aplicação não galeria, em seguida, pode configurar Olá único início de sessão método utiliza esta aplicação, selecionando Olá **Single Sign-on** item de navegação numa aplicação empresarial no Olá [Portal do Azure ](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5ab67-106">Once you add a non-gallery application, you can then configure hello Single sign-on method this application uses by selecting hello **Single Sign-on** navigation item on an Enterprise Application in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="5ab67-107">Uma das Olá Single Sign-on métodos disponível tooyou é Olá [baseada em palavra-passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opção.</span><span class="sxs-lookup"><span data-stu-id="5ab67-107">One of hello Single Sign-on methods available tooyou is hello [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="5ab67-108">Com Olá **adicionar uma aplicação não galeria** experiência, pode integrar qualquer aplicação que apresenta um nome de utilizador baseado em HTML e a palavra-passe de entrada no campo, mesmo que não está no nosso conjunto de aplicações previamente integradas.</span><span class="sxs-lookup"><span data-stu-id="5ab67-108">With hello **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="5ab67-109">Isto funciona de forma de Olá é uma página scraping tecnologia que faz parte de Olá extensão do painel de acesso que nos permite tooauto-detetar campos de entrada de nome de utilizador e palavra-passe, armazená-las de forma segura para a instância de aplicação específica.</span><span class="sxs-lookup"><span data-stu-id="5ab67-109">hello way this works is by a page scraping technology that is part of hello Access Panel extension that allows us tooauto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="5ab67-110">Em seguida, em segurança reprodução de nomes de utilizador e os campos de toothose de palavras-passe quando um utilizador navega toothat aplicação no painel de acesso da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-110">Then securely replay usernames and passwords toothose fields when a user navigates toothat application on hello application access panel.</span></span>

<span data-ttu-id="5ab67-111">Esta é uma excelente forma de tooget iniciado integrar qualquer tipo de aplicação com o Azure AD rapidamente e permite-lhe:</span><span class="sxs-lookup"><span data-stu-id="5ab67-111">This is a great way tooget started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="5ab67-112">Integrar **qualquer aplicação na Olá mundo** com o seu inquilino do Azure AD, por isso, desde compõe um campo de entrada HTML nome de utilizador e palavra-passe</span><span class="sxs-lookup"><span data-stu-id="5ab67-112">Integrate **any application in hello world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="5ab67-113">Ativar **-início de sessão único para os seus utilizadores** em segurança, armazenar e replaying nomes de utilizador e palavras-passe para a aplicação Olá tiver integrado com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ab67-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for hello application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="5ab67-114">**Entrada de deteção automática** campos para qualquer aplicação e permitem-lhe toomanually detetar esses campos utilizando Olá extensão de Browser do painel de acesso, no caso de deteção automática não encontrá-los</span><span class="sxs-lookup"><span data-stu-id="5ab67-114">**Auto-detect input** fields for any application and allow you toomanually detect those fields using hello Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="5ab67-115">**Suporta aplicações que necessitam de vários campos de início de sessão** para aplicações que necessitam de mais do que apenas nome de utilizador e palavra-passe campos toosign no</span><span class="sxs-lookup"><span data-stu-id="5ab67-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields toosign in</span></span>

-   <span data-ttu-id="5ab67-116">**Personalizar etiquetas Olá** dos campos de entrada nome de utilizador e palavra-passe Olá os seus utilizadores verão no Olá [painel de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) quando ele introduzir as respetivas credenciais</span><span class="sxs-lookup"><span data-stu-id="5ab67-116">**Customize hello labels** of hello username and password input fields your users see on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="5ab67-117">Permitir o **utilizadores** tooprovide os seus próprios nomes de utilizador e palavras-passe para as contas de aplicação existentes que são escrever manualmente no Olá [painel de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="5ab67-117">Allow your **users** tooprovide their own usernames and passwords for any existing application accounts they are typing in manually on hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="5ab67-118">Permitir que um **membro do grupo de empresas Olá** nomes de utilizador do toospecify Olá e palavras-passe tooa utilizador atribuído utilizando Olá [Self-Service de acesso de aplicação](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funcionalidade</span><span class="sxs-lookup"><span data-stu-id="5ab67-118">Allow a **member of hello business group** toospecify hello usernames and passwords assigned tooa user by using hello [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="5ab67-119">Permitir que um **administrador** nomes de utilizador do toospecify Olá e palavras-passe atribuídas tooa utilizador com credenciais de atualização de Olá funcionalidade quando [atribuir uma aplicação de tooan do utilizador](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="5ab67-119">Allow an **administrator** toospecify hello usernames and passwords assigned tooa user by using hello Update Credentials feature when [assigning a user tooan application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="5ab67-120">Permitir que um **administrador** funcionalidade quando o nome de utilizador do toospecify Olá partilhado ou palavra-passe utilizada por um grupo de pessoas com as credenciais de atualização de Olá [atribuir uma aplicação de tooan de grupo](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="5ab67-120">Allow an **administrator** toospecify hello shared username or password used by a group of people by using hello Update Credentials feature when [assigning a group tooan application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="5ab67-121">A seguir descreve como pode permitir [baseada em palavra-passe Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) aplicação tooany adicionar utilizando Olá **adicionar uma aplicação não galeria** experiência.</span><span class="sxs-lookup"><span data-stu-id="5ab67-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooany application that you add using hello **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="5ab67-122">Descrição geral dos passos necessários</span><span class="sxs-lookup"><span data-stu-id="5ab67-122">Overview of steps required</span></span>

<span data-ttu-id="5ab67-123">tooconfigure uma aplicação na galeria do Azure AD de Olá tem de:</span><span class="sxs-lookup"><span data-stu-id="5ab67-123">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="5ab67-124">Adicionar uma aplicação não Galeria</span><span class="sxs-lookup"><span data-stu-id="5ab67-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="5ab67-125">Configurar aplicação Olá para palavra-passe-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="5ab67-125">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="5ab67-126">Atribuir Olá aplicação tooa utilizador ou um grupo</span><span class="sxs-lookup"><span data-stu-id="5ab67-126">Assign hello application tooa user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="5ab67-127">Atribuir diretamente uma aplicação de tooan do utilizador</span><span class="sxs-lookup"><span data-stu-id="5ab67-127">Assign a user tooan application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="5ab67-128">Atribuir diretamente o grupo de tooa uma aplicação</span><span class="sxs-lookup"><span data-stu-id="5ab67-128">Assign an application tooa group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="5ab67-129">Adicionar uma aplicação não Galeria</span><span class="sxs-lookup"><span data-stu-id="5ab67-129">Add a non-gallery application</span></span>

<span data-ttu-id="5ab67-130">tooadd uma aplicação Olá Galeria AD do Azure, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="5ab67-130">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="5ab67-131">Abra Olá [Portal do Azure](https://portal.azure.com) e inicie sessão como um **Administrador Global** ou **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="5ab67-131">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="5ab67-132">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-132">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5ab67-133">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5ab67-133">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5ab67-134">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ab67-134">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5ab67-135">Clique em Olá **adicionar** botão no canto superior direito de Olá no Olá **aplicações empresariais** painel</span><span class="sxs-lookup"><span data-stu-id="5ab67-135">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="5ab67-136">Clique em **aplicação não galeria.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="5ab67-137">Introduza o nome de Olá da sua aplicação no Olá **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="5ab67-137">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="5ab67-138">Selecione **adicionar.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-138">Select **Add.**</span></span>

<span data-ttu-id="5ab67-139">Após um curto período de tempo, ser painel de configuração da aplicação Olá toosee possível.</span><span class="sxs-lookup"><span data-stu-id="5ab67-139">After a short period, you be able toosee hello application’s configuration blade.</span></span>

## <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="5ab67-140">Configurar aplicação Olá para palavra-passe-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="5ab67-140">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="5ab67-141">tooconfigure-início de sessão único para uma aplicação, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="5ab67-141">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="5ab67-142">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-142">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5ab67-143">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-143">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5ab67-144">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5ab67-144">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5ab67-145">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ab67-145">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5ab67-146">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="5ab67-146">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5ab67-147">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-147">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5ab67-148">Selecione aplicação Olá pretende tooconfigure-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="5ab67-148">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="5ab67-149">Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-149">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5ab67-150">Modo de Olá selecione **baseada em palavra-passe de início de sessão.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-150">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="5ab67-151">Introduza Olá **URL de início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="5ab67-151">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="5ab67-152">Este é o URL de olá onde os utilizadores introduzem as respetivas toosign no nome de utilizador e palavra-passe para.</span><span class="sxs-lookup"><span data-stu-id="5ab67-152">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="5ab67-153">Certifique-se de que o início de sessão Olá nos campos está visíveis no URL Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-153">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="5ab67-154">Atribua utilizadores toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="5ab67-154">Assign users toohello application.</span></span>

11. <span data-ttu-id="5ab67-155">Além disso, também pode fornecer as credenciais em nome de utilizador de Olá, selecionar linhas Olá de utilizadores de Olá e clicando na **credenciais de atualização** e introduzindo Olá nome de utilizador e palavra-passe em nome dos utilizadores de Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-155">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="5ab67-156">Caso contrário, os utilizadores ser tooenter pedido Olá credenciais próprios após iniciar.</span><span class="sxs-lookup"><span data-stu-id="5ab67-156">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="assign-a-user-tooan-application-directly"></a><span data-ttu-id="5ab67-157">Atribuir diretamente uma aplicação de tooan do utilizador</span><span class="sxs-lookup"><span data-stu-id="5ab67-157">Assign a user tooan application directly</span></span>

<span data-ttu-id="5ab67-158">tooassign um ou mais aplicações de tooan utilizadores diretamente, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="5ab67-158">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="5ab67-159">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5ab67-160">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5ab67-161">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5ab67-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5ab67-162">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ab67-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5ab67-163">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="5ab67-163">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5ab67-164">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5ab67-165">Selecione aplicação Olá pretende tooassign uma lista de Olá de toofrom do utilizador.</span><span class="sxs-lookup"><span data-stu-id="5ab67-165">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="5ab67-166">Quando carrega a aplicação Olá, clique em **utilizadores e grupos** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-166">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5ab67-167">Clique em Olá **adicionar** botão por cima Olá **utilizadores e grupos** Olá de tooopen lista **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="5ab67-167">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5ab67-168">Clique em Olá **utilizadores e grupos** Seletor de Olá **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="5ab67-168">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5ab67-169">Tipo de Olá **nome completo** ou **endereço de correio eletrónico** do utilizador Olá estiver interessado em atribuir para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5ab67-169">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5ab67-170">Coloque o cursor sobre Olá **utilizador** no Olá lista tooreveal um **caixa de verificação**.</span><span class="sxs-lookup"><span data-stu-id="5ab67-170">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="5ab67-171">Clique em tooadd de fotografias ou logótipo do perfil do Olá caixa de verificação seguinte toohello utilizador seu utilizador toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="5ab67-171">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="5ab67-172">**Opcional:** se gostaria demasiado**adicionar mais do que um utilizador**, tipo noutra **nome completo** ou **endereço de correio eletrónico** para Olá **pesquisar por nome ou o endereço de correio eletrónico** caixa de pesquisa e clique em Olá caixa de verificação tooadd toohello este utilizador **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="5ab67-172">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="5ab67-173">Quando tiver terminado de selecionar utilizadores, clique em Olá **selecione** botão tooadd-los toohello lista de utilizadores e grupos toobe atribuído toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="5ab67-173">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="5ab67-174">**Opcional:** clique Olá **selecionar função** Seletor no Olá **adicionar atribuição** painel tooselect uma função tooassign toohello utilizadores que selecionou.</span><span class="sxs-lookup"><span data-stu-id="5ab67-174">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="5ab67-175">Clique em Olá **atribuir** botão tooassign Olá aplicação toohello utilizadores selecionados.</span><span class="sxs-lookup"><span data-stu-id="5ab67-175">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

## <a name="assign-an-application-tooa-group-directly"></a><span data-ttu-id="5ab67-176">Atribuir diretamente o grupo de tooa uma aplicação</span><span class="sxs-lookup"><span data-stu-id="5ab67-176">Assign an application tooa group directly</span></span>

<span data-ttu-id="5ab67-177">tooassign um ou mais grupos de aplicações de tooan diretamente, siga Olá passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="5ab67-177">tooassign one or more groups tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="5ab67-178">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-178">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5ab67-179">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-179">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5ab67-180">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="5ab67-180">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5ab67-181">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5ab67-181">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5ab67-182">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="5ab67-182">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="5ab67-183">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="5ab67-183">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="5ab67-184">Selecione aplicação Olá pretende tooassign uma lista de Olá de toofrom do utilizador.</span><span class="sxs-lookup"><span data-stu-id="5ab67-184">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="5ab67-185">Quando carrega a aplicação Olá, clique em **utilizadores e grupos** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5ab67-185">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="5ab67-186">Clique em Olá **adicionar** botão por cima Olá **utilizadores e grupos** Olá de tooopen lista **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="5ab67-186">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="5ab67-187">Clique em Olá **utilizadores e grupos** Seletor de Olá **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="5ab67-187">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="5ab67-188">Tipo de Olá **nome do grupo completa** do grupo de Olá estiver interessado em atribuir para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5ab67-188">Type in hello **full group name** of hello group you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="5ab67-189">Coloque o cursor sobre Olá **grupo** no Olá lista tooreveal um **caixa de verificação**.</span><span class="sxs-lookup"><span data-stu-id="5ab67-189">Hover over hello **group** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="5ab67-190">Clique em tooadd de fotografias ou logótipo do perfil do Olá caixa de verificação seguinte toohello grupo seu utilizador toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="5ab67-190">Click hello checkbox next toohello group’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="5ab67-191">**Opcional:** se gostaria demasiado**adicionar mais de um grupo**, tipo noutra **nome do grupo completo de** para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa e clique em Olá caixa de verificação tooadd toohello este grupo **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="5ab67-191">**Optional:** If you would like too**add more than one group**, type in another **full group name** into hello **Search by name or email address** search box, and click hello checkbox tooadd this group toohello **Selected** list.</span></span>

13. <span data-ttu-id="5ab67-192">Quando tiver terminado de selecionar grupos, clique em Olá **selecione** botão tooadd-los toohello lista de utilizadores e grupos toobe atribuído toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="5ab67-192">When you are finished selecting groups, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="5ab67-193">**Opcional:** clique Olá **selecionar função** Seletor no Olá **adicionar atribuição** painel tooselect toohello de tooassign uma função de grupos selecionou.</span><span class="sxs-lookup"><span data-stu-id="5ab67-193">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello groups you have selected.</span></span>

15. <span data-ttu-id="5ab67-194">Clique em Olá **atribuir** botão tooassign Olá aplicação toohello grupos selecionados.</span><span class="sxs-lookup"><span data-stu-id="5ab67-194">Click hello **Assign** button tooassign hello application toohello selected groups.</span></span>

<span data-ttu-id="5ab67-195">Após um curto período de tempo, os utilizadores Olá que selecionou ser capaz de toolaunch estas aplicações em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="5ab67-195">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ab67-196">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5ab67-196">Next steps</span></span>
[<span data-ttu-id="5ab67-197">Fornecer aplicações de tooyour de início de sessão único com o Proxy da aplicação</span><span class="sxs-lookup"><span data-stu-id="5ab67-197">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
