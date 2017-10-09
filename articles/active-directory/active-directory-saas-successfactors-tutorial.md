---
title: "Tutorial: Integração do Azure Active Directory com SuccessFactors | Microsoft Docs"
description: "Saiba como toouse SuccessFactors com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="bdc4f-103">Tutorial: Integração do Azure Active Directory com SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="bdc4f-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="bdc4f-104">o objetivo deste tutorial Olá é tooshow como toointegrate SuccessFactors com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdc4f-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdc4f-105">Integrar SuccessFactors com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="bdc4f-106">Pode controlar no Azure AD que tenha acesso tooSuccessFactors</span><span class="sxs-lookup"><span data-stu-id="bdc4f-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="bdc4f-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSuccessFactors (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdc4f-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="bdc4f-108">Pode gerir as contas numa localização central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="bdc4f-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="bdc4f-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdc4f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdc4f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bdc4f-110">Prerequisites</span></span>
<span data-ttu-id="bdc4f-111">integração do Azure AD com SuccessFactors tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="bdc4f-112">Uma subscrição do Azure válida</span><span class="sxs-lookup"><span data-stu-id="bdc4f-112">A valid Azure subscription</span></span>
* <span data-ttu-id="bdc4f-113">Um inquilino na SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="bdc4f-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="bdc4f-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="bdc4f-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="bdc4f-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="bdc4f-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdc4f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdc4f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="bdc4f-118">Scenario description</span></span>
<span data-ttu-id="bdc4f-119">o objetivo deste tutorial Olá é tooenable tootest do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="bdc4f-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdc4f-121">Adicionar SuccessFactors da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="bdc4f-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="bdc4f-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="bdc4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="bdc4f-123">Adicionar SuccessFactors da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="bdc4f-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="bdc4f-124">tooconfigure Olá integração de SuccessFactors com o Azure AD, é necessário tooadd SuccessFactors Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bdc4f-125">**tooadd SuccessFactors da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bdc4f-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc4f-126">No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Configurar o início de sessão único][1]
2. <span data-ttu-id="bdc4f-128">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="bdc4f-129">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Configurar o início de sessão único][2]
4. <span data-ttu-id="bdc4f-131">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicações][3]
5. <span data-ttu-id="bdc4f-133">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Configurar o início de sessão único][4]
6. <span data-ttu-id="bdc4f-135">No Olá **caixa pesquisa**, tipo **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Configurar o início de sessão único][5]
7. <span data-ttu-id="bdc4f-137">No painel de resultados de Olá, selecione **SuccessFactors**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Configurar o início de sessão único][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdc4f-139">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="bdc4f-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdc4f-140">o objetivo desta secção Olá é tooshow que como tooconfigure e teste do Azure AD-início de sessão único com SuccessFactors com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bdc4f-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bdc4f-141">Para único início de sessão toowork, do Azure AD tem tooknow é o utilizador de homólogo Olá SuccessFactors tooan utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="bdc4f-142">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá SuccessFactors tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="bdc4f-143">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="bdc4f-144">tooconfigure e teste do Azure AD-início de sessão único com SuccessFactors, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bdc4f-145">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bdc4f-146">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdc4f-147">**[Criar um utilizador de teste SuccessFactors](#creating-a-successfactors-test-user)**  -toohave um homólogo de Britta Simon no SuccessFactors é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="bdc4f-148">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdc4f-149">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdc4f-150">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="bdc4f-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="bdc4f-151">Nesta secção, pode ativar do Azure AD início de sessão no portal clássico Olá e configurar o início de sessão único na sua aplicação SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="bdc4f-152">**tooconfigure do Azure AD-início de sessão único com SuccessFactors, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bdc4f-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc4f-153">No Olá portal clássico do Azure, no Olá **SuccessFactors** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Configurar o início de sessão único][7]
2. <span data-ttu-id="bdc4f-155">No Olá **como seria, como os utilizadores toosign no tooSuccessFactors** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configurar o início de sessão único][8]
3. <span data-ttu-id="bdc4f-157">No Olá **URL da aplicação configurar** página, execute os seguintes passos de Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Configurar o início de sessão único][9]
   
    <span data-ttu-id="bdc4f-159">a.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-159">a.</span></span> <span data-ttu-id="bdc4f-160">No Olá **URL de início de sessão** caixa de texto, escreva um URL utilizando um dos seguintes padrões de Olá:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="bdc4f-161">b.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-161">b.</span></span> <span data-ttu-id="bdc4f-162">No Olá **URL de resposta** caixa de texto, escreva um URL utilizando um dos seguintes padrões de Olá:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="bdc4f-163">c.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-163">c.</span></span> <span data-ttu-id="bdc4f-164">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="bdc4f-165">Tenha em atenção que estes não são valores reais Olá.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="bdc4f-166">Tiver tooupdate estes valores com Olá real URL de início de sessão e de resposta do URL.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="bdc4f-167">Contacte o tooget estes valores, [SuccessFactors suporta equipa](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="bdc4f-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="bdc4f-168">No Olá **configurar o início de sessão único em SuccessFactors** página, clique em **Transferir certificado**e, em seguida, guarde o ficheiro de certificado Olá localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configurar o início de sessão único][10]

