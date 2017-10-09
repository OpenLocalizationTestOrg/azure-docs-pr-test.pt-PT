---
title: "Tutorial: Integração do Azure Active Directory com ICIMS | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ICIMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 72dbd649-e4b1-4d72-ad76-636d84922596
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3fa970f008e64e84b0a1280f691f0181851b757c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icims"></a><span data-ttu-id="56af7-103">Tutorial: Integração do Azure Active Directory com ICIMS</span><span class="sxs-lookup"><span data-stu-id="56af7-103">Tutorial: Azure Active Directory integration with ICIMS</span></span>

<span data-ttu-id="56af7-104">Neste tutorial, saiba como toointegrate ICIMS com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56af7-104">In this tutorial, you learn how toointegrate ICIMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56af7-105">Integrar ICIMS com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="56af7-105">Integrating ICIMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="56af7-106">Pode controlar no Azure AD que tenha acesso tooICIMS</span><span class="sxs-lookup"><span data-stu-id="56af7-106">You can control in Azure AD who has access tooICIMS</span></span>
- <span data-ttu-id="56af7-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooICIMS (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="56af7-107">You can enable your users tooautomatically get signed-on tooICIMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56af7-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="56af7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="56af7-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56af7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56af7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="56af7-110">Prerequisites</span></span>

<span data-ttu-id="56af7-111">integração do Azure AD com ICIMS tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="56af7-111">tooconfigure Azure AD integration with ICIMS, you need hello following items:</span></span>

- <span data-ttu-id="56af7-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="56af7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56af7-113">Um ICIMS-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="56af7-113">An ICIMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56af7-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="56af7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56af7-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="56af7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56af7-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="56af7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56af7-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56af7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56af7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="56af7-118">Scenario description</span></span>
<span data-ttu-id="56af7-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="56af7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56af7-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="56af7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56af7-121">Adicionar ICIMS da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="56af7-121">Adding ICIMS from hello gallery</span></span>
2. <span data-ttu-id="56af7-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="56af7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icims-from-hello-gallery"></a><span data-ttu-id="56af7-123">Adicionar ICIMS da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="56af7-123">Adding ICIMS from hello gallery</span></span>
<span data-ttu-id="56af7-124">tooconfigure Olá integração de ICIMS com o Azure AD, é necessário tooadd ICIMS Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="56af7-124">tooconfigure hello integration of ICIMS into Azure AD, you need tooadd ICIMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="56af7-125">**tooadd ICIMS da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="56af7-125">**tooadd ICIMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="56af7-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="56af7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="56af7-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="56af7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="56af7-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="56af7-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="56af7-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56af7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="56af7-133">Na caixa de pesquisa de Olá, escreva **ICIMS**, selecione **ICIMS** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="56af7-133">In hello search box, type **ICIMS**, select **ICIMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ICIMS na lista de resultados de Olá](./media/active-directory-saas-icims-tutorial/tutorial_icims_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="56af7-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="56af7-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="56af7-136">Nesta secção, configure e teste do Azure AD-início de sessão único com ICIMS com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="56af7-136">In this section, you configure and test Azure AD single sign-on with ICIMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56af7-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ICIMS é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56af7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ICIMS is tooa user in Azure AD.</span></span> <span data-ttu-id="56af7-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ICIMS tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="56af7-138">In other words, a link relationship between an Azure AD user and hello related user in ICIMS needs toobe established.</span></span>

<span data-ttu-id="56af7-139">No ICIMS, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="56af7-139">In ICIMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="56af7-140">tooconfigure e teste do Azure AD-início de sessão único com ICIMS, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="56af7-140">tooconfigure and test Azure AD single sign-on with ICIMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="56af7-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="56af7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="56af7-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56af7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56af7-143">**[Criar um utilizador de teste ICIMS](#create-an-icims-test-user)**  -toohave um homólogo de Britta Simon no ICIMS é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="56af7-143">**[Create an ICIMS test user](#create-an-icims-test-user)** - toohave a counterpart of Britta Simon in ICIMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="56af7-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="56af7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56af7-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="56af7-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="56af7-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="56af7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="56af7-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação ICIMS.</span><span class="sxs-lookup"><span data-stu-id="56af7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ICIMS application.</span></span>

<span data-ttu-id="56af7-148">**tooconfigure do Azure AD-início de sessão único com ICIMS, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="56af7-148">**tooconfigure Azure AD single sign-on with ICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="56af7-149">No Olá portal do Azure, no Olá **ICIMS** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="56af7-149">In hello Azure portal, on hello **ICIMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="56af7-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="56af7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-icims-tutorial/tutorial_icims_samlbase.png)

