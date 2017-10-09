---
title: "Tutorial: Integração do Azure Active Directory com Showpad | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Showpad."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48b6bee0-dbc5-4863-964d-75b25e517741
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2c8c306b4b94c368a93f92123d3abe9fe35167db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-showpad"></a><span data-ttu-id="3d545-103">Tutorial: Integração do Azure Active Directory com Showpad</span><span class="sxs-lookup"><span data-stu-id="3d545-103">Tutorial: Azure Active Directory integration with Showpad</span></span>

<span data-ttu-id="3d545-104">Neste tutorial, saiba como toointegrate Showpad com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d545-104">In this tutorial, you learn how toointegrate Showpad with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d545-105">Integrar Showpad com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="3d545-105">Integrating Showpad with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3d545-106">Pode controlar no Azure AD que tenha acesso tooShowpad</span><span class="sxs-lookup"><span data-stu-id="3d545-106">You can control in Azure AD who has access tooShowpad</span></span>
- <span data-ttu-id="3d545-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooShowpad (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d545-107">You can enable your users tooautomatically get signed-on tooShowpad (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d545-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3d545-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3d545-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d545-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d545-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3d545-110">Prerequisites</span></span>

<span data-ttu-id="3d545-111">integração do Azure AD com Showpad tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3d545-111">tooconfigure Azure AD integration with Showpad, you need hello following items:</span></span>

- <span data-ttu-id="3d545-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d545-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d545-113">Um Showpad-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="3d545-113">A Showpad single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d545-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3d545-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d545-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3d545-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d545-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3d545-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d545-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d545-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d545-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3d545-118">Scenario description</span></span>
<span data-ttu-id="3d545-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3d545-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d545-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="3d545-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d545-121">Adicionar Showpad da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="3d545-121">Adding Showpad from hello gallery</span></span>
2. <span data-ttu-id="3d545-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="3d545-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-showpad-from-hello-gallery"></a><span data-ttu-id="3d545-123">Adicionar Showpad da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="3d545-123">Adding Showpad from hello gallery</span></span>

<span data-ttu-id="3d545-124">tooconfigure Olá integração de Showpad com o Azure AD, é necessário tooadd Showpad Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="3d545-124">tooconfigure hello integration of Showpad into Azure AD, you need tooadd Showpad from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3d545-125">**tooadd Showpad da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3d545-125">**tooadd Showpad from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d545-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="3d545-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d545-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3d545-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3d545-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="3d545-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="3d545-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d545-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="3d545-133">Na caixa de pesquisa de Olá, escreva **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="3d545-133">In hello search box, type **Showpad**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_search.png)

5. <span data-ttu-id="3d545-135">No painel de resultados de Olá, selecione **Showpad**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="3d545-135">In hello results panel, select **Showpad**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d545-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="3d545-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3d545-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Showpad com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3d545-138">In this section, you configure and test Azure AD single sign-on with Showpad based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3d545-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Showpad é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d545-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Showpad is tooa user in Azure AD.</span></span> <span data-ttu-id="3d545-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Showpad tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3d545-140">In other words, a link relationship between an Azure AD user and hello related user in Showpad needs toobe established.</span></span>

<span data-ttu-id="3d545-141">No Showpad, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="3d545-141">In Showpad, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3d545-142">tooconfigure e teste do Azure AD-início de sessão único com Showpad, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="3d545-142">tooconfigure and test Azure AD single sign-on with Showpad, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3d545-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="3d545-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3d545-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d545-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d545-145">**[Criar um utilizador de teste Showpad](#creating-a-showpad-test-user)**  -toohave um homólogo de Britta Simon no Showpad é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="3d545-145">**[Creating a Showpad test user](#creating-a-showpad-test-user)** - toohave a counterpart of Britta Simon in Showpad that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d545-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="3d545-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d545-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="3d545-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d545-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="3d545-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d545-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Showpad.</span><span class="sxs-lookup"><span data-stu-id="3d545-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Showpad application.</span></span>

<span data-ttu-id="3d545-150">**tooconfigure do Azure AD-início de sessão único com Showpad, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3d545-150">**tooconfigure Azure AD single sign-on with Showpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d545-151">No Olá portal do Azure, no Olá **Showpad** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="3d545-151">In hello Azure portal, on hello **Showpad** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="3d545-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="3d545-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_samlbase.png)

