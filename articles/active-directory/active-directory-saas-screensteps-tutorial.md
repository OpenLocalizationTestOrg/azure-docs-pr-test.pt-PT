---
title: "Tutorial: Integração do Azure Active Directory com ScreenSteps | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="2e8c0-103">Tutorial: Integração do Azure Active Directory com ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="2e8c0-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="2e8c0-104">Neste tutorial, saiba como toointegrate ScreenSteps com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e8c0-105">Integrar ScreenSteps com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2e8c0-106">Pode controlar no Azure AD que tenha acesso tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="2e8c0-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooScreenSteps (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2e8c0-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="2e8c0-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e8c0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2e8c0-110">Prerequisites</span></span>

<span data-ttu-id="2e8c0-111">integração do Azure AD com ScreenSteps tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="2e8c0-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e8c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e8c0-113">Um ScreenSteps-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="2e8c0-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e8c0-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e8c0-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e8c0-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2e8c0-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e8c0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2e8c0-118">Scenario description</span></span>
<span data-ttu-id="2e8c0-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e8c0-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e8c0-121">Adicionar ScreenSteps da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="2e8c0-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="2e8c0-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="2e8c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="2e8c0-123">Adicionar ScreenSteps da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="2e8c0-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="2e8c0-124">tooconfigure Olá integração de ScreenSteps com o Azure AD, é necessário tooadd ScreenSteps Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e8c0-125">**tooadd ScreenSteps da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="2e8c0-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e8c0-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="2e8c0-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2e8c0-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="2e8c0-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="2e8c0-133">Na caixa de pesquisa de Olá, escreva **ScreenSteps**, selecione **ScreenSteps** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ScreenSteps na lista de resultados de Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2e8c0-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="2e8c0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2e8c0-136">Nesta secção, configure e teste do Azure AD-início de sessão único com ScreenSteps com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2e8c0-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e8c0-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ScreenSteps é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="2e8c0-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ScreenSteps tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="2e8c0-139">No ScreenSteps, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2e8c0-140">tooconfigure e teste do Azure AD-início de sessão único com ScreenSteps, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2e8c0-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2e8c0-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e8c0-143">**[Criar um utilizador de teste ScreenSteps](#create-a-screensteps-test-user)**  -toohave um homólogo de Britta Simon no ScreenSteps é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2e8c0-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e8c0-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2e8c0-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="2e8c0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2e8c0-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="2e8c0-148">**tooconfigure do Azure AD-início de sessão único com ScreenSteps, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="2e8c0-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e8c0-149">No Olá portal do Azure, no Olá **ScreenSteps** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="2e8c0-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="2e8c0-153">No Olá **ScreenSteps domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![Domínio ScreenSteps e os URLs únicos de informações de início de sessão](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="2e8c0-155">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="2e8c0-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2e8c0-156">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-156">This value is not real.</span></span> <span data-ttu-id="2e8c0-157">Atualizar este valor com Olá real início de sessão no URL, que é explicado posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="2e8c0-158">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="2e8c0-160">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-160">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e8c0-162">No Olá **ScreenSteps configuração** secção, clique em **configurar ScreenSteps** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2e8c0-163">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="2e8c0-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="2e8c0-165">Numa janela do browser web diferente, inicie sessão no site da sua empresa ScreenSteps como administrador.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="2e8c0-166">Clique em **definições da conta**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="2e8c0-167">![Gestão de contas](./media/active-directory-saas-screensteps-tutorial/ic778523.png "gestão de contas")</span><span class="sxs-lookup"><span data-stu-id="2e8c0-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="2e8c0-168">Clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="2e8c0-169">![Autenticação remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "autenticação remota")</span><span class="sxs-lookup"><span data-stu-id="2e8c0-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="2e8c0-170">Clique em **criar o ponto final de início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="2e8c0-171">![Autenticação remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "autenticação remota")</span><span class="sxs-lookup"><span data-stu-id="2e8c0-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="2e8c0-172">No Olá **ponto final de início de sessão único criar** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="2e8c0-173">![Criar um ponto final de autenticação](./media/active-directory-saas-screensteps-tutorial/ic778526.png "criar um ponto final de autenticação")</span><span class="sxs-lookup"><span data-stu-id="2e8c0-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="2e8c0-174">a.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-174">a.</span></span> <span data-ttu-id="2e8c0-175">No Olá **título** caixa de texto, escreva um título.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="2e8c0-176">b.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-176">b.</span></span> <span data-ttu-id="2e8c0-177">De Olá **modo** lista, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="2e8c0-178">c.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-178">c.</span></span> <span data-ttu-id="2e8c0-179">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-179">Click **Create**.</span></span>

