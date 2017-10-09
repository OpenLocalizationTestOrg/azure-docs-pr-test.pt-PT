---
title: "Tutorial: Integração do Azure Active Directory com Picturepark | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="accd2-103">Tutorial: Integração do Azure Active Directory com Picturepark</span><span class="sxs-lookup"><span data-stu-id="accd2-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="accd2-104">Neste tutorial, saiba como toointegrate Picturepark com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="accd2-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="accd2-105">Integrar Picturepark com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="accd2-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="accd2-106">Pode controlar no Azure AD que tenha acesso tooPicturepark</span><span class="sxs-lookup"><span data-stu-id="accd2-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="accd2-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPicturepark (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="accd2-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="accd2-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="accd2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="accd2-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="accd2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="accd2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="accd2-110">Prerequisites</span></span>

<span data-ttu-id="accd2-111">integração do Azure AD com Picturepark tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="accd2-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="accd2-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="accd2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="accd2-113">Um Picturepark-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="accd2-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="accd2-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="accd2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="accd2-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="accd2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="accd2-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="accd2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="accd2-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="accd2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="accd2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="accd2-118">Scenario description</span></span>
<span data-ttu-id="accd2-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="accd2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="accd2-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="accd2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="accd2-121">Adicionar Picturepark da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="accd2-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="accd2-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="accd2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="accd2-123">Adicionar Picturepark da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="accd2-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="accd2-124">tooconfigure Olá integração de Picturepark com o Azure AD, é necessário tooadd Picturepark Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="accd2-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="accd2-125">**tooadd Picturepark da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="accd2-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="accd2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="accd2-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="accd2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="accd2-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="accd2-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="accd2-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="accd2-133">Na caixa de pesquisa de Olá, escreva **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="accd2-133">In hello search box, type **Picturepark**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="accd2-135">No painel de resultados de Olá, selecione **Picturepark**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="accd2-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="accd2-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="accd2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="accd2-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Picturepark com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="accd2-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="accd2-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Picturepark é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="accd2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="accd2-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Picturepark tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="accd2-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="accd2-141">No Picturepark, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="accd2-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="accd2-142">tooconfigure e teste do Azure AD-início de sessão único com Picturepark, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="accd2-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="accd2-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="accd2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="accd2-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="accd2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="accd2-145">**[Criar um utilizador de teste Picturepark](#creating-a-picturepark-test-user)**  -toohave um homólogo de Britta Simon no Picturepark é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="accd2-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="accd2-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="accd2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="accd2-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="accd2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="accd2-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="accd2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="accd2-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Picturepark.</span><span class="sxs-lookup"><span data-stu-id="accd2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="accd2-150">**tooconfigure do Azure AD-início de sessão único com Picturepark, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="accd2-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-151">No Olá portal do Azure, no Olá **Picturepark** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="accd2-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="accd2-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="accd2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="accd2-155">No Olá **Picturepark domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="accd2-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="accd2-157">a.</span><span class="sxs-lookup"><span data-stu-id="accd2-157">a.</span></span> <span data-ttu-id="accd2-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="accd2-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="accd2-159">b.</span><span class="sxs-lookup"><span data-stu-id="accd2-159">b.</span></span> <span data-ttu-id="accd2-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:</span><span class="sxs-lookup"><span data-stu-id="accd2-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="accd2-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="accd2-161">These values are not real.</span></span> <span data-ttu-id="accd2-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="accd2-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="accd2-163">Contacte [equipa de suporte de cliente Picturepark](https://picturepark.com/about/contact/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="accd2-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="accd2-164">No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.</span><span class="sxs-lookup"><span data-stu-id="accd2-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="accd2-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="accd2-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="accd2-168">No Olá **Picturepark configuração** secção, clique em **configurar Picturepark** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="accd2-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="accd2-169">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="accd2-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="accd2-171">Numa janela do browser web diferente, inicie sessão no site da sua empresa Picturepark como administrador.</span><span class="sxs-lookup"><span data-stu-id="accd2-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="accd2-172">Na barra de ferramentas Olá na parte superior do Olá, clique em **ferramentas administrativas**e, em seguida, clique em **consola de gestão**.</span><span class="sxs-lookup"><span data-stu-id="accd2-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="accd2-173">![Consola de gestão](./media/active-directory-saas-picturepark-tutorial/ic795062.png "consola de gestão")</span><span class="sxs-lookup"><span data-stu-id="accd2-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="accd2-174">Clique em **autenticação**e, em seguida, clique em **fornecedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="accd2-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="accd2-175">![Autenticação](./media/active-directory-saas-picturepark-tutorial/ic795063.png "autenticação")</span><span class="sxs-lookup"><span data-stu-id="accd2-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="accd2-176">No Olá **configuração do fornecedor de identidade** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="accd2-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="accd2-177">![Configuração do fornecedor de identidade](./media/active-directory-saas-picturepark-tutorial/ic795064.png "configuração do fornecedor de identidade")</span><span class="sxs-lookup"><span data-stu-id="accd2-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="accd2-178">a.</span><span class="sxs-lookup"><span data-stu-id="accd2-178">a.</span></span> <span data-ttu-id="accd2-179">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="accd2-179">Click **Add**.</span></span>
  
    <span data-ttu-id="accd2-180">b.</span><span class="sxs-lookup"><span data-stu-id="accd2-180">b.</span></span> <span data-ttu-id="accd2-181">Escreva um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="accd2-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="accd2-182">c.</span><span class="sxs-lookup"><span data-stu-id="accd2-182">c.</span></span> <span data-ttu-id="accd2-183">Selecione **configurado como predefinido**.</span><span class="sxs-lookup"><span data-stu-id="accd2-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="accd2-184">d.</span><span class="sxs-lookup"><span data-stu-id="accd2-184">d.</span></span> <span data-ttu-id="accd2-185">No **URI de Issuer** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="accd2-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="accd2-186">e.</span><span class="sxs-lookup"><span data-stu-id="accd2-186">e.</span></span> <span data-ttu-id="accd2-187">No **impressão de botão de emissor fidedigno** caixa de texto, colar Olá valor **Thumbprint** que copiou do **certificado de assinatura de SAML** secção.</span><span class="sxs-lookup"><span data-stu-id="accd2-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="accd2-188">Clique em **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="accd2-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="accd2-189">Olá tooset **Emailaddress** atributo na Olá **afirmação** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="accd2-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="accd2-190">![Configuração](./media/active-directory-saas-picturepark-tutorial/ic795065.png "configuração")</span><span class="sxs-lookup"><span data-stu-id="accd2-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="accd2-191">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="accd2-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="accd2-192">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="accd2-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="accd2-193">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="accd2-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="accd2-194">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="accd2-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="accd2-195">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="accd2-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="accd2-197">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="accd2-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-198">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="accd2-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="accd2-200">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="accd2-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="accd2-202">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="accd2-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="accd2-204">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="accd2-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="accd2-206">a.</span><span class="sxs-lookup"><span data-stu-id="accd2-206">a.</span></span> <span data-ttu-id="accd2-207">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="accd2-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="accd2-208">b.</span><span class="sxs-lookup"><span data-stu-id="accd2-208">b.</span></span> <span data-ttu-id="accd2-209">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="accd2-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="accd2-210">c.</span><span class="sxs-lookup"><span data-stu-id="accd2-210">c.</span></span> <span data-ttu-id="accd2-211">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="accd2-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="accd2-212">d.</span><span class="sxs-lookup"><span data-stu-id="accd2-212">d.</span></span> <span data-ttu-id="accd2-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="accd2-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="accd2-214">Criar um utilizador de teste Picturepark</span><span class="sxs-lookup"><span data-stu-id="accd2-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="accd2-215">Na ordem tooenable do Azure AD os utilizadores toolog para Picturepark, têm de ser aprovisionados para Picturepark.</span><span class="sxs-lookup"><span data-stu-id="accd2-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="accd2-216">No caso de Olá da Picturepark, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="accd2-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="accd2-217">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="accd2-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-218">Inicie sessão no tooyour **Picturepark** inquilino.</span><span class="sxs-lookup"><span data-stu-id="accd2-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="accd2-219">Na barra de ferramentas Olá na parte superior do Olá, clique em **ferramentas administrativas**e, em seguida, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="accd2-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="accd2-220">![Os utilizadores](./media/active-directory-saas-picturepark-tutorial/ic795067.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="accd2-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="accd2-221">No Olá **descrição geral de utilizadores** separador, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="accd2-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="accd2-222">![Gestão de utilizadores](./media/active-directory-saas-picturepark-tutorial/ic795068.png "gestão de utilizadores")</span><span class="sxs-lookup"><span data-stu-id="accd2-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="accd2-223">No Olá **criar utilizador** caixa de diálogo, Olá de efetuar os seguintes passos para um utilizador válido para o Azure Active Directory que pretende tooprovision:</span><span class="sxs-lookup"><span data-stu-id="accd2-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="accd2-224">![Criar utilizador](./media/active-directory-saas-picturepark-tutorial/ic795069.png "criar utilizador")</span><span class="sxs-lookup"><span data-stu-id="accd2-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="accd2-225">a.</span><span class="sxs-lookup"><span data-stu-id="accd2-225">a.</span></span> <span data-ttu-id="accd2-226">No Olá **endereço de correio eletrónico** caixa de texto, Olá tipo **endereço de correio eletrónico** do utilizador Olá  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="accd2-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="accd2-227">b.</span><span class="sxs-lookup"><span data-stu-id="accd2-227">b.</span></span> <span data-ttu-id="accd2-228">No Olá **palavra-passe** e **Confirmar palavra-passe** caixas de texto, Olá tipo **palavra-passe** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="accd2-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="accd2-229">c.</span><span class="sxs-lookup"><span data-stu-id="accd2-229">c.</span></span> <span data-ttu-id="accd2-230">No Olá **nome próprio** caixa de texto, Olá tipo **nome próprio** do utilizador Olá **Britta**.</span><span class="sxs-lookup"><span data-stu-id="accd2-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="accd2-231">d.</span><span class="sxs-lookup"><span data-stu-id="accd2-231">d.</span></span> <span data-ttu-id="accd2-232">No Olá **Apelido** caixa de texto, Olá tipo **Apelido** do utilizador Olá **Simon**.</span><span class="sxs-lookup"><span data-stu-id="accd2-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="accd2-233">e.</span><span class="sxs-lookup"><span data-stu-id="accd2-233">e.</span></span> <span data-ttu-id="accd2-234">No Olá **empresa** caixa de texto, Olá tipo **nome da empresa** do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="accd2-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="accd2-235">f.</span><span class="sxs-lookup"><span data-stu-id="accd2-235">f.</span></span> <span data-ttu-id="accd2-236">No Olá **país** caixa de texto, selecione de Olá **país** do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="accd2-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="accd2-237">g.</span><span class="sxs-lookup"><span data-stu-id="accd2-237">g.</span></span> <span data-ttu-id="accd2-238">No Olá **ZIP** caixa de texto, Olá tipo **código postal** da cidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="accd2-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="accd2-239">h.</span><span class="sxs-lookup"><span data-stu-id="accd2-239">h.</span></span> <span data-ttu-id="accd2-240">No Olá **Cidade** caixa de texto, Olá tipo **nome Cidade** do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="accd2-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="accd2-241">posso.</span><span class="sxs-lookup"><span data-stu-id="accd2-241">i.</span></span> <span data-ttu-id="accd2-242">Selecione um **idioma**.</span><span class="sxs-lookup"><span data-stu-id="accd2-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="accd2-243">j.</span><span class="sxs-lookup"><span data-stu-id="accd2-243">j.</span></span> <span data-ttu-id="accd2-244">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="accd2-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="accd2-245">Pode utilizar quaisquer outras Picturepark utilizador conta criação ferramentas ou APIs fornecidas pelo Picturepark tooprovision contas de utilizador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="accd2-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="accd2-246">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="accd2-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="accd2-247">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPicturepark.</span><span class="sxs-lookup"><span data-stu-id="accd2-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="accd2-249">**tooassign Britta Simon tooPicturepark, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="accd2-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="accd2-250">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="accd2-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="accd2-252">Na lista de aplicações de Olá, selecione **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="accd2-252">In hello applications list, select **Picturepark**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="accd2-254">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="accd2-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="accd2-256">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="accd2-256">Click **Add** button.</span></span> <span data-ttu-id="accd2-257">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="accd2-259">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="accd2-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="accd2-260">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="accd2-261">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="accd2-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="accd2-262">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="accd2-262">Testing single sign-on</span></span>

<span data-ttu-id="accd2-263">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="accd2-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="accd2-264">Ao clicar em mosaico de Picturepark Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Picturepark aplicação.</span><span class="sxs-lookup"><span data-stu-id="accd2-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="accd2-265">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="accd2-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="accd2-266">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="accd2-266">Additional resources</span></span>

* [<span data-ttu-id="accd2-267">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="accd2-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="accd2-268">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="accd2-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

