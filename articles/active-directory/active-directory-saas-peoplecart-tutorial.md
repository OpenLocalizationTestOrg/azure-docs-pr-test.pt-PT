---
title: "Tutorial: Integração do Azure Active Directory com Peoplecart | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Peoplecart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 481c7246a63f669ab39cb4ec652cebf40ba35f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="55e5a-103">Tutorial: Integração do Azure Active Directory com Peoplecart</span><span class="sxs-lookup"><span data-stu-id="55e5a-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="55e5a-104">Neste tutorial, saiba como toointegrate Peoplecart com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55e5a-104">In this tutorial, you learn how toointegrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55e5a-105">Integrar Peoplecart com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="55e5a-105">Integrating Peoplecart with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="55e5a-106">Pode controlar no Azure AD que tenha acesso tooPeoplecart</span><span class="sxs-lookup"><span data-stu-id="55e5a-106">You can control in Azure AD who has access tooPeoplecart</span></span>
- <span data-ttu-id="55e5a-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPeoplecart (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e5a-107">You can enable your users tooautomatically get signed-on tooPeoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55e5a-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="55e5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="55e5a-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="55e5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55e5a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="55e5a-110">Prerequisites</span></span>

<span data-ttu-id="55e5a-111">integração do Azure AD com Peoplecart tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="55e5a-111">tooconfigure Azure AD integration with Peoplecart, you need hello following items:</span></span>

- <span data-ttu-id="55e5a-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e5a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55e5a-113">Um Peoplecart-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="55e5a-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55e5a-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="55e5a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55e5a-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="55e5a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55e5a-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="55e5a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55e5a-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55e5a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55e5a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="55e5a-118">Scenario description</span></span>
<span data-ttu-id="55e5a-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="55e5a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55e5a-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="55e5a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55e5a-121">Adicionar Peoplecart da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="55e5a-121">Adding Peoplecart from hello gallery</span></span>
2. <span data-ttu-id="55e5a-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="55e5a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-hello-gallery"></a><span data-ttu-id="55e5a-123">Adicionar Peoplecart da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="55e5a-123">Adding Peoplecart from hello gallery</span></span>
<span data-ttu-id="55e5a-124">tooconfigure Olá integração de Peoplecart com o Azure AD, é necessário tooadd Peoplecart Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="55e5a-124">tooconfigure hello integration of Peoplecart into Azure AD, you need tooadd Peoplecart from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="55e5a-125">**tooadd Peoplecart da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="55e5a-125">**tooadd Peoplecart from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="55e5a-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="55e5a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="55e5a-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="55e5a-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="55e5a-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55e5a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="55e5a-133">Na caixa de pesquisa de Olá, escreva **Peoplecart**, selecione **Peoplecart** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="55e5a-133">In hello search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Peoplecart na lista de resultados de Olá](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="55e5a-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="55e5a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="55e5a-136">Nesta secção, configure e teste do Azure AD-início de sessão único com Peoplecart com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="55e5a-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55e5a-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Peoplecart é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55e5a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Peoplecart is tooa user in Azure AD.</span></span> <span data-ttu-id="55e5a-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Peoplecart tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="55e5a-138">In other words, a link relationship between an Azure AD user and hello related user in Peoplecart needs toobe established.</span></span>

