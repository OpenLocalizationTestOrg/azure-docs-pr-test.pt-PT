---
title: "Tutorial: Integração do Azure Active Directory com a plataforma de gestão de contrato Icertis | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e a plataforma de gestão do Icertis contrato."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6627e6dd-f559-4cd4-a509-f6d9a4961b49
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 6eb99553ef9df732512a38fb0489e66b41ba94a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-icertis-contract-management-platform"></a><span data-ttu-id="d7f79-103">Tutorial: Integração do Azure Active Directory com a plataforma de gestão de contrato Icertis</span><span class="sxs-lookup"><span data-stu-id="d7f79-103">Tutorial: Azure Active Directory integration with Icertis Contract Management Platform</span></span>

<span data-ttu-id="d7f79-104">Neste tutorial, saiba como toointegrate Icertis plataforma de gestão de contrato com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7f79-104">In this tutorial, you learn how toointegrate Icertis Contract Management Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7f79-105">Plataforma de gestão de contrato Icertis a integração com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="d7f79-105">Integrating Icertis Contract Management Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d7f79-106">Pode controlar no Azure AD que tenha acesso tooIcertis plataforma de gestão do contrato</span><span class="sxs-lookup"><span data-stu-id="d7f79-106">You can control in Azure AD who has access tooIcertis Contract Management Platform</span></span>
- <span data-ttu-id="d7f79-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooIcertis plataforma de gestão do contrato (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7f79-107">You can enable your users tooautomatically get signed-on tooIcertis Contract Management Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7f79-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d7f79-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d7f79-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d7f79-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7f79-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d7f79-110">Prerequisites</span></span>

<span data-ttu-id="d7f79-111">integração do Azure AD com a plataforma de gestão de contrato Icertis tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d7f79-111">tooconfigure Azure AD integration with Icertis Contract Management Platform, you need hello following items:</span></span>

- <span data-ttu-id="d7f79-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7f79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7f79-113">Uma plataforma de gestão de contrato Icertis-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="d7f79-113">An Icertis Contract Management Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7f79-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d7f79-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7f79-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d7f79-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7f79-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d7f79-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7f79-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7f79-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7f79-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d7f79-118">Scenario description</span></span>
<span data-ttu-id="d7f79-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d7f79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7f79-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="d7f79-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7f79-121">A adição de plataforma de gestão de contrato Icertis de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="d7f79-121">Adding Icertis Contract Management Platform from hello gallery</span></span>
2. <span data-ttu-id="d7f79-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="d7f79-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-icertis-contract-management-platform-from-hello-gallery"></a><span data-ttu-id="d7f79-123">A adição de plataforma de gestão de contrato Icertis de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="d7f79-123">Adding Icertis Contract Management Platform from hello gallery</span></span>
<span data-ttu-id="d7f79-124">tooconfigure Olá integração da plataforma de gestão do Icertis contrato com o Azure AD, é necessário tooadd plataforma de gestão de contrato Icertis Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="d7f79-124">tooconfigure hello integration of Icertis Contract Management Platform into Azure AD, you need tooadd Icertis Contract Management Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d7f79-125">**tooadd Icertis contrato plataforma de gestão da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d7f79-125">**tooadd Icertis Contract Management Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7f79-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="d7f79-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7f79-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d7f79-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="d7f79-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7f79-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="d7f79-133">Na caixa de pesquisa de Olá, escreva **plataforma de gestão de contrato Icertis**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-133">In hello search box, type **Icertis Contract Management Platform**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_search.png)

