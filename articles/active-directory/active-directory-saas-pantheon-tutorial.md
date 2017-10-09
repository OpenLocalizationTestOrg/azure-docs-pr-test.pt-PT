---
title: "Tutorial: Integração do Azure Active Directory com Pantheon | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a><span data-ttu-id="6f6ac-103">Tutorial: Integração do Azure Active Directory com Pantheon</span><span class="sxs-lookup"><span data-stu-id="6f6ac-103">Tutorial: Azure Active Directory integration with Pantheon</span></span>

<span data-ttu-id="6f6ac-104">Neste tutorial, saiba como toointegrate Pantheon com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f6ac-104">In this tutorial, you learn how toointegrate Pantheon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f6ac-105">Integrar Pantheon com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="6f6ac-105">Integrating Pantheon with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6f6ac-106">Pode controlar no Azure AD que tenha acesso tooPantheon</span><span class="sxs-lookup"><span data-stu-id="6f6ac-106">You can control in Azure AD who has access tooPantheon</span></span>
- <span data-ttu-id="6f6ac-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPantheon (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f6ac-107">You can enable your users tooautomatically get signed-on tooPantheon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6f6ac-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6f6ac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6f6ac-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f6ac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f6ac-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6f6ac-110">Prerequisites</span></span>

<span data-ttu-id="6f6ac-111">integração do Azure AD com Pantheon tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6f6ac-111">tooconfigure Azure AD integration with Pantheon, you need hello following items:</span></span>

- <span data-ttu-id="6f6ac-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f6ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6f6ac-113">Um Pantheon-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="6f6ac-113">A Pantheon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6f6ac-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6f6ac-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6f6ac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6f6ac-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6f6ac-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f6ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f6ac-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6f6ac-118">Scenario description</span></span>
<span data-ttu-id="6f6ac-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6f6ac-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="6f6ac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f6ac-121">Adicionar Pantheon da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6f6ac-121">Adding Pantheon from hello gallery</span></span>
2. <span data-ttu-id="6f6ac-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6f6ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pantheon-from-hello-gallery"></a><span data-ttu-id="6f6ac-123">Adicionar Pantheon da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6f6ac-123">Adding Pantheon from hello gallery</span></span>
<span data-ttu-id="6f6ac-124">tooconfigure Olá integração de Pantheon com o Azure AD, é necessário tooadd Pantheon Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-124">tooconfigure hello integration of Pantheon into Azure AD, you need tooadd Pantheon from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6f6ac-125">**tooadd Pantheon da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6f6ac-125">**tooadd Pantheon from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f6ac-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6f6ac-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6f6ac-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="6f6ac-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="6f6ac-133">Na caixa de pesquisa de Olá, escreva **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-133">In hello search box, type **Pantheon**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. <span data-ttu-id="6f6ac-135">No painel de resultados de Olá, selecione **Pantheon**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-135">In hello results panel, select **Pantheon**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6f6ac-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6f6ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6f6ac-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Pantheon com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6f6ac-138">In this section, you configure and test Azure AD single sign-on with Pantheon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f6ac-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Pantheon é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pantheon is tooa user in Azure AD.</span></span> <span data-ttu-id="6f6ac-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Pantheon tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-140">In other words, a link relationship between an Azure AD user and hello related user in Pantheon needs toobe established.</span></span>

