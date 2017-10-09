---
title: "Tutorial: Integração do Azure Active Directory com Clarizen | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="a6868-103">Tutorial: Integração do Azure Active Directory com Clarizen</span><span class="sxs-lookup"><span data-stu-id="a6868-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="a6868-104">Neste tutorial, saiba como toointegrate do Azure Active Directory (Azure AD) com Clarizen.</span><span class="sxs-lookup"><span data-stu-id="a6868-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="a6868-105">Este fornecem integração Olá os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="a6868-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="a6868-106">Pode controlar, no Azure AD, que tenha acesso tooClarizen.</span><span class="sxs-lookup"><span data-stu-id="a6868-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="a6868-107">Pode ativar a sua toobe utilizadores iniciada automaticamente no tooClarizen (-início de sessão único) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6868-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="a6868-108">Pode gerir as contas numa localização central, Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6868-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="a6868-109">cenário de Olá deste tutorial consiste em duas tarefas principais:</span><span class="sxs-lookup"><span data-stu-id="a6868-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="a6868-110">Adicione Clarizen da Galeria de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6868-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="a6868-111">Configurar e testar o Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a6868-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="a6868-112">Se pretender obter mais detalhes sobre o software como uma integração de aplicação de serviço (SaaS) com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6868-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6868-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a6868-113">Prerequisites</span></span>
<span data-ttu-id="a6868-114">integração do Azure AD com Clarizen tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a6868-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="a6868-115">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6868-115">An Azure AD subscription</span></span>
- <span data-ttu-id="a6868-116">Uma subscrição de Clarizen está ativada para o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a6868-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="a6868-117">passos de Olá tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a6868-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="a6868-118">Teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a6868-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6868-119">Não utilize o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="a6868-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a6868-120">Se não tiver um ambiente de teste do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6868-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="a6868-121">Adicionar Clarizen da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a6868-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="a6868-122">integração de Olá tooconfigure de Clarizen com o Azure AD, adicione Clarizen Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="a6868-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="a6868-123">No Olá [portal do Azure](https://portal.azure.com), no Olá painel esquerdo, clique em Olá **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a6868-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Ícone do Active Directory do Azure][1]

2. <span data-ttu-id="a6868-125">Clique em **aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a6868-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="a6868-126">Em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a6868-126">Then click **All applications**.</span></span>

    ![Ao clicar em "As aplicações empresariais" e "Todas as aplicações"][2]

3. <span data-ttu-id="a6868-128">Clique em Olá **adicionar** botão na parte superior de Olá Olá da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6868-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![botão de "Adicionar" Olá][3]

4. <span data-ttu-id="a6868-130">Na caixa de pesquisa de Olá, escreva **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="a6868-130">In hello search box, type **Clarizen**.</span></span>

    ![Escrever "Clarizen" na caixa de pesquisa de Olá](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="a6868-132">No painel de resultados de Olá, selecione **Clarizen**e, em seguida, clique em **adicionar** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="a6868-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Selecionar Clarizen no painel de resultados de Olá](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="a6868-134">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a6868-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="a6868-135">Olá secções a seguir, configure e teste do Azure AD-início de sessão único com Clarizen com base no utilizador de teste de Olá Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6868-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="a6868-136">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Clarizen é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6868-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="a6868-137">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Clarizen tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a6868-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="a6868-138">Estabelecer esta relação de ligação ao atribuir o valor Olá **nome de utilizador** no Azure AD como valor Olá **Username** no Clarizen.</span><span class="sxs-lookup"><span data-stu-id="a6868-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="a6868-139">tooconfigure e teste do Azure AD-início de sessão único com Clarizen, Olá concluída blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a6868-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="a6868-140">**[Configurar o Azure AD-início de sessão único](#configure-azure-ad-single-sign-on)**  tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a6868-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a6868-141">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6868-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6868-142">**[Criar um utilizador de teste Clarizen](#create-a-clarizen-test-user)**  toohave um homólogo de Britta Simon no Clarizen é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6868-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a6868-143">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a6868-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6868-144">**[Teste o início de sessão único](#test-single-sign-on)**  tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="a6868-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="a6868-145">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a6868-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="a6868-146">Ativar o Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Clarizen.</span><span class="sxs-lookup"><span data-stu-id="a6868-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="a6868-147">No Olá portal do Azure, no Olá **Clarizen** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="a6868-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Ao clicar em "Single sign-on"][4]

2. <span data-ttu-id="a6868-149">No Olá **de sessão único-** caixa de diálogo, para **modo**, selecione **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a6868-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Selecionar "baseados em SAML início de sessão"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="a6868-151">No Olá **Clarizen domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a6868-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Caixas de URL de identificador e resposta](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="a6868-153">a.</span><span class="sxs-lookup"><span data-stu-id="a6868-153">a.</span></span> <span data-ttu-id="a6868-154">No Olá **identificador** caixa, valor de tipo de Olá como: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="a6868-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="a6868-155">b.</span><span class="sxs-lookup"><span data-stu-id="a6868-155">b.</span></span> <span data-ttu-id="a6868-156">No Olá **URL de resposta** caixa, escreva um URL utilizando Olá seguir o padrão: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="a6868-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="a6868-157">Estes não são valores reais Olá.</span><span class="sxs-lookup"><span data-stu-id="a6868-157">These are not hello real values.</span></span> <span data-ttu-id="a6868-158">Ter toouse Olá real identificador e o URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="a6868-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="a6868-159">Aqui sugerimos que utilizar Olá valor exclusivo de uma cadeia como Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="a6868-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="a6868-160">tooget Olá valores reais, Olá contacto [equipa de suporte de Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="a6868-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="a6868-161">No Olá **certificado de assinatura de SAML** secção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="a6868-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clicar em "Criar o novo certificado"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="a6868-163">No Olá **criar o novo certificado** diálogo caixa, clique Olá ícone de calendário e selecione uma data de expiração.</span><span class="sxs-lookup"><span data-stu-id="a6868-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="a6868-164">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a6868-164">Then click **Save**.</span></span>

    ![Selecionar e guardar uma data de expiração](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="a6868-166">No Olá **certificado de assinatura de SAML** secção, selecione **tornar o novo certificado ativa**e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="a6868-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Selecionar Olá caixa de verificação para efetuar o novo certificado de Olá Active Directory](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="a6868-168">No Olá **o certificado de Rollover** caixa de diálogo, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6868-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Ao clicar em "OK" tooconfirm que pretende que o certificado de Olá toomake Active Directory](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a6868-170">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a6868-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Transferência de Olá de toostart do clicando em "Certificate (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="a6868-172">No Olá **Clarizen configuração** secção, clique em **configurar Clarizen** tooopen Olá **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="a6868-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![Clicar em "Configurar Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Janela "Configurar o início de sessão", incluindo URLs e ficheiros](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="a6868-175">Numa janela do browser web diferente, inicie sessão no site da empresa tooyour Clarizen como administrador.</span><span class="sxs-lookup"><span data-stu-id="a6868-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="a6868-176">Clique em seu nome de utilizador e, em seguida, clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="a6868-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="a6868-177">![Ao clicar em "Definições" em seu nome de utilizador](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "definições")</span><span class="sxs-lookup"><span data-stu-id="a6868-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="a6868-178">Clique em Olá **definições globais** separador. Em seguida, seguinte demasiado**autenticação federada**, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="a6868-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="a6868-179">![Separador "Definições globais"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "definições globais")</span><span class="sxs-lookup"><span data-stu-id="a6868-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="a6868-180">No Olá **autenticação federada** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a6868-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="a6868-181">![Caixa de diálogo "Autenticação federada"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "autenticação federada")</span><span class="sxs-lookup"><span data-stu-id="a6868-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="a6868-182">a.</span><span class="sxs-lookup"><span data-stu-id="a6868-182">a.</span></span> <span data-ttu-id="a6868-183">Selecione **ativar federado autenticação**.</span><span class="sxs-lookup"><span data-stu-id="a6868-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="a6868-184">b.</span><span class="sxs-lookup"><span data-stu-id="a6868-184">b.</span></span> <span data-ttu-id="a6868-185">Clique em **carregar** tooupload o certificado transferido.</span><span class="sxs-lookup"><span data-stu-id="a6868-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="a6868-186">c.</span><span class="sxs-lookup"><span data-stu-id="a6868-186">c.</span></span> <span data-ttu-id="a6868-187">No Olá **URL de início de sessão** box, introduza o valor Olá **único início de sessão no URL do serviço SAML** da janela de configuração de aplicação Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6868-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="a6868-188">d.</span><span class="sxs-lookup"><span data-stu-id="a6868-188">d.</span></span> <span data-ttu-id="a6868-189">No Olá **Sign-out URL** box, introduza o valor Olá **Sign-Out URL** da janela de configuração de aplicação Olá do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6868-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="a6868-190">e.</span><span class="sxs-lookup"><span data-stu-id="a6868-190">e.</span></span> <span data-ttu-id="a6868-191">Selecione **utilizar POST**.</span><span class="sxs-lookup"><span data-stu-id="a6868-191">Select **Use POST**.</span></span>

    <span data-ttu-id="a6868-192">f.</span><span class="sxs-lookup"><span data-stu-id="a6868-192">f.</span></span> <span data-ttu-id="a6868-193">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a6868-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a6868-194">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6868-194">Create an Azure AD test user</span></span>
<span data-ttu-id="a6868-195">Olá portal do Azure, crie um utilizador de teste chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6868-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Endereço de correio eletrónico e o nome de utilizador de teste de Olá do Azure AD][100]

1. <span data-ttu-id="a6868-197">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a6868-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Ícone do Active Directory do Azure](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="a6868-199">Clique em **utilizadores e grupos**e, em seguida, clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="a6868-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![Ao clicar em "Utilizadores e grupos" e "Todos os utilizadores"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="a6868-201">Na parte superior de Olá Olá da caixa de diálogo, clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6868-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![botão de "Adicionar" Olá](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="a6868-203">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a6868-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Caixa de diálogo "Utilizador" com o nome, endereço de correio eletrónico e palavra-passe preenchidos](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="a6868-205">a.</span><span class="sxs-lookup"><span data-stu-id="a6868-205">a.</span></span> <span data-ttu-id="a6868-206">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6868-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6868-207">b.</span><span class="sxs-lookup"><span data-stu-id="a6868-207">b.</span></span> <span data-ttu-id="a6868-208">No Olá **nome de utilizador** caixa, endereço de correio eletrónico do tipo Olá de Olá conta Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6868-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="a6868-209">c.</span><span class="sxs-lookup"><span data-stu-id="a6868-209">c.</span></span> <span data-ttu-id="a6868-210">Selecione **mostrar palavra-passe** e anote o valor Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="a6868-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="a6868-211">d.</span><span class="sxs-lookup"><span data-stu-id="a6868-211">d.</span></span> <span data-ttu-id="a6868-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a6868-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="a6868-213">Criar um utilizador de teste Clarizen</span><span class="sxs-lookup"><span data-stu-id="a6868-213">Create a Clarizen test user</span></span>
<span data-ttu-id="a6868-214">toosign de utilizadores do Azure AD tooenable no tooClarizen, terá de aprovisionar contas de utilizador.</span><span class="sxs-lookup"><span data-stu-id="a6868-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="a6868-215">No caso de Olá da Clarizen, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a6868-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="a6868-216">Inicie sessão no tooyour Clarizen site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="a6868-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="a6868-217">Clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="a6868-217">Click **People**.</span></span>

    <span data-ttu-id="a6868-218">![Clicar em "As pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "pessoas")</span><span class="sxs-lookup"><span data-stu-id="a6868-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="a6868-219">Clique em **convidar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="a6868-219">Click **Invite User**.</span></span>

    <span data-ttu-id="a6868-220">![Botão "Convidar utilizadores"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "convidar utilizadores")</span><span class="sxs-lookup"><span data-stu-id="a6868-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="a6868-221">No Olá **convidar pessoas** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a6868-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="a6868-222">![Caixa de diálogo "Convidar pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "convidar pessoas")</span><span class="sxs-lookup"><span data-stu-id="a6868-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="a6868-223">a.</span><span class="sxs-lookup"><span data-stu-id="a6868-223">a.</span></span> <span data-ttu-id="a6868-224">No Olá **E-Mail** caixa, endereço de correio eletrónico do tipo Olá de Olá conta Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6868-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="a6868-225">b.</span><span class="sxs-lookup"><span data-stu-id="a6868-225">b.</span></span> <span data-ttu-id="a6868-226">Clique em **convidar**.</span><span class="sxs-lookup"><span data-stu-id="a6868-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a6868-227">titular de conta do Azure Active Directory Olá irá receber um e-mail e siga a tooconfirm uma ligação a respetiva conta para ficar ativa.</span><span class="sxs-lookup"><span data-stu-id="a6868-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a6868-228">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6868-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="a6868-229">Ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooClarizen de acesso.</span><span class="sxs-lookup"><span data-stu-id="a6868-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Utilizador de teste atribuído][200]

1. <span data-ttu-id="a6868-231">No portal do Azure Olá, abra a vista de aplicações de Olá, procurar toohello vista de diretório, clique em **aplicações empresariais**e, em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a6868-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Ao clicar em "As aplicações empresariais" e "Todas as aplicações"][201]

2. <span data-ttu-id="a6868-233">Na lista de aplicações de Olá, selecione **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="a6868-233">In hello applications list, select **Clarizen**.</span></span>

    ![Selecionar Clarizen na lista de Olá](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="a6868-235">No painel esquerdo Olá, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a6868-235">In hello left pane, click **Users and groups**.</span></span>

    ![Ao clicar em "Utilizadores e grupos"][202]

4. <span data-ttu-id="a6868-237">Clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="a6868-237">Click hello **Add** button.</span></span> <span data-ttu-id="a6868-238">Em seguida, no Olá **adicionar atribuição** caixa de diálogo, selecione **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a6868-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![botão de "Adicionar" Olá e a caixa de diálogo de "Adicionar atribuição" Olá][203]

5. <span data-ttu-id="a6868-240">No Olá **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de Olá de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="a6868-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="a6868-241">No Olá **utilizadores e grupos** caixa de diálogo, clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="a6868-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="a6868-242">No Olá **adicionar atribuição** caixa de diálogo, clique em Olá **atribuir** botão.</span><span class="sxs-lookup"><span data-stu-id="a6868-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="a6868-243">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a6868-243">Test single sign-on</span></span>
<span data-ttu-id="a6868-244">Teste a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a6868-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="a6868-245">Ao clicar em mosaico de Clarizen Olá no painel de acesso de Olá, esta deve ser iniciada automaticamente no tooyour Clarizen aplicação.</span><span class="sxs-lookup"><span data-stu-id="a6868-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a6868-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a6868-246">Additional resources</span></span>

* [<span data-ttu-id="a6868-247">Lista de tutoriais sobre como aplicações de SaaS toointegrate com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6868-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6868-248">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6868-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
