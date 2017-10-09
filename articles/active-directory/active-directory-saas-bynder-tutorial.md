---
title: "Tutorial: Integração do Azure Active Directory com Bynder | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="a788e-103">Tutorial: Integração do Azure Active Directory com Bynder</span><span class="sxs-lookup"><span data-stu-id="a788e-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="a788e-104">o objetivo deste tutorial Olá é tooshow como toointegrate Bynder com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a788e-104">hello objective of this tutorial is tooshow you how toointegrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a788e-105">Integrar Bynder com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="a788e-105">Integrating Bynder with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="a788e-106">Pode controlar no Azure AD que tenha acesso tooBynder</span><span class="sxs-lookup"><span data-stu-id="a788e-106">You can control in Azure AD who has access tooBynder</span></span>
* <span data-ttu-id="a788e-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooBynder-início de sessão único (SSO) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a788e-107">You can enable your users tooautomatically get signed-on tooBynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="a788e-108">Pode gerir as contas numa localização central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="a788e-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="a788e-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a788e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a788e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a788e-110">Prerequisites</span></span>
<span data-ttu-id="a788e-111">integração do Azure AD com Bynder tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a788e-111">tooconfigure Azure AD integration with Bynder, you need hello following items:</span></span>

* <span data-ttu-id="a788e-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a788e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a788e-113">Um Bynder início de sessão único (SSO) ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="a788e-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="a788e-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a788e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="a788e-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a788e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a788e-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="a788e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a788e-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter um [avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a788e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a788e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a788e-118">Scenario description</span></span>
<span data-ttu-id="a788e-119">o objetivo deste tutorial Olá é tooenable tootest SSO do Microsoft Azure AD num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a788e-119">hello objective of this tutorial is tooenable you tootest Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="a788e-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="a788e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a788e-121">Adicionar Bynder da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a788e-121">Adding Bynder from hello gallery</span></span>
2. <span data-ttu-id="a788e-122">Configurar e testar o SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="a788e-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-hello-gallery"></a><span data-ttu-id="a788e-123">Adicionar Bynder da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a788e-123">Add Bynder from hello gallery</span></span>
<span data-ttu-id="a788e-124">tooconfigure Olá integração de Bynder com o Azure AD, é necessário tooadd Bynder Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="a788e-124">tooconfigure hello integration of Bynder into Azure AD, you need tooadd Bynder from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a788e-125">**tooadd Bynder da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a788e-125">**tooadd Bynder from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a788e-126">No Olá **Portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a788e-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="a788e-128">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="a788e-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a788e-129">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="a788e-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicações][2]
4. <span data-ttu-id="a788e-131">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="a788e-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicações][3]
5. <span data-ttu-id="a788e-133">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="a788e-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicações][4]
6. <span data-ttu-id="a788e-135">Na caixa de pesquisa de Olá, escreva **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="a788e-135">In hello search box, type **Bynder**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="a788e-137">No painel de resultados de Olá, selecione **Bynder**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="a788e-137">In hello results panel, select **Bynder**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Selecionar aplicação Olá na Galeria de Olá](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="a788e-139">Configurar e testar o SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="a788e-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="a788e-140">o objetivo desta secção Olá é tooshow que como tooconfigure e teste do Microsoft Azure AD SSO com Bynder com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a788e-140">hello objective of this section is tooshow you how tooconfigure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a788e-141">Para SSO toowork, do Azure AD tem tooknow é o utilizador de homólogo Olá Bynder tooan utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a788e-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Bynder tooan user in Azure AD is.</span></span> <span data-ttu-id="a788e-142">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Bynder tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a788e-142">In other words, a link relationship between an Azure AD user and hello related user in Bynder needs toobe established.</span></span>

<span data-ttu-id="a788e-143">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Bynder.</span><span class="sxs-lookup"><span data-stu-id="a788e-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bynder.</span></span>

<span data-ttu-id="a788e-144">tooconfigure e teste do Microsoft Azure AD SSO com Bynder, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a788e-144">tooconfigure and test Microsoft Azure AD SSO with Bynder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a788e-145">**[Configurar o Microsoft Azure AD-início de sessão único](#configuring-azure-ad-single-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a788e-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a788e-146">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a788e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="a788e-147">**[Criar um utilizador de teste Bynder](#creating-a-bynder-test-user)**  -toohave um homólogo de Britta Simon no Bynder é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a788e-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - toohave a counterpart of Britta Simon in Bynder that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a788e-148">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a788e-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="a788e-149">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="a788e-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="a788e-150">Configurar o SSO do Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="a788e-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="a788e-151">Nesta secção, ativar o SSO do Microsoft Azure AD no portal clássico Olá e configurar o SSO na sua aplicação Bynder.</span><span class="sxs-lookup"><span data-stu-id="a788e-151">In this section, you enable Microsoft Azure AD SSO in hello classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="a788e-152">**tooconfigure Microsoft Azure AD SSO com Bynder, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a788e-152">**tooconfigure Microsoft Azure AD SSO with Bynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="a788e-153">No portal clássico Olá, no Olá **Bynder** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar Single Sign-On** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a788e-153">In hello classic portal, on hello **Bynder** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar o início de sessão único][6] 
2. <span data-ttu-id="a788e-155">No Olá **como seria, como os utilizadores toosign no tooBynder** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a788e-155">On hello **How would you like users toosign on tooBynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="a788e-157">No Olá **configurar definições de aplicação** página da caixa de diálogo, se desejar aplicação Olá tooconfigure **IDP iniciada modo**, efetuar Olá os passos seguintes e clique em **seguinte**:</span><span class="sxs-lookup"><span data-stu-id="a788e-157">On hello **Configure App Settings** dialog page, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps and click **Next**:</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="a788e-159">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="a788e-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="a788e-160">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a788e-160">Click **Next**.</span></span>
4. <span data-ttu-id="a788e-161">Se desejar aplicação Olá tooconfigure **SP iniciada modo** no Olá **configurar definições de aplicação** página da caixa de diálogo, em seguida, clique em Olá **"(opcionais) definições avançada Show"**e, em seguida, introduza Olá **URL de início de sessão** e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a788e-161">If you wish tooconfigure hello application in **SP initiated mode** on hello **Configure App Settings** dialog page, then click on hello **“Show advanced settings (optional)”** and then enter hello **Sign On URL** and click **Next**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="a788e-163">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="a788e-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="a788e-164">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a788e-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="a788e-165">valor de Olá para Olá URL de início de sessão neste tutorial é apenas um placeholfer.</span><span class="sxs-lookup"><span data-stu-id="a788e-165">hello value for hello Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="a788e-166">tooget Olá vlaue real para o seu ambiente, contacte Bynder.</span><span class="sxs-lookup"><span data-stu-id="a788e-166">tooget hello actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="a788e-167">No Olá **configurar o início de sessão único em Bynder** página, execute os seguintes passos de Olá e clique em **seguinte**:</span><span class="sxs-lookup"><span data-stu-id="a788e-167">On hello **Configure single sign-on at Bynder** page, perform hello following steps and click **Next**:</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="a788e-169">Clique em **transferir metadados**e, em seguida, guarde o ficheiro de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a788e-169">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="a788e-170">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a788e-170">Click **Next**.</span></span>
6. <span data-ttu-id="a788e-171">tooget SSO configurado para a sua aplicação, contacte a equipa de suporte de Bynder.</span><span class="sxs-lookup"><span data-stu-id="a788e-171">tooget SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="a788e-172">Anexar o ficheiro de metadados transferido Olá e partilhá-las com Bynder equipa tooset segurança SSO no seu lado.</span><span class="sxs-lookup"><span data-stu-id="a788e-172">Attach hello downloaded metadata file and share it with Bynder team tooset up SSO on their side.</span></span>
7. <span data-ttu-id="a788e-173">No portal clássico Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a788e-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD início de sessão único][10]
8. <span data-ttu-id="a788e-175">No Olá **único início de sessão confirmação** página, clique em **concluída**.</span><span class="sxs-lookup"><span data-stu-id="a788e-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD início de sessão único][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a788e-177">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a788e-177">Create an Azure AD test user</span></span>
<span data-ttu-id="a788e-178">o objetivo desta secção Olá é toocreate um utilizador de teste no portal clássico Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a788e-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][20]

