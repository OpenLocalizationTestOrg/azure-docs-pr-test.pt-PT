---
title: "Tutorial: Integração do Azure Active Directory com Freshservice | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="3a45d-103">Tutorial: Integração do Azure Active Directory com Freshservice</span><span class="sxs-lookup"><span data-stu-id="3a45d-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="3a45d-104">Neste tutorial, saiba como toointegrate Freshservice com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a45d-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a45d-105">Integrar Freshservice com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="3a45d-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3a45d-106">Pode controlar no Azure AD que tenha acesso tooFreshservice</span><span class="sxs-lookup"><span data-stu-id="3a45d-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="3a45d-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooFreshservice (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a45d-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a45d-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3a45d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3a45d-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a45d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a45d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3a45d-110">Prerequisites</span></span>

<span data-ttu-id="3a45d-111">integração do Azure AD com Freshservice tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3a45d-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="3a45d-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a45d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a45d-113">Um Freshservice início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="3a45d-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a45d-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3a45d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a45d-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3a45d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a45d-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3a45d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a45d-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a45d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a45d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3a45d-118">Scenario description</span></span>
<span data-ttu-id="3a45d-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3a45d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a45d-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="3a45d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a45d-121">Adicionar Freshservice da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="3a45d-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="3a45d-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="3a45d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="3a45d-123">Adicionar Freshservice da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="3a45d-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="3a45d-124">tooconfigure Olá integração de Freshservice com o Azure AD, é necessário tooadd Freshservice Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="3a45d-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3a45d-125">**tooadd Freshservice da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3a45d-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a45d-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="3a45d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a45d-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3a45d-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="3a45d-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3a45d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="3a45d-133">Na caixa de pesquisa de Olá, escreva **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-133">In hello search box, type **Freshservice**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="3a45d-135">No painel de resultados de Olá, selecione **Freshservice**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="3a45d-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a45d-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="3a45d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a45d-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Freshservice com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3a45d-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a45d-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Freshservice é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a45d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="3a45d-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Freshservice tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3a45d-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="3a45d-141">No Freshservice, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="3a45d-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3a45d-142">tooconfigure e teste do Azure AD-início de sessão único com Freshservice, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="3a45d-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3a45d-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="3a45d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3a45d-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a45d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a45d-145">**[Criar um utilizador de teste Freshservice](#creating-a-freshservice-test-user)**  -toohave um homólogo de Britta Simon no Freshservice é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="3a45d-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a45d-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="3a45d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a45d-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="3a45d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a45d-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="3a45d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a45d-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Freshservice.</span><span class="sxs-lookup"><span data-stu-id="3a45d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="3a45d-150">**tooconfigure do Azure AD-início de sessão único com Freshservice, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3a45d-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a45d-151">No Olá portal do Azure, no Olá **Freshservice** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="3a45d-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="3a45d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="3a45d-155">No Olá **Freshservice domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3a45d-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="3a45d-157">a.</span><span class="sxs-lookup"><span data-stu-id="3a45d-157">a.</span></span> <span data-ttu-id="3a45d-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="3a45d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="3a45d-159">b.</span><span class="sxs-lookup"><span data-stu-id="3a45d-159">b.</span></span> <span data-ttu-id="3a45d-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="3a45d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3a45d-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="3a45d-161">These values are not real.</span></span> <span data-ttu-id="3a45d-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="3a45d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3a45d-163">Contacte [equipa de suporte de cliente Freshservice](https://support.freshservice.com/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="3a45d-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="3a45d-164">No Olá **certificado de assinatura de SAML** secção, copie **THUMBPRINT** valor do certificado.</span><span class="sxs-lookup"><span data-stu-id="3a45d-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="3a45d-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="3a45d-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a45d-168">No Olá **Freshservice configuração** secção, clique em **configurar Freshservice** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="3a45d-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3a45d-169">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="3a45d-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="3a45d-171">Numa janela do browser web diferente, inicie sessão no site da empresa tooyour Freshservice como administrador.</span><span class="sxs-lookup"><span data-stu-id="3a45d-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="3a45d-172">No menu de Olá na parte superior do Olá, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="3a45d-173">![Administração](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="3a45d-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="3a45d-174">No Olá **Portal cliente**, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="3a45d-175">![Segurança](./media/active-directory-saas-freshservice-tutorial/ic790815.png "segurança")</span><span class="sxs-lookup"><span data-stu-id="3a45d-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="3a45d-176">No Olá **segurança** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3a45d-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3a45d-177">![Início de sessão único](./media/active-directory-saas-freshservice-tutorial/ic790816.png "início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="3a45d-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="3a45d-178">a.</span><span class="sxs-lookup"><span data-stu-id="3a45d-178">a.</span></span> <span data-ttu-id="3a45d-179">Comutador **início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="3a45d-180">b.</span><span class="sxs-lookup"><span data-stu-id="3a45d-180">b.</span></span> <span data-ttu-id="3a45d-181">Selecione **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="3a45d-182">c.</span><span class="sxs-lookup"><span data-stu-id="3a45d-182">c.</span></span> <span data-ttu-id="3a45d-183">No Olá **URL de início de sessão SAML** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a45d-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a45d-184">d.</span><span class="sxs-lookup"><span data-stu-id="3a45d-184">d.</span></span> <span data-ttu-id="3a45d-185">No Olá **URL de fim de sessão** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a45d-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a45d-186">e.</span><span class="sxs-lookup"><span data-stu-id="3a45d-186">e.</span></span> <span data-ttu-id="3a45d-187">No **impressão digital do certificado de segurança** caixa de texto, colar Olá **THUMBPRINT** valor do certificado que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a45d-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3a45d-188">f.</span><span class="sxs-lookup"><span data-stu-id="3a45d-188">f.</span></span> <span data-ttu-id="3a45d-189">Clique em **guardar**</span><span class="sxs-lookup"><span data-stu-id="3a45d-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="3a45d-190">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="3a45d-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3a45d-191">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="3a45d-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3a45d-192">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a45d-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a45d-193">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a45d-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a45d-194">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a45d-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="3a45d-196">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3a45d-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a45d-197">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="3a45d-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a45d-199">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a45d-201">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="3a45d-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a45d-203">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3a45d-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a45d-205">a.</span><span class="sxs-lookup"><span data-stu-id="3a45d-205">a.</span></span> <span data-ttu-id="3a45d-206">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a45d-207">b.</span><span class="sxs-lookup"><span data-stu-id="3a45d-207">b.</span></span> <span data-ttu-id="3a45d-208">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a45d-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a45d-209">c.</span><span class="sxs-lookup"><span data-stu-id="3a45d-209">c.</span></span> <span data-ttu-id="3a45d-210">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3a45d-211">d.</span><span class="sxs-lookup"><span data-stu-id="3a45d-211">d.</span></span> <span data-ttu-id="3a45d-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="3a45d-213">Criar um utilizador de teste Freshservice</span><span class="sxs-lookup"><span data-stu-id="3a45d-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="3a45d-214">tooenable do Azure AD os utilizadores toolog no tooFreshService, estes têm de ser aprovisionados para FreshService.</span><span class="sxs-lookup"><span data-stu-id="3a45d-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="3a45d-215">No caso de Olá da FreshService, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="3a45d-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="3a45d-216">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3a45d-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a45d-217">Inicie sessão no tooyour **FreshService** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="3a45d-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="3a45d-218">No menu de Olá na parte superior do Olá, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="3a45d-219">![Administração](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="3a45d-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="3a45d-220">No Olá **gestão de utilizadores** secção, clique em **autores de pedido**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="3a45d-221">![Autores de pedido](./media/active-directory-saas-freshservice-tutorial/ic790818.png "autores de pedido")</span><span class="sxs-lookup"><span data-stu-id="3a45d-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="3a45d-222">Clique em **novo solicitador**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="3a45d-223">![Autores de pedido de nova](./media/active-directory-saas-freshservice-tutorial/ic790819.png "autores de pedido de novo")</span><span class="sxs-lookup"><span data-stu-id="3a45d-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="3a45d-224">No Olá **novo solicitador** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3a45d-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3a45d-225">![Novo solicitador](./media/active-directory-saas-freshservice-tutorial/ic790820.png "novo solicitador")</span><span class="sxs-lookup"><span data-stu-id="3a45d-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="3a45d-226">a.</span><span class="sxs-lookup"><span data-stu-id="3a45d-226">a.</span></span> <span data-ttu-id="3a45d-227">Introduza Olá **nome próprio** e **E-Mail** atributos de uma conta válida do Azure Active Directory que pretende tooprovision Olá relacionadas com caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="3a45d-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="3a45d-228">b.</span><span class="sxs-lookup"><span data-stu-id="3a45d-228">b.</span></span> <span data-ttu-id="3a45d-229">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="3a45d-230">titular de conta do Azure Active Directory Olá obtém uma mensagem de e-mail, incluindo uma conta de Olá tooconfirm ligação antes de ficar ativo</span><span class="sxs-lookup"><span data-stu-id="3a45d-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="3a45d-231">Pode utilizar quaisquer outras FreshService utilizador conta criação ferramentas ou APIs fornecidas pelo FreshService tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="3a45d-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Atribua o utilizador][200] 

<span data-ttu-id="3a45d-233">**tooassign Britta Simon tooFreshservice, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3a45d-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="3a45d-234">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="3a45d-236">Na lista de aplicações de Olá, selecione **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-236">In hello applications list, select **Freshservice**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="3a45d-238">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3a45d-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="3a45d-240">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="3a45d-240">Click **Add** button.</span></span> <span data-ttu-id="3a45d-241">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3a45d-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="3a45d-243">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="3a45d-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3a45d-244">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3a45d-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a45d-245">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3a45d-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a45d-246">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="3a45d-246">Testing single sign-on</span></span>

<span data-ttu-id="3a45d-247">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3a45d-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3a45d-248">Ao clicar em mosaico de Freshservice Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Freshservice aplicação.</span><span class="sxs-lookup"><span data-stu-id="3a45d-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a45d-249">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3a45d-249">Additional resources</span></span>

* [<span data-ttu-id="3a45d-250">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a45d-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a45d-251">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a45d-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

