---
title: "Tutorial: Integração do Azure Active Directory com Panorama9 | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="fc83c-103">Tutorial: Integração do Azure Active Directory com Panorama9</span><span class="sxs-lookup"><span data-stu-id="fc83c-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="fc83c-104">Neste tutorial, saiba como toointegrate Panorama9 com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fc83c-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc83c-105">Integrar Panorama9 com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="fc83c-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fc83c-106">Pode controlar no Azure AD que tenha acesso tooPanorama9</span><span class="sxs-lookup"><span data-stu-id="fc83c-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="fc83c-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPanorama9 (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc83c-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fc83c-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fc83c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fc83c-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fc83c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc83c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fc83c-110">Prerequisites</span></span>

<span data-ttu-id="fc83c-111">integração do Azure AD com Panorama9 tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="fc83c-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="fc83c-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc83c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc83c-113">Um Panorama9-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="fc83c-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fc83c-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="fc83c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fc83c-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="fc83c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc83c-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="fc83c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc83c-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc83c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fc83c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="fc83c-118">Scenario description</span></span>
<span data-ttu-id="fc83c-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="fc83c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc83c-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="fc83c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc83c-121">Adicionar Panorama9 da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="fc83c-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="fc83c-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="fc83c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="fc83c-123">Adicionar Panorama9 da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="fc83c-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="fc83c-124">tooconfigure Olá integração de Panorama9 com o Azure AD, é necessário tooadd Panorama9 Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="fc83c-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fc83c-125">**tooadd Panorama9 da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fc83c-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc83c-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="fc83c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fc83c-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fc83c-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="fc83c-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fc83c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="fc83c-133">Na caixa de pesquisa de Olá, escreva **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-133">In hello search box, type **Panorama9**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="fc83c-135">No painel de resultados de Olá, selecione **Panorama9**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="fc83c-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fc83c-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="fc83c-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="fc83c-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Panorama9 com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="fc83c-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fc83c-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Panorama9 é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc83c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="fc83c-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Panorama9 tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="fc83c-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="fc83c-141">No Panorama9, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="fc83c-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fc83c-142">tooconfigure e teste do Azure AD-início de sessão único com Panorama9, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fc83c-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fc83c-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="fc83c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fc83c-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc83c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc83c-145">**[Criar um utilizador de teste Panorama9](#creating-a-panorama9-test-user)**  -toohave um homólogo de Britta Simon no Panorama9 é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="fc83c-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc83c-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="fc83c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc83c-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="fc83c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fc83c-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="fc83c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fc83c-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Panorama9.</span><span class="sxs-lookup"><span data-stu-id="fc83c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="fc83c-150">**tooconfigure do Azure AD-início de sessão único com Panorama9, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fc83c-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc83c-151">No Olá portal do Azure, no Olá **Panorama9** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="fc83c-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="fc83c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="fc83c-155">No Olá **Panorama9 domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="fc83c-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="fc83c-157">a.</span><span class="sxs-lookup"><span data-stu-id="fc83c-157">a.</span></span> <span data-ttu-id="fc83c-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL como:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="fc83c-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="fc83c-159">b.</span><span class="sxs-lookup"><span data-stu-id="fc83c-159">b.</span></span> <span data-ttu-id="fc83c-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="fc83c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fc83c-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="fc83c-161">These values are not real.</span></span> <span data-ttu-id="fc83c-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="fc83c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fc83c-163">Contacte [equipa de suporte de cliente Panorama9](https://support.panorama9.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="fc83c-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="fc83c-164">No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.</span><span class="sxs-lookup"><span data-stu-id="fc83c-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="fc83c-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="fc83c-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fc83c-168">No Olá **Panorama9 configuração** secção, clique em **configurar Panorama9** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="fc83c-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fc83c-169">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="fc83c-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="fc83c-171">Numa janela do browser web diferente, inicie sessão no site da sua empresa Panorama9 como administrador.</span><span class="sxs-lookup"><span data-stu-id="fc83c-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="fc83c-172">Na barra de ferramentas Olá na parte superior do Olá, clique em **gerir**e, em seguida, clique em **extensões**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="fc83c-173">![Extensões](./media/active-directory-saas-panorama9-tutorial/ic790023.png "extensões")</span><span class="sxs-lookup"><span data-stu-id="fc83c-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="fc83c-174">No Olá **extensões** caixa de diálogo, clique em **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="fc83c-175">![De sessão único-](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="fc83c-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="fc83c-176">No Olá **definições** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="fc83c-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="fc83c-177">![Definições](./media/active-directory-saas-panorama9-tutorial/ic790025.png "definições")</span><span class="sxs-lookup"><span data-stu-id="fc83c-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="fc83c-178">a.</span><span class="sxs-lookup"><span data-stu-id="fc83c-178">a.</span></span> <span data-ttu-id="fc83c-179">No **URL do fornecedor de identidade** caixa de texto, colar Olá valor **URL Single Sign-On serviço**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc83c-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="fc83c-180">b.</span><span class="sxs-lookup"><span data-stu-id="fc83c-180">b.</span></span> <span data-ttu-id="fc83c-181">No **impressão digital do certificado** caixa de texto, colar Olá **Thumbprint** valor do certificado, o qual copiou a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc83c-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="fc83c-182">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="fc83c-183">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="fc83c-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fc83c-184">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="fc83c-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fc83c-185">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fc83c-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fc83c-186">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc83c-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="fc83c-187">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc83c-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="fc83c-189">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fc83c-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc83c-190">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="fc83c-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fc83c-192">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fc83c-194">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="fc83c-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fc83c-196">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="fc83c-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fc83c-198">a.</span><span class="sxs-lookup"><span data-stu-id="fc83c-198">a.</span></span> <span data-ttu-id="fc83c-199">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fc83c-200">b.</span><span class="sxs-lookup"><span data-stu-id="fc83c-200">b.</span></span> <span data-ttu-id="fc83c-201">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fc83c-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fc83c-202">c.</span><span class="sxs-lookup"><span data-stu-id="fc83c-202">c.</span></span> <span data-ttu-id="fc83c-203">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fc83c-204">d.</span><span class="sxs-lookup"><span data-stu-id="fc83c-204">d.</span></span> <span data-ttu-id="fc83c-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="fc83c-206">Criar um utilizador de teste Panorama9</span><span class="sxs-lookup"><span data-stu-id="fc83c-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="fc83c-207">Na ordem tooenable do Azure AD os utilizadores toolog para Panorama9, têm de ser aprovisionados para Panorama9.</span><span class="sxs-lookup"><span data-stu-id="fc83c-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="fc83c-208">No caso de Olá da Panorama9, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="fc83c-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="fc83c-209">**tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fc83c-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc83c-210">Inicie sessão no tooyour **Panorama9** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="fc83c-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="fc83c-211">No menu de Olá na parte superior do Olá, clique em **gerir**e, em seguida, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="fc83c-212">![Os utilizadores](./media/active-directory-saas-panorama9-tutorial/ic790027.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="fc83c-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="fc83c-213">Na secção utilizadores Olá, clique em  **+**  tooadd novo utilizador.</span><span class="sxs-lookup"><span data-stu-id="fc83c-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="fc83c-214">![Os utilizadores](./media/active-directory-saas-panorama9-tutorial/ic790028.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="fc83c-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="fc83c-215">Aceda toohello secção de dados de utilizador, Olá tipo endereço de e-mail de um utilizador válido do Azure Active Directory que pretende tooprovision para Olá **E-Mail** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fc83c-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="fc83c-216">São fornecidos toohello seção de utilizadores, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="fc83c-217">titular de conta do Azure Active Directory Olá recebe uma mensagem de e-mail e de que respeita a tooconfirm uma ligação a respetiva conta para ficar ativa.</span><span class="sxs-lookup"><span data-stu-id="fc83c-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fc83c-218">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc83c-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fc83c-219">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPanorama9.</span><span class="sxs-lookup"><span data-stu-id="fc83c-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="fc83c-221">**tooassign Britta Simon tooPanorama9, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fc83c-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc83c-222">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="fc83c-224">Na lista de aplicações de Olá, selecione **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-224">In hello applications list, select **Panorama9**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="fc83c-226">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="fc83c-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="fc83c-228">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="fc83c-228">Click **Add** button.</span></span> <span data-ttu-id="fc83c-229">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fc83c-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="fc83c-231">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="fc83c-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fc83c-232">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fc83c-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc83c-233">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fc83c-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fc83c-234">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="fc83c-234">Testing single sign-on</span></span>

<span data-ttu-id="fc83c-235">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="fc83c-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fc83c-236">Ao clicar em mosaico de Olá Panorama9 no painel de acesso de Olá, deve colocar a aplicação de tooPanorama9 automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="fc83c-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="fc83c-237">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fc83c-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc83c-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fc83c-238">Additional resources</span></span>

* [<span data-ttu-id="fc83c-239">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc83c-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc83c-240">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fc83c-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