<span data-ttu-id="55e5a-139">No Peoplecart, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="55e5a-139">In Peoplecart, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="55e5a-140">tooconfigure e teste do Azure AD-início de sessão único com Peoplecart, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="55e5a-140">tooconfigure and test Azure AD single sign-on with Peoplecart, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="55e5a-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="55e5a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="55e5a-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55e5a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55e5a-143">**[Criar um utilizador de teste Peoplecart](#create-a-peoplecart-test-user)**  -toohave um homólogo de Britta Simon no Peoplecart é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="55e5a-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - toohave a counterpart of Britta Simon in Peoplecart that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="55e5a-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="55e5a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55e5a-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="55e5a-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="55e5a-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="55e5a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="55e5a-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="55e5a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="55e5a-148">**tooconfigure do Azure AD-início de sessão único com Peoplecart, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="55e5a-148">**tooconfigure Azure AD single sign-on with Peoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="55e5a-149">No Olá portal do Azure, no Olá **Peoplecart** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-149">In hello Azure portal, on hello **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="55e5a-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="55e5a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="55e5a-153">No Olá **Peoplecart domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="55e5a-153">On hello **Peoplecart Domain and URLs** section, perform hello following steps:</span></span>

    ![Domínio Peoplecart e os URLs únicos de informações de início de sessão](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="55e5a-155">a.</span><span class="sxs-lookup"><span data-stu-id="55e5a-155">a.</span></span> <span data-ttu-id="55e5a-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="55e5a-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="55e5a-157">b.</span><span class="sxs-lookup"><span data-stu-id="55e5a-157">b.</span></span> <span data-ttu-id="55e5a-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="55e5a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55e5a-159">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="55e5a-159">These values are not real.</span></span> <span data-ttu-id="55e5a-160">Atualizar estes valores com Olá real URL de início de sessão e identificador.</span><span class="sxs-lookup"><span data-stu-id="55e5a-160">Update these values with hello actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="55e5a-161">Contacte [equipa de suporte de cliente Peoplecart](https://peoplecart.com/ContactUs.aspx) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="55e5a-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) tooget these values.</span></span> 
 
4. <span data-ttu-id="55e5a-162">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="55e5a-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="55e5a-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="55e5a-164">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="55e5a-166">No Olá **Peoplecart configuração** secção, clique em **configurar Peoplecart** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="55e5a-166">On hello **Peoplecart Configuration** section, click **Configure Peoplecart** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="55e5a-167">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="55e5a-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="55e5a-169">tooconfigure-início de sessão único em **Peoplecart** lado, terá de Olá toosend transferido **XML de metadados** e **único início de sessão no URL do serviço SAML** demasiado[ A equipa de suporte Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="55e5a-169">tooconfigure single sign-on on **Peoplecart** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="55e5a-170">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="55e5a-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="55e5a-171">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="55e5a-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="55e5a-172">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="55e5a-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="55e5a-173">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55e5a-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="55e5a-174">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e5a-174">Create an Azure AD test user</span></span>
<span data-ttu-id="55e5a-175">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55e5a-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="55e5a-177">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="55e5a-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="55e5a-178">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="55e5a-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="55e5a-180">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="55e5a-182">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="55e5a-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão de adição de Olá](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55e5a-184">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="55e5a-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55e5a-186">a.</span><span class="sxs-lookup"><span data-stu-id="55e5a-186">a.</span></span> <span data-ttu-id="55e5a-187">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55e5a-188">b.</span><span class="sxs-lookup"><span data-stu-id="55e5a-188">b.</span></span> <span data-ttu-id="55e5a-189">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="55e5a-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55e5a-190">c.</span><span class="sxs-lookup"><span data-stu-id="55e5a-190">c.</span></span> <span data-ttu-id="55e5a-191">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="55e5a-192">d.</span><span class="sxs-lookup"><span data-stu-id="55e5a-192">d.</span></span> <span data-ttu-id="55e5a-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="55e5a-194">Criar um utilizador de teste Peoplecart</span><span class="sxs-lookup"><span data-stu-id="55e5a-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="55e5a-195">Nesta secção, vai criar um utilizador chamado Britta Simon Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="55e5a-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="55e5a-196">Trabalhar com [equipa de suporte de Peoplecart](https://peoplecart.com/ContactUs.aspx) utilizadores de Olá tooadd na plataforma de Peoplecart Olá.</span><span class="sxs-lookup"><span data-stu-id="55e5a-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) tooadd hello users in hello Peoplecart platform.</span></span> <span data-ttu-id="55e5a-197">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="55e5a-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="55e5a-198">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="55e5a-198">Assign hello Azure AD test user</span></span>

<span data-ttu-id="55e5a-199">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPeoplecart.</span><span class="sxs-lookup"><span data-stu-id="55e5a-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPeoplecart.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="55e5a-201">**tooassign Britta Simon tooPeoplecart, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="55e5a-201">**tooassign Britta Simon tooPeoplecart, perform hello following steps:**</span></span>

1. <span data-ttu-id="55e5a-202">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="55e5a-204">Na lista de aplicações de Olá, selecione **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-204">In hello applications list, select **Peoplecart**.</span></span>

    ![ligação de Peoplecart Olá na lista de aplicações de Olá](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="55e5a-206">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="55e5a-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202] 

4. <span data-ttu-id="55e5a-208">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="55e5a-208">Click **Add** button.</span></span> <span data-ttu-id="55e5a-209">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55e5a-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="55e5a-211">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="55e5a-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="55e5a-212">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55e5a-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55e5a-213">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="55e5a-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="55e5a-214">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="55e5a-214">Test single sign-on</span></span>

<span data-ttu-id="55e5a-215">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="55e5a-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="55e5a-216">Ao clicar em mosaico de Peoplecart Olá no painel de acesso de Olá, deve obter a página de início de sessão da aplicação Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="55e5a-216">When you click hello Peoplecart tile in hello Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="55e5a-217">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="55e5a-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55e5a-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="55e5a-218">Additional resources</span></span>

* [<span data-ttu-id="55e5a-219">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55e5a-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55e5a-220">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55e5a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

