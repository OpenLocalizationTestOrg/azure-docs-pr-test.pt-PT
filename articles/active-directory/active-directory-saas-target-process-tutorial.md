---
title: "Tutorial: Integração do Azure Active Directory com TargetProcess | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="7b5f8-103">Tutorial: Integração do Azure Active Directory com TargetProcess</span><span class="sxs-lookup"><span data-stu-id="7b5f8-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="7b5f8-104">Neste tutorial, saiba como toointegrate TargetProcess com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b5f8-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b5f8-105">Integrar TargetProcess com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="7b5f8-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b5f8-106">Pode controlar no Azure AD que tenha acesso tooTargetProcess</span><span class="sxs-lookup"><span data-stu-id="7b5f8-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="7b5f8-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooTargetProcess (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b5f8-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b5f8-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7b5f8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7b5f8-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b5f8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b5f8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7b5f8-110">Prerequisites</span></span>

<span data-ttu-id="7b5f8-111">integração do Azure AD com TargetProcess tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7b5f8-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="7b5f8-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b5f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b5f8-113">Um TargetProcess-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="7b5f8-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b5f8-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b5f8-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7b5f8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b5f8-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b5f8-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b5f8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b5f8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7b5f8-118">Scenario description</span></span>
<span data-ttu-id="7b5f8-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b5f8-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="7b5f8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b5f8-121">Adicionar TargetProcess da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="7b5f8-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="7b5f8-122">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7b5f8-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="7b5f8-123">Adicionar TargetProcess da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="7b5f8-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="7b5f8-124">tooconfigure Olá integração de TargetProcess com o Azure AD, é necessário tooadd TargetProcess Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b5f8-125">**tooadd TargetProcess da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7b5f8-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b5f8-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b5f8-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b5f8-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="7b5f8-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="7b5f8-133">Na caixa de pesquisa de Olá, escreva **TargetProcess**, selecione **TargetProcess** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Adicionar TargetProcess da Galeria](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7b5f8-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7b5f8-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7b5f8-136">Nesta secção, configure e teste do Azure AD-início de sessão único com TargetProcess com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7b5f8-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b5f8-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá TargetProcess é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="7b5f8-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá TargetProcess tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="7b5f8-139">No TargetProcess, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b5f8-140">tooconfigure e teste do Azure AD-início de sessão único com TargetProcess, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7b5f8-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b5f8-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b5f8-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b5f8-143">**[Criar um utilizador de teste TargetProcess](#create-a-targetprocess-test-user)**  -toohave um homólogo de Britta Simon no TargetProcess é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b5f8-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b5f8-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7b5f8-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7b5f8-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7b5f8-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="7b5f8-148">**tooconfigure do Azure AD-início de sessão único com TargetProcess, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7b5f8-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b5f8-149">No Olá portal do Azure, no Olá **TargetProcess** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="7b5f8-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Baseados em SAML início de sessão](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="7b5f8-153">No Olá **TargetProcess domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7b5f8-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Secção TargetProcess domínio e os URLs](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="7b5f8-155">a.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-155">a.</span></span> <span data-ttu-id="7b5f8-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="7b5f8-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="7b5f8-157">b.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-157">b.</span></span> <span data-ttu-id="7b5f8-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="7b5f8-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b5f8-159">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-159">These values are not real.</span></span> <span data-ttu-id="7b5f8-160">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7b5f8-161">Contacte [equipa de suporte de cliente TargetProcess](mailto:support@targetprocess.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="7b5f8-162">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Secção de certificado de assinatura de SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="7b5f8-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-164">Click **Save** button.</span></span>

    ![botão Guardar](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b5f8-166">No Olá **TargetProcess configuração** secção, clique em **configurar TargetProcess** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7b5f8-167">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="7b5f8-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Secção de configuração de TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="7b5f8-169">Início de sessão tooyour TargetProcess aplicação como um administrador.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="7b5f8-170">No menu de Olá na parte superior do Olá, clique em **configuração**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Configurar](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="7b5f8-172">Clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-172">Click **Settings**.</span></span>
   
    ![Definições](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="7b5f8-174">Clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-174">Click **Single Sign-on**.</span></span>
   
    ![Clique em Single Sign-On](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="7b5f8-176">No Olá o início de sessão única caixa de diálogo Definições, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7b5f8-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="7b5f8-178">a.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-178">a.</span></span> <span data-ttu-id="7b5f8-179">Clique em **ativar o início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="7b5f8-180">b.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-180">b.</span></span> <span data-ttu-id="7b5f8-181">No **URL de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7b5f8-182">c.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-182">c.</span></span> <span data-ttu-id="7b5f8-183">Abra o seu certificado transferido no bloco de notas, Olá copiar conteúdo e, em seguida, cole-o Olá **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="7b5f8-184">d.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-184">d.</span></span> <span data-ttu-id="7b5f8-185">Clique em **ativar o aprovisionamento de JIT**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="7b5f8-186">e.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-186">e.</span></span> <span data-ttu-id="7b5f8-187">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7b5f8-188">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="7b5f8-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b5f8-189">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b5f8-190">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b5f8-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7b5f8-191">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b5f8-191">Create an Azure AD test user</span></span>
<span data-ttu-id="7b5f8-192">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="7b5f8-194">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7b5f8-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b5f8-195">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b5f8-197">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![lista de Olá toodisplay de utilizadores](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b5f8-199">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Botão Adicionar](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b5f8-201">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7b5f8-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Secção de utilizador](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b5f8-203">a.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-203">a.</span></span> <span data-ttu-id="7b5f8-204">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b5f8-205">b.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-205">b.</span></span> <span data-ttu-id="7b5f8-206">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b5f8-207">c.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-207">c.</span></span> <span data-ttu-id="7b5f8-208">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7b5f8-209">d.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-209">d.</span></span> <span data-ttu-id="7b5f8-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="7b5f8-211">Criar um utilizador de teste TargetProcess</span><span class="sxs-lookup"><span data-stu-id="7b5f8-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="7b5f8-212">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="7b5f8-213">TargetProcess suportam o aprovisionamento de just-in-time.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="7b5f8-214">Que já ativou-lo na [configurar do Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="7b5f8-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="7b5f8-215">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7b5f8-216">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b5f8-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7b5f8-217">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooTargetProcess.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="7b5f8-219">**tooassign Britta Simon tooTargetProcess, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7b5f8-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b5f8-220">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="7b5f8-222">Na lista de aplicações de Olá, selecione **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-222">In hello applications list, select **TargetProcess**.</span></span>

    ![TargetProcess na lista de aplicações](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="7b5f8-224">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="7b5f8-226">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-226">Click **Add** button.</span></span> <span data-ttu-id="7b5f8-227">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="7b5f8-229">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b5f8-230">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b5f8-231">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7b5f8-232">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7b5f8-232">Test single sign-on</span></span>

<span data-ttu-id="7b5f8-233">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b5f8-234">Ao clicar Olá TargetProcess na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour TargetProcess aplicação.</span><span class="sxs-lookup"><span data-stu-id="7b5f8-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="7b5f8-235">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b5f8-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b5f8-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7b5f8-236">Additional resources</span></span>

* [<span data-ttu-id="7b5f8-237">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b5f8-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b5f8-238">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b5f8-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

