---
title: "Tutorial: Integração do Azure Active Directory com Kindling | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Kindling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="ecbf6-103">Tutorial: Integração do Azure Active Directory com Kindling</span><span class="sxs-lookup"><span data-stu-id="ecbf6-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="ecbf6-104">Neste tutorial, saiba como toointegrate Kindling com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecbf6-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ecbf6-105">Integrar Kindling com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="ecbf6-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ecbf6-106">Pode controlar no Azure AD que tenha acesso tooKindling</span><span class="sxs-lookup"><span data-stu-id="ecbf6-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="ecbf6-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooKindling (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecbf6-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ecbf6-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ecbf6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ecbf6-109">Se pretender que tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="ecbf6-110">[o que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf6-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecbf6-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ecbf6-111">Prerequisites</span></span>

<span data-ttu-id="ecbf6-112">integração de tooconfigure do Azure AD com Kindling, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="ecbf6-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="ecbf6-113">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecbf6-113">An Azure AD subscription</span></span>
- <span data-ttu-id="ecbf6-114">Um Kindling-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="ecbf6-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ecbf6-115">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ecbf6-116">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ecbf6-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ecbf6-117">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ecbf6-118">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecbf6-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ecbf6-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ecbf6-119">Scenario description</span></span>
<span data-ttu-id="ecbf6-120">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ecbf6-121">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="ecbf6-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ecbf6-122">Adicionar Kindling da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="ecbf6-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="ecbf6-123">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="ecbf6-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="ecbf6-124">Adicionar Kindling da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="ecbf6-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="ecbf6-125">integração de Olá tooconfigure de Kindling com o Azure AD, terá de tooadd Kindling Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ecbf6-126">**tooadd Kindling da Galeria de Olá, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ecbf6-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecbf6-127">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ecbf6-129">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ecbf6-130">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-130">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="ecbf6-132">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="ecbf6-134">Na caixa de pesquisa de Olá, escreva **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-134">In hello search box, type **Kindling**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="ecbf6-136">No painel de resultados de Olá, selecione **Kindling**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ecbf6-138">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="ecbf6-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ecbf6-139">Nesta secção, configure e teste do Azure AD-início de sessão único com Kindling com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="ecbf6-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ecbf6-140">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Kindling é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="ecbf6-141">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados com o utilizador no Kindling necessidades toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="ecbf6-142">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Kindling.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="ecbf6-143">tooconfigure e teste do Azure AD-início de sessão único com Kindling, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ecbf6-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ecbf6-144">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ecbf6-145">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ecbf6-146">**[Criar um utilizador de teste Kindling](#creating-a-kindling-test-user)**  -toohave um homólogo de Britta Simon no Kindling que está ligado toohello do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ecbf6-147">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ecbf6-148">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ecbf6-149">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="ecbf6-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ecbf6-150">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Kindling.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="ecbf6-151">**tooconfigure do Azure AD-início de sessão único com Kindling, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ecbf6-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecbf6-152">No Olá portal do Azure, no Olá **Kindling** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="ecbf6-154">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="ecbf6-156">No Olá **Kindling domínios e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ecbf6-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="ecbf6-158">a.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-158">a.</span></span> <span data-ttu-id="ecbf6-159">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="ecbf6-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="ecbf6-160">b.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-160">b.</span></span>  <span data-ttu-id="ecbf6-161">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="ecbf6-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ecbf6-162">Estes valores não estiverem Olá real.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-162">These values are not hello real.</span></span> <span data-ttu-id="ecbf6-163">Atualize estes valores com Olá real início de sessão no URL e o identificador.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="ecbf6-164">Contacte [equipa de suporte de Kindling](mailto:support@kindlingapp.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="ecbf6-165">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="ecbf6-167">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-167">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ecbf6-169">No Olá **Kindling configuração** secção, clique em **configurar Kindling** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ecbf6-170">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ecbf6-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="ecbf6-172">tooconfigure-início de sessão único em **Kindling** lado, terá de Olá toosend transferido **certificado (Base64)**, **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML**demasiado[equipa de suporte de Kindling](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="ecbf6-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="ecbf6-173">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="ecbf6-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ecbf6-174">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ecbf6-175">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ecbf6-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ecbf6-176">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecbf6-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="ecbf6-177">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="ecbf6-179">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ecbf6-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecbf6-180">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ecbf6-182">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ecbf6-184">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ecbf6-186">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ecbf6-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ecbf6-188">a.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-188">a.</span></span> <span data-ttu-id="ecbf6-189">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ecbf6-190">b.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-190">b.</span></span> <span data-ttu-id="ecbf6-191">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ecbf6-192">c.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-192">c.</span></span> <span data-ttu-id="ecbf6-193">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ecbf6-194">d.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-194">d.</span></span> <span data-ttu-id="ecbf6-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="ecbf6-196">Criar um utilizador de teste Kindling</span><span class="sxs-lookup"><span data-stu-id="ecbf6-196">Creating a Kindling test user</span></span>

<span data-ttu-id="ecbf6-197">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon Kindling.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="ecbf6-198">Kindling suportam o aprovisionamento de just-in-time.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="ecbf6-199">Que já ativou-lo na [configurar do Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="ecbf6-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="ecbf6-200">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ecbf6-201">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecbf6-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ecbf6-202">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooKindling.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="ecbf6-204">**tooassign Britta Simon tooKindling, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="ecbf6-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="ecbf6-205">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="ecbf6-207">Na lista de aplicações de Olá, selecione **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-207">In hello applications list, select **Kindling**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="ecbf6-209">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="ecbf6-211">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-211">Click **Add** button.</span></span> <span data-ttu-id="ecbf6-212">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="ecbf6-214">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ecbf6-215">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ecbf6-216">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ecbf6-217">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="ecbf6-217">Testing single sign-on</span></span>

<span data-ttu-id="ecbf6-218">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ecbf6-219">Ao clicar em mosaico de Kindling Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Kindling aplicação.</span><span class="sxs-lookup"><span data-stu-id="ecbf6-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ecbf6-220">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ecbf6-220">Additional resources</span></span>

* [<span data-ttu-id="ecbf6-221">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecbf6-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ecbf6-222">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ecbf6-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

