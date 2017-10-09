---
title: "Tutorial: Integração do Azure Active Directory com o software de RH Cezanne | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o software de RH Cezanne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="83866-103">Tutorial: Integrar o Azure Active Directory com o software de RH Cezanne</span><span class="sxs-lookup"><span data-stu-id="83866-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="83866-104">Neste tutorial, saiba como toointegrate Cezanne HR software com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83866-104">In this tutorial, you learn how toointegrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="83866-105">Integrar o software de RH Cezanne com o Azure AD fornece-lhe Olá seguintes vantagens.</span><span class="sxs-lookup"><span data-stu-id="83866-105">Integrating Cezanne HR software with Azure AD provides you with hello following benefits.</span></span> <span data-ttu-id="83866-106">Pode:</span><span class="sxs-lookup"><span data-stu-id="83866-106">You can:</span></span>

- <span data-ttu-id="83866-107">Controlar no Azure AD que tenha acesso tooCezanne HR software.</span><span class="sxs-lookup"><span data-stu-id="83866-107">Control in Azure AD who has access tooCezanne HR software.</span></span>
- <span data-ttu-id="83866-108">Ative o seu início de sessão de tooautomatically utilizadores no software tooCezanne HR com início de sessão único (SSO) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83866-108">Enable your users tooautomatically sign in tooCezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="83866-109">Gerir as contas numa localização central: Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="83866-109">Manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="83866-110">toolearn mais informações sobre software como uma integração de aplicação de serviço (SaaS) com o Azure AD, consulte [que é o acesso a aplicações e SSO no Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="83866-110">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83866-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="83866-111">Prerequisites</span></span>

<span data-ttu-id="83866-112">integração do Azure AD com o software de RH Cezanne tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="83866-112">tooconfigure Azure AD integration with Cezanne HR software, you need hello following items:</span></span>