3. <span data-ttu-id="3d545-155">No Olá **Showpad domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3d545-155">On hello **Showpad Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_url.png)

    <span data-ttu-id="3d545-157">a.</span><span class="sxs-lookup"><span data-stu-id="3d545-157">a.</span></span> <span data-ttu-id="3d545-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<comapany-name>.showpad.biz/login`</span><span class="sxs-lookup"><span data-stu-id="3d545-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<comapany-name>.showpad.biz/login`</span></span>

    <span data-ttu-id="3d545-159">b.</span><span class="sxs-lookup"><span data-stu-id="3d545-159">b.</span></span> <span data-ttu-id="3d545-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company-name>.showpad.biz`</span><span class="sxs-lookup"><span data-stu-id="3d545-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.showpad.biz`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d545-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="3d545-161">These values are not real.</span></span> <span data-ttu-id="3d545-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="3d545-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3d545-163">Contacte [equipa de suporte de Showpad](https://help.showpad.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="3d545-163">Contact [Showpad support team](https://help.showpad.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="3d545-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="3d545-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_certificate.png) 

5. <span data-ttu-id="3d545-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="3d545-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-showpad-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3d545-168">Início de sessão tooyour Showpad inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="3d545-168">Sign-on tooyour Showpad tenant as an administrator.</span></span>

7. <span data-ttu-id="3d545-169">No menu de Olá na parte superior do Olá, clique em Olá **definições**.</span><span class="sxs-lookup"><span data-stu-id="3d545-169">In hello menu on hello top, click hello **Settings**.</span></span>
   
    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_001.png) 

8. <span data-ttu-id="3d545-171">Navegue demasiado"**Single Sign-On**"e clique em"**ativar**."</span><span class="sxs-lookup"><span data-stu-id="3d545-171">Navigate too"**Single Sign-On**" and click "**Enable**."</span></span>
   
    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_002.png)

9. <span data-ttu-id="3d545-173">No Olá **adicionar um serviço do SAML 2.0** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3d545-173">On hello **Add a SAML 2.0 Service** dialog, perform hello following steps:</span></span>
   
    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_003.png) 
   
    <span data-ttu-id="3d545-175">a.</span><span class="sxs-lookup"><span data-stu-id="3d545-175">a.</span></span> <span data-ttu-id="3d545-176">No Olá **nome** caixa de texto, nome de Olá de tipo de identificador do fornecedor (por exemplo: nome da sua empresa).</span><span class="sxs-lookup"><span data-stu-id="3d545-176">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="3d545-177">b.</span><span class="sxs-lookup"><span data-stu-id="3d545-177">b.</span></span> <span data-ttu-id="3d545-178">Como **metadados origem**, selecione **XML**.</span><span class="sxs-lookup"><span data-stu-id="3d545-178">As **Metadata Source**, select **XML**.</span></span>
   
    <span data-ttu-id="3d545-179">c.</span><span class="sxs-lookup"><span data-stu-id="3d545-179">c.</span></span> <span data-ttu-id="3d545-180">Copie Olá conteúdo do ficheiro XML de metadados, que transferiu do portal do Azure de Olá, e, em seguida, cole-o Olá **XML de metadados** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3d545-180">Copy hello content of metadata XML file, which you have downloaded from hello Azure portal, and then paste it into hello **Metadata XML** textbox.</span></span>
   
    <span data-ttu-id="3d545-181">d.</span><span class="sxs-lookup"><span data-stu-id="3d545-181">d.</span></span> <span data-ttu-id="3d545-182">Selecione **contas de aprovisionamento automático para os novos utilizadores quando iniciar sessão**.</span><span class="sxs-lookup"><span data-stu-id="3d545-182">Select **Auto-provision accounts for new users when they log in**.</span></span>
   
    <span data-ttu-id="3d545-183">e.</span><span class="sxs-lookup"><span data-stu-id="3d545-183">e.</span></span> <span data-ttu-id="3d545-184">Clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="3d545-184">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="3d545-185">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="3d545-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3d545-186">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="3d545-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3d545-187">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d545-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d545-188">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d545-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d545-189">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d545-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="3d545-191">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3d545-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d545-192">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="3d545-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d545-194">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="3d545-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d545-196">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="3d545-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d545-198">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3d545-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-showpad-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d545-200">a.</span><span class="sxs-lookup"><span data-stu-id="3d545-200">a.</span></span> <span data-ttu-id="3d545-201">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d545-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d545-202">b.</span><span class="sxs-lookup"><span data-stu-id="3d545-202">b.</span></span> <span data-ttu-id="3d545-203">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3d545-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d545-204">c.</span><span class="sxs-lookup"><span data-stu-id="3d545-204">c.</span></span> <span data-ttu-id="3d545-205">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="3d545-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3d545-206">d.</span><span class="sxs-lookup"><span data-stu-id="3d545-206">d.</span></span> <span data-ttu-id="3d545-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d545-207">Click **Create**.</span></span>
 
