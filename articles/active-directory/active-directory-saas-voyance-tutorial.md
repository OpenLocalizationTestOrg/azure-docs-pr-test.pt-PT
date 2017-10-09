---
title: "Tutorial: Integração do Azure Active Directory com Voyance | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="c52b0-103">Tutorial: Integração do Azure Active Directory com Voyance</span><span class="sxs-lookup"><span data-stu-id="c52b0-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="c52b0-104">Neste tutorial, saiba como toointegrate Voyance com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c52b0-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c52b0-105">Integrar Voyance com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="c52b0-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c52b0-106">Pode controlar no Azure AD que tenha acesso tooVoyance</span><span class="sxs-lookup"><span data-stu-id="c52b0-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="c52b0-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooVoyance (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c52b0-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c52b0-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c52b0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c52b0-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c52b0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c52b0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c52b0-110">Prerequisites</span></span>

<span data-ttu-id="c52b0-111">integração do Azure AD com Voyance tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c52b0-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="c52b0-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c52b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c52b0-113">Um Voyance-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="c52b0-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c52b0-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c52b0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c52b0-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c52b0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c52b0-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c52b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c52b0-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c52b0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c52b0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c52b0-118">Scenario description</span></span>
<span data-ttu-id="c52b0-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c52b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c52b0-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="c52b0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c52b0-121">Adicionar Voyance da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="c52b0-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="c52b0-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="c52b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="c52b0-123">Adicionar Voyance da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="c52b0-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="c52b0-124">tooconfigure Olá integração de Voyance com o Azure AD, é necessário tooadd Voyance Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="c52b0-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c52b0-125">**tooadd Voyance da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="c52b0-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c52b0-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="c52b0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="c52b0-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c52b0-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="c52b0-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c52b0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="c52b0-133">Na caixa de pesquisa de Olá, escreva **Voyance**, selecione **Voyance** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="c52b0-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance na lista de resultados de Olá](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c52b0-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="c52b0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c52b0-136">Nesta secção, configure e teste do Azure AD-início de sessão único com Voyance com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c52b0-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c52b0-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Voyance é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c52b0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="c52b0-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Voyance tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c52b0-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="c52b0-139">No Voyance, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="c52b0-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c52b0-140">tooconfigure e teste do Azure AD-início de sessão único com Voyance, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c52b0-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c52b0-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="c52b0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c52b0-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c52b0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c52b0-143">**[Criar um utilizador de teste Voyance](#create-a-voyance-test-user)**  -toohave um homólogo de Britta Simon no Voyance é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="c52b0-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c52b0-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="c52b0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c52b0-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="c52b0-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c52b0-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="c52b0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c52b0-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Voyance.</span><span class="sxs-lookup"><span data-stu-id="c52b0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="c52b0-148">**tooconfigure do Azure AD-início de sessão único com Voyance, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="c52b0-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="c52b0-149">No Olá portal do Azure, no Olá **Voyance** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="c52b0-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="c52b0-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="c52b0-153">No Olá **Voyance domínio e os URLs** secção, execute os passos seguintes se quiser aplicação Olá tooconfigure de Olá **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="c52b0-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Domínio Voyance URLs único início de sessão informações e para IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="c52b0-155">a.</span><span class="sxs-lookup"><span data-stu-id="c52b0-155">a.</span></span> <span data-ttu-id="c52b0-156">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="c52b0-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="c52b0-157">b.</span><span class="sxs-lookup"><span data-stu-id="c52b0-157">b.</span></span> <span data-ttu-id="c52b0-158">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="c52b0-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="c52b0-159">Verifique **Mostrar avançadas definições de URL** e efetuar Olá seguir passo se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="c52b0-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Domínio Voyance URLs único início de sessão informações e para SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="c52b0-161">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="c52b0-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="c52b0-162">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="c52b0-162">These values are not real.</span></span> <span data-ttu-id="c52b0-163">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="c52b0-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="c52b0-164">Contacte [equipa de suporte de cliente Voyance](mailto:support@nyansa.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="c52b0-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="c52b0-165">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="c52b0-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="c52b0-167">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="c52b0-167">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c52b0-169">No Olá **Voyance configuração** secção, clique em **configurar Voyance** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="c52b0-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c52b0-170">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c52b0-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="c52b0-172">Numa janela do browser web diferente, início de sessão tooyour Voyance inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="c52b0-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="c52b0-173">Aceda toohello canto superior direito da barra de navegação de Olá e clique em Olá pendente que indica "**Acme University**".</span><span class="sxs-lookup"><span data-stu-id="c52b0-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Configurar o início de sessão único em aplicações do lado do Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="c52b0-175">Clique em "**definições de administrador**".</span><span class="sxs-lookup"><span data-stu-id="c52b0-175">Click "**Admin Settings**".</span></span>

    ![Configurar o início de sessão único nas definições de administração do lado da aplicação](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="c52b0-177">Clique em "**acesso de utilizador**" separador.</span><span class="sxs-lookup"><span data-stu-id="c52b0-177">Click "**User Access**" tab.</span></span>

    ![Configurar o início de sessão único de acesso de utilizador do lado de aplicação](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="c52b0-179">Clique em Olá "**SSO está desativado**" botão tooconfigure do Azure AD como um IdP utilizando SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="c52b0-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configurar único início de sessão na aplicação do lado do SSO está desativado no botão](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="c52b0-181">Aceda demasiado**SAML v2** secção e executar passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="c52b0-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Configurar o início de sessão único em aplicações do lado SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="c52b0-183">a.</span><span class="sxs-lookup"><span data-stu-id="c52b0-183">a.</span></span> <span data-ttu-id="c52b0-184">Selecione **ativada**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="c52b0-185">b.</span><span class="sxs-lookup"><span data-stu-id="c52b0-185">b.</span></span> <span data-ttu-id="c52b0-186">Colar **único início de sessão no URL do serviço SAML**, que copiou do Olá portal do Azure para Olá **URL de início de sessão do IdP** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c52b0-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="c52b0-187">c.</span><span class="sxs-lookup"><span data-stu-id="c52b0-187">c.</span></span> <span data-ttu-id="c52b0-188">Abra o certificado codificado em Base64 transferido no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **IdP Cert** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c52b0-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="c52b0-189">d.</span><span class="sxs-lookup"><span data-stu-id="c52b0-189">d.</span></span> <span data-ttu-id="c52b0-190">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c52b0-191">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="c52b0-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c52b0-192">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="c52b0-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c52b0-193">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c52b0-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c52b0-194">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c52b0-194">Create an Azure AD test user</span></span>

<span data-ttu-id="c52b0-195">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c52b0-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="c52b0-197">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="c52b0-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c52b0-198">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="c52b0-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c52b0-200">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c52b0-202">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="c52b0-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão de adição de Olá](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c52b0-204">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="c52b0-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c52b0-206">a.</span><span class="sxs-lookup"><span data-stu-id="c52b0-206">a.</span></span> <span data-ttu-id="c52b0-207">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c52b0-208">b.</span><span class="sxs-lookup"><span data-stu-id="c52b0-208">b.</span></span> <span data-ttu-id="c52b0-209">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c52b0-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c52b0-210">c.</span><span class="sxs-lookup"><span data-stu-id="c52b0-210">c.</span></span> <span data-ttu-id="c52b0-211">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c52b0-212">d.</span><span class="sxs-lookup"><span data-stu-id="c52b0-212">d.</span></span> <span data-ttu-id="c52b0-213">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="c52b0-214">Criar um utilizador de teste Voyance</span><span class="sxs-lookup"><span data-stu-id="c52b0-214">Create a Voyance test user</span></span>

<span data-ttu-id="c52b0-215">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Voyance.</span><span class="sxs-lookup"><span data-stu-id="c52b0-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="c52b0-216">Voyance suporta o aprovisionamento de just-in-time, que está por predefinição, ativada.</span><span class="sxs-lookup"><span data-stu-id="c52b0-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="c52b0-217">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="c52b0-217">There is no action item for you in this section.</span></span> <span data-ttu-id="c52b0-218">Um novo utilizador é criado durante uma tentativa tooaccess Voyance se não existir ainda.</span><span class="sxs-lookup"><span data-stu-id="c52b0-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="c52b0-219">Se precisar de um utilizador de toocreate manualmente, terá de toocontact [equipa de suporte de Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="c52b0-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c52b0-220">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c52b0-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c52b0-221">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooVoyance.</span><span class="sxs-lookup"><span data-stu-id="c52b0-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Atribuir a função de utilizador Olá][200]

<span data-ttu-id="c52b0-223">**tooassign Britta Simon tooVoyance, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="c52b0-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="c52b0-224">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="c52b0-226">Na lista de aplicações de Olá, selecione **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-226">In hello applications list, select **Voyance**.</span></span>

    ![ligação de Voyance Olá na lista de aplicações de Olá](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="c52b0-228">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c52b0-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="c52b0-230">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="c52b0-230">Click **Add** button.</span></span> <span data-ttu-id="c52b0-231">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c52b0-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="c52b0-233">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="c52b0-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c52b0-234">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c52b0-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c52b0-235">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c52b0-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c52b0-236">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="c52b0-236">Test single sign-on</span></span>

<span data-ttu-id="c52b0-237">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="c52b0-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c52b0-238">Ao clicar em mosaico de Voyance Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Voyance aplicação.</span><span class="sxs-lookup"><span data-stu-id="c52b0-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c52b0-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c52b0-239">Additional resources</span></span>

* [<span data-ttu-id="c52b0-240">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c52b0-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c52b0-241">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c52b0-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

