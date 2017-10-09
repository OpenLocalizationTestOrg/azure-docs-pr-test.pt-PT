---
title: "Tutorial: Integração do Azure Active Directory com Zoom | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Zoom."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 623a1f428ad1f0aa2c8205b79d61720cad5fc6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="f3b92-103">Tutorial: Integração do Azure Active Directory com o Zoom</span><span class="sxs-lookup"><span data-stu-id="f3b92-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="f3b92-104">Neste tutorial, saiba como toointegrate Zoom no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3b92-104">In this tutorial, you learn how toointegrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3b92-105">Integrar o Zoom com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="f3b92-105">Integrating Zoom with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f3b92-106">Pode controlar no Azure AD que tenha acesso tooZoom.</span><span class="sxs-lookup"><span data-stu-id="f3b92-106">You can control in Azure AD who has access tooZoom.</span></span>
- <span data-ttu-id="f3b92-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooZoom (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3b92-107">You can enable your users tooautomatically get signed-on tooZoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f3b92-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b92-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="f3b92-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f3b92-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3b92-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f3b92-110">Prerequisites</span></span>

<span data-ttu-id="f3b92-111">integração de tooconfigure do Azure AD com o Zoom, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f3b92-111">tooconfigure Azure AD integration with Zoom, you need hello following items:</span></span>