<span data-ttu-id="a788e-180">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a788e-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a788e-181">No Olá **Portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a788e-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="a788e-183">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="a788e-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a788e-184">lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a788e-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="a788e-186">Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="a788e-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="a788e-188">No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a788e-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="a788e-190">Como tipo de utilizador, selecione o novo utilizador na sua organização.</span><span class="sxs-lookup"><span data-stu-id="a788e-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="a788e-191">No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a788e-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="a788e-192">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a788e-192">Click **Next**.</span></span>
6. <span data-ttu-id="a788e-193">No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a788e-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="a788e-195">No Olá **nome próprio** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a788e-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="a788e-196">No Olá **Apelido** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a788e-196">In hello **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="a788e-197">No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a788e-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="a788e-198">No Olá **função** lista, selecione **utilizador**.</span><span class="sxs-lookup"><span data-stu-id="a788e-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="a788e-199">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a788e-199">Click **Next**.</span></span>
7. <span data-ttu-id="a788e-200">No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a788e-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="a788e-202">No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a788e-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="a788e-204">Anote o valor Olá Olá **nova palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="a788e-204">Write down hello value of hello **New Password**.</span></span>
   2. <span data-ttu-id="a788e-205">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="a788e-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="a788e-206">Criar um utilizador de teste Bynder</span><span class="sxs-lookup"><span data-stu-id="a788e-206">Create a Bynder test user</span></span>