12. <span data-ttu-id="2e8c0-180">**Editar** Olá novo ponto final.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="2e8c0-181">![Editar endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "editar ponto final")</span><span class="sxs-lookup"><span data-stu-id="2e8c0-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="2e8c0-182">No Olá **ponto final de início de sessão único editar** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="2e8c0-183">![Ponto final de autenticação remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "ponto final de autenticação remota")</span><span class="sxs-lookup"><span data-stu-id="2e8c0-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="2e8c0-184">a.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-184">a.</span></span> <span data-ttu-id="2e8c0-185">Clique em **carregamento novo ficheiro de certificado de SAML**e, em seguida, carregue Olá certificado, o que transferiu a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="2e8c0-186">b.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-186">b.</span></span> <span data-ttu-id="2e8c0-187">Colar **único início de sessão no URL do serviço SAML** valor que copiou do Olá portal do Azure para Olá **URL de início de sessão remoto** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="2e8c0-188">c.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-188">c.</span></span> <span data-ttu-id="2e8c0-189">Colar **Sign-Out URL** valor que copiou do Olá portal do Azure para Olá **URL para terminar sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="2e8c0-190">d.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-190">d.</span></span> <span data-ttu-id="2e8c0-191">Selecione um **grupo** tooassign utilizadores toowhen terem sido aprovisionados.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="2e8c0-192">e.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-192">e.</span></span> <span data-ttu-id="2e8c0-193">Clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-193">Click **Update**.</span></span>

    <span data-ttu-id="2e8c0-194">f.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-194">f.</span></span> <span data-ttu-id="2e8c0-195">Olá cópia **SAML consumidor URL** toohello área de transferência e cole no toohello **URL de início de sessão** textbox em **ScreenSteps domínio e os URLs** secção.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="2e8c0-196">g.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-196">g.</span></span> <span data-ttu-id="2e8c0-197">Devolver toohello **ponto final de início de sessão único editar**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="2e8c0-198">h.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-198">h.</span></span> <span data-ttu-id="2e8c0-199">Clique em Olá **predefinir para conta** botão toouse este ponto final para todos os utilizadores que inicie sessão no ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="2e8c0-200">Em alternativa, pode clicar em Olá **adicionar tooSite** botão toouse este ponto final para sites específicos de **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="2e8c0-201">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="2e8c0-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2e8c0-202">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2e8c0-203">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2e8c0-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2e8c0-204">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e8c0-204">Create an Azure AD test user</span></span>

<span data-ttu-id="2e8c0-205">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="2e8c0-207">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="2e8c0-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e8c0-208">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2e8c0-210">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2e8c0-212">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2e8c0-214">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2e8c0-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2e8c0-216">a.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-216">a.</span></span> <span data-ttu-id="2e8c0-217">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e8c0-218">b.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-218">b.</span></span> <span data-ttu-id="2e8c0-219">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="2e8c0-220">c.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-220">c.</span></span> <span data-ttu-id="2e8c0-221">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="2e8c0-222">d.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-222">d.</span></span> <span data-ttu-id="2e8c0-223">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="2e8c0-224">Criar um utilizador de teste ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="2e8c0-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="2e8c0-225">Nesta secção, vai criar um utilizador chamado Britta Simon ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="2e8c0-226">Trabalhar com [equipa de suporte de cliente ScreenSteps](https://www.screensteps.com/contact) para adicionar utilizadores de Olá na plataforma de ScreenSteps Olá.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="2e8c0-227">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="2e8c0-228">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e8c0-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="2e8c0-229">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="2e8c0-231">**tooassign Britta Simon tooScreenSteps, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="2e8c0-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e8c0-232">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="2e8c0-234">Na lista de aplicações de Olá, selecione **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![ligação de ScreenSteps Olá na lista de aplicações de Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="2e8c0-236">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="2e8c0-238">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-238">Click **Add** button.</span></span> <span data-ttu-id="2e8c0-239">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="2e8c0-241">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2e8c0-242">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e8c0-243">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2e8c0-244">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="2e8c0-244">Test single sign-on</span></span>

<span data-ttu-id="2e8c0-245">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2e8c0-246">Ao clicar Olá ScreenSteps na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour ScreenSteps aplicação.</span><span class="sxs-lookup"><span data-stu-id="2e8c0-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="2e8c0-247">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2e8c0-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2e8c0-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2e8c0-248">Additional resources</span></span>

* [<span data-ttu-id="2e8c0-249">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e8c0-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e8c0-250">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2e8c0-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

