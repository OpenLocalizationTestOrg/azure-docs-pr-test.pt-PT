---
title: "Tutorial: Integração do Azure Active Directory com Proofpoint a pedido | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Proofpoint a pedido."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="5967c-103">Tutorial: Integração do Azure Active Directory com Proofpoint a pedido</span><span class="sxs-lookup"><span data-stu-id="5967c-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="5967c-104">Neste tutorial, saiba como toointegrate Proofpoint a pedido com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5967c-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5967c-105">Integrar Proofpoint a pedido com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="5967c-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5967c-106">Pode controlar no Azure AD que tenha acesso tooProofpoint a pedido</span><span class="sxs-lookup"><span data-stu-id="5967c-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="5967c-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooProofpoint a pedido (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5967c-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5967c-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5967c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5967c-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5967c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5967c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5967c-110">Prerequisites</span></span>

<span data-ttu-id="5967c-111">integração de tooconfigure do Azure AD com Proofpoint a pedido, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5967c-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="5967c-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5967c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5967c-113">Um Proofpoint no pedido-início de sessão único subscrição ativada</span><span class="sxs-lookup"><span data-stu-id="5967c-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5967c-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5967c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5967c-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5967c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5967c-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5967c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5967c-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5967c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5967c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5967c-118">Scenario description</span></span>
<span data-ttu-id="5967c-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5967c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5967c-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="5967c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5967c-121">Adicionar Proofpoint a pedido a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="5967c-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="5967c-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="5967c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="5967c-123">Adicionar Proofpoint a pedido a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="5967c-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="5967c-124">tooconfigure Olá integração de Proofpoint a pedido com o Azure AD, é necessário tooadd Proofpoint a pedido a partir da lista de tooyour Olá Galeria de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="5967c-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5967c-125">**tooadd Proofpoint a pedido a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="5967c-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5967c-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="5967c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5967c-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5967c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5967c-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="5967c-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="5967c-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5967c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="5967c-133">Na caixa de pesquisa de Olá, escreva **Proofpoint a pedido**.</span><span class="sxs-lookup"><span data-stu-id="5967c-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="5967c-135">No painel de resultados de Olá, selecione **Proofpoint a pedido**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="5967c-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5967c-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="5967c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5967c-138">Nesta secção, configurar e testar o Azure AD-início de sessão único com Proofpoint a pedido com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="5967c-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5967c-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Proofpoint a pedido é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5967c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="5967c-140">Por outras palavras, uma relação entre um utilizador do Azure AD e o utilizador relacionados Olá Proofpoint a pedido de ligação tem de toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5967c-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="5967c-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Proofpoint a pedido.</span><span class="sxs-lookup"><span data-stu-id="5967c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="5967c-142">tooconfigure e teste do Azure AD de sessão único-com Proofpoint a pedido, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="5967c-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5967c-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="5967c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5967c-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5967c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5967c-145">**[Criar um Proofpoint no utilizador de teste a pedido](#creating-a-proofpoint-on-demand-test-user)**  -toohave um homólogo de Britta Simon no Proofpoint a pedido é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="5967c-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5967c-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="5967c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5967c-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="5967c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5967c-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="5967c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5967c-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua Proofpoint na aplicação a pedido.</span><span class="sxs-lookup"><span data-stu-id="5967c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="5967c-150">**tooconfigure do Azure AD-início de sessão único com Proofpoint a pedido, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="5967c-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="5967c-151">No Olá portal do Azure, no Olá **Proofpoint a pedido** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="5967c-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="5967c-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="5967c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Configurar o início de sessão único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="5967c-155">No Olá **Proofpoint no domínio a pedido e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5967c-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="5967c-157">Olá a.In **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="5967c-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="5967c-158">b.</span><span class="sxs-lookup"><span data-stu-id="5967c-158">b.</span></span> <span data-ttu-id="5967c-159">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="5967c-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="5967c-160">c.</span><span class="sxs-lookup"><span data-stu-id="5967c-160">c.</span></span>  <span data-ttu-id="5967c-161">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="5967c-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="5967c-162">Estes valores não estiverem Olá real.</span><span class="sxs-lookup"><span data-stu-id="5967c-162">These values are not hello real.</span></span> <span data-ttu-id="5967c-163">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="5967c-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="5967c-164">Contacte [Proofpoint na equipa de suporte de cliente a pedido](https://www.proofpoint.com/us/support-services) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="5967c-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="5967c-165">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="5967c-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="5967c-167">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="5967c-167">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="5967c-169">No Olá **Proofpoint na configuração de pedido** secção, clique em **configurar Proofpoint a pedido** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="5967c-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5967c-170">Olá cópia **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5967c-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="5967c-172">tooconfigure-início de sessão único em **Proofpoint a pedido** lado, terá de Olá toosend transferido **Certificate(Base64)**,**ID de entidade de SAML**, e **SAML Single Sign-On URL do serviço** demasiado[Proofpoint na equipa de suporte de cliente a pedido](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="5967c-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="5967c-173">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="5967c-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5967c-174">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="5967c-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5967c-175">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5967c-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5967c-176">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5967c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="5967c-177">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5967c-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="5967c-179">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="5967c-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5967c-180">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="5967c-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5967c-182">Estes valores não estiverem Olá real.</span><span class="sxs-lookup"><span data-stu-id="5967c-182">These values are not hello real.</span></span> <span data-ttu-id="5967c-183">Atualizar estes valores com Olá real</span><span class="sxs-lookup"><span data-stu-id="5967c-183">Update these values with hello actual</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5967c-185">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="5967c-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5967c-187">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="5967c-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5967c-189">a.</span><span class="sxs-lookup"><span data-stu-id="5967c-189">a.</span></span> <span data-ttu-id="5967c-190">No Olá **nome** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5967c-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="5967c-191">b.</span><span class="sxs-lookup"><span data-stu-id="5967c-191">b.</span></span> <span data-ttu-id="5967c-192">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5967c-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="5967c-193">c.</span><span class="sxs-lookup"><span data-stu-id="5967c-193">c.</span></span> <span data-ttu-id="5967c-194">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="5967c-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5967c-195">d.</span><span class="sxs-lookup"><span data-stu-id="5967c-195">d.</span></span> <span data-ttu-id="5967c-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5967c-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="5967c-197">Criar um Proofpoint no utilizador de teste a pedido</span><span class="sxs-lookup"><span data-stu-id="5967c-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="5967c-198">Nesta secção, vai criar um utilizador chamado Britta Simon Proofpoint a pedido.</span><span class="sxs-lookup"><span data-stu-id="5967c-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="5967c-199">Trabalhar com [Proofpoint na equipa de suporte de cliente a pedido](https://www.proofpoint.com/us/support-services) utilizadores tooadd Olá Proofpoint na plataforma a pedido.</span><span class="sxs-lookup"><span data-stu-id="5967c-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5967c-200">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5967c-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5967c-201">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooProofpoint a pedido.</span><span class="sxs-lookup"><span data-stu-id="5967c-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="5967c-203">**tooassign Britta Simon tooProofpoint a pedido, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="5967c-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="5967c-204">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="5967c-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="5967c-206">Na lista de aplicações de Olá, selecione **Proofpoint a pedido**.</span><span class="sxs-lookup"><span data-stu-id="5967c-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="5967c-208">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5967c-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="5967c-210">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="5967c-210">Click **Add** button.</span></span> <span data-ttu-id="5967c-211">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5967c-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="5967c-213">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="5967c-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5967c-214">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5967c-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5967c-215">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5967c-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5967c-216">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="5967c-216">Testing single sign-on</span></span>

<span data-ttu-id="5967c-217">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="5967c-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5967c-218">Ao clicar em Olá **Proofpoint a pedido** mosaico Olá painel de acesso, esta deve ser iniciada automaticamente no tooyour Proofpoint na aplicação a pedido.</span><span class="sxs-lookup"><span data-stu-id="5967c-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="5967c-219">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5967c-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="5967c-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5967c-220">Additional resources</span></span>

* [<span data-ttu-id="5967c-221">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5967c-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5967c-222">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5967c-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

