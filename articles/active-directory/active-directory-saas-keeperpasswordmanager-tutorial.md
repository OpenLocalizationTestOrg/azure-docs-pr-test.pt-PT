---
title: "Tutorial: Integração do Azure Active Directory com o Gestor de palavras-passe Keeper & digitais Cofre | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o Gestor de palavras-passe Keeper & digitais cofre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="1c394-103">Tutorial: Integração do Azure Active Directory com o Gestor de palavras-passe Keeper & digitais Cofre</span><span class="sxs-lookup"><span data-stu-id="1c394-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="1c394-104">Neste tutorial, saiba como toointegrate Gestor de palavras-passe Keeper & digitais cofre com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1c394-104">In this tutorial, you learn how toointegrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1c394-105">Integrar o Gestor de palavras-passe Keeper & digitais cofre com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="1c394-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1c394-106">Pode controlar no Azure AD que tenha acesso tooKeeper Gestor de palavra-passe & digitais Cofre</span><span class="sxs-lookup"><span data-stu-id="1c394-106">You can control in Azure AD who has access tooKeeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="1c394-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooKeeper Gestor de palavra-passe & digitais cofre (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c394-107">You can enable your users tooautomatically get signed-on tooKeeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1c394-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1c394-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1c394-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1c394-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c394-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1c394-110">Prerequisites</span></span>

<span data-ttu-id="1c394-111">integração do Azure AD com o Gestor de palavras-passe Keeper & digitais cofre tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1c394-111">tooconfigure Azure AD integration with Keeper Password Manager & Digital Vault, you need hello following items:</span></span>

- <span data-ttu-id="1c394-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c394-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1c394-113">Um Gestor de palavras-passe Keeper & digitais cofre início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="1c394-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1c394-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1c394-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1c394-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1c394-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1c394-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1c394-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1c394-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1c394-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1c394-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1c394-118">Scenario description</span></span>
<span data-ttu-id="1c394-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1c394-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1c394-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="1c394-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1c394-121">Adicionar Gestor de palavras-passe Keeper & cofre Digital da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="1c394-121">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
2. <span data-ttu-id="1c394-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="1c394-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a><span data-ttu-id="1c394-123">Adicionar Gestor de palavras-passe Keeper & cofre Digital da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="1c394-123">Adding Keeper Password Manager & Digital Vault from hello gallery</span></span>
<span data-ttu-id="1c394-124">tooconfigure Olá integração do Gestor de palavras-passe Keeper & digitais cofre com o Azure AD, terá de tooadd Gestor de palavras-passe Keeper & digitais cofre Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="1c394-124">tooconfigure hello integration of Keeper Password Manager & Digital Vault into Azure AD, you need tooadd Keeper Password Manager & Digital Vault from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1c394-125">**tooadd Gestor de palavras-passe Keeper & digitais cofre a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1c394-125">**tooadd Keeper Password Manager & Digital Vault from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c394-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="1c394-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1c394-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1c394-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1c394-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="1c394-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="1c394-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c394-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="1c394-133">Na caixa de pesquisa de Olá, escreva **Gestor de palavras-passe Keeper & digitais cofre**.</span><span class="sxs-lookup"><span data-stu-id="1c394-133">In hello search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. <span data-ttu-id="1c394-135">No painel de resultados de Olá, selecione **Gestor de palavras-passe Keeper & digitais cofre**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="1c394-135">In hello results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1c394-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="1c394-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1c394-138">Nesta secção, configurar e testar o Azure AD-início de sessão único com o Gestor de palavras-passe Keeper & digitais cofre com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1c394-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1c394-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá no Gestor de palavras-passe Keeper & digitais Cofre é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c394-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Keeper Password Manager & Digital Vault is tooa user in Azure AD.</span></span> <span data-ttu-id="1c394-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no Gestor de palavras-passe Keeper & digitais cofre tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1c394-140">In other words, a link relationship between an Azure AD user and hello related user in Keeper Password Manager & Digital Vault needs toobe established.</span></span>