<span data-ttu-id="a788e-207">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Bynder.</span><span class="sxs-lookup"><span data-stu-id="a788e-207">hello objective of this section is toocreate a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="a788e-208">Bynder suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.</span><span class="sxs-lookup"><span data-stu-id="a788e-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a788e-209">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="a788e-209">There is no action item for you in this section.</span></span> <span data-ttu-id="a788e-210">Será criado um novo utilizador durante uma tentativa tooaccess Bynder se não existir ainda.</span><span class="sxs-lookup"><span data-stu-id="a788e-210">A new user will be created during an attempt tooaccess Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a788e-211">Se precisar de um utilizador de toocreate manualmente, terá de equipa de suporte do toocontact Olá Bynder.</span><span class="sxs-lookup"><span data-stu-id="a788e-211">If you need toocreate an user manually, you need toocontact hello Bynder support team.</span></span> 
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="a788e-212">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a788e-212">Assign hello Azure AD test user</span></span>
<span data-ttu-id="a788e-213">objetivo Olá desta secção é tooenabling Britta Simon toouse SSO do Azure, concedendo utras tooBynder de acesso.</span><span class="sxs-lookup"><span data-stu-id="a788e-213">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooBynder.</span></span>

   ![Atribua o utilizador][200]

<span data-ttu-id="a788e-215">**tooassign Britta Simon tooBynder, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a788e-215">**tooassign Britta Simon tooBynder, perform hello following steps:**</span></span>

1. <span data-ttu-id="a788e-216">No portal clássico Olá, clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="a788e-216">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribua o utilizador][201]
2. <span data-ttu-id="a788e-218">Na lista de aplicações de Olá, selecione **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="a788e-218">In hello applications list, select **Bynder**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="a788e-220">No menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a788e-220">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribua o utilizador][203]
4. <span data-ttu-id="a788e-222">Na lista de utilizadores Olá, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a788e-222">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="a788e-223">Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="a788e-223">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribua o utilizador][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="a788e-225">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a788e-225">Test single sign-on</span></span>
<span data-ttu-id="a788e-226">o objetivo desta secção Olá é tootest a configuração do Microsoft Azure AD SSO através de Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a788e-226">hello objective of this section is tootest your Microsoft Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a788e-227">Ao clicar em mosaico de Bynder Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Bynder aplicação.</span><span class="sxs-lookup"><span data-stu-id="a788e-227">When you click hello Bynder tile in hello Access Panel, you should get automatically signed-on tooyour Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a788e-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a788e-228">Additional resources</span></span>
* [<span data-ttu-id="a788e-229">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a788e-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a788e-230">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a788e-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
