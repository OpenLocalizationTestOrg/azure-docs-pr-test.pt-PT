---
title: "Tutorial: Integração do Azure Active Directory com EverBridge | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="f474d-103">Tutorial: Integração do Azure Active Directory com EverBridge</span><span class="sxs-lookup"><span data-stu-id="f474d-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="f474d-104">Neste tutorial, saiba como toointegrate EverBridge com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f474d-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f474d-105">Integrar EverBridge com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="f474d-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f474d-106">Pode controlar no Azure AD que tenha acesso tooEverBridge</span><span class="sxs-lookup"><span data-stu-id="f474d-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="f474d-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooEverBridge (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f474d-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f474d-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f474d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f474d-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f474d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f474d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f474d-110">Prerequisites</span></span>

<span data-ttu-id="f474d-111">integração do Azure AD com EverBridge tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f474d-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="f474d-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f474d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f474d-113">Um EverBridge início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="f474d-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f474d-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f474d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f474d-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f474d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f474d-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f474d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f474d-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f474d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f474d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f474d-118">Scenario description</span></span>
<span data-ttu-id="f474d-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f474d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f474d-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="f474d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f474d-121">Adicionar EverBridge da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f474d-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="f474d-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f474d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="f474d-123">Adicionar EverBridge da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f474d-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="f474d-124">tooconfigure Olá integração de EverBridge com o Azure AD, é necessário tooadd EverBridge Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="f474d-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f474d-125">**tooadd EverBridge da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f474d-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f474d-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f474d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f474d-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f474d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f474d-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f474d-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="f474d-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f474d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="f474d-133">Na caixa de pesquisa de Olá, escreva **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="f474d-133">In hello search box, type **EverBridge**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="f474d-135">No painel de resultados de Olá, selecione **EverBridge**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="f474d-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f474d-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f474d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f474d-138">Nesta secção, configure e teste do Azure AD-início de sessão único com EverBridge com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f474d-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f474d-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá EverBridge é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f474d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="f474d-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá EverBridge tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f474d-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="f474d-141">No EverBridge, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="f474d-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f474d-142">tooconfigure e teste do Azure AD-início de sessão único com EverBridge, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f474d-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f474d-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f474d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f474d-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f474d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f474d-145">**[Criar um utilizador de teste EverBridge](#creating-an-everbridge-test-user)**  -toohave um homólogo de Britta Simon no EverBridge é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="f474d-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f474d-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f474d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f474d-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="f474d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f474d-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f474d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f474d-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação EverBridge.</span><span class="sxs-lookup"><span data-stu-id="f474d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="f474d-150">**tooconfigure do Azure AD-início de sessão único com EverBridge, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f474d-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="f474d-151">No Olá portal do Azure, no Olá **EverBridge** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="f474d-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="f474d-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f474d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="f474d-155">No Olá **EverBridge domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f474d-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="f474d-157">a.</span><span class="sxs-lookup"><span data-stu-id="f474d-157">a.</span></span> <span data-ttu-id="f474d-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="f474d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="f474d-159">b.</span><span class="sxs-lookup"><span data-stu-id="f474d-159">b.</span></span> <span data-ttu-id="f474d-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="f474d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f474d-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="f474d-161">These values are not real.</span></span> <span data-ttu-id="f474d-162">Atualize estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="f474d-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="f474d-163">Contacte [equipa de suporte de EverBridge](mailto:support@everbridge.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="f474d-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="f474d-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="f474d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="f474d-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="f474d-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f474d-168">No Olá **EverBridge configuração** secção, clique em **configurar EverBridge** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="f474d-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f474d-169">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="f474d-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="f474d-171">tooget SSO configurado para a sua aplicação, terá de toosign no tooyour Everbridge inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="f474d-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="f474d-172">No menu de Olá na parte superior do Olá, clique em Olá **definições** separador e selecione **Single Sign-On** em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="f474d-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="f474d-174">a.</span><span class="sxs-lookup"><span data-stu-id="f474d-174">a.</span></span> <span data-ttu-id="f474d-175">No Olá **nome** caixa de texto, nome de Olá de tipo de identificador do fornecedor (por exemplo: nome da sua empresa).</span><span class="sxs-lookup"><span data-stu-id="f474d-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="f474d-176">b.</span><span class="sxs-lookup"><span data-stu-id="f474d-176">b.</span></span> <span data-ttu-id="f474d-177">No Olá **nome API** caixa de texto, nome do tipo Olá da API.</span><span class="sxs-lookup"><span data-stu-id="f474d-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="f474d-178">c.</span><span class="sxs-lookup"><span data-stu-id="f474d-178">c.</span></span> <span data-ttu-id="f474d-179">Clique em **Escolher ficheiro** botão tooupload Olá ficheiro de metadados do que transferiu a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f474d-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="f474d-180">d.</span><span class="sxs-lookup"><span data-stu-id="f474d-180">d.</span></span> <span data-ttu-id="f474d-181">Na localização de identidade de SAML Olá, selecione **é de identidade no elemento de NameIdentifier Olá do Olá instrução requerente**.</span><span class="sxs-lookup"><span data-stu-id="f474d-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="f474d-182">e.</span><span class="sxs-lookup"><span data-stu-id="f474d-182">e.</span></span> <span data-ttu-id="f474d-183">No Olá **URL de início de sessão do fornecedor de identidade** caixa de texto, colar Olá valor do URL de SSO de SAML do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f474d-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="f474d-185">f.</span><span class="sxs-lookup"><span data-stu-id="f474d-185">f.</span></span> <span data-ttu-id="f474d-186">No Olá fornecedor iniciada pedido vínculo de serviço, selecione **redirecionamento de HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f474d-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="f474d-187">g.</span><span class="sxs-lookup"><span data-stu-id="f474d-187">g.</span></span> <span data-ttu-id="f474d-188">Clique em **guardar**</span><span class="sxs-lookup"><span data-stu-id="f474d-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="f474d-189">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="f474d-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f474d-190">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="f474d-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f474d-191">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f474d-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f474d-192">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f474d-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="f474d-193">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f474d-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="f474d-195">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f474d-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f474d-196">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f474d-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f474d-198">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="f474d-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f474d-200">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="f474d-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f474d-202">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f474d-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f474d-204">a.</span><span class="sxs-lookup"><span data-stu-id="f474d-204">a.</span></span> <span data-ttu-id="f474d-205">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f474d-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f474d-206">b.</span><span class="sxs-lookup"><span data-stu-id="f474d-206">b.</span></span> <span data-ttu-id="f474d-207">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f474d-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f474d-208">c.</span><span class="sxs-lookup"><span data-stu-id="f474d-208">c.</span></span> <span data-ttu-id="f474d-209">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="f474d-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f474d-210">d.</span><span class="sxs-lookup"><span data-stu-id="f474d-210">d.</span></span> <span data-ttu-id="f474d-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f474d-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="f474d-212">Criar um utilizador de teste EverBridge</span><span class="sxs-lookup"><span data-stu-id="f474d-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="f474d-213">Nesta secção, vai criar um utilizador chamado Britta Simon Everbridge.</span><span class="sxs-lookup"><span data-stu-id="f474d-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="f474d-214">Trabalhar com [equipa de suporte de EverBridge](mailto:support@everbridge.com) utilizadores de Olá tooadd na plataforma de Everbridge Olá.</span><span class="sxs-lookup"><span data-stu-id="f474d-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f474d-215">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f474d-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f474d-216">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooEverBridge.</span><span class="sxs-lookup"><span data-stu-id="f474d-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="f474d-218">**tooassign Britta Simon tooEverBridge, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f474d-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="f474d-219">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f474d-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="f474d-221">Na lista de aplicações de Olá, selecione **EverBridge**.</span><span class="sxs-lookup"><span data-stu-id="f474d-221">In hello applications list, select **EverBridge**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="f474d-223">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f474d-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="f474d-225">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="f474d-225">Click **Add** button.</span></span> <span data-ttu-id="f474d-226">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f474d-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="f474d-228">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="f474d-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f474d-229">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f474d-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f474d-230">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f474d-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f474d-231">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f474d-231">Testing single sign-on</span></span>

<span data-ttu-id="f474d-232">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f474d-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f474d-233">Ao clicar em mosaico de Everbridge Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Everbridge aplicação.</span><span class="sxs-lookup"><span data-stu-id="f474d-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f474d-234">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f474d-234">Additional resources</span></span>

* [<span data-ttu-id="f474d-235">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f474d-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f474d-236">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f474d-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

