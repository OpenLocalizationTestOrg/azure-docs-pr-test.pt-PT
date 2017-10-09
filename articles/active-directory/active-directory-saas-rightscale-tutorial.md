---
title: "Tutorial: Integração do Azure Active Directory com Rightscale | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre Rightscale e o Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="39241-103">Tutorial: Integração do Azure Active Directory com Rightscale</span><span class="sxs-lookup"><span data-stu-id="39241-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="39241-104">Neste tutorial, saiba como toointegrate Rightscale com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39241-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39241-105">Integrar Rightscale com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="39241-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="39241-106">Pode controlar no Azure AD que tenha acesso tooRightscale</span><span class="sxs-lookup"><span data-stu-id="39241-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="39241-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooRightscale (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="39241-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39241-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="39241-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="39241-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39241-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39241-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="39241-110">Prerequisites</span></span>

<span data-ttu-id="39241-111">integração do Azure AD com Rightscale tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="39241-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="39241-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="39241-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39241-113">Um Rightscale-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="39241-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39241-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="39241-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39241-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="39241-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39241-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="39241-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39241-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39241-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39241-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="39241-118">Scenario description</span></span>
<span data-ttu-id="39241-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="39241-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39241-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="39241-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39241-121">Adicionar Rightscale da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="39241-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="39241-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="39241-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="39241-123">Adicionar Rightscale da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="39241-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="39241-124">tooconfigure Olá integração de Rightscale com o Azure AD, é necessário tooadd Rightscale Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="39241-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="39241-125">**tooadd Rightscale da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="39241-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="39241-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="39241-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39241-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="39241-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="39241-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="39241-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="39241-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39241-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="39241-133">Na caixa de pesquisa de Olá, escreva **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="39241-133">In hello search box, type **Rightscale**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="39241-135">No painel de resultados de Olá, selecione **Rightscale**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="39241-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39241-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="39241-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39241-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Rightscale com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="39241-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39241-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Rightscale é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39241-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="39241-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Rightscale tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="39241-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="39241-141">No Rightscale, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="39241-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="39241-142">tooconfigure e teste do Azure AD-início de sessão único com Rightscale, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="39241-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="39241-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="39241-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="39241-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39241-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39241-145">**[Criar um utilizador de teste Rightscale](#creating-a-rightscale-test-user)**  -toohave um homólogo de Britta Simon no Rightscale é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="39241-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="39241-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="39241-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39241-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="39241-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39241-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="39241-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39241-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Rightscale.</span><span class="sxs-lookup"><span data-stu-id="39241-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="39241-150">**tooconfigure do Azure AD-início de sessão único com Rightscale, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="39241-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="39241-151">No Olá portal do Azure, no Olá **Rightscale** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="39241-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="39241-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="39241-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="39241-155">No Olá **domínio Rightscale e URLs** secção, se desejar aplicação Olá tooconfigure **IDP iniciada modo** não dispõe de tooperform quaisquer passos conforme Olá aplicação já está pré-integrada com o Azure.</span><span class="sxs-lookup"><span data-stu-id="39241-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="39241-157">No Olá **domínio Rightscale e URLs** secção, se desejar aplicação Olá tooconfigure **SP iniciada modo**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="39241-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="39241-159">a.</span><span class="sxs-lookup"><span data-stu-id="39241-159">a.</span></span> <span data-ttu-id="39241-160">Clique em Olá **Mostrar avançadas definições de URL**.</span><span class="sxs-lookup"><span data-stu-id="39241-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="39241-161">b.</span><span class="sxs-lookup"><span data-stu-id="39241-161">b.</span></span> <span data-ttu-id="39241-162">No Olá **URL de início de sessão** caixa de texto, tipo Olá URL:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="39241-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="39241-163">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="39241-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="39241-165">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="39241-165">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="39241-167">No Olá **Rightscale configuração** secção, clique em **configurar Rightscale** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="39241-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="39241-168">Olá cópia **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="39241-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="39241-169">![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="39241-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="39241-170">tooget SSO configurado para a sua aplicação, terá de toosign no tooyour RightScale inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="39241-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="39241-171">a.</span><span class="sxs-lookup"><span data-stu-id="39241-171">a.</span></span> <span data-ttu-id="39241-172">No menu de Olá na parte superior do Olá, clique em Olá **definições** separador e selecione **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="39241-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="39241-174">b.</span><span class="sxs-lookup"><span data-stu-id="39241-174">b.</span></span> <span data-ttu-id="39241-175">Clique em Olá "**novo**" botão tooadd **fornecedores de identidade do seu SAML**.</span><span class="sxs-lookup"><span data-stu-id="39241-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="39241-177">c.</span><span class="sxs-lookup"><span data-stu-id="39241-177">c.</span></span> <span data-ttu-id="39241-178">Na caixa de texto Olá de **nome a apresentar**, introduza o nome da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="39241-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="39241-180">d.</span><span class="sxs-lookup"><span data-stu-id="39241-180">d.</span></span> <span data-ttu-id="39241-181">Selecione **SSO iniciado por permitir RightScale utilizando uma sugestão de deteção** e entrada sua **nome de domínio** no Olá abaixo caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="39241-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="39241-183">e.</span><span class="sxs-lookup"><span data-stu-id="39241-183">e.</span></span> <span data-ttu-id="39241-184">Colar o valor Olá **único início de sessão no URL do serviço SAML** que copiou do portal do Azure para **SAML SSO Endpoint** no RightScale.</span><span class="sxs-lookup"><span data-stu-id="39241-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="39241-186">f.</span><span class="sxs-lookup"><span data-stu-id="39241-186">f.</span></span> <span data-ttu-id="39241-187">Colar o valor Olá **ID de entidade de SAML** que copiou do portal do Azure para **SAML EntityID** no RightScale.</span><span class="sxs-lookup"><span data-stu-id="39241-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="39241-189">g.</span><span class="sxs-lookup"><span data-stu-id="39241-189">g.</span></span> <span data-ttu-id="39241-190">Clique em **Browser** botão tooupload Olá certificado que transferiu a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="39241-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="39241-192">h.</span><span class="sxs-lookup"><span data-stu-id="39241-192">h.</span></span> <span data-ttu-id="39241-193">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="39241-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="39241-194">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="39241-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="39241-195">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="39241-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="39241-196">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39241-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39241-197">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="39241-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="39241-198">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="39241-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="39241-200">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="39241-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="39241-201">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="39241-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39241-203">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="39241-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39241-205">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="39241-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39241-207">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="39241-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39241-209">a.</span><span class="sxs-lookup"><span data-stu-id="39241-209">a.</span></span> <span data-ttu-id="39241-210">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39241-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39241-211">b.</span><span class="sxs-lookup"><span data-stu-id="39241-211">b.</span></span> <span data-ttu-id="39241-212">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39241-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39241-213">c.</span><span class="sxs-lookup"><span data-stu-id="39241-213">c.</span></span> <span data-ttu-id="39241-214">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="39241-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="39241-215">d.</span><span class="sxs-lookup"><span data-stu-id="39241-215">d.</span></span> <span data-ttu-id="39241-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="39241-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="39241-217">Criar um utilizador de teste Rightscale</span><span class="sxs-lookup"><span data-stu-id="39241-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="39241-218">Nesta secção, vai criar um utilizador chamado Britta Simon RightScale.</span><span class="sxs-lookup"><span data-stu-id="39241-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="39241-219">Trabalhar com [equipa de suporte de cliente Rightscale](mailto:support@rightscale.com) utilizadores de Olá tooadd na plataforma de RightScale Olá.</span><span class="sxs-lookup"><span data-stu-id="39241-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="39241-220">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="39241-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="39241-221">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooRightscale.</span><span class="sxs-lookup"><span data-stu-id="39241-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="39241-223">**tooassign Britta Simon tooRightscale, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="39241-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="39241-224">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="39241-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="39241-226">Na lista de aplicações de Olá, selecione **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="39241-226">In hello applications list, select **Rightscale**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="39241-228">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="39241-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="39241-230">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="39241-230">Click **Add** button.</span></span> <span data-ttu-id="39241-231">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39241-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="39241-233">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="39241-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="39241-234">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39241-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39241-235">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="39241-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39241-236">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="39241-236">Testing single sign-on</span></span>

<span data-ttu-id="39241-237">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="39241-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="39241-238">Ao clicar em mosaico de RightScale Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour RightScale aplicação.</span><span class="sxs-lookup"><span data-stu-id="39241-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39241-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="39241-239">Additional resources</span></span>

* [<span data-ttu-id="39241-240">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39241-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39241-241">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39241-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

