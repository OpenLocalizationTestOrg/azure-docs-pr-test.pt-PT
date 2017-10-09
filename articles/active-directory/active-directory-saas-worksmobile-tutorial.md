---
title: "Tutorial: Integração do Azure Active Directory com FUNCIONA MOBILE | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e FUNCIONA MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="b8690-103">Tutorial: Integração do Azure Active Directory com FUNCIONA MOBILE</span><span class="sxs-lookup"><span data-stu-id="b8690-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="b8690-104">Neste tutorial, saiba como FUNCIONA o toointegrate MOBILE com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8690-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8690-105">Integrar o MOBILE FUNCIONA com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="b8690-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b8690-106">Pode controlar no Azure AD que tenha acesso tooWORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="b8690-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="b8690-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooWORKS MOBILE (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8690-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8690-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b8690-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b8690-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8690-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8690-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b8690-110">Prerequisites</span></span>

<span data-ttu-id="b8690-111">integração do Azure AD com FUNCIONA MOBILE tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b8690-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="b8690-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8690-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8690-113">Um FUNCIONA MOBILE-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="b8690-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8690-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b8690-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8690-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b8690-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8690-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b8690-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8690-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8690-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8690-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b8690-118">Scenario description</span></span>
<span data-ttu-id="b8690-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b8690-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8690-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="b8690-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8690-121">Adicionar MOBILE FUNCIONA na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="b8690-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="b8690-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="b8690-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="b8690-123">Adicionar MOBILE FUNCIONA na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="b8690-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="b8690-124">tooconfigure Olá integração do MOBILE FUNCIONA com o Azure AD, é necessário tooadd FUNCIONA MOBILE Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="b8690-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b8690-125">**tooadd MOBILE FUNCIONA a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b8690-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b8690-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="b8690-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8690-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b8690-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b8690-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="b8690-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="b8690-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8690-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="b8690-133">Na caixa de pesquisa de Olá, escreva **FUNCIONA MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="b8690-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="b8690-135">No painel de resultados de Olá, selecione **FUNCIONA MOBILE**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="b8690-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8690-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="b8690-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b8690-138">Nesta secção, configure e teste do Azure AD-início de sessão único com MOBILE FUNCIONA com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="b8690-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b8690-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá FUNCIONA MOBILE é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8690-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="b8690-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá FUNCIONA MOBILE tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b8690-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="b8690-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no FUNCIONA MOBILE.</span><span class="sxs-lookup"><span data-stu-id="b8690-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="b8690-142">tooconfigure e teste do Azure AD-início de sessão único com FUNCIONA móveis, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="b8690-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b8690-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="b8690-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b8690-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8690-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8690-145">**[Criar um utilizador de teste FUNCIONA MOBILE](#creating-a-works-mobile-test-user)**  -toohave um homólogo de Britta Simon no MOBILE WORKS que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="b8690-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b8690-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="b8690-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8690-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="b8690-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8690-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="b8690-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8690-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação móvel FUNCIONA.</span><span class="sxs-lookup"><span data-stu-id="b8690-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="b8690-150">**tooconfigure do Azure AD-início de sessão único com MOBILE FUNCIONA, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b8690-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="b8690-151">No Olá portal do Azure, no Olá **FUNCIONA MOBILE** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="b8690-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="b8690-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="b8690-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="b8690-155">No Olá **FUNCIONA MOBILE domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="b8690-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="b8690-157">a.</span><span class="sxs-lookup"><span data-stu-id="b8690-157">a.</span></span> <span data-ttu-id="b8690-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="b8690-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="b8690-159">b.</span><span class="sxs-lookup"><span data-stu-id="b8690-159">b.</span></span> <span data-ttu-id="b8690-160">No Olá **identificador** caixa de texto, valor de tipo de Olá como`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="b8690-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b8690-161">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="b8690-161">This value is not real.</span></span> <span data-ttu-id="b8690-162">Atualizar este valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="b8690-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b8690-163">Contacte [equipa de suporte de cliente de MOBILE FUNCIONA](mailto:dl_ssoinfo@worksmobile.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="b8690-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="b8690-164">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Raw)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="b8690-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="b8690-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="b8690-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b8690-168">No Olá **FUNCIONA MOBILE configuração** secção, clique em **configurar MOBILE de FUNCIONA** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="b8690-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b8690-169">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b8690-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="b8690-171">tooget SSO configuradas para a sua aplicação, contacte [equipa de suporte de FUNCIONA MOBILE](mailto:dl_ssoinfo@worksmobile.com) e fornecem Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="b8690-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="b8690-172">Olá • transferido **ficheiro de certificado**</span><span class="sxs-lookup"><span data-stu-id="b8690-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="b8690-173">• Olá **único início de sessão no URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="b8690-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="b8690-174">• Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="b8690-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="b8690-175">• Olá **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="b8690-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="b8690-176">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="b8690-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b8690-177">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="b8690-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b8690-178">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b8690-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8690-179">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8690-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8690-180">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8690-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="b8690-182">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b8690-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b8690-183">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="b8690-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8690-185">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="b8690-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8690-187">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="b8690-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8690-189">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="b8690-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8690-191">a.</span><span class="sxs-lookup"><span data-stu-id="b8690-191">a.</span></span> <span data-ttu-id="b8690-192">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8690-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8690-193">b.</span><span class="sxs-lookup"><span data-stu-id="b8690-193">b.</span></span> <span data-ttu-id="b8690-194">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b8690-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8690-195">c.</span><span class="sxs-lookup"><span data-stu-id="b8690-195">c.</span></span> <span data-ttu-id="b8690-196">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="b8690-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b8690-197">d.</span><span class="sxs-lookup"><span data-stu-id="b8690-197">d.</span></span> <span data-ttu-id="b8690-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b8690-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="b8690-199">Criar um utilizador de teste FUNCIONA MOBILE</span><span class="sxs-lookup"><span data-stu-id="b8690-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="b8690-200">Nesta secção, vai criar um utilizador chamado Britta Simon FUNCIONA MOBILE.</span><span class="sxs-lookup"><span data-stu-id="b8690-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="b8690-201">Consulte [equipa de suporte de FUNCIONA MOBILE](mailto:dl_ssoinfo@worksmobile.com) utilizadores de Olá tooadd na plataforma de FUNCIONA MOBILE Olá.</span><span class="sxs-lookup"><span data-stu-id="b8690-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b8690-202">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8690-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b8690-203">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooWORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="b8690-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="b8690-205">**tooassign Britta Simon tooWORKS MOBILE, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b8690-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="b8690-206">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="b8690-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="b8690-208">Na lista de aplicações de Olá, selecione **FUNCIONA MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="b8690-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="b8690-210">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b8690-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="b8690-212">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="b8690-212">Click **Add** button.</span></span> <span data-ttu-id="b8690-213">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8690-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="b8690-215">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="b8690-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b8690-216">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8690-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8690-217">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b8690-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8690-218">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="b8690-218">Testing single sign-on</span></span>

<span data-ttu-id="b8690-219">Nesta secção, testar a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="b8690-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="b8690-220">Ao clicar em mosaico de FUNCIONA MOBILE Olá no painel de acesso de Olá, deve obter a aplicação de MOBILE FUNCIONA automaticamente com sessão iniciada tooyour.</span><span class="sxs-lookup"><span data-stu-id="b8690-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="b8690-221">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b8690-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b8690-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b8690-222">Additional resources</span></span>

* [<span data-ttu-id="b8690-223">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8690-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8690-224">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8690-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

