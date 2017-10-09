---
title: "Tutorial: Integração do Azure Active Directory Atlassian nuvem | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Atlassian nuvem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="4039b-103">Tutorial: Integração do Azure Active Directory Atlassian nuvem</span><span class="sxs-lookup"><span data-stu-id="4039b-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="4039b-104">Neste tutorial, saiba como toointegrate Atlassian na nuvem com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4039b-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4039b-105">Integrar Atlassian Cloud com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="4039b-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4039b-106">Pode controlar no Azure AD que tenha acesso tooAtlassian na nuvem</span><span class="sxs-lookup"><span data-stu-id="4039b-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="4039b-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooAtlassian Cloud (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4039b-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4039b-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4039b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4039b-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4039b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4039b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4039b-110">Prerequisites</span></span>

<span data-ttu-id="4039b-111">integração do Azure AD com Atlassian nuvem tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4039b-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="4039b-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4039b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4039b-113">Uma nuvem Atlassian-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="4039b-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4039b-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4039b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4039b-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4039b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4039b-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4039b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4039b-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui: [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4039b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4039b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4039b-118">Scenario description</span></span>
<span data-ttu-id="4039b-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4039b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4039b-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="4039b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4039b-121">A adição de nuvem Atlassian de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="4039b-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="4039b-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="4039b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="4039b-123">A adição de nuvem Atlassian de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="4039b-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="4039b-124">tooconfigure Olá integração Atlassian nuvem com o Azure AD, é necessário tooadd Atlassian nuvem Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="4039b-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4039b-125">**tooadd Atlassian da nuvem da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4039b-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4039b-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="4039b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4039b-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4039b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4039b-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="4039b-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="4039b-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4039b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="4039b-133">Na caixa de pesquisa de Olá, escreva **Atlassian nuvem**.</span><span class="sxs-lookup"><span data-stu-id="4039b-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="4039b-135">No painel de resultados de Olá, selecione **Atlassian nuvem**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="4039b-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4039b-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="4039b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4039b-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Atlassian nuvem com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4039b-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4039b-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na nuvem Atlassian é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4039b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="4039b-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na nuvem Atlassian tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4039b-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="4039b-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** na nuvem Atlassian.</span><span class="sxs-lookup"><span data-stu-id="4039b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="4039b-142">tooconfigure e teste do Azure AD-início de sessão único com Atlassian nuvem, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4039b-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4039b-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="4039b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4039b-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4039b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4039b-145">**[Criar um utilizador de teste de nuvem Atlassian](#creating-an-atlassian-cloud-test-user)**  -toohave um homólogo de Britta Simon na nuvem Atlassian que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="4039b-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4039b-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="4039b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4039b-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="4039b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4039b-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="4039b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4039b-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de nuvem Atlassian.</span><span class="sxs-lookup"><span data-stu-id="4039b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="4039b-150">**tooconfigure do Azure AD-início de sessão único com Atlassian nuvem, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4039b-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="4039b-151">No Olá portal do Azure, no Olá **Atlassian nuvem** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="4039b-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="4039b-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="4039b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="4039b-155">No Olá **Atlassian nuvem domínio e os URLs** secção, execute os passos seguintes se quiser aplicação Olá tooconfigure de Olá **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="4039b-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="4039b-157">a.</span><span class="sxs-lookup"><span data-stu-id="4039b-157">a.</span></span> <span data-ttu-id="4039b-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="4039b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="4039b-159">b.</span><span class="sxs-lookup"><span data-stu-id="4039b-159">b.</span></span> <span data-ttu-id="4039b-160">No Olá **URL de resposta** caixa de texto, escreva um URL como:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="4039b-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="4039b-161">Verifique **Mostrar avançadas definições de URL** e efetuar Olá seguir passo se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="4039b-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="4039b-163">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="4039b-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4039b-164">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="4039b-164">These values are not real.</span></span> <span data-ttu-id="4039b-165">Atualizar estes valores com Olá real identificador e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="4039b-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="4039b-166">Pode obter valores exato Olá a partir do ecrã de configuração de SAML do Atlassian na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4039b-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="4039b-167">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="4039b-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="4039b-169">No Olá **configuração da nuvem Atlassian** secção, clique em **configurar a nuvem de Atlassian** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="4039b-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4039b-170">Olá cópia **ID de entidade de SAML e único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4039b-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="4039b-172">tooget SSO configurado para a sua aplicação, o início de sessão toohello Portal Atlassian com direitos de administrador Olá.</span><span class="sxs-lookup"><span data-stu-id="4039b-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="4039b-173">Na secção autenticação Olá Olá deixado navegação clique **domínios**.</span><span class="sxs-lookup"><span data-stu-id="4039b-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="4039b-175">a.</span><span class="sxs-lookup"><span data-stu-id="4039b-175">a.</span></span> <span data-ttu-id="4039b-176">Na caixa de texto Olá, escreva o seu nome de domínio e, em seguida, clique em **Adicionar domínio**.</span><span class="sxs-lookup"><span data-stu-id="4039b-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="4039b-178">b.</span><span class="sxs-lookup"><span data-stu-id="4039b-178">b.</span></span> <span data-ttu-id="4039b-179">domínio de Olá tooverify, clique em **verifique**.</span><span class="sxs-lookup"><span data-stu-id="4039b-179">tooverify hello domain, click **Verify**.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="4039b-181">c.</span><span class="sxs-lookup"><span data-stu-id="4039b-181">c.</span></span> <span data-ttu-id="4039b-182">Transferir o ficheiro de html de verificação de domínio Olá, carregá-la toohello a pasta raiz do Web site do seu domínio e, em seguida, clique em **verificar domínio**.</span><span class="sxs-lookup"><span data-stu-id="4039b-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="4039b-184">d.</span><span class="sxs-lookup"><span data-stu-id="4039b-184">d.</span></span> <span data-ttu-id="4039b-185">Depois de verificar o domínio de Olá, Olá valor Olá **estado** campo é **Verified**.</span><span class="sxs-lookup"><span data-stu-id="4039b-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="4039b-187">Na barra de navegação esquerdo Olá, clique em **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4039b-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="4039b-189">Criar uma configuração de SAML e adicionar a configuração do fornecedor de identidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="4039b-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="4039b-191">a.</span><span class="sxs-lookup"><span data-stu-id="4039b-191">a.</span></span> <span data-ttu-id="4039b-192">No Olá **fornecedor de identidade ID de entidade** caixa de texto, colar Olá valor **ID de entidade de SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4039b-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4039b-193">b.</span><span class="sxs-lookup"><span data-stu-id="4039b-193">b.</span></span> <span data-ttu-id="4039b-194">No Olá **fornecedor de identidade SSO URL** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4039b-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="4039b-195">c.</span><span class="sxs-lookup"><span data-stu-id="4039b-195">c.</span></span> <span data-ttu-id="4039b-196">Abra o certificado de Olá transferido do Azure portal cópia Olá valores e sem Olá Begin e linhas de fim e colá-lo na Olá **X509 pública certificado** caixa.</span><span class="sxs-lookup"><span data-stu-id="4039b-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="4039b-197">d.</span><span class="sxs-lookup"><span data-stu-id="4039b-197">d.</span></span> <span data-ttu-id="4039b-198">Clique em **Guardar configuração** definições de Olá tooSave.</span><span class="sxs-lookup"><span data-stu-id="4039b-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="4039b-199">Atualize Olá do Azure AD definições toomake se de que tem de corrigir o URL de identificador de Olá de configuração.</span><span class="sxs-lookup"><span data-stu-id="4039b-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="4039b-200">a.</span><span class="sxs-lookup"><span data-stu-id="4039b-200">a.</span></span> <span data-ttu-id="4039b-201">Olá cópia **SP identidade ID** de Olá SAML ecrã e cole-o no Azure AD como Olá **identificador** valor.</span><span class="sxs-lookup"><span data-stu-id="4039b-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="4039b-202">b.</span><span class="sxs-lookup"><span data-stu-id="4039b-202">b.</span></span> <span data-ttu-id="4039b-203">URL de início de sessão é Olá URL de inquilino da sua nuvem Atlassian.</span><span class="sxs-lookup"><span data-stu-id="4039b-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="4039b-205">No portal do Azure Olá, clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="4039b-205">In hello Azure portal, Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="4039b-207">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="4039b-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4039b-208">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="4039b-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4039b-209">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4039b-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4039b-210">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4039b-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="4039b-211">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4039b-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="4039b-213">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4039b-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4039b-214">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="4039b-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4039b-216">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="4039b-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4039b-218">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="4039b-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4039b-220">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="4039b-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4039b-222">a.</span><span class="sxs-lookup"><span data-stu-id="4039b-222">a.</span></span> <span data-ttu-id="4039b-223">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4039b-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4039b-224">b.</span><span class="sxs-lookup"><span data-stu-id="4039b-224">b.</span></span> <span data-ttu-id="4039b-225">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4039b-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4039b-226">c.</span><span class="sxs-lookup"><span data-stu-id="4039b-226">c.</span></span> <span data-ttu-id="4039b-227">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="4039b-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4039b-228">d.</span><span class="sxs-lookup"><span data-stu-id="4039b-228">d.</span></span> <span data-ttu-id="4039b-229">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4039b-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="4039b-230">Criar um utilizador de teste Atlassian nuvem</span><span class="sxs-lookup"><span data-stu-id="4039b-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="4039b-231">tooenable do Azure AD os utilizadores toolog no tooAtlassian na nuvem, estes têm de ser aprovisionados para Atlassian nuvem.</span><span class="sxs-lookup"><span data-stu-id="4039b-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="4039b-232">Em caso de Atlassian nuvem, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4039b-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="4039b-233">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4039b-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4039b-234">Na secção de administração de sites Olá, clique em Olá **utilizadores** botão</span><span class="sxs-lookup"><span data-stu-id="4039b-234">In hello Site administration section, click hello **Users** button</span></span>

    ![Criar utilizador de nuvem Atlassian](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="4039b-236">Clique em Olá **criar utilizador** botão toocreate um utilizador no Olá Atlassian nuvem</span><span class="sxs-lookup"><span data-stu-id="4039b-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![Criar utilizador de nuvem Atlassian](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="4039b-238">Introduza o utilizador Olá **endereço de correio eletrónico**, **Username**, e **nome completo** e atribuir acesso de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="4039b-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![Criar utilizador de nuvem Atlassian](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="4039b-240">Clique em **criar utilizador** botão, irá enviar utilizador de toohello de convite de correio eletrónico Olá e após a aceitação de utilizador do Olá convite Olá estará ativo no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="4039b-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="4039b-241">Também pode criar Olá utilizadores em volume ao clicar em Olá **em massa criar** botão no Olá seção de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="4039b-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4039b-242">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4039b-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4039b-243">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooAtlassian na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4039b-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="4039b-245">**tooassign Britta Simon tooAtlassian nuvem, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4039b-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="4039b-246">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="4039b-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="4039b-248">Na lista de aplicações de Olá, selecione **Atlassian nuvem**.</span><span class="sxs-lookup"><span data-stu-id="4039b-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="4039b-250">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4039b-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="4039b-252">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="4039b-252">Click **Add** button.</span></span> <span data-ttu-id="4039b-253">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4039b-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="4039b-255">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="4039b-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4039b-256">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4039b-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4039b-257">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4039b-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4039b-258">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="4039b-258">Testing single sign-on</span></span>

<span data-ttu-id="4039b-259">Nesta secção, testar a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="4039b-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4039b-260">Ao clicar Olá Atlassian Cloud na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação Atlassian nuvem.</span><span class="sxs-lookup"><span data-stu-id="4039b-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="4039b-261">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4039b-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4039b-262">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4039b-262">Additional resources</span></span>

* [<span data-ttu-id="4039b-263">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4039b-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4039b-264">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4039b-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

