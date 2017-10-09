---
title: "Tutorial: Integração do Azure Active Directory com Bime | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="952f5-103">Tutorial: Integração do Azure Active Directory com Bime</span><span class="sxs-lookup"><span data-stu-id="952f5-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="952f5-104">Neste tutorial, saiba como toointegrate Bime com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="952f5-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="952f5-105">Integrar Bime com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="952f5-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="952f5-106">Pode controlar no Azure AD que tenha acesso tooBime</span><span class="sxs-lookup"><span data-stu-id="952f5-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="952f5-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooBime (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="952f5-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="952f5-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="952f5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="952f5-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="952f5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="952f5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="952f5-110">Prerequisites</span></span>

<span data-ttu-id="952f5-111">integração do Azure AD com Bime tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="952f5-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="952f5-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="952f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="952f5-113">Um Bime-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="952f5-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="952f5-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="952f5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="952f5-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="952f5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="952f5-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="952f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="952f5-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="952f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="952f5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="952f5-118">Scenario description</span></span>
<span data-ttu-id="952f5-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="952f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="952f5-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="952f5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="952f5-121">Adicionar Bime da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="952f5-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="952f5-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="952f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="952f5-123">Adicionar Bime da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="952f5-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="952f5-124">tooconfigure Olá integração de Bime com o Azure AD, é necessário tooadd Bime Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="952f5-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="952f5-125">**tooadd Bime da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="952f5-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="952f5-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="952f5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="952f5-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="952f5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="952f5-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="952f5-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="952f5-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="952f5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="952f5-133">Na caixa de pesquisa de Olá, escreva **Bime**.</span><span class="sxs-lookup"><span data-stu-id="952f5-133">In hello search box, type **Bime**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="952f5-135">No painel de resultados de Olá, selecione **Bime**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="952f5-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="952f5-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="952f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="952f5-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Bime com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="952f5-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="952f5-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Bime é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="952f5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="952f5-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Bime tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="952f5-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="952f5-141">No Bime, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="952f5-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="952f5-142">tooconfigure e teste do Azure AD-início de sessão único com Bime, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="952f5-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="952f5-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="952f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="952f5-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="952f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="952f5-145">**[Criar um utilizador de teste Bime](#creating-a-bime-test-user)**  -toohave um homólogo de Britta Simon no Bime é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="952f5-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="952f5-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="952f5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="952f5-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="952f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="952f5-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="952f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="952f5-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Bime.</span><span class="sxs-lookup"><span data-stu-id="952f5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="952f5-150">**tooconfigure do Azure AD-início de sessão único com Bime, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="952f5-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="952f5-151">No Olá portal do Azure, no Olá **Bime** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="952f5-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="952f5-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="952f5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="952f5-155">No Olá **Bime domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="952f5-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="952f5-157">a.</span><span class="sxs-lookup"><span data-stu-id="952f5-157">a.</span></span> <span data-ttu-id="952f5-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="952f5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="952f5-159">b.</span><span class="sxs-lookup"><span data-stu-id="952f5-159">b.</span></span> <span data-ttu-id="952f5-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="952f5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="952f5-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="952f5-161">These values are not real.</span></span> <span data-ttu-id="952f5-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="952f5-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="952f5-163">Contacte [equipa de suporte de cliente Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="952f5-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="952f5-164">No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="952f5-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="952f5-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="952f5-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="952f5-168">No Olá **Bime configuração** secção, clique em **configurar Bime** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="952f5-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="952f5-169">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="952f5-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="952f5-171">Numa janela do browser web diferente, inicie sessão no site da sua empresa Bime como administrador.</span><span class="sxs-lookup"><span data-stu-id="952f5-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="952f5-172">Na barra de ferramentas Olá, clique em **Admin**e, em seguida, **conta**.</span><span class="sxs-lookup"><span data-stu-id="952f5-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="952f5-173">![Administração](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="952f5-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="952f5-174">Na página de configuração de conta Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="952f5-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="952f5-175">![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/ic775559.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="952f5-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="952f5-176">a.</span><span class="sxs-lookup"><span data-stu-id="952f5-176">a.</span></span> <span data-ttu-id="952f5-177">Selecione **autenticação ativar SAML**.</span><span class="sxs-lookup"><span data-stu-id="952f5-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="952f5-178">b.</span><span class="sxs-lookup"><span data-stu-id="952f5-178">b.</span></span> <span data-ttu-id="952f5-179">No Olá **URL de início de sessão remoto** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="952f5-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="952f5-180">c.</span><span class="sxs-lookup"><span data-stu-id="952f5-180">c.</span></span>  <span data-ttu-id="952f5-181">Olá colar **Thumbprint** valor a partir do portal do Azure para Olá **impressão digital do certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="952f5-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="952f5-182">d.</span><span class="sxs-lookup"><span data-stu-id="952f5-182">d.</span></span> <span data-ttu-id="952f5-183">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="952f5-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="952f5-184">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="952f5-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="952f5-185">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="952f5-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="952f5-186">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="952f5-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="952f5-187">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="952f5-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="952f5-188">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="952f5-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="952f5-190">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="952f5-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="952f5-191">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="952f5-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="952f5-193">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="952f5-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="952f5-195">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="952f5-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="952f5-197">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="952f5-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="952f5-199">a.</span><span class="sxs-lookup"><span data-stu-id="952f5-199">a.</span></span> <span data-ttu-id="952f5-200">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="952f5-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="952f5-201">b.</span><span class="sxs-lookup"><span data-stu-id="952f5-201">b.</span></span> <span data-ttu-id="952f5-202">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="952f5-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="952f5-203">c.</span><span class="sxs-lookup"><span data-stu-id="952f5-203">c.</span></span> <span data-ttu-id="952f5-204">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="952f5-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="952f5-205">d.</span><span class="sxs-lookup"><span data-stu-id="952f5-205">d.</span></span> <span data-ttu-id="952f5-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="952f5-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="952f5-207">Criar um utilizador de teste Bime</span><span class="sxs-lookup"><span data-stu-id="952f5-207">Creating a Bime test user</span></span>

<span data-ttu-id="952f5-208">Na ordem tooenable do Azure AD os utilizadores toolog no tooBime, têm de ser aprovisionados para Bime.</span><span class="sxs-lookup"><span data-stu-id="952f5-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="952f5-209">No caso de Olá da Bime, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="952f5-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="952f5-210">**tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="952f5-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="952f5-211">Inicie sessão no tooyour **Bime** inquilino.</span><span class="sxs-lookup"><span data-stu-id="952f5-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="952f5-212">Na barra de ferramentas Olá, clique em **Admin**e, em seguida, **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="952f5-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="952f5-213">![Administração](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="952f5-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="952f5-214">No Olá **lista utilizadores**, clique em **adicionar novo utilizador** ("+").</span><span class="sxs-lookup"><span data-stu-id="952f5-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="952f5-215">![Os utilizadores](./media/active-directory-saas-bime-tutorial/ic775562.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="952f5-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="952f5-216">No Olá **detalhes de utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="952f5-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="952f5-217">![Detalhes de utilizador](./media/active-directory-saas-bime-tutorial/ic775563.png "detalhes de utilizador")</span><span class="sxs-lookup"><span data-stu-id="952f5-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="952f5-218">a.</span><span class="sxs-lookup"><span data-stu-id="952f5-218">a.</span></span> <span data-ttu-id="952f5-219">No Olá **nome próprio** caixa de texto, introduza Olá primeiro nome de utilizador como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="952f5-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="952f5-220">b.</span><span class="sxs-lookup"><span data-stu-id="952f5-220">b.</span></span> <span data-ttu-id="952f5-221">No Olá **Apelido** caixa de texto, introduza o apelido Olá do utilizador, como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="952f5-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="952f5-222">c.</span><span class="sxs-lookup"><span data-stu-id="952f5-222">c.</span></span> <span data-ttu-id="952f5-223">No Olá **E-Mail** caixa de texto, introduza Olá e-mail do utilizador, como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="952f5-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="952f5-224">d.</span><span class="sxs-lookup"><span data-stu-id="952f5-224">d.</span></span> <span data-ttu-id="952f5-225">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="952f5-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="952f5-226">Pode utilizar quaisquer outras Bime utilizador conta criação ferramentas ou APIs fornecidas pelo Bime tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="952f5-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="952f5-227">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="952f5-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="952f5-228">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooBime.</span><span class="sxs-lookup"><span data-stu-id="952f5-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="952f5-230">**tooassign Britta Simon tooBime, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="952f5-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="952f5-231">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="952f5-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="952f5-233">Na lista de aplicações de Olá, selecione **Bime**.</span><span class="sxs-lookup"><span data-stu-id="952f5-233">In hello applications list, select **Bime**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="952f5-235">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="952f5-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="952f5-237">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="952f5-237">Click **Add** button.</span></span> <span data-ttu-id="952f5-238">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="952f5-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="952f5-240">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="952f5-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="952f5-241">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="952f5-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="952f5-242">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="952f5-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="952f5-243">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="952f5-243">Testing single sign-on</span></span>

<span data-ttu-id="952f5-244">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="952f5-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="952f5-245">Ao clicar em mosaico de Bime Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Bime aplicação.</span><span class="sxs-lookup"><span data-stu-id="952f5-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="952f5-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="952f5-246">Additional resources</span></span>

* [<span data-ttu-id="952f5-247">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="952f5-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="952f5-248">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="952f5-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

