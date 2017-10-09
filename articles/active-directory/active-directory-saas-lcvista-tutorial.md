---
title: "Tutorial: Integração do Azure Active Directory com LCVista | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="a43a5-103">Tutorial: Integração do Azure Active Directory com LCVista</span><span class="sxs-lookup"><span data-stu-id="a43a5-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="a43a5-104">Neste tutorial, saiba como toointegrate LCVista com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a43a5-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a43a5-105">Integrar LCVista com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="a43a5-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a43a5-106">Pode controlar no Azure AD que tenha acesso tooLCVista</span><span class="sxs-lookup"><span data-stu-id="a43a5-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="a43a5-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooLCVista (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a43a5-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a43a5-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a43a5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a43a5-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a43a5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a43a5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a43a5-110">Prerequisites</span></span>

<span data-ttu-id="a43a5-111">integração do Azure AD com LCVista tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a43a5-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="a43a5-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a43a5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a43a5-113">Um LCVista início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="a43a5-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a43a5-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a43a5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a43a5-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a43a5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a43a5-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a43a5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a43a5-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a43a5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a43a5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a43a5-118">Scenario description</span></span>
<span data-ttu-id="a43a5-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a43a5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a43a5-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="a43a5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a43a5-121">Adicionar LCVista da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a43a5-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="a43a5-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a43a5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="a43a5-123">Adicionar LCVista da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a43a5-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="a43a5-124">tooconfigure Olá integração de LCVista com o Azure AD, é necessário tooadd LCVista Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="a43a5-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a43a5-125">**tooadd LCVista da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a43a5-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a43a5-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a43a5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a43a5-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a43a5-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="a43a5-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a43a5-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="a43a5-133">Na caixa de pesquisa de Olá, escreva **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-133">In hello search box, type **LCVista**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="a43a5-135">No painel de resultados de Olá, selecione **LCVista**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="a43a5-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a43a5-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a43a5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a43a5-138">Nesta secção, configure e teste do Azure AD-início de sessão único com LCVista com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a43a5-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a43a5-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá LCVista é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a43a5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="a43a5-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá LCVista tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a43a5-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="a43a5-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no LCVista.</span><span class="sxs-lookup"><span data-stu-id="a43a5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="a43a5-142">tooconfigure e teste do Azure AD-início de sessão único com LCVista, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a43a5-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a43a5-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a43a5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a43a5-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a43a5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a43a5-145">**[Criar um utilizador de teste LCVista](#creating-a-lcvista-test-user)**  -toohave um homólogo de Britta Simon no LCVista é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="a43a5-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a43a5-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a43a5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a43a5-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="a43a5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a43a5-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a43a5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a43a5-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação LCVista.</span><span class="sxs-lookup"><span data-stu-id="a43a5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="a43a5-150">**tooconfigure do Azure AD-início de sessão único com LCVista, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a43a5-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="a43a5-151">No Olá portal do Azure, no Olá **LCVista** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="a43a5-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a43a5-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="a43a5-155">No Olá **LCVista domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a43a5-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="a43a5-157">a.</span><span class="sxs-lookup"><span data-stu-id="a43a5-157">a.</span></span> <span data-ttu-id="a43a5-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="a43a5-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="a43a5-159">b.</span><span class="sxs-lookup"><span data-stu-id="a43a5-159">b.</span></span> <span data-ttu-id="a43a5-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="a43a5-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="a43a5-161">Estes valores não estiverem Olá real.</span><span class="sxs-lookup"><span data-stu-id="a43a5-161">These values are not hello real.</span></span> <span data-ttu-id="a43a5-162">Atualizar estes valores com Olá real identificador e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="a43a5-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="a43a5-163">Contacte [equipa de suporte de cliente LCVista](https://lcvista.com/contact) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="a43a5-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="a43a5-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a43a5-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="a43a5-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="a43a5-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="a43a5-168">No Olá **LCVista configuração** secção, clique em **configurar LCVista** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="a43a5-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a43a5-169">Olá cópia **ID de entidade de SAML** e **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="a43a5-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="a43a5-171">Início de sessão tooyour LCVista aplicação como um administrador.</span><span class="sxs-lookup"><span data-stu-id="a43a5-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="a43a5-172">No Olá **configuração SAML** secção, verifique Olá **início de sessão SAML ativar** e introduza os detalhes de Olá, tal como mencionado na abaixo imagem.</span><span class="sxs-lookup"><span data-stu-id="a43a5-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="a43a5-174">a.</span><span class="sxs-lookup"><span data-stu-id="a43a5-174">a.</span></span> <span data-ttu-id="a43a5-175">Olá colar **URL do emissor** que copiou do Azure AD no Olá **ID de entidade** secção.</span><span class="sxs-lookup"><span data-stu-id="a43a5-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="a43a5-176">b.</span><span class="sxs-lookup"><span data-stu-id="a43a5-176">b.</span></span> <span data-ttu-id="a43a5-177">Olá colar **URL Single Sign-On serviço** que copiou do Azure AD no Olá **URL** secção.</span><span class="sxs-lookup"><span data-stu-id="a43a5-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="a43a5-178">c.</span><span class="sxs-lookup"><span data-stu-id="a43a5-178">c.</span></span> <span data-ttu-id="a43a5-179">De metadados (XML) que transferiu a partir do portal do Azure, copie o valor de Olá **certificado X509** e colá-lo na Olá **certificados x509** secção.</span><span class="sxs-lookup"><span data-stu-id="a43a5-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="a43a5-180">d.</span><span class="sxs-lookup"><span data-stu-id="a43a5-180">d.</span></span> <span data-ttu-id="a43a5-181">No Olá **nome próprio atributo** caixa de texto, colar Olá valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="a43a5-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="a43a5-182">e.</span><span class="sxs-lookup"><span data-stu-id="a43a5-182">e.</span></span> <span data-ttu-id="a43a5-183">No Olá **atributo de nome do último** caixa de texto, colar Olá valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="a43a5-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="a43a5-184">f.</span><span class="sxs-lookup"><span data-stu-id="a43a5-184">f.</span></span> <span data-ttu-id="a43a5-185">No Olá **atributo de correio eletrónico** caixa de texto, colar Olá valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="a43a5-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="a43a5-186">g.</span><span class="sxs-lookup"><span data-stu-id="a43a5-186">g.</span></span> <span data-ttu-id="a43a5-187">No Olá **atributo de nome de utilizador** caixa de texto, colar Olá valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="a43a5-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="a43a5-188">e.</span><span class="sxs-lookup"><span data-stu-id="a43a5-188">e.</span></span> <span data-ttu-id="a43a5-189">Clique em **guardar** definições de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="a43a5-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="a43a5-190">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="a43a5-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a43a5-191">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="a43a5-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a43a5-192">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a43a5-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a43a5-193">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a43a5-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="a43a5-194">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a43a5-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="a43a5-196">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a43a5-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a43a5-197">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a43a5-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a43a5-199">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a43a5-201">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="a43a5-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a43a5-203">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a43a5-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a43a5-205">a.</span><span class="sxs-lookup"><span data-stu-id="a43a5-205">a.</span></span> <span data-ttu-id="a43a5-206">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a43a5-207">b.</span><span class="sxs-lookup"><span data-stu-id="a43a5-207">b.</span></span> <span data-ttu-id="a43a5-208">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a43a5-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a43a5-209">c.</span><span class="sxs-lookup"><span data-stu-id="a43a5-209">c.</span></span> <span data-ttu-id="a43a5-210">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a43a5-211">d.</span><span class="sxs-lookup"><span data-stu-id="a43a5-211">d.</span></span> <span data-ttu-id="a43a5-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="a43a5-213">Criar um utilizador de teste LCVista</span><span class="sxs-lookup"><span data-stu-id="a43a5-213">Creating a LCVista test user</span></span>

<span data-ttu-id="a43a5-214">Nesta secção, vai criar um utilizador chamado Britta Simon LCVista.</span><span class="sxs-lookup"><span data-stu-id="a43a5-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="a43a5-215">Terá de toocontact [equipa de suporte de cliente LCVista](https://lcvista.com/contact) tooadd utilizadores Olá Olá LCVista aplicação.</span><span class="sxs-lookup"><span data-stu-id="a43a5-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a43a5-216">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a43a5-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a43a5-217">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooLCVista.</span><span class="sxs-lookup"><span data-stu-id="a43a5-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="a43a5-219">**tooassign Britta Simon tooLCVista, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a43a5-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="a43a5-220">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="a43a5-222">Na lista de aplicações de Olá, selecione **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-222">In hello applications list, select **LCVista**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="a43a5-224">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a43a5-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="a43a5-226">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="a43a5-226">Click **Add** button.</span></span> <span data-ttu-id="a43a5-227">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a43a5-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="a43a5-229">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="a43a5-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a43a5-230">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a43a5-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a43a5-231">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a43a5-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a43a5-232">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a43a5-232">Testing single sign-on</span></span>

<span data-ttu-id="a43a5-233">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a43a5-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="a43a5-234">Clique no mosaico LCVista Olá no painel de acesso Olá, será redirecionado tooOrganization página de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="a43a5-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="a43a5-235">Após o início de sessão com êxito, será com sessão iniciada tooyour LCVista aplicação.</span><span class="sxs-lookup"><span data-stu-id="a43a5-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="a43a5-236">Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a43a5-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a43a5-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a43a5-237">Additional resources</span></span>

* [<span data-ttu-id="a43a5-238">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a43a5-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a43a5-239">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a43a5-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