<span data-ttu-id="1c394-141">No Gestor de palavras-passe Keeper & digitais cofre, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="1c394-141">In Keeper Password Manager & Digital Vault, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1c394-142">tooconfigure e teste do Azure AD-início de sessão único com o Gestor de palavras-passe Keeper & digitais cofre, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1c394-142">tooconfigure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1c394-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="1c394-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1c394-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1c394-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1c394-145">**[Criar um utilizador de teste do Gestor de palavras-passe Keeper & digitais cofre](#creating-a-keeperpasswordmanager-test-user)**  -toohave um homólogo de Britta Simon no Gestor de palavras-passe Keeper & digitais cofre que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="1c394-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - toohave a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1c394-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="1c394-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1c394-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="1c394-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1c394-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="1c394-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1c394-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação do Gestor de palavras-passe Keeper & digitais cofre.</span><span class="sxs-lookup"><span data-stu-id="1c394-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="1c394-150">**tooconfigure do Azure AD-início de sessão único com o Gestor de palavras-passe Keeper & digitais cofre, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1c394-150">**tooconfigure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c394-151">No Olá portal do Azure, no Olá **Gestor de palavras-passe Keeper & digitais cofre** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="1c394-151">In hello Azure portal, on hello **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="1c394-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="1c394-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. <span data-ttu-id="1c394-155">No Olá **Gestor de palavras-passe Keeper & digitais de Cofre de domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="1c394-155">On hello **Keeper Password Manager & Digital Vault Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="1c394-157">a.</span><span class="sxs-lookup"><span data-stu-id="1c394-157">a.</span></span> <span data-ttu-id="1c394-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="1c394-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="1c394-159">b.</span><span class="sxs-lookup"><span data-stu-id="1c394-159">b.</span></span> <span data-ttu-id="1c394-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="1c394-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="1c394-161">c.</span><span class="sxs-lookup"><span data-stu-id="1c394-161">c.</span></span> <span data-ttu-id="1c394-162">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="1c394-162">In hello **Identifier** textbox, type a URL using hello following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1c394-163">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="1c394-163">These values are not real.</span></span> <span data-ttu-id="1c394-164">Atualize estes valores com o URL de resposta real Olá e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="1c394-164">Update these values with hello actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1c394-165">Contacte [equipa de suporte do Gestor de palavras-passe Keeper & digitais cofre cliente](https://keepersecurity.com/contact.html) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="1c394-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="1c394-166">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="1c394-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. <span data-ttu-id="1c394-168">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="1c394-168">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="1c394-170">No Olá **Gestor de palavras-passe Keeper & digitais cofre configuração** secção, clique em **configurar Gestor de palavras-passe Keeper & digitais cofre** tooopen **configurar início de sessão**janela.</span><span class="sxs-lookup"><span data-stu-id="1c394-170">On hello **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1c394-171">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="1c394-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. <span data-ttu-id="1c394-173">tooconfigure-início de sessão único em **Gestor de palavras-passe Keeper & digitais cofre configuração** lado, siga as diretrizes de Olá fornecidas durante a [Keeper guia de suporte](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span><span class="sxs-lookup"><span data-stu-id="1c394-173">tooconfigure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow hello guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)</span></span>

> [!TIP]
> <span data-ttu-id="1c394-174">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="1c394-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1c394-175">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="1c394-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1c394-176">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1c394-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1c394-177">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c394-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="1c394-178">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c394-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="1c394-180">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1c394-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c394-181">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="1c394-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1c394-183">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="1c394-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1c394-185">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="1c394-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1c394-187">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="1c394-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1c394-189">a.</span><span class="sxs-lookup"><span data-stu-id="1c394-189">a.</span></span> <span data-ttu-id="1c394-190">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1c394-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1c394-191">b.</span><span class="sxs-lookup"><span data-stu-id="1c394-191">b.</span></span> <span data-ttu-id="1c394-192">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1c394-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1c394-193">c.</span><span class="sxs-lookup"><span data-stu-id="1c394-193">c.</span></span> <span data-ttu-id="1c394-194">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="1c394-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1c394-195">d.</span><span class="sxs-lookup"><span data-stu-id="1c394-195">d.</span></span> <span data-ttu-id="1c394-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1c394-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="1c394-197">Criar um utilizador de teste do Gestor de palavras-passe Keeper & digitais Cofre</span><span class="sxs-lookup"><span data-stu-id="1c394-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="1c394-198">tooenable do Azure AD os utilizadores toolog tooKeeper Gestor de palavra-passe & digitais cofre, estes têm de ser aprovisionados no Gestor de palavras-passe Keeper & digitais cofre.</span><span class="sxs-lookup"><span data-stu-id="1c394-198">tooenable Azure AD users toolog in tooKeeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="1c394-199">Aplicação suporta apenas no tempo de aprovisionamento de utilizador e de utilizadores de autenticação serão criados na aplicação Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1c394-199">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="1c394-200">Pode contactar [Keeper suporte](https://keepersecurity.com/contact.html), se pretender que os utilizadores de toosetup manualmente.</span><span class="sxs-lookup"><span data-stu-id="1c394-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want toosetup users manually.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1c394-201">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c394-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1c394-202">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooKeeper Gestor de palavra-passe & digitais cofre.</span><span class="sxs-lookup"><span data-stu-id="1c394-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKeeper Password Manager & Digital Vault.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="1c394-204">**tooassign Britta Simon tooKeeper Gestor de palavra-passe & digitais cofre, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1c394-204">**tooassign Britta Simon tooKeeper Password Manager & Digital Vault, perform hello following steps:**</span></span>

1. <span data-ttu-id="1c394-205">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="1c394-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="1c394-207">Na lista de aplicações de Olá, selecione **Gestor de palavras-passe Keeper & digitais cofre**.</span><span class="sxs-lookup"><span data-stu-id="1c394-207">In hello applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. <span data-ttu-id="1c394-209">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1c394-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="1c394-211">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="1c394-211">Click **Add** button.</span></span> <span data-ttu-id="1c394-212">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c394-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="1c394-214">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="1c394-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1c394-215">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c394-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1c394-216">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1c394-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1c394-217">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="1c394-217">Testing single sign-on</span></span>

<span data-ttu-id="1c394-218">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="1c394-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1c394-219">Ao clicar Olá Gestor de palavras-passe Keeper & mosaico de cofre Digital no painel de acesso de Olá, deve obter a página de início de sessão da aplicação do Gestor de palavras-passe Keeper & digitais cofre.</span><span class="sxs-lookup"><span data-stu-id="1c394-219">When you click hello Keeper Password Manager & Digital Vault tile in hello Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="1c394-220">Após a autenticação com êxito, deve obter numa aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="1c394-220">Upon successful authentication, you should get into hello application.</span></span> <span data-ttu-id="1c394-221">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1c394-221">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1c394-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1c394-222">Additional resources</span></span>

* [<span data-ttu-id="1c394-223">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c394-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1c394-224">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1c394-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

