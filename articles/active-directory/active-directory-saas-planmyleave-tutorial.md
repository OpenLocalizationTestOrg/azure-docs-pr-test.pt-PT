---
title: "Tutorial: Integração do Azure Active Directory com PlanMyLeave | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="a833d-103">Tutorial: Integração do Azure Active Directory com PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="a833d-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="a833d-104">Neste tutorial, saiba como toointegrate PlanMyLeave com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a833d-104">In this tutorial, you learn how toointegrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a833d-105">Integrar PlanMyLeave com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="a833d-105">Integrating PlanMyLeave with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a833d-106">Pode controlar no Azure AD que tenha acesso tooPlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="a833d-106">You can control in Azure AD who has access tooPlanMyLeave</span></span>
- <span data-ttu-id="a833d-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPlanMyLeave (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a833d-107">You can enable your users tooautomatically get signed-on tooPlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a833d-108">Pode gerir as contas numa localização central - portal de gestão do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="a833d-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="a833d-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a833d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a833d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a833d-110">Prerequisites</span></span>

<span data-ttu-id="a833d-111">integração do Azure AD com PlanMyLeave tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a833d-111">tooconfigure Azure AD integration with PlanMyLeave, you need hello following items:</span></span>

- <span data-ttu-id="a833d-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a833d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a833d-113">Um PlanMyLeave início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="a833d-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="a833d-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a833d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="a833d-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a833d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a833d-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="a833d-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="a833d-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a833d-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="a833d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a833d-118">Scenario description</span></span>
<span data-ttu-id="a833d-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a833d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a833d-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="a833d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a833d-121">Adicionar PlanMyLeave da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a833d-121">Adding PlanMyLeave from hello gallery</span></span>
2. <span data-ttu-id="a833d-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a833d-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-hello-gallery"></a><span data-ttu-id="a833d-123">Adicionar PlanMyLeave da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a833d-123">Adding PlanMyLeave from hello gallery</span></span>
<span data-ttu-id="a833d-124">tooconfigure Olá integração de PlanMyLeave com o Azure AD, é necessário tooadd PlanMyLeave Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="a833d-124">tooconfigure hello integration of PlanMyLeave into Azure AD, you need tooadd PlanMyLeave from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a833d-125">**tooadd PlanMyLeave da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a833d-125">**tooadd PlanMyLeave from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a833d-126">No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a833d-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a833d-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a833d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a833d-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a833d-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="a833d-131">Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="a833d-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="a833d-133">Na caixa de pesquisa de Olá, escreva **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="a833d-133">In hello search box, type **PlanMyLeave**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="a833d-135">No painel de resultados de Olá, selecione **PlanMyLeave**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="a833d-135">In hello results panel, select **PlanMyLeave**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a833d-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a833d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a833d-138">Nesta secção, configure e teste do Azure AD-início de sessão único com PlanMyLeave com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a833d-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a833d-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá PlanMyLeave é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a833d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PlanMyLeave is tooa user in Azure AD.</span></span> <span data-ttu-id="a833d-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá PlanMyLeave tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a833d-140">In other words, a link relationship between an Azure AD user and hello related user in PlanMyLeave needs toobe established.</span></span>

