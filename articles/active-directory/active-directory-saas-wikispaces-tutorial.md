---
title: "Tutorial: Integração do Azure Active Directory com Wikispaces | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: eb5b72e60b415cb657b70ba530df731ae14b0425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="08a86-103">Tutorial: Integração do Azure Active Directory com Wikispaces</span><span class="sxs-lookup"><span data-stu-id="08a86-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="08a86-104">Neste tutorial, saiba como toointegrate Wikispaces com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="08a86-104">In this tutorial, you learn how toointegrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08a86-105">Integrar Wikispaces com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="08a86-105">Integrating Wikispaces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="08a86-106">Pode controlar no Azure AD que tenha acesso tooWikispaces</span><span class="sxs-lookup"><span data-stu-id="08a86-106">You can control in Azure AD who has access tooWikispaces</span></span>
- <span data-ttu-id="08a86-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooWikispaces (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08a86-107">You can enable your users tooautomatically get signed-on tooWikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08a86-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="08a86-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="08a86-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08a86-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08a86-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08a86-110">Prerequisites</span></span>

<span data-ttu-id="08a86-111">integração do Azure AD com Wikispaces tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="08a86-111">tooconfigure Azure AD integration with Wikispaces, you need hello following items:</span></span>

- <span data-ttu-id="08a86-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08a86-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08a86-113">Um Wikispaces-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="08a86-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08a86-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="08a86-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08a86-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="08a86-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08a86-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="08a86-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08a86-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08a86-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08a86-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="08a86-118">Scenario description</span></span>
<span data-ttu-id="08a86-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="08a86-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08a86-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="08a86-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08a86-121">Adicionar Wikispaces da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="08a86-121">Adding Wikispaces from hello gallery</span></span>
2. <span data-ttu-id="08a86-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="08a86-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-hello-gallery"></a><span data-ttu-id="08a86-123">Adicionar Wikispaces da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="08a86-123">Adding Wikispaces from hello gallery</span></span>
<span data-ttu-id="08a86-124">tooconfigure Olá integração de Wikispaces com o Azure AD, é necessário tooadd Wikispaces Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="08a86-124">tooconfigure hello integration of Wikispaces into Azure AD, you need tooadd Wikispaces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="08a86-125">**tooadd Wikispaces da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="08a86-125">**tooadd Wikispaces from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="08a86-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="08a86-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="08a86-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="08a86-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="08a86-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="08a86-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="08a86-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08a86-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="08a86-133">Na caixa de pesquisa de Olá, escreva **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="08a86-133">In hello search box, type **Wikispaces**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="08a86-135">No painel de resultados de Olá, selecione **Wikispaces**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="08a86-135">In hello results panel, select **Wikispaces**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="08a86-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="08a86-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="08a86-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Wikispaces com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="08a86-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="08a86-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Wikispaces é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08a86-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wikispaces is tooa user in Azure AD.</span></span> <span data-ttu-id="08a86-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Wikispaces tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="08a86-140">In other words, a link relationship between an Azure AD user and hello related user in Wikispaces needs toobe established.</span></span>

