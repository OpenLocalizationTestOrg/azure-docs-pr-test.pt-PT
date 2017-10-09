---
title: "Tutorial: Integração do Azure Active Directory com MobileXpense | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e MobileXpense."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: b9d109f9d4244f8a7eb8b49b0d980cd3df0fc59d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="dc4e3-103">Tutorial: Integração do Azure Active Directory com MobileXpense</span><span class="sxs-lookup"><span data-stu-id="dc4e3-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="dc4e3-104">Neste tutorial, saiba como toointegrate MobileXpense com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc4e3-104">In this tutorial, you learn how toointegrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc4e3-105">Integrar MobileXpense com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="dc4e3-105">Integrating MobileXpense with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dc4e3-106">Pode controlar no Azure AD que tenha acesso tooMobileXpense</span><span class="sxs-lookup"><span data-stu-id="dc4e3-106">You can control in Azure AD who has access tooMobileXpense</span></span>
- <span data-ttu-id="dc4e3-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooMobileXpense (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc4e3-107">You can enable your users tooautomatically get signed-on tooMobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc4e3-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dc4e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dc4e3-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc4e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc4e3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dc4e3-110">Prerequisites</span></span>

<span data-ttu-id="dc4e3-111">integração do Azure AD com MobileXpense tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="dc4e3-111">tooconfigure Azure AD integration with MobileXpense, you need hello following items:</span></span>

- <span data-ttu-id="dc4e3-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc4e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc4e3-113">Um MobileXpense início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="dc4e3-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc4e3-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc4e3-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="dc4e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc4e3-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc4e3-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc4e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc4e3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="dc4e3-118">Scenario description</span></span>
<span data-ttu-id="dc4e3-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc4e3-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="dc4e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc4e3-121">Adicionar MobileXpense da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="dc4e3-121">Adding MobileXpense from hello gallery</span></span>
2. <span data-ttu-id="dc4e3-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="dc4e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-hello-gallery"></a><span data-ttu-id="dc4e3-123">Adicionar MobileXpense da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="dc4e3-123">Adding MobileXpense from hello gallery</span></span>
<span data-ttu-id="dc4e3-124">tooconfigure Olá integração de MobileXpense com o Azure AD, é necessário tooadd MobileXpense Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-124">tooconfigure hello integration of MobileXpense into Azure AD, you need tooadd MobileXpense from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dc4e3-125">**tooadd MobileXpense da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="dc4e3-125">**tooadd MobileXpense from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc4e3-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc4e3-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dc4e3-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="dc4e3-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="dc4e3-133">Na caixa de pesquisa de Olá, escreva **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-133">In hello search box, type **MobileXpense**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="dc4e3-135">No painel de resultados de Olá, selecione **MobileXpense**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-135">In hello results panel, select **MobileXpense**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc4e3-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="dc4e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc4e3-138">Nesta secção, configure e teste do Azure AD-início de sessão único com MobileXpense com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="dc4e3-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dc4e3-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá MobileXpense é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MobileXpense is tooa user in Azure AD.</span></span> <span data-ttu-id="dc4e3-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá MobileXpense tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-140">In other words, a link relationship between an Azure AD user and hello related user in MobileXpense needs toobe established.</span></span>

<span data-ttu-id="dc4e3-141">No MobileXpense, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-141">In MobileXpense, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dc4e3-142">tooconfigure e teste do Azure AD-início de sessão único com MobileXpense, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="dc4e3-142">tooconfigure and test Azure AD single sign-on with MobileXpense, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dc4e3-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dc4e3-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc4e3-145">**[Criar um utilizador de teste MobileXpense](#creating-a-mobilexpense-test-user)**  -toohave um homólogo de Britta Simon no MobileXpense é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - toohave a counterpart of Britta Simon in MobileXpense that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc4e3-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc4e3-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc4e3-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="dc4e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc4e3-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="dc4e3-150">**tooconfigure do Azure AD-início de sessão único com MobileXpense, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="dc4e3-150">**tooconfigure Azure AD single sign-on with MobileXpense, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc4e3-151">No Olá portal do Azure, no Olá **MobileXpense** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-151">In hello Azure portal, on hello **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="dc4e3-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="dc4e3-155">No Olá **MobileXpense domínio e os URLs** secção, se desejar aplicação Olá tooconfigure **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="dc4e3-155">On hello **MobileXpense Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="dc4e3-157">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="dc4e3-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="dc4e3-158">Verifique **Mostrar avançadas definições de URL**, se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="dc4e3-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="dc4e3-160">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="dc4e3-160">In hello **Sign-on URL** textbox, type a URL using hello following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="dc4e3-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-161">These values are not real.</span></span> <span data-ttu-id="dc4e3-162">Atualize estes valores com o URL de resposta real Olá e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="dc4e3-163">Contacte [equipa de suporte de cliente MobileXpense](http://www.mobilexpense.net/contact) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) tooget these values.</span></span> 

5. <span data-ttu-id="dc4e3-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="dc4e3-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="dc4e3-168">tooconfigure-início de sessão único em **MobileXpense** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="dc4e3-168">tooconfigure single sign-on on **MobileXpense** side, you need toosend hello downloaded **Metadata XML** too[MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="dc4e3-169">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="dc4e3-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dc4e3-170">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dc4e3-171">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc4e3-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc4e3-172">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc4e3-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc4e3-173">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="dc4e3-175">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="dc4e3-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc4e3-176">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc4e3-178">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc4e3-180">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc4e3-182">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="dc4e3-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc4e3-184">a.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-184">a.</span></span> <span data-ttu-id="dc4e3-185">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc4e3-186">b.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-186">b.</span></span> <span data-ttu-id="dc4e3-187">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc4e3-188">c.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-188">c.</span></span> <span data-ttu-id="dc4e3-189">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dc4e3-190">d.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-190">d.</span></span> <span data-ttu-id="dc4e3-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="dc4e3-192">Criar um utilizador de teste MobileXpense</span><span class="sxs-lookup"><span data-stu-id="dc4e3-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="dc4e3-193">Nesta secção, vai criar um utilizador chamado Britta Simon MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="dc4e3-194">trabalhar com [equipa de suporte de MobileXpense](http://www.mobilexpense.net/contact) para adicionar utilizadores de Olá na plataforma de MobileXpense Olá.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add hello users in hello MobileXpense platform.</span></span> <span data-ttu-id="dc4e3-195">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dc4e3-196">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc4e3-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dc4e3-197">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooMobileXpense.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMobileXpense.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="dc4e3-199">**tooassign Britta Simon tooMobileXpense, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="dc4e3-199">**tooassign Britta Simon tooMobileXpense, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc4e3-200">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="dc4e3-202">Na lista de aplicações de Olá, selecione **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-202">In hello applications list, select **MobileXpense**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="dc4e3-204">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="dc4e3-206">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-206">Click **Add** button.</span></span> <span data-ttu-id="dc4e3-207">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="dc4e3-209">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dc4e3-210">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc4e3-211">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc4e3-212">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="dc4e3-212">Testing single sign-on</span></span>

<span data-ttu-id="dc4e3-213">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dc4e3-214">Ao clicar em mosaico de MobileXpense Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour MobileXpense aplicação.</span><span class="sxs-lookup"><span data-stu-id="dc4e3-214">When you click hello MobileXpense tile in hello Access Panel, you should get automatically signed-on tooyour MobileXpense application.</span></span>
<span data-ttu-id="dc4e3-215">Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="dc4e3-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dc4e3-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="dc4e3-216">Additional resources</span></span>

* [<span data-ttu-id="dc4e3-217">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc4e3-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc4e3-218">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc4e3-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

