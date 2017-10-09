---
title: "Tutorial: Integração do Azure Active Directory com HappyFox | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 1190652d7d1144c7eddea339cb3f9175912407fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="618aa-103">Tutorial: Integração do Azure Active Directory com HappyFox</span><span class="sxs-lookup"><span data-stu-id="618aa-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="618aa-104">Neste tutorial, saiba como toointegrate HappyFox com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="618aa-104">In this tutorial, you learn how toointegrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="618aa-105">Integrar HappyFox com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="618aa-105">Integrating HappyFox with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="618aa-106">Pode controlar no Azure AD que tenha acesso tooHappyFox</span><span class="sxs-lookup"><span data-stu-id="618aa-106">You can control in Azure AD who has access tooHappyFox</span></span>
- <span data-ttu-id="618aa-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooHappyFox (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="618aa-107">You can enable your users tooautomatically get signed-on tooHappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="618aa-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="618aa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="618aa-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="618aa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="618aa-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="618aa-110">Prerequisites</span></span>

<span data-ttu-id="618aa-111">integração do Azure AD com HappyFox tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="618aa-111">tooconfigure Azure AD integration with HappyFox, you need hello following items:</span></span>

- <span data-ttu-id="618aa-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="618aa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="618aa-113">Um HappyFox início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="618aa-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="618aa-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="618aa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="618aa-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="618aa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="618aa-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="618aa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="618aa-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="618aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="618aa-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="618aa-118">Scenario description</span></span>
<span data-ttu-id="618aa-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="618aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="618aa-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="618aa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="618aa-121">Adicionar HappyFox da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="618aa-121">Adding HappyFox from hello gallery</span></span>
2. <span data-ttu-id="618aa-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="618aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-hello-gallery"></a><span data-ttu-id="618aa-123">Adicionar HappyFox da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="618aa-123">Adding HappyFox from hello gallery</span></span>
<span data-ttu-id="618aa-124">tooconfigure Olá integração de HappyFox com o Azure AD, é necessário tooadd HappyFox Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="618aa-124">tooconfigure hello integration of HappyFox into Azure AD, you need tooadd HappyFox from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="618aa-125">**tooadd HappyFox da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="618aa-125">**tooadd HappyFox from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="618aa-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="618aa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="618aa-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="618aa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="618aa-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="618aa-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="618aa-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="618aa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="618aa-133">Na caixa de pesquisa de Olá, escreva **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="618aa-133">In hello search box, type **HappyFox**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="618aa-135">No painel de resultados de Olá, selecione **HappyFox**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="618aa-135">In hello results panel, select **HappyFox**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="618aa-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="618aa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="618aa-138">Nesta secção, configure e teste do Azure AD-início de sessão único com HappyFox com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="618aa-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="618aa-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá HappyFox é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="618aa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HappyFox is tooa user in Azure AD.</span></span> <span data-ttu-id="618aa-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá HappyFox tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="618aa-140">In other words, a link relationship between an Azure AD user and hello related user in HappyFox needs toobe established.</span></span>

