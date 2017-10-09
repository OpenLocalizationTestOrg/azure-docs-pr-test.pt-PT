---
title: "Tutorial: Integração do Azure Active Directory Predictix preços relatórios | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Predictix preços Reporting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: c2ba85f613f5a71de72278a0d1916c135b835b60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="df702-103">Tutorial: Integração do Azure Active Directory Predictix preços relatórios</span><span class="sxs-lookup"><span data-stu-id="df702-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>

<span data-ttu-id="df702-104">Neste tutorial, saiba como toointegrate Predictix preços relatórios com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df702-104">In this tutorial, you learn how toointegrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df702-105">Relatórios de preços Predictix a integração com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="df702-105">Integrating Predictix Price Reporting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="df702-106">Pode controlar no Azure AD que tenha tooPredictix de acesso a relatórios de preços.</span><span class="sxs-lookup"><span data-stu-id="df702-106">You can control in Azure AD who has access tooPredictix Price Reporting.</span></span>
- <span data-ttu-id="df702-107">Pode ativar os seus utilizadores tooautomatically get com sessão iniciada tooPredictix preços Reporting (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df702-107">You can enable your users tooautomatically get signed-on tooPredictix Price Reporting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="df702-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="df702-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="df702-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df702-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df702-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="df702-110">Prerequisites</span></span>

<span data-ttu-id="df702-111">integração do Azure AD com relatórios de preços Predictix tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="df702-111">tooconfigure Azure AD integration with Predictix Price Reporting, you need hello following items:</span></span>

- <span data-ttu-id="df702-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df702-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df702-113">Um Predictix preços Reporting-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="df702-113">A Predictix Price Reporting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df702-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="df702-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df702-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="df702-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df702-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="df702-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df702-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df702-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df702-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="df702-118">Scenario description</span></span>
<span data-ttu-id="df702-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="df702-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df702-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="df702-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df702-121">A adição de relatórios de preços Predictix da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="df702-121">Adding Predictix Price Reporting from hello gallery</span></span>
2. <span data-ttu-id="df702-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="df702-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-hello-gallery"></a><span data-ttu-id="df702-123">A adição de relatórios de preços Predictix da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="df702-123">Adding Predictix Price Reporting from hello gallery</span></span>
<span data-ttu-id="df702-124">tooconfigure Olá integração de criação de relatórios de preços Predictix com o Azure AD, é necessário tooadd Predictix preços Reporting Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="df702-124">tooconfigure hello integration of Predictix Price Reporting into Azure AD, you need tooadd Predictix Price Reporting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="df702-125">**tooadd Predictix preços relatórios na Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="df702-125">**tooadd Predictix Price Reporting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="df702-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="df702-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="df702-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="df702-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="df702-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="df702-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="df702-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df702-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="df702-133">Na caixa de pesquisa de Olá, escreva **Predictix preços Reporting**, selecione **Predictix preços Reporting** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="df702-133">In hello search box, type **Predictix Price Reporting**, select **Predictix Price Reporting** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Relatórios de preços Predictix na lista de resultados de Olá](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="df702-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="df702-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="df702-136">Nesta secção, configure e teste do Azure AD-início de sessão único com Predictix preços relatórios com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="df702-136">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df702-137">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá no relatório de preços Predictix é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df702-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Price Reporting is tooa user in Azure AD.</span></span> <span data-ttu-id="df702-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Predictix preços Reporting necessita de toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="df702-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Price Reporting needs toobe established.</span></span>

<span data-ttu-id="df702-139">No relatório de preços Predictix, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="df702-139">In Predictix Price Reporting, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="df702-140">tooconfigure e teste do Azure AD-início de sessão único, com preços de Predictix relatórios, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="df702-140">tooconfigure and test Azure AD single sign-on with Predictix Price Reporting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="df702-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="df702-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="df702-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df702-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df702-143">**[Criar um utilizador de teste Predictix preços Reporting](#create-a-predictix-price-reporting-test-user)**  -toohave um homólogo de Britta Simon na Predictix preços relatórios que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="df702-143">**[Create a Predictix Price Reporting test user](#create-a-predictix-price-reporting-test-user)** - toohave a counterpart of Britta Simon in Predictix Price Reporting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="df702-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="df702-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df702-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="df702-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="df702-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="df702-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="df702-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Predictix preços Reporting.</span><span class="sxs-lookup"><span data-stu-id="df702-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="df702-148">**tooconfigure do Azure AD-início de sessão único, com preços Predictix Reporting Services, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="df702-148">**tooconfigure Azure AD single sign-on with Predictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="df702-149">No Olá portal do Azure, no Olá **Predictix preços Reporting** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="df702-149">In hello Azure portal, on hello **Predictix Price Reporting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="df702-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="df702-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. <span data-ttu-id="df702-153">No Olá **Predictix preços Reporting domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="df702-153">On hello **Predictix Price Reporting Domain and URLs** section, perform hello following steps:</span></span>

    ![Predictix preços Reporting domínio e os URLs únicos de informações de início de sessão](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    <span data-ttu-id="df702-155">a.</span><span class="sxs-lookup"><span data-stu-id="df702-155">a.</span></span> <span data-ttu-id="df702-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<companyname-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="df702-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.predictix.com/sso/request`</span></span>

    <span data-ttu-id="df702-157">b.</span><span class="sxs-lookup"><span data-stu-id="df702-157">b.</span></span> <span data-ttu-id="df702-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:</span><span class="sxs-lookup"><span data-stu-id="df702-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="df702-159">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="df702-159">These values are not real.</span></span> <span data-ttu-id="df702-160">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="df702-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="df702-161">Contacte [equipa de suporte de cliente de relatórios de preços em Predictix](http://www.infor.com/company/customer-center/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="df702-161">Contact [Predictix Price Reporting Client support team](http://www.infor.com/company/customer-center/) tooget these values.</span></span> 
 
4. <span data-ttu-id="df702-162">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="df702-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. <span data-ttu-id="df702-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="df702-164">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="df702-166">No Olá **Predictix preços Reporting Configuration** secção, clique em **configurar relatórios de preços Predictix** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="df702-166">On hello **Predictix Price Reporting Configuration** section, click **Configure Predictix Price Reporting** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="df702-167">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="df702-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de relatórios Predictix preço](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. <span data-ttu-id="df702-169">tooconfigure-início de sessão único em **Predictix preços Reporting** lado, terá de Olá toosend transferido **certificado (Base64)**, **Sign-Out URL, ID de entidade de SAML e SAML Single Sign-On URL do serviço** demasiado[equipa de suporte de relatórios de preços Predictix](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="df702-169">tooconfigure single sign-on on **Predictix Price Reporting** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Price Reporting support team](http://www.infor.com/company/customer-center/).</span></span> <span data-ttu-id="df702-170">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="df702-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="df702-171">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="df702-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="df702-172">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="df702-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="df702-173">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df702-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="df702-174">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df702-174">Create an Azure AD test user</span></span>

<span data-ttu-id="df702-175">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="df702-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="df702-177">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="df702-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="df702-178">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="df702-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="df702-180">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="df702-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="df702-182">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df702-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="df702-184">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="df702-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="df702-186">a.</span><span class="sxs-lookup"><span data-stu-id="df702-186">a.</span></span> <span data-ttu-id="df702-187">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df702-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df702-188">b.</span><span class="sxs-lookup"><span data-stu-id="df702-188">b.</span></span> <span data-ttu-id="df702-189">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df702-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="df702-190">c.</span><span class="sxs-lookup"><span data-stu-id="df702-190">c.</span></span> <span data-ttu-id="df702-191">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="df702-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="df702-192">d.</span><span class="sxs-lookup"><span data-stu-id="df702-192">d.</span></span> <span data-ttu-id="df702-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="df702-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-price-reporting-test-user"></a><span data-ttu-id="df702-194">Criar um utilizador de teste Predictix preços relatórios</span><span class="sxs-lookup"><span data-stu-id="df702-194">Create a Predictix Price Reporting test user</span></span>

<span data-ttu-id="df702-195">Nesta secção, vai criar um utilizador chamado Britta Simon no relatório de preços Predictix.</span><span class="sxs-lookup"><span data-stu-id="df702-195">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="df702-196">Trabalhar com [equipa de suporte de relatórios de preços Predictix](http://www.infor.com/company/customer-center/) utilizadores de Olá tooadd na plataforma de relatórios de preços Predictix Olá.</span><span class="sxs-lookup"><span data-stu-id="df702-196">Work with [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/) tooadd hello users in hello Predictix Price Reporting platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="df702-197">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df702-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="df702-198">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo tooPredictix de acesso a relatórios de preços.</span><span class="sxs-lookup"><span data-stu-id="df702-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Price Reporting.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="df702-200">**tooassign tooPredictix Britta Simon preços relatórios, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="df702-200">**tooassign Britta Simon tooPredictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="df702-201">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="df702-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="df702-203">Na lista de aplicações de Olá, selecione **Predictix preços Reporting**.</span><span class="sxs-lookup"><span data-stu-id="df702-203">In hello applications list, select **Predictix Price Reporting**.</span></span>

    ![ligação de relatórios de preços Predictix Olá na lista de aplicações de Olá](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. <span data-ttu-id="df702-205">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="df702-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="df702-207">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="df702-207">Click **Add** button.</span></span> <span data-ttu-id="df702-208">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df702-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="df702-210">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="df702-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="df702-211">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df702-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df702-212">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df702-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="df702-213">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="df702-213">Test single sign-on</span></span>

<span data-ttu-id="df702-214">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="df702-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="df702-215">Ao clicar em mosaico de relatórios de preços Predictix Olá no painel de acesso de Olá, deve obter a aplicação de relatórios de preços Predictix tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="df702-215">When you click hello Predictix Price Reporting tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df702-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="df702-216">Additional resources</span></span>

* [<span data-ttu-id="df702-217">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df702-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df702-218">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df702-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png

