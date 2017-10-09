---
title: "Tutorial: Integração do Azure Active Directory com Nexonia | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 3778804084a7989414260bae5654cf76e9ccca6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="30f53-103">Tutorial: Integração do Azure Active Directory com Nexonia</span><span class="sxs-lookup"><span data-stu-id="30f53-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="30f53-104">Neste tutorial, saiba como toointegrate Nexonia com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30f53-104">In this tutorial, you learn how toointegrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30f53-105">Integrar Nexonia com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="30f53-105">Integrating Nexonia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="30f53-106">Pode controlar no Azure AD que tenha acesso tooNexonia</span><span class="sxs-lookup"><span data-stu-id="30f53-106">You can control in Azure AD who has access tooNexonia</span></span>
- <span data-ttu-id="30f53-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooNexonia (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="30f53-107">You can enable your users tooautomatically get signed-on tooNexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30f53-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="30f53-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="30f53-109">Se pretender que tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo.</span><span class="sxs-lookup"><span data-stu-id="30f53-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="30f53-110">[O que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30f53-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30f53-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="30f53-111">Prerequisites</span></span>

<span data-ttu-id="30f53-112">integração do Azure AD com Nexonia tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="30f53-112">tooconfigure Azure AD integration with Nexonia, you need hello following items:</span></span>

- <span data-ttu-id="30f53-113">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="30f53-113">An Azure AD subscription</span></span>
- <span data-ttu-id="30f53-114">Um Nexonia início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="30f53-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30f53-115">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="30f53-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30f53-116">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="30f53-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30f53-117">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="30f53-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30f53-118">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30f53-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30f53-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="30f53-119">Scenario description</span></span>
<span data-ttu-id="30f53-120">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="30f53-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30f53-121">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="30f53-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30f53-122">Adicionar Nexonia da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="30f53-122">Adding Nexonia from hello gallery</span></span>
2. <span data-ttu-id="30f53-123">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="30f53-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-hello-gallery"></a><span data-ttu-id="30f53-124">Adicionar Nexonia da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="30f53-124">Adding Nexonia from hello gallery</span></span>
<span data-ttu-id="30f53-125">tooconfigure Olá integração de Nexonia com o Azure AD, é necessário tooadd Nexonia Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="30f53-125">tooconfigure hello integration of Nexonia into Azure AD, you need tooadd Nexonia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="30f53-126">**tooadd Nexonia da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="30f53-126">**tooadd Nexonia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="30f53-127">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="30f53-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="30f53-129">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="30f53-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="30f53-130">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="30f53-130">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="30f53-132">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="30f53-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="30f53-134">Na caixa de pesquisa de Olá, escreva **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="30f53-134">In hello search box, type **Nexonia**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="30f53-136">No painel de resultados de Olá, selecione **Nexonia**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="30f53-136">In hello results panel, select **Nexonia**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="30f53-138">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="30f53-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="30f53-139">Nesta secção, configure e teste do Azure AD-início de sessão único com Nexonia com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="30f53-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="30f53-140">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Nexonia é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30f53-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nexonia is tooa user in Azure AD.</span></span> <span data-ttu-id="30f53-141">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Nexonia tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="30f53-141">In other words, a link relationship between an Azure AD user and hello related user in Nexonia needs toobe established.</span></span>