<span data-ttu-id="618aa-141">No HappyFox, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="618aa-141">In HappyFox, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="618aa-142">tooconfigure e teste do Azure AD-início de sessão único com HappyFox, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="618aa-142">tooconfigure and test Azure AD single sign-on with HappyFox, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="618aa-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="618aa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="618aa-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="618aa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="618aa-145">**[Criar um utilizador de teste HappyFox](#creating-a-happyfox-test-user)**  -toohave um homólogo de Britta Simon no HappyFox é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="618aa-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - toohave a counterpart of Britta Simon in HappyFox that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="618aa-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="618aa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="618aa-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="618aa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="618aa-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="618aa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="618aa-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação HappyFox.</span><span class="sxs-lookup"><span data-stu-id="618aa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="618aa-150">**tooconfigure do Azure AD-início de sessão único com HappyFox, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="618aa-150">**tooconfigure Azure AD single sign-on with HappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="618aa-151">No Olá portal do Azure, no Olá **HappyFox** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="618aa-151">In hello Azure portal, on hello **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="618aa-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="618aa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="618aa-155">No Olá **HappyFox domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="618aa-155">On hello **HappyFox Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="618aa-157">a.</span><span class="sxs-lookup"><span data-stu-id="618aa-157">a.</span></span> <span data-ttu-id="618aa-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="618aa-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="618aa-159">b.</span><span class="sxs-lookup"><span data-stu-id="618aa-159">b.</span></span> <span data-ttu-id="618aa-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="618aa-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="618aa-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="618aa-161">These values are not real.</span></span> <span data-ttu-id="618aa-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="618aa-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="618aa-163">Contacte [equipa de suporte de cliente HappyFox](https://support.happyfox.com/home) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="618aa-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) tooget these values.</span></span> 
 
4. <span data-ttu-id="618aa-164">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="618aa-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="618aa-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="618aa-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="618aa-168">No Olá **HappyFox configuração** secção, clique em **configurar HappyFox** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="618aa-168">On hello **HappyFox Configuration** section, click **Configure HappyFox** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="618aa-169">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida**.</span><span class="sxs-lookup"><span data-stu-id="618aa-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="618aa-171">Inicie sessão no portal do tooyour HappyFox pessoal e navegue demasiado**gerir**, clique em **integrações** separador.</span><span class="sxs-lookup"><span data-stu-id="618aa-171">Sign on tooyour HappyFox staff portal and navigate too**Manage**, Click on **Integrations** tab.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="618aa-173">No separador de integrações Olá, clique em **configurar** em **SAML integração** tooopen Olá início de sessão único em definições.</span><span class="sxs-lookup"><span data-stu-id="618aa-173">In hello Integrations tab, Click **Configure** under **SAML Integration** tooopen hello Single Sign On Settings.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="618aa-175">Na secção de configuração de SAML, cole Olá **único início de sessão no URL do serviço SAML** que copiou a partir do portal do Azure para **URL de destino de SSO** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="618aa-175">Inside SAML configuration section, paste hello **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="618aa-177">Abra o certificado Olá transferido a partir do portal do Azure no bloco de notas e cole o conteúdo **IdP assinatura** secção.</span><span class="sxs-lookup"><span data-stu-id="618aa-177">Open hello certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="618aa-179">Clique em **guardar definições** botão.</span><span class="sxs-lookup"><span data-stu-id="618aa-179">Click **Save Settings** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="618aa-181">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="618aa-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="618aa-182">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="618aa-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="618aa-183">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="618aa-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="618aa-184">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="618aa-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="618aa-185">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="618aa-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="618aa-187">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="618aa-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="618aa-188">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="618aa-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="618aa-190">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="618aa-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="618aa-192">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="618aa-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="618aa-194">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="618aa-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="618aa-196">a.</span><span class="sxs-lookup"><span data-stu-id="618aa-196">a.</span></span> <span data-ttu-id="618aa-197">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="618aa-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="618aa-198">b.</span><span class="sxs-lookup"><span data-stu-id="618aa-198">b.</span></span> <span data-ttu-id="618aa-199">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="618aa-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="618aa-200">c.</span><span class="sxs-lookup"><span data-stu-id="618aa-200">c.</span></span> <span data-ttu-id="618aa-201">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="618aa-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="618aa-202">d.</span><span class="sxs-lookup"><span data-stu-id="618aa-202">d.</span></span> <span data-ttu-id="618aa-203">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="618aa-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="618aa-204">Criar um utilizador de teste HappyFox</span><span class="sxs-lookup"><span data-stu-id="618aa-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="618aa-205">Aplicação suporta apenas no tempo de aprovisionamento de utilizador e de utilizadores de autenticação são criados na aplicação Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="618aa-205">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="618aa-206">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="618aa-206">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="618aa-207">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooHappyFox.</span><span class="sxs-lookup"><span data-stu-id="618aa-207">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHappyFox.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="618aa-209">**tooassign Britta Simon tooHappyFox, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="618aa-209">**tooassign Britta Simon tooHappyFox, perform hello following steps:**</span></span>

1. <span data-ttu-id="618aa-210">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="618aa-210">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="618aa-212">Na lista de aplicações de Olá, selecione **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="618aa-212">In hello applications list, select **HappyFox**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="618aa-214">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="618aa-214">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="618aa-216">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="618aa-216">Click **Add** button.</span></span> <span data-ttu-id="618aa-217">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="618aa-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="618aa-219">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="618aa-219">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="618aa-220">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="618aa-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="618aa-221">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="618aa-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="618aa-222">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="618aa-222">Testing single sign-on</span></span>

<span data-ttu-id="618aa-223">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="618aa-223">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="618aa-224">Ao clicar em mosaico de HappyFox Olá no painel de acesso de Olá, deve obter a página de início de sessão da aplicação HappyFox.</span><span class="sxs-lookup"><span data-stu-id="618aa-224">When you click hello HappyFox tile in hello Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="618aa-225">Deverá ver Olá **'SAML'** botão página de início de sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="618aa-225">You should see hello **‘SAML’** button on hello sign-in page.</span></span>

    ![Plug-in](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="618aa-227">Clique em Olá **'SAML'** botão toolog no tooHappyFox utilizando a sua conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="618aa-227">Click hello **‘SAML’** button toolog in tooHappyFox using your Azure AD account.</span></span>

<span data-ttu-id="618aa-228">Para obter mais informações sobre Olá painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="618aa-228">For more information about hello Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="618aa-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="618aa-229">Additional resources</span></span>

* [<span data-ttu-id="618aa-230">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="618aa-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="618aa-231">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="618aa-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

