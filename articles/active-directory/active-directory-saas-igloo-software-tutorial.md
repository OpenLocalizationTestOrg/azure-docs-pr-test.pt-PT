---
title: "Tutorial: Integração do Azure Active Directory com o Igloo Software | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="ae868-103">Tutorial: Integração do Azure Active Directory com Igloo Software</span><span class="sxs-lookup"><span data-stu-id="ae868-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="ae868-104">Neste tutorial, saiba como toointegrate Igloo Software com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae868-104">In this tutorial, you learn how toointegrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae868-105">Integrar Igloo Software com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="ae868-105">Integrating Igloo Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ae868-106">Pode controlar no Azure AD que tenha acesso tooIgloo Software</span><span class="sxs-lookup"><span data-stu-id="ae868-106">You can control in Azure AD who has access tooIgloo Software</span></span>
- <span data-ttu-id="ae868-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooIgloo Software (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae868-107">You can enable your users tooautomatically get signed-on tooIgloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae868-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ae868-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ae868-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae868-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae868-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae868-110">Prerequisites</span></span>

<span data-ttu-id="ae868-111">integração do Azure AD com o Software de Igloo tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ae868-111">tooconfigure Azure AD integration with Igloo Software, you need hello following items:</span></span>

- <span data-ttu-id="ae868-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae868-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae868-113">Um Igloo Software-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="ae868-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae868-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ae868-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae868-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ae868-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae868-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ae868-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae868-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae868-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae868-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ae868-118">Scenario description</span></span>
<span data-ttu-id="ae868-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ae868-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae868-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="ae868-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae868-121">Adicionar Igloo Software da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="ae868-121">Adding Igloo Software from hello gallery</span></span>
2. <span data-ttu-id="ae868-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="ae868-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-hello-gallery"></a><span data-ttu-id="ae868-123">Adicionar Igloo Software da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="ae868-123">Adding Igloo Software from hello gallery</span></span>
<span data-ttu-id="ae868-124">tooconfigure Olá integração Igloo software com o Azure AD, é necessário tooadd Igloo Software Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="ae868-124">tooconfigure hello integration of Igloo Software into Azure AD, you need tooadd Igloo Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ae868-125">**tooadd Software Igloo da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ae868-125">**tooadd Igloo Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae868-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="ae868-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae868-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ae868-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ae868-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="ae868-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="ae868-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae868-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="ae868-133">Na caixa de pesquisa de Olá, escreva **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="ae868-133">In hello search box, type **Igloo Software**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="ae868-135">No painel de resultados de Olá, selecione **Igloo Software**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="ae868-135">In hello results panel, select **Igloo Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae868-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="ae868-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae868-138">Nesta secção, configure e teste do Azure AD-início de sessão único com o Software de Igloo com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae868-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae868-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Igloo Software é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae868-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Igloo Software is tooa user in Azure AD.</span></span> <span data-ttu-id="ae868-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no Igloo Software tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ae868-140">In other words, a link relationship between an Azure AD user and hello related user in Igloo Software needs toobe established.</span></span>

