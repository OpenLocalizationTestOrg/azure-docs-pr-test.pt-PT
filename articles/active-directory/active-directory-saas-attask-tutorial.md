---
title: "Tutorial: Integração do Azure Active Directory com @Task| Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="8ac0f-103">Tutorial: Integração do Azure Active Directory com o@Task</span><span class="sxs-lookup"><span data-stu-id="8ac0f-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="8ac0f-104">o objetivo deste tutorial Olá é tooshow como toointegrate @Task com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ac0f-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="8ac0f-105">Integrar @Task com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="8ac0f-106">Pode controlar no Azure AD quem tem acessotoo@Task</span><span class="sxs-lookup"><span data-stu-id="8ac0f-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="8ac0f-107">Pode ativar os seus utilizadores tooautomatically obter com sessão iniciada too@Task (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac0f-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8ac0f-108">Pode gerir as contas numa localização central - Olá Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="8ac0f-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="8ac0f-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ac0f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ac0f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ac0f-110">Prerequisites</span></span>
<span data-ttu-id="8ac0f-111">integração de tooconfigure do Azure AD com @Task, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="8ac0f-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac0f-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8ac0f-113">Um @Task início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="8ac0f-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ac0f-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8ac0f-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8ac0f-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8ac0f-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ac0f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="8ac0f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8ac0f-118">Scenario Description</span></span>
<span data-ttu-id="8ac0f-119">o objetivo deste tutorial Olá é tooenable tootest do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="8ac0f-120">cenário de Olá descrito neste tutorial consiste em três blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="8ac0f-121">Adicionar @Task da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="8ac0f-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="8ac0f-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="8ac0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="8ac0f-123">Adicionar @Task da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="8ac0f-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="8ac0f-124">integração de Olá tooconfigure de @Task com o Azure AD, terá de tooadd @Task Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ac0f-125">**tooadd @Task da Galeria de Olá, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8ac0f-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac0f-126">No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="8ac0f-128">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="8ac0f-129">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicações][2] 
4. <span data-ttu-id="8ac0f-131">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicações][3] 
5. <span data-ttu-id="8ac0f-133">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicações][4] 
6. <span data-ttu-id="8ac0f-135">Na caixa de pesquisa de Olá, escreva  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="8ac0f-135">In hello search box, type **@Task**.</span></span>
   
    ![Aplicações][5] 
7. <span data-ttu-id="8ac0f-137">No painel de resultados de Olá, selecione  **@Task** e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Aplicações][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ac0f-139">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="8ac0f-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ac0f-140">Olá objetivo desta secção é tooshow tem como único tooconfigure e teste do Azure AD início de sessão com @Task com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8ac0f-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ac0f-141">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá @Task tooan utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="8ac0f-142">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados utilizador @Task tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="8ac0f-143">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no @Task.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="8ac0f-144">tooconfigure e teste do Azure AD de sessão único-com @Task, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ac0f-145">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ac0f-146">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ac0f-147">**[Criar um @Tasktest utilizador](#creating-a-halogen-software-test-user)**  -toohave uma homólogo de Britta Simon no @Taskthat é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="8ac0f-148">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ac0f-149">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ac0f-150">Configurar o Azure AD início de sessão único</span><span class="sxs-lookup"><span data-stu-id="8ac0f-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="8ac0f-151">o objetivo desta secção Olá é tooenable do Azure AD início de sessão no portal clássico do Azure de Olá e tooconfigure-início de sessão único na sua @Task aplicação.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="8ac0f-152">**tooconfigure do Azure AD-início de sessão único com @Task, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8ac0f-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac0f-153">No Olá portal clássico do Azure, no Olá  **@Task**  página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar Single Sign-On**  caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar o início de sessão único][6] 
2. <span data-ttu-id="8ac0f-155">No Olá **como faria, como os utilizadores toosign num too@Task**  página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD início de sessão único][7] 
3. <span data-ttu-id="8ac0f-157">No Olá **configurar definições de aplicação** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Configurar definições da aplicação][8] 
   
     <span data-ttu-id="8ac0f-159">a.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-159">a.</span></span> <span data-ttu-id="8ac0f-160">No Olá **URL de início de sessão** caixa de texto, tipo Olá URL utilizado por utilizadores em toosign tooyour @Task aplicação (por ex.:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="8ac0f-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="8ac0f-161">b.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-161">b.</span></span> <span data-ttu-id="8ac0f-162">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-162">Click **Next**.</span></span>
4. <span data-ttu-id="8ac0f-163">No Olá **configurar início de sessão único em @Task**  página, clique em **transferir metadados**, guarde o ficheiro de metadados de Olá localmente no seu computador e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![O que é o Azure AD Connect][9] 
5. <span data-ttu-id="8ac0f-165">Início de sessão tooyour @Task site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="8ac0f-166">Aceda demasiado**início de sessão único na configuração**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="8ac0f-167">No Olá **Single Sign-On** caixa de diálogo, efetuar Olá os passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8ac0f-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![Configurar o início de sessão único][23]
   
    <span data-ttu-id="8ac0f-169">a.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-169">a.</span></span> <span data-ttu-id="8ac0f-170">Como **tipo**, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="8ac0f-171">b.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-171">b.</span></span> <span data-ttu-id="8ac0f-172">Selecione **ID do fornecedor de serviço**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="8ac0f-173">c.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-173">c.</span></span> <span data-ttu-id="8ac0f-174">No portal clássico do Azure Olá, copie Olá **URL de início de sessão remoto**e, em seguida, cole-o Olá **URL do Portal de início de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="8ac0f-175">d.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-175">d.</span></span> <span data-ttu-id="8ac0f-176">No portal clássico do Azure Olá, copie Olá **único URL de serviço Sign-Out**e, em seguida, cole-o Olá **Sign-Out URL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="8ac0f-177">e.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-177">e.</span></span> <span data-ttu-id="8ac0f-178">No portal clássico do Azure Olá, copie Olá **alterar palavra-passe URL**e, em seguida, cole-o Olá **alterar palavra-passe URL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="8ac0f-179">f.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-179">f.</span></span> <span data-ttu-id="8ac0f-180">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-180">Click **Save**.</span></span>
