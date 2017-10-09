---
title: "Tutorial: Integração do Azure Active Directory com o Google Apps no Azure | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="2a81d-103">Tutorial: Integração do Azure Active Directory com o Google Apps</span><span class="sxs-lookup"><span data-stu-id="2a81d-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="2a81d-104">Neste tutorial, saiba como toointegrate Google Apps com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2a81d-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2a81d-105">Integrar o Google Apps com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="2a81d-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2a81d-106">Pode controlar no Azure AD que tenha acesso tooGoogle aplicações</span><span class="sxs-lookup"><span data-stu-id="2a81d-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="2a81d-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooGoogle aplicações (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a81d-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2a81d-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2a81d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2a81d-109">Se pretender tooknow mais informações sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2a81d-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a81d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2a81d-110">Prerequisites</span></span>

<span data-ttu-id="2a81d-111">tooconfigure integração do Azure AD com o Google Apps, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2a81d-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="2a81d-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a81d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2a81d-113">Um Google Apps-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="2a81d-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2a81d-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="2a81d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2a81d-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="2a81d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2a81d-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="2a81d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2a81d-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a81d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="2a81d-118">Tutorial de vídeo</span><span class="sxs-lookup"><span data-stu-id="2a81d-118">Video tutorial</span></span>
<span data-ttu-id="2a81d-119">Como tooEnable Single Sign-On tooGoogle aplicações em 2 minutos:</span><span class="sxs-lookup"><span data-stu-id="2a81d-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="2a81d-120">Perguntas Mais Frequentes</span><span class="sxs-lookup"><span data-stu-id="2a81d-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="2a81d-121">**P: são Chromebooks e outros dispositivos Chrome compatíveis com o Azure AD-início de sessão único?**</span><span class="sxs-lookup"><span data-stu-id="2a81d-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="2a81d-122">R: Sim, os utilizadores são capaz toosign para os respetivos dispositivos Chromebook utilizando as credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a81d-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="2a81d-123">Consulte este [Google Apps suporta artigo](https://support.google.com/chrome/a/answer/6060880) para obter informações sobre o motivo os utilizadores podem obter pedidos as credenciais duas vezes.</span><span class="sxs-lookup"><span data-stu-id="2a81d-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="2a81d-124">**P: Se ativar a início de sessão único, irão os utilizadores ser capaz toouse os respetivos toosign de credenciais do Azure AD para qualquer produto da Google, tais como o Google sala de aula, GMail, Google Drive, YouTube e assim sucessivamente?**</span><span class="sxs-lookup"><span data-stu-id="2a81d-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="2a81d-125">R: Sim, dependendo da [que aplicações da Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) escolha tooenable ou desativar para a sua organização.</span><span class="sxs-lookup"><span data-stu-id="2a81d-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="2a81d-126">**P: posso ativar início de sessão para apenas um subconjunto de utilizadores Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="2a81d-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="2a81d-127">R: não, ativar o início de sessão único imediatamente requer que todos os utilizadores Google Apps tooauthenticate com as respetivas credenciais do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a81d-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="2a81d-128">Porque o Google Apps não suporta a ter vários fornecedores de identidade, fornecedor de identidade Olá para o seu ambiente do Google Apps pode ser do Azure AD ou Google - mas não ambos em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="2a81d-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="2a81d-129">**P: se um utilizador é iniciada no através do Windows, são que automaticamente se autenticar tooGoogle aplicações sem obter um pedido de uma palavra-passe?**</span><span class="sxs-lookup"><span data-stu-id="2a81d-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="2a81d-130">R: Existem duas opções para ativar este cenário.</span><span class="sxs-lookup"><span data-stu-id="2a81d-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="2a81d-131">Em primeiro lugar, os utilizadores foi inicie sessão em dispositivos Windows 10 através de [associação do Azure Active Directory](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a81d-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="2a81d-132">Em alternativa, os utilizadores foi inicie sessão em dispositivos Windows que estão associados a um domínio tooan no local do Active Directory que foi ativada para único início de sessão tooAzure AD através de um [serviços de Federação do Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) implementação.</span><span class="sxs-lookup"><span data-stu-id="2a81d-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="2a81d-133">Ambas as opções necessitam passos Olá tooperform Olá seguir tutorial tooenable-início de sessão único entre o Azure AD e o Google Apps.</span><span class="sxs-lookup"><span data-stu-id="2a81d-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2a81d-134">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="2a81d-134">Scenario description</span></span>
<span data-ttu-id="2a81d-135">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="2a81d-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2a81d-136">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="2a81d-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2a81d-137">Adicionar Google Apps a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="2a81d-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="2a81d-138">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="2a81d-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="2a81d-139">Adicionar Google Apps a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="2a81d-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="2a81d-140">tooconfigure Olá integração do Google Apps com o Azure AD, é necessário tooadd Google Apps Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="2a81d-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2a81d-141">**tooadd Google Apps a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="2a81d-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a81d-142">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="2a81d-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2a81d-144">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2a81d-145">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-145">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="2a81d-147">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a81d-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="2a81d-149">Na caixa de pesquisa de Olá, escreva **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-149">In hello search box, type **Google Apps**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="2a81d-151">No painel de resultados de Olá, selecione **Google Apps**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="2a81d-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2a81d-153">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="2a81d-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2a81d-154">Nesta secção, configure e teste do Azure AD-início de sessão único com o Google Apps, com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2a81d-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2a81d-155">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Google Apps é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a81d-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="2a81d-156">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no Google Apps tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2a81d-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="2a81d-157">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Google Apps.</span><span class="sxs-lookup"><span data-stu-id="2a81d-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="2a81d-158">tooconfigure e teste do Azure AD-início de sessão único com o Google Apps, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2a81d-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2a81d-159">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="2a81d-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2a81d-160">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2a81d-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2a81d-161">**[Criar um utilizador de teste do Google Apps](#creating-a-google-apps-test-user)**  -toohave um homólogo de Britta Simon no Google Apps, que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="2a81d-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2a81d-162">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="2a81d-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2a81d-163">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="2a81d-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2a81d-164">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="2a81d-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2a81d-165">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação do Google Apps.</span><span class="sxs-lookup"><span data-stu-id="2a81d-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="2a81d-166">**tooconfigure do Azure AD-início de sessão único com o Google Apps, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="2a81d-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a81d-167">No Olá portal do Azure, no Olá **Google Apps** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="2a81d-169">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="2a81d-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="2a81d-171">No Olá **domínio de aplicações do Google e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2a81d-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="2a81d-173">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="2a81d-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2a81d-174">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="2a81d-174">This value is not real.</span></span> <span data-ttu-id="2a81d-175">Atualize o valor de Olá com Olá real URL Sign-on.</span><span class="sxs-lookup"><span data-stu-id="2a81d-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="2a81d-176">Contacte Olá [equipa de suporte do Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="2a81d-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="2a81d-177">No Olá **certificado de assinatura de SAML** secção, clique em **certificado** e, em seguida, guarde o certificado de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="2a81d-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="2a81d-179">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="2a81d-179">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2a81d-181">No Olá **configuração de aplicações do Google** secção, clique em **configurar o Google Apps** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="2a81d-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2a81d-182">Olá cópia **Sign-Out URL, único início de sessão no URL do serviço SAML e alteração URL de palavra-passe** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="2a81d-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="2a81d-184">Abra um novo separador no seu browser e inicie sessão no Olá [consola de administração de aplicações do Google](http://admin.google.com/) utilizando a sua conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="2a81d-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="2a81d-185">Clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-185">Click **Security**.</span></span> <span data-ttu-id="2a81d-186">Se não vir ligação Olá, pode estar ocultado em Olá **mais controlos** menu na parte inferior de Olá do ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a81d-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Clique em Security.][10]

9. <span data-ttu-id="2a81d-188">No Olá **segurança** página, clique em **configurar início de sessão único (SSO).**</span><span class="sxs-lookup"><span data-stu-id="2a81d-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Clique em SSO.][11]

10. <span data-ttu-id="2a81d-190">Execute Olá seguintes alterações de configuração:</span><span class="sxs-lookup"><span data-stu-id="2a81d-190">Perform hello following configuration changes:</span></span>
   
    ![Configurar o SSO][12]
   
    <span data-ttu-id="2a81d-192">a.</span><span class="sxs-lookup"><span data-stu-id="2a81d-192">a.</span></span> <span data-ttu-id="2a81d-193">Selecione **SSO de configuração com o fornecedor de identidade de terceiros**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="2a81d-194">b.</span><span class="sxs-lookup"><span data-stu-id="2a81d-194">b.</span></span> <span data-ttu-id="2a81d-195">No **URL de página de início de sessão** campo no Google Apps, cole o valor Olá **URL Single Sign-On serviço**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a81d-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2a81d-196">c.</span><span class="sxs-lookup"><span data-stu-id="2a81d-196">c.</span></span> <span data-ttu-id="2a81d-197">No Olá **URL da página de início de sessão** campo no Google Apps, cole o valor Olá **Sign-Out URL**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a81d-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="2a81d-198">d.</span><span class="sxs-lookup"><span data-stu-id="2a81d-198">d.</span></span> <span data-ttu-id="2a81d-199">No Olá **alterar palavra-passe URL** campo no Google Apps, cole o valor Olá **alterar palavra-passe URL**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a81d-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="2a81d-200">e.</span><span class="sxs-lookup"><span data-stu-id="2a81d-200">e.</span></span> <span data-ttu-id="2a81d-201">No Google Apps, para Olá **certificado de verificação**, certificado de Olá de carregamento do que transferiu a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a81d-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="2a81d-202">f.</span><span class="sxs-lookup"><span data-stu-id="2a81d-202">f.</span></span> <span data-ttu-id="2a81d-203">Clique em **guardar alterações**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2a81d-204">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="2a81d-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2a81d-205">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a81d-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2a81d-206">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2a81d-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2a81d-207">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a81d-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="2a81d-208">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a81d-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="2a81d-210">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="2a81d-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a81d-211">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="2a81d-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2a81d-213">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2a81d-215">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="2a81d-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2a81d-217">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2a81d-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2a81d-219">a.</span><span class="sxs-lookup"><span data-stu-id="2a81d-219">a.</span></span> <span data-ttu-id="2a81d-220">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2a81d-221">b.</span><span class="sxs-lookup"><span data-stu-id="2a81d-221">b.</span></span> <span data-ttu-id="2a81d-222">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2a81d-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2a81d-223">c.</span><span class="sxs-lookup"><span data-stu-id="2a81d-223">c.</span></span> <span data-ttu-id="2a81d-224">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2a81d-225">d.</span><span class="sxs-lookup"><span data-stu-id="2a81d-225">d.</span></span> <span data-ttu-id="2a81d-226">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="2a81d-227">Criar um utilizador de teste do Google Apps</span><span class="sxs-lookup"><span data-stu-id="2a81d-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="2a81d-228">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon no Software de aplicações do Google.</span><span class="sxs-lookup"><span data-stu-id="2a81d-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="2a81d-229">Google Apps suporta o aprovisionamento automático, que é por predefinição ativada.</span><span class="sxs-lookup"><span data-stu-id="2a81d-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="2a81d-230">Não há nenhuma ação por si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="2a81d-230">There is no action for you in this section.</span></span> <span data-ttu-id="2a81d-231">Se um utilizador já não existe no Software de aplicações do Google, uma nova é criada quando tenta tooaccess Software de aplicações do Google.</span><span class="sxs-lookup"><span data-stu-id="2a81d-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="2a81d-232">Se precisar de um utilizador de toocreate manualmente, contacte Olá [equipa de suporte do Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="2a81d-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2a81d-233">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2a81d-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2a81d-234">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooGoogle aplicações.</span><span class="sxs-lookup"><span data-stu-id="2a81d-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="2a81d-236">**tooassign Britta Simon tooGoogle aplicações, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="2a81d-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="2a81d-237">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="2a81d-239">Na lista de aplicações de Olá, selecione **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-239">In hello applications list, select **Google Apps**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="2a81d-241">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="2a81d-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="2a81d-243">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="2a81d-243">Click **Add** button.</span></span> <span data-ttu-id="2a81d-244">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a81d-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="2a81d-246">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="2a81d-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2a81d-247">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a81d-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2a81d-248">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2a81d-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2a81d-249">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="2a81d-249">Testing single sign-on</span></span>

<span data-ttu-id="2a81d-250">Nesta secção, tootest Olá, as único início de sessão definições, abra o painel de acesso em [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), em seguida, iniciar sessão na conta de teste de Olá e, em **Google Apps** mosaico no painel de acesso de Olá.</span><span class="sxs-lookup"><span data-stu-id="2a81d-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2a81d-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2a81d-251">Additional resources</span></span>

* [<span data-ttu-id="2a81d-252">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a81d-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2a81d-253">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2a81d-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2a81d-254">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="2a81d-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png