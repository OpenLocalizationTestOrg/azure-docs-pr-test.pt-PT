---
title: "Tutorial: Integração do Azure Active Directory com estrelas CS | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o CS estrelas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5704d151-afb8-40a4-b286-8bacd4f279ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: d84533e8a7e9bca2f7bdf4be7f3050bca2f18496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cs-stars"></a><span data-ttu-id="54f85-103">Tutorial: Integração do Azure Active Directory com CS estrelas</span><span class="sxs-lookup"><span data-stu-id="54f85-103">Tutorial: Azure Active Directory integration with CS Stars</span></span>

<span data-ttu-id="54f85-104">Neste tutorial, saiba como toointegrate CS estrelas com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54f85-104">In this tutorial, you learn how toointegrate CS Stars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54f85-105">CS estrelas a integração com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="54f85-105">Integrating CS Stars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="54f85-106">Pode controlar no Azure AD que tenha acesso tooCS estrelas</span><span class="sxs-lookup"><span data-stu-id="54f85-106">You can control in Azure AD who has access tooCS Stars</span></span>
- <span data-ttu-id="54f85-107">Pode ativar a sua tooautomatically utilizadores obter estrelas tooCS com sessão iniciada (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="54f85-107">You can enable your users tooautomatically get signed-on tooCS Stars (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54f85-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="54f85-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="54f85-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54f85-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54f85-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="54f85-110">Prerequisites</span></span>

<span data-ttu-id="54f85-111">integração do Azure AD com CS estrelas tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="54f85-111">tooconfigure Azure AD integration with CS Stars, you need hello following items:</span></span>

- <span data-ttu-id="54f85-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="54f85-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54f85-113">Um estrelas CS-início de sessão único subscrição ativada</span><span class="sxs-lookup"><span data-stu-id="54f85-113">A CS Stars single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54f85-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="54f85-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54f85-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="54f85-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54f85-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="54f85-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54f85-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54f85-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54f85-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="54f85-118">Scenario description</span></span>
<span data-ttu-id="54f85-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="54f85-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54f85-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="54f85-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54f85-121">Adicionar CS estrelas na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="54f85-121">Adding CS Stars from hello gallery</span></span>
2. <span data-ttu-id="54f85-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="54f85-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cs-stars-from-hello-gallery"></a><span data-ttu-id="54f85-123">Adicionar CS estrelas na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="54f85-123">Adding CS Stars from hello gallery</span></span>
<span data-ttu-id="54f85-124">tooconfigure Olá integração de CS estrelas com o Azure AD, é necessário tooadd CS estrelas Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="54f85-124">tooconfigure hello integration of CS Stars into Azure AD, you need tooadd CS Stars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="54f85-125">**tooadd CS estrelas na Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="54f85-125">**tooadd CS Stars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="54f85-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="54f85-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="54f85-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="54f85-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="54f85-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="54f85-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="54f85-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54f85-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="54f85-133">Na caixa de pesquisa de Olá, escreva **CS estrelas**.</span><span class="sxs-lookup"><span data-stu-id="54f85-133">In hello search box, type **CS Stars**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_search.png)

5. <span data-ttu-id="54f85-135">No painel de resultados de Olá, selecione **CS estrelas**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="54f85-135">In hello results panel, select **CS Stars**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54f85-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="54f85-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54f85-138">Nesta secção, configure e teste do Azure AD-início de sessão único com estrelas CS com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="54f85-138">In this section, you configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="54f85-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá CS estrelas é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54f85-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CS Stars is tooa user in Azure AD.</span></span> <span data-ttu-id="54f85-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá CS estrelas tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="54f85-140">In other words, a link relationship between an Azure AD user and hello related user in CS Stars needs toobe established.</span></span>

<span data-ttu-id="54f85-141">CS estrelas, atribuir valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="54f85-141">In CS Stars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="54f85-142">tooconfigure e teste do Azure AD-início de sessão único com CS estrelas, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="54f85-142">tooconfigure and test Azure AD single sign-on with CS Stars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="54f85-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="54f85-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="54f85-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54f85-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54f85-145">**[Criar um utilizador de teste de CS estrelas](#creating-a-cs-stars-test-user)**  -toohave um homólogo de Britta Simon em estrelas de CS que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="54f85-145">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - toohave a counterpart of Britta Simon in CS Stars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="54f85-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="54f85-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54f85-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="54f85-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="54f85-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="54f85-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="54f85-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação CS estrelas.</span><span class="sxs-lookup"><span data-stu-id="54f85-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CS Stars application.</span></span>

<span data-ttu-id="54f85-150">**tooconfigure do Azure AD-início de sessão único com CS estrelas, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="54f85-150">**tooconfigure Azure AD single sign-on with CS Stars, perform hello following steps:**</span></span>

1. <span data-ttu-id="54f85-151">No Olá portal do Azure, no Olá **CS estrelas** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="54f85-151">In hello Azure portal, on hello **CS Stars** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="54f85-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="54f85-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_samlbase.png)

3. <span data-ttu-id="54f85-155">No Olá **CS estrelas domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="54f85-155">On hello **CS Stars Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_url.png)

    <span data-ttu-id="54f85-157">a.</span><span class="sxs-lookup"><span data-stu-id="54f85-157">a.</span></span> <span data-ttu-id="54f85-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="54f85-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span></span>

    <span data-ttu-id="54f85-159">b.</span><span class="sxs-lookup"><span data-stu-id="54f85-159">b.</span></span> <span data-ttu-id="54f85-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.csstars.com/enterprise/`</span><span class="sxs-lookup"><span data-stu-id="54f85-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.csstars.com/enterprise/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54f85-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="54f85-161">These values are not real.</span></span> <span data-ttu-id="54f85-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="54f85-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="54f85-163">Contacte [equipa de suporte de cliente de estrelas CS](http://www.marshclearsight.com/support/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="54f85-163">Contact [CS Stars Client support team](http://www.marshclearsight.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="54f85-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="54f85-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_certificate.png) 

5. <span data-ttu-id="54f85-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="54f85-166">Click **Save** button.</span></span>

    <span data-ttu-id="54f85-167">![Configurar o início de sessão único](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="54f85-167">![Configure Single Sign-On](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span></span>
6. <span data-ttu-id="54f85-168">tooconfigure-início de sessão único em **CS estrelas** lado, terá de Olá toosend transferido **XML de metadados** demasiado[CS estrelas suporta equipa](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="54f85-168">tooconfigure single sign-on on **CS Stars** side, you need toosend hello downloaded **Metadata XML** too[CS Stars support team](http://www.marshclearsight.com/support/).</span></span> 
<CE>

> [!TIP]
> <span data-ttu-id="54f85-169">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="54f85-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="54f85-170">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="54f85-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="54f85-171">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54f85-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54f85-172">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="54f85-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="54f85-173">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="54f85-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="54f85-175">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="54f85-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="54f85-176">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="54f85-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="54f85-178">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="54f85-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="54f85-180">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="54f85-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="54f85-182">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="54f85-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54f85-184">a.</span><span class="sxs-lookup"><span data-stu-id="54f85-184">a.</span></span> <span data-ttu-id="54f85-185">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54f85-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54f85-186">b.</span><span class="sxs-lookup"><span data-stu-id="54f85-186">b.</span></span> <span data-ttu-id="54f85-187">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="54f85-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54f85-188">c.</span><span class="sxs-lookup"><span data-stu-id="54f85-188">c.</span></span> <span data-ttu-id="54f85-189">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="54f85-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="54f85-190">d.</span><span class="sxs-lookup"><span data-stu-id="54f85-190">d.</span></span> <span data-ttu-id="54f85-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="54f85-191">Click **Create**.</span></span>
 
### <a name="creating-a-cs-stars-test-user"></a><span data-ttu-id="54f85-192">Criar um utilizador de teste de CS estrelas</span><span class="sxs-lookup"><span data-stu-id="54f85-192">Creating a CS Stars test user</span></span>

<span data-ttu-id="54f85-193">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon em estrelas de CS.</span><span class="sxs-lookup"><span data-stu-id="54f85-193">hello objective of this section is toocreate a user called Britta Simon in CS Stars.</span></span>

<span data-ttu-id="54f85-194">tooget um utilizador que criou no CS estrelas, terá de toocontact sua [CS estrelas suporta equipa](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="54f85-194">tooget a user created in CS Stars, you need toocontact your [CS Stars support team](http://www.marshclearsight.com/support/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="54f85-195">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="54f85-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="54f85-196">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooCS estrelas.</span><span class="sxs-lookup"><span data-stu-id="54f85-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCS Stars.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="54f85-198">**tooassign Britta Simon tooCS estrelas, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="54f85-198">**tooassign Britta Simon tooCS Stars, perform hello following steps:**</span></span>

1. <span data-ttu-id="54f85-199">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="54f85-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="54f85-201">Na lista de aplicações de Olá, selecione **CS estrelas**.</span><span class="sxs-lookup"><span data-stu-id="54f85-201">In hello applications list, select **CS Stars**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_app.png) 

3. <span data-ttu-id="54f85-203">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="54f85-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="54f85-205">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="54f85-205">Click **Add** button.</span></span> <span data-ttu-id="54f85-206">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54f85-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="54f85-208">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="54f85-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="54f85-209">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54f85-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54f85-210">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="54f85-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="54f85-211">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="54f85-211">Testing single sign-on</span></span>

<span data-ttu-id="54f85-212">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="54f85-212">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="54f85-213">Ao clicar Olá CS estrelas na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação CS estrelas.</span><span class="sxs-lookup"><span data-stu-id="54f85-213">When you click hello CS Stars tile in hello Access Panel, you should get automatically signed-on tooyour CS Stars application.</span></span>
 

## <a name="additional-resources"></a><span data-ttu-id="54f85-214">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="54f85-214">Additional resources</span></span>

* [<span data-ttu-id="54f85-215">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54f85-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54f85-216">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54f85-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_203.png

