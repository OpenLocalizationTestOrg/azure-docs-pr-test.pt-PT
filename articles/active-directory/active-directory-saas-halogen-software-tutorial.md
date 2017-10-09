---
title: "Tutorial: Integração do Azure Active Directory com o Halogen Software | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Halogen Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="f54b1-103">Tutorial: Integração do Azure Active Directory com Halogen Software</span><span class="sxs-lookup"><span data-stu-id="f54b1-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="f54b1-104">Neste tutorial, saiba como toointegrate Halogen Software com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f54b1-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f54b1-105">Integrar Halogen Software com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="f54b1-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f54b1-106">Pode controlar no Azure AD que tenha acesso tooHalogen Software</span><span class="sxs-lookup"><span data-stu-id="f54b1-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="f54b1-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooHalogen Software (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f54b1-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f54b1-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f54b1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f54b1-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f54b1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f54b1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f54b1-110">Prerequisites</span></span>

<span data-ttu-id="f54b1-111">integração do Azure AD com o Software de Halogen tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f54b1-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="f54b1-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f54b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f54b1-113">Um Halogen Software-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="f54b1-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f54b1-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f54b1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f54b1-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f54b1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f54b1-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="f54b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f54b1-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f54b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f54b1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f54b1-118">Scenario description</span></span>

