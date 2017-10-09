---
title: "Tutorial: Integração do Azure Active Directory com Citrix ShareFile | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="6e547-103">Tutorial: Integração do Azure Active Directory com Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6e547-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="6e547-104">Neste tutorial, saiba como toointegrate Citrix ShareFile com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e547-104">In this tutorial, you learn how toointegrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e547-105">Integrar o Citrix ShareFile com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="6e547-105">Integrating Citrix ShareFile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6e547-106">Pode controlar no Azure AD que tenha acesso tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6e547-106">You can control in Azure AD who has access tooCitrix ShareFile.</span></span>
- <span data-ttu-id="6e547-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooCitrix ShareFile (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e547-107">You can enable your users tooautomatically get signed-on tooCitrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6e547-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e547-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6e547-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e547-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e547-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6e547-110">Prerequisites</span></span>

<span data-ttu-id="6e547-111">integração do Azure AD com Citrix ShareFile tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6e547-111">tooconfigure Azure AD integration with Citrix ShareFile, you need hello following items:</span></span>

- <span data-ttu-id="6e547-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e547-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e547-113">Um Citrix ShareFile-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="6e547-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e547-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6e547-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e547-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6e547-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e547-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6e547-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e547-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e547-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e547-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6e547-118">Scenario description</span></span>
<span data-ttu-id="6e547-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6e547-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e547-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="6e547-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e547-121">Adicionar Citrix ShareFile da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6e547-121">Add Citrix ShareFile from hello gallery</span></span>
2. <span data-ttu-id="6e547-122">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6e547-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-hello-gallery"></a><span data-ttu-id="6e547-123">Adicionar Citrix ShareFile da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6e547-123">Add Citrix ShareFile from hello gallery</span></span>
<span data-ttu-id="6e547-124">tooconfigure Olá integração da Citrix ShareFile com o Azure AD, é necessário tooadd Citrix ShareFile Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="6e547-124">tooconfigure hello integration of Citrix ShareFile into Azure AD, you need tooadd Citrix ShareFile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6e547-125">**tooadd Citrix ShareFile da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e547-125">**tooadd Citrix ShareFile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e547-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6e547-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="6e547-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6e547-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6e547-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6e547-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="6e547-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e547-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="6e547-133">Na caixa de pesquisa de Olá, escreva **Citrix ShareFile**, selecione **Citrix ShareFile** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="6e547-133">In hello search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Lista de resultados da Citrix ShareFile no Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6e547-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6e547-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6e547-136">Nesta secção, configure e teste do Azure AD-início de sessão único com Citrix ShareFile baseado na chamado "Britta Simon" um utilizador de teste.</span><span class="sxs-lookup"><span data-stu-id="6e547-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e547-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Citrix ShareFile é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e547-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix ShareFile is tooa user in Azure AD.</span></span> <span data-ttu-id="6e547-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Citrix ShareFile tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6e547-138">In other words, a link relationship between an Azure AD user and hello related user in Citrix ShareFile needs toobe established.</span></span>

