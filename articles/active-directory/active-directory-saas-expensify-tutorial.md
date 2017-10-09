---
title: "Tutorial: Integração do Azure Active Directory com Expensify | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: 141513ef27c90dae2d77a52ecab2f89c4e5a55ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="cfe23-103">Tutorial: Integração do Azure Active Directory com Expensify</span><span class="sxs-lookup"><span data-stu-id="cfe23-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="cfe23-104">Neste tutorial, saiba como toointegrate Expensify com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cfe23-104">In this tutorial, you learn how toointegrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cfe23-105">Integrar Expensify com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="cfe23-105">Integrating Expensify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cfe23-106">Pode controlar no Azure AD que tenha acesso tooExpensify</span><span class="sxs-lookup"><span data-stu-id="cfe23-106">You can control in Azure AD who has access tooExpensify</span></span>
- <span data-ttu-id="cfe23-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooExpensify (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfe23-107">You can enable your users tooautomatically get signed-on tooExpensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cfe23-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cfe23-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cfe23-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cfe23-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfe23-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cfe23-110">Prerequisites</span></span>

<span data-ttu-id="cfe23-111">integração do Azure AD com Expensify tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="cfe23-111">tooconfigure Azure AD integration with Expensify, you need hello following items:</span></span>

- <span data-ttu-id="cfe23-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfe23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cfe23-113">Um Expensify início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="cfe23-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cfe23-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cfe23-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cfe23-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cfe23-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cfe23-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cfe23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cfe23-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cfe23-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cfe23-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cfe23-118">Scenario description</span></span>
<span data-ttu-id="cfe23-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cfe23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cfe23-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="cfe23-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cfe23-121">Adicionar Expensify da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="cfe23-121">Adding Expensify from hello gallery</span></span>
2. <span data-ttu-id="cfe23-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="cfe23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-hello-gallery"></a><span data-ttu-id="cfe23-123">Adicionar Expensify da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="cfe23-123">Adding Expensify from hello gallery</span></span>
<span data-ttu-id="cfe23-124">tooconfigure Olá integração de Expensify com o Azure AD, é necessário tooadd Expensify Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="cfe23-124">tooconfigure hello integration of Expensify into Azure AD, you need tooadd Expensify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cfe23-125">**tooadd Expensify da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cfe23-125">**tooadd Expensify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfe23-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="cfe23-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cfe23-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cfe23-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="cfe23-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfe23-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="cfe23-133">Na caixa de pesquisa de Olá, escreva **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-133">In hello search box, type **Expensify**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="cfe23-135">No painel de resultados de Olá, selecione **Expensify**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="cfe23-135">In hello results panel, select **Expensify**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cfe23-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="cfe23-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cfe23-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Expensify com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cfe23-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cfe23-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Expensify é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfe23-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Expensify is tooa user in Azure AD.</span></span> <span data-ttu-id="cfe23-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Expensify tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cfe23-140">In other words, a link relationship between an Azure AD user and hello related user in Expensify needs toobe established.</span></span>

