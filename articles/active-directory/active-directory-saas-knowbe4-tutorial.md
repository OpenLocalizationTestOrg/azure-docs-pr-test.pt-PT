---
title: "Tutorial: Integração do Azure Active Directory com formação de deteção de segurança KnowBe4 | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e formação de deteção de segurança KnowBe4."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 907fa814b82c9ffb2376f73470b746a37104c66e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4-security-awareness-training"></a><span data-ttu-id="9cf4c-103">Tutorial: Integração do Azure Active Directory com KnowBe4 segurança deteção formação</span><span class="sxs-lookup"><span data-stu-id="9cf4c-103">Tutorial: Azure Active Directory integration with KnowBe4 Security Awareness Training</span></span>

<span data-ttu-id="9cf4c-104">Neste tutorial, saiba como toointegrate KnowBe4 formação de deteção de segurança no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9cf4c-104">In this tutorial, you learn how toointegrate KnowBe4 Security Awareness Training with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cf4c-105">A integração de formação de deteção de segurança KnowBe4 com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="9cf4c-105">Integrating KnowBe4 Security Awareness Training with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9cf4c-106">Pode controlar no Azure AD que tenha acesso tooKnowBe4 segurança deteção formação</span><span class="sxs-lookup"><span data-stu-id="9cf4c-106">You can control in Azure AD who has access tooKnowBe4 Security Awareness Training</span></span>
- <span data-ttu-id="9cf4c-107">Pode ativar os seus utilizadores tooautomatically obter com sessão iniciada tooKnowBe4 formação de deteção de segurança (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf4c-107">You can enable your users tooautomatically get signed-on tooKnowBe4 Security Awareness Training (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cf4c-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9cf4c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9cf4c-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9cf4c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cf4c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9cf4c-110">Prerequisites</span></span>

<span data-ttu-id="9cf4c-111">integração do Azure AD com formação de deteção de segurança KnowBe4 tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9cf4c-111">tooconfigure Azure AD integration with KnowBe4 Security Awareness Training, you need hello following items:</span></span>

- <span data-ttu-id="9cf4c-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf4c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cf4c-113">Uma formação de deteção de segurança KnowBe4-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="9cf4c-113">A KnowBe4 Security Awareness Training single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cf4c-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cf4c-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9cf4c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cf4c-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cf4c-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9cf4c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cf4c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9cf4c-118">Scenario description</span></span>
<span data-ttu-id="9cf4c-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cf4c-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="9cf4c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cf4c-121">A adição de formação de deteção de segurança KnowBe4 de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="9cf4c-121">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
2. <span data-ttu-id="9cf4c-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="9cf4c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-knowbe4-security-awareness-training-from-hello-gallery"></a><span data-ttu-id="9cf4c-123">A adição de formação de deteção de segurança KnowBe4 de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="9cf4c-123">Adding KnowBe4 Security Awareness Training from hello gallery</span></span>
<span data-ttu-id="9cf4c-124">tooconfigure Olá integração de formação de deteção de segurança KnowBe4 com o Azure AD, é necessário tooadd formação de deteção de segurança KnowBe4 Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-124">tooconfigure hello integration of KnowBe4 Security Awareness Training into Azure AD, you need tooadd KnowBe4 Security Awareness Training from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9cf4c-125">**tooadd KnowBe4 formação de deteção de segurança da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9cf4c-125">**tooadd KnowBe4 Security Awareness Training from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf4c-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cf4c-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9cf4c-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="9cf4c-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="9cf4c-133">Na caixa de pesquisa de Olá, escreva **formação de deteção de segurança KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-133">In hello search box, type **KnowBe4 Security Awareness Training**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_search.png)

5. <span data-ttu-id="9cf4c-135">No painel de resultados de Olá, selecione **formação de deteção de segurança KnowBe4**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-135">In hello results panel, select **KnowBe4 Security Awareness Training**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cf4c-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="9cf4c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cf4c-138">Nesta secção, configure e teste do Azure AD-início de sessão único com formação de deteção de segurança de KnowBe4 com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9cf4c-138">In this section, you configure and test Azure AD single sign-on with KnowBe4 Security Awareness Training based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9cf4c-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na formação de deteção de segurança KnowBe4 é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in KnowBe4 Security Awareness Training is tooa user in Azure AD.</span></span> <span data-ttu-id="9cf4c-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na formação de deteção de segurança KnowBe4 tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-140">In other words, a link relationship between an Azure AD user and hello related user in KnowBe4 Security Awareness Training needs toobe established.</span></span>

<span data-ttu-id="9cf4c-141">No KnowBe4 formação de deteção de segurança, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-141">In KnowBe4 Security Awareness Training, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9cf4c-142">tooconfigure e teste do Azure AD-início de sessão único com KnowBe4 segurança deteção formação, é necessário Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9cf4c-142">tooconfigure and test Azure AD single sign-on with KnowBe4 Security Awareness Training, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9cf4c-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9cf4c-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cf4c-145">**[Criar um utilizador de teste de formação de deteção de segurança KnowBe4](#creating-a-knowbe4-security-awareness-training-test-user)**  -toohave um homólogo de Britta Simon na formação de deteção de segurança KnowBe4 é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-145">**[Creating a KnowBe4 Security Awareness Training test user](#creating-a-knowbe4-security-awareness-training-test-user)** - toohave a counterpart of Britta Simon in KnowBe4 Security Awareness Training that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cf4c-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cf4c-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cf4c-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9cf4c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cf4c-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de formação de deteção de segurança KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your KnowBe4 Security Awareness Training application.</span></span>

<span data-ttu-id="9cf4c-150">**tooconfigure do Azure AD-início de sessão único com KnowBe4 formação de deteção de segurança, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9cf4c-150">**tooconfigure Azure AD single sign-on with KnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf4c-151">No Olá portal do Azure, no Olá **formação de deteção de segurança KnowBe4** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-151">In hello Azure portal, on hello **KnowBe4 Security Awareness Training** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="9cf4c-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_samlbase.png)

3. <span data-ttu-id="9cf4c-155">No Olá **URLs e de domínio de formação de deteção de segurança KnowBe4** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9cf4c-155">On hello **KnowBe4 Security Awareness Training Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_url.png)

    <span data-ttu-id="9cf4c-157">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="9cf4c-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.KnowBe4.com/auth/saml/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9cf4c-158">o valor de Olá não é real.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-158">hello value is not real.</span></span> <span data-ttu-id="9cf4c-159">Atualização Olá valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9cf4c-160">Contacte [equipa de suporte de cliente de formação de deteção de segurança KnowBe4](mailto:support@KnowBe4.com) valor de Olá tooget.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-160">Contact [KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com) tooget hello value.</span></span> 
 

4. <span data-ttu-id="9cf4c-161">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (bruto)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_certificate.png) 

