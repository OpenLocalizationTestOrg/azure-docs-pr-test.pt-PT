---
title: "Tutorial: Integração do Azure Active Directory com o Procore SSO | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Procore SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="ead9f-103">Tutorial: Integração do Azure Active Directory com o Procore SSO</span><span class="sxs-lookup"><span data-stu-id="ead9f-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="ead9f-104">Neste tutorial, saiba como toointegrate Procore SSO ao Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ead9f-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ead9f-105">Integrar o Procore SSO com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="ead9f-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ead9f-106">Pode controlar no Azure AD que tenha acesso tooProcore SSO</span><span class="sxs-lookup"><span data-stu-id="ead9f-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="ead9f-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooProcore SSO (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ead9f-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ead9f-108">Pode gerir as contas numa localização central - portal de gestão do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="ead9f-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="ead9f-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ead9f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="ead9f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ead9f-110">Prerequisites</span></span>

<span data-ttu-id="ead9f-111">integração do Azure AD com o Procore SSO tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ead9f-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="ead9f-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ead9f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ead9f-113">Um Procore SSO início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="ead9f-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ead9f-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ead9f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ead9f-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ead9f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ead9f-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="ead9f-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="ead9f-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ead9f-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ead9f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ead9f-118">Scenario description</span></span>
<span data-ttu-id="ead9f-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ead9f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ead9f-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="ead9f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ead9f-121">A adição de Procore SSO de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="ead9f-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="ead9f-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="ead9f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="ead9f-123">A adição de Procore SSO de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="ead9f-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="ead9f-124">tooconfigure Olá integração do Procore SSO com o Azure AD, é necessário tooadd Procore SSO Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="ead9f-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ead9f-125">**tooadd SSO Procore da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ead9f-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ead9f-126">No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="ead9f-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ead9f-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ead9f-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="ead9f-131">Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="ead9f-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="ead9f-133">Na caixa de pesquisa de Olá, escreva **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-133">In hello search box, type **Procore SSO**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="ead9f-135">No painel de resultados de Olá, selecione **Procore SSO**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="ead9f-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ead9f-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="ead9f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ead9f-138">Nesta secção, configure e teste do Azure AD-início de sessão único com o SSO Procore com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ead9f-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ead9f-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Procore SSO é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ead9f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="ead9f-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Procore SSO tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ead9f-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="ead9f-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** em Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="ead9f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="ead9f-142">tooconfigure e teste do Azure AD-início de sessão único com o Procore SSO, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ead9f-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ead9f-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="ead9f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ead9f-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ead9f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ead9f-145">**[Criar um utilizador de teste de Procore SSO](#creating-a-procore-sso-test-user)**  -toohave um homólogo de Britta Simon em Procore SSO que é a representação de toohello ligado do Azure AD de forma.</span><span class="sxs-lookup"><span data-stu-id="ead9f-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="ead9f-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="ead9f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ead9f-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="ead9f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ead9f-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="ead9f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ead9f-149">Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação Procore SSO.</span><span class="sxs-lookup"><span data-stu-id="ead9f-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="ead9f-150">**tooconfigure do Azure AD-início de sessão único com o Procore SSO, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ead9f-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="ead9f-151">No portal de gestão do Azure de Olá, no Olá **Procore SSO** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="ead9f-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="ead9f-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="ead9f-155">No Olá **Procore de SSO de domínio e os URLs** secção, hello utilizador não tem tooperform quaisquer passos conforme Olá aplicação já está pré-integrada com o Azure.</span><span class="sxs-lookup"><span data-stu-id="ead9f-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="ead9f-157">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ead9f-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="ead9f-159">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="ead9f-159">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ead9f-161">No Olá **Procore SSO configuração** secção, clique em **configurar Procore SSO** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="ead9f-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ead9f-162">Olá cópia **ID de entidade de SAML e único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ead9f-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="ead9f-164">tooconfigure-início de sessão único em **Procore SSO** lado, o site de empresa procore de tooyour de início de sessão como administrador.</span><span class="sxs-lookup"><span data-stu-id="ead9f-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="ead9f-165">Na lista de caixa de ferramentas de Olá pendente, clique em **Admin** página de definições do tooopen Olá SSO.</span><span class="sxs-lookup"><span data-stu-id="ead9f-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="ead9f-167">Colar Olá valores nas caixas de Olá como descrito abaixo-</span><span class="sxs-lookup"><span data-stu-id="ead9f-167">Paste hello values in hello boxes as described below-</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="ead9f-169">a.</span><span class="sxs-lookup"><span data-stu-id="ead9f-169">a.</span></span> <span data-ttu-id="ead9f-170">No Olá **único início de sessão no URL do emissor** caixa, cole Olá copiado de ID de entidade de SAML do Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ead9f-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="ead9f-171">b.</span><span class="sxs-lookup"><span data-stu-id="ead9f-171">b.</span></span> <span data-ttu-id="ead9f-172">No Olá **sessão SAML no URL de destino** caixa, cole Olá único início de sessão no URL do serviço SAML copiado Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ead9f-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="ead9f-173">c.</span><span class="sxs-lookup"><span data-stu-id="ead9f-173">c.</span></span> <span data-ttu-id="ead9f-174">Agora abra Olá **XML de metadados** transferido acima de Olá portal do Azure e cópia Olá certficate na tag de Olá denominado **certificado X509**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="ead9f-175">Olá colar copiados valor para Olá **certificado de início de sessão único x509** caixa.</span><span class="sxs-lookup"><span data-stu-id="ead9f-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="ead9f-176">Clique em **guardar alterações**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="ead9f-177">Depois destas definições, necessita de toosend Olá **nome de domínio** (por exemplo **contoso.com**) através do qual está a iniciar sessão em Procore toohello [equipa de suporte Procore](https://support.procore.com/) quais serão Ative a SSO federado desse domínio.</span><span class="sxs-lookup"><span data-stu-id="ead9f-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ead9f-178">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ead9f-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="ead9f-179">o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ead9f-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="ead9f-181">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ead9f-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ead9f-182">No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="ead9f-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ead9f-184">Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="ead9f-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ead9f-186">Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ead9f-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ead9f-188">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ead9f-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ead9f-190">a.</span><span class="sxs-lookup"><span data-stu-id="ead9f-190">a.</span></span> <span data-ttu-id="ead9f-191">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ead9f-192">b.</span><span class="sxs-lookup"><span data-stu-id="ead9f-192">b.</span></span> <span data-ttu-id="ead9f-193">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ead9f-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ead9f-194">c.</span><span class="sxs-lookup"><span data-stu-id="ead9f-194">c.</span></span> <span data-ttu-id="ead9f-195">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ead9f-196">d.</span><span class="sxs-lookup"><span data-stu-id="ead9f-196">d.</span></span> <span data-ttu-id="ead9f-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="ead9f-198">Criar um utilizador de teste de Procore SSO</span><span class="sxs-lookup"><span data-stu-id="ead9f-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="ead9f-199">Siga Olá abaixo passos toocreate um utilizador de teste Procore no seu lado.</span><span class="sxs-lookup"><span data-stu-id="ead9f-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="ead9f-200">Site de empresa procore de tooyour de início de sessão como administrador.</span><span class="sxs-lookup"><span data-stu-id="ead9f-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="ead9f-201">Na lista de caixa de ferramentas de Olá pendente, clique em **diretório** página de diretório do tooopen Olá da empresa.</span><span class="sxs-lookup"><span data-stu-id="ead9f-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="ead9f-203">Clique em **adicionar uma pessoa** opção formulário de Olá tooopen e introduza efetuar os seguintes opções -</span><span class="sxs-lookup"><span data-stu-id="ead9f-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="ead9f-205">a.</span><span class="sxs-lookup"><span data-stu-id="ead9f-205">a.</span></span> <span data-ttu-id="ead9f-206">No Olá **nome próprio** caixa de texto, nome do próprio do utilizador do tipo como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="ead9f-207">b.</span><span class="sxs-lookup"><span data-stu-id="ead9f-207">b.</span></span> <span data-ttu-id="ead9f-208">No Olá **Apelido** caixa de texto, apelido do utilizador do tipo como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="ead9f-209">c.</span><span class="sxs-lookup"><span data-stu-id="ead9f-209">c.</span></span> <span data-ttu-id="ead9f-210">No Olá **endereço de correio eletrónico** como endereço de correio eletrónico do utilizador do tipo de caixa de texto,  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="ead9f-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="ead9f-211">d.</span><span class="sxs-lookup"><span data-stu-id="ead9f-211">d.</span></span> <span data-ttu-id="ead9f-212">Selecione **permissão modelo** como **aplicar o modelo de permissão mais tarde**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="ead9f-213">e.</span><span class="sxs-lookup"><span data-stu-id="ead9f-213">e.</span></span> <span data-ttu-id="ead9f-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-214">Click **Create**.</span></span>

