---
title: "Tutorial: Integração do Azure Active Directory com a plataforma de Capriza | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Capriza plataforma."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1c4adb737bb5ba4690bbf74688010238c5c83f3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="0927e-103">Tutorial: Integração do Azure Active Directory Capriza plataforma</span><span class="sxs-lookup"><span data-stu-id="0927e-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="0927e-104">Neste tutorial, saiba como toointegrate Capriza plataforma no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0927e-104">In this tutorial, you learn how toointegrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0927e-105">Integrar Capriza plataforma com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="0927e-105">Integrating Capriza Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0927e-106">Pode controlar no Azure AD que tenha acesso tooCapriza plataforma</span><span class="sxs-lookup"><span data-stu-id="0927e-106">You can control in Azure AD who has access tooCapriza Platform</span></span>
- <span data-ttu-id="0927e-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooCapriza plataforma (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0927e-107">You can enable your users tooautomatically get signed-on tooCapriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0927e-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0927e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0927e-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0927e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0927e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0927e-110">Prerequisites</span></span>

<span data-ttu-id="0927e-111">integração do Azure AD com a plataforma de Capriza tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0927e-111">tooconfigure Azure AD integration with Capriza Platform, you need hello following items:</span></span>

- <span data-ttu-id="0927e-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0927e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0927e-113">Uma plataforma de Capriza-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="0927e-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0927e-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0927e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0927e-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0927e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0927e-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0927e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0927e-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0927e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0927e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0927e-118">Scenario description</span></span>
<span data-ttu-id="0927e-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0927e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0927e-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="0927e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0927e-121">A adição de plataforma Capriza de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="0927e-121">Adding Capriza Platform from hello gallery</span></span>
2. <span data-ttu-id="0927e-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="0927e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-hello-gallery"></a><span data-ttu-id="0927e-123">A adição de plataforma Capriza de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="0927e-123">Adding Capriza Platform from hello gallery</span></span>
<span data-ttu-id="0927e-124">tooconfigure Olá integração da plataforma Capriza com o Azure AD, é necessário tooadd Capriza plataforma Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="0927e-124">tooconfigure hello integration of Capriza Platform into Azure AD, you need tooadd Capriza Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0927e-125">**tooadd Capriza plataforma a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0927e-125">**tooadd Capriza Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0927e-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="0927e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0927e-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0927e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0927e-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="0927e-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="0927e-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0927e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="0927e-133">Na caixa de pesquisa de Olá, escreva **Capriza plataforma**.</span><span class="sxs-lookup"><span data-stu-id="0927e-133">In hello search box, type **Capriza Platform**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="0927e-135">No painel de resultados de Olá, selecione **Capriza plataforma**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="0927e-135">In hello results panel, select **Capriza Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0927e-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="0927e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0927e-138">Nesta secção, configure e teste do Azure AD-início de sessão único com a plataforma de Capriza com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0927e-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0927e-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Capriza plataforma é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0927e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Capriza Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="0927e-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Capriza plataforma tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0927e-140">In other words, a link relationship between an Azure AD user and hello related user in Capriza Platform needs toobe established.</span></span>