5. <span data-ttu-id="d7f79-135">No painel de resultados de Olá, selecione **plataforma de gestão de contrato Icertis**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="d7f79-135">In hello results panel, select **Icertis Contract Management Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7f79-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="d7f79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7f79-138">Nesta secção, configure e teste do Azure AD-início de sessão único com a plataforma de gestão de contrato de Icertis com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d7f79-138">In this section, you configure and test Azure AD single sign-on with Icertis Contract Management Platform based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7f79-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na plataforma de gestão de contrato Icertis é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7f79-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Icertis Contract Management Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="d7f79-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na plataforma de gestão de contrato Icertis tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d7f79-140">In other words, a link relationship between an Azure AD user and hello related user in Icertis Contract Management Platform needs toobe established.</span></span>

<span data-ttu-id="d7f79-141">Na plataforma de gestão de contrato Icertis, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="d7f79-141">In Icertis Contract Management Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d7f79-142">tooconfigure e teste do Azure AD-início de sessão único com a plataforma de gestão de contrato Icertis, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d7f79-142">tooconfigure and test Azure AD single sign-on with Icertis Contract Management Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d7f79-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="d7f79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d7f79-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7f79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7f79-145">**[Criar um utilizador de teste de plataforma de gestão de contrato Icertis](#creating-an-icertis-contract-management-platform-test-user)**  -toohave um homólogo de Britta Simon na plataforma de gestão de contrato Icertis é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="d7f79-145">**[Creating an Icertis Contract Management Platform test user](#creating-an-icertis-contract-management-platform-test-user)** - toohave a counterpart of Britta Simon in Icertis Contract Management Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7f79-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="d7f79-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7f79-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="d7f79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7f79-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d7f79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7f79-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação da plataforma de gestão do Icertis contrato.</span><span class="sxs-lookup"><span data-stu-id="d7f79-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Icertis Contract Management Platform application.</span></span>

<span data-ttu-id="d7f79-150">**tooconfigure do Azure AD-início de sessão único com a plataforma de gestão de contrato de Icertis efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d7f79-150">**tooconfigure Azure AD single sign-on with Icertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7f79-151">No Olá portal do Azure, no Olá **plataforma de gestão de contrato Icertis** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-151">In hello Azure portal, on hello **Icertis Contract Management Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="d7f79-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="d7f79-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_samlbase.png)

3. <span data-ttu-id="d7f79-155">No Olá **URLs e de domínio de plataforma de gestão de contrato Icertis** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="d7f79-155">On hello **Icertis Contract Management Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_url.png)

    <span data-ttu-id="d7f79-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7f79-157">a.</span></span> <span data-ttu-id="d7f79-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="d7f79-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    <span data-ttu-id="d7f79-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7f79-159">b.</span></span> <span data-ttu-id="d7f79-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company name>.icertis.com`</span><span class="sxs-lookup"><span data-stu-id="d7f79-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.icertis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7f79-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="d7f79-161">These values are not real.</span></span> <span data-ttu-id="d7f79-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="d7f79-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d7f79-163">Contacte [equipa de suporte de cliente de plataforma de gestão de contrato Icertis](https://www.icertis.com/company/contact/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="d7f79-163">Contact [Icertis Contract Management Platform Client support team](https://www.icertis.com/company/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="d7f79-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="d7f79-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_certificate.png) 

5. <span data-ttu-id="d7f79-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="d7f79-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-icertisicm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d7f79-168">No Olá **configuração de plataforma de gestão de contrato Icertis** secção, clique em **configurar plataforma de gestão de contrato de Icertis** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="d7f79-168">On hello **Icertis Contract Management Platform Configuration** section, click **Configure Icertis Contract Management Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d7f79-169">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="d7f79-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_configure.png) 

