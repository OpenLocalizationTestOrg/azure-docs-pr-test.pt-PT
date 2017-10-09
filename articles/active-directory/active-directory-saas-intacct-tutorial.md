---
title: "Tutorial: Integração do Azure Active Directory com Intacct | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="88e82-103">Tutorial: Integração do Azure Active Directory com Intacct</span><span class="sxs-lookup"><span data-stu-id="88e82-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="88e82-104">Neste tutorial, saiba como toointegrate Intacct com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88e82-104">In this tutorial, you learn how toointegrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88e82-105">Integrar Intacct com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="88e82-105">Integrating Intacct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="88e82-106">Pode controlar no Azure AD que tenha acesso tooIntacct</span><span class="sxs-lookup"><span data-stu-id="88e82-106">You can control in Azure AD who has access tooIntacct</span></span>
- <span data-ttu-id="88e82-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooIntacct (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e82-107">You can enable your users tooautomatically get signed-on tooIntacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88e82-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="88e82-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="88e82-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88e82-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88e82-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="88e82-110">Prerequisites</span></span>

<span data-ttu-id="88e82-111">integração do Azure AD com Intacct tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="88e82-111">tooconfigure Azure AD integration with Intacct, you need hello following items:</span></span>

- <span data-ttu-id="88e82-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88e82-113">Um Intacct-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="88e82-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88e82-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="88e82-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88e82-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="88e82-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88e82-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="88e82-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88e82-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88e82-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88e82-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="88e82-118">Scenario description</span></span>
<span data-ttu-id="88e82-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="88e82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88e82-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="88e82-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88e82-121">Adicionar Intacct da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="88e82-121">Adding Intacct from hello gallery</span></span>
2. <span data-ttu-id="88e82-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="88e82-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-hello-gallery"></a><span data-ttu-id="88e82-123">Adicionar Intacct da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="88e82-123">Adding Intacct from hello gallery</span></span>
<span data-ttu-id="88e82-124">tooconfigure Olá integração de Intacct com o Azure AD, é necessário tooadd Intacct Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="88e82-124">tooconfigure hello integration of Intacct into Azure AD, you need tooadd Intacct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="88e82-125">**tooadd Intacct da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="88e82-125">**tooadd Intacct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="88e82-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="88e82-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="88e82-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="88e82-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="88e82-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="88e82-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="88e82-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="88e82-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="88e82-133">Na caixa de pesquisa de Olá, escreva **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="88e82-133">In hello search box, type **Intacct**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="88e82-135">No painel de resultados de Olá, selecione **Intacct**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="88e82-135">In hello results panel, select **Intacct**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88e82-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="88e82-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88e82-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Intacct com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="88e82-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="88e82-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Intacct é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88e82-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intacct is tooa user in Azure AD.</span></span> <span data-ttu-id="88e82-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Intacct tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="88e82-140">In other words, a link relationship between an Azure AD user and hello related user in Intacct needs toobe established.</span></span>

