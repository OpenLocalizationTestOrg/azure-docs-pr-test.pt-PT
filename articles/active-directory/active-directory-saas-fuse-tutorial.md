---
title: "Tutorial: Integração do Azure Active Directory com Fuse | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Fuse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 720ed8af0b5de1e3bee5a40353ca0ee661766864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="89f6a-103">Tutorial: Integração do Azure Active Directory com Fuse</span><span class="sxs-lookup"><span data-stu-id="89f6a-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="89f6a-104">Neste tutorial, saiba como toointegrate Fuse com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89f6a-104">In this tutorial, you learn how toointegrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89f6a-105">Integrar Fuse com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="89f6a-105">Integrating Fuse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89f6a-106">Pode controlar no Azure AD que tenha acesso tooFuse.</span><span class="sxs-lookup"><span data-stu-id="89f6a-106">You can control in Azure AD who has access tooFuse.</span></span>
- <span data-ttu-id="89f6a-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooFuse (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89f6a-107">You can enable your users tooautomatically get signed-on tooFuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="89f6a-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="89f6a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="89f6a-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89f6a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89f6a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="89f6a-110">Prerequisites</span></span>

<span data-ttu-id="89f6a-111">integração de tooconfigure do Azure AD com Fuse, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="89f6a-111">tooconfigure Azure AD integration with Fuse, you need hello following items:</span></span>

