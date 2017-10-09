---
title: "Tutorial: Integração do Azure Active Directory com o Tableau Online | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="f11a2-103">Tutorial: Integração do Azure Active Directory com o Tableau Online</span><span class="sxs-lookup"><span data-stu-id="f11a2-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="f11a2-104">Neste tutorial, saiba como toointegrate Tableau Online com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f11a2-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f11a2-105">Integrar o Tableau Online com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="f11a2-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f11a2-106">Pode controlar no Azure AD que tenha acesso tooTableau Online</span><span class="sxs-lookup"><span data-stu-id="f11a2-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="f11a2-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooTableau Online (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f11a2-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f11a2-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f11a2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f11a2-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f11a2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f11a2-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f11a2-110">Prerequisites</span></span>

<span data-ttu-id="f11a2-111">tooconfigure integração do Azure AD com o Tableau Online, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f11a2-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="f11a2-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f11a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f11a2-113">Um Tableau Online-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="f11a2-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f11a2-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f11a2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f11a2-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f11a2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f11a2-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f11a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f11a2-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f11a2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f11a2-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f11a2-118">Scenario description</span></span>
<span data-ttu-id="f11a2-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f11a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f11a2-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="f11a2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f11a2-121">Adicionar Tableau Online a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f11a2-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="f11a2-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f11a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="f11a2-123">Adicionar Tableau Online a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f11a2-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="f11a2-124">tooconfigure Olá integração do Tableau Online com o Azure AD, é necessário tooadd Tableau Online Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="f11a2-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f11a2-125">**tooadd Tableau Online da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f11a2-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f11a2-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f11a2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f11a2-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f11a2-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="f11a2-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f11a2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="f11a2-133">Na caixa de pesquisa de Olá, escreva **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-133">In hello search box, type **Tableau Online**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="f11a2-135">No painel de resultados de Olá, selecione **Tableau Online**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="f11a2-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f11a2-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f11a2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f11a2-138">Nesta secção, configure e teste do Azure AD-início de sessão único com o Tableau Online de acordo com um utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="f11a2-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f11a2-139">Para único início de sessão toowork, do Azure AD tem tooknow que Olá homólogo utilizador Tableau Online é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f11a2-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="f11a2-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados utilizador Tableau Online tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f11a2-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="f11a2-141">No Tableau Online, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="f11a2-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f11a2-142">tooconfigure e teste do Azure AD-início de sessão único com o Tableau Online, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f11a2-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f11a2-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f11a2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f11a2-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f11a2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f11a2-145">**[Criar um utilizador de teste Tableau Online](#creating-a-tableau-online-test-user)**  -toohave um homólogo de Britta Simon Tableau online que está ligado toohello do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="f11a2-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f11a2-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f11a2-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f11a2-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="f11a2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f11a2-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f11a2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f11a2-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="f11a2-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="f11a2-150">**tooconfigure do Azure AD-início de sessão único com o Tableau Online, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f11a2-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="f11a2-151">No Olá portal do Azure, no Olá **Tableau Online** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="f11a2-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f11a2-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="f11a2-155">No Olá **domínio Online Tableau e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f11a2-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="f11a2-157">a.</span><span class="sxs-lookup"><span data-stu-id="f11a2-157">a.</span></span> <span data-ttu-id="f11a2-158">No Olá **URL de início de sessão** caixa de texto, tipo Olá URL:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="f11a2-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="f11a2-159">b.</span><span class="sxs-lookup"><span data-stu-id="f11a2-159">b.</span></span> <span data-ttu-id="f11a2-160">No Olá **identificador** caixa de texto, tipo Olá URL:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="f11a2-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="f11a2-161">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="f11a2-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="f11a2-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="f11a2-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f11a2-165">Na janela do browser diferente, início de sessão tooyour aplicação Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="f11a2-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="f11a2-166">Aceda demasiado**definições** e, em seguida, **autenticação**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="f11a2-168">tooenable SAML, em **tipos de autenticação** secção.</span><span class="sxs-lookup"><span data-stu-id="f11a2-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="f11a2-169">Verifique Olá **-início de sessão único com o SAML** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="f11a2-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="f11a2-171">Desloque para baixo até **ficheiro de metadados de importação para o Tableau Online** secção.</span><span class="sxs-lookup"><span data-stu-id="f11a2-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="f11a2-172">Clique em Procurar e importar o ficheiro de metadados de Olá que transferiu a partir do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f11a2-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="f11a2-173">Em seguida, clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-173">Then, click **Apply**.</span></span>
   
   ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="f11a2-175">No Olá **corresponder asserções** secção, inserir Olá fornecedor de identidade asserção nome correspondente para **endereço de correio eletrónico**, **nome próprio**, e **Apelido** .</span><span class="sxs-lookup"><span data-stu-id="f11a2-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="f11a2-176">tooget estas informações do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="f11a2-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="f11a2-177">a.</span><span class="sxs-lookup"><span data-stu-id="f11a2-177">a.</span></span> <span data-ttu-id="f11a2-178">No Olá portal do Azure, visite no Olá **Tableau Online** página de integração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="f11a2-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="f11a2-179">b.</span><span class="sxs-lookup"><span data-stu-id="f11a2-179">b.</span></span> <span data-ttu-id="f11a2-180">Na secção de atributos de Olá, selecione Olá **"ver e editar todos os outros atributos de utilizador"** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="f11a2-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="f11a2-182">c.</span><span class="sxs-lookup"><span data-stu-id="f11a2-182">c.</span></span> <span data-ttu-id="f11a2-183">Copie o valor de espaço de nomes de Olá para estes atributos: givenname, ao e-mail e apelido utilizando Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f11a2-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Azure AD início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="f11a2-185">d.</span><span class="sxs-lookup"><span data-stu-id="f11a2-185">d.</span></span> <span data-ttu-id="f11a2-186">Clique em **user.givenname** valor</span><span class="sxs-lookup"><span data-stu-id="f11a2-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="f11a2-187">e.</span><span class="sxs-lookup"><span data-stu-id="f11a2-187">e.</span></span> <span data-ttu-id="f11a2-188">Copie o valor de Olá de Olá **espaço de nomes** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f11a2-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="f11a2-190">f.</span><span class="sxs-lookup"><span data-stu-id="f11a2-190">f.</span></span> <span data-ttu-id="f11a2-191">toocopy Olá namesapce os valores e-mail Olá e apelido siga Olá precedente passos.</span><span class="sxs-lookup"><span data-stu-id="f11a2-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="f11a2-192">g.</span><span class="sxs-lookup"><span data-stu-id="f11a2-192">g.</span></span> <span data-ttu-id="f11a2-193">Comutador aplicação Tableau Online toohello, em seguida, definir Olá **atributos Online Tableau** secção da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f11a2-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="f11a2-194">E-mail: **correio** ou **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="f11a2-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="f11a2-195">Nome próprio: **givenname**</span><span class="sxs-lookup"><span data-stu-id="f11a2-195">First name: **givenname**</span></span>
     * <span data-ttu-id="f11a2-196">Apelido: **Apelido**</span><span class="sxs-lookup"><span data-stu-id="f11a2-196">Last name: **surname**</span></span>
   
   ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="f11a2-198">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="f11a2-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f11a2-199">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="f11a2-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f11a2-200">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f11a2-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f11a2-201">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f11a2-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="f11a2-202">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f11a2-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="f11a2-204">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f11a2-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f11a2-205">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f11a2-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f11a2-207">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f11a2-209">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="f11a2-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f11a2-211">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f11a2-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f11a2-213">a.</span><span class="sxs-lookup"><span data-stu-id="f11a2-213">a.</span></span> <span data-ttu-id="f11a2-214">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f11a2-215">b.</span><span class="sxs-lookup"><span data-stu-id="f11a2-215">b.</span></span> <span data-ttu-id="f11a2-216">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f11a2-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f11a2-217">c.</span><span class="sxs-lookup"><span data-stu-id="f11a2-217">c.</span></span> <span data-ttu-id="f11a2-218">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f11a2-219">d.</span><span class="sxs-lookup"><span data-stu-id="f11a2-219">d.</span></span> <span data-ttu-id="f11a2-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="f11a2-221">Criar um utilizador de teste Tableau Online</span><span class="sxs-lookup"><span data-stu-id="f11a2-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="f11a2-222">Nesta secção, vai criar um utilizador chamado Britta Simon Tableau online.</span><span class="sxs-lookup"><span data-stu-id="f11a2-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="f11a2-223">No **Tableau Online**, clique em **definições** e, em seguida, **autenticação** secção.</span><span class="sxs-lookup"><span data-stu-id="f11a2-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="f11a2-224">Desloque para baixo demasiado**selecionar utilizadores** secção.</span><span class="sxs-lookup"><span data-stu-id="f11a2-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="f11a2-225">Clique em **adicionar utilizadores** e, em seguida, **introduza os endereços de correio eletrónico**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="f11a2-227">Selecione **adicionar utilizadores para a autenticação de início de sessão único (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="f11a2-228">No Olá **Introduza endereços de correio eletrónico** adicionar caixa de textobritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="f11a2-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="f11a2-230">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f11a2-231">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f11a2-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f11a2-232">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooTableau Online.</span><span class="sxs-lookup"><span data-stu-id="f11a2-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="f11a2-234">**tooassign Britta Simon tooTableau Online, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f11a2-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="f11a2-235">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="f11a2-237">Na lista de aplicações de Olá, selecione **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="f11a2-239">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f11a2-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="f11a2-241">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="f11a2-241">Click **Add** button.</span></span> <span data-ttu-id="f11a2-242">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f11a2-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="f11a2-244">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="f11a2-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f11a2-245">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f11a2-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f11a2-246">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f11a2-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f11a2-247">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f11a2-247">Testing single sign-on</span></span>

<span data-ttu-id="f11a2-248">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f11a2-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f11a2-249">Ao clicar em mosaico Tableau Online do Olá no painel de acesso de Olá, deve obter aplicações Tableau Online tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="f11a2-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f11a2-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f11a2-250">Additional resources</span></span>

* [<span data-ttu-id="f11a2-251">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f11a2-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f11a2-252">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f11a2-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

