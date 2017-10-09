---
title: "Tutorial: Integração do Azure Active Directory com TimeOffManager | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a><span data-ttu-id="9eee4-103">Tutorial: Integração do Azure Active Directory com TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="9eee4-103">Tutorial: Azure Active Directory integration with TimeOffManager</span></span>

<span data-ttu-id="9eee4-104">Neste tutorial, saiba como toointegrate TimeOffManager com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9eee4-104">In this tutorial, you learn how toointegrate TimeOffManager with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9eee4-105">Integrar TimeOffManager com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="9eee4-105">Integrating TimeOffManager with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9eee4-106">Pode controlar no Azure AD que tenha acesso tooTimeOffManager</span><span class="sxs-lookup"><span data-stu-id="9eee4-106">You can control in Azure AD who has access tooTimeOffManager</span></span>
- <span data-ttu-id="9eee4-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooTimeOffManager (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eee4-107">You can enable your users tooautomatically get signed-on tooTimeOffManager (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9eee4-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9eee4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9eee4-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9eee4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9eee4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9eee4-110">Prerequisites</span></span>

<span data-ttu-id="9eee4-111">integração do Azure AD com TimeOffManager tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9eee4-111">tooconfigure Azure AD integration with TimeOffManager, you need hello following items:</span></span>

- <span data-ttu-id="9eee4-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eee4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9eee4-113">Um TimeOffManager-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="9eee4-113">A TimeOffManager single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9eee4-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9eee4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9eee4-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9eee4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9eee4-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9eee4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9eee4-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9eee4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9eee4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9eee4-118">Scenario description</span></span>
<span data-ttu-id="9eee4-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9eee4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9eee4-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="9eee4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9eee4-121">Adicionar TimeOffManager da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="9eee4-121">Add TimeOffManager from hello gallery</span></span>
2. <span data-ttu-id="9eee4-122">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9eee4-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-timeoffmanager-from-hello-gallery"></a><span data-ttu-id="9eee4-123">Adicionar TimeOffManager da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="9eee4-123">Add TimeOffManager from hello gallery</span></span>
<span data-ttu-id="9eee4-124">tooconfigure Olá integração de TimeOffManager com o Azure AD, é necessário tooadd TimeOffManager Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="9eee4-124">tooconfigure hello integration of TimeOffManager into Azure AD, you need tooadd TimeOffManager from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9eee4-125">**tooadd TimeOffManager da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9eee4-125">**tooadd TimeOffManager from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eee4-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="9eee4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9eee4-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9eee4-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="9eee4-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9eee4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="9eee4-133">Na caixa de pesquisa de Olá, escreva **TimeOffManager**, selecione **TimeOffManager** do painel de resultados e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="9eee4-133">In hello search box, type **TimeOffManager**, select **TimeOffManager** from result panel and then click **Add** button tooadd hello application.</span></span>

    ![Adicionar a partir da Galeria](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9eee4-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9eee4-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9eee4-136">Nesta secção, configure e teste do Azure AD-início de sessão único com TimeOffManager com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9eee4-136">In this section, you configure and test Azure AD single sign-on with TimeOffManager based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9eee4-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá TimeOffManager é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9eee4-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TimeOffManager is tooa user in Azure AD.</span></span> <span data-ttu-id="9eee4-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá TimeOffManager tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9eee4-138">In other words, a link relationship between an Azure AD user and hello related user in TimeOffManager needs toobe established.</span></span>

<span data-ttu-id="9eee4-139">No TimeOffManager, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="9eee4-139">In TimeOffManager, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9eee4-140">tooconfigure e teste do Azure AD-início de sessão único com TimeOffManager, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="9eee4-140">tooconfigure and test Azure AD single sign-on with TimeOffManager, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9eee4-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="9eee4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9eee4-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9eee4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9eee4-143">**[Criar um utilizador de teste TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave um homólogo de Britta Simon no TimeOffManager é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="9eee4-143">**[Create a TimeOffManager test user](#create-a-timeoffmanager-test-user)** - toohave a counterpart of Britta Simon in TimeOffManager that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9eee4-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="9eee4-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9eee4-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="9eee4-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9eee4-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9eee4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9eee4-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação TimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="9eee4-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TimeOffManager application.</span></span>

<span data-ttu-id="9eee4-148">**tooconfigure do Azure AD-início de sessão único com TimeOffManager, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9eee4-148">**tooconfigure Azure AD single sign-on with TimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eee4-149">No Olá portal do Azure, no Olá **TimeOffManager** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-149">In hello Azure portal, on hello **TimeOffManager** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="9eee4-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="9eee4-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![SAML com base em início de sessão](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. <span data-ttu-id="9eee4-153">No Olá **TimeOffManager domínio e os URLs** secção, execute o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="9eee4-153">On hello **TimeOffManager Domain and URLs** section, perform hello following:</span></span>

     ![Secção TimeOffManager domínio e os URLs](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    <span data-ttu-id="9eee4-155">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span><span class="sxs-lookup"><span data-stu-id="9eee4-155">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9eee4-156">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="9eee4-156">This value is not real.</span></span> <span data-ttu-id="9eee4-157">Atualize este valor com o URL de resposta real Olá.</span><span class="sxs-lookup"><span data-stu-id="9eee4-157">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="9eee4-158">Pode obter este valor de **início de sessão único na página Definições** que é explicado mais tarde no tutorial Olá ou contacte [equipa de suporte de TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).</span><span class="sxs-lookup"><span data-stu-id="9eee4-158">You can get this value from **Single Sign on settings page** which is explained later in hello tutorial or Contact [TimeOffManager support team](http://www.timeoffmanager.com/contact-us.aspx).</span></span>
 
4. <span data-ttu-id="9eee4-159">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="9eee4-159">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Secção de certificado de assinatura de SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. <span data-ttu-id="9eee4-161">o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooTimeOffManger à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.</span><span class="sxs-lookup"><span data-stu-id="9eee4-161">hello objective of this section is toooutline how tooenable users tooauthenticate tooTimeOffManger with their account in Azure AD using federation based on hello SAML protocol.</span></span>
    
    <span data-ttu-id="9eee4-162">A aplicação de TimeOffManger espera asserções de SAML Olá num formato específico, que requer tooadd atributo personalizado mapeamentos tooyour configuração SAML do token de atributos.</span><span class="sxs-lookup"><span data-stu-id="9eee4-162">Your TimeOffManger application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="9eee4-163">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="9eee4-163">hello following screenshot shows an example for this.</span></span>

    <span data-ttu-id="9eee4-164">![atributos de token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "atributos token saml")</span><span class="sxs-lookup"><span data-stu-id="9eee4-164">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")</span></span>
    
    | <span data-ttu-id="9eee4-165">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="9eee4-165">Attribute Name</span></span> | <span data-ttu-id="9eee4-166">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="9eee4-166">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="9eee4-167">nome próprio</span><span class="sxs-lookup"><span data-stu-id="9eee4-167">Firstname</span></span> |<span data-ttu-id="9eee4-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="9eee4-168">User.givenname</span></span> |
    | <span data-ttu-id="9eee4-169">Apelido</span><span class="sxs-lookup"><span data-stu-id="9eee4-169">Lastname</span></span> |<span data-ttu-id="9eee4-170">User.Surname</span><span class="sxs-lookup"><span data-stu-id="9eee4-170">User.surname</span></span> |
    | <span data-ttu-id="9eee4-171">E-mail</span><span class="sxs-lookup"><span data-stu-id="9eee4-171">Email</span></span> |<span data-ttu-id="9eee4-172">User.Mail</span><span class="sxs-lookup"><span data-stu-id="9eee4-172">User.mail</span></span> |
    
    <span data-ttu-id="9eee4-173">a.</span><span class="sxs-lookup"><span data-stu-id="9eee4-173">a.</span></span>  <span data-ttu-id="9eee4-174">Para cada linha de dados na tabela de Olá acima, clique em **adicionar o atributo de utilizador**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-174">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="9eee4-175">![atributos de token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "atributos token saml")</span><span class="sxs-lookup"><span data-stu-id="9eee4-175">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")</span></span>
    
    <span data-ttu-id="9eee4-176">![atributos de token SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "atributos token saml")</span><span class="sxs-lookup"><span data-stu-id="9eee4-176">![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")</span></span>
    
    <span data-ttu-id="9eee4-177">b.</span><span class="sxs-lookup"><span data-stu-id="9eee4-177">b.</span></span>  <span data-ttu-id="9eee4-178">No Olá **nome de atributo** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="9eee4-178">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="9eee4-179">c.</span><span class="sxs-lookup"><span data-stu-id="9eee4-179">c.</span></span>  <span data-ttu-id="9eee4-180">No Olá **valor do atributo** caixa de texto, o valor do atributo Olá selecione mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="9eee4-180">In hello **Attribute Value** textbox, select hello attribute  value shown for that row.</span></span>
    
    <span data-ttu-id="9eee4-181">d.</span><span class="sxs-lookup"><span data-stu-id="9eee4-181">d.</span></span>  <span data-ttu-id="9eee4-182">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-182">Click **Ok**.</span></span>
    
6. <span data-ttu-id="9eee4-183">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="9eee4-183">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="9eee4-185">No Olá **TimeOffManager configuração** secção, clique em **configurar TimeOffManager** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="9eee4-185">On hello **TimeOffManager Configuration** section, click **Configure TimeOffManager** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9eee4-186">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9eee4-186">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Secção de configuração de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. <span data-ttu-id="9eee4-188">Numa janela do browser web diferente, inicie sessão no site da sua empresa TimeOffManager como administrador.</span><span class="sxs-lookup"><span data-stu-id="9eee4-188">In a different web browser window, log into your TimeOffManager company site as an administrator.</span></span>

9. <span data-ttu-id="9eee4-189">Aceda demasiado**conta \> opções de conta \> as definições de início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-189">Go too**Account \> Account Options \> Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="9eee4-190">![Single Sign-On definições](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "único as definições de início de sessão")</span><span class="sxs-lookup"><span data-stu-id="9eee4-190">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Single Sign-On Settings")</span></span>
7. <span data-ttu-id="9eee4-191">No Olá **as definições de início de sessão único** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9eee4-191">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="9eee4-192">![Single Sign-On definições](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "único as definições de início de sessão")</span><span class="sxs-lookup"><span data-stu-id="9eee4-192">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="9eee4-193">a.</span><span class="sxs-lookup"><span data-stu-id="9eee4-193">a.</span></span> <span data-ttu-id="9eee4-194">Abra o seu certificado codificado base-64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole Olá certificados inteira no **certificado x. 509** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="9eee4-194">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>
   
   <span data-ttu-id="9eee4-195">b.</span><span class="sxs-lookup"><span data-stu-id="9eee4-195">b.</span></span> <span data-ttu-id="9eee4-196">No **Idp emissor** caixa de texto, colar Olá valor **ID de entidade de SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9eee4-196">In **Idp Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="9eee4-197">c.</span><span class="sxs-lookup"><span data-stu-id="9eee4-197">c.</span></span> <span data-ttu-id="9eee4-198">No **URL de ponto final do IdP** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9eee4-198">In **IdP Endpoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="9eee4-199">d.</span><span class="sxs-lookup"><span data-stu-id="9eee4-199">d.</span></span> <span data-ttu-id="9eee4-200">Como **impor SAML**, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-200">As **Enforce SAML**, select **No**.</span></span>
   
   <span data-ttu-id="9eee4-201">e.</span><span class="sxs-lookup"><span data-stu-id="9eee4-201">e.</span></span> <span data-ttu-id="9eee4-202">Como **Auto-criar utilizadores**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-202">As **Auto-Create Users**, select **Yes**.</span></span>
   
   <span data-ttu-id="9eee4-203">f.</span><span class="sxs-lookup"><span data-stu-id="9eee4-203">f.</span></span> <span data-ttu-id="9eee4-204">No **URL de fim de sessão** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9eee4-204">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="9eee4-205">g.</span><span class="sxs-lookup"><span data-stu-id="9eee4-205">g.</span></span> <span data-ttu-id="9eee4-206">Clique em **guardar alterações**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-206">click **Save Changes**.</span></span>

11. <span data-ttu-id="9eee4-207">No **as definições de início de sessão único** página cópia Olá valor **asserção URL do serviço de consumidor** e colá-lo na Olá **URL de resposta** caixa de texto em **TimeOffManager Domínios e URLs** secção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9eee4-207">In **Single Sign on settings** page, copy hello value of **Assertion Consumer Service URL** and paste it in hello **Reply URL** text box under **TimeOffManager Domain and URLs** section in Azure portal.</span></span> 

      <span data-ttu-id="9eee4-208">![Single Sign-On definições](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "único as definições de início de sessão")</span><span class="sxs-lookup"><span data-stu-id="9eee4-208">![Single Sign-On Settings](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Single Sign-On Settings")</span></span>

> [!TIP]
> <span data-ttu-id="9eee4-209">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="9eee4-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9eee4-210">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="9eee4-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9eee4-211">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9eee4-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9eee4-212">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eee4-212">Create an Azure AD test user</span></span>
<span data-ttu-id="9eee4-213">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9eee4-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="9eee4-215">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9eee4-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eee4-216">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="9eee4-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9eee4-218">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utilizadores e grupos--> todos os utilizadores](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9eee4-220">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="9eee4-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Botão Adicionar](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9eee4-222">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9eee4-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Página de caixa de diálogo de utilizador](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9eee4-224">a.</span><span class="sxs-lookup"><span data-stu-id="9eee4-224">a.</span></span> <span data-ttu-id="9eee4-225">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9eee4-226">b.</span><span class="sxs-lookup"><span data-stu-id="9eee4-226">b.</span></span> <span data-ttu-id="9eee4-227">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9eee4-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9eee4-228">c.</span><span class="sxs-lookup"><span data-stu-id="9eee4-228">c.</span></span> <span data-ttu-id="9eee4-229">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9eee4-230">d.</span><span class="sxs-lookup"><span data-stu-id="9eee4-230">d.</span></span> <span data-ttu-id="9eee4-231">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-231">Click **Create**.</span></span>
 
### <a name="create-a-timeoffmanager-test-user"></a><span data-ttu-id="9eee4-232">Criar um utilizador de teste TimeOffManager</span><span class="sxs-lookup"><span data-stu-id="9eee4-232">Create a TimeOffManager test user</span></span>

<span data-ttu-id="9eee4-233">Na ordem tooenable do Azure AD os utilizadores toolog para TimeOffManager, têm de ser tooTimeOffManager aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="9eee4-233">In order tooenable Azure AD users toolog into TimeOffManager, they must be provisioned tooTimeOffManager.</span></span>  

<span data-ttu-id="9eee4-234">TimeOffManager apenas suporta o aprovisionamento de utilizadores do tempo.</span><span class="sxs-lookup"><span data-stu-id="9eee4-234">TimeOffManager supports just in time user provisioning.</span></span> <span data-ttu-id="9eee4-235">Não há nenhum item de ação para si.</span><span class="sxs-lookup"><span data-stu-id="9eee4-235">There is no action item for you.</span></span>  

<span data-ttu-id="9eee4-236">são adicionados automaticamente utilizadores de Olá durante Olá primeiro início de sessão utilizando o início de sessão único em.</span><span class="sxs-lookup"><span data-stu-id="9eee4-236">hello users are added automatically during hello first login using single sign on.</span></span>

>[!NOTE]
><span data-ttu-id="9eee4-237">Pode utilizar quaisquer outras TimeOffManager utilizador conta criação ferramentas ou APIs fornecidas pelo TimeOffManager tooprovision contas de utilizador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9eee4-237">You can use any other TimeOffManager user account creation tools or APIs provided by TimeOffManager tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9eee4-238">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eee4-238">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9eee4-239">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooTimeOffManager.</span><span class="sxs-lookup"><span data-stu-id="9eee4-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTimeOffManager.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="9eee4-241">**tooassign Britta Simon tooTimeOffManager, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="9eee4-241">**tooassign Britta Simon tooTimeOffManager, perform hello following steps:**</span></span>

1. <span data-ttu-id="9eee4-242">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="9eee4-244">Na lista de aplicações de Olá, selecione **TimeOffManager**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-244">In hello applications list, select **TimeOffManager**.</span></span>

    ![TimeOffManager na lista de aplicações](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. <span data-ttu-id="9eee4-246">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9eee4-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="9eee4-248">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="9eee4-248">Click **Add** button.</span></span> <span data-ttu-id="9eee4-249">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9eee4-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="9eee4-251">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="9eee4-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9eee4-252">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9eee4-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9eee4-253">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9eee4-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9eee4-254">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="9eee4-254">Test single sign-on</span></span>

<span data-ttu-id="9eee4-255">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="9eee4-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9eee4-256">Ao clicar em mosaico de TimeOffManager Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour TimeOffManager aplicação.</span><span class="sxs-lookup"><span data-stu-id="9eee4-256">When you click hello TimeOffManager tile in hello Access Panel, you should get automatically signed-on tooyour TimeOffManager application.</span></span> <span data-ttu-id="9eee4-257">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9eee4-257">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9eee4-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9eee4-258">Additional resources</span></span>

* [<span data-ttu-id="9eee4-259">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9eee4-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9eee4-260">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9eee4-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