<span data-ttu-id="88e82-141">No Intacct, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="88e82-141">In Intacct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="88e82-142">tooconfigure e teste do Azure AD-início de sessão único com Intacct, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="88e82-142">tooconfigure and test Azure AD single sign-on with Intacct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="88e82-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="88e82-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="88e82-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="88e82-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88e82-145">**[Criar um utilizador de teste Intacct](#creating-an-intacct-test-user)**  -toohave um homólogo de Britta Simon no Intacct é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="88e82-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - toohave a counterpart of Britta Simon in Intacct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="88e82-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="88e82-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88e82-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="88e82-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88e82-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="88e82-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88e82-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Intacct.</span><span class="sxs-lookup"><span data-stu-id="88e82-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="88e82-150">**tooconfigure do Azure AD-início de sessão único com Intacct, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="88e82-150">**tooconfigure Azure AD single sign-on with Intacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="88e82-151">No Olá portal do Azure, no Olá **Intacct** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="88e82-151">In hello Azure portal, on hello **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="88e82-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="88e82-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="88e82-155">No Olá **Intacct domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="88e82-155">On hello **Intacct Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="88e82-157">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:</span><span class="sxs-lookup"><span data-stu-id="88e82-157">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="88e82-158">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="88e82-158">This value is not real.</span></span> <span data-ttu-id="88e82-159">Atualize este valor com o URL de resposta real Olá.</span><span class="sxs-lookup"><span data-stu-id="88e82-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="88e82-160">Contacte [equipa de suporte de Intacct](https://us.intacct.com/support) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="88e82-160">Contact [Intacct support team](https://us.intacct.com/support) tooget this value.</span></span>

4. <span data-ttu-id="88e82-161">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="88e82-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="88e82-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="88e82-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88e82-165">No Olá **Intacct configuração** secção, clique em **configurar Intacct** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="88e82-165">On hello **Intacct Configuration** section, click **Configure Intacct** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="88e82-166">Olá cópia **ID de entidade de SAML e único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="88e82-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="88e82-168">Numa janela do browser web diferente, inicie sessão no site da empresa tooyour Intacct como administrador.</span><span class="sxs-lookup"><span data-stu-id="88e82-168">In a different web browser window, sign in tooyour Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="88e82-169">Clique em Olá **empresa** separador e, em seguida, clique em **informações da empresa**.</span><span class="sxs-lookup"><span data-stu-id="88e82-169">Click hello **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="88e82-170">![Empresa](./media/active-directory-saas-intacct-tutorial/ic790037.png "empresa")</span><span class="sxs-lookup"><span data-stu-id="88e82-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="88e82-171">Clique em Olá **segurança** separador e, em seguida, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="88e82-171">Click hello **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="88e82-172">![Segurança](./media/active-directory-saas-intacct-tutorial/ic790038.png "segurança")</span><span class="sxs-lookup"><span data-stu-id="88e82-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="88e82-173">No Olá **início de sessão (SSO) único** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="88e82-173">In hello **Single sign on (SSO)** section, perform hello following steps:</span></span>

    <span data-ttu-id="88e82-174">![Início de sessão único](./media/active-directory-saas-intacct-tutorial/ic790039.png "início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="88e82-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="88e82-175">a.</span><span class="sxs-lookup"><span data-stu-id="88e82-175">a.</span></span> <span data-ttu-id="88e82-176">Selecione **ativar o início de sessão único em**.</span><span class="sxs-lookup"><span data-stu-id="88e82-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="88e82-177">b.</span><span class="sxs-lookup"><span data-stu-id="88e82-177">b.</span></span> <span data-ttu-id="88e82-178">Como **tipo de fornecedor de identidade**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="88e82-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="88e82-179">c.</span><span class="sxs-lookup"><span data-stu-id="88e82-179">c.</span></span> <span data-ttu-id="88e82-180">No **URL do emissor** caixa de texto, colar Olá valor **ID de entidade de SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="88e82-180">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="88e82-181">d.</span><span class="sxs-lookup"><span data-stu-id="88e82-181">d.</span></span> <span data-ttu-id="88e82-182">No **URL de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="88e82-182">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="88e82-183">e.</span><span class="sxs-lookup"><span data-stu-id="88e82-183">e.</span></span> <span data-ttu-id="88e82-184">Abra o **base-64** codificado certificado no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado** caixa.</span><span class="sxs-lookup"><span data-stu-id="88e82-184">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** box.</span></span>
   
    <span data-ttu-id="88e82-185">f.</span><span class="sxs-lookup"><span data-stu-id="88e82-185">f.</span></span> <span data-ttu-id="88e82-186">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="88e82-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="88e82-187">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="88e82-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="88e82-188">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="88e82-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="88e82-189">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88e82-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88e82-190">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e82-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="88e82-191">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="88e82-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="88e82-193">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="88e82-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="88e82-194">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="88e82-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88e82-196">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="88e82-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88e82-198">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="88e82-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88e82-200">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="88e82-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88e82-202">a.</span><span class="sxs-lookup"><span data-stu-id="88e82-202">a.</span></span> <span data-ttu-id="88e82-203">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88e82-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88e82-204">b.</span><span class="sxs-lookup"><span data-stu-id="88e82-204">b.</span></span> <span data-ttu-id="88e82-205">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="88e82-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="88e82-206">c.</span><span class="sxs-lookup"><span data-stu-id="88e82-206">c.</span></span> <span data-ttu-id="88e82-207">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="88e82-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="88e82-208">d.</span><span class="sxs-lookup"><span data-stu-id="88e82-208">d.</span></span> <span data-ttu-id="88e82-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="88e82-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="88e82-210">Criar um utilizador de teste Intacct</span><span class="sxs-lookup"><span data-stu-id="88e82-210">Creating an Intacct test user</span></span>

<span data-ttu-id="88e82-211">tooset cópias de segurança utilizadores do Azure AD, para poderem iniciar sessão tooIntacct, estes têm de ser aprovisionados para Intacct.</span><span class="sxs-lookup"><span data-stu-id="88e82-211">tooset up Azure AD users so they can sign in tooIntacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="88e82-212">Intacct, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="88e82-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="88e82-213">**contas de utilizador tooprovision, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="88e82-213">**tooprovision user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="88e82-214">Inicie sessão no tooyour **Intacct** inquilino.</span><span class="sxs-lookup"><span data-stu-id="88e82-214">Sign in tooyour **Intacct** tenant.</span></span>

2. <span data-ttu-id="88e82-215">Clique em Olá **empresa** separador e, em seguida, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="88e82-215">Click hello **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="88e82-216">![Os utilizadores](./media/active-directory-saas-intacct-tutorial/ic790041.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="88e82-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="88e82-217">Clique em Olá **adicionar** separador.</span><span class="sxs-lookup"><span data-stu-id="88e82-217">Click hello **Add** tab.</span></span>

    <span data-ttu-id="88e82-218">![Adicionar](./media/active-directory-saas-intacct-tutorial/ic790042.png "adicionar")</span><span class="sxs-lookup"><span data-stu-id="88e82-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="88e82-219">No Olá **informações do utilizador** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="88e82-219">In hello **User Information** section, perform hello following steps:</span></span>

    <span data-ttu-id="88e82-220">![Informações do utilizador](./media/active-directory-saas-intacct-tutorial/ic790043.png "informações do utilizador")</span><span class="sxs-lookup"><span data-stu-id="88e82-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="88e82-221">a.</span><span class="sxs-lookup"><span data-stu-id="88e82-221">a.</span></span> <span data-ttu-id="88e82-222">Introduza Olá **ID de utilizador**, Olá **Apelido**, **nome próprio**, Olá **endereço de correio eletrónico**, Olá **título**, e Olá **Phone** de uma conta do Azure AD que pretenda tooprovision incorporar Olá **informações do utilizador** secção.</span><span class="sxs-lookup"><span data-stu-id="88e82-222">Enter hello **User ID**, hello **Last name**, **First name**, hello **Email address**, hello **Title**, and hello **Phone** of an Azure AD account that you want tooprovision into hello **User Information** section.</span></span>

    <span data-ttu-id="88e82-223">b.</span><span class="sxs-lookup"><span data-stu-id="88e82-223">b.</span></span> <span data-ttu-id="88e82-224">Selecione Olá **privilégios de administrador** de uma conta do Azure AD que pretende que o tooprovision.</span><span class="sxs-lookup"><span data-stu-id="88e82-224">Select hello **Admin privileges** of an Azure AD account that you want tooprovision.</span></span>
   
    <span data-ttu-id="88e82-225">c.</span><span class="sxs-lookup"><span data-stu-id="88e82-225">c.</span></span> <span data-ttu-id="88e82-226">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="88e82-226">Click **Save**.</span></span> <span data-ttu-id="88e82-227">titular da conta do Olá do Azure AD recebe uma mensagem de e-mail e segue um tooconfirm ligação respetiva conta para ficar ativa.</span><span class="sxs-lookup"><span data-stu-id="88e82-227">hello Azure AD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="88e82-228">tooprovision contas de utilizador do Azure AD, pode utilizar outras ferramentas de criação de conta de utilizador Intacct ou APIs fornecidas pelo Intacct.</span><span class="sxs-lookup"><span data-stu-id="88e82-228">tooprovision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="88e82-229">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="88e82-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="88e82-230">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooIntacct.</span><span class="sxs-lookup"><span data-stu-id="88e82-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntacct.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="88e82-232">**tooassign Britta Simon tooIntacct, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="88e82-232">**tooassign Britta Simon tooIntacct, perform hello following steps:**</span></span>

1. <span data-ttu-id="88e82-233">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="88e82-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="88e82-235">Na lista de aplicações de Olá, selecione **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="88e82-235">In hello applications list, select **Intacct**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="88e82-237">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="88e82-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="88e82-239">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="88e82-239">Click **Add** button.</span></span> <span data-ttu-id="88e82-240">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="88e82-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="88e82-242">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="88e82-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="88e82-243">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="88e82-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88e82-244">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="88e82-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88e82-245">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="88e82-245">Testing single sign-on</span></span>

<span data-ttu-id="88e82-246">Nesta secção, teste configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="88e82-246">In this section, you test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="88e82-247">Ao clicar em mosaico de Intacct Olá no painel de acesso de Olá, esta deve ser iniciada automaticamente no tooyour Intacct aplicação.</span><span class="sxs-lookup"><span data-stu-id="88e82-247">When you click hello Intacct tile in hello Access Panel, you should be automatically signed in tooyour Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88e82-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="88e82-248">Additional resources</span></span>

* [<span data-ttu-id="88e82-249">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88e82-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88e82-250">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88e82-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