<span data-ttu-id="f54b1-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f54b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f54b1-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="f54b1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f54b1-121">Adicionar Halogen Software da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f54b1-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="f54b1-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f54b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="f54b1-123">Adicionar Halogen Software da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f54b1-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="f54b1-124">tooconfigure Olá integração Halogen software com o Azure AD, é necessário tooadd Halogen Software Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="f54b1-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f54b1-125">**tooadd Software Halogen da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f54b1-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f54b1-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f54b1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f54b1-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f54b1-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="f54b1-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f54b1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="f54b1-133">Na caixa de pesquisa de Olá, escreva **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-133">In hello search box, type **Halogen Software**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="f54b1-135">No painel de resultados de Olá, selecione **Halogen Software**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="f54b1-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f54b1-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f54b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f54b1-138">Nesta secção, configure e teste do Azure AD-início de sessão único com o Software de Halogen com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f54b1-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f54b1-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Halogen Software é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f54b1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="f54b1-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no Halogen Software tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f54b1-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="f54b1-141">No Halogen Software, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="f54b1-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f54b1-142">tooconfigure e teste do Azure AD-início de sessão único com o Software de Halogen, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f54b1-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f54b1-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f54b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f54b1-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f54b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f54b1-145">**[Criar um utilizador de teste de Halogen Software](#creating-a-halogen-software-test-user)**  -toohave um homólogo de Britta Simon no Software Halogen toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="f54b1-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f54b1-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f54b1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f54b1-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="f54b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f54b1-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f54b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f54b1-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="f54b1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="f54b1-150">**tooconfigure do Azure AD-início de sessão único com o Software de Halogen, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f54b1-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="f54b1-151">No Olá portal do Azure, no Olá **Halogen Software** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="f54b1-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f54b1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="f54b1-155">No Olá **Halogen Software domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f54b1-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="f54b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="f54b1-157">a.</span></span> <span data-ttu-id="f54b1-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="f54b1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="f54b1-159">b.</span><span class="sxs-lookup"><span data-stu-id="f54b1-159">b.</span></span> <span data-ttu-id="f54b1-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="f54b1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f54b1-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="f54b1-161">These values are not real.</span></span> <span data-ttu-id="f54b1-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="f54b1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f54b1-163">Contacte [equipa de suporte de cliente de Software Halogen](https://support.halogensoftware.com/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="f54b1-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="f54b1-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="f54b1-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="f54b1-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="f54b1-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f54b1-168">Numa janela do browser diferente, início de sessão tooyour **Halogen Software** aplicação como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f54b1-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="f54b1-169">Clique em Olá **opções** separador.</span><span class="sxs-lookup"><span data-stu-id="f54b1-169">Click hello **Options** tab.</span></span> 
   
    ![O que é o Azure AD Connect][12]

8. <span data-ttu-id="f54b1-171">No painel de navegação esquerdo Olá, clique em **configuração SAML**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![O que é o Azure AD Connect][13]

9. <span data-ttu-id="f54b1-173">No Olá **configuração SAML** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f54b1-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![O que é o Azure AD Connect][14]

     <span data-ttu-id="f54b1-175">a.</span><span class="sxs-lookup"><span data-stu-id="f54b1-175">a.</span></span> <span data-ttu-id="f54b1-176">Como **Identificador exclusivo**, selecione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="f54b1-177">b.</span><span class="sxs-lookup"><span data-stu-id="f54b1-177">b.</span></span> <span data-ttu-id="f54b1-178">Como **exclusivo mapas de identificador da para**, selecione **Username**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="f54b1-179">c.</span><span class="sxs-lookup"><span data-stu-id="f54b1-179">c.</span></span> <span data-ttu-id="f54b1-180">tooupload o ficheiro de metadados transferido, clique em **procurar** tooselect ficheiro de Olá e, em seguida, **carregar o ficheiro**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="f54b1-181">d.</span><span class="sxs-lookup"><span data-stu-id="f54b1-181">d.</span></span> <span data-ttu-id="f54b1-182">configuração de Olá tootest, clique em **executar teste**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="f54b1-183">Precisa de toowait para mensagem de saudação "*Olá SAML teste estiver concluído. Feche esta janela*".</span><span class="sxs-lookup"><span data-stu-id="f54b1-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="f54b1-184">Em seguida, feche a janela do browser aberta de Olá.</span><span class="sxs-lookup"><span data-stu-id="f54b1-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="f54b1-185">Olá **ativar SAML** caixa de verificação só é ativada se o teste de Olá foi concluída.</span><span class="sxs-lookup"><span data-stu-id="f54b1-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="f54b1-186">e.</span><span class="sxs-lookup"><span data-stu-id="f54b1-186">e.</span></span> <span data-ttu-id="f54b1-187">Selecione **ativar SAML**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="f54b1-188">f.</span><span class="sxs-lookup"><span data-stu-id="f54b1-188">f.</span></span> <span data-ttu-id="f54b1-189">Clique em **guardar alterações**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="f54b1-190">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="f54b1-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f54b1-191">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="f54b1-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f54b1-192">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f54b1-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f54b1-193">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f54b1-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="f54b1-194">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f54b1-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="f54b1-196">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f54b1-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f54b1-197">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f54b1-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f54b1-199">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f54b1-201">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="f54b1-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f54b1-203">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f54b1-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f54b1-205">a.</span><span class="sxs-lookup"><span data-stu-id="f54b1-205">a.</span></span> <span data-ttu-id="f54b1-206">No Olá **nome** caixa de texto, nome do tipo como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="f54b1-207">b.</span><span class="sxs-lookup"><span data-stu-id="f54b1-207">b.</span></span> <span data-ttu-id="f54b1-208">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f54b1-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f54b1-209">c.</span><span class="sxs-lookup"><span data-stu-id="f54b1-209">c.</span></span> <span data-ttu-id="f54b1-210">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f54b1-211">d.</span><span class="sxs-lookup"><span data-stu-id="f54b1-211">d.</span></span> <span data-ttu-id="f54b1-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="f54b1-213">Criar um utilizador de teste Halogen Software</span><span class="sxs-lookup"><span data-stu-id="f54b1-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="f54b1-214">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Halogen software.</span><span class="sxs-lookup"><span data-stu-id="f54b1-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="f54b1-215">**toocreate um utilizador chamado Britta Simon no Halogen Software, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f54b1-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="f54b1-216">Início de sessão tooyour **Halogen Software** aplicação como um administrador.</span><span class="sxs-lookup"><span data-stu-id="f54b1-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="f54b1-217">Clique em Olá **utilizador Center** separador e, em seguida, clique em **criar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![O que é o Azure AD Connect][300]  

3. <span data-ttu-id="f54b1-219">No Olá **novo utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f54b1-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![O que é o Azure AD Connect][301]

    <span data-ttu-id="f54b1-221">a.</span><span class="sxs-lookup"><span data-stu-id="f54b1-221">a.</span></span> <span data-ttu-id="f54b1-222">No Olá **nome próprio** caixa de texto, nome do primeiro tipo de utilizador de Olá como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="f54b1-223">b.</span><span class="sxs-lookup"><span data-stu-id="f54b1-223">b.</span></span> <span data-ttu-id="f54b1-224">No Olá **Apelido** caixa de texto, apelido tipo de utilizador de Olá como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="f54b1-225">c.</span><span class="sxs-lookup"><span data-stu-id="f54b1-225">c.</span></span> <span data-ttu-id="f54b1-226">No Olá **Username** caixa de texto, tipo **Britta Simon**, nome de utilizador de Olá que aparece Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f54b1-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="f54b1-227">d.</span><span class="sxs-lookup"><span data-stu-id="f54b1-227">d.</span></span> <span data-ttu-id="f54b1-228">No Olá **palavra-passe** caixa de texto, escreva um palavra-passe para Britta.</span><span class="sxs-lookup"><span data-stu-id="f54b1-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="f54b1-229">e.</span><span class="sxs-lookup"><span data-stu-id="f54b1-229">e.</span></span> <span data-ttu-id="f54b1-230">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f54b1-231">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f54b1-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f54b1-232">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooHalogen Software.</span><span class="sxs-lookup"><span data-stu-id="f54b1-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="f54b1-234">**tooassign Britta Simon tooHalogen Software, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f54b1-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="f54b1-235">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="f54b1-237">Na lista de aplicações de Olá, selecione **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="f54b1-239">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f54b1-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="f54b1-241">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="f54b1-241">Click **Add** button.</span></span> <span data-ttu-id="f54b1-242">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f54b1-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="f54b1-244">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="f54b1-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f54b1-245">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f54b1-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f54b1-246">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f54b1-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f54b1-247">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f54b1-247">Testing single sign-on</span></span>

<span data-ttu-id="f54b1-248">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f54b1-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="f54b1-249">Ao clicar em mosaico de Halogen Software Olá no painel de acesso de Olá, deve obter as aplicações de Halogen Software tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="f54b1-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f54b1-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f54b1-250">Additional resources</span></span>

* [<span data-ttu-id="f54b1-251">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f54b1-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f54b1-252">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f54b1-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
