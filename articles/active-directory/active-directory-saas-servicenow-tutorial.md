---
title: "Tutorial: Integração do Azure Active Directory com o ServiceNow | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ServiceNow e ServiceNow rápida."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="a9eef-103">Tutorial: Integração do Azure Active Directory com o ServiceNow</span><span class="sxs-lookup"><span data-stu-id="a9eef-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="a9eef-104">Neste tutorial, saiba como toointegrate ServiceNow e ServiceNow Express com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9eef-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9eef-105">Integrar o ServiceNow e ServiceNow Express com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="a9eef-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="a9eef-106">Pode controlar no Azure AD que tenha acesso tooServiceNow e ServiceNow rápida</span><span class="sxs-lookup"><span data-stu-id="a9eef-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="a9eef-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooServiceNow e ServiceNow rápida (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9eef-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="a9eef-108">Pode gerir as contas numa localização central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="a9eef-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="a9eef-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a9eef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9eef-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a9eef-110">Prerequisites</span></span>
<span data-ttu-id="a9eef-111">tooconfigure integração do Azure AD com o ServiceNow e Express do ServiceNow, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a9eef-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="a9eef-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9eef-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a9eef-113">Para o ServiceNow, uma instância ou o inquilino do ServiceNow, versão Calgary ou superior</span><span class="sxs-lookup"><span data-stu-id="a9eef-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="a9eef-114">Para expressas ServiceNow, uma instância do ServiceNow rápida, versão Helsinki ou superior</span><span class="sxs-lookup"><span data-stu-id="a9eef-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="a9eef-115">inquilino de ServiceNow Olá tem de ter Olá [vários fornecedor único início de sessão no plug-in](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) ativada.</span><span class="sxs-lookup"><span data-stu-id="a9eef-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="a9eef-116">Isto pode ser feito [submeter um pedido de serviço](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="a9eef-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="a9eef-117">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a9eef-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="a9eef-118">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a9eef-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a9eef-119">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="a9eef-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a9eef-120">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9eef-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9eef-121">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a9eef-121">Scenario description</span></span>
<span data-ttu-id="a9eef-122">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a9eef-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9eef-123">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="a9eef-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9eef-124">A adição de ServiceNow de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="a9eef-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="a9eef-125">Configurar e testar o Azure AD de sessão único-ServiceNow ou ServiceNow rápida</span><span class="sxs-lookup"><span data-stu-id="a9eef-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="a9eef-126">A adição de ServiceNow de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="a9eef-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="a9eef-127">tooconfigure Olá integração do ServiceNow ou ServiceNow Express com o Azure AD, é necessário tooadd ServiceNow Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="a9eef-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="a9eef-128">**tooadd ServiceNow da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a9eef-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9eef-129">No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="a9eef-131">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="a9eef-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a9eef-132">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="a9eef-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicações][2]
4. <span data-ttu-id="a9eef-134">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="a9eef-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicações][3]
5. <span data-ttu-id="a9eef-136">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicações][4]
6. <span data-ttu-id="a9eef-138">Na caixa de pesquisa de Olá, escreva **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="a9eef-140">No painel de resultados de Olá, selecione **ServiceNow**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="a9eef-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9eef-142">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a9eef-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9eef-143">Nesta secção, configura e teste do Azure AD-início de sessão único com ServiceNow ou ServiceNow rápida com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a9eef-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9eef-144">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ServiceNow é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9eef-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="a9eef-145">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ServiceNow tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a9eef-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="a9eef-146">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="a9eef-147">tooconfigure e teste do Azure AD-início de sessão único com ServiceNow, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a9eef-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a9eef-148">**[Configurar o Azure AD Single Sign-On para ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a9eef-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a9eef-149">**[Configurar o Azure AD Single Sign-On para ServiceNow rápida](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a9eef-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="a9eef-150">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9eef-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="a9eef-151">**[Criar um utilizador de teste do ServiceNow](#creating-a-servicenow-test-user)**  -toohave um homólogo de Britta Simon no ServiceNow é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9eef-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="a9eef-152">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a9eef-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="a9eef-153">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="a9eef-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="a9eef-154">Se quiser tooconfigure ServiceNow omita o passo 2.</span><span class="sxs-lookup"><span data-stu-id="a9eef-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="a9eef-155">Da mesma forma, se quiser tooconfigure ServiceNow rápida omita passo 1.</span><span class="sxs-lookup"><span data-stu-id="a9eef-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="a9eef-156">Configurar o Azure AD início de sessão único para o ServiceNow</span><span class="sxs-lookup"><span data-stu-id="a9eef-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="a9eef-157">No portal clássico do Azure AD de Olá, no Olá **ServiceNow** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo .</span><span class="sxs-lookup"><span data-stu-id="a9eef-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="a9eef-158">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="a9eef-159">No Olá **como seria, como os utilizadores toosign no tooServiceNow** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="a9eef-160">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="a9eef-161">No Olá **configurar definições de aplicação** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a9eef-162">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC769497.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="a9eef-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="a9eef-163">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-163">a.</span></span> <span data-ttu-id="a9eef-164">no Olá **ServiceNow no URL sessão** caixa de texto, escreva o seu URL utilizado pela sua aplicação de ServiceNow utilizadores tooyour toosign-na seguir o padrão de Olá: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="a9eef-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="a9eef-165">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-165">b.</span></span> <span data-ttu-id="a9eef-166">No Olá **identificador** caixa de texto, escreva o seu URL utilizado pela sua aplicação de ServiceNow utilizadores tooyour toosign-na seguir o padrão de Olá: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="a9eef-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="a9eef-167">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-167">c.</span></span> <span data-ttu-id="a9eef-168">Clique em **Seguinte**</span><span class="sxs-lookup"><span data-stu-id="a9eef-168">Click **Next**</span></span>

4. <span data-ttu-id="a9eef-169">toohave do Azure AD automaticamente configurar ServiceNow para autenticação baseada em SAML, introduza o nome da instância de ServiceNow, nome de utilizador de admin e palavra-passe de administrador no Olá **automática configurar o início de sessão único** formam e clique em  *Configurar*.</span><span class="sxs-lookup"><span data-stu-id="a9eef-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="a9eef-170">Tenha em atenção que nome de utilizador de admin Olá fornecido tem de ter Olá **security_admin** função atribuída em ServiceNow para este toowork.</span><span class="sxs-lookup"><span data-stu-id="a9eef-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="a9eef-171">Caso contrário, toomanually configurar ServiceNow toouse do Azure AD como um fornecedor de identidade, clique em **configurar manualmente a aplicação Olá para o início de sessão único**, em seguida, clique em **seguinte** e Olá concluída passos seguintes.</span><span class="sxs-lookup"><span data-stu-id="a9eef-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="a9eef-172">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="a9eef-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="a9eef-173">No Olá **configurar o início de sessão único em ServiceNow** página, clique em **Transferir certificado**, guarde o ficheiro de certificado Olá localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a9eef-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="a9eef-174">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="a9eef-175">Início de sessão tooyour ServiceNow aplicação como um administrador.</span><span class="sxs-lookup"><span data-stu-id="a9eef-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="a9eef-176">Ativar Olá *integração - vários único início de sessão instalador de fornecedor* Plug-in seguindo Olá passos seguintes:</span><span class="sxs-lookup"><span data-stu-id="a9eef-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="a9eef-177">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-177">a.</span></span> <span data-ttu-id="a9eef-178">No painel de navegação de Olá no lado esquerdo Olá, aceda demasiado**definição de sistema** secção e, em seguida, clique em **plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="a9eef-179">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "ativar Plug-in")</span><span class="sxs-lookup"><span data-stu-id="a9eef-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="a9eef-180">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-180">b.</span></span> <span data-ttu-id="a9eef-181">Procurar *integração - vários único início de sessão instalador de fornecedor*.</span><span class="sxs-lookup"><span data-stu-id="a9eef-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="a9eef-182">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "ativar Plug-in")</span><span class="sxs-lookup"><span data-stu-id="a9eef-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="a9eef-183">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-183">c.</span></span> <span data-ttu-id="a9eef-184">Selecione o plug-in de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9eef-184">Select hello plugin.</span></span> <span data-ttu-id="a9eef-185">Rigth clique e selecione **ativar/atualização**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="a9eef-186">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-186">d.</span></span> <span data-ttu-id="a9eef-187">Clique em Olá **ativar** botão.</span><span class="sxs-lookup"><span data-stu-id="a9eef-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="a9eef-188">No painel de navegação de Olá no lado esquerdo Olá, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="a9eef-189">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="a9eef-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="a9eef-190">No Olá **várias propriedades do fornecedor de SSO** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="a9eef-191">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="a9eef-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="a9eef-192">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-192">a.</span></span> <span data-ttu-id="a9eef-193">Como **ativar o fornecedor de várias SSO**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="a9eef-194">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-194">b.</span></span> <span data-ttu-id="a9eef-195">Como **ativar registo de depuração obteve Olá fornecedor de várias integração SSO**, selecione **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="a9eef-196">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-196">c.</span></span> <span data-ttu-id="a9eef-197">No **campo Olá utilizador Olá tabela que...**  caixa de texto, tipo **user_name**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="a9eef-198">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-198">d.</span></span> <span data-ttu-id="a9eef-199">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-199">Click **Save**.</span></span>

10. <span data-ttu-id="a9eef-200">No painel de navegação de Olá no lado esquerdo Olá, clique em **certificados x509**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="a9eef-201">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="a9eef-202">No Olá **certificados x. 509** caixa de diálogo, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="a9eef-203">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="a9eef-204">No Olá **certificados x. 509** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="a9eef-205">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="a9eef-206">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-206">a.</span></span> <span data-ttu-id="a9eef-207">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-207">Click **New**.</span></span>
    
     <span data-ttu-id="a9eef-208">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-208">b.</span></span> <span data-ttu-id="a9eef-209">No Olá **nome** caixa de texto, escreva um nome para a sua configuração (por ex.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="a9eef-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="a9eef-210">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-210">c.</span></span> <span data-ttu-id="a9eef-211">Selecione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-211">Select **Active**.</span></span>
    
     <span data-ttu-id="a9eef-212">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-212">d.</span></span> <span data-ttu-id="a9eef-213">Como **formato**, selecione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="a9eef-214">e.</span><span class="sxs-lookup"><span data-stu-id="a9eef-214">e.</span></span> <span data-ttu-id="a9eef-215">Como **tipo**, selecione **confiar o arquivo de certificados**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="a9eef-216">f.</span><span class="sxs-lookup"><span data-stu-id="a9eef-216">f.</span></span> <span data-ttu-id="a9eef-217">Abra o certificado codificado em Base64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **PEM certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9eef-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="a9eef-218">g.</span><span class="sxs-lookup"><span data-stu-id="a9eef-218">g.</span></span> <span data-ttu-id="a9eef-219">Clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-219">Click **Update**.</span></span>

13. <span data-ttu-id="a9eef-220">No painel de navegação de Olá no lado esquerdo Olá, clique em **fornecedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="a9eef-221">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="a9eef-222">No Olá **fornecedores de identidade** caixa de diálogo, clique em **novo**:</span><span class="sxs-lookup"><span data-stu-id="a9eef-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="a9eef-223">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="a9eef-224">No Olá **fornecedores de identidade** caixa de diálogo, clique em **SAML2 atualização1?**:</span><span class="sxs-lookup"><span data-stu-id="a9eef-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="a9eef-225">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="a9eef-226">Na caixa de diálogo de propriedades de atualização1 SAML2 Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="a9eef-227">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="a9eef-228">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-228">a.</span></span> <span data-ttu-id="a9eef-229">no Olá **nome** caixa de texto, escreva um nome para a sua configuração (por ex.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="a9eef-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="a9eef-230">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-230">b.</span></span> <span data-ttu-id="a9eef-231">No Olá **campo utilizador** caixa de texto, tipo **e-mail** ou **user_name**, consoante o campo que é utilizado toouniquely identificar os utilizadores na sua implementação do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="a9eef-232">Pode tooemit configue do Azure AD ou ID de utilizador Olá do Azure AD (nome principal de utilizador) ou Olá endereço de correio eletrónico como Olá Identificador exclusivo no token SAML Olá por vai toohello **ServiceNow > atributos > Single Sign-On** secção Olá portal clássico do Azure e mapeamento Olá pretendido campo toohello **nameidentifier** atributo.</span><span class="sxs-lookup"><span data-stu-id="a9eef-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="a9eef-233">valor de Olá armazenado para o atributo selecionado Olá no Azure AD (por exemplo, nome principal de utilizador) tem de corresponder ao valor de Olá armazenado no ServiceNow para o campo de Olá introduzido (por exemplo, user_name)</span><span class="sxs-lookup"><span data-stu-id="a9eef-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="a9eef-234">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-234">c.</span></span> <span data-ttu-id="a9eef-235">No portal clássico do Azure AD de Olá, copie Olá **ID do fornecedor de identidade** valor e, em seguida, cole-o Olá **URL do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9eef-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="a9eef-236">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-236">d.</span></span> <span data-ttu-id="a9eef-237">No portal clássico do Azure AD de Olá, copie Olá **URL de pedido de autenticação** valor e, em seguida, cole-o Olá **AuthnRequest do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9eef-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="a9eef-238">e.</span><span class="sxs-lookup"><span data-stu-id="a9eef-238">e.</span></span> <span data-ttu-id="a9eef-239">No portal clássico do Azure AD de Olá, copie Olá **único URL de serviço Sign-Out** valor e, em seguida, cole-o Olá **SingleLogoutRequest do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9eef-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="a9eef-240">f.</span><span class="sxs-lookup"><span data-stu-id="a9eef-240">f.</span></span> <span data-ttu-id="a9eef-241">No Olá **home page do ServiceNow** caixa de texto, tipo Olá URL da sua home page de instância de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a9eef-242">Home page de instância do ServiceNow Olá é uma concatenação do seu **ServieNow URL de inquilino** e **/navpage.do** (por ex.:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="a9eef-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="a9eef-243">g.</span><span class="sxs-lookup"><span data-stu-id="a9eef-243">g.</span></span> <span data-ttu-id="a9eef-244">No Olá **ID de entidade / emissor** caixa de texto, tipo Olá URL do seu inquilino do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="a9eef-245">h.</span><span class="sxs-lookup"><span data-stu-id="a9eef-245">h.</span></span> <span data-ttu-id="a9eef-246">No Olá **URL público-alvo** caixa de texto, tipo Olá URL do seu inquilino do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="a9eef-247">posso.</span><span class="sxs-lookup"><span data-stu-id="a9eef-247">i.</span></span> <span data-ttu-id="a9eef-248">No Olá **protocolo do enlace para Olá do IDP SingleLogoutRequest** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:2.0:bindings:HTTP-redirecionar**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="a9eef-249">j.</span><span class="sxs-lookup"><span data-stu-id="a9eef-249">j.</span></span> <span data-ttu-id="a9eef-250">Na caixa de texto de política de NameID Olá, escreva **urn: oasis: os nomes: tc: SAML:1.1:nameid-formato: não especificado**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="a9eef-251">k.</span><span class="sxs-lookup"><span data-stu-id="a9eef-251">k.</span></span> <span data-ttu-id="a9eef-252">Anular seleção de **criar um AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="a9eef-253">l.</span><span class="sxs-lookup"><span data-stu-id="a9eef-253">l.</span></span> <span data-ttu-id="a9eef-254">No Olá **AuthnContextClassRef método**, tipo `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="a9eef-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="a9eef-255">Só é necessária se estiverem organização apenas de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a9eef-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="a9eef-256">Se estiver a utilizar no local ADFS ou MFA para a autenticação, em seguida, não deve configurar este valor.</span><span class="sxs-lookup"><span data-stu-id="a9eef-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="a9eef-257">m.</span><span class="sxs-lookup"><span data-stu-id="a9eef-257">m.</span></span> <span data-ttu-id="a9eef-258">No **desfasamento de relógio** caixa de texto, tipo **60**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="a9eef-259">n.</span><span class="sxs-lookup"><span data-stu-id="a9eef-259">n.</span></span> <span data-ttu-id="a9eef-260">Como **início de sessão único no Script**, selecione **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="a9eef-261">Nã.</span><span class="sxs-lookup"><span data-stu-id="a9eef-261">o.</span></span> <span data-ttu-id="a9eef-262">Como **x509 certificado**, selecione o certificado de Olá que criou no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="a9eef-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="a9eef-263">p.</span><span class="sxs-lookup"><span data-stu-id="a9eef-263">p.</span></span> <span data-ttu-id="a9eef-264">Clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="a9eef-265">No portal clássico do Azure AD de Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="a9eef-266">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="a9eef-267">No Olá **único início de sessão confirmação** página, clique em **concluída**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="a9eef-268">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="a9eef-269">Configurar o Azure AD início de sessão único para ServiceNow rápida</span><span class="sxs-lookup"><span data-stu-id="a9eef-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="a9eef-270">No portal clássico do Azure AD de Olá, no Olá **ServiceNow** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo .</span><span class="sxs-lookup"><span data-stu-id="a9eef-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="a9eef-271">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749323.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="a9eef-272">No Olá **como seria, como os utilizadores toosign no tooServiceNow** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="a9eef-273">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749324.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="a9eef-274">No Olá **configurar definições de aplicação** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a9eef-275">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC769497.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="a9eef-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="a9eef-276">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-276">a.</span></span> <span data-ttu-id="a9eef-277">no Olá **ServiceNow no URL sessão** caixa de texto, escreva o seu URL utilizado pela sua aplicação de ServiceNow utilizadores tooyour toosign-na seguir o padrão de Olá: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="a9eef-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="a9eef-278">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-278">b.</span></span> <span data-ttu-id="a9eef-279">No Olá **URL do emissor** caixa de texto, escreva o seu URL utilizado pela sua aplicação de ServiceNow utilizadores tooyour toosign-na seguir o padrão de Olá `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="a9eef-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="a9eef-280">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-280">c.</span></span> <span data-ttu-id="a9eef-281">Clique em **Seguinte**</span><span class="sxs-lookup"><span data-stu-id="a9eef-281">Click **Next**</span></span>

4. <span data-ttu-id="a9eef-282">Clique em **configurar manualmente a aplicação Olá para o início de sessão único**, em seguida, clique em **seguinte** e Olá concluir os passos seguintes.</span><span class="sxs-lookup"><span data-stu-id="a9eef-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="a9eef-283">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="a9eef-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="a9eef-284">No Olá **configurar o início de sessão único em ServiceNow** página, clique em **Transferir certificado**, guarde o ficheiro de certificado Olá localmente no seu computador e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="a9eef-285">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC749325.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="a9eef-286">Início de sessão tooyour ServiceNow rápida aplicação como um administrador.</span><span class="sxs-lookup"><span data-stu-id="a9eef-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="a9eef-287">No painel de navegação de Olá no lado esquerdo Olá, clique em **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="a9eef-288">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="a9eef-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="a9eef-289">No Olá **Single Sign-On** caixa de diálogo, clique em Olá configuração no ícone no limite superior de Olá direita e defina hello seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="a9eef-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="a9eef-290">![Configurar o URL da aplicação](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="a9eef-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="a9eef-291">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-291">a.</span></span> <span data-ttu-id="a9eef-292">Ativar/desativar **ativar o fornecedor de várias SSO** toohello direito.</span><span class="sxs-lookup"><span data-stu-id="a9eef-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="a9eef-293">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-293">b.</span></span> <span data-ttu-id="a9eef-294">Ativar/desativar **depuração de ativar o registo para Olá fornecedor de várias integração SSO** toohello direito.</span><span class="sxs-lookup"><span data-stu-id="a9eef-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="a9eef-295">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-295">c.</span></span> <span data-ttu-id="a9eef-296">No **campo Olá utilizador Olá tabela que...**  caixa de texto, tipo **user_name**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="a9eef-297">No Olá **Single Sign-On** caixa de diálogo, clique em **adicionar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="a9eef-298">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="a9eef-299">No Olá **certificados x. 509** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="a9eef-300">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="a9eef-301">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-301">a.</span></span> <span data-ttu-id="a9eef-302">No Olá **nome** caixa de texto, escreva um nome para a sua configuração (por ex.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="a9eef-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="a9eef-303">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-303">b.</span></span> <span data-ttu-id="a9eef-304">Selecione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-304">Select **Active**.</span></span>
    
    <span data-ttu-id="a9eef-305">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-305">c.</span></span> <span data-ttu-id="a9eef-306">Como **formato**, selecione **PEM**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="a9eef-307">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-307">d.</span></span> <span data-ttu-id="a9eef-308">Como **tipo**, selecione **confiar o arquivo de certificados**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="a9eef-309">e.</span><span class="sxs-lookup"><span data-stu-id="a9eef-309">e.</span></span> <span data-ttu-id="a9eef-310">Crie um ficheiro de codificado em Base64 a partir do seu certificado transferido.</span><span class="sxs-lookup"><span data-stu-id="a9eef-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a9eef-311">Para obter mais detalhes, consulte [como tooconvert um binário de certificado para um ficheiro de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a9eef-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="a9eef-312">f.</span><span class="sxs-lookup"><span data-stu-id="a9eef-312">f.</span></span> <span data-ttu-id="a9eef-313">Abra o certificado codificado em Base64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **PEM certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9eef-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="a9eef-314">g.</span><span class="sxs-lookup"><span data-stu-id="a9eef-314">g.</span></span> <span data-ttu-id="a9eef-315">Clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-315">Click **Update**.</span></span>
11. <span data-ttu-id="a9eef-316">No Olá **Single Sign-On** caixa de diálogo, clique em **Adicionar nova IdP**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="a9eef-317">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="a9eef-318">No Olá **adicionar novo fornecedor de identidade** caixa de diálogo, em **configurar o fornecedor de identidade**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="a9eef-319">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="a9eef-320">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-320">a.</span></span> <span data-ttu-id="a9eef-321">no Olá **nome** caixa de texto, escreva um nome para a sua configuração (por ex.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="a9eef-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="a9eef-322">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-322">b.</span></span> <span data-ttu-id="a9eef-323">No portal clássico do Azure AD de Olá, copie Olá **ID do fornecedor de identidade** valor e, em seguida, cole-o Olá **URL do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9eef-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="a9eef-324">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-324">c.</span></span> <span data-ttu-id="a9eef-325">No portal clássico do Azure AD de Olá, copie Olá **URL de pedido de autenticação** valor e, em seguida, cole-o Olá **AuthnRequest do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9eef-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="a9eef-326">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-326">d.</span></span> <span data-ttu-id="a9eef-327">No portal clássico do Azure AD de Olá, copie Olá **único URL de serviço Sign-Out** valor e, em seguida, cole-o Olá **SingleLogoutRequest do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9eef-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="a9eef-328">e.</span><span class="sxs-lookup"><span data-stu-id="a9eef-328">e.</span></span> <span data-ttu-id="a9eef-329">Como **certificado do fornecedor de identidade**, selecione o certificado de Olá que criou no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="a9eef-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="a9eef-330">Clique em **definições avançadas**e, em **propriedades do fornecedor de identidade adicionais**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="a9eef-331">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="a9eef-332">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-332">a.</span></span> <span data-ttu-id="a9eef-333">No Olá **protocolo do enlace para Olá do IDP SingleLogoutRequest** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:2.0:bindings:HTTP-redirecionar**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="a9eef-334">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-334">b.</span></span> <span data-ttu-id="a9eef-335">No Olá **NameID política** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:1.1:nameid-formato: não especificado**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="a9eef-336">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-336">c.</span></span> <span data-ttu-id="a9eef-337">No Olá **AuthnContextClassRef método**, tipo **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="a9eef-338">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-338">d.</span></span> <span data-ttu-id="a9eef-339">Anular seleção de **criar um AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="a9eef-340">Em **propriedades adicionais de fornecedor de serviço**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="a9eef-341">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="a9eef-342">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-342">a.</span></span> <span data-ttu-id="a9eef-343">No Olá **home page do ServiceNow** caixa de texto, tipo Olá URL da sua home page de instância de ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="a9eef-344">Home page de instância do ServiceNow Olá é uma concatenação do seu **ServieNow URL de inquilino** e **/navpage.do** (por ex.: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="a9eef-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="a9eef-345">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-345">b.</span></span> <span data-ttu-id="a9eef-346">No Olá **ID de entidade / emissor** caixa de texto, tipo Olá URL do seu inquilino do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="a9eef-347">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-347">c.</span></span> <span data-ttu-id="a9eef-348">No Olá **URI de audiência** caixa de texto, tipo Olá URL do seu inquilino do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="a9eef-349">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-349">d.</span></span> <span data-ttu-id="a9eef-350">No **desfasamento de relógio** caixa de texto, tipo **60**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="a9eef-351">e.</span><span class="sxs-lookup"><span data-stu-id="a9eef-351">e.</span></span> <span data-ttu-id="a9eef-352">No Olá **campo utilizador** caixa de texto, tipo **e-mail** ou **user_name**, consoante o campo que é utilizado toouniquely identificar os utilizadores na sua implementação do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="a9eef-353">Pode tooemit configue do Azure AD ou ID de utilizador Olá do Azure AD (nome principal de utilizador) ou Olá endereço de correio eletrónico como Olá Identificador exclusivo no token SAML Olá por vai toohello **ServiceNow > atributos > Single Sign-On** secção Olá portal clássico do Azure e mapeamento Olá pretendido campo toohello **nameidentifier** atributo.</span><span class="sxs-lookup"><span data-stu-id="a9eef-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="a9eef-354">valor de Olá armazenado para o atributo selecionado Olá no Azure AD (por exemplo, nome principal de utilizador) tem de corresponder ao valor de Olá armazenado no ServiceNow para o campo de Olá introduzido (por exemplo, user_name)</span><span class="sxs-lookup"><span data-stu-id="a9eef-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="a9eef-355">f.</span><span class="sxs-lookup"><span data-stu-id="a9eef-355">f.</span></span> <span data-ttu-id="a9eef-356">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-356">Click **Save**.</span></span> 

3. <span data-ttu-id="a9eef-357">No portal clássico do Azure AD de Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="a9eef-358">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="a9eef-359">No Olá **único início de sessão confirmação** página, clique em **concluída**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="a9eef-360">![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="a9eef-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="a9eef-361">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="a9eef-361">Configuring user provisioning</span></span>
<span data-ttu-id="a9eef-362">o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizadores do utilizador do Active Directory tooServiceNow de contas.</span><span class="sxs-lookup"><span data-stu-id="a9eef-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="a9eef-363">tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="a9eef-364">No Olá Azure Management portal clássico, no Olá **ServiceNow** página de integração de aplicações, clique em **configurar o aprovisionamento de utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="a9eef-365">![Aprovisionamento de utilizadores](./media/active-directory-saas-servicenow-tutorial/IC769498.png "aprovisionamento de utilizadores")</span><span class="sxs-lookup"><span data-stu-id="a9eef-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="a9eef-366">No Olá **introduza aprovisionamento de utilizadores automática do ServiceNow credenciais tooenable** , indique Olá seguintes definições de configuração:</span><span class="sxs-lookup"><span data-stu-id="a9eef-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="a9eef-367">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-367">a.</span></span> <span data-ttu-id="a9eef-368">No Olá **nome da instância do ServiceNow** caixa de texto, o nome de instância do tipo Olá ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="a9eef-369">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-369">b.</span></span> <span data-ttu-id="a9eef-370">No Olá **nome de utilizador de Admin do ServiceNow** caixa de texto, nome do tipo Olá de Olá conta de administrador do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="a9eef-371">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-371">c.</span></span> <span data-ttu-id="a9eef-372">No Olá **palavra-passe de administrador de ServiceNow** caixa de texto, tipo Olá palavra-passe desta conta.</span><span class="sxs-lookup"><span data-stu-id="a9eef-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="a9eef-373">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-373">d.</span></span> <span data-ttu-id="a9eef-374">Clique em **validar** tooverify a configuração.</span><span class="sxs-lookup"><span data-stu-id="a9eef-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="a9eef-375">e.</span><span class="sxs-lookup"><span data-stu-id="a9eef-375">e.</span></span> <span data-ttu-id="a9eef-376">Clique em Olá **seguinte** Olá do botão tooopen **passos** página.</span><span class="sxs-lookup"><span data-stu-id="a9eef-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="a9eef-377">f.</span><span class="sxs-lookup"><span data-stu-id="a9eef-377">f.</span></span> <span data-ttu-id="a9eef-378">Se pretender que tooprovision todos os utilizadores toothis aplicação, selecione "**aprovisionar automaticamente todas as contas de utilizador na aplicação do Olá diretório toothis**".</span><span class="sxs-lookup"><span data-stu-id="a9eef-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="a9eef-379">![Próximos passos](./media/active-directory-saas-servicenow-tutorial/IC698804.png "próximos passos")</span><span class="sxs-lookup"><span data-stu-id="a9eef-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="a9eef-380">g.</span><span class="sxs-lookup"><span data-stu-id="a9eef-380">g.</span></span> <span data-ttu-id="a9eef-381">No Olá **passos** página, clique em **concluída** toosave a configuração.</span><span class="sxs-lookup"><span data-stu-id="a9eef-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9eef-382">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9eef-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9eef-383">Nesta secção, vai criar um utilizador de teste no portal clássico Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9eef-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][20]

<span data-ttu-id="a9eef-385">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a9eef-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9eef-386">No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="a9eef-388">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="a9eef-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="a9eef-389">lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a9eef-391">Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="a9eef-393">No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="a9eef-395">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-395">a.</span></span> <span data-ttu-id="a9eef-396">Como tipo de utilizador, selecione o novo utilizador na sua organização.</span><span class="sxs-lookup"><span data-stu-id="a9eef-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="a9eef-397">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-397">b.</span></span> <span data-ttu-id="a9eef-398">No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="a9eef-399">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-399">c.</span></span> <span data-ttu-id="a9eef-400">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-400">Click **Next**.</span></span>

6. <span data-ttu-id="a9eef-401">No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="a9eef-403">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-403">a.</span></span> <span data-ttu-id="a9eef-404">No Olá **nome próprio** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="a9eef-405">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-405">b.</span></span> <span data-ttu-id="a9eef-406">No Olá **Apelido** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="a9eef-407">c.</span><span class="sxs-lookup"><span data-stu-id="a9eef-407">c.</span></span> <span data-ttu-id="a9eef-408">No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="a9eef-409">d.</span><span class="sxs-lookup"><span data-stu-id="a9eef-409">d.</span></span> <span data-ttu-id="a9eef-410">No Olá **função** lista, selecione **utilizador**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="a9eef-411">e.</span><span class="sxs-lookup"><span data-stu-id="a9eef-411">e.</span></span> <span data-ttu-id="a9eef-412">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-412">Click **Next**.</span></span>

7. <span data-ttu-id="a9eef-413">No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="a9eef-415">No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a9eef-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="a9eef-417">a.</span><span class="sxs-lookup"><span data-stu-id="a9eef-417">a.</span></span> <span data-ttu-id="a9eef-418">Anote o valor Olá Olá **nova palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="a9eef-419">b.</span><span class="sxs-lookup"><span data-stu-id="a9eef-419">b.</span></span> <span data-ttu-id="a9eef-420">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="a9eef-421">Criar um utilizador de teste do ServiceNow</span><span class="sxs-lookup"><span data-stu-id="a9eef-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="a9eef-422">Nesta secção, vai criar um utilizador chamado Britta Simon ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="a9eef-423">Nesta secção, vai criar um utilizador chamado Britta Simon ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="a9eef-424">Se não souber como tooadd no seu ServiceNow ou ServiceNow rápida da conta de utilizador, contacte a equipa de suporte do ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="a9eef-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a9eef-425">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9eef-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="a9eef-426">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooServiceNow de acesso.</span><span class="sxs-lookup"><span data-stu-id="a9eef-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="a9eef-428">**tooassign Britta Simon tooServiceNow, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a9eef-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="a9eef-429">No portal clássico Olá, clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="a9eef-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribua o utilizador][201] 

2. <span data-ttu-id="a9eef-431">Na lista de aplicações de Olá, selecione **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="a9eef-433">No menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribua o utilizador][203] 

4. <span data-ttu-id="a9eef-435">Na lista de todos os utilizadores de Olá, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="a9eef-436">Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="a9eef-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribua o utilizador][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="a9eef-438">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a9eef-438">Testing single sign-on</span></span>
<span data-ttu-id="a9eef-439">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a9eef-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a9eef-440">Ao clicar em mosaico de ServiceNow Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour ServiceNow aplicação.</span><span class="sxs-lookup"><span data-stu-id="a9eef-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9eef-441">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a9eef-441">Additional resources</span></span>
* [<span data-ttu-id="a9eef-442">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9eef-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9eef-443">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9eef-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