<span data-ttu-id="08a86-141">No Wikispaces, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="08a86-141">In Wikispaces, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="08a86-142">tooconfigure e teste do Azure AD-início de sessão único com Wikispaces, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="08a86-142">tooconfigure and test Azure AD single sign-on with Wikispaces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="08a86-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="08a86-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="08a86-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08a86-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08a86-145">**[Criar um utilizador de teste Wikispaces](#creating-a-wikispaces-test-user)**  -toohave um homólogo de Britta Simon no Wikispaces é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="08a86-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - toohave a counterpart of Britta Simon in Wikispaces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="08a86-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="08a86-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08a86-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="08a86-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="08a86-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="08a86-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="08a86-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="08a86-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="08a86-150">**tooconfigure do Azure AD-início de sessão único com Wikispaces, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="08a86-150">**tooconfigure Azure AD single sign-on with Wikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="08a86-151">No Olá portal do Azure, no Olá **Wikispaces** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="08a86-151">In hello Azure portal, on hello **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="08a86-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="08a86-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="08a86-155">No Olá **Wikispaces domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="08a86-155">On hello **Wikispaces Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="08a86-157">a.</span><span class="sxs-lookup"><span data-stu-id="08a86-157">a.</span></span> <span data-ttu-id="08a86-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="08a86-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="08a86-159">b.</span><span class="sxs-lookup"><span data-stu-id="08a86-159">b.</span></span> <span data-ttu-id="08a86-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="08a86-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08a86-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="08a86-161">These values are not real.</span></span> <span data-ttu-id="08a86-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="08a86-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="08a86-163">Contacte [equipa de suporte de cliente Wikispaces](https://www.wikispaces.com/site/help) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="08a86-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) tooget these values.</span></span> 

4. <span data-ttu-id="08a86-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="08a86-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="08a86-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="08a86-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="08a86-168">tooconfigure-início de sessão único em **Wikispaces** lado, terá de Olá toosend transferido **XML de metadados** demasiado[Wikispaces suporta equipa](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="08a86-168">tooconfigure single sign-on on **Wikispaces** side, you need toosend hello downloaded **Metadata XML** too[Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="08a86-169">Irá receber uma notificação assim que a configuração de Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="08a86-169">You will get a notification as soon as hello configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="08a86-170">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="08a86-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="08a86-171">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="08a86-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="08a86-172">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08a86-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="08a86-173">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08a86-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="08a86-174">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08a86-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="08a86-176">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="08a86-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="08a86-177">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="08a86-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08a86-179">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="08a86-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08a86-181">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="08a86-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08a86-183">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="08a86-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08a86-185">a.</span><span class="sxs-lookup"><span data-stu-id="08a86-185">a.</span></span> <span data-ttu-id="08a86-186">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08a86-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08a86-187">b.</span><span class="sxs-lookup"><span data-stu-id="08a86-187">b.</span></span> <span data-ttu-id="08a86-188">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="08a86-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08a86-189">c.</span><span class="sxs-lookup"><span data-stu-id="08a86-189">c.</span></span> <span data-ttu-id="08a86-190">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="08a86-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="08a86-191">d.</span><span class="sxs-lookup"><span data-stu-id="08a86-191">d.</span></span> <span data-ttu-id="08a86-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08a86-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="08a86-193">Criar um utilizador de teste Wikispaces</span><span class="sxs-lookup"><span data-stu-id="08a86-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="08a86-194">Na ordem tooenable do Azure AD os utilizadores toolog no tooWikispaces, têm de ser aprovisionados para Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="08a86-194">In order tooenable Azure AD users toolog in tooWikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="08a86-195">No caso de Olá da Wikispaces, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="08a86-195">In hello case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="08a86-196">executar de contas de utilizador, tooprovision Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="08a86-196">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="08a86-197">Inicie sessão no tooyour **Wikispaces** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="08a86-197">Log in tooyour **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="08a86-198">Aceda demasiado**membros**.</span><span class="sxs-lookup"><span data-stu-id="08a86-198">Go too**Members**.</span></span>
   
    <span data-ttu-id="08a86-199">![Os membros](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "membros")</span><span class="sxs-lookup"><span data-stu-id="08a86-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="08a86-200">Clique em Olá **convidar pessoas**.</span><span class="sxs-lookup"><span data-stu-id="08a86-200">Click hello **Invite People**.</span></span>
   
    <span data-ttu-id="08a86-201">![Convidar pessoas](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "convidar pessoas")</span><span class="sxs-lookup"><span data-stu-id="08a86-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="08a86-202">No Olá **convidar pessoas** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="08a86-202">In hello **Invite People** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="08a86-203">![Convidar pessoas](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "convidar pessoas")</span><span class="sxs-lookup"><span data-stu-id="08a86-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="08a86-204">a.</span><span class="sxs-lookup"><span data-stu-id="08a86-204">a.</span></span> <span data-ttu-id="08a86-205">Olá tipo **nomes de utilizador ou endereço de correio eletrónico** de uma conta válida do AAD que pretende tooprovision Olá relacionadas com caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="08a86-205">Type hello **Usernames or Email Address** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="08a86-206">b.</span><span class="sxs-lookup"><span data-stu-id="08a86-206">b.</span></span> <span data-ttu-id="08a86-207">Clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="08a86-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="08a86-208">titular de conta do Azure Active Directory Olá recebe uma mensagem de e-mail, incluindo uma conta de Olá ligação tooconfirm para ficar ativa.</span><span class="sxs-lookup"><span data-stu-id="08a86-208">hello Azure Active Directory account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="08a86-209">Pode utilizar quaisquer outras Wikispaces utilizador conta criação ferramentas ou APIs fornecidas pelo Wikispaces tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="08a86-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="08a86-210">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08a86-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="08a86-211">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooWikispaces.</span><span class="sxs-lookup"><span data-stu-id="08a86-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWikispaces.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="08a86-213">**tooassign Britta Simon tooWikispaces, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="08a86-213">**tooassign Britta Simon tooWikispaces, perform hello following steps:**</span></span>

1. <span data-ttu-id="08a86-214">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="08a86-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="08a86-216">Na lista de aplicações de Olá, selecione **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="08a86-216">In hello applications list, select **Wikispaces**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="08a86-218">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="08a86-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="08a86-220">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="08a86-220">Click **Add** button.</span></span> <span data-ttu-id="08a86-221">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08a86-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="08a86-223">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="08a86-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="08a86-224">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08a86-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08a86-225">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08a86-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="08a86-226">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="08a86-226">Testing single sign-on</span></span>

<span data-ttu-id="08a86-227">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="08a86-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="08a86-228">Ao clicar Olá Wikispaces na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour Wikispaces aplicação.</span><span class="sxs-lookup"><span data-stu-id="08a86-228">When you click hello Wikispaces tile in hello Access Panel, you should get automatically signed-on tooyour Wikispaces application.</span></span>
<span data-ttu-id="08a86-229">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="08a86-229">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08a86-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="08a86-230">Additional resources</span></span>

* [<span data-ttu-id="08a86-231">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08a86-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08a86-232">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08a86-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