- <span data-ttu-id="f3b92-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3b92-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3b92-113">Um Zoom-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="f3b92-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3b92-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f3b92-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3b92-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f3b92-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3b92-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f3b92-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3b92-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3b92-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3b92-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f3b92-118">Scenario description</span></span>
<span data-ttu-id="f3b92-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f3b92-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3b92-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="f3b92-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3b92-121">A adição de Zoom da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f3b92-121">Adding Zoom from hello gallery</span></span>
2. <span data-ttu-id="f3b92-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f3b92-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-hello-gallery"></a><span data-ttu-id="f3b92-123">A adição de Zoom da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f3b92-123">Adding Zoom from hello gallery</span></span>
<span data-ttu-id="f3b92-124">integração de Olá tooconfigure de Zoom com o Azure AD, é necessário tooadd Zoom Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="f3b92-124">tooconfigure hello integration of Zoom into Azure AD, you need tooadd Zoom from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f3b92-125">**tooadd Zoom da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f3b92-125">**tooadd Zoom from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3b92-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f3b92-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="f3b92-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f3b92-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="f3b92-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3b92-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="f3b92-133">Na caixa de pesquisa de Olá, escreva **Zoom**, selecione **Zoom** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="f3b92-133">In hello search box, type **Zoom**, select **Zoom** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ampliar a lista de resultados de Olá](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f3b92-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f3b92-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f3b92-136">Nesta secção, configure e teste do Azure AD-início de sessão único com Zoom com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f3b92-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f3b92-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Zoom é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3b92-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zoom is tooa user in Azure AD.</span></span> <span data-ttu-id="f3b92-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados com o utilizador no Zoom necessidades toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f3b92-138">In other words, a link relationship between an Azure AD user and hello related user in Zoom needs toobe established.</span></span>

<span data-ttu-id="f3b92-139">Zoom, atribuir valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="f3b92-139">In Zoom, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f3b92-140">tooconfigure e teste do Azure AD-início de sessão único com Zoom, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f3b92-140">tooconfigure and test Azure AD single sign-on with Zoom, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f3b92-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f3b92-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f3b92-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3b92-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f3b92-143">**[Criar um utilizador de teste de Zoom](#create-a-zoom-test-user)**  -toohave um homólogo de Britta Simon no Zoom é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="f3b92-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - toohave a counterpart of Britta Simon in Zoom that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f3b92-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f3b92-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f3b92-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="f3b92-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f3b92-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f3b92-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f3b92-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de Zoom.</span><span class="sxs-lookup"><span data-stu-id="f3b92-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="f3b92-148">**tooconfigure do Azure AD-início de sessão único com Zoom, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f3b92-148">**tooconfigure Azure AD single sign-on with Zoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3b92-149">No Olá portal do Azure, no Olá **Zoom** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-149">In hello Azure portal, on hello **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="f3b92-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f3b92-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="f3b92-153">No Olá **domínio Zoom e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f3b92-153">On hello **Zoom Domain and URLs** section, perform hello following steps:</span></span>

    ![Domínio de zoom e os URLs únicos de informações de início de sessão](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="f3b92-155">a.</span><span class="sxs-lookup"><span data-stu-id="f3b92-155">a.</span></span> <span data-ttu-id="f3b92-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="f3b92-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="f3b92-157">b.</span><span class="sxs-lookup"><span data-stu-id="f3b92-157">b.</span></span> <span data-ttu-id="f3b92-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="f3b92-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f3b92-159">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="f3b92-159">These values are not real.</span></span> <span data-ttu-id="f3b92-160">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="f3b92-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f3b92-161">Contacte [equipa de suporte de cliente de Zoom](https://support.zoom.us/hc) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="f3b92-161">Contact [Zoom Client support team](https://support.zoom.us/hc) tooget these values.</span></span> 
 
4. <span data-ttu-id="f3b92-162">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="f3b92-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="f3b92-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="f3b92-164">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f3b92-166">No Olá **Zoom configuração** secção, clique em **configurar Zoom** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="f3b92-166">On hello **Zoom Configuration** section, click **Configure Zoom** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f3b92-167">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="f3b92-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="f3b92-169">Numa janela do browser web diferente, inicie sessão no site de empresa de Zoom tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="f3b92-169">In a different web browser window, log in tooyour Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="f3b92-170">Clique em Olá **Single Sign-On** separador.</span><span class="sxs-lookup"><span data-stu-id="f3b92-170">Click hello **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="f3b92-171">![Separador de início de sessão único](./media/active-directory-saas-zoom-tutorial/IC784700.png "de sessão único-")</span><span class="sxs-lookup"><span data-stu-id="f3b92-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="f3b92-172">Clique em Olá **controlo de segurança** separador e, em seguida, aceda toohello **Single Sign-On** definições.</span><span class="sxs-lookup"><span data-stu-id="f3b92-172">Click hello **Security Control** tab, and then go toohello **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="f3b92-173">Na secção Single Sign-On Olá, efetue Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f3b92-173">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f3b92-174">![Único início de sessão na secção](./media/active-directory-saas-zoom-tutorial/IC784701.png "de sessão único-")</span><span class="sxs-lookup"><span data-stu-id="f3b92-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="f3b92-175">a.</span><span class="sxs-lookup"><span data-stu-id="f3b92-175">a.</span></span> <span data-ttu-id="f3b92-176">No Olá **URL de página de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b92-176">In hello **Sign-in page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="f3b92-177">b.</span><span class="sxs-lookup"><span data-stu-id="f3b92-177">b.</span></span> <span data-ttu-id="f3b92-178">No Olá **URL da página de início de sessão** caixa de texto, colar Olá valor **Sign-Out URL**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b92-178">In hello **Sign-out page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="f3b92-179">c.</span><span class="sxs-lookup"><span data-stu-id="f3b92-179">c.</span></span> <span data-ttu-id="f3b92-180">Abra o certificado codificado base-64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f3b92-180">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="f3b92-181">d.</span><span class="sxs-lookup"><span data-stu-id="f3b92-181">d.</span></span> <span data-ttu-id="f3b92-182">No Olá **emissor** caixa de texto, colar Olá valor **ID de entidade de SAML**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b92-182">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="f3b92-183">e.</span><span class="sxs-lookup"><span data-stu-id="f3b92-183">e.</span></span> <span data-ttu-id="f3b92-184">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f3b92-185">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="f3b92-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f3b92-186">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="f3b92-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f3b92-187">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3b92-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f3b92-188">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3b92-188">Create an Azure AD test user</span></span>

<span data-ttu-id="f3b92-189">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f3b92-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="f3b92-191">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f3b92-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3b92-192">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="f3b92-192">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f3b92-194">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-194">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f3b92-196">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3b92-196">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f3b92-198">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f3b92-198">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f3b92-200">a.</span><span class="sxs-lookup"><span data-stu-id="f3b92-200">a.</span></span> <span data-ttu-id="f3b92-201">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-201">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3b92-202">b.</span><span class="sxs-lookup"><span data-stu-id="f3b92-202">b.</span></span> <span data-ttu-id="f3b92-203">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3b92-203">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="f3b92-204">c.</span><span class="sxs-lookup"><span data-stu-id="f3b92-204">c.</span></span> <span data-ttu-id="f3b92-205">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="f3b92-205">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="f3b92-206">d.</span><span class="sxs-lookup"><span data-stu-id="f3b92-206">d.</span></span> <span data-ttu-id="f3b92-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="f3b92-208">Criar um utilizador de teste de Zoom</span><span class="sxs-lookup"><span data-stu-id="f3b92-208">Create a Zoom test user</span></span>

<span data-ttu-id="f3b92-209">Na ordem tooenable do Azure AD os utilizadores toolog no tooZoom, têm de ser aprovisionados para Zoom.</span><span class="sxs-lookup"><span data-stu-id="f3b92-209">In order tooenable Azure AD users toolog in tooZoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="f3b92-210">No caso de Olá do Zoom, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f3b92-210">In hello case of Zoom, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="f3b92-211">tooprovision uma conta de utilizador, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f3b92-211">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="f3b92-212">Inicie sessão no tooyour **Zoom** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="f3b92-212">Log in tooyour **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="f3b92-213">Clique em Olá **gestão de contas** separador e, em seguida, clique em **gestão de utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-213">Click hello **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="f3b92-214">Na secção de gestão de utilizadores Olá, clique em **adicionar utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-214">In hello User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="f3b92-215">![Gestão de utilizadores](./media/active-directory-saas-zoom-tutorial/IC784703.png "gestão de utilizadores")</span><span class="sxs-lookup"><span data-stu-id="f3b92-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="f3b92-216">No Olá **adicionar utilizadores** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f3b92-216">On hello **Add users** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="f3b92-217">![Adicionar utilizadores](./media/active-directory-saas-zoom-tutorial/IC784704.png "adicionar utilizadores")</span><span class="sxs-lookup"><span data-stu-id="f3b92-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="f3b92-218">a.</span><span class="sxs-lookup"><span data-stu-id="f3b92-218">a.</span></span> <span data-ttu-id="f3b92-219">Como **tipo de utilizador**, selecione **básico**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="f3b92-220">b.</span><span class="sxs-lookup"><span data-stu-id="f3b92-220">b.</span></span> <span data-ttu-id="f3b92-221">No Olá **E-mails** caixa de texto, tipo Olá endereço de correio eletrónico de um Azure válido pretende tooprovision de conta do AD.</span><span class="sxs-lookup"><span data-stu-id="f3b92-221">In hello **Emails** textbox, type hello email address of a valid Azure AD account you want tooprovision.</span></span>

    <span data-ttu-id="f3b92-222">c.</span><span class="sxs-lookup"><span data-stu-id="f3b92-222">c.</span></span> <span data-ttu-id="f3b92-223">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="f3b92-224">Pode utilizar quaisquer outras Zoom utilizador conta criação ferramentas ou APIs fornecidas pelo tooprovision de Zoom do Azure Active Directory, contas de utilizador.</span><span class="sxs-lookup"><span data-stu-id="f3b92-224">You can use any other Zoom user account creation tools or APIs provided by Zoom tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f3b92-225">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3b92-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f3b92-226">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooZoom.</span><span class="sxs-lookup"><span data-stu-id="f3b92-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZoom.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="f3b92-228">**tooassign Britta Simon tooZoom, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f3b92-228">**tooassign Britta Simon tooZoom, perform hello following steps:**</span></span>

1. <span data-ttu-id="f3b92-229">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="f3b92-231">Na lista de aplicações de Olá, selecione **Zoom**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-231">In hello applications list, select **Zoom**.</span></span>

    ![ligação de Zoom Olá na lista de aplicações de Olá](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="f3b92-233">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f3b92-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="f3b92-235">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="f3b92-235">Click **Add** button.</span></span> <span data-ttu-id="f3b92-236">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3b92-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="f3b92-238">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="f3b92-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f3b92-239">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3b92-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f3b92-240">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f3b92-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f3b92-241">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f3b92-241">Test single sign-on</span></span>

<span data-ttu-id="f3b92-242">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f3b92-242">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f3b92-243">Ao clicar em mosaico de Zoom Olá no painel de acesso de Olá, deve colocar a aplicação de Zoom do tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="f3b92-243">When you click hello Zoom tile in hello Access Panel, you should get automatically signed-on tooyour Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3b92-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f3b92-244">Additional resources</span></span>

* [<span data-ttu-id="f3b92-245">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3b92-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f3b92-246">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3b92-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

