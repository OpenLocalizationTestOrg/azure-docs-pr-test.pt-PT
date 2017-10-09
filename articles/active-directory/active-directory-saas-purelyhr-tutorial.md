---
title: "Tutorial: Integração do Azure Active Directory com PurelyHR | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: bdc1748ed650cff36b1ef7d7330dd2a17b3bc760
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="957d0-103">Tutorial: Integração do Azure Active Directory com PurelyHR</span><span class="sxs-lookup"><span data-stu-id="957d0-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="957d0-104">Neste tutorial, saiba como toointegrate PurelyHR com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="957d0-104">In this tutorial, you learn how toointegrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="957d0-105">Integrar PurelyHR com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="957d0-105">Integrating PurelyHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="957d0-106">Pode controlar no Azure AD que tenha acesso tooPurelyHR</span><span class="sxs-lookup"><span data-stu-id="957d0-106">You can control in Azure AD who has access tooPurelyHR</span></span>
- <span data-ttu-id="957d0-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPurelyHR (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="957d0-107">You can enable your users tooautomatically get signed-on tooPurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="957d0-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="957d0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="957d0-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="957d0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="957d0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="957d0-110">Prerequisites</span></span>

<span data-ttu-id="957d0-111">integração do Azure AD com PurelyHR tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="957d0-111">tooconfigure Azure AD integration with PurelyHR, you need hello following items:</span></span>

- <span data-ttu-id="957d0-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="957d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="957d0-113">Um PurelyHR início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="957d0-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="957d0-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="957d0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="957d0-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="957d0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="957d0-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="957d0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="957d0-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="957d0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="957d0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="957d0-118">Scenario description</span></span>
<span data-ttu-id="957d0-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="957d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="957d0-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="957d0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="957d0-121">Adicionar PurelyHR da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="957d0-121">Adding PurelyHR from hello gallery</span></span>
2. <span data-ttu-id="957d0-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="957d0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-hello-gallery"></a><span data-ttu-id="957d0-123">Adicionar PurelyHR da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="957d0-123">Adding PurelyHR from hello gallery</span></span>
<span data-ttu-id="957d0-124">tooconfigure Olá integração de PurelyHR com o Azure AD, é necessário tooadd PurelyHR Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="957d0-124">tooconfigure hello integration of PurelyHR into Azure AD, you need tooadd PurelyHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="957d0-125">**tooadd PurelyHR da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="957d0-125">**tooadd PurelyHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="957d0-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="957d0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="957d0-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="957d0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="957d0-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="957d0-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="957d0-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="957d0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="957d0-133">Na caixa de pesquisa de Olá, escreva **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="957d0-133">In hello search box, type **PurelyHR**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="957d0-135">No painel de resultados de Olá, selecione **PurelyHR**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="957d0-135">In hello results panel, select **PurelyHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="957d0-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="957d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="957d0-138">Nesta secção, configure e teste do Azure AD-início de sessão único com PurelyHR com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="957d0-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="957d0-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá PurelyHR é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="957d0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PurelyHR is tooa user in Azure AD.</span></span> <span data-ttu-id="957d0-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá PurelyHR tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="957d0-140">In other words, a link relationship between an Azure AD user and hello related user in PurelyHR needs toobe established.</span></span>

