---
title: "Tutorial: Integração do Azure Active Directory com Boomi | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a><span data-ttu-id="4de55-103">Tutorial: Integração do Azure Active Directory com Boomi</span><span class="sxs-lookup"><span data-stu-id="4de55-103">Tutorial: Azure Active Directory integration with Boomi</span></span>

<span data-ttu-id="4de55-104">Neste tutorial, saiba como toointegrate Boomi com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4de55-104">In this tutorial, you learn how toointegrate Boomi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4de55-105">Integrar Boomi com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="4de55-105">Integrating Boomi with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4de55-106">Pode controlar no Azure AD que tenha acesso tooBoomi</span><span class="sxs-lookup"><span data-stu-id="4de55-106">You can control in Azure AD who has access tooBoomi</span></span>
- <span data-ttu-id="4de55-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooBoomi (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de55-107">You can enable your users tooautomatically get signed-on tooBoomi (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4de55-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4de55-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4de55-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4de55-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4de55-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4de55-110">Prerequisites</span></span>

<span data-ttu-id="4de55-111">integração do Azure AD com Boomi tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4de55-111">tooconfigure Azure AD integration with Boomi, you need hello following items:</span></span>

- <span data-ttu-id="4de55-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de55-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4de55-113">Um Boomi-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="4de55-113">A Boomi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4de55-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4de55-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4de55-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4de55-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4de55-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4de55-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4de55-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4de55-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4de55-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4de55-118">Scenario description</span></span>
<span data-ttu-id="4de55-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4de55-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4de55-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="4de55-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4de55-121">Adicionar Boomi da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="4de55-121">Adding Boomi from hello gallery</span></span>
2. <span data-ttu-id="4de55-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="4de55-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-boomi-from-hello-gallery"></a><span data-ttu-id="4de55-123">Adicionar Boomi da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="4de55-123">Adding Boomi from hello gallery</span></span>
<span data-ttu-id="4de55-124">tooconfigure Olá integração de Boomi com o Azure AD, é necessário tooadd Boomi Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="4de55-124">tooconfigure hello integration of Boomi into Azure AD, you need tooadd Boomi from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4de55-125">**tooadd Boomi da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4de55-125">**tooadd Boomi from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4de55-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="4de55-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4de55-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4de55-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4de55-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="4de55-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="4de55-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4de55-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="4de55-133">Na caixa de pesquisa de Olá, escreva **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="4de55-133">In hello search box, type **Boomi**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. <span data-ttu-id="4de55-135">No painel de resultados de Olá, selecione **Boomi**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="4de55-135">In hello results panel, select **Boomi**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4de55-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="4de55-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4de55-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Boomi com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4de55-138">In this section, you configure and test Azure AD single sign-on with Boomi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4de55-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Boomi é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4de55-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Boomi is tooa user in Azure AD.</span></span> <span data-ttu-id="4de55-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Boomi tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4de55-140">In other words, a link relationship between an Azure AD user and hello related user in Boomi needs toobe established.</span></span>

<span data-ttu-id="4de55-141">No Boomi, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="4de55-141">In Boomi, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4de55-142">tooconfigure e teste do Azure AD-início de sessão único com Boomi, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4de55-142">tooconfigure and test Azure AD single sign-on with Boomi, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4de55-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="4de55-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4de55-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4de55-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4de55-145">**[Criar um utilizador de teste Boomi](#creating-a-boomi-test-user)**  -toohave um homólogo de Britta Simon no Boomi é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="4de55-145">**[Creating a Boomi test user](#creating-a-boomi-test-user)** - toohave a counterpart of Britta Simon in Boomi that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4de55-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="4de55-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4de55-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="4de55-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4de55-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="4de55-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4de55-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Boomi.</span><span class="sxs-lookup"><span data-stu-id="4de55-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Boomi application.</span></span>

<span data-ttu-id="4de55-150">**tooconfigure do Azure AD-início de sessão único com Boomi, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4de55-150">**tooconfigure Azure AD single sign-on with Boomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="4de55-151">No Olá portal do Azure, no Olá **Boomi** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="4de55-151">In hello Azure portal, on hello **Boomi** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="4de55-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="4de55-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. <span data-ttu-id="4de55-155">No Olá **Boomi domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="4de55-155">On hello **Boomi Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    <span data-ttu-id="4de55-157">a.</span><span class="sxs-lookup"><span data-stu-id="4de55-157">a.</span></span> <span data-ttu-id="4de55-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="4de55-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    <span data-ttu-id="4de55-159">b.</span><span class="sxs-lookup"><span data-stu-id="4de55-159">b.</span></span> <span data-ttu-id="4de55-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://platform.boomi.com/sso/<accountname>/saml`</span><span class="sxs-lookup"><span data-stu-id="4de55-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.boomi.com/sso/<accountname>/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4de55-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="4de55-161">These values are not real.</span></span> <span data-ttu-id="4de55-162">Atualize estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="4de55-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="4de55-163">Contacte [equipa de suporte de Boomi](https://boomi.com/company/contact/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="4de55-163">Contact [Boomi support team](https://boomi.com/company/contact/) tooget these values.</span></span>

4. <span data-ttu-id="4de55-164">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="4de55-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. <span data-ttu-id="4de55-166">Aplicação de Boomi espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="4de55-166">Boomi application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="4de55-167">Configure Olá seguintes afirmações para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="4de55-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="4de55-168">Pode gerir os valores de Olá destes atributos a partir de Olá "**atributos de utilizador**" secção na página de integração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="4de55-168">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="4de55-169">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="4de55-169">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="4de55-171">No Olá **atributos de utilizador** secção em Olá **de sessão único-** caixa de diálogo, para cada linha mostrada na tabela de Olá abaixo, efetue Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="4de55-171">In hello **User Attributes** section on hello **Single sign-on** dialog, for each row shown in hello table below, perform hello following steps:</span></span>

    | <span data-ttu-id="4de55-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="4de55-172">Attribute Name</span></span> | <span data-ttu-id="4de55-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="4de55-173">Attribute Value</span></span> |
    | -------------- | --------------- |
    | <span data-ttu-id="4de55-174">FEDERATION_ID</span><span class="sxs-lookup"><span data-stu-id="4de55-174">FEDERATION_ID</span></span> | <span data-ttu-id="4de55-175">User.Mail</span><span class="sxs-lookup"><span data-stu-id="4de55-175">user.mail</span></span> |
    
    <span data-ttu-id="4de55-176">a.</span><span class="sxs-lookup"><span data-stu-id="4de55-176">a.</span></span> <span data-ttu-id="4de55-177">Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4de55-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="4de55-180">b.</span><span class="sxs-lookup"><span data-stu-id="4de55-180">b.</span></span> <span data-ttu-id="4de55-181">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="4de55-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="4de55-182">c.</span><span class="sxs-lookup"><span data-stu-id="4de55-182">c.</span></span> <span data-ttu-id="4de55-183">De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="4de55-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4de55-184">d.</span><span class="sxs-lookup"><span data-stu-id="4de55-184">d.</span></span> <span data-ttu-id="4de55-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4de55-185">Click **Ok**.</span></span>

6. <span data-ttu-id="4de55-186">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="4de55-186">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="4de55-188">No Olá **Boomi configuração** secção, clique em **configurar Boomi** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="4de55-188">On hello **Boomi Configuration** section, click **Configure Boomi** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4de55-189">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4de55-189">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. <span data-ttu-id="4de55-191">Numa janela do browser web diferente, inicie sessão no site da sua empresa Boomi como administrador.</span><span class="sxs-lookup"><span data-stu-id="4de55-191">In a different web browser window, log into your Boomi company site as an administrator.</span></span> 

9. <span data-ttu-id="4de55-192">Navegue demasiado**nome da empresa** e aceda demasiado**configurar**.</span><span class="sxs-lookup"><span data-stu-id="4de55-192">Navigate too**Company Name** and go too**Set up**.</span></span>

10. <span data-ttu-id="4de55-193">Clique em Olá **SSO opções** separador e executar passos abaixo.</span><span class="sxs-lookup"><span data-stu-id="4de55-193">Click hello **SSO Options** tab and perform below steps.</span></span>

    ![Configurar o início de sessão único no lado de aplicação](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    <span data-ttu-id="4de55-195">a.</span><span class="sxs-lookup"><span data-stu-id="4de55-195">a.</span></span> <span data-ttu-id="4de55-196">Verifique **ativar SAML Single Sign-On** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="4de55-196">Check **Enable SAML Single Sign-On** checkbox.</span></span>

    <span data-ttu-id="4de55-197">b.</span><span class="sxs-lookup"><span data-stu-id="4de55-197">b.</span></span> <span data-ttu-id="4de55-198">Clique em **importação** Olá tooupload transferido certificado a partir do Azure AD demasiado**certificado do fornecedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="4de55-198">Click **Import** tooupload hello downloaded certificate from Azure AD too**Identity Provider Certificate**.</span></span>
    
    <span data-ttu-id="4de55-199">c.</span><span class="sxs-lookup"><span data-stu-id="4de55-199">c.</span></span> <span data-ttu-id="4de55-200">No Olá **URL de início de sessão do fornecedor de identidade** caixa de texto, coloque o valor Olá **único início de sessão no URL do serviço SAML** da janela de configuração de aplicação do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4de55-200">In hello **Identity Provider Login URL** textbox, put hello value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="4de55-201">d.</span><span class="sxs-lookup"><span data-stu-id="4de55-201">d.</span></span> <span data-ttu-id="4de55-202">Como **Federação Id localização**, selecione **Id de Federação é no elemento de atributo FEDERATION_ID** botão de opção.</span><span class="sxs-lookup"><span data-stu-id="4de55-202">As **Federation Id Location**, select **Federation Id is in FEDERATION_ID Attribute element** radio button.</span></span> 

    <span data-ttu-id="4de55-203">e.</span><span class="sxs-lookup"><span data-stu-id="4de55-203">e.</span></span> <span data-ttu-id="4de55-204">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="4de55-204">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="4de55-205">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="4de55-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4de55-206">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="4de55-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4de55-207">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4de55-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4de55-208">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de55-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="4de55-209">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4de55-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="4de55-211">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4de55-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4de55-212">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="4de55-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4de55-214">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="4de55-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4de55-216">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="4de55-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4de55-218">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="4de55-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4de55-220">a.</span><span class="sxs-lookup"><span data-stu-id="4de55-220">a.</span></span> <span data-ttu-id="4de55-221">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4de55-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4de55-222">b.</span><span class="sxs-lookup"><span data-stu-id="4de55-222">b.</span></span> <span data-ttu-id="4de55-223">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4de55-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4de55-224">c.</span><span class="sxs-lookup"><span data-stu-id="4de55-224">c.</span></span> <span data-ttu-id="4de55-225">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="4de55-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4de55-226">d.</span><span class="sxs-lookup"><span data-stu-id="4de55-226">d.</span></span> <span data-ttu-id="4de55-227">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4de55-227">Click **Create**.</span></span>
 
### <a name="creating-a-boomi-test-user"></a><span data-ttu-id="4de55-228">Criar um utilizador de teste Boomi</span><span class="sxs-lookup"><span data-stu-id="4de55-228">Creating a Boomi test user</span></span>

<span data-ttu-id="4de55-229">Na ordem tooenable do Azure AD os utilizadores toolog no tooBoomi, têm de ser aprovisionados para Boomi.</span><span class="sxs-lookup"><span data-stu-id="4de55-229">In order tooenable Azure AD users toolog in tooBoomi, they must be provisioned into Boomi.</span></span> <span data-ttu-id="4de55-230">No caso de Olá da Boomi, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4de55-230">In hello case of Boomi, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="4de55-231">tooprovision uma conta de utilizador, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="4de55-231">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="4de55-232">Inicie sessão no tooyour Boomi site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="4de55-232">Log in tooyour Boomi company site as an administrator.</span></span>

2. <span data-ttu-id="4de55-233">Após iniciar sessão, navegue até demasiado**gestão de utilizadores** e aceda demasiado**utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="4de55-233">After logging in, navigate too**User Management** and go too**Users**.</span></span>

    <span data-ttu-id="4de55-234">![Os utilizadores](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="4de55-234">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Users")</span></span>

3. <span data-ttu-id="4de55-235">Clique em  **+**  ícone e Olá **funções de utilizador de adicionar/manter** abre a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4de55-235">Click **+**  icon and hello **Add/Maintain User Roles** dialog opens.</span></span>

    <span data-ttu-id="4de55-236">![Os utilizadores](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="4de55-236">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Users")</span></span>

    <span data-ttu-id="4de55-237">![Os utilizadores](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="4de55-237">![Users](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Users")</span></span>

    <span data-ttu-id="4de55-238">a.</span><span class="sxs-lookup"><span data-stu-id="4de55-238">a.</span></span> <span data-ttu-id="4de55-239">No Olá **endereço de correio eletrónico do utilizador** caixa de texto, como o tipo Olá e-mail do utilizador BrittaSimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4de55-239">In hello **User e-mail address** textbox, type hello email of user like BrittaSimon@contoso.com.</span></span>
    
    <span data-ttu-id="4de55-240">b.</span><span class="sxs-lookup"><span data-stu-id="4de55-240">b.</span></span> <span data-ttu-id="4de55-241">No Olá **nome próprio** caixa de texto, tipo Olá primeiro nome de utilizador como Britta.</span><span class="sxs-lookup"><span data-stu-id="4de55-241">In hello **First name** textbox, type hello First name of user like Britta.</span></span>

    <span data-ttu-id="4de55-242">c.</span><span class="sxs-lookup"><span data-stu-id="4de55-242">c.</span></span> <span data-ttu-id="4de55-243">No Olá **Apelido** caixa de texto, tipo Olá apelido do utilizador como Simon.</span><span class="sxs-lookup"><span data-stu-id="4de55-243">In hello **Last name** textbox, type hello Last name of user like Simon.</span></span>
    
    <span data-ttu-id="4de55-244">d.</span><span class="sxs-lookup"><span data-stu-id="4de55-244">d.</span></span> <span data-ttu-id="4de55-245">Introduza o utilizador Olá **ID de Federação**.</span><span class="sxs-lookup"><span data-stu-id="4de55-245">Enter hello user's **Federation ID**.</span></span> <span data-ttu-id="4de55-246">Cada utilizador tem de ter um ID de federação que identifica exclusivamente o utilizador de Olá numa conta Olá.</span><span class="sxs-lookup"><span data-stu-id="4de55-246">Each user must have a Federation ID that uniquely identifies hello user within hello account.</span></span>
    
    <span data-ttu-id="4de55-247">e.</span><span class="sxs-lookup"><span data-stu-id="4de55-247">e.</span></span> <span data-ttu-id="4de55-248">Atribuir Olá **utilizador padrão** utilizador toohello de função.</span><span class="sxs-lookup"><span data-stu-id="4de55-248">Assign hello **Standard User** role toohello user.</span></span> <span data-ttu-id="4de55-249">Não atribua a função de administrador Olá porque que deverá dar-lhe normal Atmosphere acesso, bem como o acesso de início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="4de55-249">Do not assign hello Administrator role because that would give him normal Atmosphere access as well as single sign-on access.</span></span>
    
    <span data-ttu-id="4de55-250">f.</span><span class="sxs-lookup"><span data-stu-id="4de55-250">f.</span></span> <span data-ttu-id="4de55-251">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4de55-251">Click **OK**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4de55-252">utilizador Olá não irá receber um e-mail de notificação de boas-vindas com uma palavra-passe que pode ser utilizado toolog no toohello AtomSphere conta porque a palavra-passe é gerida através do fornecedor de identidade Olá.</span><span class="sxs-lookup"><span data-stu-id="4de55-252">hello user will not receive a welcome notification email containing a password that can be used toolog in toohello AtomSphere account because his password is managed through hello identity provider.</span></span> <span data-ttu-id="4de55-253">Pode utilizar quaisquer outras Boomi utilizador conta criação ferramentas ou APIs fornecidas pelo Boomi tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="4de55-253">You may use any other Boomi user account creation tools or APIs provided by Boomi tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4de55-254">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de55-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4de55-255">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooBoomi.</span><span class="sxs-lookup"><span data-stu-id="4de55-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBoomi.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="4de55-257">**tooassign Britta Simon tooBoomi, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4de55-257">**tooassign Britta Simon tooBoomi, perform hello following steps:**</span></span>

1. <span data-ttu-id="4de55-258">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="4de55-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="4de55-260">Na lista de aplicações de Olá, selecione **Boomi**.</span><span class="sxs-lookup"><span data-stu-id="4de55-260">In hello applications list, select **Boomi**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. <span data-ttu-id="4de55-262">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4de55-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="4de55-264">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="4de55-264">Click **Add** button.</span></span> <span data-ttu-id="4de55-265">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4de55-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="4de55-267">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="4de55-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4de55-268">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4de55-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4de55-269">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4de55-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4de55-270">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="4de55-270">Testing single sign-on</span></span>

<span data-ttu-id="4de55-271">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="4de55-271">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4de55-272">Ao clicar em mosaico de Boomi Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Boomi aplicação.</span><span class="sxs-lookup"><span data-stu-id="4de55-272">When you click hello Boomi tile in hello Access Panel, you should get automatically signed-on tooyour Boomi application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4de55-273">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4de55-273">Additional resources</span></span>

* [<span data-ttu-id="4de55-274">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4de55-274">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4de55-275">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4de55-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

