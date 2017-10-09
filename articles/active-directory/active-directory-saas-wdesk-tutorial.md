---
title: "Tutorial: Integração do Azure Active Directory com Wdesk | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 2c278a5e4f50cc362663efc0f826ff0c0fcf6e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="a7dc4-103">Tutorial: Integração do Azure Active Directory com Wdesk</span><span class="sxs-lookup"><span data-stu-id="a7dc4-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="a7dc4-104">Neste tutorial, saiba como toointegrate Wdesk com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7dc4-104">In this tutorial, you learn how toointegrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7dc4-105">Integrar Wdesk com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-105">Integrating Wdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a7dc4-106">Pode controlar no Azure AD que tenha acesso tooWdesk</span><span class="sxs-lookup"><span data-stu-id="a7dc4-106">You can control in Azure AD who has access tooWdesk</span></span>
- <span data-ttu-id="a7dc4-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooWdesk (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7dc4-107">You can enable your users tooautomatically get signed-on tooWdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7dc4-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a7dc4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a7dc4-109">Se pretender que tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="a7dc4-110">[O que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7dc4-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7dc4-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a7dc4-111">Prerequisites</span></span>

<span data-ttu-id="a7dc4-112">integração do Azure AD com Wdesk tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-112">tooconfigure Azure AD integration with Wdesk, you need hello following items:</span></span>

- <span data-ttu-id="a7dc4-113">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7dc4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a7dc4-114">Um Wdesk início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="a7dc4-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7dc4-115">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7dc4-116">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7dc4-117">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7dc4-118">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7dc4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7dc4-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a7dc4-119">Scenario description</span></span>
<span data-ttu-id="a7dc4-120">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7dc4-121">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7dc4-122">Adicionar Wdesk da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a7dc4-122">Adding Wdesk from hello gallery</span></span>
2. <span data-ttu-id="a7dc4-123">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a7dc4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-hello-gallery"></a><span data-ttu-id="a7dc4-124">Adicionar Wdesk da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a7dc4-124">Adding Wdesk from hello gallery</span></span>
<span data-ttu-id="a7dc4-125">tooconfigure Olá integração de Wdesk com o Azure AD, é necessário tooadd Wdesk Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-125">tooconfigure hello integration of Wdesk into Azure AD, you need tooadd Wdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a7dc4-126">**tooadd Wdesk da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dc4-126">**tooadd Wdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dc4-127">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7dc4-129">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a7dc4-130">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-130">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="a7dc4-132">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="a7dc4-134">Na caixa de pesquisa de Olá, escreva **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-134">In hello search box, type **Wdesk**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="a7dc4-136">No painel de resultados de Olá, selecione **Wdesk**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-136">In hello results panel, select **Wdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7dc4-138">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a7dc4-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7dc4-139">Nesta secção, configure e teste do Azure AD-início de sessão único com Wdesk com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a7dc4-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a7dc4-140">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Wdesk é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Wdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="a7dc4-141">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Wdesk tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-141">In other words, a link relationship between an Azure AD user and hello related user in Wdesk needs toobe established.</span></span>

<span data-ttu-id="a7dc4-142">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Wdesk.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wdesk.</span></span>