5. <span data-ttu-id="9cf4c-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cf4c-165">No Olá **configuração de formação de deteção de segurança KnowBe4** secção, clique em **configurar formação de deteção de segurança de KnowBe4** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-165">On hello **KnowBe4 Security Awareness Training Configuration** section, click **Configure KnowBe4 Security Awareness Training** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9cf4c-166">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9cf4c-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_configure.png) 

7. <span data-ttu-id="9cf4c-168">tooconfigure-início de sessão único em **formação de deteção de segurança KnowBe4** lado, terá de Olá toosend transferido **certificado (bruto)**, **Sign-Out URL, ID de entidade de SAML e SAML Single Sign-On URL do serviço** demasiado[equipa de suporte de cliente de formação de deteção de segurança KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="9cf4c-168">tooconfigure single sign-on on **KnowBe4 Security Awareness Training** side, you need toosend hello downloaded **Certificate (Raw)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[KnowBe4 Security Awareness Training Client support team](mailto:support@KnowBe4.com).</span></span>

> [!TIP]
> <span data-ttu-id="9cf4c-169">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="9cf4c-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9cf4c-170">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9cf4c-171">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cf4c-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cf4c-172">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf4c-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cf4c-173">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="9cf4c-175">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9cf4c-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf4c-176">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cf4c-178">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cf4c-180">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cf4c-182">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9cf4c-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-KnowBe4-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cf4c-184">a.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-184">a.</span></span> <span data-ttu-id="9cf4c-185">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cf4c-186">b.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-186">b.</span></span> <span data-ttu-id="9cf4c-187">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cf4c-188">c.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-188">c.</span></span> <span data-ttu-id="9cf4c-189">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9cf4c-190">d.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-190">d.</span></span> <span data-ttu-id="9cf4c-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-191">Click **Create**.</span></span>
 
### <a name="creating-a-knowbe4-security-awareness-training-test-user"></a><span data-ttu-id="9cf4c-192">Criar um utilizador de teste de formação de deteção de segurança KnowBe4</span><span class="sxs-lookup"><span data-stu-id="9cf4c-192">Creating a KnowBe4 Security Awareness Training test user</span></span>

<span data-ttu-id="9cf4c-193">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon na formação de deteção de segurança KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-193">hello objective of this section is toocreate a user called Britta Simon in KnowBe4 Security Awareness Training.</span></span> <span data-ttu-id="9cf4c-194">Formação de deteção de segurança KnowBe4 suportam o aprovisionamento de just-in-time, que é por predefinição ativada.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-194">KnowBe4 Security Awareness Training supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9cf4c-195">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-195">There is no action item for you in this section.</span></span> <span data-ttu-id="9cf4c-196">Um novo utilizador é criado durante uma tentativa tooaccess formação de deteção de segurança KnowBe4 se não existir ainda.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-196">A new user is created during an attempt tooaccess KnowBe4 Security Awareness Training if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="9cf4c-197">Se precisar de um utilizador de toocreate manualmente, terá de toocontact Olá [equipa de suporte de formação de deteção de segurança KnowBe4](mailto:support@KnowBe4.com).</span><span class="sxs-lookup"><span data-stu-id="9cf4c-197">If you need toocreate a user manually, you need toocontact hello [KnowBe4 Security Awareness Training support team](mailto:support@KnowBe4.com).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9cf4c-198">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9cf4c-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9cf4c-199">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooKnowBe4 segurança deteção formação.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKnowBe4 Security Awareness Training.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="9cf4c-201">**tooassign Britta Simon tooKnowBe4 formação de deteção de segurança, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9cf4c-201">**tooassign Britta Simon tooKnowBe4 Security Awareness Training, perform hello following steps:**</span></span>

1. <span data-ttu-id="9cf4c-202">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="9cf4c-204">Na lista de aplicações de Olá, selecione **formação de deteção de segurança KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-204">In hello applications list, select **KnowBe4 Security Awareness Training**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-KnowBe4-tutorial/tutorial_knowbe4sat_app.png) 

3. <span data-ttu-id="9cf4c-206">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="9cf4c-208">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-208">Click **Add** button.</span></span> <span data-ttu-id="9cf4c-209">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="9cf4c-211">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9cf4c-212">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cf4c-213">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cf4c-214">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9cf4c-214">Testing single sign-on</span></span>

<span data-ttu-id="9cf4c-215">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="9cf4c-216">Ao clicar em mosaico de formação de deteção de segurança KnowBe4 Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour aplicação KnowBe4 segurança deteção formação.</span><span class="sxs-lookup"><span data-stu-id="9cf4c-216">When you click hello KnowBe4 Security Awareness Training tile in hello Access Panel, you should get automatically signed-on tooyour KnowBe4 Security Awareness Training application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cf4c-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9cf4c-217">Additional resources</span></span>

* [<span data-ttu-id="9cf4c-218">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cf4c-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cf4c-219">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9cf4c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-KnowBe4-tutorial/tutorial_general_203.png

