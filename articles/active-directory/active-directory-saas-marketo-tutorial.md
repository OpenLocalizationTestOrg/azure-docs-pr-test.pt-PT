---
title: "Tutorial: Integração do Azure Active Directory com Marketo | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e do Marketo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="0256b-103">Tutorial: Integração do Azure Active Directory com Marketo</span><span class="sxs-lookup"><span data-stu-id="0256b-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="0256b-104">Neste tutorial, saiba como toointegrate Marketo no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0256b-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0256b-105">Integração do Marketo com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="0256b-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0256b-106">Pode controlar no Azure AD que tenha acesso tooMarketo</span><span class="sxs-lookup"><span data-stu-id="0256b-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="0256b-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooMarketo (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0256b-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0256b-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0256b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0256b-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0256b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0256b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0256b-110">Prerequisites</span></span>

<span data-ttu-id="0256b-111">integração do Azure AD com Marketo tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0256b-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="0256b-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0256b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0256b-113">Um Marketo início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="0256b-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0256b-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0256b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0256b-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0256b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0256b-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0256b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0256b-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0256b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0256b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0256b-118">Scenario description</span></span>
<span data-ttu-id="0256b-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0256b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0256b-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="0256b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0256b-121">A adição do Marketo da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="0256b-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="0256b-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="0256b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="0256b-123">A adição do Marketo da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="0256b-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="0256b-124">tooconfigure Olá integração do Marketo com o Azure AD, é necessário tooadd Marketo Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="0256b-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0256b-125">**tooadd Marketo da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0256b-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0256b-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="0256b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0256b-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0256b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0256b-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="0256b-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="0256b-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0256b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="0256b-133">Na caixa de pesquisa de Olá, escreva **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="0256b-133">In hello search box, type **Marketo**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="0256b-135">No painel de resultados de Olá, selecione **Marketo**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="0256b-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0256b-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="0256b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0256b-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Marketo com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0256b-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0256b-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Marketo é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0256b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="0256b-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Marketo tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0256b-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="0256b-141">No Marketo, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="0256b-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0256b-142">tooconfigure e teste do Azure AD-início de sessão único com Marketo, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0256b-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0256b-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="0256b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0256b-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0256b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0256b-145">**[Criar um utilizador de teste do Marketo](#creating-a-marketo-test-user)**  -toohave um homólogo de Britta Simon no Marketo é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="0256b-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0256b-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="0256b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0256b-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="0256b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0256b-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="0256b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0256b-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação do Marketo.</span><span class="sxs-lookup"><span data-stu-id="0256b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="0256b-150">**tooconfigure do Azure AD-início de sessão único com Marketo, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0256b-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="0256b-151">No Olá portal do Azure, no Olá **Marketo** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="0256b-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="0256b-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="0256b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="0256b-155">No Olá **URLs e de domínio do Marketo** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0256b-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="0256b-157">a.</span><span class="sxs-lookup"><span data-stu-id="0256b-157">a.</span></span> <span data-ttu-id="0256b-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="0256b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="0256b-159">b.</span><span class="sxs-lookup"><span data-stu-id="0256b-159">b.</span></span> <span data-ttu-id="0256b-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="0256b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0256b-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="0256b-161">These values are not real.</span></span> <span data-ttu-id="0256b-162">Atualize estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0256b-163">Contacte [equipa de suporte do Marketo](http://investors.marketo.com/contactus.cfm) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="0256b-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="0256b-164">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="0256b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="0256b-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="0256b-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0256b-168">No Olá **Marketo configuração** secção, clique em **configurar Marketo** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="0256b-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0256b-169">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="0256b-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="0256b-171">tooget Munchkin Id da aplicação, inicie sessão no tooMarketo utilizando credenciais de administrador e execute os seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="0256b-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="0256b-172">a.</span><span class="sxs-lookup"><span data-stu-id="0256b-172">a.</span></span> <span data-ttu-id="0256b-173">Inicie sessão na aplicação tooMarketo com credenciais do administrador.</span><span class="sxs-lookup"><span data-stu-id="0256b-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="0256b-174">b.</span><span class="sxs-lookup"><span data-stu-id="0256b-174">b.</span></span> <span data-ttu-id="0256b-175">Clique em Olá **Admin** botão no painel de navegação superior Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="0256b-177">c.</span><span class="sxs-lookup"><span data-stu-id="0256b-177">c.</span></span> <span data-ttu-id="0256b-178">Navegue toohello menu de integração e clique em Olá **ligação Munchkin**.</span><span class="sxs-lookup"><span data-stu-id="0256b-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="0256b-180">d.</span><span class="sxs-lookup"><span data-stu-id="0256b-180">d.</span></span> <span data-ttu-id="0256b-181">Copie Olá Id Munchkin mostrado no ecrã de Olá e concluir o seu URL de resposta no Assistente de configuração de Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0256b-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="0256b-183">tooconfigure Olá SSO na aplicação Olá, siga Olá passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="0256b-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="0256b-184">a.</span><span class="sxs-lookup"><span data-stu-id="0256b-184">a.</span></span> <span data-ttu-id="0256b-185">Inicie sessão na aplicação tooMarketo com credenciais do administrador.</span><span class="sxs-lookup"><span data-stu-id="0256b-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="0256b-186">b.</span><span class="sxs-lookup"><span data-stu-id="0256b-186">b.</span></span> <span data-ttu-id="0256b-187">Clique em Olá **Admin** botão no painel de navegação superior Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="0256b-189">c.</span><span class="sxs-lookup"><span data-stu-id="0256b-189">c.</span></span> <span data-ttu-id="0256b-190">Navegue toohello menu de integração e clique em **início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="0256b-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="0256b-192">d.</span><span class="sxs-lookup"><span data-stu-id="0256b-192">d.</span></span> <span data-ttu-id="0256b-193">Olá tooenable SAML definições, clique em **editar** botão.</span><span class="sxs-lookup"><span data-stu-id="0256b-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="0256b-195">e.</span><span class="sxs-lookup"><span data-stu-id="0256b-195">e.</span></span> <span data-ttu-id="0256b-196">**Ativado** Single Sign-On definições.</span><span class="sxs-lookup"><span data-stu-id="0256b-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="0256b-197">f.</span><span class="sxs-lookup"><span data-stu-id="0256b-197">f.</span></span> <span data-ttu-id="0256b-198">Olá colar **ID de entidade de SAML**, no Olá **emissor ID** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="0256b-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="0256b-199">g.</span><span class="sxs-lookup"><span data-stu-id="0256b-199">g.</span></span> <span data-ttu-id="0256b-200">No Olá **ID de entidade** caixa de texto, introduza o URL de Olá como `http://saml.marketo.com/sp`.</span><span class="sxs-lookup"><span data-stu-id="0256b-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="0256b-201">h.</span><span class="sxs-lookup"><span data-stu-id="0256b-201">h.</span></span> <span data-ttu-id="0256b-202">Selecione Olá localização do ID de utilizador como **elemento identificador de nome**.</span><span class="sxs-lookup"><span data-stu-id="0256b-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="0256b-204">Se o identificador de utilizador não é o valor UPN e altera o valor de Olá no separador de atributo Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="0256b-205">posso.</span><span class="sxs-lookup"><span data-stu-id="0256b-205">i.</span></span> <span data-ttu-id="0256b-206">Carregue o certificado Olá, que transferiu a partir do Assistente de configuração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0256b-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="0256b-207">**Guardar** Olá definições.</span><span class="sxs-lookup"><span data-stu-id="0256b-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="0256b-208">j.</span><span class="sxs-lookup"><span data-stu-id="0256b-208">j.</span></span> <span data-ttu-id="0256b-209">Edite definições de páginas de redirecionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="0256b-210">k.</span><span class="sxs-lookup"><span data-stu-id="0256b-210">k.</span></span> <span data-ttu-id="0256b-211">Olá colar **único início de sessão no URL do serviço SAML** no Olá **URL de início de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="0256b-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="0256b-212">l.</span><span class="sxs-lookup"><span data-stu-id="0256b-212">l.</span></span> <span data-ttu-id="0256b-213">Olá colar **Sign-Out URL** no Olá **URL de fim de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="0256b-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="0256b-214">m.</span><span class="sxs-lookup"><span data-stu-id="0256b-214">m.</span></span> <span data-ttu-id="0256b-215">No Olá **erro URL**, copiar o **URL de instância do Marketo** e clique em **guardar** botão toosave definições.</span><span class="sxs-lookup"><span data-stu-id="0256b-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="0256b-217">tooenable Olá SSO para os utilizadores, Olá concluída seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="0256b-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="0256b-218">a.</span><span class="sxs-lookup"><span data-stu-id="0256b-218">a.</span></span> <span data-ttu-id="0256b-219">Inicie sessão na aplicação tooMarketo com credenciais do administrador.</span><span class="sxs-lookup"><span data-stu-id="0256b-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="0256b-220">b.</span><span class="sxs-lookup"><span data-stu-id="0256b-220">b.</span></span> <span data-ttu-id="0256b-221">Clique em Olá **Admin** botão no painel de navegação superior Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="0256b-223">c.</span><span class="sxs-lookup"><span data-stu-id="0256b-223">c.</span></span> <span data-ttu-id="0256b-224">Navegue toohello **segurança** menu e **definições de início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="0256b-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="0256b-226">d.</span><span class="sxs-lookup"><span data-stu-id="0256b-226">d.</span></span> <span data-ttu-id="0256b-227">Verifique Olá **requerem SSO** opção e **guardar** Olá definições.</span><span class="sxs-lookup"><span data-stu-id="0256b-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="0256b-229">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="0256b-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0256b-230">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0256b-231">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0256b-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0256b-232">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0256b-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="0256b-233">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0256b-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="0256b-235">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0256b-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0256b-236">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="0256b-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0256b-238">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="0256b-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0256b-240">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0256b-242">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0256b-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0256b-244">a.</span><span class="sxs-lookup"><span data-stu-id="0256b-244">a.</span></span> <span data-ttu-id="0256b-245">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0256b-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0256b-246">b.</span><span class="sxs-lookup"><span data-stu-id="0256b-246">b.</span></span> <span data-ttu-id="0256b-247">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0256b-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0256b-248">c.</span><span class="sxs-lookup"><span data-stu-id="0256b-248">c.</span></span> <span data-ttu-id="0256b-249">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="0256b-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0256b-250">d.</span><span class="sxs-lookup"><span data-stu-id="0256b-250">d.</span></span> <span data-ttu-id="0256b-251">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0256b-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="0256b-252">Criar um utilizador de teste do Marketo</span><span class="sxs-lookup"><span data-stu-id="0256b-252">Creating a Marketo test user</span></span>

<span data-ttu-id="0256b-253">Nesta secção, vai criar um utilizador chamado Britta Simon Marketo.</span><span class="sxs-lookup"><span data-stu-id="0256b-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="0256b-254">Siga estes passos toocreate um utilizador na plataforma do Marketo.</span><span class="sxs-lookup"><span data-stu-id="0256b-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="0256b-255">Inicie sessão na aplicação tooMarketo com credenciais do administrador.</span><span class="sxs-lookup"><span data-stu-id="0256b-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="0256b-256">Clique em Olá **Admin** botão no painel de navegação superior Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="0256b-258">Navegue toohello **segurança** menu e **utilizadores e funções**</span><span class="sxs-lookup"><span data-stu-id="0256b-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="0256b-260">Clique em Olá **convidar novo utilizador** ligação no separador de utilizadores Olá</span><span class="sxs-lookup"><span data-stu-id="0256b-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="0256b-262">No Olá preenchimento Olá convidar novo utilizador assistente informações a seguir</span><span class="sxs-lookup"><span data-stu-id="0256b-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="0256b-263">a.</span><span class="sxs-lookup"><span data-stu-id="0256b-263">a.</span></span> <span data-ttu-id="0256b-264">Introduza o utilizador Olá **E-Mail** endereço na caixa de texto Olá</span><span class="sxs-lookup"><span data-stu-id="0256b-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="0256b-266">b.</span><span class="sxs-lookup"><span data-stu-id="0256b-266">b.</span></span> <span data-ttu-id="0256b-267">Introduza Olá **nome próprio** na caixa de texto Olá</span><span class="sxs-lookup"><span data-stu-id="0256b-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="0256b-268">c.</span><span class="sxs-lookup"><span data-stu-id="0256b-268">c.</span></span> <span data-ttu-id="0256b-269">Introduza Olá **Apelido** na caixa de texto Olá</span><span class="sxs-lookup"><span data-stu-id="0256b-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="0256b-270">d.</span><span class="sxs-lookup"><span data-stu-id="0256b-270">d.</span></span> <span data-ttu-id="0256b-271">Clique em **Seguinte**</span><span class="sxs-lookup"><span data-stu-id="0256b-271">Click **Next**</span></span>

6. <span data-ttu-id="0256b-272">No Olá **permissões** separador, selecione de Olá **userRoles** e clique em **seguinte**</span><span class="sxs-lookup"><span data-stu-id="0256b-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="0256b-274">Clique em Olá **enviar** botão convite de utilizador de Olá toosend</span><span class="sxs-lookup"><span data-stu-id="0256b-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="0256b-276">Utilizador recebe uma notificação de correio eletrónico Olá e tem tooclick Olá e alterar Olá palavra-passe tooactivate Olá conta da ligação.</span><span class="sxs-lookup"><span data-stu-id="0256b-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0256b-277">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0256b-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0256b-278">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooMarketo.</span><span class="sxs-lookup"><span data-stu-id="0256b-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="0256b-280">**tooassign Britta Simon tooMarketo, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0256b-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="0256b-281">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="0256b-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="0256b-283">Na lista de aplicações de Olá, selecione **Marketo**.</span><span class="sxs-lookup"><span data-stu-id="0256b-283">In hello applications list, select **Marketo**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="0256b-285">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0256b-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="0256b-287">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="0256b-287">Click **Add** button.</span></span> <span data-ttu-id="0256b-288">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0256b-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="0256b-290">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="0256b-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0256b-291">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0256b-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0256b-292">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0256b-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0256b-293">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="0256b-293">Testing single sign-on</span></span>

<span data-ttu-id="0256b-294">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="0256b-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0256b-295">Ao clicar em mosaico do Marketo Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Marketo aplicação.</span><span class="sxs-lookup"><span data-stu-id="0256b-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0256b-296">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0256b-296">Additional resources</span></span>

* [<span data-ttu-id="0256b-297">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0256b-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0256b-298">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0256b-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

