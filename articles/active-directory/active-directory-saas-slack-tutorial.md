---
title: "Tutorial: Integração do Azure Active Directory com Slack | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Slack."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="3877a-103">Tutorial: Integração do Azure Active Directory com Slack</span><span class="sxs-lookup"><span data-stu-id="3877a-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="3877a-104">Neste tutorial, saiba como toointegrate Slack com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3877a-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3877a-105">Integrar Slack com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="3877a-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3877a-106">Pode controlar no Azure AD que tenha acesso tooSlack</span><span class="sxs-lookup"><span data-stu-id="3877a-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="3877a-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSlack (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3877a-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3877a-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3877a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3877a-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3877a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3877a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3877a-110">Prerequisites</span></span>

<span data-ttu-id="3877a-111">integração do Azure AD com Slack tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3877a-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="3877a-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3877a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3877a-113">Um Slack-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="3877a-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3877a-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3877a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3877a-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3877a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3877a-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3877a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3877a-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3877a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3877a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3877a-118">Scenario description</span></span>
<span data-ttu-id="3877a-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3877a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3877a-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="3877a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3877a-121">Adicionar Slack da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="3877a-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="3877a-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="3877a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="3877a-123">Adicionar Slack da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="3877a-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="3877a-124">integração de Olá tooconfigure de Slack com o Azure AD, é necessário tooadd Slack Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="3877a-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3877a-125">**tooadd Slack da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3877a-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3877a-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="3877a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3877a-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3877a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3877a-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="3877a-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="3877a-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3877a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="3877a-133">Na caixa de pesquisa de Olá, escreva **Slack**.</span><span class="sxs-lookup"><span data-stu-id="3877a-133">In hello search box, type **Slack**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="3877a-135">No painel de resultados de Olá, selecione **Slack**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="3877a-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3877a-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="3877a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3877a-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Slack com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3877a-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3877a-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Slack é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3877a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="3877a-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Slack tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3877a-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="3877a-141">No Slack, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="3877a-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3877a-142">tooconfigure e teste do Azure AD-início de sessão único com Slack, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="3877a-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3877a-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="3877a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3877a-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3877a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3877a-145">**[Criar um utilizador de teste Slack](#creating-a-slack-test-user)**  -toohave um homólogo de Britta Simon no Slack é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="3877a-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3877a-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="3877a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3877a-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="3877a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3877a-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="3877a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3877a-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Slack.</span><span class="sxs-lookup"><span data-stu-id="3877a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="3877a-150">**tooconfigure do Azure AD-início de sessão único com Slack, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3877a-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="3877a-151">No Olá portal do Azure, no Olá **Slack** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="3877a-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="3877a-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="3877a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="3877a-155">No Olá **Slack domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3877a-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="3877a-157">a.</span><span class="sxs-lookup"><span data-stu-id="3877a-157">a.</span></span> <span data-ttu-id="3877a-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="3877a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="3877a-159">b.</span><span class="sxs-lookup"><span data-stu-id="3877a-159">b.</span></span> <span data-ttu-id="3877a-160">No Olá **identificador** caixa de texto, tipo Olá URL:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="3877a-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3877a-161">o valor de Olá não é real.</span><span class="sxs-lookup"><span data-stu-id="3877a-161">hello value is not real.</span></span> <span data-ttu-id="3877a-162">Tem de valor de Olá tooupdate com Olá real no URL de sessão.</span><span class="sxs-lookup"><span data-stu-id="3877a-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="3877a-163">Contacte [equipa de suporte Slack](https://slack.com/help/contact) valor de Olá tooget</span><span class="sxs-lookup"><span data-stu-id="3877a-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="3877a-164">Aplicação slack espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="3877a-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="3877a-165">Configure Olá seguintes afirmações para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="3877a-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="3877a-166">Pode gerir os valores de Olá destes atributos a partir de Olá "**atributos de utilizador**" secção na página de integração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="3877a-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="3877a-167">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="3877a-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="3877a-169">No Olá **atributos de utilizador** secção em Olá **de sessão único-** caixa de diálogo, selecione **user.mail** como **identificador de utilizador** e para cada linha visível na tabela de Olá abaixo, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3877a-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="3877a-170">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="3877a-170">Attribute Name</span></span> | <span data-ttu-id="3877a-171">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="3877a-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="3877a-172">first_name</span><span class="sxs-lookup"><span data-stu-id="3877a-172">first_name</span></span> | <span data-ttu-id="3877a-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="3877a-173">user.givenname</span></span> |
    | <span data-ttu-id="3877a-174">last_name</span><span class="sxs-lookup"><span data-stu-id="3877a-174">last_name</span></span> | <span data-ttu-id="3877a-175">User.Surname</span><span class="sxs-lookup"><span data-stu-id="3877a-175">user.surname</span></span> |
    | <span data-ttu-id="3877a-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="3877a-176">User.Email</span></span> | <span data-ttu-id="3877a-177">User.Mail</span><span class="sxs-lookup"><span data-stu-id="3877a-177">user.mail</span></span> |  
    | <span data-ttu-id="3877a-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="3877a-178">User.Username</span></span> | <span data-ttu-id="3877a-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3877a-179">user.userprincipalname</span></span> |

    <span data-ttu-id="3877a-180">a.</span><span class="sxs-lookup"><span data-stu-id="3877a-180">a.</span></span> <span data-ttu-id="3877a-181">Clique em **atributo** tooopen **Editar atributo** diálogo caixa e efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3877a-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="3877a-183">a.</span><span class="sxs-lookup"><span data-stu-id="3877a-183">a.</span></span> <span data-ttu-id="3877a-184">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="3877a-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="3877a-185">b.</span><span class="sxs-lookup"><span data-stu-id="3877a-185">b.</span></span> <span data-ttu-id="3877a-186">De Olá **valor** lista, o valor do atributo Olá selecione mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="3877a-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="3877a-187">c.</span><span class="sxs-lookup"><span data-stu-id="3877a-187">c.</span></span> <span data-ttu-id="3877a-188">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="3877a-188">Click **OK**</span></span>

6. <span data-ttu-id="3877a-189">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="3877a-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="3877a-191">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="3877a-191">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3877a-193">No Olá **Slack configuração** secção, clique em **configurar Slack** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="3877a-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3877a-194">Olá cópia **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="3877a-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="3877a-196">Numa janela do browser web diferente, inicie sessão no site de empresa Slack tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="3877a-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="3877a-197">Navegue demasiado**Microsoft Azure AD** , visite demasiado**definições Team**.</span><span class="sxs-lookup"><span data-stu-id="3877a-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="3877a-199">No Olá **definições Team** secção, clique em Olá **autenticação** separador e, em seguida, clique em **alterar definições**.</span><span class="sxs-lookup"><span data-stu-id="3877a-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="3877a-201">No Olá **definições de autenticação SAML** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3877a-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="3877a-203">a.</span><span class="sxs-lookup"><span data-stu-id="3877a-203">a.</span></span>  <span data-ttu-id="3877a-204">No Olá **SAML 2.0 ponto final de protocolo HTTP ()** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3877a-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3877a-205">b.</span><span class="sxs-lookup"><span data-stu-id="3877a-205">b.</span></span>  <span data-ttu-id="3877a-206">No Olá **emissor do fornecedor de identidade** caixa de texto, colar Olá valor **ID de entidade de SAML**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3877a-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3877a-207">c.</span><span class="sxs-lookup"><span data-stu-id="3877a-207">c.</span></span>  <span data-ttu-id="3877a-208">Abra o ficheiro de certificado transferido no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado público** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3877a-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="3877a-209">d.</span><span class="sxs-lookup"><span data-stu-id="3877a-209">d.</span></span> <span data-ttu-id="3877a-210">Configure Olá acima três definições conforme adequado para a sua equipa Slack.</span><span class="sxs-lookup"><span data-stu-id="3877a-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="3877a-211">Para obter mais informações sobre as definições de Olá, determinar Olá **guia de configuração do Slack SSO** aqui.</span><span class="sxs-lookup"><span data-stu-id="3877a-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="3877a-212">e.</span><span class="sxs-lookup"><span data-stu-id="3877a-212">e.</span></span>  <span data-ttu-id="3877a-213">Clique em **Guardar configuração**.</span><span class="sxs-lookup"><span data-stu-id="3877a-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="3877a-214">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="3877a-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3877a-215">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="3877a-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3877a-216">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3877a-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3877a-217">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3877a-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="3877a-218">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3877a-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="3877a-220">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3877a-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3877a-221">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="3877a-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3877a-223">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="3877a-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3877a-225">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="3877a-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3877a-227">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3877a-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3877a-229">a.</span><span class="sxs-lookup"><span data-stu-id="3877a-229">a.</span></span> <span data-ttu-id="3877a-230">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3877a-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3877a-231">b.</span><span class="sxs-lookup"><span data-stu-id="3877a-231">b.</span></span> <span data-ttu-id="3877a-232">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3877a-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3877a-233">c.</span><span class="sxs-lookup"><span data-stu-id="3877a-233">c.</span></span> <span data-ttu-id="3877a-234">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="3877a-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3877a-235">d.</span><span class="sxs-lookup"><span data-stu-id="3877a-235">d.</span></span> <span data-ttu-id="3877a-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3877a-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="3877a-237">Criar um utilizador de teste Slack</span><span class="sxs-lookup"><span data-stu-id="3877a-237">Creating a Slack test user</span></span>

<span data-ttu-id="3877a-238">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Slack.</span><span class="sxs-lookup"><span data-stu-id="3877a-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="3877a-239">Slack suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.</span><span class="sxs-lookup"><span data-stu-id="3877a-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="3877a-240">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="3877a-240">There is no action item for you in this section.</span></span> <span data-ttu-id="3877a-241">Um novo utilizador é criado durante uma tentativa tooaccess Slack se não existir ainda.</span><span class="sxs-lookup"><span data-stu-id="3877a-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="3877a-242">Se precisar de um utilizador de toocreate manualmente, terá de tooContact [equipa de suporte Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="3877a-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3877a-243">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3877a-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3877a-244">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSlack.</span><span class="sxs-lookup"><span data-stu-id="3877a-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="3877a-246">**tooassign Britta Simon tooSlack, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3877a-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="3877a-247">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="3877a-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="3877a-249">Na lista de aplicações de Olá, selecione **Slack**.</span><span class="sxs-lookup"><span data-stu-id="3877a-249">In hello applications list, select **Slack**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="3877a-251">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3877a-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="3877a-253">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="3877a-253">Click **Add** button.</span></span> <span data-ttu-id="3877a-254">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3877a-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="3877a-256">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="3877a-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3877a-257">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3877a-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3877a-258">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3877a-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3877a-259">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="3877a-259">Testing single sign-on</span></span>

<span data-ttu-id="3877a-260">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3877a-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3877a-261">Ao clicar em mosaico Slack Olá no painel de acesso de Olá, deve obter aplicações Slack tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="3877a-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3877a-262">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3877a-262">Additional resources</span></span>

* [<span data-ttu-id="3877a-263">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3877a-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3877a-264">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3877a-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

