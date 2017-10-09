---
title: "Tutorial: Integração do Azure Active Directory com UserVoice | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="9cdd1-103">Tutorial: Integração do Azure Active Directory com UserVoice</span><span class="sxs-lookup"><span data-stu-id="9cdd1-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="9cdd1-104">Neste tutorial, saiba como toointegrate UserVoice com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9cdd1-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cdd1-105">Integrar o UserVoice com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9cdd1-106">Pode controlar no Azure AD que tenha acesso tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="9cdd1-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooUserVoice (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9cdd1-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9cdd1-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cdd1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cdd1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9cdd1-110">Prerequisites</span></span>

<span data-ttu-id="9cdd1-111">integração do Azure AD com UserVoice tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="9cdd1-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cdd1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cdd1-113">Um UserVoice-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="9cdd1-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cdd1-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cdd1-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cdd1-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cdd1-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cdd1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cdd1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9cdd1-118">Scenario description</span></span>
<span data-ttu-id="9cdd1-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cdd1-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cdd1-121">Adicionar UserVoice da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="9cdd1-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="9cdd1-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="9cdd1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="9cdd1-123">Adicionar UserVoice da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="9cdd1-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="9cdd1-124">tooconfigure Olá integração do UserVoice com o Azure AD, é necessário tooadd UserVoice Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9cdd1-125">**tooadd UserVoice da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9cdd1-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cdd1-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="9cdd1-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9cdd1-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="9cdd1-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="9cdd1-133">Na caixa de pesquisa de Olá, escreva **UserVoice**, selecione **UserVoice** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados do UserVoice no Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9cdd1-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9cdd1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9cdd1-136">Nesta secção, configure e teste do Azure AD-início de sessão único com UserVoice com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9cdd1-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9cdd1-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá UserVoice é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="9cdd1-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no UserVoice tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="9cdd1-139">No UserVoice, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9cdd1-140">tooconfigure e teste do Azure AD-início de sessão único com o UserVoice, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9cdd1-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9cdd1-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cdd1-143">**[Criar um utilizador de teste do UserVoice](#create-a-uservoice-test-user)**  -toohave um homólogo de Britta Simon no UserVoice é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cdd1-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cdd1-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9cdd1-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9cdd1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9cdd1-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação da UserVoice.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="9cdd1-148">**tooconfigure do Azure AD-início de sessão único com o UserVoice, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9cdd1-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cdd1-149">No Olá portal do Azure, no Olá **UserVoice** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="9cdd1-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="9cdd1-153">No Olá **UserVoice domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![UserVoice domínio e os URLs únicos de informações de início de sessão](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="9cdd1-155">a.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-155">a.</span></span> <span data-ttu-id="9cdd1-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="9cdd1-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="9cdd1-157">b.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-157">b.</span></span> <span data-ttu-id="9cdd1-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="9cdd1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9cdd1-159">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-159">These values are not real.</span></span> <span data-ttu-id="9cdd1-160">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9cdd1-161">Contacte [equipa de suporte de cliente do UserVoice](https://www.uservoice.com/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="9cdd1-162">No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="9cdd1-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-164">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cdd1-166">No Olá **UserVoice configuração** secção, clique em **configurar UserVoice** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9cdd1-167">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9cdd1-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="9cdd1-169">Numa janela do browser web diferente, inicie sessão no site de empresa do UserVoice tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="9cdd1-170">Na barra de ferramentas Olá na parte superior do Olá, clique em **definições**e, em seguida, selecione **Web portal** menu Olá.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="9cdd1-171">![Secção de definições no lado de aplicação](./media/active-directory-saas-uservoice-tutorial/ic777519.png "definições")</span><span class="sxs-lookup"><span data-stu-id="9cdd1-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="9cdd1-172">No Olá **Web portal** separador, Olá **autenticação de utilizador** secção, clique em **editar** tooopen Olá **editar autenticação de utilizador** caixa de diálogo página.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="9cdd1-173">![Portal Web do separador](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span><span class="sxs-lookup"><span data-stu-id="9cdd1-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="9cdd1-174">No Olá **editar autenticação de utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="9cdd1-175">![Editar autenticação de utilizador](./media/active-directory-saas-uservoice-tutorial/ic777521.png "editar autenticação de utilizador")</span><span class="sxs-lookup"><span data-stu-id="9cdd1-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="9cdd1-176">a.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-176">a.</span></span> <span data-ttu-id="9cdd1-177">Clique em **Single Sign-On (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="9cdd1-178">b.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-178">b.</span></span> <span data-ttu-id="9cdd1-179">Olá colar **único início de sessão no URL do serviço SAML** valor que copiou do Olá portal do Azure para Olá **SSO remoto início de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="9cdd1-180">c.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-180">c.</span></span> <span data-ttu-id="9cdd1-181">Olá colar **Sign-Out URL** valor que copiou do Olá portal do Azure para Olá **Sign-Out remoto SSO caixa de texto**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="9cdd1-182">d.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-182">d.</span></span> <span data-ttu-id="9cdd1-183">Olá colar **Thumbprint** valor que copiou do portal do Azure para o **impressão digital de certificado SHA1 atual** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="9cdd1-184">e.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-184">e.</span></span> <span data-ttu-id="9cdd1-185">Clique em **guardar as definições de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="9cdd1-186">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="9cdd1-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9cdd1-187">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9cdd1-188">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cdd1-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9cdd1-189">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cdd1-189">Create an Azure AD test user</span></span>

<span data-ttu-id="9cdd1-190">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="9cdd1-192">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9cdd1-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cdd1-193">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9cdd1-195">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9cdd1-197">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9cdd1-199">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9cdd1-201">a.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-201">a.</span></span> <span data-ttu-id="9cdd1-202">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cdd1-203">b.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-203">b.</span></span> <span data-ttu-id="9cdd1-204">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9cdd1-205">c.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-205">c.</span></span> <span data-ttu-id="9cdd1-206">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9cdd1-207">d.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-207">d.</span></span> <span data-ttu-id="9cdd1-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="9cdd1-209">Criar um utilizador de teste do UserVoice</span><span class="sxs-lookup"><span data-stu-id="9cdd1-209">Create a UserVoice test user</span></span>

<span data-ttu-id="9cdd1-210">tooenable do Azure AD os utilizadores toolog no tooUserVoice, estes têm de ser aprovisionados para UserVoice.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="9cdd1-211">No caso de Olá da UserVoice, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="9cdd1-212">tooprovision uma conta de utilizador, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="9cdd1-213">Inicie sessão no tooyour **UserVoice** inquilino.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="9cdd1-214">Aceda demasiado**definições**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="9cdd1-215">![Definições](./media/active-directory-saas-uservoice-tutorial/ic777811.png "definições")</span><span class="sxs-lookup"><span data-stu-id="9cdd1-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="9cdd1-216">Clique em **geral**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-216">Click **General**.</span></span>

4. <span data-ttu-id="9cdd1-217">Clique em **agentes e permissões**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="9cdd1-218">![Os agentes e permissões](./media/active-directory-saas-uservoice-tutorial/ic777812.png "agentes e permissões")</span><span class="sxs-lookup"><span data-stu-id="9cdd1-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="9cdd1-219">Clique em **adicione administradores**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="9cdd1-220">![Adicionar administradores](./media/active-directory-saas-uservoice-tutorial/ic777813.png "adicione administradores")</span><span class="sxs-lookup"><span data-stu-id="9cdd1-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="9cdd1-221">No Olá **convidar admins** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9cdd1-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="9cdd1-222">![Convidar admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "convidar admins")</span><span class="sxs-lookup"><span data-stu-id="9cdd1-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="9cdd1-223">a.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-223">a.</span></span> <span data-ttu-id="9cdd1-224">Na caixa de texto de mensagens de correio eletrónico Olá, escreva o endereço de correio eletrónico Olá da conta de Olá pretende tooprovision e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="9cdd1-225">b.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-225">b.</span></span> <span data-ttu-id="9cdd1-226">Clique em **convidar**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="9cdd1-227">Pode utilizar quaisquer outras UserVoice utilizador conta criação ferramentas ou APIs fornecidas pelo UserVoice tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9cdd1-228">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cdd1-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9cdd1-229">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="9cdd1-231">**tooassign Britta Simon tooUserVoice, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9cdd1-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cdd1-232">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="9cdd1-234">Na lista de aplicações de Olá, selecione **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-234">In hello applications list, select **UserVoice**.</span></span>

    ![ligação do UserVoice Olá na lista de aplicações de Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="9cdd1-236">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="9cdd1-238">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-238">Click **Add** button.</span></span> <span data-ttu-id="9cdd1-239">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="9cdd1-241">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9cdd1-242">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cdd1-243">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9cdd1-244">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9cdd1-244">Test single sign-on</span></span>

<span data-ttu-id="9cdd1-245">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9cdd1-246">Ao clicar em mosaico de UserVoice Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour UserVoice aplicação.</span><span class="sxs-lookup"><span data-stu-id="9cdd1-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="9cdd1-247">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9cdd1-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9cdd1-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9cdd1-248">Additional resources</span></span>

* [<span data-ttu-id="9cdd1-249">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cdd1-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cdd1-250">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cdd1-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

