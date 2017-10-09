---
title: "Tutorial: Integração do Azure Active Directory com Blackboard saiba - Shibboleth | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Blackboard saiba - Shibboleth."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 40aa3ec5f42b93157af3c56daaadfa66203b21d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="77e93-103">Tutorial: Integração do Azure Active Directory com Blackboard saiba - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="77e93-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="77e93-104">Neste tutorial, saiba como toointegrate Blackboard saiba - Shibboleth com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="77e93-104">In this tutorial, you learn how toointegrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77e93-105">Integrar Blackboard saiba - Shibboleth com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="77e93-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77e93-106">Pode controlar no Azure AD que tenha acesso tooBlackboard saiba - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="77e93-106">You can control in Azure AD who has access tooBlackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="77e93-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooBlackboard saiba - Shibboleth (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="77e93-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77e93-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="77e93-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77e93-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="77e93-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77e93-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="77e93-110">Prerequisites</span></span>

<span data-ttu-id="77e93-111">tooconfigure integração do Azure AD com Blackboard saiba - Shibboleth, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="77e93-111">tooconfigure Azure AD integration with Blackboard Learn - Shibboleth, you need hello following items:</span></span>

- <span data-ttu-id="77e93-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="77e93-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77e93-113">Obtenha um Blackboard - Shibboleth início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="77e93-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77e93-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="77e93-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77e93-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="77e93-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77e93-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="77e93-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77e93-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="77e93-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77e93-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="77e93-118">Scenario description</span></span>
<span data-ttu-id="77e93-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="77e93-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77e93-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="77e93-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77e93-121">Adicionar mais Blackboard - Shibboleth da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="77e93-121">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
2. <span data-ttu-id="77e93-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="77e93-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-hello-gallery"></a><span data-ttu-id="77e93-123">Adicionar mais Blackboard - Shibboleth da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="77e93-123">Adding Blackboard Learn - Shibboleth from hello gallery</span></span>
<span data-ttu-id="77e93-124">integração de Olá tooconfigure de Blackboard saiba - Shibboleth com o Azure AD, é necessário tooadd Blackboard saiba - Shibboleth Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="77e93-124">tooconfigure hello integration of Blackboard Learn - Shibboleth into Azure AD, you need tooadd Blackboard Learn - Shibboleth from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77e93-125">**tooadd Blackboard saiba - Shibboleth da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="77e93-125">**tooadd Blackboard Learn - Shibboleth from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e93-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="77e93-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77e93-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="77e93-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77e93-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="77e93-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="77e93-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77e93-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="77e93-133">Na caixa de pesquisa de Olá, escreva **Blackboard saiba - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="77e93-133">In hello search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="77e93-135">No painel de resultados de Olá, selecione **Blackboard saiba - Shibboleth**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="77e93-135">In hello results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77e93-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="77e93-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77e93-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Blackboard saiba - Shibboleth baseada num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="77e93-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="77e93-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador Olá homólogo Blackboard saiba - Shibboleth é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="77e93-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn - Shibboleth is tooa user in Azure AD.</span></span> <span data-ttu-id="77e93-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Blackboard saiba - Shibboleth tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="77e93-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn - Shibboleth needs toobe established.</span></span>

