---
title: "Tutorial: Integração do Azure Active Directory com itslearning | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e itslearning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 4ee6c8d450cc3972a87da67fc79890473cfa498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="5b4e3-103">Tutorial: Integração do Azure Active Directory com itslearning</span><span class="sxs-lookup"><span data-stu-id="5b4e3-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="5b4e3-104">Neste tutorial, saiba como toointegrate itslearning com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b4e3-104">In this tutorial, you learn how toointegrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b4e3-105">Integrar itslearning com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="5b4e3-105">Integrating itslearning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5b4e3-106">Pode controlar no Azure AD que tenha acesso tooitslearning</span><span class="sxs-lookup"><span data-stu-id="5b4e3-106">You can control in Azure AD who has access tooitslearning</span></span>
- <span data-ttu-id="5b4e3-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooitslearning (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b4e3-107">You can enable your users tooautomatically get signed-on tooitslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b4e3-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5b4e3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5b4e3-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b4e3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b4e3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5b4e3-110">Prerequisites</span></span>

<span data-ttu-id="5b4e3-111">integração do Azure AD com itslearning tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5b4e3-111">tooconfigure Azure AD integration with itslearning, you need hello following items:</span></span>

- <span data-ttu-id="5b4e3-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b4e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b4e3-113">Um itslearning-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="5b4e3-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b4e3-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b4e3-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5b4e3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b4e3-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b4e3-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b4e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b4e3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5b4e3-118">Scenario description</span></span>
<span data-ttu-id="5b4e3-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b4e3-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="5b4e3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b4e3-121">Adicionar itslearning da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="5b4e3-121">Adding itslearning from hello gallery</span></span>
2. <span data-ttu-id="5b4e3-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="5b4e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-hello-gallery"></a><span data-ttu-id="5b4e3-123">Adicionar itslearning da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="5b4e3-123">Adding itslearning from hello gallery</span></span>
<span data-ttu-id="5b4e3-124">tooconfigure Olá integração de itslearning com o Azure AD, é necessário tooadd itslearning Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-124">tooconfigure hello integration of itslearning into Azure AD, you need tooadd itslearning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5b4e3-125">**tooadd itslearning da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="5b4e3-125">**tooadd itslearning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b4e3-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b4e3-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5b4e3-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="5b4e3-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="5b4e3-133">Na caixa de pesquisa de Olá, escreva **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-133">In hello search box, type **itslearning**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="5b4e3-135">No painel de resultados de Olá, selecione **itslearning**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-135">In hello results panel, select **itslearning**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b4e3-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="5b4e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b4e3-138">Nesta secção, configure e teste do Azure AD-início de sessão único com itslearning com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b4e3-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b4e3-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá itslearning é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in itslearning is tooa user in Azure AD.</span></span> <span data-ttu-id="5b4e3-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá itslearning tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-140">In other words, a link relationship between an Azure AD user and hello related user in itslearning needs toobe established.</span></span>

<span data-ttu-id="5b4e3-141">No itslearning, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-141">In itslearning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5b4e3-142">tooconfigure e teste do Azure AD-início de sessão único com itslearning, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5b4e3-142">tooconfigure and test Azure AD single sign-on with itslearning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5b4e3-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5b4e3-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b4e3-145">**[Criar um utilizador de teste itslearning](#creating-an-itslearning-test-user)**  -toohave um homólogo de Britta Simon no itslearning é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - toohave a counterpart of Britta Simon in itslearning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b4e3-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b4e3-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b4e3-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="5b4e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b4e3-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação itslearning.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="5b4e3-150">**tooconfigure do Azure AD-início de sessão único com itslearning, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="5b4e3-150">**tooconfigure Azure AD single sign-on with itslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b4e3-151">No Olá portal do Azure, no Olá **itslearning** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-151">In hello Azure portal, on hello **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="5b4e3-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="5b4e3-155">No Olá **itslearning domínios e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5b4e3-155">On hello **itslearning Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="5b4e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-157">a.</span></span> <span data-ttu-id="5b4e3-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL como:</span><span class="sxs-lookup"><span data-stu-id="5b4e3-158">In hello **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="5b4e3-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-159">b.</span></span> <span data-ttu-id="5b4e3-160">No Olá **identificador** caixa de texto, escreva um URL como:`urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="5b4e3-160">In hello **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="5b4e3-161">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="5b4e3-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5b4e3-165">tooconfigure-início de sessão único em **itslearning** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de itslearning](mailto:support@itslearning.com).</span><span class="sxs-lookup"><span data-stu-id="5b4e3-165">tooconfigure single sign-on on **itslearning** side, you need toosend hello downloaded **Metadata XML** too[itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="5b4e3-166">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5b4e3-167">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="5b4e3-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5b4e3-168">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5b4e3-169">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b4e3-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b4e3-170">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b4e3-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b4e3-171">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="5b4e3-173">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="5b4e3-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b4e3-174">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b4e3-176">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b4e3-178">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b4e3-180">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5b4e3-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b4e3-182">a.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-182">a.</span></span> <span data-ttu-id="5b4e3-183">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b4e3-184">b.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-184">b.</span></span> <span data-ttu-id="5b4e3-185">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b4e3-186">c.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-186">c.</span></span> <span data-ttu-id="5b4e3-187">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5b4e3-188">d.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-188">d.</span></span> <span data-ttu-id="5b4e3-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="5b4e3-190">Criar um utilizador de teste itslearning</span><span class="sxs-lookup"><span data-stu-id="5b4e3-190">Creating an itslearning test user</span></span>

<span data-ttu-id="5b4e3-191">Nesta secção, vai criar um utilizador chamado Britta Simon itslearning.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="5b4e3-192">Trabalhar com [equipa de suporte de cliente itslearning](mailto:support@itslearning.com) para adicionar utilizadores de Olá na plataforma de itslearning Olá.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add hello users in hello itslearning platform.</span></span> <span data-ttu-id="5b4e3-193">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5b4e3-194">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b4e3-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5b4e3-195">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooitslearning.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooitslearning.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="5b4e3-197">**tooassign Britta Simon tooitslearning, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="5b4e3-197">**tooassign Britta Simon tooitslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5b4e3-198">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="5b4e3-200">Na lista de aplicações de Olá, selecione **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-200">In hello applications list, select **itslearning**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="5b4e3-202">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="5b4e3-204">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-204">Click **Add** button.</span></span> <span data-ttu-id="5b4e3-205">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="5b4e3-207">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5b4e3-208">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b4e3-209">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5b4e3-210">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="5b4e3-210">Testing single sign-on</span></span>

<span data-ttu-id="5b4e3-211">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5b4e3-212">Ao clicar Olá itslearning mosaico no painel de acesso de Olá, deve obter a página de início de sessão da aplicação itslearning.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-212">When you click hello itslearning tile in hello Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="5b4e3-213">Clique em **iniciar sessão com o Windows Azure ACS1** para início de sessão com êxito na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="5b4e3-213">Click **Log in with Windows Azure ACS1** for successful login into hello application.</span></span>

  ![Iniciar sessão](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="5b4e3-215">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5b4e3-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b4e3-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5b4e3-216">Additional resources</span></span>

* [<span data-ttu-id="5b4e3-217">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b4e3-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b4e3-218">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b4e3-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png