<span data-ttu-id="6e547-139">No Citrix ShareFile, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="6e547-139">In Citrix ShareFile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6e547-140">tooconfigure e teste do Azure AD-início de sessão único com Citrix ShareFile, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6e547-140">tooconfigure and test Azure AD single sign-on with Citrix ShareFile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6e547-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="6e547-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6e547-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e547-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e547-143">**[Criar um utilizador de teste do Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave um homólogo de Britta Simon no Citrix ShareFile que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="6e547-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - toohave a counterpart of Britta Simon in Citrix ShareFile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e547-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6e547-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e547-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="6e547-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6e547-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6e547-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6e547-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6e547-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="6e547-148">**tooconfigure do Azure AD-início de sessão único com Citrix ShareFile, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e547-148">**tooconfigure Azure AD single sign-on with Citrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e547-149">No Olá portal do Azure, no Olá **Citrix ShareFile** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="6e547-149">In hello Azure portal, on hello **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="6e547-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6e547-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="6e547-153">No Olá **Citrix ShareFile domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6e547-153">On hello **Citrix ShareFile Domain and URLs** section, perform hello following steps:</span></span>

    ![Citrix ShareFile domínio e os URLs únicos de informações de início de sessão](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="6e547-155">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="6e547-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e547-156">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="6e547-156">This value is not real.</span></span> <span data-ttu-id="6e547-157">Atualizar este valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="6e547-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6e547-158">Contacte [equipa de suporte de cliente do Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="6e547-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) tooget this value.</span></span> 

4. <span data-ttu-id="6e547-159">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6e547-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="6e547-161">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="6e547-161">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e547-163">No Olá **configuração da Citrix ShareFile** secção, clique em **configurar ShareFile de Citrix** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="6e547-163">On hello **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6e547-164">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="6e547-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração da Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="6e547-166">Numa janela do browser web diferente, inicie sessão no seu **Citrix ShareFile** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="6e547-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="6e547-167">Na barra de ferramentas Olá na parte superior do Olá, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="6e547-167">In hello toolbar on hello top, click **Admin**.</span></span>

9. <span data-ttu-id="6e547-168">No painel de navegação esquerdo Olá, selecione **configurar Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6e547-168">In hello left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="6e547-169">![Conta de administração](./media/active-directory-saas-sharefile-tutorial/ic773627.png "administração da conta")</span><span class="sxs-lookup"><span data-stu-id="6e547-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="6e547-170">No Olá **Single Sign-On / SAML 2.0 configuração** página da caixa de diálogo em **definições básicas**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6e547-170">On hello **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform hello following steps:</span></span>
   
    <span data-ttu-id="6e547-171">![De sessão único-](./media/active-directory-saas-sharefile-tutorial/ic773628.png "de sessão único-")</span><span class="sxs-lookup"><span data-stu-id="6e547-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="6e547-172">a.</span><span class="sxs-lookup"><span data-stu-id="6e547-172">a.</span></span> <span data-ttu-id="6e547-173">Clique em **ativar SAML**.</span><span class="sxs-lookup"><span data-stu-id="6e547-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="6e547-174">b.</span><span class="sxs-lookup"><span data-stu-id="6e547-174">b.</span></span> <span data-ttu-id="6e547-175">No **o emissor de IDP / ID de entidade** caixa de texto, colar Olá valor **ID de entidade de SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e547-175">In **Your IDP Issuer/ Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6e547-176">c.</span><span class="sxs-lookup"><span data-stu-id="6e547-176">c.</span></span> <span data-ttu-id="6e547-177">Clique em **alteração** toohello seguinte **certificado x. 509** Olá, campo e, em seguida, o certificado de Olá de carregamento transferiu a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e547-177">Click **Change** next toohello **X.509 Certificate** field and then upload hello certificate you downloaded from hello Azure portal.</span></span>
    
    <span data-ttu-id="6e547-178">d.</span><span class="sxs-lookup"><span data-stu-id="6e547-178">d.</span></span> <span data-ttu-id="6e547-179">No **URL de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e547-179">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="6e547-180">e.</span><span class="sxs-lookup"><span data-stu-id="6e547-180">e.</span></span> <span data-ttu-id="6e547-181">No **URL de fim de sessão** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e547-181">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="6e547-182">Clique em **guardar** no Olá portal de gestão do Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6e547-182">Click **Save** on hello Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="6e547-183">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="6e547-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6e547-184">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e547-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6e547-185">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e547-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6e547-186">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e547-186">Create an Azure AD test user</span></span>

<span data-ttu-id="6e547-187">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e547-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="6e547-189">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e547-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e547-190">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="6e547-190">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6e547-192">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="6e547-192">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6e547-194">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e547-194">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6e547-196">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6e547-196">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6e547-198">a.</span><span class="sxs-lookup"><span data-stu-id="6e547-198">a.</span></span> <span data-ttu-id="6e547-199">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e547-199">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e547-200">b.</span><span class="sxs-lookup"><span data-stu-id="6e547-200">b.</span></span> <span data-ttu-id="6e547-201">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e547-201">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="6e547-202">c.</span><span class="sxs-lookup"><span data-stu-id="6e547-202">c.</span></span> <span data-ttu-id="6e547-203">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="6e547-203">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="6e547-204">d.</span><span class="sxs-lookup"><span data-stu-id="6e547-204">d.</span></span> <span data-ttu-id="6e547-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6e547-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="6e547-206">Criar um utilizador de teste Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="6e547-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="6e547-207">Na ordem tooenable do Azure AD os utilizadores toolog para Citrix ShareFile, têm de ser aprovisionados para Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6e547-207">In order tooenable Azure AD users toolog into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="6e547-208">No caso de Olá da Citrix ShareFile, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="6e547-208">In hello case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="6e547-209">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e547-209">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e547-210">Inicie sessão no tooyour **Citrix ShareFile** inquilino.</span><span class="sxs-lookup"><span data-stu-id="6e547-210">Log in tooyour **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="6e547-211">Clique em **gerir utilizadores \> gerir utilizadores Home \> + criar empregado**.</span><span class="sxs-lookup"><span data-stu-id="6e547-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="6e547-212">![Criar empregado](./media/active-directory-saas-sharefile-tutorial/IC781050.png "criar empregado")</span><span class="sxs-lookup"><span data-stu-id="6e547-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="6e547-213">No Olá **informações básicas** secção, execute passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="6e547-213">On hello **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="6e547-214">![Informações básicas](./media/active-directory-saas-sharefile-tutorial/IC799951.png "informações básicas")</span><span class="sxs-lookup"><span data-stu-id="6e547-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="6e547-215">a.</span><span class="sxs-lookup"><span data-stu-id="6e547-215">a.</span></span> <span data-ttu-id="6e547-216">No Olá **endereço de correio eletrónico** caixa de texto, endereço de correio eletrónico do tipo Olá de Britta Simon como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="6e547-216">In hello **Email Address** textbox, type hello email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="6e547-217">b.</span><span class="sxs-lookup"><span data-stu-id="6e547-217">b.</span></span> <span data-ttu-id="6e547-218">No Olá **nome próprio** caixa de texto, tipo **nome próprio** do utilizador como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6e547-218">In hello **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="6e547-219">c.</span><span class="sxs-lookup"><span data-stu-id="6e547-219">c.</span></span> <span data-ttu-id="6e547-220">No Olá **Apelido** caixa de texto, tipo **Apelido** do utilizador como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6e547-220">In hello **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="6e547-221">Clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="6e547-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="6e547-222">titular da conta do Olá do Azure AD irá receber um e-mail e siga a tooconfirm uma ligação a respetiva conta para ficar ativa. Pode utilizar quaisquer outras Citrix ShareFile utilizador conta criação ferramentas ou APIs fornecidas pelo Citrix ShareFile tooprovision contas de utilizador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e547-222">hello Azure AD account holder will receive an email and follow a link tooconfirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6e547-223">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e547-223">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6e547-224">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooCitrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6e547-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix ShareFile.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="6e547-226">**tooassign Britta Simon tooCitrix ShareFile, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e547-226">**tooassign Britta Simon tooCitrix ShareFile, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e547-227">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6e547-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="6e547-229">Na lista de aplicações de Olá, selecione **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="6e547-229">In hello applications list, select **Citrix ShareFile**.</span></span>

    ![Olá Citrix ShareFile ligação na lista de aplicações de Olá](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="6e547-231">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6e547-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="6e547-233">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="6e547-233">Click **Add** button.</span></span> <span data-ttu-id="6e547-234">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e547-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="6e547-236">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="6e547-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6e547-237">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e547-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e547-238">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e547-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6e547-239">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6e547-239">Test single sign-on</span></span>

<span data-ttu-id="6e547-240">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="6e547-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6e547-241">Ao clicar Olá Citrix ShareFile na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="6e547-241">When you click hello Citrix ShareFile tile in hello Access Panel, you should get automatically signed-on tooyour Citrix ShareFile application.</span></span>
<span data-ttu-id="6e547-242">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e547-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6e547-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6e547-243">Additional resources</span></span>

* [<span data-ttu-id="6e547-244">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e547-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e547-245">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e547-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

