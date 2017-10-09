---
title: "Tutorial: Integração do Azure Active Directory com o SSO Kantega para FishEye/Crucible | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Kantega SSO para FishEye/Crucible."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: fdd68b5e90c3e2893887650735429a33e21ffa68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a><span data-ttu-id="a4550-103">Tutorial: Integração do Azure Active Directory com o SSO Kantega para FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="a4550-103">Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible</span></span>

<span data-ttu-id="a4550-104">Neste tutorial, saiba como toointegrate Kantega SSO para FishEye/Crucible com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4550-104">In this tutorial, you learn how toointegrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4550-105">Integrar Kantega SSO para FishEye/Crucible com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="a4550-105">Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a4550-106">Pode controlar no Azure AD que tenha acesso tooKantega SSO para FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="a4550-106">You can control in Azure AD who has access tooKantega SSO for FishEye/Crucible</span></span>
- <span data-ttu-id="a4550-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooKantega SSO para FishEye/Crucible (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4550-107">You can enable your users tooautomatically get signed-on tooKantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a4550-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a4550-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a4550-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4550-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4550-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4550-110">Prerequisites</span></span>

<span data-ttu-id="a4550-111">integração do Azure AD com o SSO Kantega para FishEye/Crucible tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a4550-111">tooconfigure Azure AD integration with Kantega SSO for FishEye/Crucible, you need hello following items:</span></span>

- <span data-ttu-id="a4550-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4550-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a4550-113">Um SSO Kantega para FishEye/Crucible-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="a4550-113">A Kantega SSO for FishEye/Crucible single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4550-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a4550-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a4550-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a4550-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a4550-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a4550-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a4550-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4550-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4550-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a4550-118">Scenario description</span></span>
<span data-ttu-id="a4550-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a4550-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4550-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="a4550-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4550-121">Adicionar Kantega SSO para FishEye/Crucible da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a4550-121">Adding Kantega SSO for FishEye/Crucible from hello gallery</span></span>
2. <span data-ttu-id="a4550-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a4550-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-fisheyecrucible-from-hello-gallery"></a><span data-ttu-id="a4550-123">Adicionar Kantega SSO para FishEye/Crucible da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a4550-123">Adding Kantega SSO for FishEye/Crucible from hello gallery</span></span>
<span data-ttu-id="a4550-124">tooconfigure Olá integração do SSO Kantega para FishEye/Crucible com o Azure AD, terá de tooadd Kantega SSO para FishEye/Crucible Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="a4550-124">tooconfigure hello integration of Kantega SSO for FishEye/Crucible into Azure AD, you need tooadd Kantega SSO for FishEye/Crucible from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a4550-125">**tooadd Kantega SSO para FishEye/Crucible da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a4550-125">**tooadd Kantega SSO for FishEye/Crucible from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4550-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a4550-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a4550-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a4550-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a4550-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a4550-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="a4550-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a4550-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="a4550-133">Na caixa de pesquisa de Olá, escreva **Kantega SSO para FishEye/Crucible**.</span><span class="sxs-lookup"><span data-stu-id="a4550-133">In hello search box, type **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. <span data-ttu-id="a4550-135">No painel de resultados de Olá, selecione **Kantega SSO para FishEye/Crucible**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="a4550-135">In hello results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4550-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a4550-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4550-138">Nesta secção, configure e teste do Azure AD-início de sessão único com o SSO Kantega para FishEye/Crucible com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a4550-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a4550-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Kantega SSO para FishEye/Crucible é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4550-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for FishEye/Crucible is tooa user in Azure AD.</span></span> <span data-ttu-id="a4550-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Kantega SSO para FishEye/Crucible tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a4550-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for FishEye/Crucible needs toobe established.</span></span>

