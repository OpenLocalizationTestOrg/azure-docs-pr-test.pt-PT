---
title: "Tutorial: Integração do Azure Active Directory com DocuSign | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="e74a9-103">Tutorial: Integração do Azure Active Directory com DocuSign</span><span class="sxs-lookup"><span data-stu-id="e74a9-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="e74a9-104">Neste tutorial, saiba como toointegrate DocuSign com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e74a9-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e74a9-105">Integrar DocuSign com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="e74a9-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e74a9-106">Pode controlar no Azure AD que tenha acesso tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="e74a9-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="e74a9-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooDocuSign (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e74a9-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e74a9-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e74a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e74a9-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e74a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e74a9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e74a9-110">Prerequisites</span></span>

<span data-ttu-id="e74a9-111">integração do Azure AD com DocuSign tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="e74a9-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="e74a9-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e74a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e74a9-113">Um DocuSign-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="e74a9-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e74a9-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e74a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e74a9-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e74a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e74a9-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e74a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e74a9-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e74a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e74a9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e74a9-118">Scenario description</span></span>
<span data-ttu-id="e74a9-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e74a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e74a9-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="e74a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e74a9-121">Adicionar DocuSign da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="e74a9-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="e74a9-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="e74a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="e74a9-123">Adicionar DocuSign da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="e74a9-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="e74a9-124">tooconfigure Olá integração de DocuSign com o Azure AD, é necessário tooadd DocuSign Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="e74a9-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e74a9-125">**tooadd DocuSign da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="e74a9-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e74a9-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="e74a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e74a9-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e74a9-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="e74a9-131">Clique em **nova aplicação** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="e74a9-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="e74a9-133">Na caixa de pesquisa de Olá, escreva **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-133">In hello search box, type **DocuSign**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="e74a9-135">No painel de resultados de Olá, selecione **DocuSign**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="e74a9-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e74a9-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="e74a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e74a9-138">Nesta secção, configure e teste do Azure AD-início de sessão único com DocuSign com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e74a9-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e74a9-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá DocuSign é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e74a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="e74a9-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá DocuSign tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e74a9-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="e74a9-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no DocuSign.</span><span class="sxs-lookup"><span data-stu-id="e74a9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="e74a9-142">tooconfigure e teste do Azure AD-início de sessão único com DocuSign, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="e74a9-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e74a9-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="e74a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e74a9-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e74a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e74a9-145">**[Criar um utilizador de teste DocuSign](#creating-a-docusign-test-user)**  -toohave um homólogo de Britta Simon no DocuSign é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="e74a9-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e74a9-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="e74a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e74a9-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="e74a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e74a9-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="e74a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e74a9-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação DocuSign.</span><span class="sxs-lookup"><span data-stu-id="e74a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="e74a9-150">**tooconfigure do Azure AD-início de sessão único com DocuSign, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="e74a9-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e74a9-151">No Olá portal do Azure, no Olá **DocuSign** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="e74a9-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="e74a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="e74a9-155">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base 64)** e, em seguida, guarde o ficheiro de certificado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="e74a9-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="e74a9-157">No Olá **DocuSign configuração** secção do portal do Azure, clique em **configurar DocuSign** janela tooopen configurar início de sessão.</span><span class="sxs-lookup"><span data-stu-id="e74a9-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="e74a9-158">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="e74a9-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="e74a9-160">Numa janela do browser web diferente, início de sessão tooyour **portal de administração de DocuSign** como administrador.</span><span class="sxs-lookup"><span data-stu-id="e74a9-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="e74a9-161">No menu de navegação de Olá Olá esquerda, clique em **domínios**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Configurar o início de sessão único][51]

7. <span data-ttu-id="e74a9-163">No painel direito Olá, clique em **afirmação domínio**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Configurar o início de sessão único][52]

