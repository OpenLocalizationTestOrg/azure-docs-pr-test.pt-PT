---
title: "Tutorial: Integração do Azure Active Directory com Tangoe comando Premium Mobile | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Tangoe comando Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="24ca7-103">Tutorial: Integração do Azure Active Directory com Tangoe comando Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="24ca7-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="24ca7-104">Neste tutorial, saiba como toointegrate Tangoe comando Premium Mobile com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24ca7-104">In this tutorial, you learn how toointegrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24ca7-105">Integrar Tangoe comando Premium Mobile com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="24ca7-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24ca7-106">Pode controlar no Azure AD que tenha acesso tooTangoe comando Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="24ca7-106">You can control in Azure AD who has access tooTangoe Command Premium Mobile</span></span>
- <span data-ttu-id="24ca7-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooTangoe comando Premium Mobile (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24ca7-107">You can enable your users tooautomatically get signed-on tooTangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24ca7-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="24ca7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24ca7-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24ca7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24ca7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="24ca7-110">Prerequisites</span></span>

<span data-ttu-id="24ca7-111">integração do Azure AD com Tangoe comando Premium Mobile tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="24ca7-111">tooconfigure Azure AD integration with Tangoe Command Premium Mobile, you need hello following items:</span></span>

- <span data-ttu-id="24ca7-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24ca7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24ca7-113">Um Tangoe comando Premium Mobile-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="24ca7-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24ca7-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="24ca7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24ca7-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="24ca7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24ca7-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="24ca7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24ca7-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24ca7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24ca7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="24ca7-118">Scenario description</span></span>
<span data-ttu-id="24ca7-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="24ca7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24ca7-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="24ca7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24ca7-121">Adicionar Tangoe comando Premium móveis a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="24ca7-121">Add Tangoe Command Premium Mobile from hello gallery</span></span>
2. <span data-ttu-id="24ca7-122">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="24ca7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a><span data-ttu-id="24ca7-123">Adicionar Tangoe comando Premium móveis a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="24ca7-123">Add Tangoe Command Premium Mobile from hello gallery</span></span>
<span data-ttu-id="24ca7-124">tooconfigure Olá integração de Tangoe comando Premium Mobile com o Azure AD, é necessário tooadd Tangoe comando Premium Mobile Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="24ca7-124">tooconfigure hello integration of Tangoe Command Premium Mobile into Azure AD, you need tooadd Tangoe Command Premium Mobile from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24ca7-125">**tooadd Tangoe comando Premium Mobile da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="24ca7-125">**tooadd Tangoe Command Premium Mobile from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24ca7-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="24ca7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24ca7-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24ca7-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="24ca7-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24ca7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="24ca7-133">Na caixa de pesquisa de Olá, escreva **Tangoe comando Premium Mobile**, selecione **Tangoe comando Premium Mobile** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="24ca7-133">In hello search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button tooadd hello application.</span></span>

    ![<span data-ttu-id="24ca7-134">Adicionar Tangoe comando Premium móveis a partir da Galeria</span><span class="sxs-lookup"><span data-stu-id="24ca7-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="24ca7-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="24ca7-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="24ca7-136">Nesta secção, configure e teste do Azure AD-início de sessão único com Tangoe comando Premium móvel com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="24ca7-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24ca7-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Tangoe comando Premium Mobile é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24ca7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tangoe Command Premium Mobile is tooa user in Azure AD.</span></span> <span data-ttu-id="24ca7-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Tangoe comando Premium Mobile tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="24ca7-138">In other words, a link relationship between an Azure AD user and hello related user in Tangoe Command Premium Mobile needs toobe established.</span></span>

<span data-ttu-id="24ca7-139">No Tangoe comando Premium Mobile, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="24ca7-139">In Tangoe Command Premium Mobile, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24ca7-140">tooconfigure e teste do Azure AD-início de sessão único com Tangoe comando Premium móveis, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="24ca7-140">tooconfigure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24ca7-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="24ca7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24ca7-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24ca7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24ca7-143">**[Criar um utilizador de teste Tangoe comando Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave um homólogo de Britta Simon no Tangoe comando Premium móvel que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="24ca7-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - toohave a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24ca7-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="24ca7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24ca7-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="24ca7-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="24ca7-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="24ca7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="24ca7-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação móvel do Tangoe comando Premium.</span><span class="sxs-lookup"><span data-stu-id="24ca7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="24ca7-148">**tooconfigure do Azure AD-início de sessão único com Tangoe comando Premium Mobile, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="24ca7-148">**tooconfigure Azure AD single sign-on with Tangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="24ca7-149">No Olá portal do Azure, no Olá **Tangoe comando Premium Mobile** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-149">In hello Azure portal, on hello **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="24ca7-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="24ca7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Baseados em SAML início de sessão](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="24ca7-153">No Olá **Tangoe comando Premium Mobile domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="24ca7-153">On hello **Tangoe Command Premium Mobile Domain and URLs** section, perform hello following steps:</span></span>

    ![Comando Tangoe Premium móveis domínio e os URLs](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="24ca7-155">a.</span><span class="sxs-lookup"><span data-stu-id="24ca7-155">a.</span></span> <span data-ttu-id="24ca7-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="24ca7-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="24ca7-157">b.</span><span class="sxs-lookup"><span data-stu-id="24ca7-157">b.</span></span> <span data-ttu-id="24ca7-158">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="24ca7-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24ca7-159">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="24ca7-159">These values are not real.</span></span> <span data-ttu-id="24ca7-160">Atualize estes valores com o URL de resposta real Olá e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="24ca7-160">Update these values with hello actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="24ca7-161">Contacte [equipa de suporte de cliente de Mobile Tangoe comando Premium](https://www.tangoe.com/contact-2/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="24ca7-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooget these values.</span></span> 

4. <span data-ttu-id="24ca7-162">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="24ca7-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Secção de certificado de assinatura de SAML](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="24ca7-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="24ca7-164">Click **Save** button.</span></span>

    ![botão Guardar](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="24ca7-166">No Olá **Tangoe comando Premium Mobile configuração** secção, clique em **configurar Tangoe comando Premium Mobile** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="24ca7-166">On hello **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="24ca7-167">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="24ca7-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Secção de configuração de móvel Tangoe comando Premium](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="24ca7-169">tooget SSO configurado para a sua aplicação, contacte o seu [equipa de suporte de cliente de Mobile Tangoe comando Premium](https://www.tangoe.com/contact-2/) e fornece Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="24ca7-169">tooget SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide hello following:</span></span>

   - <span data-ttu-id="24ca7-170">ficheiro de metadados transferido Olá</span><span class="sxs-lookup"><span data-stu-id="24ca7-170">hello downloaded metadata file</span></span>
   - <span data-ttu-id="24ca7-171">Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="24ca7-171">hello **SAML Entity ID**</span></span>
   - <span data-ttu-id="24ca7-172">Olá **único início de sessão no URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="24ca7-172">hello **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="24ca7-173">Olá **Sign-Out URL**</span><span class="sxs-lookup"><span data-stu-id="24ca7-173">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="24ca7-174">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="24ca7-174">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24ca7-175">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="24ca7-175">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24ca7-176">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24ca7-176">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="24ca7-177">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24ca7-177">Create an Azure AD test user</span></span>
<span data-ttu-id="24ca7-178">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="24ca7-178">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="24ca7-180">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="24ca7-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24ca7-181">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="24ca7-181">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24ca7-183">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-183">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utilizadores e grupos -> todos os utilizadores](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24ca7-185">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="24ca7-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Adicionar utilizador](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24ca7-187">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="24ca7-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Página de caixa de diálogo de utilizador](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24ca7-189">a.</span><span class="sxs-lookup"><span data-stu-id="24ca7-189">a.</span></span> <span data-ttu-id="24ca7-190">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-190">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24ca7-191">b.</span><span class="sxs-lookup"><span data-stu-id="24ca7-191">b.</span></span> <span data-ttu-id="24ca7-192">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24ca7-192">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24ca7-193">c.</span><span class="sxs-lookup"><span data-stu-id="24ca7-193">c.</span></span> <span data-ttu-id="24ca7-194">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24ca7-195">d.</span><span class="sxs-lookup"><span data-stu-id="24ca7-195">d.</span></span> <span data-ttu-id="24ca7-196">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="24ca7-197">Criar um utilizador de teste Tangoe comando Premium Mobile</span><span class="sxs-lookup"><span data-stu-id="24ca7-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="24ca7-198">Nesta secção, vai criar um utilizador chamado Britta Simon Tangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="24ca7-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="24ca7-199">Aplicação Tangoe comando Premium Mobile tem todos os Olá utilizadores toobe aprovisionados na aplicação Olá antes de efetuar início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="24ca7-199">Tangoe Command Premium Mobile application needs all hello users toobe provisioned in hello application before doing Single Sign On.</span></span> <span data-ttu-id="24ca7-200">Por isso, consulte o trabalho com Olá [equipa de suporte de cliente de Mobile Tangoe comando Premium](https://www.tangoe.com/contact-2/) tooprovision todos os estes utilizadores numa aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="24ca7-200">So please work with hello [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) tooprovision all these users into hello application.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="24ca7-201">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24ca7-201">Assign hello Azure AD test user</span></span>

<span data-ttu-id="24ca7-202">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooTangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="24ca7-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTangoe Command Premium Mobile.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="24ca7-204">**tooassign Britta Simon tooTangoe comando Premium Mobile, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="24ca7-204">**tooassign Britta Simon tooTangoe Command Premium Mobile, perform hello following steps:**</span></span>

1. <span data-ttu-id="24ca7-205">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="24ca7-207">Na lista de aplicações de Olá, selecione **Tangoe comando Premium Mobile**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-207">In hello applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![Tangoe comando Premium Mobile na lista de aplicações](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="24ca7-209">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="24ca7-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="24ca7-211">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="24ca7-211">Click **Add** button.</span></span> <span data-ttu-id="24ca7-212">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24ca7-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="24ca7-214">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="24ca7-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24ca7-215">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24ca7-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24ca7-216">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24ca7-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="24ca7-217">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="24ca7-217">Test single sign-on</span></span>

<span data-ttu-id="24ca7-218">Nesta secção, testar a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="24ca7-218">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="24ca7-219">Ao clicar em mosaico de Tangoe comando Premium Mobile Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour aplicação Tangoe comando Premium Mobile.</span><span class="sxs-lookup"><span data-stu-id="24ca7-219">When you click hello Tangoe Command Premium Mobile tile in hello Access Panel, you should get automatically signed-on tooyour Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="24ca7-220">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24ca7-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="24ca7-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="24ca7-221">Additional resources</span></span>

* [<span data-ttu-id="24ca7-222">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24ca7-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24ca7-223">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24ca7-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