<span data-ttu-id="a4550-141">Em Kantega SSO para FishEye/Crucible, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="a4550-141">In Kantega SSO for FishEye/Crucible, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a4550-142">tooconfigure e teste do Azure AD-início de sessão único com o Kantega SSO para FishEye/Crucible, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a4550-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a4550-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a4550-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a4550-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4550-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4550-145">**[Criar um SSO Kantega para o utilizador de teste de FishEye/Crucible](#creating-a-kantega-sso-for-fisheyecrucible-test-user)**  -toohave um homólogo de Britta Simon em Kantega SSO para FishEye/Crucible é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="a4550-145">**[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a4550-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a4550-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4550-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="a4550-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4550-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a4550-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a4550-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua SSO Kantega para aplicação FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="a4550-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.</span></span>

<span data-ttu-id="a4550-150">**tooconfigure do Azure AD-início de sessão único com o SSO Kantega para FishEye/Crucible, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a4550-150">**tooconfigure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4550-151">No Olá portal do Azure, no Olá **Kantega SSO para FishEye/Crucible** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="a4550-151">In hello Azure portal, on hello **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="a4550-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a4550-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. <span data-ttu-id="a4550-155">No **IDP** iniciada modo, Olá **Kantega SSO para o domínio de FishEye/Crucible e URLs** secção efetuar Olá passo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4550-155">In **IDP** initiated mode, on hello **Kantega SSO for FishEye/Crucible Domain and URLs** section perform hello following step :</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    <span data-ttu-id="a4550-157">a.</span><span class="sxs-lookup"><span data-stu-id="a4550-157">a.</span></span> <span data-ttu-id="a4550-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="a4550-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="a4550-159">b.</span><span class="sxs-lookup"><span data-stu-id="a4550-159">b.</span></span> <span data-ttu-id="a4550-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="a4550-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="a4550-161">No **SP** modo iniciado, verifique **Mostrar avançadas definições de URL** e efetuar Olá passo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4550-161">In **SP** initiated mode, check **Show advanced URL settings** and perform hello following step:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    <span data-ttu-id="a4550-163">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="a4550-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a4550-164">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="a4550-164">These values are not real.</span></span> <span data-ttu-id="a4550-165">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="a4550-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a4550-166">Estes valores são recebidos durante a configuração de Olá do plug-in de FishEye/Crucible que é explicado mais tarde no tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="a4550-166">These values are recieved during hello configuration of FishEye/Crucible plugin which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="a4550-167">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a4550-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. <span data-ttu-id="a4550-169">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="a4550-169">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a4550-171">Numa janela do browser web diferente, inicie sessão no tooyour FishEye/Crucible no servidor no local como administrador.</span><span class="sxs-lookup"><span data-stu-id="a4550-171">In a different web browser window, log in tooyour FishEye/Crucible on premise server as an administrator.</span></span>

8. <span data-ttu-id="a4550-172">Paire o rato sobre o ícone e clique em Olá **suplementos**.</span><span class="sxs-lookup"><span data-stu-id="a4550-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. <span data-ttu-id="a4550-174">Na secção de definições do sistema, clique em **localizar novos suplementos**.</span><span class="sxs-lookup"><span data-stu-id="a4550-174">Under System Settings section, click **Find new add-ons**.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. <span data-ttu-id="a4550-176">Pesquisa **Kantega SSO para Crucible** e clique em **instalar** botão tooinstall Olá Plug-in SAML de novo.</span><span class="sxs-lookup"><span data-stu-id="a4550-176">Search **Kantega SSO for Crucible** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. <span data-ttu-id="a4550-178">inicia a instalação de plug-in de Olá.</span><span class="sxs-lookup"><span data-stu-id="a4550-178">hello plugin installation starts.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. <span data-ttu-id="a4550-180">Depois de concluída a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="a4550-180">Once hello installation is complete.</span></span> <span data-ttu-id="a4550-181">Clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="a4550-181">Click **Close**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. <span data-ttu-id="a4550-183">Clique em **Gerir**.</span><span class="sxs-lookup"><span data-stu-id="a4550-183">Click **Manage**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. <span data-ttu-id="a4550-185">Clique em **configurar** tooconfigure Olá novo plug-in.</span><span class="sxs-lookup"><span data-stu-id="a4550-185">Click **Configure** tooconfigure hello new plugin.</span></span>  

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. <span data-ttu-id="a4550-187">No Olá **SAML** secção.</span><span class="sxs-lookup"><span data-stu-id="a4550-187">In hello **SAML** section.</span></span> <span data-ttu-id="a4550-188">Selecione **Azure Active Directory (Azure AD)** de Olá **Adicionar fornecedor de identidade** pendente.</span><span class="sxs-lookup"><span data-stu-id="a4550-188">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. <span data-ttu-id="a4550-190">Selecione o nível de subscrição como **básico**.</span><span class="sxs-lookup"><span data-stu-id="a4550-190">Select subscription level as **Basic**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. <span data-ttu-id="a4550-192">No Olá **as propriedades da aplicação** secção, execute os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a4550-192">On hello **App properties** section, perform following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    <span data-ttu-id="a4550-194">a.</span><span class="sxs-lookup"><span data-stu-id="a4550-194">a.</span></span> <span data-ttu-id="a4550-195">Olá cópia **URI de ID de aplicação** valor e utilizá-lo como **identificador, o URL de resposta e o URL de início de sessão** no Olá **Kantega SSO para o domínio de FishEye/Crucible e URLs** secção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4550-195">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="a4550-196">b.</span><span class="sxs-lookup"><span data-stu-id="a4550-196">b.</span></span> <span data-ttu-id="a4550-197">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a4550-197">Click **Next**.</span></span>

18. <span data-ttu-id="a4550-198">No Olá **importar metadados** secção, execute os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a4550-198">On hello **Metadata import** section, perform following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    <span data-ttu-id="a4550-200">a.</span><span class="sxs-lookup"><span data-stu-id="a4550-200">a.</span></span> <span data-ttu-id="a4550-201">Selecione **ficheiro de metadados no meu computador**e o ficheiro de metadados do carregamento, que transferiu a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4550-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="a4550-202">b.</span><span class="sxs-lookup"><span data-stu-id="a4550-202">b.</span></span> <span data-ttu-id="a4550-203">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a4550-203">Click **Next**.</span></span>

19. <span data-ttu-id="a4550-204">No Olá **localização nome e SSO** secção, execute os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a4550-204">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    <span data-ttu-id="a4550-206">a.</span><span class="sxs-lookup"><span data-stu-id="a4550-206">a.</span></span> <span data-ttu-id="a4550-207">Adicione o nome do fornecedor de identidade de Olá no **nome do fornecedor de identidade** caixa de texto (por exemplo, do Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4550-207">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="a4550-208">b.</span><span class="sxs-lookup"><span data-stu-id="a4550-208">b.</span></span> <span data-ttu-id="a4550-209">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a4550-209">Click **Next**.</span></span>

20. <span data-ttu-id="a4550-210">Verificar o certificado de assinatura de Olá e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a4550-210">Verify hello Signing certificate and click **Next**.</span></span>    

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. <span data-ttu-id="a4550-212">No Olá **contas de utilizador FishEye** secção, execute os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a4550-212">On hello **FishEye user accounts** section, perform following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    <span data-ttu-id="a4550-214">a.</span><span class="sxs-lookup"><span data-stu-id="a4550-214">a.</span></span> <span data-ttu-id="a4550-215">Selecione **criar utilizadores no diretório interno do FishEye se for necessário** e introduza o nome adequado Olá do grupo de Olá para os utilizadores (pode ser não vários.</span><span class="sxs-lookup"><span data-stu-id="a4550-215">Select **Create users in FishEye's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="a4550-216">de grupos separados por vírgulas).</span><span class="sxs-lookup"><span data-stu-id="a4550-216">of groups separated by comma).</span></span>

    <span data-ttu-id="a4550-217">b.</span><span class="sxs-lookup"><span data-stu-id="a4550-217">b.</span></span> <span data-ttu-id="a4550-218">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a4550-218">Click **Next**.</span></span>

22. <span data-ttu-id="a4550-219">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a4550-219">Click **Finish**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. <span data-ttu-id="a4550-221">No Olá **conhecido domínios para o Azure AD** secção, execute os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a4550-221">On hello **Known domains for Azure AD** section, perform following steps:</span></span>   

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    <span data-ttu-id="a4550-223">a.</span><span class="sxs-lookup"><span data-stu-id="a4550-223">a.</span></span> <span data-ttu-id="a4550-224">Selecione **conhecido domínios** do painel esquerdo do Olá da página Olá.</span><span class="sxs-lookup"><span data-stu-id="a4550-224">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="a4550-225">b.</span><span class="sxs-lookup"><span data-stu-id="a4550-225">b.</span></span> <span data-ttu-id="a4550-226">Introduza o nome de domínio no Olá **conhecido domínios** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a4550-226">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="a4550-227">c.</span><span class="sxs-lookup"><span data-stu-id="a4550-227">c.</span></span> <span data-ttu-id="a4550-228">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a4550-228">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="a4550-229">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="a4550-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a4550-230">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="a4550-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a4550-231">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a4550-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4550-232">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4550-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4550-233">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4550-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="a4550-235">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a4550-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4550-236">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a4550-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4550-238">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a4550-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4550-240">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="a4550-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4550-242">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a4550-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4550-244">a.</span><span class="sxs-lookup"><span data-stu-id="a4550-244">a.</span></span> <span data-ttu-id="a4550-245">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4550-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4550-246">b.</span><span class="sxs-lookup"><span data-stu-id="a4550-246">b.</span></span> <span data-ttu-id="a4550-247">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a4550-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a4550-248">c.</span><span class="sxs-lookup"><span data-stu-id="a4550-248">c.</span></span> <span data-ttu-id="a4550-249">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="a4550-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a4550-250">d.</span><span class="sxs-lookup"><span data-stu-id="a4550-250">d.</span></span> <span data-ttu-id="a4550-251">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a4550-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a><span data-ttu-id="a4550-252">Criar um SSO Kantega para o utilizador de teste de FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="a4550-252">Creating a Kantega SSO for FishEye/Crucible test user</span></span>

<span data-ttu-id="a4550-253">tooenable do Azure AD os utilizadores toolog no tooFishEye/Crucible, estes têm de ser aprovisionados para FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="a4550-253">tooenable Azure AD users toolog in tooFishEye/Crucible, they must be provisioned into FishEye/Crucible.</span></span> <span data-ttu-id="a4550-254">Em Kantega SSO para FishEye/Crucible, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a4550-254">In Kantega SSO for FishEye/Crucible, provisioning is a manual task.</span></span>

<span data-ttu-id="a4550-255">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a4550-255">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4550-256">Inicie sessão no tooyour Crucible no servidor no local como administrador.</span><span class="sxs-lookup"><span data-stu-id="a4550-256">Log in tooyour Crucible on premise server as an administrator.</span></span>

2. <span data-ttu-id="a4550-257">Paire o rato sobre o ícone e clique em Olá **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a4550-257">Hover on cog and click hello **Users**.</span></span>

    ![Adicionar empregado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. <span data-ttu-id="a4550-259">Em **utilizadores** separador de secção, clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="a4550-259">Under **Users** tab section, click **Add user**.</span></span>

    ![Adicionar empregado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. <span data-ttu-id="a4550-261">No Olá **adicionar novo utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a4550-261">On hello **Add New User** dialog page, perform hello following steps:</span></span>

    ![Adicionar empregado](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    <span data-ttu-id="a4550-263">a.</span><span class="sxs-lookup"><span data-stu-id="a4550-263">a.</span></span> <span data-ttu-id="a4550-264">No Olá **Username** caixa de texto, como o tipo Olá e-mail do utilizador Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a4550-264">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="a4550-265">b.</span><span class="sxs-lookup"><span data-stu-id="a4550-265">b.</span></span> <span data-ttu-id="a4550-266">No Olá **nome a apresentar** caixa de texto, nome a apresentar do tipo de utilizador de Olá como Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a4550-266">In hello **Display Name** textbox, type display name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="a4550-267">c.</span><span class="sxs-lookup"><span data-stu-id="a4550-267">c.</span></span> <span data-ttu-id="a4550-268">No Olá **endereço de correio eletrónico** caixa de texto, como o endereço de correio eletrónico de Olá de tipo de utilizador Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a4550-268">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="a4550-269">d.</span><span class="sxs-lookup"><span data-stu-id="a4550-269">d.</span></span> <span data-ttu-id="a4550-270">No Olá **palavra-passe** caixa de texto, palavra-passe Olá de tipo de utilizador.</span><span class="sxs-lookup"><span data-stu-id="a4550-270">In hello **Password** textbox, type hello password of user.</span></span>  

    <span data-ttu-id="a4550-271">e.</span><span class="sxs-lookup"><span data-stu-id="a4550-271">e.</span></span> <span data-ttu-id="a4550-272">No Olá **Confirmar palavra-passe** caixa de texto, reintroduza o Olá palavra-passe do utilizador.</span><span class="sxs-lookup"><span data-stu-id="a4550-272">In hello **Confirm Password** textbox, reenter hello password of user.</span></span>

    <span data-ttu-id="a4550-273">f.</span><span class="sxs-lookup"><span data-stu-id="a4550-273">f.</span></span> <span data-ttu-id="a4550-274">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a4550-274">Click **Add**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a4550-275">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4550-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a4550-276">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooKantega SSO para FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="a4550-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for FishEye/Crucible.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="a4550-278">**tooassign Britta Simon tooKantega SSO para FishEye/Crucible, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a4550-278">**tooassign Britta Simon tooKantega SSO for FishEye/Crucible, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4550-279">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a4550-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="a4550-281">Na lista de aplicações de Olá, selecione **Kantega SSO para FishEye/Crucible**.</span><span class="sxs-lookup"><span data-stu-id="a4550-281">In hello applications list, select **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. <span data-ttu-id="a4550-283">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a4550-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="a4550-285">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="a4550-285">Click **Add** button.</span></span> <span data-ttu-id="a4550-286">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a4550-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="a4550-288">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="a4550-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a4550-289">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a4550-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4550-290">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a4550-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a4550-291">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a4550-291">Testing single sign-on</span></span>

<span data-ttu-id="a4550-292">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a4550-292">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a4550-293">Ao clicar Olá Kantega SSO para mosaico FishEye/Crucible no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Kantega SSO para a aplicação de FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="a4550-293">When you click hello Kantega SSO for FishEye/Crucible tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for FishEye/Crucible application.</span></span>
<span data-ttu-id="a4550-294">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4550-294">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a4550-295">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a4550-295">Additional resources</span></span>

* [<span data-ttu-id="a4550-296">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4550-296">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4550-297">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a4550-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