8. <span data-ttu-id="e74a9-165">No Olá **de afirmações de um domínio** caixa de diálogo, no Olá **nome de domínio** caixa de texto, escreva o domínio da sua empresa e, em seguida, clique em **afirmação**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="e74a9-166">Certifique-se que verifique o domínio de Olá e estado de Olá está ativo.</span><span class="sxs-lookup"><span data-stu-id="e74a9-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Configurar o início de sessão único][53]

9. <span data-ttu-id="e74a9-168">No menu no lado esquerdo Olá, clique em **fornecedores de identidade**</span><span class="sxs-lookup"><span data-stu-id="e74a9-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Configurar o início de sessão único][54]
10. <span data-ttu-id="e74a9-170">No painel direito Olá, clique em **Adicionar fornecedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configurar o início de sessão único][55]

11. <span data-ttu-id="e74a9-172">No Olá **as definições do fornecedor de identidade** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="e74a9-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Configurar o início de sessão único][56]

    <span data-ttu-id="e74a9-174">a.</span><span class="sxs-lookup"><span data-stu-id="e74a9-174">a.</span></span> <span data-ttu-id="e74a9-175">No Olá **nome** caixa de texto, escreva um nome exclusivo para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="e74a9-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="e74a9-176">Não utilize espaços.</span><span class="sxs-lookup"><span data-stu-id="e74a9-176">Do not use spaces.</span></span>

    <span data-ttu-id="e74a9-177">b.</span><span class="sxs-lookup"><span data-stu-id="e74a9-177">b.</span></span> <span data-ttu-id="e74a9-178">Colar **ID de entidade de SAML** para Olá **emissor do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e74a9-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="e74a9-179">c.</span><span class="sxs-lookup"><span data-stu-id="e74a9-179">c.</span></span> <span data-ttu-id="e74a9-180">Colar **único início de sessão no URL do serviço SAML** para Olá **URL de início de sessão do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e74a9-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="e74a9-181">d.</span><span class="sxs-lookup"><span data-stu-id="e74a9-181">d.</span></span> <span data-ttu-id="e74a9-182">Colar **Sign-Out URL** para Olá **URL de fim de sessão do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e74a9-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="e74a9-183">e.</span><span class="sxs-lookup"><span data-stu-id="e74a9-183">e.</span></span> <span data-ttu-id="e74a9-184">Selecione **assinar pedido AuthN**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="e74a9-185">f.</span><span class="sxs-lookup"><span data-stu-id="e74a9-185">f.</span></span> <span data-ttu-id="e74a9-186">Como **AuthN enviar pedido pelo**, selecione **POST**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="e74a9-187">g.</span><span class="sxs-lookup"><span data-stu-id="e74a9-187">g.</span></span> <span data-ttu-id="e74a9-188">Como **envio fim de sessão pedido pelo**, selecione **obter**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="e74a9-189">No Olá **mapeamento de atributos personalizado** secção, escolha o campo de Olá pretende toomap com afirmações do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e74a9-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="e74a9-190">Neste exemplo, Olá **emailaddress** afirmação está mapeada com o valor Olá **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="e74a9-191">Este é o nome de afirmação de predefinido de Olá do Azure AD para afirmações de e-mail.</span><span class="sxs-lookup"><span data-stu-id="e74a9-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="e74a9-192">Olá de utilização adequado **identificador de utilizador** utilizador de Olá toomap do mapeamento de utilizador de tooDocuSign do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e74a9-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="e74a9-193">Selecione Olá campo adequado e introduza o valor adequado Olá com base nas definições da sua organização.</span><span class="sxs-lookup"><span data-stu-id="e74a9-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Configurar o início de sessão único][57]

13. <span data-ttu-id="e74a9-195">No Olá **certificado do fornecedor de identidade** secção, clique em **adicionar certificado**e, em seguida, carregue o certificado de Olá transferiu a partir do portal do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e74a9-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configurar o início de sessão único][58]

14. <span data-ttu-id="e74a9-197">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-197">Click **Save**.</span></span>

15. <span data-ttu-id="e74a9-198">No Olá **fornecedores de identidade** secção, clique em **ações**e, em seguida, clique em **pontos finais**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configurar o início de sessão único][59]
 