7. <span data-ttu-id="d7f79-171">tooconfigure-início de sessão único em **plataforma de gestão de contrato Icertis** lado, terá de Olá toosend transferido **XML de metadados** e **Sign-Out URL, ID de entidade de SAML e SAML Single Sign-On URL do serviço** demasiado[equipa de suporte de plataforma de gestão de contrato Icertis](https://www.icertis.com/company/contact/).</span><span class="sxs-lookup"><span data-stu-id="d7f79-171">tooconfigure single sign-on on **Icertis Contract Management Platform** side, you need toosend hello downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="d7f79-172">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="d7f79-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d7f79-173">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="d7f79-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d7f79-174">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7f79-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7f79-175">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7f79-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7f79-176">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f79-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="d7f79-178">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d7f79-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7f79-179">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="d7f79-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7f79-181">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7f79-183">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="d7f79-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7f79-185">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="d7f79-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-icertisicm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7f79-187">a.</span><span class="sxs-lookup"><span data-stu-id="d7f79-187">a.</span></span> <span data-ttu-id="d7f79-188">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7f79-189">b.</span><span class="sxs-lookup"><span data-stu-id="d7f79-189">b.</span></span> <span data-ttu-id="d7f79-190">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d7f79-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7f79-191">c.</span><span class="sxs-lookup"><span data-stu-id="d7f79-191">c.</span></span> <span data-ttu-id="d7f79-192">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d7f79-193">d.</span><span class="sxs-lookup"><span data-stu-id="d7f79-193">d.</span></span> <span data-ttu-id="d7f79-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-194">Click **Create**.</span></span>
 
### <a name="creating-an-icertis-contract-management-platform-test-user"></a><span data-ttu-id="d7f79-195">Criar um utilizador de teste de plataforma de gestão de contrato Icertis</span><span class="sxs-lookup"><span data-stu-id="d7f79-195">Creating an Icertis Contract Management Platform test user</span></span>

<span data-ttu-id="d7f79-196">Nesta secção, vai criar um utilizador chamado Britta Simon na plataforma de gestão do Icertis contrato.</span><span class="sxs-lookup"><span data-stu-id="d7f79-196">In this section, you create a user called Britta Simon in Icertis Contract Management Platform.</span></span> <span data-ttu-id="d7f79-197">Consulte [equipa de suporte de plataforma de gestão de contrato Icertis](https://www.icertis.com/company/contact/) tooadd utilizadores Olá Olá Icertis plataforma de gestão de contrato.</span><span class="sxs-lookup"><span data-stu-id="d7f79-197">Please work with [Icertis Contract Management Platform support team](https://www.icertis.com/company/contact/) tooadd hello users in hello Icertis Contract Management Platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d7f79-198">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7f79-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d7f79-199">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooIcertis plataforma de gestão de contrato.</span><span class="sxs-lookup"><span data-stu-id="d7f79-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIcertis Contract Management Platform.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="d7f79-201">**tooassign Britta Simon tooIcertis plataforma de gestão do contrato, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d7f79-201">**tooassign Britta Simon tooIcertis Contract Management Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="d7f79-202">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="d7f79-204">Na lista de aplicações de Olá, selecione **plataforma de gestão de contrato Icertis**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-204">In hello applications list, select **Icertis Contract Management Platform**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-icertisicm-tutorial/tutorial_icertisicm_app.png) 

3. <span data-ttu-id="d7f79-206">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d7f79-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="d7f79-208">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="d7f79-208">Click **Add** button.</span></span> <span data-ttu-id="d7f79-209">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7f79-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="d7f79-211">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="d7f79-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d7f79-212">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7f79-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7f79-213">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7f79-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7f79-214">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d7f79-214">Testing single sign-on</span></span>

<span data-ttu-id="d7f79-215">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="d7f79-215">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="d7f79-216">Ao clicar em mosaico de plataforma de gestão de contrato Icertis Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour aplicação Icertis plataforma de gestão de contrato.</span><span class="sxs-lookup"><span data-stu-id="d7f79-216">When you click hello Icertis Contract Management Platform tile in hello Access Panel, you should get automatically signed-on tooyour Icertis Contract Management Platform application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7f79-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d7f79-217">Additional resources</span></span>

* [<span data-ttu-id="d7f79-218">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7f79-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7f79-219">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d7f79-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-icertisicm-tutorial/tutorial_general_203.png

