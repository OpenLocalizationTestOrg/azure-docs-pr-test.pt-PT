---
title: "Tutorial: Integração do Azure Active Directory com Syncplicity | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="6a149-103">Tutorial: Integração do Azure Active Directory com Syncplicity</span><span class="sxs-lookup"><span data-stu-id="6a149-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="6a149-104">Neste tutorial, saiba como toointegrate Syncplicity com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6a149-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a149-105">Integrar Syncplicity com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="6a149-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6a149-106">Pode controlar no Azure AD que tenha acesso tooSyncplicity</span><span class="sxs-lookup"><span data-stu-id="6a149-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="6a149-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSyncplicity (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a149-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a149-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6a149-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6a149-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6a149-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a149-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a149-110">Prerequisites</span></span>

<span data-ttu-id="6a149-111">integração do Azure AD com Syncplicity tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6a149-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="6a149-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a149-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a149-113">Um Syncplicity-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="6a149-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a149-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6a149-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a149-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6a149-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a149-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6a149-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a149-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6a149-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a149-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6a149-118">Scenario description</span></span>
<span data-ttu-id="6a149-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6a149-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a149-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="6a149-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a149-121">Adicionar Syncplicity da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6a149-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="6a149-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6a149-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="6a149-123">Adicionar Syncplicity da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6a149-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="6a149-124">tooconfigure Olá integração de Syncplicity com o Azure AD, é necessário tooadd Syncplicity Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="6a149-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6a149-125">**tooadd Syncplicity da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6a149-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a149-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6a149-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a149-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6a149-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6a149-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6a149-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="6a149-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a149-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="6a149-133">Na caixa de pesquisa de Olá, escreva **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="6a149-133">In hello search box, type **Syncplicity**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="6a149-135">No painel de resultados de Olá, selecione **Syncplicity**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="6a149-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a149-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6a149-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a149-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Syncplicity com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6a149-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6a149-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Syncplicity é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a149-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="6a149-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Syncplicity tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6a149-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="6a149-141">No Syncplicity, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="6a149-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6a149-142">tooconfigure e teste do Azure AD-início de sessão único com Syncplicity, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6a149-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6a149-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="6a149-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6a149-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6a149-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a149-145">**[Criar um utilizador de teste Syncplicity](#creating-a-syncplicity-test-user)**  -toohave um homólogo de Britta Simon no Syncplicity é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="6a149-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a149-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6a149-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a149-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="6a149-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a149-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6a149-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a149-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6a149-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="6a149-150">**tooconfigure do Azure AD-início de sessão único com Syncplicity, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6a149-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a149-151">No Olá portal do Azure, no Olá **Syncplicity** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="6a149-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="6a149-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6a149-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="6a149-155">No Olá **Syncplicity domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6a149-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="6a149-157">a.</span><span class="sxs-lookup"><span data-stu-id="6a149-157">a.</span></span> <span data-ttu-id="6a149-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="6a149-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="6a149-159">b.</span><span class="sxs-lookup"><span data-stu-id="6a149-159">b.</span></span> <span data-ttu-id="6a149-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="6a149-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6a149-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="6a149-161">These values are not real.</span></span> <span data-ttu-id="6a149-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="6a149-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6a149-163">Contacte [equipa de suporte de cliente Syncplicity](https://www.syncplicity.com/contact-us) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="6a149-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="6a149-164">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6a149-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="6a149-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="6a149-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6a149-168">No Olá **Syncplicity configuração** secção, clique em **configurar Syncplicity** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="6a149-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6a149-169">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="6a149-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="6a149-171">Inicie sessão no tooyour **Syncplicity** inquilino.</span><span class="sxs-lookup"><span data-stu-id="6a149-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="6a149-172">No menu de Olá na parte superior do Olá, clique em **admin**, selecione **definições**e, em seguida, clique em **domínio personalizado e o início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="6a149-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="6a149-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="6a149-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="6a149-174">No Olá **único Sign-On (SSO)** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6a149-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="6a149-175">![De sessão único- \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="6a149-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="6a149-176">a.</span><span class="sxs-lookup"><span data-stu-id="6a149-176">a.</span></span> <span data-ttu-id="6a149-177">No Olá **domínio personalizado** caixa de texto, nome do tipo Olá do seu domínio.</span><span class="sxs-lookup"><span data-stu-id="6a149-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="6a149-178">b.</span><span class="sxs-lookup"><span data-stu-id="6a149-178">b.</span></span> <span data-ttu-id="6a149-179">Selecione **ativada** como **Single Sign-On estado**.</span><span class="sxs-lookup"><span data-stu-id="6a149-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="6a149-180">c.</span><span class="sxs-lookup"><span data-stu-id="6a149-180">c.</span></span> <span data-ttu-id="6a149-181">No Olá **Id de entidade** caixa de texto, valor Olá colar **ID de entidade de SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a149-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6a149-182">d.</span><span class="sxs-lookup"><span data-stu-id="6a149-182">d.</span></span> <span data-ttu-id="6a149-183">No Olá **URL de página de início de sessão** caixa de texto, Olá colar **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a149-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6a149-184">e.</span><span class="sxs-lookup"><span data-stu-id="6a149-184">e.</span></span> <span data-ttu-id="6a149-185">No Olá **terminar o URL da página** caixa de texto, Olá colar **Sign-Out URL** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a149-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6a149-186">f.</span><span class="sxs-lookup"><span data-stu-id="6a149-186">f.</span></span> <span data-ttu-id="6a149-187">No **certificado do fornecedor de identidade**, clique em **Escolher ficheiro**e, em seguida, carregue o certificado de Olá que transferiu do Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a149-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="6a149-188">g.</span><span class="sxs-lookup"><span data-stu-id="6a149-188">g.</span></span> <span data-ttu-id="6a149-189">Clique em **guardar alterações**.</span><span class="sxs-lookup"><span data-stu-id="6a149-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="6a149-190">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="6a149-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6a149-191">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a149-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6a149-192">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a149-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a149-193">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a149-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a149-194">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a149-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="6a149-196">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6a149-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a149-197">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6a149-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a149-199">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="6a149-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a149-201">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="6a149-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a149-203">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6a149-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a149-205">a.</span><span class="sxs-lookup"><span data-stu-id="6a149-205">a.</span></span> <span data-ttu-id="6a149-206">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6a149-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a149-207">b.</span><span class="sxs-lookup"><span data-stu-id="6a149-207">b.</span></span> <span data-ttu-id="6a149-208">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6a149-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a149-209">c.</span><span class="sxs-lookup"><span data-stu-id="6a149-209">c.</span></span> <span data-ttu-id="6a149-210">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="6a149-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6a149-211">d.</span><span class="sxs-lookup"><span data-stu-id="6a149-211">d.</span></span> <span data-ttu-id="6a149-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6a149-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="6a149-213">Criar um utilizador de teste Syncplicity</span><span class="sxs-lookup"><span data-stu-id="6a149-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="6a149-214">Para o AAD utilizadores toobe capaz de toosign no, têm de ser aprovisionada tooSyncplicity aplicação.</span><span class="sxs-lookup"><span data-stu-id="6a149-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="6a149-215">Esta secção descreve como de contas de utilizador AAD toocreate Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6a149-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="6a149-216">**tooprovision um tooSyncplicity de conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6a149-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a149-217">Inicie sessão no tooyour **Syncplicity** inquilino (por exemplo: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="6a149-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="6a149-218">Clique em **admin** e selecione **contas de utilizador**.</span><span class="sxs-lookup"><span data-stu-id="6a149-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="6a149-219">Clique em **adicionar um utilizador**.</span><span class="sxs-lookup"><span data-stu-id="6a149-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="6a149-220">![Gerir utilizadores](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "gerir utilizadores")</span><span class="sxs-lookup"><span data-stu-id="6a149-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="6a149-221">Olá tipo **endereços de correio eletrónico** de uma conta do AAD pretende tooprovision, selecione **utilizador** como **função**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6a149-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="6a149-222">![Informações de conta](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "informações de conta")</span><span class="sxs-lookup"><span data-stu-id="6a149-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="6a149-223">titular da conta do Olá AAD obtém uma mensagem de e-mail, incluindo um tooconfirm de ligação e ativar a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a149-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="6a149-224">Selecione um grupo na sua empresa que o novo utilizador deve ser membro de e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6a149-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="6a149-225">![Associação ao grupo](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "associação ao grupo")</span><span class="sxs-lookup"><span data-stu-id="6a149-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="6a149-226">Se não existem não existem grupos listados, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6a149-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="6a149-227">Selecione as pastas de Olá teria como tooplace sob o controlo da Syncplicity no computador do utilizador Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="6a149-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="6a149-228">![Pastas de Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity pastas")</span><span class="sxs-lookup"><span data-stu-id="6a149-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="6a149-229">Pode utilizar quaisquer outras Syncplicity utilizador conta criação ferramentas ou APIs fornecidas pelo Syncplicity tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="6a149-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6a149-230">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a149-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6a149-231">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSyncplicity.</span><span class="sxs-lookup"><span data-stu-id="6a149-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="6a149-233">**tooassign Britta Simon tooSyncplicity, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6a149-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a149-234">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6a149-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="6a149-236">Na lista de aplicações de Olá, selecione **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="6a149-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="6a149-238">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6a149-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="6a149-240">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="6a149-240">Click **Add** button.</span></span> <span data-ttu-id="6a149-241">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a149-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="6a149-243">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="6a149-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6a149-244">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a149-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a149-245">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a149-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a149-246">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6a149-246">Testing single sign-on</span></span>

<span data-ttu-id="6a149-247">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="6a149-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6a149-248">Ao clicar em mosaico de Syncplicity Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Syncplicity aplicação.</span><span class="sxs-lookup"><span data-stu-id="6a149-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="6a149-249">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6a149-249">Additional resources</span></span>

* [<span data-ttu-id="6a149-250">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a149-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a149-251">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6a149-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

