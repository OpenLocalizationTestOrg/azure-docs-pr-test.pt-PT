---
title: "Tutorial: Integração do Azure Active Directory com o T & Express I | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e T & I Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="6e499-103">Tutorial: Integração do Azure Active Directory com o T & I Express</span><span class="sxs-lookup"><span data-stu-id="6e499-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="6e499-104">Neste tutorial, saiba como toointegrate T & I Express com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e499-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e499-105">Integrar o T & I Express com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="6e499-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6e499-106">Pode controlar no Azure AD que tenha tooT acesso & I Express</span><span class="sxs-lookup"><span data-stu-id="6e499-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="6e499-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooT & I Express (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e499-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e499-108">Pode gerir as contas numa localização central - portal de gestão do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="6e499-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="6e499-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e499-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e499-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6e499-110">Prerequisites</span></span>

<span data-ttu-id="6e499-111">integração do Azure AD com o T & I Express tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6e499-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="6e499-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e499-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e499-113">Um Redireccionamen & I Express início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="6e499-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e499-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6e499-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e499-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6e499-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e499-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="6e499-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6e499-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e499-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e499-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6e499-118">Scenario description</span></span>
<span data-ttu-id="6e499-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6e499-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e499-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="6e499-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e499-121">Adicionar e & I Express na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6e499-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="6e499-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6e499-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="6e499-123">Adicionar e & I Express na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6e499-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="6e499-124">tooconfigure Olá integração d & I Express com o Azure AD, terá de tooadd T & I Express Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="6e499-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6e499-125">**tooadd T & I Express a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e499-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e499-126">No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6e499-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6e499-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6e499-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6e499-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6e499-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="6e499-131">Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="6e499-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="6e499-133">Na caixa de pesquisa de Olá, escreva **T & I Express**.</span><span class="sxs-lookup"><span data-stu-id="6e499-133">In hello search box, type **T&E Express**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="6e499-135">No painel de resultados de Olá, selecione **T & I Express**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="6e499-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e499-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6e499-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e499-138">Nesta secção, configure e teste do Azure AD-início de sessão único com o T & I Express com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6e499-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e499-139">Para único início de sessão toowork, do Azure AD tem tooknow que Olá homólogo utilizador T & I Express é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e499-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="6e499-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados com o utilizador no T & I Express toobe necessidades estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6e499-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="6e499-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** T & I Express.</span><span class="sxs-lookup"><span data-stu-id="6e499-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="6e499-142">tooconfigure e teste do Azure AD-início de sessão único com o T & I Express, necessitará de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6e499-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6e499-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="6e499-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6e499-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e499-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e499-145">**[Criar um utilizador de teste T & I Express](#creating-a-te-express-test-user)**  -toohave um homólogo de Britta Simon T & I Express que é a representação de toohello ligado do Azure AD de forma.</span><span class="sxs-lookup"><span data-stu-id="6e499-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="6e499-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6e499-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e499-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="6e499-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e499-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6e499-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e499-149">Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação T & I Express.</span><span class="sxs-lookup"><span data-stu-id="6e499-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="6e499-150">**tooconfigure do Azure AD-início de sessão único com o T & I Express, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e499-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e499-151">No portal de gestão do Azure de Olá, no Olá **T & I Express** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="6e499-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="6e499-153">No Olá **de sessão único-** caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6e499-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="6e499-155">No Olá **T & I Express domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6e499-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="6e499-157">a.</span><span class="sxs-lookup"><span data-stu-id="6e499-157">a.</span></span> <span data-ttu-id="6e499-158">No Olá **identificador** caixa de texto, valor de tipo de Olá como:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="6e499-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="6e499-159">b.</span><span class="sxs-lookup"><span data-stu-id="6e499-159">b.</span></span> <span data-ttu-id="6e499-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="6e499-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e499-161">Tenha em atenção que estes não são valores reais Olá.</span><span class="sxs-lookup"><span data-stu-id="6e499-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="6e499-162">Tiver tooupdate estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="6e499-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6e499-163">Aqui sugerimos toouse Olá exclusivo valor da cadeia no Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="6e499-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="6e499-164">Contacte [equipa de suporte de T & I Express](http://www.tyeexpress.com/contacto.aspx) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="6e499-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="6e499-165">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6e499-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="6e499-167">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="6e499-167">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6e499-169">tooconfigure-início de sessão único em **T & i rápida** lado, início de sessão toohello T & aplicação rápida do i sem SAML único início de sessão com credenciais do administrador.</span><span class="sxs-lookup"><span data-stu-id="6e499-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="6e499-170">Em Olá **Admin** separador, clique em **domínio SAML** página de definições do tooOpen Olá SAML.</span><span class="sxs-lookup"><span data-stu-id="6e499-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="6e499-172">Selecione Olá **Activar(Activate)** opção de **não** demasiado**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="6e499-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="6e499-173">No Olá **metadados do fornecedor de identidade** caixa de texto, colar Olá metadados XML que tiver donwloaded a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e499-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="6e499-175">Clique em Olá **Guardar(Save)** no botão Definições de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="6e499-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e499-176">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e499-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e499-177">o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e499-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="6e499-179">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e499-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e499-180">No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6e499-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6e499-182">Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="6e499-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e499-184">Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e499-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e499-186">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6e499-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e499-188">a.</span><span class="sxs-lookup"><span data-stu-id="6e499-188">a.</span></span> <span data-ttu-id="6e499-189">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e499-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e499-190">b.</span><span class="sxs-lookup"><span data-stu-id="6e499-190">b.</span></span> <span data-ttu-id="6e499-191">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e499-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e499-192">c.</span><span class="sxs-lookup"><span data-stu-id="6e499-192">c.</span></span> <span data-ttu-id="6e499-193">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="6e499-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6e499-194">d.</span><span class="sxs-lookup"><span data-stu-id="6e499-194">d.</span></span> <span data-ttu-id="6e499-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6e499-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="6e499-196">Criar um utilizador de teste T & I Express</span><span class="sxs-lookup"><span data-stu-id="6e499-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="6e499-197">Na ordem tooenable do Azure AD os utilizadores toolog em T & I Express, têm de ser aprovisionados para T & I Express.</span><span class="sxs-lookup"><span data-stu-id="6e499-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="6e499-198">Em caso de T & I Express, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="6e499-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="6e499-199">**executar de contas de utilizador, tooprovision Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e499-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e499-200">Inicie sessão no tooyour T & I Express site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="6e499-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="6e499-201">Na etiqueta do administrador, clique na página principal do utilizadores tooopen Olá utilizadores.</span><span class="sxs-lookup"><span data-stu-id="6e499-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Adicionar empregado](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="6e499-203">Na página inicial de Olá, clique em  **+**  utilizadores de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="6e499-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Adicionar empregado](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="6e499-205">Introduza todos os detalhes de obrigatório Olá, tal como pedido no formulário de Olá e clique em Olá guardar botão toosave Olá detalhes.</span><span class="sxs-lookup"><span data-stu-id="6e499-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Adicionar empregado](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Adicionar empregado](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6e499-208">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e499-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6e499-209">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooT acesso & I Express.</span><span class="sxs-lookup"><span data-stu-id="6e499-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="6e499-211">**tooassign tooT Britta Simon & I Express, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6e499-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="6e499-212">No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6e499-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="6e499-214">Na lista de aplicações de Olá, selecione **T & I Express**.</span><span class="sxs-lookup"><span data-stu-id="6e499-214">In hello applications list, select **T&E Express**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="6e499-216">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6e499-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="6e499-218">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="6e499-218">Click **Add** button.</span></span> <span data-ttu-id="6e499-219">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e499-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="6e499-221">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="6e499-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6e499-222">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e499-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e499-223">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6e499-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e499-224">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6e499-224">Testing single sign-on</span></span>

<span data-ttu-id="6e499-225">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="6e499-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6e499-226">Ao clicar Olá T & I Express mosaico no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour T & I Express desta aplicação.</span><span class="sxs-lookup"><span data-stu-id="6e499-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e499-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6e499-227">Additional resources</span></span>

* [<span data-ttu-id="6e499-228">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e499-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e499-229">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e499-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

