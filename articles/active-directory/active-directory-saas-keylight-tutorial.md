---
title: "Tutorial: Integração do Azure Active Directory com LockPath Keylight | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="f315e-103">Tutorial: Integração do Azure Active Directory com LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="f315e-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="f315e-104">Neste tutorial, saiba como toointegrate LockPath Keylight com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f315e-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f315e-105">Integrar LockPath Keylight com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="f315e-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f315e-106">Pode controlar no Azure AD que tenha acesso tooLockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="f315e-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="f315e-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooLockPath Keylight (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f315e-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f315e-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f315e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f315e-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f315e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f315e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f315e-110">Prerequisites</span></span>

<span data-ttu-id="f315e-111">integração do Azure AD com LockPath Keylight tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f315e-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="f315e-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f315e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f315e-113">Um LockPath Keylight início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="f315e-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f315e-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f315e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f315e-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f315e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f315e-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f315e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f315e-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f315e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f315e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f315e-118">Scenario description</span></span>
<span data-ttu-id="f315e-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f315e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f315e-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="f315e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f315e-121">Adicionar LockPath Keylight da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f315e-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="f315e-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f315e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="f315e-123">Adicionar LockPath Keylight da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f315e-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="f315e-124">tooconfigure Olá integração de LockPath Keylight com o Azure AD, é necessário tooadd LockPath Keylight Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="f315e-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f315e-125">**tooadd LockPath Keylight da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f315e-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f315e-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f315e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f315e-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f315e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f315e-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f315e-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="f315e-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f315e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="f315e-133">Na caixa de pesquisa de Olá, escreva **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="f315e-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="f315e-135">No painel de resultados de Olá, selecione **LockPath Keylight**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="f315e-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f315e-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f315e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f315e-138">Nesta secção, configure e teste do Azure AD-início de sessão único com LockPath Keylight com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f315e-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f315e-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá LockPath Keylight é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f315e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="f315e-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá LockPath Keylight tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f315e-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="f315e-141">No LockPath Keylight, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="f315e-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f315e-142">tooconfigure e teste do Azure AD-início de sessão único com LockPath Keylight, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f315e-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f315e-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f315e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f315e-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f315e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f315e-145">**[Criar um utilizador de teste LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave um homólogo de Britta Simon no LockPath Keylight que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="f315e-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f315e-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f315e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f315e-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="f315e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f315e-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f315e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f315e-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="f315e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="f315e-150">**tooconfigure do Azure AD-início de sessão único com LockPath Keylight, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f315e-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f315e-151">No Olá portal do Azure, no Olá **LockPath Keylight** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="f315e-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="f315e-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f315e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="f315e-155">No Olá **LockPath Keylight domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f315e-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="f315e-157">a.</span><span class="sxs-lookup"><span data-stu-id="f315e-157">a.</span></span> <span data-ttu-id="f315e-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="f315e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="f315e-159">b.</span><span class="sxs-lookup"><span data-stu-id="f315e-159">b.</span></span> <span data-ttu-id="f315e-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="f315e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="f315e-161">c.</span><span class="sxs-lookup"><span data-stu-id="f315e-161">c.</span></span> <span data-ttu-id="f315e-162">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="f315e-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="f315e-163">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="f315e-163">These values are not real.</span></span> <span data-ttu-id="f315e-164">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="f315e-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="f315e-165">Contacte [equipa de suporte de cliente de Keylight LockPath](https://www.lockpath.com/contact/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="f315e-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="f315e-166">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Raw)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="f315e-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="f315e-168">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="f315e-168">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="f315e-170">No Olá **LockPath Keylight configuração** secção, clique em **configurar Keylight de LockPath** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="f315e-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f315e-171">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="f315e-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="f315e-173">tooenable SSO no LockPath Keylight, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f315e-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="f315e-174">a.</span><span class="sxs-lookup"><span data-stu-id="f315e-174">a.</span></span> <span data-ttu-id="f315e-175">Início de sessão tooyour LockPath Keylight conta como administrador.</span><span class="sxs-lookup"><span data-stu-id="f315e-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="f315e-176">b.</span><span class="sxs-lookup"><span data-stu-id="f315e-176">b.</span></span> <span data-ttu-id="f315e-177">No menu de Olá na parte superior do Olá, clique em **pessoa**e selecione **Keylight configuração**.</span><span class="sxs-lookup"><span data-stu-id="f315e-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="f315e-179">c.</span><span class="sxs-lookup"><span data-stu-id="f315e-179">c.</span></span> <span data-ttu-id="f315e-180">Olá TreeView Olá esquerda, clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="f315e-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="f315e-182">d.</span><span class="sxs-lookup"><span data-stu-id="f315e-182">d.</span></span> <span data-ttu-id="f315e-183">No Olá **SAML definições** caixa de diálogo, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="f315e-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="f315e-185">No Olá **editar definições de SAML** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f315e-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="f315e-187">a.</span><span class="sxs-lookup"><span data-stu-id="f315e-187">a.</span></span> <span data-ttu-id="f315e-188">Definir **autenticação SAML** demasiado**Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f315e-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="f315e-189">b.</span><span class="sxs-lookup"><span data-stu-id="f315e-189">b.</span></span> <span data-ttu-id="f315e-190">Olá colar **único início de sessão no URL do serviço SAML** valor que copiou do Olá portal do Azure para Olá **URL de início de sessão do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f315e-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="f315e-191">c.</span><span class="sxs-lookup"><span data-stu-id="f315e-191">c.</span></span> <span data-ttu-id="f315e-192">Olá colar **único URL de serviço Sign-Out** valor que copiou do Olá portal do Azure para Olá **URL de fim de sessão do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f315e-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="f315e-193">d.</span><span class="sxs-lookup"><span data-stu-id="f315e-193">d.</span></span> <span data-ttu-id="f315e-194">Clique em **Escolher ficheiro** tooselect sua LockPath Keylight transferido do certificado e, em seguida, clique em **abra** certificado de Olá tooupload.</span><span class="sxs-lookup"><span data-stu-id="f315e-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="f315e-195">e.</span><span class="sxs-lookup"><span data-stu-id="f315e-195">e.</span></span> <span data-ttu-id="f315e-196">Definir **localização de Id de utilizador de SAML** demasiado**NameIdentifier elemento da instrução de assunto Olá**.</span><span class="sxs-lookup"><span data-stu-id="f315e-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="f315e-197">f.</span><span class="sxs-lookup"><span data-stu-id="f315e-197">f.</span></span> <span data-ttu-id="f315e-198">Fornecer Olá **fornecedor de serviços de Keylight** Olá seguir o padrão de utilização: **https://&lt;CompanyName&gt;. keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="f315e-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="f315e-199">g.</span><span class="sxs-lookup"><span data-stu-id="f315e-199">g.</span></span> <span data-ttu-id="f315e-200">Definir **utilizadores de aprovisionamento automático** demasiado**Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f315e-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="f315e-201">h.</span><span class="sxs-lookup"><span data-stu-id="f315e-201">h.</span></span> <span data-ttu-id="f315e-202">Definir **tipo de conta de aprovisionamento automático** demasiado**utilizador completo**.</span><span class="sxs-lookup"><span data-stu-id="f315e-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="f315e-203">posso.</span><span class="sxs-lookup"><span data-stu-id="f315e-203">i.</span></span> <span data-ttu-id="f315e-204">Definir **função de segurança de aprovisionamento automático**, selecione **utilizador padrão com SAML**.</span><span class="sxs-lookup"><span data-stu-id="f315e-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="f315e-205">j.</span><span class="sxs-lookup"><span data-stu-id="f315e-205">j.</span></span> <span data-ttu-id="f315e-206">Definir **configuração de segurança de aprovisionamento automático**, selecione **configuração de utilizador padrão**.</span><span class="sxs-lookup"><span data-stu-id="f315e-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="f315e-207">k.</span><span class="sxs-lookup"><span data-stu-id="f315e-207">k.</span></span> <span data-ttu-id="f315e-208">No Olá **atributo de correio eletrónico** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="f315e-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="f315e-209">l.</span><span class="sxs-lookup"><span data-stu-id="f315e-209">l.</span></span> <span data-ttu-id="f315e-210">No Olá **nome próprio atributo** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="f315e-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="f315e-211">m.</span><span class="sxs-lookup"><span data-stu-id="f315e-211">m.</span></span> <span data-ttu-id="f315e-212">No Olá **atributo de nome do último** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="f315e-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="f315e-213">n.</span><span class="sxs-lookup"><span data-stu-id="f315e-213">n.</span></span> <span data-ttu-id="f315e-214">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f315e-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f315e-215">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="f315e-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f315e-216">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="f315e-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f315e-217">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f315e-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f315e-218">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f315e-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="f315e-219">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f315e-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="f315e-221">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f315e-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f315e-222">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f315e-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f315e-224">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="f315e-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f315e-226">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="f315e-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f315e-228">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f315e-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f315e-230">a.</span><span class="sxs-lookup"><span data-stu-id="f315e-230">a.</span></span> <span data-ttu-id="f315e-231">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f315e-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f315e-232">b.</span><span class="sxs-lookup"><span data-stu-id="f315e-232">b.</span></span> <span data-ttu-id="f315e-233">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f315e-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f315e-234">c.</span><span class="sxs-lookup"><span data-stu-id="f315e-234">c.</span></span> <span data-ttu-id="f315e-235">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="f315e-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f315e-236">d.</span><span class="sxs-lookup"><span data-stu-id="f315e-236">d.</span></span> <span data-ttu-id="f315e-237">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f315e-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="f315e-238">Criar um utilizador de teste LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="f315e-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="f315e-239">Nesta secção, vai criar um utilizador chamado Britta Simon LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="f315e-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="f315e-240">LockPath Keylight suporta o aprovisionamento de just-in-time, que está ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="f315e-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="f315e-241">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="f315e-241">There is no action item for you in this section.</span></span> <span data-ttu-id="f315e-242">Um novo utilizador é criado quando aceder ao LockPath Keylight se o utilizador Olá ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="f315e-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="f315e-243">Se precisar de um utilizador de toocreate manualmente, terá de toocontact Olá [equipa de suporte de cliente de Keylight LockPath](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="f315e-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f315e-244">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f315e-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f315e-245">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooLockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="f315e-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="f315e-247">**tooassign Britta Simon tooLockPath Keylight, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f315e-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f315e-248">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f315e-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="f315e-250">Na lista de aplicações de Olá, selecione **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="f315e-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="f315e-252">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f315e-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="f315e-254">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="f315e-254">Click **Add** button.</span></span> <span data-ttu-id="f315e-255">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f315e-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="f315e-257">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="f315e-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f315e-258">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f315e-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f315e-259">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f315e-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f315e-260">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f315e-260">Testing single sign-on</span></span>

<span data-ttu-id="f315e-261">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f315e-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f315e-262">Ao clicar Olá LockPath Keylight na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour LockPath Keylight aplicação.</span><span class="sxs-lookup"><span data-stu-id="f315e-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f315e-263">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f315e-263">Additional resources</span></span>

* [<span data-ttu-id="f315e-264">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f315e-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f315e-265">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f315e-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

