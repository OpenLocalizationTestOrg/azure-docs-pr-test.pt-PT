---
title: "Tutorial: Integração do Azure Active Directory com direta | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e direto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="da47f-103">Tutorial: Integração do Azure Active Directory com direta</span><span class="sxs-lookup"><span data-stu-id="da47f-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="da47f-104">Neste tutorial, saiba como toointegrate direta com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="da47f-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da47f-105">Integração direta com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="da47f-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="da47f-106">Pode controlar no Azure AD que tenha acesso tooDirect</span><span class="sxs-lookup"><span data-stu-id="da47f-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="da47f-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooDirect (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="da47f-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da47f-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da47f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="da47f-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da47f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da47f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="da47f-110">Prerequisites</span></span>

<span data-ttu-id="da47f-111">tooconfigure a integração do Azure AD com direta, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="da47f-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="da47f-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="da47f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da47f-113">Um direto-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="da47f-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da47f-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="da47f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da47f-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="da47f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da47f-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="da47f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da47f-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da47f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da47f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="da47f-118">Scenario description</span></span>
<span data-ttu-id="da47f-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="da47f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da47f-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="da47f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da47f-121">Adicionar direta a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="da47f-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="da47f-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="da47f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="da47f-123">Adicionar direta a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="da47f-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="da47f-124">tooconfigure Olá integração de direta com o Azure AD, é necessário tooadd direta Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="da47f-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="da47f-125">**tooadd direta a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="da47f-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="da47f-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="da47f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da47f-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="da47f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="da47f-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="da47f-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="da47f-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da47f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="da47f-133">Na caixa de pesquisa de Olá, escreva **direta**.</span><span class="sxs-lookup"><span data-stu-id="da47f-133">In hello search box, type **Direct**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="da47f-135">No painel de resultados de Olá, selecione **direta**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="da47f-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da47f-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="da47f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da47f-138">Nesta secção, configurar e testar do Azure AD-início de sessão único com direta com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="da47f-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="da47f-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá é direta tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da47f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="da47f-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados com o utilizador no toobe necessidades direta estabelecida.</span><span class="sxs-lookup"><span data-stu-id="da47f-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="da47f-141">Em direto, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="da47f-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="da47f-142">tooconfigure e teste do Azure AD de sessão único-com direta, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="da47f-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="da47f-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="da47f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="da47f-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="da47f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da47f-145">**[Criar um utilizador de teste direta](#creating-a-direct-test-user)**  -toohave um homólogo de Britta Simon em direto é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="da47f-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="da47f-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="da47f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da47f-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="da47f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da47f-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="da47f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da47f-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação em direta.</span><span class="sxs-lookup"><span data-stu-id="da47f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="da47f-150">**tooconfigure do Azure AD-início de sessão único com direta, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="da47f-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="da47f-151">No Olá portal do Azure, no Olá **direta** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="da47f-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="da47f-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="da47f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="da47f-155">No Olá **domínio direta e URLs** secção, se desejar aplicação Olá tooconfigure **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="da47f-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="da47f-157">No Olá **identificador** caixa de texto, tipo Olá URL:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="da47f-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="da47f-158">Verifique **Mostrar avançadas definições de URL**, se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="da47f-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="da47f-160">No Olá **URL de início de sessão** caixa de texto, tipo Olá URL:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="da47f-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="da47f-161">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="da47f-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="da47f-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="da47f-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="da47f-165">tooconfigure-início de sessão único em **direta** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte direto](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="da47f-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="da47f-166">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="da47f-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="da47f-167">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="da47f-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="da47f-168">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="da47f-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da47f-169">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="da47f-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="da47f-170">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="da47f-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="da47f-172">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="da47f-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="da47f-173">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="da47f-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da47f-175">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="da47f-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da47f-177">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="da47f-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da47f-179">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="da47f-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da47f-181">a.</span><span class="sxs-lookup"><span data-stu-id="da47f-181">a.</span></span> <span data-ttu-id="da47f-182">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="da47f-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da47f-183">b.</span><span class="sxs-lookup"><span data-stu-id="da47f-183">b.</span></span> <span data-ttu-id="da47f-184">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="da47f-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da47f-185">c.</span><span class="sxs-lookup"><span data-stu-id="da47f-185">c.</span></span> <span data-ttu-id="da47f-186">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="da47f-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="da47f-187">d.</span><span class="sxs-lookup"><span data-stu-id="da47f-187">d.</span></span> <span data-ttu-id="da47f-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="da47f-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="da47f-189">Criar um utilizador de teste direta</span><span class="sxs-lookup"><span data-stu-id="da47f-189">Creating a Direct test user</span></span>

<span data-ttu-id="da47f-190">Nesta secção, vai criar um utilizador chamado Britta Simon em direto.</span><span class="sxs-lookup"><span data-stu-id="da47f-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="da47f-191">Trabalhar com [equipa de suporte direto](https://direct4b.com/ja/support.html#inquiry) para adicionar utilizadores de Olá na plataforma direta Olá.</span><span class="sxs-lookup"><span data-stu-id="da47f-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="da47f-192">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="da47f-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="da47f-193">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="da47f-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="da47f-194">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooDirect.</span><span class="sxs-lookup"><span data-stu-id="da47f-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="da47f-196">**tooassign Britta Simon tooDirect, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="da47f-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="da47f-197">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="da47f-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="da47f-199">Na lista de aplicações de Olá, selecione **direta**.</span><span class="sxs-lookup"><span data-stu-id="da47f-199">In hello applications list, select **Direct**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="da47f-201">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="da47f-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="da47f-203">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="da47f-203">Click **Add** button.</span></span> <span data-ttu-id="da47f-204">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da47f-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="da47f-206">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="da47f-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="da47f-207">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da47f-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da47f-208">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="da47f-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="da47f-209">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="da47f-209">Testing single sign-on</span></span>

<span data-ttu-id="da47f-210">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="da47f-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="da47f-211">Se desejar tootest no **IDP iniciada modo**:</span><span class="sxs-lookup"><span data-stu-id="da47f-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="da47f-212">Ao clicar em Olá **direta** Olá de mosaico no painel de acesso, deve obter automaticamente com sessão iniciada tooyour **direta** aplicação.</span><span class="sxs-lookup"><span data-stu-id="da47f-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="da47f-213">Se desejar tootest no **SP iniciada modo**:</span><span class="sxs-lookup"><span data-stu-id="da47f-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="da47f-214">a.</span><span class="sxs-lookup"><span data-stu-id="da47f-214">a.</span></span> <span data-ttu-id="da47f-215">Clique em Olá **direta** mosaico no painel de acesso de Olá e deixará de ser redirecionada toohello página aplicação de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="da47f-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="da47f-216">b.</span><span class="sxs-lookup"><span data-stu-id="da47f-216">b.</span></span> <span data-ttu-id="da47f-217">Introduza o `subdomain` na caixa de texto Olá apresentados e prima '次へ (seguinte)' e o utilizador deve obter automaticamente com sessão iniciada tooyour **direta** aplicação.</span><span class="sxs-lookup"><span data-stu-id="da47f-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="da47f-218">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="da47f-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="da47f-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="da47f-219">Additional resources</span></span>

* [<span data-ttu-id="da47f-220">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da47f-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da47f-221">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="da47f-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