<span data-ttu-id="30f53-142">No Nexonia, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="30f53-142">In Nexonia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="30f53-143">tooconfigure e teste do Azure AD-início de sessão único com Nexonia, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="30f53-143">tooconfigure and test Azure AD single sign-on with Nexonia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="30f53-144">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="30f53-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="30f53-145">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30f53-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30f53-146">**[Criar um utilizador de teste Nexonia](#creating-a-nexonia-test-user)**  -toohave um homólogo de Britta Simon no Nexonia é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="30f53-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - toohave a counterpart of Britta Simon in Nexonia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="30f53-147">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="30f53-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30f53-148">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="30f53-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="30f53-149">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="30f53-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="30f53-150">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Nexonia.</span><span class="sxs-lookup"><span data-stu-id="30f53-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="30f53-151">Se tiver problemas na integração Olá, consulte este [ligação](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) para guia de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="30f53-151">If you have issues in hello integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="30f53-152">Se ainda não ter encontrado solução Olá, em seguida, emitir um pedido de suporte de Olá a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="30f53-152">If you still have not found hello solution, then raise hello support request from Azure portal.</span></span>

<span data-ttu-id="30f53-153">**tooconfigure do Azure AD-início de sessão único com Nexonia, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="30f53-153">**tooconfigure Azure AD single sign-on with Nexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="30f53-154">No Olá portal do Azure, no Olá **Nexonia** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="30f53-154">In hello Azure portal, on hello **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="30f53-156">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="30f53-156">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="30f53-158">No Olá **Nexonia domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="30f53-158">On hello **Nexonia Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="30f53-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="30f53-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="30f53-161">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="30f53-161">This value is not real.</span></span> <span data-ttu-id="30f53-162">Atualize este valor com o URL de resposta real Olá.</span><span class="sxs-lookup"><span data-stu-id="30f53-162">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="30f53-163">Contacte [equipa de suporte de Nexonia](https://nexonia.zendesk.com/hc/requests/new) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="30f53-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooget this value.</span></span> 


4. <span data-ttu-id="30f53-164">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="30f53-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="30f53-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="30f53-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="30f53-168">No Olá **Nexonia configuração** secção, clique em **configurar Nexonia** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="30f53-168">On hello **Nexonia Configuration** section, click **Configure Nexonia** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="30f53-169">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="30f53-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="30f53-171">tooget SSO configuradas para a sua aplicação, contacte [equipa de suporte de Nexonia](https://nexonia.zendesk.com/hc/requests/new) e forneça-los com o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="30f53-171">tooget SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with hello following:</span></span>

    <span data-ttu-id="30f53-172">Olá • transferido **certificado**</span><span class="sxs-lookup"><span data-stu-id="30f53-172">• hello downloaded **certificate**</span></span>

    <span data-ttu-id="30f53-173">• Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="30f53-173">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="30f53-174">• Olá **único início de sessão no URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="30f53-174">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="30f53-175">• Olá **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="30f53-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="30f53-176">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="30f53-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="30f53-177">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="30f53-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="30f53-178">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="30f53-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="30f53-179">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="30f53-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="30f53-180">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="30f53-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="30f53-182">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="30f53-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="30f53-183">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="30f53-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="30f53-185">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="30f53-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30f53-187">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="30f53-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30f53-189">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="30f53-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30f53-191">a.</span><span class="sxs-lookup"><span data-stu-id="30f53-191">a.</span></span> <span data-ttu-id="30f53-192">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30f53-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30f53-193">b.</span><span class="sxs-lookup"><span data-stu-id="30f53-193">b.</span></span> <span data-ttu-id="30f53-194">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="30f53-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30f53-195">c.</span><span class="sxs-lookup"><span data-stu-id="30f53-195">c.</span></span> <span data-ttu-id="30f53-196">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="30f53-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="30f53-197">d.</span><span class="sxs-lookup"><span data-stu-id="30f53-197">d.</span></span> <span data-ttu-id="30f53-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="30f53-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="30f53-199">Criar um utilizador de teste Nexonia</span><span class="sxs-lookup"><span data-stu-id="30f53-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="30f53-200">Nesta secção, vai criar um utilizador chamado Britta Simon Nexonia.</span><span class="sxs-lookup"><span data-stu-id="30f53-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="30f53-201">Trabalhar com [equipa de suporte de Nexonia](https://nexonia.zendesk.com/hc/requests/new) utilizadores de Olá tooadd na plataforma de Nexonia Olá.</span><span class="sxs-lookup"><span data-stu-id="30f53-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooadd hello users in hello Nexonia platform.</span></span> <span data-ttu-id="30f53-202">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="30f53-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="30f53-203">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="30f53-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="30f53-204">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooNexonia.</span><span class="sxs-lookup"><span data-stu-id="30f53-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNexonia.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="30f53-206">**tooassign Britta Simon tooNexonia, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="30f53-206">**tooassign Britta Simon tooNexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="30f53-207">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="30f53-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="30f53-209">Na lista de aplicações de Olá, selecione **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="30f53-209">In hello applications list, select **Nexonia**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="30f53-211">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="30f53-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="30f53-213">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="30f53-213">Click **Add** button.</span></span> <span data-ttu-id="30f53-214">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="30f53-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="30f53-216">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="30f53-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="30f53-217">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="30f53-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30f53-218">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="30f53-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="30f53-219">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="30f53-219">Testing single sign-on</span></span>

<span data-ttu-id="30f53-220">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="30f53-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="30f53-221">Ao clicar em mosaico de Nexonia Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Nexonia aplicação.</span><span class="sxs-lookup"><span data-stu-id="30f53-221">When you click hello Nexonia tile in hello Access Panel, you should get automatically signed-on tooyour Nexonia application.</span></span>
<span data-ttu-id="30f53-222">Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="30f53-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30f53-223">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="30f53-223">Additional resources</span></span>

* [<span data-ttu-id="30f53-224">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30f53-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30f53-225">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="30f53-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