- <span data-ttu-id="83866-113">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="83866-113">An Azure AD subscription</span></span>
- <span data-ttu-id="83866-114">Um software de RH Cezanne subscrição SSO ativado</span><span class="sxs-lookup"><span data-stu-id="83866-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="83866-115">tootest Olá obter os passos neste tutorial, recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="83866-115">tootest hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="83866-116">passos de Olá tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="83866-116">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="83866-117">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="83866-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="83866-118">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83866-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="83866-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="83866-119">Scenario description</span></span>
<span data-ttu-id="83866-120">Neste tutorial, testar o SSO do Azure AD num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="83866-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="83866-121">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="83866-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="83866-122">Adicionar software Cezanne HR da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="83866-122">Adding Cezanne HR software from hello gallery</span></span>
* <span data-ttu-id="83866-123">Configurar e testar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="83866-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-hello-gallery"></a><span data-ttu-id="83866-124">Adicionar software Cezanne HR da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="83866-124">Add Cezanne HR software from hello gallery</span></span>
<span data-ttu-id="83866-125">integração de Olá tooconfigure de RH Cezanne software com o Azure AD, adicione software Cezanne HR Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="83866-125">tooconfigure hello integration of Cezanne HR software into Azure AD, add Cezanne HR software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="83866-126">tooadd software Cezanne HR da Galeria de Olá, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="83866-126">tooadd Cezanne HR software from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="83866-127">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel esquerdo de Olá, selecione Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="83866-127">In hello **[Azure portal](https://portal.azure.com)**, in hello left pane, select hello **Azure Active Directory** button.</span></span> 

    ![botão de "Do Azure Active Directory" Olá][1]

2. <span data-ttu-id="83866-129">Selecione **aplicações empresariais** > **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="83866-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Olá "Todas as aplicações" ligação][2]
    
3. <span data-ttu-id="83866-131">tooadd uma nova aplicação, na parte superior de Olá de Olá **todas as aplicações** caixa de diálogo, selecione **nova aplicação**.</span><span class="sxs-lookup"><span data-stu-id="83866-131">tooadd a new application, at hello top of hello **All applications** dialog box, select **New application**.</span></span>

    ![Olá "Nova aplicação" botão][3]

4. <span data-ttu-id="83866-133">Na caixa de pesquisa de Olá, escreva **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="83866-133">In hello search box, type **Cezanne HR Software**.</span></span>

    ![caixa de pesquisa de Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="83866-135">Na lista de resultados de Olá, selecione **Cezanne HR Software** e, em seguida, selecione Olá **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="83866-135">In hello results list, select **Cezanne HR Software** and then select hello **Add** button tooadd hello application.</span></span>

    ![lista de resultados de Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="83866-137">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="83866-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="83866-138">Nesta secção, configurar e testar o SSO do Azure AD com o software de RH Cezanne com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="83866-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="83866-139">Para SSO toowork, do Azure AD tem tooknow Olá Cezanne HR software homólogo toohello utilizador do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="83866-139">For SSO toowork, Azure AD needs tooknow hello Cezanne HR software counterpart toohello Azure AD user.</span></span> <span data-ttu-id="83866-140">Por outras palavras, tem de estabelecer uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá no Olá Cezanne HR software.</span><span class="sxs-lookup"><span data-stu-id="83866-140">In other words, you must establish a link relationship between an Azure AD user and hello related user in hello Cezanne HR software.</span></span>

<span data-ttu-id="83866-141">relação de ligação de Olá tooestablish, atribuir Olá Cezanne HR software **nome de utilizador** valor como Olá do Azure AD **Username** valor.</span><span class="sxs-lookup"><span data-stu-id="83866-141">tooestablish hello link relationship, assign hello Cezanne HR software **user name** value as hello Azure AD **Username** value.</span></span>

<span data-ttu-id="83866-142">tooconfigure e teste do Azure AD SSO utilizando software de RH Cezanne, Olá concluir os seguintes blocos modulares.</span><span class="sxs-lookup"><span data-stu-id="83866-142">tooconfigure and test Azure AD SSO by using Cezanne HR software, complete hello following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="83866-143">Configurar o SSO do Azure AD</span><span class="sxs-lookup"><span data-stu-id="83866-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="83866-144">Nesta secção, pode ativar a SSO do Azure AD no portal do Azure de Olá e configurar o SSO na sua aplicação de software Cezanne HR, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="83866-144">In this section, you can enable Azure AD SSO in hello Azure portal and configure SSO in your Cezanne HR software application by doing hello following:</span></span>

1. <span data-ttu-id="83866-145">No Olá portal do Azure, no Olá **Cezanne HR Software** página de integração de aplicações, selecione **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="83866-145">In hello Azure portal, on hello **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Olá "De sessão único-" o comando][4]

2. <span data-ttu-id="83866-147">tooenable SSO, no Olá **de sessão único-** caixa de diálogo, selecione de Olá **modo** como **baseados em SAML início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="83866-147">tooenable SSO, in hello **Single sign-on** dialog box, select hello **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![caixa de "Modo de" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="83866-149">Em **Cezanne HR Software domínio e os URLs**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="83866-149">Under **Cezanne HR Software Domain and URLs**, do hello following:</span></span>

    ![Olá "Cezanne HR Software domínio e os URLs" secção](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="83866-151">a.</span><span class="sxs-lookup"><span data-stu-id="83866-151">a.</span></span> <span data-ttu-id="83866-152">No Olá **URL de início de sessão** caixa, escreva um URL que tem Olá a seguinte sintaxe:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="83866-152">In hello **Sign-on URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="83866-153">b.</span><span class="sxs-lookup"><span data-stu-id="83866-153">b.</span></span> <span data-ttu-id="83866-154">No Olá **URL de resposta** caixa, escreva um URL que tem Olá a seguinte sintaxe:`https://w3.cezanneondemand.com:443/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="83866-154">In hello **Reply URL** box, type a URL that has hello following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="83866-155">Olá anteriores valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="83866-155">hello preceding values are not real.</span></span> <span data-ttu-id="83866-156">Atualize-as com o URL de resposta real Olá e o URL de início de sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="83866-156">Update them with hello actual reply URL and hello sign-on URL.</span></span> <span data-ttu-id="83866-157">os valores de Olá tooobtain, Olá contacto [equipa de suporte de cliente de software Cezanne HR](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="83866-157">tooobtain hello values, contact hello [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="83866-158">Em **certificado de assinatura de SAML**, selecione **certificado (Base64)**e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="83866-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Olá secção "Certificado de assinatura de SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="83866-160">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="83866-160">Select **Save**.</span></span>

    ![botão de "Guardar" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="83866-162">Em **Cezanne HR Software configuração**, selecione **configurar Cezanne HR Software** tooopen Olá **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="83866-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="83866-163">Olá cópia **ID de entidade de SAML** e **SAML único início de sessão no serviço** URL de Olá **referência rápida** secção.</span><span class="sxs-lookup"><span data-stu-id="83866-163">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service** URL from hello **Quick Reference** section.</span></span>

    ![Olá secção "Configuração de Software de RH Cezanne"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="83866-165">Numa janela do browser web diferente, inicie sessão no inquilino de software de RH Cezanne tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="83866-165">In a different web browser window, sign on tooyour Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="83866-166">No painel esquerdo Olá, selecione **a configuração do sistema**.</span><span class="sxs-lookup"><span data-stu-id="83866-166">In hello left pane, select **System Setup**.</span></span> <span data-ttu-id="83866-167">Selecione **definições de segurança** > **Single Sign-On configuração**.</span><span class="sxs-lookup"><span data-stu-id="83866-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![Olá "único início de sessão" a ligação de configuração](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="83866-169">No Olá **permitir que os utilizadores toolog utilizando Olá os seguintes serviços único Sign-On (SSO)** painel, selecione de Olá **SAML 2.0** caixa de verificação e selecione Olá **configuração avançada** opção.</span><span class="sxs-lookup"><span data-stu-id="83866-169">In hello **Allow users toolog in using hello following Single Sign-On (SSO) services** pane, select hello **SAML 2.0** check box and select hello **Advanced Configuration** option.</span></span>

    ![O início de sessão único dos serviços de opções](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="83866-171">Selecione **adicionar novos**.</span><span class="sxs-lookup"><span data-stu-id="83866-171">Select **Add New**.</span></span>

    ![botão "Adicionar novo" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="83866-173">Em **fornecedores de identidade SAML 2.0**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="83866-173">Under **SAML 2.0 Identity Providers**, do hello following:</span></span>

    ![Olá secção "Fornecedores de identidade SAML 2.0"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="83866-175">a.</span><span class="sxs-lookup"><span data-stu-id="83866-175">a.</span></span> <span data-ttu-id="83866-176">No Olá **nome a apresentar** box, introduza o nome de Olá do seu fornecedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="83866-176">In hello **Display Name** box, enter hello name of your identity provider.</span></span>

    <span data-ttu-id="83866-177">b.</span><span class="sxs-lookup"><span data-stu-id="83866-177">b.</span></span> <span data-ttu-id="83866-178">No Olá **identificador da entidade** caixa, cole Olá **ID de entidade de SAML** que copiou do Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="83866-178">In hello **Entity Identifier** box, paste hello **SAML Entity ID** that you copied from hello Azure portal.</span></span> 

    <span data-ttu-id="83866-179">c.</span><span class="sxs-lookup"><span data-stu-id="83866-179">c.</span></span> <span data-ttu-id="83866-180">No Olá **SAML enlace** caixa de lista, selecione **POST**.</span><span class="sxs-lookup"><span data-stu-id="83866-180">In hello **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="83866-181">d.</span><span class="sxs-lookup"><span data-stu-id="83866-181">d.</span></span> <span data-ttu-id="83866-182">No Olá **ponto final de serviço de Token segurança** caixa, cole Olá **SAML único início de sessão no serviço** URL que copiou do Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="83866-182">In hello **Security Token Service Endpoint** box, paste hello **SAML Single Sign-On Service** URL that you copied from hello Azure portal.</span></span> 
    
    <span data-ttu-id="83866-183">e.</span><span class="sxs-lookup"><span data-stu-id="83866-183">e.</span></span> <span data-ttu-id="83866-184">No Olá **nome de atributo de ID de utilizador** box, introduza `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="83866-184">In hello **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="83866-185">f.</span><span class="sxs-lookup"><span data-stu-id="83866-185">f.</span></span> <span data-ttu-id="83866-186">Olá tooupload transferido o certificado do Azure AD, selecione de Olá **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="83866-186">tooupload hello downloaded certificate from Azure AD, select hello **Upload** button.</span></span>
    
    <span data-ttu-id="83866-187">g.</span><span class="sxs-lookup"><span data-stu-id="83866-187">g.</span></span> <span data-ttu-id="83866-188">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="83866-188">Select **OK**.</span></span> 

12. <span data-ttu-id="83866-189">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="83866-189">Select **Save**.</span></span>

    ![botão de "Guardar" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="83866-191">Como configurar a aplicação Olá, pode ler uma versão de Olá precedente instruções no Olá concisa [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83866-191">As you set up hello app, you can read a concise version of hello preceding instructions in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="83866-192">Depois de adicionar aplicação Olá de Olá **do Active Directory** > **aplicações empresariais** secção, selecione de Olá **de sessão único-** separador. Em seguida, Olá de acesso incorporados documentação de Olá **configuração** secção.</span><span class="sxs-lookup"><span data-stu-id="83866-192">After you add hello app from hello **Active Directory** > **Enterprise applications** section, select hello **Single sign-on** tab. Then access hello embedded documentation from hello **Configuration** section.</span></span> 

<span data-ttu-id="83866-193">toolearn mais informações sobre a funcionalidade de documentação incorporados Olá, consulte [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="83866-193">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="83866-194">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="83866-194">Create an Azure AD test user</span></span>
<span data-ttu-id="83866-195">Nesta secção, vai criar o utilizador de teste Britta Simon no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="83866-195">In this section, you create test user Britta Simon in hello Azure portal.</span></span>

![utilizador de teste de Olá Britta Simon][100]

<span data-ttu-id="83866-197">toocreate um utilizador de teste no Azure AD, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="83866-197">toocreate a test user in Azure AD, do hello following:</span></span>

1. <span data-ttu-id="83866-198">No Olá **portal do Azure**, no painel esquerdo de Olá, selecione Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="83866-198">In hello **Azure portal**, in hello left pane, select hello **Azure Active Directory** button.</span></span>

    ![botão de "Do Azure Active Directory" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="83866-200">lista de Olá toodisplay de utilizadores, selecionadas **utilizadores e grupos** > **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="83866-200">toodisplay hello list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Olá "Todos os utilizadores" ligação](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="83866-202">Olá **todos os utilizadores** é aberta a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="83866-202">hello **All users** dialog box opens.</span></span>

3. <span data-ttu-id="83866-203">Olá tooopen **utilizador** caixa de diálogo, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="83866-203">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![botão de "Adicionar" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="83866-205">No Olá **utilizador** diálogo caixa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="83866-205">In hello **User** dialog box, do hello following:</span></span>
 
    ![caixa de diálogo Olá "Utilizador"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="83866-207">a.</span><span class="sxs-lookup"><span data-stu-id="83866-207">a.</span></span> <span data-ttu-id="83866-208">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="83866-208">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="83866-209">b.</span><span class="sxs-lookup"><span data-stu-id="83866-209">b.</span></span> <span data-ttu-id="83866-210">No Olá **nome de utilizador** caixa, escreva de utilizador Britta Simon **endereço de correio eletrónico**.</span><span class="sxs-lookup"><span data-stu-id="83866-210">In hello **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="83866-211">c.</span><span class="sxs-lookup"><span data-stu-id="83866-211">c.</span></span> <span data-ttu-id="83866-212">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, o valor de Olá de nota que foi gerado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="83866-212">Select hello **Show Password** check box, and then note hello value that was generated in hello **Password** box.</span></span>

    <span data-ttu-id="83866-213">d.</span><span class="sxs-lookup"><span data-stu-id="83866-213">d.</span></span> <span data-ttu-id="83866-214">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="83866-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="83866-215">Criar um utilizador de teste do software de RH Cezanne</span><span class="sxs-lookup"><span data-stu-id="83866-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="83866-216">tooenable do Azure AD os utilizadores toosign no software tooCezanne HR, estes têm de ser aprovisionados para Cezanne HR software.</span><span class="sxs-lookup"><span data-stu-id="83866-216">tooenable Azure AD users toosign in tooCezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="83866-217">No caso de Olá de RH Cezanne software, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="83866-217">In hello case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="83866-218">Aprovisionar uma conta de utilizador, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="83866-218">Provision a user account by doing hello following:</span></span>

1.  <span data-ttu-id="83866-219">Inicie sessão no tooyour Cezanne HR site da empresa de software como um administrador.</span><span class="sxs-lookup"><span data-stu-id="83866-219">Sign in tooyour Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="83866-220">No painel esquerdo Olá, selecione **a configuração do sistema** > **gerir utilizadores** > **adicionar novo utilizador**.</span><span class="sxs-lookup"><span data-stu-id="83866-220">In hello left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="83866-221">![ligação de "Adicionar novo utilizador" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "novo utilizador")</span><span class="sxs-lookup"><span data-stu-id="83866-221">![hello "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="83866-222">Em **pessoa detalhes**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="83866-222">Under **Person Details**, do hello following:</span></span>

    <span data-ttu-id="83866-223">![Olá seção "Pessoa Detalhes"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "novo utilizador")</span><span class="sxs-lookup"><span data-stu-id="83866-223">![hello "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="83866-224">a.</span><span class="sxs-lookup"><span data-stu-id="83866-224">a.</span></span> <span data-ttu-id="83866-225">Definir **utilizador interno** como **OFF**.</span><span class="sxs-lookup"><span data-stu-id="83866-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="83866-226">b.</span><span class="sxs-lookup"><span data-stu-id="83866-226">b.</span></span> <span data-ttu-id="83866-227">No Olá **nome próprio** caixa, tipo Olá nome próprio do utilizador, por exemplo, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="83866-227">In hello **First Name** box, type hello user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="83866-228">c.</span><span class="sxs-lookup"><span data-stu-id="83866-228">c.</span></span> <span data-ttu-id="83866-229">No Olá **Apelido** caixa, tipo Olá apelido do utilizador, por exemplo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="83866-229">In hello **Last Name** box, type hello user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="83866-230">d.</span><span class="sxs-lookup"><span data-stu-id="83866-230">d.</span></span> <span data-ttu-id="83866-231">No Olá **correio electrónico** caixa, escreva o endereço de e-mail do utilizador Olá, por exemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="83866-231">In hello **E-mail** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="83866-232">Em **informações da conta**, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="83866-232">Under **Account Information**, do hello following:</span></span>

    <span data-ttu-id="83866-233">![Olá secção "Informações de conta"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "novo utilizador")</span><span class="sxs-lookup"><span data-stu-id="83866-233">![hello "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="83866-234">a.</span><span class="sxs-lookup"><span data-stu-id="83866-234">a.</span></span> <span data-ttu-id="83866-235">No Olá **Username** caixa, escreva o endereço de e-mail do utilizador Olá, por exemplo, Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="83866-235">In hello **Username** box, type hello user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="83866-236">b.</span><span class="sxs-lookup"><span data-stu-id="83866-236">b.</span></span> <span data-ttu-id="83866-237">No Olá **palavra-passe** caixa, escreva a palavra-passe do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="83866-237">In hello **Password** box, type hello user's password.</span></span>
    
    <span data-ttu-id="83866-238">c.</span><span class="sxs-lookup"><span data-stu-id="83866-238">c.</span></span> <span data-ttu-id="83866-239">No Olá **função de segurança** caixa, selecione **HR Professional**.</span><span class="sxs-lookup"><span data-stu-id="83866-239">In hello **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="83866-240">d.</span><span class="sxs-lookup"><span data-stu-id="83866-240">d.</span></span> <span data-ttu-id="83866-241">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="83866-241">Select **OK**.</span></span>

5. <span data-ttu-id="83866-242">No Olá **de sessão único-** separador, Olá **SAML 2.0 identificadores** secção, selecione **adicionar novo**.</span><span class="sxs-lookup"><span data-stu-id="83866-242">On hello **Single sign-on** tab, in hello **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="83866-243">![botão "Adicionar novo" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "utilizador")</span><span class="sxs-lookup"><span data-stu-id="83866-243">![hello "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="83866-244">No Olá **fornecedor de identidade** caixa de lista, selecione o seu fornecedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="83866-244">In hello **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="83866-245">No Olá **identificador de utilizador** box, introduza o endereço de correio eletrónico Olá para a conta de Simon de teste, utilizador Britta.</span><span class="sxs-lookup"><span data-stu-id="83866-245">In hello **User Identifier** box, enter hello email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="83866-246">![Olá "Fornecedor de identidade" e "Utilizador identificador" caixas](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "utilizador")</span><span class="sxs-lookup"><span data-stu-id="83866-246">![hello "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="83866-247">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="83866-247">Select **Save**.</span></span>

    <span data-ttu-id="83866-248">![botão de "Guardar" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "utilizador")</span><span class="sxs-lookup"><span data-stu-id="83866-248">![hello "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="83866-249">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="83866-249">Assign hello Azure AD test user</span></span>

<span data-ttu-id="83866-250">Nesta secção, ativar o utilizador de teste Britta Simon toouse SSO do Azure, concedendo acesso tooCezanne HR software.</span><span class="sxs-lookup"><span data-stu-id="83866-250">In this section, you enable test user Britta Simon toouse Azure SSO by granting access tooCezanne HR software.</span></span>

![Acesso de utilizador de teste][200] 

1. <span data-ttu-id="83866-252">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, aceda a vista de diretório toohello.</span><span class="sxs-lookup"><span data-stu-id="83866-252">In hello Azure portal, open hello applications view and then go toohello directory view.</span></span> <span data-ttu-id="83866-253">Selecione **aplicações empresariais** > **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="83866-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Olá "Todas as aplicações" ligação][201] 

2. <span data-ttu-id="83866-255">Na lista de aplicações de Olá, selecione **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="83866-255">In hello applications list, select **Cezanne HR Software**.</span></span>

    ![lista de "Aplicações" Olá](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="83866-257">No menu de Olá Olá esquerda, selecione **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="83866-257">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="83866-259">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="83866-259">Select **Add**.</span></span> <span data-ttu-id="83866-260">Em seguida, no Olá **adicionar atribuição** caixa de diálogo, selecione **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="83866-260">Then in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Ligação de "Utilizadores e grupos"][203]

5. <span data-ttu-id="83866-262">No Olá **utilizadores e grupos** Olá caixa de diálogo **utilizadores** lista, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="83866-262">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="83866-263">No Olá **utilizadores e grupos** caixa de diálogo, selecione **selecione**.</span><span class="sxs-lookup"><span data-stu-id="83866-263">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="83866-264">No Olá **adicionar atribuição** caixa de diálogo, selecione **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="83866-264">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="83866-265">Teste SSO</span><span class="sxs-lookup"><span data-stu-id="83866-265">Test SSO</span></span>

<span data-ttu-id="83866-266">Nesta secção, testar a configuração do Azure AD SSO utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="83866-266">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="83866-267">Quando selecionar o mosaico de software Olá Cezanne HR no painel de acesso de Olá, inicie sessão no tooyour automaticamente a aplicação de software de RH Cezanne.</span><span class="sxs-lookup"><span data-stu-id="83866-267">When you select hello Cezanne HR software tile in hello Access Panel, you sign on automatically tooyour Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83866-268">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="83866-268">Next steps</span></span>

* [<span data-ttu-id="83866-269">Lista de tutoriais sobre como aplicações de SaaS toointegrate com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83866-269">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="83866-270">O que é o acesso a aplicações e SSO no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="83866-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

