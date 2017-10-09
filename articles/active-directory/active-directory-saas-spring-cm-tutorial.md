---
title: "Tutorial: Integração do Azure Active Directory com SpringCM | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="cb443-103">Tutorial: Integração do Azure Active Directory com SpringCM</span><span class="sxs-lookup"><span data-stu-id="cb443-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="cb443-104">Neste tutorial, saiba como toointegrate SpringCM com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb443-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb443-105">Integrar SpringCM com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="cb443-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb443-106">Pode controlar no Azure AD que tenha acesso tooSpringCM</span><span class="sxs-lookup"><span data-stu-id="cb443-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="cb443-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSpringCM (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb443-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb443-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cb443-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb443-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb443-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb443-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb443-110">Prerequisites</span></span>

<span data-ttu-id="cb443-111">integração do Azure AD com SpringCM tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cb443-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="cb443-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb443-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb443-113">Um SpringCM-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="cb443-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb443-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cb443-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb443-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cb443-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb443-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cb443-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb443-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb443-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb443-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cb443-118">Scenario description</span></span>
<span data-ttu-id="cb443-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cb443-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb443-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="cb443-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb443-121">Adicionar SpringCM da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="cb443-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="cb443-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="cb443-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="cb443-123">Adicionar SpringCM da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="cb443-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="cb443-124">tooconfigure Olá integração de SpringCM com o Azure AD, é necessário tooadd SpringCM Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="cb443-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb443-125">**tooadd SpringCM da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cb443-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb443-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="cb443-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cb443-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cb443-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb443-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="cb443-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="cb443-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb443-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="cb443-133">Na caixa de pesquisa de Olá, escreva **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="cb443-133">In hello search box, type **SpringCM**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="cb443-135">No painel de resultados de Olá, selecione **SpringCM**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="cb443-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb443-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="cb443-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb443-138">Nesta secção, configure e teste do Azure AD-início de sessão único com SpringCM com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="cb443-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb443-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá SpringCM é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb443-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="cb443-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá SpringCM tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cb443-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="cb443-141">No SpringCM, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="cb443-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cb443-142">tooconfigure e teste do Azure AD-início de sessão único com SpringCM, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cb443-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb443-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="cb443-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb443-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cb443-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb443-145">**[Criar um utilizador de teste SpringCM](#creating-a-springcm-test-user)**  -toohave um homólogo de Britta Simon no SpringCM é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="cb443-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb443-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="cb443-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb443-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="cb443-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb443-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="cb443-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb443-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação SpringCM.</span><span class="sxs-lookup"><span data-stu-id="cb443-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="cb443-150">**tooconfigure do Azure AD-início de sessão único com SpringCM, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cb443-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb443-151">No Olá portal do Azure, no Olá **SpringCM** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="cb443-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="cb443-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="cb443-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="cb443-155">No Olá **SpringCM domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cb443-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="cb443-157">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="cb443-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb443-158">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="cb443-158">This value is not real.</span></span> <span data-ttu-id="cb443-159">Atualizar este valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="cb443-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="cb443-160">Contacte [equipa de suporte de cliente SpringCM](https://knowledge.springcm.com/support) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="cb443-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="cb443-161">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Raw)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="cb443-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="cb443-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="cb443-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cb443-165">No Olá **SpringCM configuração** secção, clique em **configurar SpringCM** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="cb443-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cb443-166">Olá cópia **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="cb443-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="cb443-168">Numa janela do browser web diferente, início de sessão tooyour **SpringCM** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="cb443-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="cb443-169">No menu de Olá na parte superior do Olá, clique em **ACEDA ao**, clique em **preferências**e, em seguida, no Olá **preferências de conta** secção, clique em **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="cb443-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="cb443-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="cb443-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="cb443-171">Na secção de configuração do fornecedor de identidade Olá, efetue Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cb443-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="cb443-172">![Configuração do fornecedor de identidade](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "configuração do fornecedor de identidade")</span><span class="sxs-lookup"><span data-stu-id="cb443-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="cb443-173">a.</span><span class="sxs-lookup"><span data-stu-id="cb443-173">a.</span></span> <span data-ttu-id="cb443-174">tooupload seu certificado transferido do Azure Active Directory, clique em **selecionar certificado de emissor** ou **certificados de emissor de alteração**.</span><span class="sxs-lookup"><span data-stu-id="cb443-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="cb443-175">b.</span><span class="sxs-lookup"><span data-stu-id="cb443-175">b.</span></span> <span data-ttu-id="cb443-176">Colar **ID de entidade de SAML** valor que copiou do portal do Azure para Olá **emissor** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cb443-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="cb443-177">c.</span><span class="sxs-lookup"><span data-stu-id="cb443-177">c.</span></span> <span data-ttu-id="cb443-178">Colar **único início de sessão no URL do serviço SAML** valor que copiou do Olá portal do Azure para Olá **fornecedor de serviço (SP) iniciada Endpoint** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cb443-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="cb443-179">d.</span><span class="sxs-lookup"><span data-stu-id="cb443-179">d.</span></span> <span data-ttu-id="cb443-180">Selecione **SAML ativada** como **ativar**.</span><span class="sxs-lookup"><span data-stu-id="cb443-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="cb443-181">e.</span><span class="sxs-lookup"><span data-stu-id="cb443-181">e.</span></span> <span data-ttu-id="cb443-182">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cb443-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="cb443-183">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="cb443-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb443-184">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="cb443-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb443-185">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb443-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb443-186">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb443-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb443-187">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb443-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="cb443-189">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cb443-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb443-190">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="cb443-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb443-192">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="cb443-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb443-194">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="cb443-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb443-196">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cb443-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb443-198">a.</span><span class="sxs-lookup"><span data-stu-id="cb443-198">a.</span></span> <span data-ttu-id="cb443-199">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb443-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb443-200">b.</span><span class="sxs-lookup"><span data-stu-id="cb443-200">b.</span></span> <span data-ttu-id="cb443-201">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cb443-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb443-202">c.</span><span class="sxs-lookup"><span data-stu-id="cb443-202">c.</span></span> <span data-ttu-id="cb443-203">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="cb443-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb443-204">d.</span><span class="sxs-lookup"><span data-stu-id="cb443-204">d.</span></span> <span data-ttu-id="cb443-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cb443-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="cb443-206">Criar um utilizador de teste SpringCM</span><span class="sxs-lookup"><span data-stu-id="cb443-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="cb443-207">toolog de utilizadores do Azure Active Directory tooenable no tooSpringCM, estes têm de ser aprovisionados para SpringCM.</span><span class="sxs-lookup"><span data-stu-id="cb443-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="cb443-208">No caso de Olá da SpringCM, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="cb443-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="cb443-209">Para obter mais informações, consulte [criar e editar um utilizador SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="cb443-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="cb443-210">**tooprovision um tooSpringCM de conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cb443-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb443-211">Inicie sessão no tooyour **SpringCM** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="cb443-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="cb443-212">Clique em **GOTO**e, em seguida, clique em **no livro de endereços**.</span><span class="sxs-lookup"><span data-stu-id="cb443-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="cb443-213">![Criar utilizador](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "criar utilizador")</span><span class="sxs-lookup"><span data-stu-id="cb443-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="cb443-214">Clique em **criar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="cb443-214">Click **Create User**.</span></span>

4. <span data-ttu-id="cb443-215">Selecione um **função de utilizador**.</span><span class="sxs-lookup"><span data-stu-id="cb443-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="cb443-216">Selecione **Enviar E-Mail de ativação**.</span><span class="sxs-lookup"><span data-stu-id="cb443-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="cb443-217">Nome do tipo Olá próprio, apelido e o endereço de e-mail de uma conta de utilizador válido do Azure Active Directory que pretende tooprovision Olá relacionados com caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="cb443-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="cb443-218">Adicionar Olá utilizador tooa **grupo de segurança**.</span><span class="sxs-lookup"><span data-stu-id="cb443-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="cb443-219">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cb443-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="cb443-220">Pode utilizar quaisquer outras SpringCM utilizador conta criação ferramentas ou APIs fornecidas pelo SpringCM tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="cb443-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb443-221">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb443-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb443-222">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSpringCM.</span><span class="sxs-lookup"><span data-stu-id="cb443-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="cb443-224">**tooassign Britta Simon tooSpringCM, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cb443-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb443-225">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="cb443-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="cb443-227">Na lista de aplicações de Olá, selecione **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="cb443-227">In hello applications list, select **SpringCM**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="cb443-229">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cb443-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="cb443-231">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="cb443-231">Click **Add** button.</span></span> <span data-ttu-id="cb443-232">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb443-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="cb443-234">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="cb443-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb443-235">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb443-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb443-236">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cb443-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb443-237">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="cb443-237">Testing single sign-on</span></span>

<span data-ttu-id="cb443-238">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="cb443-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="cb443-239">Ao clicar em mosaico de SpringCM Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour SpringCM aplicação.</span><span class="sxs-lookup"><span data-stu-id="cb443-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="cb443-240">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb443-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cb443-241">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cb443-241">Additional resources</span></span>

* [<span data-ttu-id="cb443-242">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb443-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb443-243">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb443-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