<span data-ttu-id="a833d-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="a833d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="a833d-142">tooconfigure e teste do Azure AD-início de sessão único com PlanMyLeave, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a833d-142">tooconfigure and test Azure AD single sign-on with PlanMyLeave, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a833d-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a833d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a833d-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a833d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a833d-145">**[Criar um utilizador de teste PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave um homólogo de Britta Simon no PlanMyLeave é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a833d-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - toohave a counterpart of Britta Simon in PlanMyLeave that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a833d-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a833d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a833d-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="a833d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a833d-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a833d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a833d-149">Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="a833d-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="a833d-150">**tooconfigure do Azure AD-início de sessão único com PlanMyLeave, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a833d-150">**tooconfigure Azure AD single sign-on with PlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="a833d-151">No portal de gestão do Azure de Olá, no Olá **PlanMyLeave** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="a833d-151">In hello Azure Management portal, on hello **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="a833d-153">No Olá **de sessão único-** página da caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a833d-153">On hello **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="a833d-155">No Olá **PlanMyLeave domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a833d-155">On hello **PlanMyLeave Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="a833d-157">a.</span><span class="sxs-lookup"><span data-stu-id="a833d-157">a.</span></span> <span data-ttu-id="a833d-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="a833d-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="a833d-159">b.</span><span class="sxs-lookup"><span data-stu-id="a833d-159">b.</span></span> <span data-ttu-id="a833d-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="a833d-160">In hello **Identifer** textbox, type a URL using hello following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a833d-161">Tenha em atenção que estes não são valores reais Olá.</span><span class="sxs-lookup"><span data-stu-id="a833d-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="a833d-162">Ter tooupdate estes valores com Olá real, inicie sessão no URL e o identificador.</span><span class="sxs-lookup"><span data-stu-id="a833d-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="a833d-163">Contacte [equipa de suporte de PlanMyLeave](mailto:support@planmyleave.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="a833d-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) tooget these values.</span></span>

4. <span data-ttu-id="a833d-164">No Olá **certificado de assinatura de SAML** secção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="a833d-164">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="a833d-166">No Olá **criar o novo certificado** caixa de diálogo, clique Olá ícone de calendário e selecione um **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="a833d-166">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="a833d-167">Em seguida, clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="a833d-167">Then click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="a833d-169">No Olá **certificado de assinatura de SAML** secção, selecione **tornar o novo certificado ativa** e clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="a833d-169">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="a833d-171">No pop-up de Olá **o certificado de Rollover** janela, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a833d-171">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="a833d-173">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a833d-173">On hello **SAML Signing Certificate** section, click **Certificate (base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="a833d-175">No Olá **PlanMyLeave configuração** secção, clique em **configurar PlanMyLeave** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="a833d-175">On hello **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** tooopen **Configure sign-on** window.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="a833d-178">Numa janela do browser web diferente, inicie sessão no seu inquilino PlanMyLeave como administrador.</span><span class="sxs-lookup"><span data-stu-id="a833d-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="a833d-179">Aceda demasiado**a configuração do sistema**.</span><span class="sxs-lookup"><span data-stu-id="a833d-179">Go too**System Setup**.</span></span> <span data-ttu-id="a833d-180">Em seguida, na Olá **gestão de segurança** secção clique **definições da empresa SAML** .</span><span class="sxs-lookup"><span data-stu-id="a833d-180">Then on hello **Security Management** section click **Company SAML settings** .</span></span>

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="a833d-182">No Olá **SAML definições** secção, clique em ícone do editor.</span><span class="sxs-lookup"><span data-stu-id="a833d-182">On hello **SAML Settings** section, click editor icon.</span></span>

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="a833d-184">No Olá **definições de atualização de SAML** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a833d-184">On hello **Update SAML Settings** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="a833d-186">a.</span><span class="sxs-lookup"><span data-stu-id="a833d-186">a.</span></span>  <span data-ttu-id="a833d-187">No Olá **URL de início de sessão** caixa de texto, coloque o valor Olá **único início de sessão no URL do serviço SAML** da janela de configuração de aplicação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a833d-187">In hello **Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="a833d-188">b.</span><span class="sxs-lookup"><span data-stu-id="a833d-188">b.</span></span>  <span data-ttu-id="a833d-189">Abra o ficheiro de certificado transferido no bloco de notas, copie apenas Olá conteúdo entre Olá---começar certificado--- e ---fim certificado----lo na sua área de transferência e, em seguida, cole-toohello **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a833d-189">Open your downloaded certificate file in notepad, copy only hello content between hello ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>

    <span data-ttu-id="a833d-190">c.</span><span class="sxs-lookup"><span data-stu-id="a833d-190">c.</span></span> <span data-ttu-id="a833d-191">Definir"**está activada**"demasiado"**Sim**".</span><span class="sxs-lookup"><span data-stu-id="a833d-191">Set "**Is Enable**" too"**Yes**".</span></span>

    <span data-ttu-id="a833d-192">d.</span><span class="sxs-lookup"><span data-stu-id="a833d-192">d.</span></span> <span data-ttu-id="a833d-193">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a833d-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a833d-194">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a833d-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="a833d-195">o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a833d-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="a833d-197">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a833d-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a833d-198">No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a833d-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a833d-200">Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="a833d-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a833d-202">Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a833d-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a833d-204">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a833d-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a833d-206">a.</span><span class="sxs-lookup"><span data-stu-id="a833d-206">a.</span></span> <span data-ttu-id="a833d-207">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a833d-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a833d-208">b.</span><span class="sxs-lookup"><span data-stu-id="a833d-208">b.</span></span> <span data-ttu-id="a833d-209">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a833d-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a833d-210">c.</span><span class="sxs-lookup"><span data-stu-id="a833d-210">c.</span></span> <span data-ttu-id="a833d-211">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="a833d-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a833d-212">d.</span><span class="sxs-lookup"><span data-stu-id="a833d-212">d.</span></span> <span data-ttu-id="a833d-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a833d-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="a833d-214">Criar um utilizador de teste PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="a833d-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="a833d-215">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="a833d-215">hello objective of this section is toocreate a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="a833d-216">PlanMyLeave suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.</span><span class="sxs-lookup"><span data-stu-id="a833d-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a833d-217">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="a833d-217">There is no action item for you in this section.</span></span> <span data-ttu-id="a833d-218">Será criado um novo utilizador durante uma tentativa tooaccess PlanMyLeave se não existir ainda.</span><span class="sxs-lookup"><span data-stu-id="a833d-218">A new user will be created during an attempt tooaccess PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="a833d-219">Se precisar de um utilizador de toocreate manualmente, terá de toocontact [equipa de suporte de PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="a833d-219">If you need toocreate an user manually, you need toocontact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a833d-220">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a833d-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a833d-221">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooPlanMyLeave de acesso.</span><span class="sxs-lookup"><span data-stu-id="a833d-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPlanMyLeave.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="a833d-223">**tooassign Britta Simon tooPlanMyLeave, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a833d-223">**tooassign Britta Simon tooPlanMyLeave, perform hello following steps:**</span></span>

1. <span data-ttu-id="a833d-224">No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a833d-224">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="a833d-226">Na lista de aplicações de Olá, selecione **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="a833d-226">In hello applications list, select **PlanMyLeave**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="a833d-228">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a833d-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="a833d-230">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="a833d-230">Click **Add** button.</span></span> <span data-ttu-id="a833d-231">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a833d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="a833d-233">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="a833d-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a833d-234">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a833d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a833d-235">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a833d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="a833d-236">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a833d-236">Testing single sign-on</span></span>

<span data-ttu-id="a833d-237">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a833d-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a833d-238">Ao clicar em mosaico de PlanMyLeave Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour PlanMyLeave aplicação.</span><span class="sxs-lookup"><span data-stu-id="a833d-238">When you click hello PlanMyLeave tile in hello Access Panel, you should get automatically signed-on tooyour PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a833d-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a833d-239">Additional resources</span></span>

* [<span data-ttu-id="a833d-240">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a833d-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a833d-241">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a833d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png