<span data-ttu-id="77e93-141">Saiba Blackboard - Shibboleth, atribuir valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="77e93-141">In Blackboard Learn - Shibboleth, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="77e93-142">tooconfigure e teste do Azure AD-início de sessão único com Blackboard saiba - Shibboleth, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="77e93-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77e93-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="77e93-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77e93-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="77e93-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77e93-145">**[Criar um Blackboard saiba - utilizador de teste de Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)**  - toohave um homólogo de Britta Simon no Blackboard saiba - Shibboleth é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="77e93-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77e93-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="77e93-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77e93-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="77e93-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77e93-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="77e93-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77e93-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua Blackboard saiba - aplicação Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="77e93-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="77e93-150">**tooconfigure do Azure AD-início de sessão único com Blackboard saiba - Shibboleth, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="77e93-150">**tooconfigure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e93-151">No Olá portal do Azure, no Olá **Blackboard saiba - Shibboleth** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="77e93-151">In hello Azure portal, on hello **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="77e93-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="77e93-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="77e93-155">No Olá **Blackboard saiba - domínio Shibboleth e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="77e93-155">On hello **Blackboard Learn - Shibboleth Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="77e93-157">a.</span><span class="sxs-lookup"><span data-stu-id="77e93-157">a.</span></span> <span data-ttu-id="77e93-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="77e93-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="77e93-159">b.</span><span class="sxs-lookup"><span data-stu-id="77e93-159">b.</span></span> <span data-ttu-id="77e93-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="77e93-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="77e93-161">c.</span><span class="sxs-lookup"><span data-stu-id="77e93-161">c.</span></span> <span data-ttu-id="77e93-162">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span><span class="sxs-lookup"><span data-stu-id="77e93-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="77e93-163">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="77e93-163">These values are not real.</span></span> <span data-ttu-id="77e93-164">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="77e93-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="77e93-165">Contacte [Blackboard saiba - a equipa de suporte de cliente Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="77e93-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="77e93-166">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="77e93-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="77e93-168">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="77e93-168">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="77e93-170">No Olá **Blackboard saiba - configuração Shibboleth** secção, clique em **configurar Blackboard saiba - Shibboleth** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="77e93-170">On hello **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="77e93-171">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="77e93-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="77e93-173">tooconfigure-início de sessão único em **Blackboard saiba - Shibboleth** lado, terá de Olá toosend transferido **XML de metadados** e **Sign-Out URL, ID de entidade de SAML e SAML único início de sessão no serviço URL** demasiado[Blackboard saiba - a equipa de suporte Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="77e93-173">tooconfigure single sign-on on **Blackboard Learn - Shibboleth** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="77e93-174">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="77e93-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77e93-175">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="77e93-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77e93-176">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77e93-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77e93-177">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="77e93-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="77e93-178">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="77e93-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="77e93-180">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="77e93-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e93-181">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="77e93-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77e93-183">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="77e93-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77e93-185">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="77e93-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77e93-187">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="77e93-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77e93-189">a.</span><span class="sxs-lookup"><span data-stu-id="77e93-189">a.</span></span> <span data-ttu-id="77e93-190">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="77e93-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77e93-191">b.</span><span class="sxs-lookup"><span data-stu-id="77e93-191">b.</span></span> <span data-ttu-id="77e93-192">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="77e93-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="77e93-193">c.</span><span class="sxs-lookup"><span data-stu-id="77e93-193">c.</span></span> <span data-ttu-id="77e93-194">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="77e93-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77e93-195">d.</span><span class="sxs-lookup"><span data-stu-id="77e93-195">d.</span></span> <span data-ttu-id="77e93-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="77e93-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="77e93-197">Criar um Blackboard saiba - utilizador de teste de Shibboleth</span><span class="sxs-lookup"><span data-stu-id="77e93-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="77e93-198">Nesta secção, vai criar um utilizador chamado Britta Simon Blackboard saiba - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="77e93-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="77e93-199">Trabalhar com o seu [Blackboard saiba - a equipa de suporte Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd utilizadores Olá Olá Blackboard saiba - plataforma Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="77e93-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) tooadd hello users in hello Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="77e93-200">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="77e93-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="77e93-201">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooBlackboard saiba - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="77e93-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn - Shibboleth.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="77e93-203">**tooassign Britta Simon tooBlackboard saiba - Shibboleth, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="77e93-203">**tooassign Britta Simon tooBlackboard Learn - Shibboleth, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e93-204">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="77e93-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="77e93-206">Na lista de aplicações de Olá, selecione **Blackboard saiba - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="77e93-206">In hello applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="77e93-208">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="77e93-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="77e93-210">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="77e93-210">Click **Add** button.</span></span> <span data-ttu-id="77e93-211">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77e93-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="77e93-213">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="77e93-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77e93-214">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77e93-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77e93-215">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="77e93-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77e93-216">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="77e93-216">Testing single sign-on</span></span>

<span data-ttu-id="77e93-217">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="77e93-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77e93-218">Ao clicar em Olá Blackboard saiba - mosaico Shibboleth no Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour Blackboard saiba - aplicação Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="77e93-218">When you click hello Blackboard Learn - Shibboleth tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77e93-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="77e93-219">Additional resources</span></span>

* [<span data-ttu-id="77e93-220">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77e93-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77e93-221">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="77e93-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