16. <span data-ttu-id="e74a9-200">No Olá **ver SAML 2.0 pontos finais** secção no **portal de administração de DocuSign**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="e74a9-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Configurar o início de sessão único][60]
   
    <span data-ttu-id="e74a9-202">a.</span><span class="sxs-lookup"><span data-stu-id="e74a9-202">a.</span></span> <span data-ttu-id="e74a9-203">Olá cópia **URL do emissor de fornecedor de serviço**e, em seguida, cole Olá **identificador** caixa de texto no **DocuSign domínio e os URLs** secção Olá Olá seguinte de portal do Azure padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="e74a9-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="e74a9-204">b.</span><span class="sxs-lookup"><span data-stu-id="e74a9-204">b.</span></span> <span data-ttu-id="e74a9-205">Olá cópia **URL de início de sessão do fornecedor de serviço**e, em seguida, cole Olá **URL de início de sessão** caixa de texto no **DocuSign domínio e os URLs** secção Olá Olá seguinte de portal do Azure padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="e74a9-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="e74a9-207">c.</span><span class="sxs-lookup"><span data-stu-id="e74a9-207">c.</span></span>  <span data-ttu-id="e74a9-208">Clique em **fechar**</span><span class="sxs-lookup"><span data-stu-id="e74a9-208">Click **Close**</span></span>
    
17. <span data-ttu-id="e74a9-209">No portal do Azure Olá, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="e74a9-211">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="e74a9-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e74a9-212">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="e74a9-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e74a9-213">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e74a9-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e74a9-214">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e74a9-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="e74a9-215">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e74a9-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="e74a9-217">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="e74a9-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e74a9-218">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="e74a9-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e74a9-220">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e74a9-222">Na parte superior de Olá da caixa de diálogo Olá, clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e74a9-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e74a9-224">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="e74a9-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e74a9-226">a.</span><span class="sxs-lookup"><span data-stu-id="e74a9-226">a.</span></span> <span data-ttu-id="e74a9-227">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e74a9-228">b.</span><span class="sxs-lookup"><span data-stu-id="e74a9-228">b.</span></span> <span data-ttu-id="e74a9-229">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e74a9-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e74a9-230">c.</span><span class="sxs-lookup"><span data-stu-id="e74a9-230">c.</span></span> <span data-ttu-id="e74a9-231">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e74a9-232">d.</span><span class="sxs-lookup"><span data-stu-id="e74a9-232">d.</span></span> <span data-ttu-id="e74a9-233">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="e74a9-234">Criar um utilizador de teste DocuSign</span><span class="sxs-lookup"><span data-stu-id="e74a9-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="e74a9-235">Aplicação suporta **apenas no tempo de aprovisionamento de utilizador** e depois dos utilizadores de autenticação são criados na aplicação Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e74a9-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e74a9-236">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e74a9-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e74a9-237">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooDocuSign de acesso.</span><span class="sxs-lookup"><span data-stu-id="e74a9-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="e74a9-239">**tooassign Britta Simon tooDocuSign, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="e74a9-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e74a9-240">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="e74a9-242">Na lista de aplicações de Olá, selecione **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-242">In hello applications list, select **DocuSign**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="e74a9-244">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e74a9-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="e74a9-246">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="e74a9-246">Click **Add** button.</span></span> <span data-ttu-id="e74a9-247">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e74a9-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="e74a9-249">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="e74a9-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e74a9-250">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e74a9-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e74a9-251">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e74a9-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e74a9-252">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="e74a9-252">Testing single sign-on</span></span>

<span data-ttu-id="e74a9-253">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="e74a9-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e74a9-254">Ao clicar em mosaico de DocuSign Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour DocuSign aplicação.</span><span class="sxs-lookup"><span data-stu-id="e74a9-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="e74a9-255">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e74a9-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e74a9-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e74a9-256">Additional resources</span></span>

* [<span data-ttu-id="e74a9-257">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e74a9-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e74a9-258">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e74a9-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e74a9-259">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="e74a9-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