2. <span data-ttu-id="bdc4f-170">Numa janela do browser web diferente, inicie sessão no seu **portal de administração de SuccessFactors** como administrador.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="bdc4f-171">Visite **segurança da aplicação** e nativo demasiado**início de sessão único na funcionalidade**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="bdc4f-172">Colocar qualquer valor Olá **repor Token** e clique em **guardar Token** tooenable SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Configurar o início de sessão único no lado de aplicação][11]

    > [!NOTE] 
    > <span data-ttu-id="bdc4f-174">Este valor é utilizado apenas como Olá/desative comutador.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="bdc4f-175">Se qualquer valor for guardado, Olá SAML SSO está ON.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="bdc4f-176">Se um valor em branco é guardado Olá SAML SSO está OFF.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="bdc4f-177">Captura de ecrã toobelow nativo e efetuar Olá ações a seguir.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Configurar o início de sessão único no lado de aplicação][12]
   
    <span data-ttu-id="bdc4f-179">a.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-179">a.</span></span> <span data-ttu-id="bdc4f-180">Selecione Olá **SAML v2 SSO** botão de opção</span><span class="sxs-lookup"><span data-stu-id="bdc4f-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="bdc4f-181">b.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-181">b.</span></span> <span data-ttu-id="bdc4f-182">Defina Olá SAML Asserting terceiros Name(e.g. SAml issuer + company name).</span><span class="sxs-lookup"><span data-stu-id="bdc4f-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="bdc4f-183">c.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-183">c.</span></span> <span data-ttu-id="bdc4f-184">No Olá **SAML emissor** caixa de texto colocados valor Olá **URL do emissor** do Assistente de configuração de aplicações do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="bdc4f-185">d.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-185">d.</span></span> <span data-ttu-id="bdc4f-186">Selecione **resposta (cliente gerado/IdP/AP)** como **exigir assinatura obrigatória**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="bdc4f-187">e.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-187">e.</span></span> <span data-ttu-id="bdc4f-188">Selecione **ativada** como **ativar SAML sinalizador**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="bdc4f-189">f.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-189">f.</span></span> <span data-ttu-id="bdc4f-190">Selecione **não** como **assinatura do pedido de início de sessão (SF gerado/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="bdc4f-191">g.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-191">g.</span></span> <span data-ttu-id="bdc4f-192">Selecione **Browser/Post perfil** como **perfil SAML**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="bdc4f-193">h.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-193">h.</span></span> <span data-ttu-id="bdc4f-194">Selecione **não** como **impor período válido de certificado**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="bdc4f-195">posso.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-195">i.</span></span> <span data-ttu-id="bdc4f-196">Copie Olá conteúdo do ficheiro de certificado transferido Olá e, em seguida, cole-o Olá **SAML verificar certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bdc4f-197">conteúdo de certificado Olá tem de ter começar etiquetas de certificado do certificado e de fim.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="bdc4f-198">Navegue tooSAML V2 e, em seguida, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Configurar o início de sessão único no lado de aplicação][13]
   
    <span data-ttu-id="bdc4f-200">a.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-200">a.</span></span> <span data-ttu-id="bdc4f-201">Selecione **Sim** como **suporta iniciado por SP Global terminar**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="bdc4f-202">b.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-202">b.</span></span> <span data-ttu-id="bdc4f-203">No Olá **Global URL do serviço fim de sessão (LogoutRequest destino)** caixa de texto colocados valor Olá **URL de fim de sessão remoto** do Assistente de configuração de aplicações do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="bdc4f-204">c.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-204">c.</span></span> <span data-ttu-id="bdc4f-205">Selecione **não** como **requerem sp tem de encriptar todos os NameID elemento**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="bdc4f-206">d.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-206">d.</span></span> <span data-ttu-id="bdc4f-207">Selecione **não especificado** como **NameID formato**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="bdc4f-208">e.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-208">e.</span></span> <span data-ttu-id="bdc4f-209">Selecione **Sim** como **ativar SP2 iniciada pelo início de sessão (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="bdc4f-210">f.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-210">f.</span></span> <span data-ttu-id="bdc4f-211">No Olá **pedido de envio como emissor de toda a empresa** caixa de texto colocados valor Olá **URL de início de sessão remoto** do Assistente de configuração de aplicações do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="bdc4f-212">Execute estes passos, se pretender que os nomes de utilizador de início de sessão de Olá de toomake sensível,.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="bdc4f-213">a.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-213">a.</span></span> <span data-ttu-id="bdc4f-214">Visite **definições da empresa**(perto do fim Olá).</span><span class="sxs-lookup"><span data-stu-id="bdc4f-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="bdc4f-215">b.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-215">b.</span></span> <span data-ttu-id="bdc4f-216">Selecione a caixa de verificação junto **ativar o nome de utilizador de caso de não-sensíveis**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="bdc4f-217">c.Click **guardar**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-217">c.Click **Save**.</span></span>
   
    ![Configurar o início de sessão único][29]

    > [!NOTE] 
    > <span data-ttu-id="bdc4f-219">Se tentar tooenable isto, o sistema Olá verifica se criará um nome de início de sessão SAML duplicado.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="bdc4f-220">Por exemplo, se o cliente de Olá tem nomes de utilizador User1 e user1.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="bdc4f-221">Colocar ausente sensibilidade às maiúsculas e minúsculas torna estas duplicados.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="bdc4f-222">sistema de Olá irá dar-lhe uma mensagem de erro e não irá ativar a funcionalidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="bdc4f-223">Olá cliente terá de toochange um dos nomes de utilizador Olá pelo que, na verdade, está a ser escrito diferentes.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="bdc4f-224">No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída** tooclose Olá **configurar início de sessão único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Aplicações][14]