3. <span data-ttu-id="56af7-153">No Olá **ICIMS domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="56af7-153">On hello **ICIMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Domínio ICIMS e os URLs únicos de informações de início de sessão](./media/active-directory-saas-icims-tutorial/tutorial_icims_url.png)

    <span data-ttu-id="56af7-155">a.</span><span class="sxs-lookup"><span data-stu-id="56af7-155">a.</span></span> <span data-ttu-id="56af7-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="56af7-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    <span data-ttu-id="56af7-157">b.</span><span class="sxs-lookup"><span data-stu-id="56af7-157">b.</span></span> <span data-ttu-id="56af7-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenant name>.icims.com`</span><span class="sxs-lookup"><span data-stu-id="56af7-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant name>.icims.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56af7-159">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="56af7-159">These values are not real.</span></span> <span data-ttu-id="56af7-160">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="56af7-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="56af7-161">Contacte [equipa de suporte de cliente ICIMS](https://www.icims.com/contact-us) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="56af7-161">Contact [ICIMS Client support team](https://www.icims.com/contact-us) tooget these values.</span></span> 
 
4. <span data-ttu-id="56af7-162">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="56af7-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-icims-tutorial/tutorial_icims_certificate.png) 

5. <span data-ttu-id="56af7-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="56af7-164">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-icims-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="56af7-166">No Olá **ICIMS configuração** secção, clique em **configurar ICIMS** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="56af7-166">On hello **ICIMS Configuration** section, click **Configure ICIMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="56af7-167">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="56af7-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de ICIMS](./media/active-directory-saas-icims-tutorial/tutorial_icims_configure.png) 

7. <span data-ttu-id="56af7-169">tooconfigure-início de sessão único em **ICIMS** lado, terá de Olá toosend transferido **XML de metadados**, **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** demasiado [ICIMS suporta equipa](https://www.icims.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="56af7-169">tooconfigure single sign-on on **ICIMS** side, you need toosend hello downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ICIMS support team](https://www.icims.com/contact-us).</span></span> <span data-ttu-id="56af7-170">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="56af7-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="56af7-171">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="56af7-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="56af7-172">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="56af7-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="56af7-173">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56af7-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="56af7-174">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="56af7-174">Create an Azure AD test user</span></span>
<span data-ttu-id="56af7-175">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="56af7-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="56af7-177">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="56af7-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="56af7-178">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="56af7-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-icims-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56af7-180">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="56af7-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-icims-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56af7-182">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="56af7-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botão de adição de Olá](./media/active-directory-saas-icims-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56af7-184">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="56af7-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-icims-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56af7-186">a.</span><span class="sxs-lookup"><span data-stu-id="56af7-186">a.</span></span> <span data-ttu-id="56af7-187">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56af7-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56af7-188">b.</span><span class="sxs-lookup"><span data-stu-id="56af7-188">b.</span></span> <span data-ttu-id="56af7-189">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="56af7-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56af7-190">c.</span><span class="sxs-lookup"><span data-stu-id="56af7-190">c.</span></span> <span data-ttu-id="56af7-191">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="56af7-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="56af7-192">d.</span><span class="sxs-lookup"><span data-stu-id="56af7-192">d.</span></span> <span data-ttu-id="56af7-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="56af7-193">Click **Create**.</span></span>
 
### <a name="create-an-icims-test-user"></a><span data-ttu-id="56af7-194">Criar um utilizador de teste ICIMS</span><span class="sxs-lookup"><span data-stu-id="56af7-194">Create an ICIMS test user</span></span>

<span data-ttu-id="56af7-195">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon ICIMS.</span><span class="sxs-lookup"><span data-stu-id="56af7-195">hello objective of this section is toocreate a user called Britta Simon in ICIMS.</span></span> <span data-ttu-id="56af7-196">Trabalhar com [ICIMS suporta equipa](https://www.icims.com/contact-us) tooadd utilizadores Olá Olá conta ICIMS.</span><span class="sxs-lookup"><span data-stu-id="56af7-196">Work with [ICIMS support team](https://www.icims.com/contact-us) tooadd hello users in hello ICIMS account.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="56af7-197">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="56af7-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="56af7-198">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooICIMS.</span><span class="sxs-lookup"><span data-stu-id="56af7-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooICIMS.</span></span>

![Atribuir a função de utilizador Olá][200]

<span data-ttu-id="56af7-200">**tooassign Britta Simon tooICIMS, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="56af7-200">**tooassign Britta Simon tooICIMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="56af7-201">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="56af7-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="56af7-203">Na lista de aplicações de Olá, selecione **ICIMS**.</span><span class="sxs-lookup"><span data-stu-id="56af7-203">In hello applications list, select **ICIMS**.</span></span>

    ![Olá ICIMS ligação na lista de aplicações de Olá](./media/active-directory-saas-icims-tutorial/tutorial_icims_app.png) 

3. <span data-ttu-id="56af7-205">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="56af7-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202] 

4. <span data-ttu-id="56af7-207">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="56af7-207">Click **Add** button.</span></span> <span data-ttu-id="56af7-208">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56af7-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="56af7-210">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="56af7-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="56af7-211">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56af7-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56af7-212">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="56af7-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="56af7-213">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="56af7-213">Test single sign-on</span></span>

<span data-ttu-id="56af7-214">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="56af7-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="56af7-215">Ao clicar Olá ICIMS na peça de mosaico Olá painel de acesso, pode ser obtido a aplicação de ICIMS tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="56af7-215">When you click hello ICIMS tile in hello Access Panel, you should get automatically signed-on tooyour ICIMS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56af7-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="56af7-216">Additional resources</span></span>

* [<span data-ttu-id="56af7-217">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56af7-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56af7-218">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="56af7-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icims-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icims-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icims-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icims-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icims-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icims-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icims-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icims-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icims-tutorial/tutorial_general_203.png