<span data-ttu-id="957d0-141">No PurelyHR, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="957d0-141">In PurelyHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="957d0-142">tooconfigure e teste do Azure AD-início de sessão único com PurelyHR, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="957d0-142">tooconfigure and test Azure AD single sign-on with PurelyHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="957d0-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="957d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="957d0-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="957d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="957d0-145">**[Criar um utilizador de teste PurelyHR](#creating-a-purelyhr-test-user)**  -toohave um homólogo de Britta Simon no PurelyHR é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="957d0-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - toohave a counterpart of Britta Simon in PurelyHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="957d0-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="957d0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="957d0-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="957d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="957d0-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="957d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="957d0-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="957d0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="957d0-150">**tooconfigure do Azure AD-início de sessão único com PurelyHR, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="957d0-150">**tooconfigure Azure AD single sign-on with PurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="957d0-151">No Olá portal do Azure, no Olá **PurelyHR** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="957d0-151">In hello Azure portal, on hello **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="957d0-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="957d0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="957d0-155">No Olá **PurelyHR domínio e os URLs** secção, execute os passos seguintes se quiser aplicação Olá tooconfigure de Olá **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="957d0-155">On hello **PurelyHR Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="957d0-157">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="957d0-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="957d0-158">Verifique **Mostrar avançadas definições de URL**, se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="957d0-158">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="957d0-160">No Olá **URL de início de sessão** caixa de texto, o valor do tipo Olá Olá seguir o padrão de utilização:`https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="957d0-160">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="957d0-161">Estes valores não estiverem Olá real.</span><span class="sxs-lookup"><span data-stu-id="957d0-161">These values are not hello real.</span></span> <span data-ttu-id="957d0-162">Atualize estes valores com o URL de resposta real Olá e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="957d0-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="957d0-163">Contacte [equipa de suporte de cliente PurelyHR](http://support.purelyhr.com/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="957d0-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) tooget these values.</span></span> 

5. <span data-ttu-id="957d0-164">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="957d0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="957d0-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="957d0-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="957d0-168">No Olá **PurelyHR configuração** secção, clique em **configurar PurelyHR** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="957d0-168">On hello **PurelyHR Configuration** section, click **Configure PurelyHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="957d0-169">Olá cópia **ID de entidade de SAML e único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="957d0-169">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="957d0-171">tooconfigure-início de sessão único em **PurelyHR** lado, o Web site tootheir de início de sessão como administrador.</span><span class="sxs-lookup"><span data-stu-id="957d0-171">tooconfigure single sign-on on **PurelyHR** side, login tootheir website as an administrator.</span></span>

9. <span data-ttu-id="957d0-172">Abra Olá **Dashboard** das opções de Olá na barra de ferramentas Olá e clique em **SSO definições**.</span><span class="sxs-lookup"><span data-stu-id="957d0-172">Open hello **Dashboard** from hello options in hello toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="957d0-173">Colar Olá valores nas caixas de Olá como descrito abaixo-</span><span class="sxs-lookup"><span data-stu-id="957d0-173">Paste hello values in hello boxes as described below-</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="957d0-175">a.</span><span class="sxs-lookup"><span data-stu-id="957d0-175">a.</span></span> <span data-ttu-id="957d0-176">Abra Olá **Certificate(Bas64)** transferido a partir de Olá portal do Azure no bloco de notas e copie-valor do certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="957d0-176">Open hello **Certificate(Bas64)** downloaded from hello Azure portal in notepad and copy hello certificate value.</span></span> <span data-ttu-id="957d0-177">Olá colar copiados valor para Olá **certificado x. 509** caixa.</span><span class="sxs-lookup"><span data-stu-id="957d0-177">Paste hello copied value into hello **X.509 Certificate** box.</span></span>

    <span data-ttu-id="957d0-178">b.</span><span class="sxs-lookup"><span data-stu-id="957d0-178">b.</span></span> <span data-ttu-id="957d0-179">No Olá **URL do emissor Idp** caixa, cole Olá **ID de entidade de SAML** copiados Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="957d0-179">In hello **Idp Issuer URL** box, paste hello **SAML Entity ID** copied from hello Azure portal.</span></span>

    <span data-ttu-id="957d0-180">c.</span><span class="sxs-lookup"><span data-stu-id="957d0-180">c.</span></span> <span data-ttu-id="957d0-181">No Olá **URL de ponto final do Idp** caixa, cole Olá **único início de sessão no URL do serviço SAML** copiados Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="957d0-181">In hello **Idp Endpoint URL** box, paste hello **SAML Single Sign-On Service URL** copied from hello Azure portal.</span></span> 

    <span data-ttu-id="957d0-182">d.</span><span class="sxs-lookup"><span data-stu-id="957d0-182">d.</span></span> <span data-ttu-id="957d0-183">Verifique Olá **Auto-criar utilizadores** caixa de verificação o aprovisionamento de utilizador automáticas de tooenable no PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="957d0-183">Check hello **Auto-Create Users** checkbox tooenable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="957d0-184">e.</span><span class="sxs-lookup"><span data-stu-id="957d0-184">e.</span></span> <span data-ttu-id="957d0-185">Clique em **guardar alterações** definições de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="957d0-185">Click **Save Changes** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="957d0-186">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="957d0-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="957d0-187">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="957d0-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="957d0-188">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="957d0-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="957d0-189">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="957d0-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="957d0-190">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="957d0-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="957d0-192">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="957d0-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="957d0-193">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="957d0-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="957d0-195">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="957d0-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="957d0-197">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="957d0-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="957d0-199">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="957d0-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="957d0-201">a.</span><span class="sxs-lookup"><span data-stu-id="957d0-201">a.</span></span> <span data-ttu-id="957d0-202">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="957d0-202">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="957d0-203">b.</span><span class="sxs-lookup"><span data-stu-id="957d0-203">b.</span></span> <span data-ttu-id="957d0-204">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="957d0-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="957d0-205">c.</span><span class="sxs-lookup"><span data-stu-id="957d0-205">c.</span></span> <span data-ttu-id="957d0-206">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="957d0-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="957d0-207">d.</span><span class="sxs-lookup"><span data-stu-id="957d0-207">d.</span></span> <span data-ttu-id="957d0-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="957d0-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="957d0-209">Criar um utilizador de teste PurelyHR</span><span class="sxs-lookup"><span data-stu-id="957d0-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="957d0-210">tooenable do Azure AD os utilizadores toolog no tooPurelyHR, estes têm de ser aprovisionados para PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="957d0-210">tooenable Azure AD users toolog in tooPurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="957d0-211">PurelyHR, o aprovisionamento é uma tarefa automática e não existem passos manuais são necessários quando o aprovisionamento de utilizadores automático está ativado.</span><span class="sxs-lookup"><span data-stu-id="957d0-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="957d0-212">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="957d0-212">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="957d0-213">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPurelyHR.</span><span class="sxs-lookup"><span data-stu-id="957d0-213">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPurelyHR.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="957d0-215">**tooassign Britta Simon tooPurelyHR, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="957d0-215">**tooassign Britta Simon tooPurelyHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="957d0-216">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="957d0-216">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="957d0-218">Na lista de aplicações de Olá, selecione **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="957d0-218">In hello applications list, select **PurelyHR**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="957d0-220">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="957d0-220">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="957d0-222">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="957d0-222">Click **Add** button.</span></span> <span data-ttu-id="957d0-223">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="957d0-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="957d0-225">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="957d0-225">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="957d0-226">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="957d0-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="957d0-227">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="957d0-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="957d0-228">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="957d0-228">Testing single sign-on</span></span>

<span data-ttu-id="957d0-229">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="957d0-229">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="957d0-230">Clique em Olá absorver LMS na peça de mosaico Olá painel de acesso, obter aplicações de absorver LMS tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="957d0-230">Click hello Absorb LMS tile in hello Access Panel, you get automatically signed-on tooyour Absorb LMS application.</span></span>

<span data-ttu-id="957d0-231">Para obter mais informações sobre Olá painel de acesso, consulte.</span><span class="sxs-lookup"><span data-stu-id="957d0-231">For more information about hello Access Panel, see.</span></span> <span data-ttu-id="957d0-232">[No painel de acesso do introdução toohello](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="957d0-232">[Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="957d0-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="957d0-233">Additional resources</span></span>

* [<span data-ttu-id="957d0-234">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="957d0-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="957d0-235">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="957d0-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