<span data-ttu-id="0927e-141">Na plataforma de Capriza, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="0927e-141">In Capriza Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0927e-142">tooconfigure e teste do Azure AD-início de sessão único com a plataforma de Capriza, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0927e-142">tooconfigure and test Azure AD single sign-on with Capriza Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0927e-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="0927e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0927e-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0927e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0927e-145">**[Criar um utilizador de teste de plataforma Capriza](#creating-a-capriza-platform-test-user)**  -toohave um homólogo de Britta Simon na plataforma de Capriza que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="0927e-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - toohave a counterpart of Britta Simon in Capriza Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0927e-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="0927e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0927e-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="0927e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0927e-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="0927e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0927e-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Capriza plataforma.</span><span class="sxs-lookup"><span data-stu-id="0927e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="0927e-150">**tooconfigure do Azure AD-início de sessão único com a plataforma de Capriza efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0927e-150">**tooconfigure Azure AD single sign-on with Capriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="0927e-151">No Olá portal do Azure, no Olá **Capriza plataforma** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="0927e-151">In hello Azure portal, on hello **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="0927e-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="0927e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="0927e-155">No Olá **Capriza plataforma de domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0927e-155">On hello **Capriza Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="0927e-157">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="0927e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0927e-158">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="0927e-158">This value is not real.</span></span> <span data-ttu-id="0927e-159">Atualizar este valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="0927e-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0927e-160">Contacte [equipa de suporte de cliente de plataforma Capriza](mailTo:support@capriza.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="0927e-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) tooget this value.</span></span> 

4. <span data-ttu-id="0927e-161">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="0927e-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="0927e-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="0927e-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0927e-165">No Olá **Capriza plataforma configuração** secção, clique em **configurar plataforma de Capriza** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="0927e-165">On hello **Capriza Platform Configuration** section, click **Configure Capriza Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0927e-166">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="0927e-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="0927e-168">tooconfigure-início de sessão único em **Capriza plataforma** lado, terá de Olá toosend transferido **certificado**, **Sign-Out URL**, **ID de entidade de SAML** e **único início de sessão no URL do serviço SAML** demasiado[equipa de suporte de plataforma Capriza](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="0927e-168">tooconfigure single sign-on on **Capriza Platform** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="0927e-169">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="0927e-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="0927e-170">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="0927e-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0927e-171">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="0927e-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0927e-172">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0927e-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0927e-173">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0927e-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="0927e-174">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0927e-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="0927e-176">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0927e-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0927e-177">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="0927e-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0927e-179">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="0927e-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0927e-181">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="0927e-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0927e-183">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0927e-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0927e-185">a.</span><span class="sxs-lookup"><span data-stu-id="0927e-185">a.</span></span> <span data-ttu-id="0927e-186">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0927e-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0927e-187">b.</span><span class="sxs-lookup"><span data-stu-id="0927e-187">b.</span></span> <span data-ttu-id="0927e-188">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0927e-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0927e-189">c.</span><span class="sxs-lookup"><span data-stu-id="0927e-189">c.</span></span> <span data-ttu-id="0927e-190">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="0927e-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0927e-191">d.</span><span class="sxs-lookup"><span data-stu-id="0927e-191">d.</span></span> <span data-ttu-id="0927e-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0927e-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="0927e-193">Criar um utilizador de teste Capriza plataforma</span><span class="sxs-lookup"><span data-stu-id="0927e-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="0927e-194">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Capriza.</span><span class="sxs-lookup"><span data-stu-id="0927e-194">hello objective of this section is toocreate a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="0927e-195">Capriza suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.</span><span class="sxs-lookup"><span data-stu-id="0927e-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="0927e-196">**Certifique-se que o seu nome de domínio está configurado com Capriza para aprovisionamento de utilizadores. Após esse Olá apenas o aprovisionamento de utilizadores de just-in-time irá funcionar.**</span><span class="sxs-lookup"><span data-stu-id="0927e-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only hello just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="0927e-197">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="0927e-197">There is no action item for you in this section.</span></span> <span data-ttu-id="0927e-198">Será criado um novo utilizador durante uma tentativa tooaccess Capriza se não existir ainda.</span><span class="sxs-lookup"><span data-stu-id="0927e-198">A new user will be created during an attempt tooaccess Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0927e-199">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0927e-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0927e-200">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooCapriza plataforma.</span><span class="sxs-lookup"><span data-stu-id="0927e-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCapriza Platform.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="0927e-202">**tooassign Britta Simon tooCapriza plataforma, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0927e-202">**tooassign Britta Simon tooCapriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="0927e-203">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="0927e-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="0927e-205">Na lista de aplicações de Olá, selecione **Capriza plataforma**.</span><span class="sxs-lookup"><span data-stu-id="0927e-205">In hello applications list, select **Capriza Platform**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="0927e-207">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0927e-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="0927e-209">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="0927e-209">Click **Add** button.</span></span> <span data-ttu-id="0927e-210">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0927e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="0927e-212">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="0927e-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0927e-213">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0927e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0927e-214">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0927e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0927e-215">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="0927e-215">Testing single sign-on</span></span>

<span data-ttu-id="0927e-216">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="0927e-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0927e-217">Ao clicar Olá Capriza plataforma na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour Capriza aplicação.</span><span class="sxs-lookup"><span data-stu-id="0927e-217">When you click hello Capriza Platform tile in hello Access Panel, you should get automatically signed-on tooyour Capriza application.</span></span> <span data-ttu-id="0927e-218">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0927e-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0927e-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0927e-219">Additional resources</span></span>

* [<span data-ttu-id="0927e-220">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0927e-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0927e-221">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0927e-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