- <span data-ttu-id="89f6a-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="89f6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89f6a-113">Um Fuse-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="89f6a-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89f6a-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="89f6a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89f6a-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="89f6a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89f6a-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="89f6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89f6a-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89f6a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89f6a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="89f6a-118">Scenario description</span></span>
<span data-ttu-id="89f6a-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="89f6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89f6a-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="89f6a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89f6a-121">Adicionar Fuse da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="89f6a-121">Add Fuse from hello gallery</span></span>
2. <span data-ttu-id="89f6a-122">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="89f6a-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-hello-gallery"></a><span data-ttu-id="89f6a-123">Adicionar Fuse da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="89f6a-123">Add Fuse from hello gallery</span></span>
<span data-ttu-id="89f6a-124">tooconfigure Olá integração de Fuse com o Azure AD, é necessário tooadd Fuse Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="89f6a-124">tooconfigure hello integration of Fuse into Azure AD, you need tooadd Fuse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89f6a-125">**tooadd Fuse da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="89f6a-125">**tooadd Fuse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89f6a-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="89f6a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="89f6a-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89f6a-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="89f6a-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89f6a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="89f6a-133">Na caixa de pesquisa de Olá, escreva **Fuse**, selecione **Fuse** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="89f6a-133">In hello search box, type **Fuse**, select **Fuse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Fuse na lista de resultados de Olá](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="89f6a-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="89f6a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="89f6a-136">Nesta secção, configure e teste do Azure AD-início de sessão único com Fuse com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="89f6a-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89f6a-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Fuse é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89f6a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuse is tooa user in Azure AD.</span></span> <span data-ttu-id="89f6a-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados com o utilizador no Fuse necessidades toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="89f6a-138">In other words, a link relationship between an Azure AD user and hello related user in Fuse needs toobe established.</span></span>

<span data-ttu-id="89f6a-139">No Fuse, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="89f6a-139">In Fuse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="89f6a-140">tooconfigure e teste do Azure AD-início de sessão único com Fuse, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="89f6a-140">tooconfigure and test Azure AD single sign-on with Fuse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89f6a-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="89f6a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89f6a-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89f6a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89f6a-143">**[Criar um utilizador de teste Fuse](#create-a-fuse-test-user)**  -toohave um homólogo de Britta Simon no Fuse é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="89f6a-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - toohave a counterpart of Britta Simon in Fuse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="89f6a-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="89f6a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89f6a-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="89f6a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="89f6a-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="89f6a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="89f6a-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Fuse.</span><span class="sxs-lookup"><span data-stu-id="89f6a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="89f6a-148">**tooconfigure do Azure AD-início de sessão único com Fuse, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="89f6a-148">**tooconfigure Azure AD single sign-on with Fuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="89f6a-149">No Olá portal do Azure, no Olá **Fuse** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-149">In hello Azure portal, on hello **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="89f6a-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="89f6a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="89f6a-153">No Olá **Fuse domínios e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="89f6a-153">On hello **Fuse Domain and URLs** section, perform hello following steps:</span></span>

    ![Fuse URLs e de domínio único início de sessão informações](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="89f6a-155">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="89f6a-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89f6a-156">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="89f6a-156">This value is not real.</span></span> <span data-ttu-id="89f6a-157">Atualizar este valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="89f6a-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="89f6a-158">Contacte [equipa de suporte de cliente Fuse](mailto:support@fusion-universal.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="89f6a-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="89f6a-159">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (bruto)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="89f6a-159">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="89f6a-161">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="89f6a-161">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89f6a-163">No Olá **Fuse configuração** secção, clique em **configurar Fuse** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="89f6a-163">On hello **Fuse Configuration** section, click **Configure Fuse** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="89f6a-164">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="89f6a-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="89f6a-166">tooget SSO configuradas para a sua aplicação, contacte [equipa de suporte de Fuse](mailto:support@fusion-universal.com) e forneça-los com o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="89f6a-166">tooget SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with hello following:</span></span>

    * <span data-ttu-id="89f6a-167">Olá transferido **ficheiro de certificado (bruto)**</span><span class="sxs-lookup"><span data-stu-id="89f6a-167">hello downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="89f6a-168">Olá **único início de sessão no URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="89f6a-168">hello **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="89f6a-169">Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="89f6a-169">hello **SAML Entity ID**</span></span>
    * <span data-ttu-id="89f6a-170">Olá **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="89f6a-170">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="89f6a-171">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="89f6a-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89f6a-172">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="89f6a-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89f6a-173">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89f6a-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="89f6a-174">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="89f6a-174">Create an Azure AD test user</span></span>

<span data-ttu-id="89f6a-175">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="89f6a-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="89f6a-177">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="89f6a-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89f6a-178">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="89f6a-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="89f6a-180">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="89f6a-182">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89f6a-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="89f6a-184">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="89f6a-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="89f6a-186">a.</span><span class="sxs-lookup"><span data-stu-id="89f6a-186">a.</span></span> <span data-ttu-id="89f6a-187">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89f6a-188">b.</span><span class="sxs-lookup"><span data-stu-id="89f6a-188">b.</span></span> <span data-ttu-id="89f6a-189">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89f6a-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="89f6a-190">c.</span><span class="sxs-lookup"><span data-stu-id="89f6a-190">c.</span></span> <span data-ttu-id="89f6a-191">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="89f6a-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="89f6a-192">d.</span><span class="sxs-lookup"><span data-stu-id="89f6a-192">d.</span></span> <span data-ttu-id="89f6a-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="89f6a-194">Criar um utilizador de teste Fuse</span><span class="sxs-lookup"><span data-stu-id="89f6a-194">Create a Fuse test user</span></span>

<span data-ttu-id="89f6a-195">Nesta secção, vai criar um utilizador chamado Britta Simon Fuse.</span><span class="sxs-lookup"><span data-stu-id="89f6a-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="89f6a-196">Consulte [equipa de suporte de Fuse](mailto:support@fusion-universal.com) utilizadores de Olá tooadd na plataforma de Fuse Olá.</span><span class="sxs-lookup"><span data-stu-id="89f6a-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) tooadd hello users in hello Fuse platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="89f6a-197">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="89f6a-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="89f6a-198">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooFuse.</span><span class="sxs-lookup"><span data-stu-id="89f6a-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFuse.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="89f6a-200">**tooassign Britta Simon tooFuse, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="89f6a-200">**tooassign Britta Simon tooFuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="89f6a-201">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="89f6a-203">Na lista de aplicações de Olá, selecione **Fuse**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-203">In hello applications list, select **Fuse**.</span></span>

    ![ligação de Fuse Olá na lista de aplicações de Olá](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="89f6a-205">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="89f6a-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="89f6a-207">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="89f6a-207">Click **Add** button.</span></span> <span data-ttu-id="89f6a-208">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89f6a-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="89f6a-210">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="89f6a-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89f6a-211">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89f6a-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89f6a-212">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="89f6a-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="89f6a-213">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="89f6a-213">Test single sign-on</span></span>

<span data-ttu-id="89f6a-214">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="89f6a-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="89f6a-215">Ao clicar em mosaico de Fuse Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Fuse aplicação.</span><span class="sxs-lookup"><span data-stu-id="89f6a-215">When you click hello Fuse tile in hello Access Panel, you should get automatically signed-on tooyour Fuse application.</span></span>
<span data-ttu-id="89f6a-216">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89f6a-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="89f6a-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="89f6a-217">Additional resources</span></span>

* [<span data-ttu-id="89f6a-218">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89f6a-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89f6a-219">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89f6a-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