### <a name="creating-a-showpad-test-user"></a><span data-ttu-id="3d545-208">Criar um utilizador de teste Showpad</span><span class="sxs-lookup"><span data-stu-id="3d545-208">Creating a Showpad test user</span></span>

<span data-ttu-id="3d545-209">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Showpad.</span><span class="sxs-lookup"><span data-stu-id="3d545-209">hello objective of this section is toocreate a user called Britta Simon in Showpad.</span></span> 

<span data-ttu-id="3d545-210">Showpad suportam o aprovisionamento de just-in-time.</span><span class="sxs-lookup"><span data-stu-id="3d545-210">Showpad supports just-in-time provisioning.</span></span> <span data-ttu-id="3d545-211">Ativar aprovisionamento no  **[configurar do Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span><span class="sxs-lookup"><span data-stu-id="3d545-211">You have enabled provisioning in **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**.</span></span> 

<span data-ttu-id="3d545-212">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="3d545-212">There is no action item for you in this section.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3d545-213">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d545-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3d545-214">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooShowpad.</span><span class="sxs-lookup"><span data-stu-id="3d545-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooShowpad.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="3d545-216">**tooassign Britta Simon tooShowpad, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3d545-216">**tooassign Britta Simon tooShowpad, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d545-217">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="3d545-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="3d545-219">Na lista de aplicações de Olá, selecione **Showpad**.</span><span class="sxs-lookup"><span data-stu-id="3d545-219">In hello applications list, select **Showpad**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-showpad-tutorial/tutorial_showpad_app.png) 

3. <span data-ttu-id="3d545-221">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3d545-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="3d545-223">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="3d545-223">Click **Add** button.</span></span> <span data-ttu-id="3d545-224">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d545-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="3d545-226">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="3d545-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3d545-227">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d545-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d545-228">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d545-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d545-229">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="3d545-229">Testing single sign-on</span></span>

<span data-ttu-id="3d545-230">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3d545-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3d545-231">Ao clicar em mosaico de Showpad Olá no painel de acesso de Olá, deve colocar a aplicação de tooShowpad automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="3d545-231">When you click hello Showpad tile in hello Access Panel, you should get automatically signed-on tooShowpad application.</span></span>
<span data-ttu-id="3d545-232">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d545-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d545-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3d545-233">Additional resources</span></span>

* [<span data-ttu-id="3d545-234">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d545-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d545-235">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d545-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-showpad-tutorial/tutorial_general_203.png