<span data-ttu-id="a7dc4-143">tooconfigure e teste do Azure AD-início de sessão único com Wdesk, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-143">tooconfigure and test Azure AD single sign-on with Wdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a7dc4-144">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a7dc4-145">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7dc4-146">**[Criar um utilizador de teste Wdesk](#creating-a-wdesk-test-user)**  -toohave um homólogo de Britta Simon no Wdesk é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - toohave a counterpart of Britta Simon in Wdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7dc4-147">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7dc4-148">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7dc4-149">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a7dc4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7dc4-150">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Wdesk.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="a7dc4-151">**tooconfigure do Azure AD-início de sessão único com Wdesk, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dc4-151">**tooconfigure Azure AD single sign-on with Wdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dc4-152">No Olá portal do Azure, no Olá **Wdesk** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-152">In hello Azure portal, on hello **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="a7dc4-154">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="a7dc4-156">No Olá **Wdesk domínio e os URLs** secção, se desejar aplicação Olá tooconfigure **IDP** modo iniciado efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-156">On hello **Wdesk Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="a7dc4-158">a.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-158">a.</span></span> <span data-ttu-id="a7dc4-159">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="a7dc4-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="a7dc4-160">b.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-160">b.</span></span> <span data-ttu-id="a7dc4-161">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="a7dc4-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="a7dc4-162">Verifique **Mostrar avançadas definições de URL**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a7dc4-163">Se desejar aplicação Olá tooconfigure **SP** iniciada modo, efetuar Olá passo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-163">If you wish tooconfigure hello application in **SP** initiated mode, perform hello following step:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="a7dc4-165">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="a7dc4-165">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a7dc4-166">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-166">These values are not real.</span></span> <span data-ttu-id="a7dc4-167">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="a7dc4-168">Pode obter estes valores do portal de WDesk quando configurar Olá SSO.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-168">You get these values from WDesk portal when you configure hello SSO.</span></span> 
  
5. <span data-ttu-id="a7dc4-169">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="a7dc4-171">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-171">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="a7dc4-173">Numa janela do browser web diferente, tooWdesk de início de sessão como um administrador de segurança.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-173">In a different web browser window, login tooWdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="a7dc4-174">No Olá parte inferior esquerda, clique em **Admin** e escolha **administrador da conta**:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-174">In hello bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="a7dc4-176">No Wdesk administrador, navegue demasiado**segurança**, em seguida, **SAML** > **SAML definições**:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-176">In Wdesk Admin, navigate too**Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="a7dc4-178">Em **definições gerais**, verifique Olá **ativar SAML início de sessão único**:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-178">Under **General Settings**, check hello **Enable SAML Single Sign On**:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="a7dc4-180">Em **os detalhes do fornecedor de serviço**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-180">Under **Service Provider Details**, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="a7dc4-182">a.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-182">a.</span></span> <span data-ttu-id="a7dc4-183">Olá cópia **URL de início de sessão** e cole-a no **Url de início de sessão** caixa de texto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-183">Copy hello **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="a7dc4-184">b.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-184">b.</span></span> <span data-ttu-id="a7dc4-185">Olá cópia **Url de metadados** e cole-a no **identificador** caixa de texto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-185">Copy hello **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="a7dc4-186">c.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-186">c.</span></span> <span data-ttu-id="a7dc4-187">Olá cópia **url de consumidor** e cole-a no **Url de resposta** caixa de texto no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-187">Copy hello **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="a7dc4-188">d.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-188">d.</span></span> <span data-ttu-id="a7dc4-189">Clique em **guardar** nas alterações de Olá toosave portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-189">Click **Save** on Azure portal toosave hello changes.</span></span>      

12. <span data-ttu-id="a7dc4-190">Clique em **configurar definições de IdP** tooopen **editar definições de IdP** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-190">Click **Configure IdP Settings** tooopen **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="a7dc4-191">Clique em **Escolher ficheiro** toolocate Olá **Metadata.xml** ficheiro guardado no portal do Azure, em seguida, carregue-o.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-191">Click **Choose File** toolocate hello **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="a7dc4-193">Clique em **guardar alterações**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-193">Click **Save changes**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="a7dc4-195">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="a7dc4-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a7dc4-196">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a7dc4-197">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7dc4-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7dc4-198">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7dc4-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7dc4-199">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="a7dc4-201">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dc4-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dc4-202">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7dc4-204">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7dc4-206">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-206">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7dc4-208">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7dc4-210">a.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-210">a.</span></span> <span data-ttu-id="a7dc4-211">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7dc4-212">b.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-212">b.</span></span> <span data-ttu-id="a7dc4-213">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7dc4-214">c.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-214">c.</span></span> <span data-ttu-id="a7dc4-215">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a7dc4-216">d.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-216">d.</span></span> <span data-ttu-id="a7dc4-217">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="a7dc4-218">Criar um utilizador de teste Wdesk</span><span class="sxs-lookup"><span data-stu-id="a7dc4-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="a7dc4-219">tooenable do Azure AD os utilizadores toolog no tooWdesk, estes têm de ser aprovisionados para Wdesk.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-219">tooenable Azure AD users toolog in tooWdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="a7dc4-220">No Wdesk, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="a7dc4-221">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dc4-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dc4-222">Inicie sessão no tooWdesk como um administrador de segurança.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-222">Log in tooWdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="a7dc4-223">Navegue demasiado**Admin** > **administrador da conta**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-223">Navigate too**Admin** > **Account Admin**.</span></span>

     ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="a7dc4-225">Clique em **membros** em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="a7dc4-226">Agora, clique em **Add Member** tooopen **Add Member** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-226">Now click **Add Member** tooopen **Add Member** dialog box.</span></span> 
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="a7dc4-228">No **utilizador** texto, introduza o nome de utilizador de Olá do utilizador, como  **brittasimon@contoso.com**  e clique em **continuar** botão.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-228">In **User** text box, enter hello username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="a7dc4-230">Introduza os detalhes de Olá, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="a7dc4-230">Enter hello details as shown below:</span></span>
  
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="a7dc4-232">a.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-232">a.</span></span> <span data-ttu-id="a7dc4-233">No **correio electrónico** texto, introduza o e-mail de Olá do utilizador, como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a7dc4-233">In **E-mail** text box, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="a7dc4-234">b.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-234">b.</span></span> <span data-ttu-id="a7dc4-235">No **nome próprio** texto, introduza Olá primeiro nome de utilizador como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-235">In **First Name** text box, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="a7dc4-236">c.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-236">c.</span></span> <span data-ttu-id="a7dc4-237">No **Apelido** texto, introduza o apelido Olá do utilizador, como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-237">In **Last Name** text box, enter hello last name of user like **Simon**.</span></span>

7. <span data-ttu-id="a7dc4-238">Clique em **guardar membro** botão.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-238">Click **Save Member** button.</span></span>  

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a7dc4-240">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7dc4-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a7dc4-241">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooWdesk.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWdesk.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="a7dc4-243">**tooassign Britta Simon tooWdesk, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dc4-243">**tooassign Britta Simon tooWdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dc4-244">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="a7dc4-246">Na lista de aplicações de Olá, selecione **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-246">In hello applications list, select **Wdesk**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="a7dc4-248">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="a7dc4-250">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-250">Click **Add** button.</span></span> <span data-ttu-id="a7dc4-251">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="a7dc4-253">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a7dc4-254">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7dc4-255">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7dc4-256">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a7dc4-256">Testing single sign-on</span></span>

<span data-ttu-id="a7dc4-257">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-257">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a7dc4-258">Ao clicar em mosaico de Wdesk Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Wdesk aplicação.</span><span class="sxs-lookup"><span data-stu-id="a7dc4-258">When you click hello Wdesk tile in hello Access Panel, you should get automatically signed-on tooyour Wdesk application.</span></span>
<span data-ttu-id="a7dc4-259">Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a7dc4-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a7dc4-260">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a7dc4-260">Additional resources</span></span>

* [<span data-ttu-id="a7dc4-261">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7dc4-261">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7dc4-262">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7dc4-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