2. <span data-ttu-id="bdc4f-226">No Olá **único início de sessão confirmação** página, clique em **concluída**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Aplicações][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdc4f-228">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdc4f-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdc4f-229">o objetivo desta secção Olá é toocreate um utilizador de teste no portal clássico Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][16]

<span data-ttu-id="bdc4f-231">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bdc4f-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc4f-232">No Olá **Portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD][17]
2. <span data-ttu-id="bdc4f-234">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="bdc4f-235">lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD][18]
4. <span data-ttu-id="bdc4f-237">Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD][19]
5. <span data-ttu-id="bdc4f-239">No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criar um utilizador de teste do Azure AD][20]
   
    <span data-ttu-id="bdc4f-241">a.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-241">a.</span></span> <span data-ttu-id="bdc4f-242">Como tipo de utilizador, selecione o novo utilizador na sua organização.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="bdc4f-243">b.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-243">b.</span></span> <span data-ttu-id="bdc4f-244">No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="bdc4f-245">c.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-245">c.</span></span> <span data-ttu-id="bdc4f-246">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-246">Click **Next**.</span></span>
6. <span data-ttu-id="bdc4f-247">No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Criar um utilizador de teste do Azure AD][21]
   
    <span data-ttu-id="bdc4f-249">a.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-249">a.</span></span> <span data-ttu-id="bdc4f-250">No Olá **nome próprio** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="bdc4f-251">b.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-251">b.</span></span> <span data-ttu-id="bdc4f-252">No Olá **Apelido** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="bdc4f-253">c.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-253">c.</span></span> <span data-ttu-id="bdc4f-254">No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="bdc4f-255">d.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-255">d.</span></span> <span data-ttu-id="bdc4f-256">No Olá **função** lista, selecione **utilizador**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="bdc4f-257">e.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-257">e.</span></span> <span data-ttu-id="bdc4f-258">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-258">Click **Next**.</span></span>
7. <span data-ttu-id="bdc4f-259">No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criar um utilizador de teste do Azure AD][22]
8. <span data-ttu-id="bdc4f-261">No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="bdc4f-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criar um utilizador de teste do Azure AD][23]
   
    <span data-ttu-id="bdc4f-263">a.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-263">a.</span></span> <span data-ttu-id="bdc4f-264">Anote o valor Olá Olá **nova palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="bdc4f-265">b.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-265">b.</span></span> <span data-ttu-id="bdc4f-266">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="bdc4f-267">Criar um utilizador de teste SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="bdc4f-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="bdc4f-268">Na ordem tooenable do Azure AD os utilizadores toolog para SuccessFactors, têm de ser aprovisionados para SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="bdc4f-269">No caso de Olá da SuccessFactors, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="bdc4f-270">utilizadores de tooget criados no SuccessFactors, terá de toocontact Olá [SuccessFactors suporta equipa](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="bdc4f-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bdc4f-271">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdc4f-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="bdc4f-272">objetivo Olá desta secção é tooenabling Britta Simon toouse do Azure-início de sessão único, concedendo utras tooSuccessFactors de acesso.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Atribua o utilizador][24]

<span data-ttu-id="bdc4f-274">**tooassign Britta Simon tooSuccessFactors, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="bdc4f-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdc4f-275">No portal clássico Olá, clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Atribua o utilizador][25]
2. <span data-ttu-id="bdc4f-277">Na lista de aplicações de Olá, selecione **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Configurar o início de sessão único][26]
3. <span data-ttu-id="bdc4f-279">No menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Atribua o utilizador][27]
4. <span data-ttu-id="bdc4f-281">Na lista de utilizadores Olá, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="bdc4f-282">Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Atribua o utilizador][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="bdc4f-284">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="bdc4f-284">Testing single sign-on</span></span>
<span data-ttu-id="bdc4f-285">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bdc4f-286">Ao clicar Olá SuccessFactors na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour SuccessFactors aplicação.</span><span class="sxs-lookup"><span data-stu-id="bdc4f-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bdc4f-287">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="bdc4f-287">Additional resources</span></span>
* [<span data-ttu-id="bdc4f-288">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdc4f-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdc4f-289">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bdc4f-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
