---
title: "Tutorial: Integração do Azure Active Directory com Halosys | Microsoft Docs"
description: "Saiba como toouse Halosys com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="538ec-103">Tutorial: Integração do Azure Active Directory com Halosys</span><span class="sxs-lookup"><span data-stu-id="538ec-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="538ec-104">Neste tutorial, saiba como toointegrate Halosys com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="538ec-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="538ec-105">Integrar Halosys com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="538ec-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="538ec-106">Pode controlar no Azure AD que tenha acesso tooHalosys</span><span class="sxs-lookup"><span data-stu-id="538ec-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="538ec-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooHalosys (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="538ec-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="538ec-108">Pode gerir as contas numa localização central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="538ec-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="538ec-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="538ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="538ec-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="538ec-110">Prerequisites</span></span>

<span data-ttu-id="538ec-111">integração do Azure AD com Halosys tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="538ec-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="538ec-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="538ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="538ec-113">Um Halosys início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="538ec-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="538ec-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="538ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="538ec-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="538ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="538ec-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="538ec-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="538ec-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="538ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="538ec-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="538ec-118">Scenario description</span></span>
<span data-ttu-id="538ec-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="538ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="538ec-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="538ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="538ec-121">Adicionar Halosys da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="538ec-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="538ec-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="538ec-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="538ec-123">Adicionar Halosys da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="538ec-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="538ec-124">tooconfigure Olá integração de Halosys com o Azure AD, é necessário tooadd Halosys Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="538ec-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="538ec-125">**tooadd Halosys da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="538ec-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="538ec-126">No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="538ec-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="538ec-128">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="538ec-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="538ec-129">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="538ec-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Aplicações][2]

4. <span data-ttu-id="538ec-131">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="538ec-131">Click **Add** at hello bottom of hello page.</span></span>

    ![Aplicações][3]

5. <span data-ttu-id="538ec-133">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="538ec-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![Aplicações][4]

6. <span data-ttu-id="538ec-135">Na caixa de pesquisa de Olá, escreva **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="538ec-135">In hello search box, type **Halosys**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="538ec-137">No painel de resultados de Olá, selecione **Halosys**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="538ec-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="538ec-139">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="538ec-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="538ec-140">Nesta secção, configure e teste do Azure AD-início de sessão único com Halosys com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="538ec-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="538ec-141">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Halosys é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="538ec-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="538ec-142">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Halosys tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="538ec-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="538ec-143">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Halosys.</span><span class="sxs-lookup"><span data-stu-id="538ec-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="538ec-144">tooconfigure e teste do Azure AD-início de sessão único com Halosys, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="538ec-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="538ec-145">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="538ec-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="538ec-146">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="538ec-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="538ec-147">**[Criar um utilizador de teste Halosys](#creating-a-halosys-test-user)**  -toohave um homólogo de Britta Simon no Halosys é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="538ec-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="538ec-148">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="538ec-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="538ec-149">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="538ec-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="538ec-150">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="538ec-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="538ec-151">Nesta secção, pode ativar do Azure AD início de sessão no portal clássico Olá e configurar o início de sessão único na sua aplicação Halosys.</span><span class="sxs-lookup"><span data-stu-id="538ec-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="538ec-152">**tooconfigure do Azure AD-início de sessão único com Halosys, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="538ec-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="538ec-153">No portal clássico Olá, no Olá **Halosys** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar Single Sign-On** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="538ec-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![Configurar o início de sessão único][6] 

2. <span data-ttu-id="538ec-155">No Olá **como seria, como os utilizadores toosign no tooHalosys** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="538ec-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="538ec-157">No Olá **configurar definições de aplicação** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="538ec-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="538ec-159">a.</span><span class="sxs-lookup"><span data-stu-id="538ec-159">a.</span></span> <span data-ttu-id="538ec-160">No Olá **URL de início de sessão** caixa de texto, tipo Olá URL utilizado por utilizadores em toosign tooyour Halosys aplicação Olá seguir o padrão de utilização: `https://<company-name>.Halosys.com/client-api/api`.</span><span class="sxs-lookup"><span data-stu-id="538ec-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="538ec-161">Olá b.In **URL de identificador** caixa de texto, tipo Olá URL no Olá seguir o padrão: `https://<company-name>.Halosys.com`.</span><span class="sxs-lookup"><span data-stu-id="538ec-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="538ec-162">No Olá **configurar o início de sessão único em Halosys** página, clique em **transferir metadados**e, em seguida, guarde o ficheiro de Olá no seu computador:</span><span class="sxs-lookup"><span data-stu-id="538ec-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="538ec-164">tooget SSO configurado para a sua aplicação, contacte a equipa de suporte de Halosys e forneça-los com o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="538ec-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="538ec-165">Olá • transferido **ficheiro de metadados**</span><span class="sxs-lookup"><span data-stu-id="538ec-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="538ec-166">• Olá **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="538ec-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="538ec-167">No portal clássico Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="538ec-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD início de sessão único][10]

7. <span data-ttu-id="538ec-169">No Olá **único início de sessão confirmação** página, clique em **concluída**.</span><span class="sxs-lookup"><span data-stu-id="538ec-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD início de sessão único][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="538ec-171">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="538ec-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="538ec-172">Nesta secção, vai criar um utilizador de teste no portal clássico Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="538ec-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![Criar utilizador do Azure AD][20]

<span data-ttu-id="538ec-174">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="538ec-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="538ec-175">No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="538ec-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="538ec-177">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="538ec-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="538ec-178">lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="538ec-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="538ec-180">Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="538ec-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="538ec-182">No Olá **diga-nos informações sobre este utilizador** diálogo página, execute os seguintes passos de Olá: ![criação de um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="538ec-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="538ec-183">a.</span><span class="sxs-lookup"><span data-stu-id="538ec-183">a.</span></span> <span data-ttu-id="538ec-184">Como tipo de utilizador, selecione o novo utilizador na sua organização.</span><span class="sxs-lookup"><span data-stu-id="538ec-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="538ec-185">b.</span><span class="sxs-lookup"><span data-stu-id="538ec-185">b.</span></span> <span data-ttu-id="538ec-186">No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="538ec-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="538ec-187">c.</span><span class="sxs-lookup"><span data-stu-id="538ec-187">c.</span></span> <span data-ttu-id="538ec-188">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="538ec-188">Click **Next**.</span></span>

6.  <span data-ttu-id="538ec-189">No Olá **perfil de utilizador** diálogo página, execute os seguintes passos de Olá: ![criação de um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="538ec-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="538ec-190">a.</span><span class="sxs-lookup"><span data-stu-id="538ec-190">a.</span></span> <span data-ttu-id="538ec-191">No Olá **nome próprio** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="538ec-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="538ec-192">b.</span><span class="sxs-lookup"><span data-stu-id="538ec-192">b.</span></span> <span data-ttu-id="538ec-193">No Olá **Apelido** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="538ec-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="538ec-194">c.</span><span class="sxs-lookup"><span data-stu-id="538ec-194">c.</span></span> <span data-ttu-id="538ec-195">No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="538ec-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="538ec-196">d.</span><span class="sxs-lookup"><span data-stu-id="538ec-196">d.</span></span> <span data-ttu-id="538ec-197">No Olá **função** lista, selecione **utilizador**.</span><span class="sxs-lookup"><span data-stu-id="538ec-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="538ec-198">e.</span><span class="sxs-lookup"><span data-stu-id="538ec-198">e.</span></span> <span data-ttu-id="538ec-199">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="538ec-199">Click **Next**.</span></span>

7. <span data-ttu-id="538ec-200">No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="538ec-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="538ec-202">No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="538ec-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="538ec-204">a.</span><span class="sxs-lookup"><span data-stu-id="538ec-204">a.</span></span> <span data-ttu-id="538ec-205">Anote o valor Olá Olá **nova palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="538ec-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="538ec-206">b.</span><span class="sxs-lookup"><span data-stu-id="538ec-206">b.</span></span> <span data-ttu-id="538ec-207">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="538ec-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="538ec-208">Criar um utilizador de teste Halosys</span><span class="sxs-lookup"><span data-stu-id="538ec-208">Creating a Halosys test user</span></span>

<span data-ttu-id="538ec-209">Nesta secção, vai criar um utilizador chamado Britta Simon Halosys.</span><span class="sxs-lookup"><span data-stu-id="538ec-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="538ec-210">. Funciona com Halosys suporte equipa tooadd Olá utilizadores numa plataforma de Halosys Olá.</span><span class="sxs-lookup"><span data-stu-id="538ec-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="538ec-211">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="538ec-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="538ec-212">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooHalosys de acesso.</span><span class="sxs-lookup"><span data-stu-id="538ec-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="538ec-214">**tooassign Britta Simon tooHalosys, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="538ec-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="538ec-215">No portal clássico Olá, clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="538ec-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="538ec-217">Na lista de aplicações de Olá, selecione **Halosys**.</span><span class="sxs-lookup"><span data-stu-id="538ec-217">In hello applications list, select **Halosys**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="538ec-219">No menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="538ec-219">In hello menu on hello top, click **Users**.</span></span>

    ![Atribua o utilizador][203]

4. <span data-ttu-id="538ec-221">Na lista de utilizadores Olá, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="538ec-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="538ec-222">Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="538ec-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![Atribua o utilizador][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="538ec-224">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="538ec-224">Testing single sign-on</span></span>

<span data-ttu-id="538ec-225">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="538ec-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="538ec-226">Ao clicar Olá Halosys na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour Halosys aplicação.</span><span class="sxs-lookup"><span data-stu-id="538ec-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="538ec-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="538ec-227">Additional resources</span></span>

* [<span data-ttu-id="538ec-228">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="538ec-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="538ec-229">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="538ec-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