8. <span data-ttu-id="8ac0f-181">No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![O que é o Azure AD Connect][10]
9. <span data-ttu-id="8ac0f-183">No Olá **único início de sessão confirmação** página, clique em **concluída**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![O que é o Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ac0f-185">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac0f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ac0f-186">o objetivo desta secção Olá é toocreate um utilizador de teste no portal clássico do Azure chamado Britta Simon de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![Criar utilizador do Azure AD][20]

<span data-ttu-id="8ac0f-188">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8ac0f-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac0f-189">No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="8ac0f-191">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="8ac0f-192">lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="8ac0f-194">Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="8ac0f-196">No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="8ac0f-198">a.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-198">a.</span></span> <span data-ttu-id="8ac0f-199">Como tipo de utilizador, selecione o novo utilizador na sua organização.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="8ac0f-200">b.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-200">b.</span></span> <span data-ttu-id="8ac0f-201">No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="8ac0f-202">c.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-202">c.</span></span> <span data-ttu-id="8ac0f-203">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-203">Click **Next**.</span></span>
6. <span data-ttu-id="8ac0f-204">No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="8ac0f-206">a.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-206">a.</span></span> <span data-ttu-id="8ac0f-207">No Olá **nome próprio** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="8ac0f-208">b.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-208">b.</span></span> <span data-ttu-id="8ac0f-209">No Olá **Apelido** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="8ac0f-210">c.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-210">c.</span></span> <span data-ttu-id="8ac0f-211">No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="8ac0f-212">d.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-212">d.</span></span> <span data-ttu-id="8ac0f-213">No Olá **função** lista, selecione **utilizador**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="8ac0f-214">e.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-214">e.</span></span> <span data-ttu-id="8ac0f-215">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-215">Click **Next**.</span></span>

7. <span data-ttu-id="8ac0f-216">No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="8ac0f-218">No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="8ac0f-220">a.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-220">a.</span></span> <span data-ttu-id="8ac0f-221">Anote o valor Olá Olá **nova palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="8ac0f-222">b.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-222">b.</span></span> <span data-ttu-id="8ac0f-223">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="8ac0f-224">Criar um @Task utilizador de teste</span><span class="sxs-lookup"><span data-stu-id="8ac0f-224">Creating an @Task test user</span></span>
<span data-ttu-id="8ac0f-225">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon no @Task.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="8ac0f-226">**toocreate um utilizador chamado Britta Simon @Task, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8ac0f-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac0f-227">Início de sessão tooyour @Task site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="8ac0f-228">No menu de Olá na parte superior do Olá, clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="8ac0f-229">Clique em **nova pessoa**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="8ac0f-230">Na caixa de diálogo de nova pessoa Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8ac0f-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![Criar um @Task utilizador de teste][21] 
   
    <span data-ttu-id="8ac0f-232">a.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-232">a.</span></span> <span data-ttu-id="8ac0f-233">No Olá **nome próprio** caixa de texto, escreva "Britta".</span><span class="sxs-lookup"><span data-stu-id="8ac0f-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="8ac0f-234">b.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-234">b.</span></span> <span data-ttu-id="8ac0f-235">No Olá **Apelido** caixa de texto, escreva "Simon".</span><span class="sxs-lookup"><span data-stu-id="8ac0f-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="8ac0f-236">c.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-236">c.</span></span> <span data-ttu-id="8ac0f-237">No Olá **endereço de correio eletrónico** caixa de texto, escreva o endereço de correio eletrónico de Britta Simon no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="8ac0f-238">d.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-238">d.</span></span> <span data-ttu-id="8ac0f-239">Clique em **Adicionar pessoa**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8ac0f-240">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac0f-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="8ac0f-241">objetivo Olá desta secção é tooenabling Britta Simon toouse do Azure-início de sessão único, concedendo o respetivo acesso too@Task.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="8ac0f-243">**tooassign Britta Simon too@Task, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8ac0f-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac0f-244">Olá, Azure portal clássico, a vista de aplicações Olá tooopen, na vista de diretório Olá, clique em **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribua o utilizador][201] 
2. <span data-ttu-id="8ac0f-246">Na lista de aplicações de Olá, selecione  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="8ac0f-246">In hello applications list, select **@Task**.</span></span>
   
    ![Atribua o utilizador][202] 
3. <span data-ttu-id="8ac0f-248">No menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribua o utilizador][203] 
4. <span data-ttu-id="8ac0f-250">Na lista de utilizadores Olá, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8ac0f-251">Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribua o utilizador][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="8ac0f-253">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="8ac0f-253">Testing Single Sign-On</span></span>
<span data-ttu-id="8ac0f-254">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="8ac0f-255">Ao clicar em Olá @Task Olá de mosaico no painel de acesso, deve obter automaticamente com sessão iniciada tooyour @Task aplicação.</span><span class="sxs-lookup"><span data-stu-id="8ac0f-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ac0f-256">Recursos Adicionais</span><span class="sxs-lookup"><span data-stu-id="8ac0f-256">Additional Resources</span></span>
* [<span data-ttu-id="8ac0f-257">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ac0f-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ac0f-258">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ac0f-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






