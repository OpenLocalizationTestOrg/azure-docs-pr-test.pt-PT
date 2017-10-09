---
title: "Tutorial: Integração do Azure Active Directory com ITRP | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="eff45-103">Tutorial: Integração do Azure Active Directory com ITRP</span><span class="sxs-lookup"><span data-stu-id="eff45-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="eff45-104">Neste tutorial, saiba como toointegrate ITRP com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eff45-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eff45-105">Integrar ITRP com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="eff45-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eff45-106">Pode controlar no Azure AD que tenha acesso tooITRP</span><span class="sxs-lookup"><span data-stu-id="eff45-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="eff45-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooITRP (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eff45-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eff45-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eff45-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eff45-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eff45-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eff45-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eff45-110">Prerequisites</span></span>

<span data-ttu-id="eff45-111">integração do Azure AD com ITRP tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="eff45-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="eff45-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eff45-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eff45-113">Um ITRP-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="eff45-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eff45-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="eff45-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eff45-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="eff45-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eff45-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="eff45-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eff45-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eff45-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eff45-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="eff45-118">Scenario description</span></span>
<span data-ttu-id="eff45-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="eff45-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eff45-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="eff45-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eff45-121">Adicionar ITRP da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="eff45-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="eff45-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="eff45-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="eff45-123">Adicionar ITRP da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="eff45-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="eff45-124">tooconfigure Olá integração de ITRP no tooAzure AD, é necessário tooadd ITRP Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="eff45-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eff45-125">**tooadd ITRP da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="eff45-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff45-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="eff45-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eff45-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="eff45-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eff45-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="eff45-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="eff45-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff45-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="eff45-133">Na caixa de pesquisa de Olá, escreva **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="eff45-133">In hello search box, type **ITRP**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="eff45-135">No painel de resultados de Olá, selecione **ITRP**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="eff45-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eff45-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="eff45-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="eff45-138">Nesta secção, configure e teste do Azure AD-início de sessão único com ITRP com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="eff45-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eff45-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ITRP é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eff45-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="eff45-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ITRP tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="eff45-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="eff45-141">No ITRP, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="eff45-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eff45-142">tooconfigure e teste do Azure AD-início de sessão único com ITRP, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="eff45-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eff45-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="eff45-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eff45-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eff45-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eff45-145">**[Criar um ITRP utilizador de teste](#creating-an-itrp-test-user)**  -toohave um homólogo de Britta Simon no ITRP é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="eff45-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eff45-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="eff45-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eff45-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="eff45-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eff45-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="eff45-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eff45-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação ITRP.</span><span class="sxs-lookup"><span data-stu-id="eff45-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="eff45-150">**tooconfigure do Azure AD-início de sessão único com ITRP, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="eff45-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff45-151">No Olá portal do Azure, no Olá **ITRP** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="eff45-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="eff45-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="eff45-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="eff45-155">No Olá **ITRP domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="eff45-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="eff45-157">a.</span><span class="sxs-lookup"><span data-stu-id="eff45-157">a.</span></span> <span data-ttu-id="eff45-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="eff45-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="eff45-159">b.</span><span class="sxs-lookup"><span data-stu-id="eff45-159">b.</span></span> <span data-ttu-id="eff45-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="eff45-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eff45-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="eff45-161">These values are not real.</span></span> <span data-ttu-id="eff45-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="eff45-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eff45-163">Contacte [equipa de suporte de cliente ITRP](https://www.itrp.com/support) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="eff45-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="eff45-164">No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.</span><span class="sxs-lookup"><span data-stu-id="eff45-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="eff45-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="eff45-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eff45-168">No Olá **ITRP configuração** secção, clique em **configurar ITRP** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="eff45-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eff45-169">Olá cópia **único início de sessão no URL do serviço SAML e o URL de Sign-Out** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="eff45-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="eff45-171">Numa janela do browser web diferente, inicie sessão no site da empresa tooyour ITRP como administrador.</span><span class="sxs-lookup"><span data-stu-id="eff45-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="eff45-172">Na barra de ferramentas Olá na parte superior do Olá, clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="eff45-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="eff45-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="eff45-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="eff45-174">No painel de navegação esquerdo Olá, selecione **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="eff45-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="eff45-175">![De sessão único-](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="eff45-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="eff45-176">Na secção de configuração Single Sign-On Olá, efetue Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="eff45-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="eff45-177">![De sessão único-](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="eff45-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="eff45-178">![De sessão único-](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="eff45-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="eff45-179">a.</span><span class="sxs-lookup"><span data-stu-id="eff45-179">a.</span></span> <span data-ttu-id="eff45-180">Clique em **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="eff45-180">Click **Enable**.</span></span>

    <span data-ttu-id="eff45-181">b.</span><span class="sxs-lookup"><span data-stu-id="eff45-181">b.</span></span> <span data-ttu-id="eff45-182">No **remoto URL terminar sessão** caixa de texto, colar Olá valor **Sign-Out URL**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eff45-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="eff45-183">c.</span><span class="sxs-lookup"><span data-stu-id="eff45-183">c.</span></span> <span data-ttu-id="eff45-184">No **SAML SSO URL** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eff45-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="eff45-185">d.In **impressão digital do certificado** caixa de texto, colar Olá **Thumbprint** valor do certificado, o qual copiou a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eff45-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="eff45-186">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="eff45-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="eff45-187">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="eff45-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eff45-188">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="eff45-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eff45-189">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eff45-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eff45-190">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eff45-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="eff45-191">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eff45-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="eff45-193">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="eff45-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff45-194">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="eff45-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eff45-196">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="eff45-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eff45-198">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="eff45-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eff45-200">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="eff45-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eff45-202">a.</span><span class="sxs-lookup"><span data-stu-id="eff45-202">a.</span></span> <span data-ttu-id="eff45-203">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eff45-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eff45-204">b.</span><span class="sxs-lookup"><span data-stu-id="eff45-204">b.</span></span> <span data-ttu-id="eff45-205">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eff45-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eff45-206">c.</span><span class="sxs-lookup"><span data-stu-id="eff45-206">c.</span></span> <span data-ttu-id="eff45-207">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="eff45-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eff45-208">d.</span><span class="sxs-lookup"><span data-stu-id="eff45-208">d.</span></span> <span data-ttu-id="eff45-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="eff45-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="eff45-210">Criar um utilizador de teste ITRP</span><span class="sxs-lookup"><span data-stu-id="eff45-210">Creating an ITRP test user</span></span>

<span data-ttu-id="eff45-211">tooenable do Azure AD os utilizadores toolog no tooITRP, estes têm de ser aprovisionados na tooITRP.</span><span class="sxs-lookup"><span data-stu-id="eff45-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="eff45-212">No caso de Olá da ITRP, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="eff45-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="eff45-213">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="eff45-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff45-214">Inicie sessão no tooyour **ITRP** inquilino.</span><span class="sxs-lookup"><span data-stu-id="eff45-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="eff45-215">Na barra de ferramentas Olá na parte superior do Olá, clique em **registos**.</span><span class="sxs-lookup"><span data-stu-id="eff45-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="eff45-216">![Administração](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="eff45-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="eff45-217">No menu de pop-up de Olá, selecione **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="eff45-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="eff45-218">![As pessoas](./media/active-directory-saas-itrp-tutorial/ic775587.png "pessoas")</span><span class="sxs-lookup"><span data-stu-id="eff45-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="eff45-219">Clique em **Adicionar nova pessoa** ("+").</span><span class="sxs-lookup"><span data-stu-id="eff45-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="eff45-220">![Administração](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="eff45-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="eff45-221">Na caixa de diálogo de adicionar nova pessoa Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="eff45-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="eff45-222">![Utilizador](./media/active-directory-saas-itrp-tutorial/ic775577.png "utilizador")</span><span class="sxs-lookup"><span data-stu-id="eff45-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="eff45-223">a.</span><span class="sxs-lookup"><span data-stu-id="eff45-223">a.</span></span> <span data-ttu-id="eff45-224">Olá tipo **nome**, **E-Mail** de uma conta válida do AAD pretende tooprovision.</span><span class="sxs-lookup"><span data-stu-id="eff45-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="eff45-225">b.</span><span class="sxs-lookup"><span data-stu-id="eff45-225">b.</span></span> <span data-ttu-id="eff45-226">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="eff45-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="eff45-227">Pode utilizar quaisquer outras ITRP utilizador conta criação ferramentas ou APIs fornecidas pelo ITRP tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="eff45-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eff45-228">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eff45-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eff45-229">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooITRP.</span><span class="sxs-lookup"><span data-stu-id="eff45-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="eff45-231">**tooassign Britta Simon tooITRP, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="eff45-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="eff45-232">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="eff45-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="eff45-234">Na lista de aplicações de Olá, selecione **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="eff45-234">In hello applications list, select **ITRP**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="eff45-236">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="eff45-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="eff45-238">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="eff45-238">Click **Add** button.</span></span> <span data-ttu-id="eff45-239">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff45-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="eff45-241">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="eff45-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eff45-242">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff45-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eff45-243">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eff45-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eff45-244">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="eff45-244">Testing single sign-on</span></span>

<span data-ttu-id="eff45-245">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="eff45-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eff45-246">Ao clicar Olá ITRP na peça de mosaico Olá painel de acesso, pode ser obtido a aplicação de ITRP tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="eff45-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="eff45-247">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eff45-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eff45-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="eff45-248">Additional resources</span></span>

* [<span data-ttu-id="eff45-249">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eff45-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eff45-250">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eff45-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

