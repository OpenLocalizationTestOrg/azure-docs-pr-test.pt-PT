---
title: "Tutorial: Integração do Azure Active Directory com Teamphoria | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="619cb-103">Tutorial: Integração do Azure Active Directory com Teamphoria</span><span class="sxs-lookup"><span data-stu-id="619cb-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="619cb-104">Neste tutorial, saiba como toointegrate Teamphoria com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="619cb-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="619cb-105">Integrar Teamphoria com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="619cb-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="619cb-106">Pode controlar no Azure AD que tenha acesso tooTeamphoria</span><span class="sxs-lookup"><span data-stu-id="619cb-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="619cb-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooTeamphoria (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="619cb-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="619cb-108">Pode gerir as contas numa localização central - portal de gestão do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="619cb-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="619cb-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="619cb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="619cb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="619cb-110">Prerequisites</span></span>

<span data-ttu-id="619cb-111">integração do Azure AD com Teamphoria tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="619cb-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="619cb-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="619cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="619cb-113">Um Teamphoria início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="619cb-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="619cb-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="619cb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="619cb-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="619cb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="619cb-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="619cb-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="619cb-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="619cb-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="619cb-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="619cb-118">Scenario description</span></span>
<span data-ttu-id="619cb-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="619cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="619cb-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="619cb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="619cb-121">Adicionar Teamphoria da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="619cb-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="619cb-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="619cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="619cb-123">Adicionar Teamphoria da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="619cb-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="619cb-124">tooconfigure Olá integração de Teamphoria com o Azure AD, é necessário tooadd Teamphoria Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="619cb-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="619cb-125">**tooadd Teamphoria da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="619cb-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="619cb-126">No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="619cb-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="619cb-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="619cb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="619cb-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="619cb-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="619cb-131">Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="619cb-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="619cb-133">Na caixa de pesquisa de Olá, escreva **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="619cb-133">In hello search box, type **Teamphoria**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="619cb-135">No painel de resultados de Olá, selecione **Teamphoria**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="619cb-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="619cb-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="619cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="619cb-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Teamphoria com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="619cb-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="619cb-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Teamphoria é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="619cb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="619cb-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Teamphoria tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="619cb-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="619cb-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="619cb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="619cb-142">tooconfigure e teste do Azure AD-início de sessão único com Teamphoria, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="619cb-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="619cb-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="619cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="619cb-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="619cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="619cb-145">**[Criar um utilizador de teste Teamphoria](#creating-a-teamphoria-test-user)**  -toohave um homólogo de Britta Simon no Teamphoria é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="619cb-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="619cb-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="619cb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="619cb-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="619cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="619cb-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="619cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="619cb-149">Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="619cb-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="619cb-150">**tooconfigure do Azure AD-início de sessão único com Teamphoria, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="619cb-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="619cb-151">No portal de gestão do Azure de Olá, no Olá **Teamphoria** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="619cb-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="619cb-153">No Olá **de sessão único-** caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="619cb-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="619cb-155">No Olá **Teamphoria domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="619cb-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="619cb-157">a.</span><span class="sxs-lookup"><span data-stu-id="619cb-157">a.</span></span> <span data-ttu-id="619cb-158">No Olá **URL de início de sessão** caixa de texto, tipo Olá URL Olá seguir o padrão de utilização:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="619cb-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="619cb-159">Tenha em atenção que estes não são valores reais Olá.</span><span class="sxs-lookup"><span data-stu-id="619cb-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="619cb-160">Tiver tooupdate estes valores com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="619cb-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="619cb-161">Contacte [equipa de suporte de cliente Teamphoria](https://www.teamphoria.com/) tooget Olá início de sessão no URL.</span><span class="sxs-lookup"><span data-stu-id="619cb-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="619cb-162">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o certificado de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="619cb-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="619cb-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="619cb-164">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="619cb-166">No Olá **Teamphoria configuração** secção, clique em **configurar Teamphoria** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="619cb-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="619cb-167">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="619cb-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="619cb-169">tooconfigure-início de sessão único em **Teamphoria** lado, a aplicação de Teamphoria tooyour início de sessão como administrador.</span><span class="sxs-lookup"><span data-stu-id="619cb-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="619cb-170">Aceda demasiado**definições de administrador** opção na barra de ferramentas esquerdo Olá e em Olá Olá configurar separador, clique em **ON de início de sessão único** janela de configuração do tooopen Olá SSO.</span><span class="sxs-lookup"><span data-stu-id="619cb-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="619cb-172">Clique em **adicionar novo fornecedor de identidade** opção no formulário do Olá canto superior direito tooopen Olá para adicionar as definições de Olá para SSO.</span><span class="sxs-lookup"><span data-stu-id="619cb-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="619cb-174">Introduza os detalhes de Olá nos campos de Olá, conforme descrito abaixo-</span><span class="sxs-lookup"><span data-stu-id="619cb-174">Enter hello details in hello fields as described below-</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="619cb-176">a.</span><span class="sxs-lookup"><span data-stu-id="619cb-176">a.</span></span> <span data-ttu-id="619cb-177">**NOME a apresentar** : introduza o nome a apresentar Olá do plug-in de Olá na página Administração de Olá.</span><span class="sxs-lookup"><span data-stu-id="619cb-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="619cb-178">b.</span><span class="sxs-lookup"><span data-stu-id="619cb-178">b.</span></span> <span data-ttu-id="619cb-179">**NOME do botão** : nome de Olá do separador Olá que será apresentado na página de início de sessão de Olá para iniciar sessão através do SSO.</span><span class="sxs-lookup"><span data-stu-id="619cb-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="619cb-180">c.</span><span class="sxs-lookup"><span data-stu-id="619cb-180">c.</span></span> <span data-ttu-id="619cb-181">**CERTIFICADO** : Abra Olá certificado transferido anteriormente da Olá portal do Azure no bloco de notas, copiar conteúdo Olá Olá mesmo e cole-o aqui na caixa de Olá.</span><span class="sxs-lookup"><span data-stu-id="619cb-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="619cb-182">d.</span><span class="sxs-lookup"><span data-stu-id="619cb-182">d.</span></span> <span data-ttu-id="619cb-183">**PONTO de entrada** : Olá colar **único início de sessão no URL do serviço SAML** copiados anterior Olá de formulário portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="619cb-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="619cb-184">e.</span><span class="sxs-lookup"><span data-stu-id="619cb-184">e.</span></span> <span data-ttu-id="619cb-185">Mudar a opção de Olá demasiado**ON** e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="619cb-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="619cb-186">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="619cb-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="619cb-187">o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="619cb-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="619cb-189">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="619cb-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="619cb-190">No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="619cb-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="619cb-192">Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="619cb-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="619cb-194">Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="619cb-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="619cb-196">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="619cb-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="619cb-198">a.</span><span class="sxs-lookup"><span data-stu-id="619cb-198">a.</span></span> <span data-ttu-id="619cb-199">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="619cb-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="619cb-200">b.</span><span class="sxs-lookup"><span data-stu-id="619cb-200">b.</span></span> <span data-ttu-id="619cb-201">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="619cb-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="619cb-202">c.</span><span class="sxs-lookup"><span data-stu-id="619cb-202">c.</span></span> <span data-ttu-id="619cb-203">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="619cb-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="619cb-204">d.</span><span class="sxs-lookup"><span data-stu-id="619cb-204">d.</span></span> <span data-ttu-id="619cb-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="619cb-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="619cb-206">Criar um utilizador de teste Teamphoria</span><span class="sxs-lookup"><span data-stu-id="619cb-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="619cb-207">Na ordem tooenable do Azure AD os utilizadores toolog para Teamphoria, têm de ser aprovisionados para Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="619cb-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="619cb-208">No caso de Olá da Teamphoria, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="619cb-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="619cb-209">**executar de contas de utilizador, tooprovision Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="619cb-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="619cb-210">Inicie sessão no tooyour Teamphoria site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="619cb-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="619cb-211">Clique em **ADMIN** definições na barra de ferramentas esquerdo Olá e em Olá **GERIR** separador clique no **utilizadores** página de admin Olá tooopen para os utilizadores.</span><span class="sxs-lookup"><span data-stu-id="619cb-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Adicionar empregado](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="619cb-213">Clique em Olá **MANUAL CONVIDAR** opção.</span><span class="sxs-lookup"><span data-stu-id="619cb-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Convidar pessoas](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="619cb-215">Nesta página, execute os seguintes ação.</span><span class="sxs-lookup"><span data-stu-id="619cb-215">On this page, perform following action.</span></span> 
    
    ![Convidar pessoas](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="619cb-217">a.</span><span class="sxs-lookup"><span data-stu-id="619cb-217">a.</span></span> <span data-ttu-id="619cb-218">No Olá **endereço de correio ELETRÓNICO** caixa de texto, Olá **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="619cb-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="619cb-219">b.</span><span class="sxs-lookup"><span data-stu-id="619cb-219">b.</span></span> <span data-ttu-id="619cb-220">No Olá **nome próprio** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="619cb-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="619cb-221">c.</span><span class="sxs-lookup"><span data-stu-id="619cb-221">c.</span></span> <span data-ttu-id="619cb-222">No Olá **Apelido** caixa de texto, tipo **Simon**.</span><span class="sxs-lookup"><span data-stu-id="619cb-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="619cb-223">d.</span><span class="sxs-lookup"><span data-stu-id="619cb-223">d.</span></span> <span data-ttu-id="619cb-224">Clique em **convite 1 utilizador**.</span><span class="sxs-lookup"><span data-stu-id="619cb-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="619cb-225">Utilizador precisa tooaccept Olá convite tooget criado no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="619cb-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="619cb-226">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="619cb-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="619cb-227">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooTeamphoria de acesso.</span><span class="sxs-lookup"><span data-stu-id="619cb-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="619cb-229">**tooassign Britta Simon tooTeamphoria, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="619cb-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="619cb-230">No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="619cb-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="619cb-232">Na lista de aplicações de Olá, selecione **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="619cb-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="619cb-234">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="619cb-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="619cb-236">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="619cb-236">Click **Add** button.</span></span> <span data-ttu-id="619cb-237">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="619cb-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="619cb-239">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="619cb-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="619cb-240">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="619cb-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="619cb-241">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="619cb-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="619cb-242">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="619cb-242">Testing single sign-on</span></span>

<span data-ttu-id="619cb-243">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="619cb-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="619cb-244">Se pretender testar as definições de início de sessão único, abra o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="619cb-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="619cb-245">Para obter mais detalhes sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="619cb-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="619cb-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="619cb-246">Additional resources</span></span>

* [<span data-ttu-id="619cb-247">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="619cb-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="619cb-248">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="619cb-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

