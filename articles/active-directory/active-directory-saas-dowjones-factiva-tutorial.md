---
title: "Tutorial: Integração do Azure Active Directory com utenção Jones Factiva | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e utenção Jones Factiva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c42b5d64433c7bdcb512771a3e68115cc5f6874
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="7e1d8-103">Tutorial: Integração do Azure Active Directory com utenção Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="7e1d8-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="7e1d8-104">Neste tutorial, saiba como toointegrate utenção Jones Factiva com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e1d8-104">In this tutorial, you learn how toointegrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e1d8-105">Integrar utenção Jones Factiva com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="7e1d8-105">Integrating Dow Jones Factiva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e1d8-106">Pode controlar no Azure AD que tenha acesso tooDow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="7e1d8-106">You can control in Azure AD who has access tooDow Jones Factiva</span></span>
- <span data-ttu-id="7e1d8-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooDow Jones Factiva (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1d8-107">You can enable your users tooautomatically get signed-on tooDow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e1d8-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7e1d8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7e1d8-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e1d8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e1d8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7e1d8-110">Prerequisites</span></span>

<span data-ttu-id="7e1d8-111">integração do Azure AD com utenção Jones Factiva tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7e1d8-111">tooconfigure Azure AD integration with Dow Jones Factiva, you need hello following items:</span></span>

- <span data-ttu-id="7e1d8-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e1d8-113">Um utenção Jones Factiva início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="7e1d8-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e1d8-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e1d8-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7e1d8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e1d8-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e1d8-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e1d8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e1d8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7e1d8-118">Scenario description</span></span>
<span data-ttu-id="7e1d8-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e1d8-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="7e1d8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e1d8-121">Adicionar utenção Jones Factiva da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="7e1d8-121">Adding Dow Jones Factiva from hello gallery</span></span>
2. <span data-ttu-id="7e1d8-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="7e1d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-hello-gallery"></a><span data-ttu-id="7e1d8-123">Adicionar utenção Jones Factiva da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="7e1d8-123">Adding Dow Jones Factiva from hello gallery</span></span>
<span data-ttu-id="7e1d8-124">tooconfigure Olá integração de utenção Jones Factiva com o Azure AD, é necessário tooadd utenção Jones Factiva Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-124">tooconfigure hello integration of Dow Jones Factiva into Azure AD, you need tooadd Dow Jones Factiva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e1d8-125">**tooadd utenção Jones Factiva da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7e1d8-125">**tooadd Dow Jones Factiva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e1d8-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7e1d8-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e1d8-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="7e1d8-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="7e1d8-133">Na caixa de pesquisa de Olá, escreva **utenção Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-133">In hello search box, type **Dow Jones Factiva**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="7e1d8-135">No painel de resultados de Olá, selecione **utenção Jones Factiva**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-135">In hello results panel, select **Dow Jones Factiva**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e1d8-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="7e1d8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e1d8-138">Nesta secção, configure e teste do Azure AD-início de sessão único com utenção Jones Factiva com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7e1d8-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7e1d8-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá utenção Jones Factiva é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dow Jones Factiva is tooa user in Azure AD.</span></span> <span data-ttu-id="7e1d8-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá utenção Jones Factiva tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-140">In other words, a link relationship between an Azure AD user and hello related user in Dow Jones Factiva needs toobe established.</span></span>

<span data-ttu-id="7e1d8-141">No utenção Jones Factiva, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-141">In Dow Jones Factiva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7e1d8-142">tooconfigure e teste do Azure AD-início de sessão único com utenção Jones Factiva, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7e1d8-142">tooconfigure and test Azure AD single sign-on with Dow Jones Factiva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e1d8-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e1d8-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e1d8-145">**[Criar um utilizador de teste utenção Jones Factiva](#creating-a-dow-jones-factiva-test-user)**  -toohave um homólogo de Britta Simon no utenção Jones Factiva que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - toohave a counterpart of Britta Simon in Dow Jones Factiva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e1d8-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e1d8-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e1d8-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7e1d8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7e1d8-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação utenção Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="7e1d8-150">**tooconfigure do Azure AD-início de sessão único com utenção Jones Factiva, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7e1d8-150">**tooconfigure Azure AD single sign-on with Dow Jones Factiva, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e1d8-151">No Olá portal do Azure, no Olá **utenção Jones Factiva** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-151">In hello Azure portal, on hello **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="7e1d8-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="7e1d8-155">No Olá **utenção Jones Factiva domínio e os URLs** secção, hello utilizador não tem tooperform quaisquer passos conforme Olá aplicação já está pré-integrada com o Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-155">On hello **Dow Jones Factiva Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="7e1d8-157">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="7e1d8-159">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-159">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7e1d8-161">tooconfigure-início de sessão único em **utenção Jones Factiva** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de utenção Jones Factiva](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="7e1d8-161">tooconfigure single sign-on on **Dow Jones Factiva** side, you need toosend hello downloaded **Metadata XML** too[Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="7e1d8-162">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-162">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7e1d8-163">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="7e1d8-163">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e1d8-164">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-164">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e1d8-165">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e1d8-165">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e1d8-166">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1d8-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e1d8-167">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="7e1d8-169">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7e1d8-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e1d8-170">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e1d8-172">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e1d8-174">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e1d8-176">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7e1d8-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e1d8-178">a.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-178">a.</span></span> <span data-ttu-id="7e1d8-179">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e1d8-180">b.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-180">b.</span></span> <span data-ttu-id="7e1d8-181">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7e1d8-182">c.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-182">c.</span></span> <span data-ttu-id="7e1d8-183">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7e1d8-184">d.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-184">d.</span></span> <span data-ttu-id="7e1d8-185">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="7e1d8-186">Criar um utilizador de teste utenção Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="7e1d8-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="7e1d8-187">Nesta secção, vai criar um utilizador chamado Britta Simon utenção Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="7e1d8-188">. Trabalhar com utenção [equipa de suporte de Jones Factiva](https://www.dowjones.com/contact/) utilizadores de Olá tooadd na plataforma de utenção Jones Factiva Olá.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) tooadd hello users in hello Dow Jones Factiva platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7e1d8-189">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e1d8-189">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7e1d8-190">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooDow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-190">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDow Jones Factiva.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="7e1d8-192">**tooassign Britta Simon tooDow Jones Factiva, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7e1d8-192">**tooassign Britta Simon tooDow Jones Factiva, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e1d8-193">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-193">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="7e1d8-195">Na lista de aplicações de Olá, selecione **utenção Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-195">In hello applications list, select **Dow Jones Factiva**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="7e1d8-197">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-197">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="7e1d8-199">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-199">Click **Add** button.</span></span> <span data-ttu-id="7e1d8-200">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="7e1d8-202">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-202">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e1d8-203">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e1d8-204">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7e1d8-205">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7e1d8-205">Testing single sign-on</span></span>

<span data-ttu-id="7e1d8-206">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-206">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7e1d8-207">Ao clicar em mosaico de utenção Jones Factiva Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour utenção Jones Factiva aplicação.</span><span class="sxs-lookup"><span data-stu-id="7e1d8-207">When you click hello Dow Jones Factiva tile in hello Access Panel, you should get automatically signed-on tooyour Dow Jones Factiva application.</span></span>
<span data-ttu-id="7e1d8-208">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e1d8-208">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7e1d8-209">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7e1d8-209">Additional resources</span></span>

* [<span data-ttu-id="7e1d8-210">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e1d8-210">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e1d8-211">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e1d8-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