<span data-ttu-id="cfe23-141">No Expensify, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="cfe23-141">In Expensify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cfe23-142">tooconfigure e teste do Azure AD-início de sessão único com Expensify, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cfe23-142">tooconfigure and test Azure AD single sign-on with Expensify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cfe23-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="cfe23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cfe23-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cfe23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cfe23-145">**[Criar um utilizador de teste Expensify](#creating-an-expensify-test-user)**  -toohave um homólogo de Britta Simon no Expensify é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="cfe23-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - toohave a counterpart of Britta Simon in Expensify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cfe23-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="cfe23-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cfe23-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="cfe23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cfe23-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="cfe23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cfe23-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Expensify.</span><span class="sxs-lookup"><span data-stu-id="cfe23-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="cfe23-150">**tooconfigure do Azure AD-início de sessão único com Expensify, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cfe23-150">**tooconfigure Azure AD single sign-on with Expensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfe23-151">No Olá portal do Azure, no Olá **Expensify** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-151">In hello Azure portal, on hello **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="cfe23-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="cfe23-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="cfe23-155">No Olá **Expensify domínios e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cfe23-155">On hello **Expensify Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="cfe23-157">a.</span><span class="sxs-lookup"><span data-stu-id="cfe23-157">a.</span></span> <span data-ttu-id="cfe23-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="cfe23-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="cfe23-159">b.</span><span class="sxs-lookup"><span data-stu-id="cfe23-159">b.</span></span> <span data-ttu-id="cfe23-160">No Olá **URL de identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="cfe23-160">In hello **Identifier URL** textbox, type a URL using hello following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="cfe23-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="cfe23-161">These values are not real.</span></span> <span data-ttu-id="cfe23-162">Atualize estes valores com o URL de início de sessão do URL e o identificador real no Olá.</span><span class="sxs-lookup"><span data-stu-id="cfe23-162">Update these values with hello actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="cfe23-163">Contacte [equipa de suporte de cliente Expensify](mailto:help@expensify.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="cfe23-163">Contact [Expensify Client support team](mailto:help@expensify.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="cfe23-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="cfe23-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="cfe23-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="cfe23-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cfe23-168">tooenable SSO no Expensify, terá primeiro tooenable **domínio controlo** na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="cfe23-168">tooenable SSO in Expensify, you first need tooenable **Domain Control** in hello application.</span></span> <span data-ttu-id="cfe23-169">Pode ativar o controlo de domínio na aplicação Olá passos Olá listados [aqui](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="cfe23-169">You can enable Domain Control in hello application through hello steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="cfe23-170">Para obter suporte adicional, trabalhar com [equipa de suporte de cliente Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="cfe23-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="cfe23-171">Depois de ter controlo de domínio ativado, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="cfe23-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="cfe23-173">a.</span><span class="sxs-lookup"><span data-stu-id="cfe23-173">a.</span></span> <span data-ttu-id="cfe23-174">Início de sessão tooyour Expensify aplicação.</span><span class="sxs-lookup"><span data-stu-id="cfe23-174">Sign on tooyour Expensify application.</span></span>
    
    <span data-ttu-id="cfe23-175">b.</span><span class="sxs-lookup"><span data-stu-id="cfe23-175">b.</span></span> <span data-ttu-id="cfe23-176">Na barra de ferramentas Olá na parte superior do Olá, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-176">In hello toolbar on hello top, click **Admin**.</span></span>
    
    <span data-ttu-id="cfe23-177">c.</span><span class="sxs-lookup"><span data-stu-id="cfe23-177">c.</span></span> <span data-ttu-id="cfe23-178">No painel esquerdo Olá, clique em **domínio**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-178">In hello left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="cfe23-179">d.</span><span class="sxs-lookup"><span data-stu-id="cfe23-179">d.</span></span> <span data-ttu-id="cfe23-180">Clique no nome do domínio verificado.</span><span class="sxs-lookup"><span data-stu-id="cfe23-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="cfe23-181">e.</span><span class="sxs-lookup"><span data-stu-id="cfe23-181">e.</span></span> <span data-ttu-id="cfe23-182">No painel esquerdo Olá, clique em **SAML**e, em seguida, selecione **ativado**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-182">In hello left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="cfe23-183">f.</span><span class="sxs-lookup"><span data-stu-id="cfe23-183">f.</span></span> <span data-ttu-id="cfe23-184">Abra Olá transferir metadados de Federação do Azure AD no bloco de notas, Olá copiar conteúdo e, em seguida, cole-o Olá **metadados do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cfe23-184">Open hello downloaded Federation Metadata from Azure AD in notepad, copy hello content, and then paste it into hello **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="cfe23-185">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="cfe23-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cfe23-186">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="cfe23-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cfe23-187">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cfe23-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cfe23-188">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfe23-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="cfe23-189">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe23-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="cfe23-191">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cfe23-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfe23-192">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="cfe23-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cfe23-194">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cfe23-196">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="cfe23-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cfe23-198">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="cfe23-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cfe23-200">a.</span><span class="sxs-lookup"><span data-stu-id="cfe23-200">a.</span></span> <span data-ttu-id="cfe23-201">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cfe23-202">b.</span><span class="sxs-lookup"><span data-stu-id="cfe23-202">b.</span></span> <span data-ttu-id="cfe23-203">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cfe23-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cfe23-204">c.</span><span class="sxs-lookup"><span data-stu-id="cfe23-204">c.</span></span> <span data-ttu-id="cfe23-205">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cfe23-206">d.</span><span class="sxs-lookup"><span data-stu-id="cfe23-206">d.</span></span> <span data-ttu-id="cfe23-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="cfe23-208">Criar um utilizador de teste Expensify</span><span class="sxs-lookup"><span data-stu-id="cfe23-208">Creating an Expensify test user</span></span>

<span data-ttu-id="cfe23-209">Nesta secção, vai criar um utilizador chamado Britta Simon Expensify.</span><span class="sxs-lookup"><span data-stu-id="cfe23-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="cfe23-210">Trabalhar com [equipa de suporte de cliente Expensify](mailto:help@expensify.com) utilizadores de Olá tooadd na plataforma de Expensify Olá.</span><span class="sxs-lookup"><span data-stu-id="cfe23-210">Work with [Expensify Client support team](mailto:help@expensify.com) tooadd hello users in hello Expensify platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cfe23-211">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfe23-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cfe23-212">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooExpensify.</span><span class="sxs-lookup"><span data-stu-id="cfe23-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooExpensify.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="cfe23-214">**tooassign Britta Simon tooExpensify, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="cfe23-214">**tooassign Britta Simon tooExpensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="cfe23-215">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="cfe23-217">Na lista de aplicações de Olá, selecione **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-217">In hello applications list, select **Expensify**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="cfe23-219">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cfe23-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="cfe23-221">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="cfe23-221">Click **Add** button.</span></span> <span data-ttu-id="cfe23-222">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfe23-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="cfe23-224">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="cfe23-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cfe23-225">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfe23-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cfe23-226">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cfe23-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cfe23-227">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="cfe23-227">Testing single sign-on</span></span>

<span data-ttu-id="cfe23-228">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="cfe23-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="cfe23-229">Ao clicar em mosaico de Expensify Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Expensify aplicação.</span><span class="sxs-lookup"><span data-stu-id="cfe23-229">When you click hello Expensify tile in hello Access Panel, you should get automatically signed-on tooyour Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cfe23-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cfe23-230">Additional resources</span></span>

* [<span data-ttu-id="cfe23-231">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfe23-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cfe23-232">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cfe23-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

