---
title: "Tutorial: Integração do Azure Active Directory com o GitHub | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e do GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="bc195-103">Tutorial: Integração do Azure Active Directory com o GitHub</span><span class="sxs-lookup"><span data-stu-id="bc195-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="bc195-104">Neste tutorial, saiba como toointegrate GitHub com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc195-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bc195-105">Integrar o GitHub com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="bc195-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bc195-106">Pode controlar no Azure AD que tenha acesso tooGitHub</span><span class="sxs-lookup"><span data-stu-id="bc195-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="bc195-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooGitHub (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc195-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bc195-108">Pode gerir as contas numa localização central - portal de gestão do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="bc195-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="bc195-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bc195-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc195-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bc195-110">Prerequisites</span></span>

<span data-ttu-id="bc195-111">tooconfigure integração do Azure AD com o GitHub, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="bc195-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="bc195-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc195-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bc195-113">Um GitHub início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="bc195-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="bc195-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bc195-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="bc195-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bc195-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bc195-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="bc195-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="bc195-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bc195-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="bc195-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bc195-118">Scenario description</span></span>
<span data-ttu-id="bc195-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bc195-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bc195-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="bc195-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bc195-121">A adição de GitHub da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="bc195-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="bc195-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="bc195-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="bc195-123">A adição de GitHub da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="bc195-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="bc195-124">tooconfigure Olá integração do GitHub com o Azure AD, é necessário tooadd GitHub Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="bc195-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bc195-125">**tooadd GitHub da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bc195-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc195-126">No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="bc195-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bc195-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="bc195-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bc195-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="bc195-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="bc195-131">Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="bc195-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="bc195-133">Na caixa de pesquisa de Olá, escreva **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="bc195-133">In hello search box, type **GitHub.com**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="bc195-135">No painel de resultados de Olá, selecione **GitHub**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="bc195-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bc195-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="bc195-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bc195-138">Nesta secção, configure e teste do Azure AD-início de sessão único com o GitHub com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bc195-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bc195-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá no GitHub é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc195-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="bc195-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no GitHub tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="bc195-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="bc195-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no GitHub.</span><span class="sxs-lookup"><span data-stu-id="bc195-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="bc195-142">tooconfigure e teste do Azure AD-início de sessão único com o GitHub, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="bc195-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bc195-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="bc195-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bc195-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc195-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bc195-145">**[Criar um utilizador de teste do GitHub](#creating-a-GitHub-test-user)**  -toohave um homólogo de Britta Simon no GitHub que é a representação de toohello ligado do Azure AD de forma.</span><span class="sxs-lookup"><span data-stu-id="bc195-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="bc195-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="bc195-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bc195-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="bc195-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bc195-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="bc195-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bc195-149">Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="bc195-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="bc195-150">**tooconfigure do Azure AD-início de sessão único com o GitHub, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bc195-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc195-151">No portal de gestão do Azure de Olá, no Olá **GitHub** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="bc195-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="bc195-153">No Olá **de sessão único-** caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="bc195-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="bc195-155">No Olá **domínio GitHub e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="bc195-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="bc195-157">a.</span><span class="sxs-lookup"><span data-stu-id="bc195-157">a.</span></span> <span data-ttu-id="bc195-158">No Olá **URL de início de sessão** caixa de texto, valor de tipo de Olá como:`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="bc195-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="bc195-159">b.</span><span class="sxs-lookup"><span data-stu-id="bc195-159">b.</span></span> <span data-ttu-id="bc195-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="bc195-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bc195-161">Tenha em atenção que estes não são valores reais Olá.</span><span class="sxs-lookup"><span data-stu-id="bc195-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="bc195-162">Tiver tooupdate estes valores com Olá real iniciar sessão no URL e o identificador.</span><span class="sxs-lookup"><span data-stu-id="bc195-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="bc195-163">Aqui sugerimos toouse Olá exclusivo valor da cadeia no Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="bc195-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="bc195-164">Aceda tooGitHub Admin secção tooretrieve estes valores.</span><span class="sxs-lookup"><span data-stu-id="bc195-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="bc195-165">No Olá **atributos de utilizador** secção, selecione **identificador de utilizador** como user.mail.</span><span class="sxs-lookup"><span data-stu-id="bc195-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="bc195-167">No Olá **certificado de assinatura de SAML** secção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="bc195-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="bc195-169">No Olá **criar o novo certificado** caixa de diálogo, clique Olá ícone de calendário e selecione um **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="bc195-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="bc195-170">Em seguida, clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="bc195-170">Then click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="bc195-172">No Olá **certificado de assinatura de SAML** secção, selecione **tornar o novo certificado ativa** e clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="bc195-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="bc195-174">No pop-up de Olá **o certificado de Rollover** janela, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bc195-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="bc195-176">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="bc195-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="bc195-178">No Olá **configuração de GitHub** secção, clique em **configurar GitHub** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="bc195-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="bc195-181">Numa janela do browser web diferente, inicie sessão no seu site do GitHub organização como um administrador.</span><span class="sxs-lookup"><span data-stu-id="bc195-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="bc195-182">Navegue demasiado**definições** e clique em **segurança**</span><span class="sxs-lookup"><span data-stu-id="bc195-182">Navigate too**Settings** and click **Security**</span></span>

    ![Definições](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="bc195-184">Verifique Olá **autenticação ativar SAML** caixa, revelando Olá Single Sign-on configuração os campos.</span><span class="sxs-lookup"><span data-stu-id="bc195-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="bc195-185">Em seguida, utilize Olá URL single sign-on URL valor tooupdate Olá único início de sessão na configuração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc195-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![Definições](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="bc195-187">Configure Olá seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="bc195-187">Configure hello following fields:</span></span>

    <span data-ttu-id="bc195-188">a.</span><span class="sxs-lookup"><span data-stu-id="bc195-188">a.</span></span> <span data-ttu-id="bc195-189">**Inicie sessão no URL**: introduza **SAML-início de sessão único URL de serviço** de Olá **configurar GitHub** secção sobre o Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc195-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="bc195-190">b.</span><span class="sxs-lookup"><span data-stu-id="bc195-190">b.</span></span> <span data-ttu-id="bc195-191">**Emissor**: introduza **ID de entidade de SAML** de Olá **configurar GitHub** secção sobre o Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc195-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="bc195-192">c.</span><span class="sxs-lookup"><span data-stu-id="bc195-192">c.</span></span> <span data-ttu-id="bc195-193">**Certificado público**: Abra Olá transferido o certificado do Azure AD num bloco de notas e copie Olá o conteúdo, incluindo "Certificado começar" e "END certificado"</span><span class="sxs-lookup"><span data-stu-id="bc195-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![Definições](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="bc195-195">Clique em **configuração SAML do teste** tooconfirm que não existem falhas de validação ou erros durante a SSO.</span><span class="sxs-lookup"><span data-stu-id="bc195-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![Definições](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="bc195-197">Clique em **guardar**</span><span class="sxs-lookup"><span data-stu-id="bc195-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bc195-198">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc195-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="bc195-199">o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc195-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="bc195-201">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bc195-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc195-202">No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="bc195-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bc195-204">Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="bc195-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bc195-206">Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bc195-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bc195-208">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="bc195-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bc195-210">a.</span><span class="sxs-lookup"><span data-stu-id="bc195-210">a.</span></span> <span data-ttu-id="bc195-211">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bc195-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bc195-212">b.</span><span class="sxs-lookup"><span data-stu-id="bc195-212">b.</span></span> <span data-ttu-id="bc195-213">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bc195-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bc195-214">c.</span><span class="sxs-lookup"><span data-stu-id="bc195-214">c.</span></span> <span data-ttu-id="bc195-215">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="bc195-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bc195-216">d.</span><span class="sxs-lookup"><span data-stu-id="bc195-216">d.</span></span> <span data-ttu-id="bc195-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bc195-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="bc195-218">Criar um utilizador de teste do GitHub</span><span class="sxs-lookup"><span data-stu-id="bc195-218">Creating a GitHub test user</span></span>

<span data-ttu-id="bc195-219">Na ordem tooenable do Azure AD os utilizadores toolog no GitHub, tem de ser aprovisionados no GitHub.</span><span class="sxs-lookup"><span data-stu-id="bc195-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="bc195-220">No caso de Olá do GitHub, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="bc195-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="bc195-221">**executar de contas de utilizador, tooprovision Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bc195-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc195-222">Inicie sessão no tooyour GitHub site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="bc195-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="bc195-223">Clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="bc195-223">Click **People**.</span></span>

    <span data-ttu-id="bc195-224">![As pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "pessoas")</span><span class="sxs-lookup"><span data-stu-id="bc195-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="bc195-225">Clique em **convite membro**.</span><span class="sxs-lookup"><span data-stu-id="bc195-225">Click **Invite member**.</span></span>

    <span data-ttu-id="bc195-226">![Convidar utilizadores](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "convidar utilizadores")</span><span class="sxs-lookup"><span data-stu-id="bc195-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="bc195-227">No Olá **convite membro** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="bc195-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="bc195-228">a.</span><span class="sxs-lookup"><span data-stu-id="bc195-228">a.</span></span> <span data-ttu-id="bc195-229">No Olá **E-Mail** caixa de texto, endereço de correio eletrónico de Olá de tipo de conta Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc195-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="bc195-230">![Convidar pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "convidar pessoas")</span><span class="sxs-lookup"><span data-stu-id="bc195-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="bc195-231">b.</span><span class="sxs-lookup"><span data-stu-id="bc195-231">b.</span></span> <span data-ttu-id="bc195-232">Clique em **enviar o convite**.</span><span class="sxs-lookup"><span data-stu-id="bc195-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="bc195-233">![Convidar pessoas](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "convidar pessoas")</span><span class="sxs-lookup"><span data-stu-id="bc195-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="bc195-234">titular de conta do Azure Active Directory Olá irá receber um e-mail e siga a tooconfirm uma ligação a respetiva conta para ficar ativa.</span><span class="sxs-lookup"><span data-stu-id="bc195-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bc195-235">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc195-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bc195-236">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooGitHub de acesso.</span><span class="sxs-lookup"><span data-stu-id="bc195-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="bc195-238">**tooassign Britta Simon tooGitHub, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bc195-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="bc195-239">No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="bc195-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="bc195-241">Na lista de aplicações de Olá, selecione **GitHub.com**.</span><span class="sxs-lookup"><span data-stu-id="bc195-241">In hello applications list, select **GitHub.com**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="bc195-243">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="bc195-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="bc195-245">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="bc195-245">Click **Add** button.</span></span> <span data-ttu-id="bc195-246">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bc195-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="bc195-248">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="bc195-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bc195-249">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bc195-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bc195-250">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bc195-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="bc195-251">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="bc195-251">Testing single sign-on</span></span>

<span data-ttu-id="bc195-252">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="bc195-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bc195-253">Ao clicar em mosaico de GitHub Olá no painel de acesso de Olá, deve obter com sessão iniciada tooyour aplicação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="bc195-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="bc195-254">Irá ser iniciar sessão como uma conta de organização, mas, em seguida, é necessário toolog com a sua conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="bc195-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="bc195-255">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bc195-255">Additional resources</span></span>

* [<span data-ttu-id="bc195-256">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc195-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bc195-257">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bc195-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