<span data-ttu-id="6f6ac-141">No Pantheon, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-141">In Pantheon, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6f6ac-142">tooconfigure e teste do Azure AD-início de sessão único com Pantheon, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6f6ac-142">tooconfigure and test Azure AD single sign-on with Pantheon, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6f6ac-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6f6ac-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f6ac-145">**[Criar um utilizador de teste Pantheon](#creating-a-pantheon-test-user)**  -toohave um homólogo de Britta Simon no Pantheon é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-145">**[Creating a Pantheon test user](#creating-a-pantheon-test-user)** - toohave a counterpart of Britta Simon in Pantheon that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6f6ac-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f6ac-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6f6ac-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6f6ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6f6ac-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Pantheon.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pantheon application.</span></span>

<span data-ttu-id="6f6ac-150">**tooconfigure do Azure AD-início de sessão único com Pantheon, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6f6ac-150">**tooconfigure Azure AD single sign-on with Pantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f6ac-151">No Olá portal do Azure, no Olá **Pantheon** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-151">In hello Azure portal, on hello **Pantheon** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="6f6ac-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. <span data-ttu-id="6f6ac-155">No Olá **Pantheon domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6f6ac-155">On hello **Pantheon Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    <span data-ttu-id="6f6ac-157">a.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-157">a.</span></span> <span data-ttu-id="6f6ac-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`urn:auth0:pantheon:<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="6f6ac-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:auth0:pantheon:<orgname>-SSO`</span></span>

    <span data-ttu-id="6f6ac-159">b.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-159">b.</span></span> <span data-ttu-id="6f6ac-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span><span class="sxs-lookup"><span data-stu-id="6f6ac-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6f6ac-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-161">These values are not real.</span></span> <span data-ttu-id="6f6ac-162">Atualize estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6f6ac-163">Contacte [equipa de suporte de Pantheon](https://pantheon.io/docs/getting-support/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-163">Contact [Pantheon support team](https://pantheon.io/docs/getting-support/) tooget these values.</span></span>

4. <span data-ttu-id="6f6ac-164">Aplicação de pantheon espera de asserção SAML Olá no formato específico, o que requer tooset Olá UserIdentifier o valor do atributo com o endereço de correio eletrónico do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-164">Pantheon application expects hello SAML assertion in specific format, which requires you tooset hello UserIdentifier attribute value with hello user’s email address.</span></span> <span data-ttu-id="6f6ac-165">Por predefinição do Azure AD utiliza Olá UserPrincipalName UserIdentifier atributo.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-165">By default Azure AD uses hello UserPrincipalName for UserIdentifier attribute.</span></span> <span data-ttu-id="6f6ac-166">Mas para integração com êxito terá tooadjust toomatch este valor com o endereço de correio eletrónico do utilizador.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-166">But for successful integration you need tooadjust this value toomatch with user’s email address.</span></span> <span data-ttu-id="6f6ac-167">integração de Olá funcionará apenas depois de efetuar o mapeamento correto da Olá.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-167">hello integration will only work after doing hello correct mapping.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. <span data-ttu-id="6f6ac-169">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. <span data-ttu-id="6f6ac-171">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-171">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6f6ac-173">No Olá **Pantheon configuração** secção, clique em **configurar Pantheon** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-173">On hello **Pantheon Configuration** section, click **Configure Pantheon** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6f6ac-174">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="6f6ac-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. <span data-ttu-id="6f6ac-176">tooconfigure-início de sessão único em **Pantheon** lado, terá de Olá toosend transferido **certificado** e **único início de sessão no URL do serviço SAML** demasiado[Pantheon equipa de suporte](https://pantheon.io/docs/getting-support/).</span><span class="sxs-lookup"><span data-stu-id="6f6ac-176">tooconfigure single sign-on on **Pantheon** side, you need toosend hello downloaded **Certificate** and **SAML Single Sign-On Service URL** too[Pantheon support team](https://pantheon.io/docs/getting-support/).</span></span>

     > [!Note]
     > <span data-ttu-id="6f6ac-177">Também precisa de informações de domínios de E-Mail de Olá tooprovide e data hora quando quiser tooenable esta ligação.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-177">You also need tooprovide hello Email Domain(s) information and Date Time when you want tooenable this connection.</span></span> <span data-ttu-id="6f6ac-178">Pode encontrar mais detalhes sobre a [aqui](https://pantheon.io/docs/sso-organizations/)</span><span class="sxs-lookup"><span data-stu-id="6f6ac-178">You can find more details about it from [here](https://pantheon.io/docs/sso-organizations/)</span></span>

> [!TIP]
> <span data-ttu-id="6f6ac-179">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="6f6ac-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6f6ac-180">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6f6ac-181">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6f6ac-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6f6ac-182">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f6ac-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="6f6ac-183">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="6f6ac-185">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6f6ac-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f6ac-186">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6f6ac-188">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6f6ac-190">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6f6ac-192">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6f6ac-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6f6ac-194">a.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-194">a.</span></span> <span data-ttu-id="6f6ac-195">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6f6ac-196">b.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-196">b.</span></span> <span data-ttu-id="6f6ac-197">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6f6ac-198">c.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-198">c.</span></span> <span data-ttu-id="6f6ac-199">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6f6ac-200">d.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-200">d.</span></span> <span data-ttu-id="6f6ac-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-201">Click **Create**.</span></span>
 
### <a name="creating-a-pantheon-test-user"></a><span data-ttu-id="6f6ac-202">Criar um utilizador de teste Pantheon</span><span class="sxs-lookup"><span data-stu-id="6f6ac-202">Creating a Pantheon test user</span></span>

<span data-ttu-id="6f6ac-203">Nesta secção, vai criar um utilizador chamado Britta Simon Pantheon.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-203">In this section, you create a user called Britta Simon in Pantheon.</span></span> <span data-ttu-id="6f6ac-204">Siga Olá abaixo utilizador de Olá tooadd passos no Pantheon.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-204">Please follow hello below steps tooadd hello user in Pantheon.</span></span> 

>[!NOTE] 
><span data-ttu-id="6f6ac-205">Para SSO toowork utilizador precisa de toobe criado primeiro no Pantheon.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-205">For SSO toowork user needs toobe created first in Pantheon.</span></span>

1. <span data-ttu-id="6f6ac-206">TooPantheon de início de sessão com credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-206">Login tooPantheon with admin credentials.</span></span>

2. <span data-ttu-id="6f6ac-207">Navegue demasiado**organização** página do dashboard.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-207">Navigate too**Organization** dashboard page.</span></span>
 
3. <span data-ttu-id="6f6ac-208">Clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-208">Click **People**.</span></span>

4. <span data-ttu-id="6f6ac-209">Clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-209">Click **Add user**.</span></span>

5. <span data-ttu-id="6f6ac-210">Introduza o endereço de correio eletrónico do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-210">Enter hello user's email address.</span></span>

6. <span data-ttu-id="6f6ac-211">Escolha a função do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-211">Choose hello user's role.</span></span>

7. <span data-ttu-id="6f6ac-212">Clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-212">Click **Add user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6f6ac-213">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f6ac-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6f6ac-214">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPantheon.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPantheon.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="6f6ac-216">**tooassign Britta Simon tooPantheon, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6f6ac-216">**tooassign Britta Simon tooPantheon, perform hello following steps:**</span></span>

1. <span data-ttu-id="6f6ac-217">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="6f6ac-219">Na lista de aplicações de Olá, selecione **Pantheon**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-219">In hello applications list, select **Pantheon**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. <span data-ttu-id="6f6ac-221">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="6f6ac-223">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-223">Click **Add** button.</span></span> <span data-ttu-id="6f6ac-224">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="6f6ac-226">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6f6ac-227">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6f6ac-228">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6f6ac-229">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6f6ac-229">Testing single sign-on</span></span>

<span data-ttu-id="6f6ac-230">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6f6ac-231">Ao clicar em mosaico de Pantheon Olá no painel de acesso de Olá, deve obter a aplicação de Pantheon tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="6f6ac-231">When you click hello Pantheon tile in hello Access Panel, you should get automatically signed-on tooyour Pantheon application.</span></span>
<span data-ttu-id="6f6ac-232">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f6ac-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6f6ac-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6f6ac-233">Additional resources</span></span>

* [<span data-ttu-id="6f6ac-234">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f6ac-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f6ac-235">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6f6ac-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

