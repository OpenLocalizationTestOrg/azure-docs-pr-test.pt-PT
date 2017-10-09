---
title: "Tutorial: Integração do Azure Active Directory com início | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e frente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="fdc63-103">Tutorial: Integração do Azure Active Directory com início</span><span class="sxs-lookup"><span data-stu-id="fdc63-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="fdc63-104">Neste tutorial, saiba como toointegrate frente com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fdc63-104">In this tutorial, you learn how toointegrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fdc63-105">Integrar frente com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="fdc63-105">Integrating Front with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fdc63-106">Pode controlar no Azure AD que tenha acesso tooFront.</span><span class="sxs-lookup"><span data-stu-id="fdc63-106">You can control in Azure AD who has access tooFront.</span></span>
- <span data-ttu-id="fdc63-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooFront (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdc63-107">You can enable your users tooautomatically get signed-on tooFront (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fdc63-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdc63-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fdc63-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fdc63-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdc63-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fdc63-110">Prerequisites</span></span>

<span data-ttu-id="fdc63-111">integração de tooconfigure do Azure AD com o início, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="fdc63-111">tooconfigure Azure AD integration with Front, you need hello following items:</span></span>

- <span data-ttu-id="fdc63-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc63-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fdc63-113">Um frente-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="fdc63-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fdc63-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="fdc63-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fdc63-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="fdc63-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fdc63-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="fdc63-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fdc63-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fdc63-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fdc63-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="fdc63-118">Scenario description</span></span>
<span data-ttu-id="fdc63-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="fdc63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fdc63-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="fdc63-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fdc63-121">A adição de frente da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="fdc63-121">Adding Front from hello gallery</span></span>
2. <span data-ttu-id="fdc63-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="fdc63-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-hello-gallery"></a><span data-ttu-id="fdc63-123">A adição de frente da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="fdc63-123">Adding Front from hello gallery</span></span>
<span data-ttu-id="fdc63-124">tooconfigure Olá integração da frente com o Azure AD, é necessário tooadd frente Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="fdc63-124">tooconfigure hello integration of Front into Azure AD, you need tooadd Front from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fdc63-125">**tooadd frente da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fdc63-125">**tooadd Front from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdc63-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="fdc63-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="fdc63-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fdc63-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="fdc63-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fdc63-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="fdc63-133">Na caixa de pesquisa de Olá, escreva **front-**, selecione **front-** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="fdc63-133">In hello search box, type **Front**, select **Front** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Frente na lista de resultados de Olá](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fdc63-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="fdc63-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fdc63-136">Nesta secção, configure e teste do Azure AD-início de sessão único com início num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fdc63-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fdc63-137">Para único início de sessão toowork, do Azure AD tem tooknow qual Olá homólogo o utilizador à frente é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdc63-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Front is tooa user in Azure AD.</span></span> <span data-ttu-id="fdc63-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados com o utilizador à frente tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="fdc63-138">In other words, a link relationship between an Azure AD user and hello related user in Front needs toobe established.</span></span>

<span data-ttu-id="fdc63-139">Atribuir à frente, o valor de Olá de Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="fdc63-139">In Front, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fdc63-140">tooconfigure e teste do Azure AD-início de sessão único com o início, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fdc63-140">tooconfigure and test Azure AD single sign-on with Front, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fdc63-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="fdc63-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fdc63-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fdc63-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fdc63-143">**[Criar um utilizador de teste de frente](#create-a-front-test-user)**  -toohave um homólogo à frente de Britta Simon é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="fdc63-143">**[Create a Front test user](#create-a-front-test-user)** - toohave a counterpart of Britta Simon in Front that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fdc63-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="fdc63-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fdc63-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="fdc63-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fdc63-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="fdc63-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fdc63-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de início.</span><span class="sxs-lookup"><span data-stu-id="fdc63-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="fdc63-148">**tooconfigure do Azure AD-início de sessão único com o início, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fdc63-148">**tooconfigure Azure AD single sign-on with Front, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdc63-149">No Olá portal do Azure, no Olá **front-** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-149">In hello Azure portal, on hello **Front** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="fdc63-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="fdc63-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="fdc63-153">No Olá **URLs e de domínio de front-** secção, se desejar aplicação Olá tooconfigure **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="fdc63-153">On hello **Front Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="fdc63-155">a.</span><span class="sxs-lookup"><span data-stu-id="fdc63-155">a.</span></span> <span data-ttu-id="fdc63-156">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="fdc63-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="fdc63-157">b.</span><span class="sxs-lookup"><span data-stu-id="fdc63-157">b.</span></span> <span data-ttu-id="fdc63-158">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="fdc63-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="fdc63-159">Verifique **Mostrar avançadas definições de URL**, se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="fdc63-159">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="fdc63-161">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="fdc63-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="fdc63-162">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="fdc63-162">These values are not real.</span></span> <span data-ttu-id="fdc63-163">Atualização, estes valores com Olá real identificador, o URL de resposta e URL de início de sessão que serão explicados de forma mais tarde no tutorial ou contacte [equipa de suporte de front-cliente](mailto:support@frontapp.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="fdc63-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) tooget these values.</span></span> 

5. <span data-ttu-id="fdc63-164">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="fdc63-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="fdc63-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="fdc63-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="fdc63-168">No Olá **front-configuração** secção, clique em **configurar Front** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="fdc63-168">On hello **Front Configuration** section, click **Configure Front** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fdc63-169">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="fdc63-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="fdc63-171">Inquilino de frente tooyour início de sessão como administrador.</span><span class="sxs-lookup"><span data-stu-id="fdc63-171">Sign-on tooyour Front tenant as an administrator.</span></span>

9. <span data-ttu-id="fdc63-172">Aceda demasiado**definições (ícone roda dentada em Olá parte inferior da barra lateral esquerdo de Olá) > Preferências**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-172">Go too**Settings (cog icon at hello bottom of hello left sidebar) > Preferences**.</span></span>
   
    ![Configurar lado único início de sessão na aplicação](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="fdc63-174">Clique em **início de sessão único** ligação.</span><span class="sxs-lookup"><span data-stu-id="fdc63-174">Click **Single Sign On** link.</span></span>
   
    ![Configurar lado único início de sessão na aplicação](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="fdc63-176">Selecione **SAML** no Olá na lista pendente de **início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-176">Select **SAML** in hello drop-down list of **Single Sign On**.</span></span>
   
    ![Configurar lado único início de sessão na aplicação](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="fdc63-178">No Olá **ponto de entrada** caixa de texto colocados valor Olá **URL Single Sign-on serviço** do Assistente de configuração de aplicações do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fdc63-178">In hello **Entry Point** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![Configurar lado único início de sessão na aplicação](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="fdc63-180">Abra o transferido **Certificate(Base64)** no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência de ficheiros e, em seguida, cole-toohello **certificado de assinatura** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="fdc63-180">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Signing certificate** textbox.</span></span>
    
    ![Configurar lado único início de sessão na aplicação](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="fdc63-182">No Olá **as definições do fornecedor de serviço** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="fdc63-182">On hello **Service provider settings** section, perform hello following steps:</span></span>

    ![Configurar lado único início de sessão na aplicação](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="fdc63-184">a.</span><span class="sxs-lookup"><span data-stu-id="fdc63-184">a.</span></span> <span data-ttu-id="fdc63-185">Copie o valor Olá **ID de entidade** e cole-Olá **identificador** textbox em **URLs e de domínio de front-** secção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdc63-185">Copy hello value of **Entity ID** and paste it into hello **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="fdc63-186">b.</span><span class="sxs-lookup"><span data-stu-id="fdc63-186">b.</span></span> <span data-ttu-id="fdc63-187">Copie o valor de Olá de **ACS URL** e cole-Olá **URL de início de sessão** textbox em **URLs e de domínio de front-** secção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdc63-187">Copy hello value of **ACS URL** and paste it into hello **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="fdc63-188">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="fdc63-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="fdc63-189">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="fdc63-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fdc63-190">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="fdc63-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fdc63-191">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fdc63-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fdc63-192">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc63-192">Create an Azure AD test user</span></span>

<span data-ttu-id="fdc63-193">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdc63-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="fdc63-195">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fdc63-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdc63-196">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="fdc63-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fdc63-198">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fdc63-200">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fdc63-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fdc63-202">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="fdc63-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fdc63-204">a.</span><span class="sxs-lookup"><span data-stu-id="fdc63-204">a.</span></span> <span data-ttu-id="fdc63-205">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fdc63-206">b.</span><span class="sxs-lookup"><span data-stu-id="fdc63-206">b.</span></span> <span data-ttu-id="fdc63-207">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fdc63-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fdc63-208">c.</span><span class="sxs-lookup"><span data-stu-id="fdc63-208">c.</span></span> <span data-ttu-id="fdc63-209">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="fdc63-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fdc63-210">d.</span><span class="sxs-lookup"><span data-stu-id="fdc63-210">d.</span></span> <span data-ttu-id="fdc63-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="fdc63-212">Criar um utilizador de teste de início</span><span class="sxs-lookup"><span data-stu-id="fdc63-212">Create a Front test user</span></span>

<span data-ttu-id="fdc63-213">Nesta secção, vai criar um utilizador chamado Britta Simon à frente.</span><span class="sxs-lookup"><span data-stu-id="fdc63-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="fdc63-214">Trabalhar com [equipa de suporte de front-cliente](mailto:support@frontapp.com) para adicionar utilizadores de Olá na plataforma de frente Olá.</span><span class="sxs-lookup"><span data-stu-id="fdc63-214">Work with [Front Client support team](mailto:support@frontapp.com) to add hello users in hello Front platform.</span></span> <span data-ttu-id="fdc63-215">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="fdc63-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fdc63-216">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="fdc63-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fdc63-217">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooFront.</span><span class="sxs-lookup"><span data-stu-id="fdc63-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFront.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="fdc63-219">**tooassign Britta Simon tooFront, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="fdc63-219">**tooassign Britta Simon tooFront, perform hello following steps:**</span></span>

1. <span data-ttu-id="fdc63-220">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="fdc63-222">Na lista de aplicações de Olá, selecione **front-**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-222">In hello applications list, select **Front**.</span></span>

    ![ligação de frente Olá na lista de aplicações de Olá](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="fdc63-224">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="fdc63-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="fdc63-226">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="fdc63-226">Click **Add** button.</span></span> <span data-ttu-id="fdc63-227">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fdc63-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="fdc63-229">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="fdc63-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fdc63-230">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fdc63-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fdc63-231">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fdc63-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fdc63-232">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="fdc63-232">Test single sign-on</span></span>

<span data-ttu-id="fdc63-233">o objetivo desta secção Olá é tootest utilizando o Azure AD SSOconfiguration Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="fdc63-233">hello objective of this section is tootest your Azure AD SSOconfiguration using hello Access Panel.</span></span>

<span data-ttu-id="fdc63-234">Ao clicar em mosaico de frente Olá no painel de acesso de Olá, deve colocar a aplicação de frente de tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="fdc63-234">When you click hello Front tile in hello Access Panel, you should get automatically signed-on tooyour Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fdc63-235">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fdc63-235">Additional resources</span></span>

* [<span data-ttu-id="fdc63-236">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdc63-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fdc63-237">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fdc63-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

