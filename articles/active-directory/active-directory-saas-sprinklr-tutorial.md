---
title: "Tutorial: Integração do Azure Active Directory com Sprinklr | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="512c0-103">Tutorial: Integração do Azure Active Directory com Sprinklr</span><span class="sxs-lookup"><span data-stu-id="512c0-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="512c0-104">Neste tutorial, saiba como toointegrate Sprinklr com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="512c0-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="512c0-105">Integrar Sprinklr com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="512c0-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="512c0-106">Pode controlar no Azure AD que tenha acesso tooSprinklr</span><span class="sxs-lookup"><span data-stu-id="512c0-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="512c0-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSprinklr (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="512c0-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="512c0-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="512c0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="512c0-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="512c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="512c0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="512c0-110">Prerequisites</span></span>

<span data-ttu-id="512c0-111">integração do Azure AD com Sprinklr tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="512c0-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="512c0-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="512c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="512c0-113">Um Sprinklr início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="512c0-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="512c0-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="512c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="512c0-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="512c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="512c0-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="512c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="512c0-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="512c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="512c0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="512c0-118">Scenario description</span></span>
<span data-ttu-id="512c0-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="512c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="512c0-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="512c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="512c0-121">Adicionar Sprinklr da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="512c0-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="512c0-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="512c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="512c0-123">Adicionar Sprinklr da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="512c0-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="512c0-124">tooconfigure Olá integração de Sprinklr com o Azure AD, é necessário tooadd Sprinklr Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="512c0-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="512c0-125">**tooadd Sprinklr da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="512c0-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="512c0-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="512c0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="512c0-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="512c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="512c0-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="512c0-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="512c0-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="512c0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="512c0-133">Na caixa de pesquisa de Olá, escreva **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="512c0-133">In hello search box, type **Sprinklr**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="512c0-135">No painel de resultados de Olá, selecione **Sprinklr**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="512c0-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="512c0-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="512c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="512c0-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Sprinklr com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="512c0-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="512c0-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Sprinklr é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="512c0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="512c0-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Sprinklr tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="512c0-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="512c0-141">No Sprinklr, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="512c0-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="512c0-142">tooconfigure e teste do Azure AD-início de sessão único com Sprinklr, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="512c0-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="512c0-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="512c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="512c0-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="512c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="512c0-145">**[Criar um utilizador de teste Sprinklr](#creating-a-sprinklr-test-user)**  -toohave um homólogo de Britta Simon no Sprinklr é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="512c0-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="512c0-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="512c0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="512c0-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="512c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="512c0-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="512c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="512c0-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Sprinklr.</span><span class="sxs-lookup"><span data-stu-id="512c0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="512c0-150">**tooconfigure do Azure AD-início de sessão único com Sprinklr, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="512c0-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="512c0-151">No Olá portal do Azure, no Olá **Sprinklr** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="512c0-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="512c0-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="512c0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="512c0-155">No Olá **Sprinklr domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="512c0-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="512c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="512c0-157">a.</span></span> <span data-ttu-id="512c0-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="512c0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="512c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="512c0-159">b.</span></span> <span data-ttu-id="512c0-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="512c0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="512c0-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="512c0-161">These values are not real.</span></span> <span data-ttu-id="512c0-162">Atualize o valor de Olá com Olá real URL de início de sessão e identificador.</span><span class="sxs-lookup"><span data-stu-id="512c0-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="512c0-163">Contacte [equipa de suporte de cliente Sprinklr](https://www.sprinklr.com/contact-us/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="512c0-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="512c0-164">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="512c0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="512c0-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="512c0-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="512c0-168">No Olá **Sprinklr configuração** secção, clique em **configurar Sprinklr** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="512c0-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="512c0-169">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="512c0-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="512c0-170">Numa janela do browser web diferente, inicie sessão no site da empresa tooyour Sprinklr como administrador.</span><span class="sxs-lookup"><span data-stu-id="512c0-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="512c0-171">Aceda demasiado**administração \> definições**.</span><span class="sxs-lookup"><span data-stu-id="512c0-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="512c0-172">![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "administração")</span><span class="sxs-lookup"><span data-stu-id="512c0-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="512c0-173">Aceda demasiado**gerir parceiro \> início de sessão único** na partir do painel esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="512c0-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="512c0-174">![Gerir parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "gerir parceiro")</span><span class="sxs-lookup"><span data-stu-id="512c0-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="512c0-175">Clique em **+ adicionar inícios de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="512c0-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="512c0-176">![Único inícios de sessão](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "único inícios de sessão")</span><span class="sxs-lookup"><span data-stu-id="512c0-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="512c0-177">No Olá **início de sessão único** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="512c0-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="512c0-178">![Único inícios de sessão](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "único inícios de sessão")</span><span class="sxs-lookup"><span data-stu-id="512c0-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="512c0-179">a.</span><span class="sxs-lookup"><span data-stu-id="512c0-179">a.</span></span> <span data-ttu-id="512c0-180">No Olá **nome** caixa de texto, escreva um nome para a sua configuração (por exemplo: *WAADSSOTest*).</span><span class="sxs-lookup"><span data-stu-id="512c0-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="512c0-181">b.</span><span class="sxs-lookup"><span data-stu-id="512c0-181">b.</span></span> <span data-ttu-id="512c0-182">Selecione **ativada**.</span><span class="sxs-lookup"><span data-stu-id="512c0-182">Select **Enabled**.</span></span>

    <span data-ttu-id="512c0-183">c.</span><span class="sxs-lookup"><span data-stu-id="512c0-183">c.</span></span> <span data-ttu-id="512c0-184">Selecione **utilizar o novo certificado de SSO**.</span><span class="sxs-lookup"><span data-stu-id="512c0-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="512c0-185">e.</span><span class="sxs-lookup"><span data-stu-id="512c0-185">e.</span></span> <span data-ttu-id="512c0-186">Abra o certificado codificado base-64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="512c0-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="512c0-187">f.</span><span class="sxs-lookup"><span data-stu-id="512c0-187">f.</span></span> <span data-ttu-id="512c0-188">Olá colar **ID de entidade de SAML** valor que copiou do Portal do Azure para Olá **Id de entidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="512c0-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="512c0-189">g.</span><span class="sxs-lookup"><span data-stu-id="512c0-189">g.</span></span> <span data-ttu-id="512c0-190">Olá colar **único início de sessão no URL do serviço SAML** valor que copiou do Portal do Azure para Olá **URL de início de sessão do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="512c0-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="512c0-191">h.</span><span class="sxs-lookup"><span data-stu-id="512c0-191">h.</span></span> <span data-ttu-id="512c0-192">Olá colar **Sign-Out URL** valor que copiou do Portal do Azure para Olá **URL de fim de sessão do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="512c0-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="512c0-193">posso.</span><span class="sxs-lookup"><span data-stu-id="512c0-193">i.</span></span> <span data-ttu-id="512c0-194">Como **tipo de ID de utilizador de SAML**, selecione **asserção contém utilizador "nome de utilizador do s sprinklr.com**.</span><span class="sxs-lookup"><span data-stu-id="512c0-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="512c0-195">j.</span><span class="sxs-lookup"><span data-stu-id="512c0-195">j.</span></span> <span data-ttu-id="512c0-196">Como **localização de ID de utilizador de SAML**, selecione **ID de utilizador está no elemento de identificador de nome de Olá do Olá instrução requerente**.</span><span class="sxs-lookup"><span data-stu-id="512c0-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="512c0-197">k.</span><span class="sxs-lookup"><span data-stu-id="512c0-197">k.</span></span> <span data-ttu-id="512c0-198">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="512c0-198">Click **Save**.</span></span>
       
    <span data-ttu-id="512c0-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="512c0-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="512c0-200">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="512c0-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="512c0-201">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="512c0-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="512c0-202">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="512c0-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="512c0-203">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="512c0-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="512c0-204">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="512c0-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="512c0-206">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="512c0-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="512c0-207">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="512c0-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="512c0-209">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="512c0-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="512c0-211">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="512c0-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="512c0-213">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="512c0-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="512c0-215">a.</span><span class="sxs-lookup"><span data-stu-id="512c0-215">a.</span></span> <span data-ttu-id="512c0-216">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="512c0-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="512c0-217">b.</span><span class="sxs-lookup"><span data-stu-id="512c0-217">b.</span></span> <span data-ttu-id="512c0-218">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="512c0-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="512c0-219">c.</span><span class="sxs-lookup"><span data-stu-id="512c0-219">c.</span></span> <span data-ttu-id="512c0-220">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="512c0-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="512c0-221">d.</span><span class="sxs-lookup"><span data-stu-id="512c0-221">d.</span></span> <span data-ttu-id="512c0-222">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="512c0-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="512c0-223">Criar um utilizador de teste Sprinklr</span><span class="sxs-lookup"><span data-stu-id="512c0-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="512c0-224">Inicie sessão no tooyour Sprinklr site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="512c0-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="512c0-225">Aceda demasiado**administração \> definições**.</span><span class="sxs-lookup"><span data-stu-id="512c0-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="512c0-226">![Administração](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "administração")</span><span class="sxs-lookup"><span data-stu-id="512c0-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="512c0-227">Aceda demasiado**cliente gerir \> utilizadores** a partir do painel esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="512c0-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="512c0-228">![Definições](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "definições")</span><span class="sxs-lookup"><span data-stu-id="512c0-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="512c0-229">Clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="512c0-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="512c0-230">![Definições](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "definições")</span><span class="sxs-lookup"><span data-stu-id="512c0-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="512c0-231">No Olá **Editar utilizador** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="512c0-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="512c0-232">![Editar utilizador](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Editar utilizador")</span><span class="sxs-lookup"><span data-stu-id="512c0-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="512c0-233">a.</span><span class="sxs-lookup"><span data-stu-id="512c0-233">a.</span></span> <span data-ttu-id="512c0-234">No Olá **E-Mail**, **nome próprio** e **Apelido** caixas de texto, informações de tipo de Olá de uma conta de utilizador do Azure AD que pretende tooprovision.</span><span class="sxs-lookup"><span data-stu-id="512c0-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="512c0-235">b.</span><span class="sxs-lookup"><span data-stu-id="512c0-235">b.</span></span> <span data-ttu-id="512c0-236">Selecione **desativado de palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="512c0-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="512c0-237">c.</span><span class="sxs-lookup"><span data-stu-id="512c0-237">c.</span></span> <span data-ttu-id="512c0-238">Selecione **idioma**.</span><span class="sxs-lookup"><span data-stu-id="512c0-238">Select **Language**.</span></span>

    <span data-ttu-id="512c0-239">d.</span><span class="sxs-lookup"><span data-stu-id="512c0-239">d.</span></span> <span data-ttu-id="512c0-240">Selecione **tipo de utilizador**.</span><span class="sxs-lookup"><span data-stu-id="512c0-240">Select **User Type**.</span></span>

    <span data-ttu-id="512c0-241">e.</span><span class="sxs-lookup"><span data-stu-id="512c0-241">e.</span></span> <span data-ttu-id="512c0-242">Clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="512c0-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="512c0-243">**Palavra-passe desativado** tem de ser selecionado tooenable toolog um utilizador no através de um fornecedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="512c0-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="512c0-244">Aceda demasiado**função**e, em seguida, executar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="512c0-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="512c0-245">![Funções do parceiro](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "funções do parceiro")</span><span class="sxs-lookup"><span data-stu-id="512c0-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="512c0-246">a.</span><span class="sxs-lookup"><span data-stu-id="512c0-246">a.</span></span> <span data-ttu-id="512c0-247">De Olá **Global** lista, selecione **todos os\_permissões**.</span><span class="sxs-lookup"><span data-stu-id="512c0-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="512c0-248">b.</span><span class="sxs-lookup"><span data-stu-id="512c0-248">b.</span></span> <span data-ttu-id="512c0-249">Clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="512c0-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="512c0-250">Pode utilizar quaisquer outras Sprinklr utilizador conta criação ferramentas ou APIs fornecidas pelo Sprinklr tooprovision contas de utilizador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="512c0-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="512c0-251">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="512c0-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="512c0-252">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSprinklr.</span><span class="sxs-lookup"><span data-stu-id="512c0-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="512c0-254">**tooassign Britta Simon tooSprinklr, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="512c0-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="512c0-255">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="512c0-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="512c0-257">Na lista de aplicações de Olá, selecione **Sprinklr**.</span><span class="sxs-lookup"><span data-stu-id="512c0-257">In hello applications list, select **Sprinklr**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="512c0-259">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="512c0-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="512c0-261">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="512c0-261">Click **Add** button.</span></span> <span data-ttu-id="512c0-262">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="512c0-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="512c0-264">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="512c0-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="512c0-265">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="512c0-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="512c0-266">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="512c0-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="512c0-267">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="512c0-267">Testing single sign-on</span></span>

<span data-ttu-id="512c0-268">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="512c0-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="512c0-269">Ao clicar em mosaico de Sprinklr Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Sprinklr aplicação para obter mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="512c0-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="512c0-270">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="512c0-270">Additional resources</span></span>

* [<span data-ttu-id="512c0-271">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="512c0-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="512c0-272">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="512c0-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