4. <span data-ttu-id="ead9f-215">Verifique e atualizar os detalhes de Olá para Olá recentemente adicionadas contacto.</span><span class="sxs-lookup"><span data-stu-id="ead9f-215">Check and update hello details for hello newly added contact.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="ead9f-217">Clique em **guardar e enviar Invitiation** (se for necessário um convite através de correio) ou **guardar** (guardar diretamente) registo de utilizador de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ead9f-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ead9f-219">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ead9f-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ead9f-220">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo tooProcore respetivo acesso SSO.</span><span class="sxs-lookup"><span data-stu-id="ead9f-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="ead9f-222">**tooassign Britta Simon tooProcore SSO, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ead9f-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="ead9f-223">No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="ead9f-225">Na lista de aplicações de Olá, selecione **Procore SSO**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="ead9f-227">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ead9f-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="ead9f-229">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="ead9f-229">Click **Add** button.</span></span> <span data-ttu-id="ead9f-230">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ead9f-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="ead9f-232">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="ead9f-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ead9f-233">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ead9f-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ead9f-234">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ead9f-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ead9f-235">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="ead9f-235">Testing single sign-on</span></span>

<span data-ttu-id="ead9f-236">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="ead9f-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ead9f-237">Se pretender testar as definições de início de sessão único, abra o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="ead9f-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ead9f-238">Para obter mais detalhes sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="ead9f-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="ead9f-239">Ao clicar em mosaico de Procore SSO Olá no painel de acesso de Olá, deve obter a aplicação de Procore SSO tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="ead9f-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ead9f-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ead9f-240">Additional resources</span></span>

* [<span data-ttu-id="ead9f-241">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ead9f-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ead9f-242">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ead9f-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