<span data-ttu-id="ae868-141">No Igloo Software, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="ae868-141">In Igloo Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ae868-142">tooconfigure e teste do Azure AD-início de sessão único com o Software de Igloo, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ae868-142">tooconfigure and test Azure AD single sign-on with Igloo Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ae868-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="ae868-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ae868-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae868-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae868-145">**[Criar um utilizador de teste de Igloo Software](#creating-an-igloo-software-test-user)**  -toohave um homólogo de Britta Simon no Software Igloo toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ae868-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - toohave a counterpart of Britta Simon in Igloo Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae868-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="ae868-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae868-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="ae868-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae868-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="ae868-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae868-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="ae868-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="ae868-150">**tooconfigure do Azure AD-início de sessão único com o Software de Igloo, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ae868-150">**tooconfigure Azure AD single sign-on with Igloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae868-151">No Olá portal do Azure, no Olá **Igloo Software** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="ae868-151">In hello Azure portal, on hello **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="ae868-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="ae868-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="ae868-155">No Olá **Igloo Software domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ae868-155">On hello **Igloo Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="ae868-157">a.</span><span class="sxs-lookup"><span data-stu-id="ae868-157">a.</span></span> <span data-ttu-id="ae868-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="ae868-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="ae868-159">b.</span><span class="sxs-lookup"><span data-stu-id="ae868-159">b.</span></span> <span data-ttu-id="ae868-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="ae868-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="ae868-161">c.</span><span class="sxs-lookup"><span data-stu-id="ae868-161">c.</span></span> <span data-ttu-id="ae868-162">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="ae868-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae868-163">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="ae868-163">These values are not real.</span></span> <span data-ttu-id="ae868-164">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="ae868-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ae868-165">Contacte [equipa de suporte de cliente de Software Igloo](https://www.igloosoftware.com/services/support) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="ae868-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="ae868-166">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ae868-166">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="ae868-168">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="ae868-168">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="ae868-170">No Olá **Igloo Software configuração** secção, clique em **configurar Software Igloo** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="ae868-170">On hello **Igloo Software Configuration** section, click **Configure Igloo Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ae868-171">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ae868-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="ae868-173">Numa janela do browser web diferente, inicie sessão no site de empresa de Igloo Software tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="ae868-173">In a different web browser window, log in tooyour Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="ae868-174">Aceda toohello **painel de controlo**.</span><span class="sxs-lookup"><span data-stu-id="ae868-174">Go toohello **Control Panel**.</span></span>
   
     <span data-ttu-id="ae868-175">![Painel de controlo](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "painel de controlo")</span><span class="sxs-lookup"><span data-stu-id="ae868-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="ae868-176">No Olá **associação** separador, clique em **definições de início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="ae868-176">In hello **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="ae868-177">![Iniciar sessão nas definições](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "iniciar sessão nas definições")</span><span class="sxs-lookup"><span data-stu-id="ae868-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="ae868-178">Na secção de configuração de SAML Olá, clique em **configurar a autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="ae868-178">In hello SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="ae868-179">![Configuração de SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="ae868-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="ae868-180">No Olá **configuração geral** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ae868-180">In hello **General Configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ae868-181">![Configuração geral](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "configuração geral")</span><span class="sxs-lookup"><span data-stu-id="ae868-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="ae868-182">a.</span><span class="sxs-lookup"><span data-stu-id="ae868-182">a.</span></span> <span data-ttu-id="ae868-183">No Olá **nome da ligação** caixa de texto, escreva um nome personalizado para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="ae868-183">In hello **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="ae868-184">b.</span><span class="sxs-lookup"><span data-stu-id="ae868-184">b.</span></span> <span data-ttu-id="ae868-185">No Olá **URL de início de sessão do IdP** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae868-185">In hello **IdP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="ae868-186">c.</span><span class="sxs-lookup"><span data-stu-id="ae868-186">c.</span></span> <span data-ttu-id="ae868-187">No Olá **URL de fim de sessão do IdP** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae868-187">In hello **IdP Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="ae868-188">d.</span><span class="sxs-lookup"><span data-stu-id="ae868-188">d.</span></span> <span data-ttu-id="ae868-189">Selecione **resposta de fim de sessão e o tipo de pedido de HTTP** como **POST**.</span><span class="sxs-lookup"><span data-stu-id="ae868-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="ae868-190">e.</span><span class="sxs-lookup"><span data-stu-id="ae868-190">e.</span></span> <span data-ttu-id="ae868-191">Abra o **base-64** codificado certificado no bloco de notas transferido a partir do portal do Azure, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado público** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ae868-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="ae868-192">No Olá **resposta e a configuração de autenticação**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ae868-192">In hello **Response and Authentication Configuration**, perform hello following steps:</span></span>
    
    <span data-ttu-id="ae868-193">![Resposta e a configuração de autenticação](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "resposta e a configuração de autenticação")</span><span class="sxs-lookup"><span data-stu-id="ae868-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="ae868-194">a.</span><span class="sxs-lookup"><span data-stu-id="ae868-194">a.</span></span> <span data-ttu-id="ae868-195">Como **fornecedor de identidade**, selecione **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="ae868-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="ae868-196">b.</span><span class="sxs-lookup"><span data-stu-id="ae868-196">b.</span></span> <span data-ttu-id="ae868-197">Como **tipo de identificador**, selecione **endereço de correio eletrónico**.</span><span class="sxs-lookup"><span data-stu-id="ae868-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="ae868-198">c.</span><span class="sxs-lookup"><span data-stu-id="ae868-198">c.</span></span> <span data-ttu-id="ae868-199">No Olá **atributo de correio eletrónico** caixa de texto, tipo **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="ae868-199">In hello **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="ae868-200">d.</span><span class="sxs-lookup"><span data-stu-id="ae868-200">d.</span></span> <span data-ttu-id="ae868-201">No Olá **nome próprio atributo** caixa de texto, tipo **givenname**.</span><span class="sxs-lookup"><span data-stu-id="ae868-201">In hello **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="ae868-202">e.</span><span class="sxs-lookup"><span data-stu-id="ae868-202">e.</span></span> <span data-ttu-id="ae868-203">No Olá **último nome do atributo** caixa de texto, tipo **Apelido**.</span><span class="sxs-lookup"><span data-stu-id="ae868-203">In hello **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="ae868-204">Execute Olá configuração de Olá toocomplete de passos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae868-204">Perform hello following steps toocomplete hello configuration:</span></span>
    
    <span data-ttu-id="ae868-205">![Criação de utilizador no início de sessão](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "criação de utilizador no início de sessão")</span><span class="sxs-lookup"><span data-stu-id="ae868-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="ae868-206">a.</span><span class="sxs-lookup"><span data-stu-id="ae868-206">a.</span></span> <span data-ttu-id="ae868-207">Como **criação de utilizador no início de sessão**, selecione **criar um novo utilizador do seu site quando iniciam sessão no**.</span><span class="sxs-lookup"><span data-stu-id="ae868-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="ae868-208">b.</span><span class="sxs-lookup"><span data-stu-id="ae868-208">b.</span></span> <span data-ttu-id="ae868-209">Como **iniciar sessão nas definições**, selecione **botão SAML de utilização no ecrã de "Iniciar sessão"**.</span><span class="sxs-lookup"><span data-stu-id="ae868-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="ae868-210">c.</span><span class="sxs-lookup"><span data-stu-id="ae868-210">c.</span></span> <span data-ttu-id="ae868-211">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ae868-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ae868-212">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="ae868-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ae868-213">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae868-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ae868-214">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ae868-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae868-215">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae868-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae868-216">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae868-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="ae868-218">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ae868-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae868-219">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="ae868-219">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae868-221">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="ae868-221">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae868-223">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="ae868-223">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae868-225">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ae868-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae868-227">a.</span><span class="sxs-lookup"><span data-stu-id="ae868-227">a.</span></span> <span data-ttu-id="ae868-228">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae868-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae868-229">b.</span><span class="sxs-lookup"><span data-stu-id="ae868-229">b.</span></span> <span data-ttu-id="ae868-230">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae868-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae868-231">c.</span><span class="sxs-lookup"><span data-stu-id="ae868-231">c.</span></span> <span data-ttu-id="ae868-232">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="ae868-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ae868-233">d.</span><span class="sxs-lookup"><span data-stu-id="ae868-233">d.</span></span> <span data-ttu-id="ae868-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ae868-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="ae868-235">Criar um utilizador de teste Igloo Software</span><span class="sxs-lookup"><span data-stu-id="ae868-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="ae868-236">Não há nenhum item de ação para tooconfigure aprovisionamento de utilizadores tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="ae868-236">There is no action item for you tooconfigure user provisioning tooIgloo Software.</span></span>  

<span data-ttu-id="ae868-237">Quando um utilizador atribuído tenta toolog no tooIgloo Software utilizando o painel de acesso de Olá, Igloo Software verifica se o utilizador Olá existe.</span><span class="sxs-lookup"><span data-stu-id="ae868-237">When an assigned user tries toolog in tooIgloo Software using hello access panel, Igloo Software checks whether hello user exists.</span></span>  <span data-ttu-id="ae868-238">Se não existe nenhuma conta de utilizador ainda estão disponíveis, é criado automaticamente pelo Software de Igloo.</span><span class="sxs-lookup"><span data-stu-id="ae868-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ae868-239">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae868-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ae868-240">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooIgloo Software.</span><span class="sxs-lookup"><span data-stu-id="ae868-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIgloo Software.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="ae868-242">**tooassign Britta Simon tooIgloo Software, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ae868-242">**tooassign Britta Simon tooIgloo Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="ae868-243">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="ae868-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="ae868-245">Na lista de aplicações de Olá, selecione **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="ae868-245">In hello applications list, select **Igloo Software**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="ae868-247">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ae868-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="ae868-249">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="ae868-249">Click **Add** button.</span></span> <span data-ttu-id="ae868-250">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae868-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="ae868-252">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="ae868-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ae868-253">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae868-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae868-254">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae868-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae868-255">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="ae868-255">Testing single sign-on</span></span>

<span data-ttu-id="ae868-256">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="ae868-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ae868-257">Ao clicar em mosaico de Igloo Software Olá no painel de acesso de Olá, deve obter as aplicações de Igloo Software tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="ae868-257">When you click hello Igloo Software tile in hello Access Panel, you should get automatically signed-on tooyour Igloo Software application.</span></span>
<span data-ttu-id="ae868-258">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae868-258">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ae868-259">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ae868-259">Additional resources</span></span>

* [<span data-ttu-id="ae868-260">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae868-260">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae868-261">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae868-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

