---
title: "Tutorial: Integração do Azure Active Directory com Zendesk | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e do Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="32a0a-103">Tutorial: Integração do Azure Active Directory com Zendesk</span><span class="sxs-lookup"><span data-stu-id="32a0a-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="32a0a-104">Neste tutorial, saiba como toointegrate Zendesk com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32a0a-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32a0a-105">Integração do Zendesk com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="32a0a-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32a0a-106">Pode controlar no Azure AD que tenha acesso tooZendesk</span><span class="sxs-lookup"><span data-stu-id="32a0a-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="32a0a-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooZendesk (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a0a-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32a0a-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="32a0a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32a0a-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32a0a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32a0a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="32a0a-110">Prerequisites</span></span>

<span data-ttu-id="32a0a-111">integração do Azure AD com Zendesk tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="32a0a-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="32a0a-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32a0a-113">Um Zendesk-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="32a0a-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="32a0a-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="32a0a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="32a0a-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="32a0a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32a0a-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="32a0a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32a0a-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32a0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="32a0a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="32a0a-118">Scenario description</span></span>
<span data-ttu-id="32a0a-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="32a0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32a0a-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="32a0a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32a0a-121">A adição do Zendesk da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="32a0a-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="32a0a-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="32a0a-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="32a0a-123">A adição do Zendesk da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="32a0a-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="32a0a-124">tooconfigure Olá integração do Zendesk com o Azure AD, é necessário tooadd Zendesk Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="32a0a-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32a0a-125">**tooadd Zendesk da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="32a0a-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32a0a-126">No Olá  **[Portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="32a0a-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32a0a-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32a0a-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="32a0a-131">Clique em **nova aplicação** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="32a0a-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="32a0a-133">Na caixa de pesquisa de Olá, escreva **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-133">In hello search box, type **Zendesk**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="32a0a-135">No painel de resultados de Olá, selecione **Zendesk**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="32a0a-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32a0a-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="32a0a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32a0a-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Zendesk com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="32a0a-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32a0a-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Zendesk é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a0a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="32a0a-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Zendesk tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="32a0a-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="32a0a-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Zendesk.</span><span class="sxs-lookup"><span data-stu-id="32a0a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="32a0a-142">tooconfigure e teste do Azure AD-início de sessão único com Zendesk, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="32a0a-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32a0a-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="32a0a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32a0a-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32a0a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32a0a-145">**[Criar um utilizador de teste do Zendesk](#creating-a-zendesk-test-user)**  -toohave um homólogo de Britta Simon no Zendesk é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="32a0a-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="32a0a-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="32a0a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32a0a-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="32a0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32a0a-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="32a0a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32a0a-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação do Zendesk.</span><span class="sxs-lookup"><span data-stu-id="32a0a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="32a0a-150">**tooconfigure do Azure AD-início de sessão único com Zendesk, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="32a0a-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="32a0a-151">No Olá portal do Azure, no Olá **Zendesk** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="32a0a-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="32a0a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="32a0a-155">No Olá **URLs de domínio do Zendesk e** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="32a0a-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="32a0a-157">a.</span><span class="sxs-lookup"><span data-stu-id="32a0a-157">a.</span></span> <span data-ttu-id="32a0a-158">No Olá **URL de início de sessão** caixa de texto, o valor do tipo Olá Olá seguir o padrão de utilização:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="32a0a-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="32a0a-159">b.</span><span class="sxs-lookup"><span data-stu-id="32a0a-159">b.</span></span> <span data-ttu-id="32a0a-160">No Olá **identificador** caixa de texto, o valor do tipo Olá Olá seguir o padrão de utilização:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="32a0a-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32a0a-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="32a0a-161">These values are not real.</span></span> <span data-ttu-id="32a0a-162">Atualize estes valores com Olá real início de sessão no URL e o URL de identificador.</span><span class="sxs-lookup"><span data-stu-id="32a0a-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="32a0a-163">Contacte [equipa de suporte do Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="32a0a-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="32a0a-164">Zendesk espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="32a0a-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="32a0a-165">Existem não existem atributos SAML obrigatórios, mas, opcionalmente, pode adicionar um atributo de **atributos de utilizador** secção por Olá seguinte passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="32a0a-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Configurar o início de sessão único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="32a0a-167">a.</span><span class="sxs-lookup"><span data-stu-id="32a0a-167">a.</span></span> <span data-ttu-id="32a0a-168">Clique em Olá **Olá, ver e editar todos os outros atributos** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="32a0a-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Configurar o início de sessão único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="32a0a-170">b.</span><span class="sxs-lookup"><span data-stu-id="32a0a-170">b.</span></span> <span data-ttu-id="32a0a-171">Clique em Olá **adicionar atributo** tooopen **adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32a0a-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="32a0a-173">c.</span><span class="sxs-lookup"><span data-stu-id="32a0a-173">c.</span></span> <span data-ttu-id="32a0a-174">No Olá **nome** caixa de texto, o nome de atributo do tipo Olá (por exemplo **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="32a0a-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="32a0a-175">d.</span><span class="sxs-lookup"><span data-stu-id="32a0a-175">d.</span></span> <span data-ttu-id="32a0a-176">De Olá **valor** lista, o valor do atributo Olá selecione (como **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="32a0a-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="32a0a-177">e.</span><span class="sxs-lookup"><span data-stu-id="32a0a-177">e.</span></span> <span data-ttu-id="32a0a-178">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="32a0a-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="32a0a-179">Utilize tooadd de atributos de atributos de extensão que não estão no Azure AD por predefinição.</span><span class="sxs-lookup"><span data-stu-id="32a0a-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="32a0a-180">Clique em [atributos de utilizador que podem ser definidos no SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget lista completa de Olá de SAML atributos que **Zendesk** aceita.</span><span class="sxs-lookup"><span data-stu-id="32a0a-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="32a0a-181">No Olá **certificado de assinatura de SAML** secção, Olá cópia **THUMBPRINT** valor do certificado.</span><span class="sxs-lookup"><span data-stu-id="32a0a-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="32a0a-183">No Olá **Zendesk configuração** secção, clique em **configurar Zendesk** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="32a0a-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="32a0a-184">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="32a0a-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="32a0a-186">Numa janela do browser web diferente, inicie sessão no site da sua empresa Zendesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="32a0a-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="32a0a-187">Clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-187">Click **Admin**.</span></span>

9. <span data-ttu-id="32a0a-188">No painel de navegação esquerdo Olá, clique em **definições**e, em seguida, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="32a0a-189">No Olá **segurança** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="32a0a-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="32a0a-190">![Segurança](./media/active-directory-saas-zendesk-tutorial/ic773089.png "segurança")</span><span class="sxs-lookup"><span data-stu-id="32a0a-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="32a0a-191">![De sessão único-](./media/active-directory-saas-zendesk-tutorial/ic773090.png "de sessão único-")</span><span class="sxs-lookup"><span data-stu-id="32a0a-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="32a0a-192">a.</span><span class="sxs-lookup"><span data-stu-id="32a0a-192">a.</span></span> <span data-ttu-id="32a0a-193">Clique em Olá **Admin & agentes** separador.</span><span class="sxs-lookup"><span data-stu-id="32a0a-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="32a0a-194">b.</span><span class="sxs-lookup"><span data-stu-id="32a0a-194">b.</span></span> <span data-ttu-id="32a0a-195">Selecione **único início de sessão (SSO) e SAML**e, em seguida, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="32a0a-196">c.</span><span class="sxs-lookup"><span data-stu-id="32a0a-196">c.</span></span> <span data-ttu-id="32a0a-197">No **SAML SSO URL** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32a0a-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="32a0a-198">d.</span><span class="sxs-lookup"><span data-stu-id="32a0a-198">d.</span></span> <span data-ttu-id="32a0a-199">No **URL de fim de sessão remoto** caixa de texto, colar Olá valor **Sign-Out URL** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32a0a-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="32a0a-200">e.</span><span class="sxs-lookup"><span data-stu-id="32a0a-200">e.</span></span> <span data-ttu-id="32a0a-201">No **impressão digital do certificado** caixa de texto, colar Olá **Thumbprint** valor do certificado que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32a0a-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="32a0a-202">f.</span><span class="sxs-lookup"><span data-stu-id="32a0a-202">f.</span></span> <span data-ttu-id="32a0a-203">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32a0a-204">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a0a-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="32a0a-205">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32a0a-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="32a0a-207">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="32a0a-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32a0a-208">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="32a0a-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32a0a-210">lista de Olá toodisplay de utilizadores aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32a0a-212">Na parte superior de Olá da caixa de diálogo Olá, clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32a0a-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32a0a-214">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="32a0a-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32a0a-216">a.</span><span class="sxs-lookup"><span data-stu-id="32a0a-216">a.</span></span> <span data-ttu-id="32a0a-217">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32a0a-218">b.</span><span class="sxs-lookup"><span data-stu-id="32a0a-218">b.</span></span> <span data-ttu-id="32a0a-219">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32a0a-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32a0a-220">c.</span><span class="sxs-lookup"><span data-stu-id="32a0a-220">c.</span></span> <span data-ttu-id="32a0a-221">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32a0a-222">d.</span><span class="sxs-lookup"><span data-stu-id="32a0a-222">d.</span></span> <span data-ttu-id="32a0a-223">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="32a0a-224">Criar um utilizador de teste do Zendesk</span><span class="sxs-lookup"><span data-stu-id="32a0a-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="32a0a-225">tooenable do Azure AD os utilizadores toolog para **Zendesk**, têm de ser aprovisionados para **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="32a0a-226">Dependendo da função de Olá atribuída Olá aplicações, de Olá esperado comportamento:</span><span class="sxs-lookup"><span data-stu-id="32a0a-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="32a0a-227">**Utilizador final** contas são aprovisionadas automaticamente quando iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="32a0a-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="32a0a-228">**Agente** e **Admin** contas precisam de toobe aprovisionada manualmente no **Zendesk** antes de iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="32a0a-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="32a0a-229">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="32a0a-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="32a0a-230">Inicie sessão no tooyour **Zendesk** inquilino.</span><span class="sxs-lookup"><span data-stu-id="32a0a-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="32a0a-231">Selecione Olá **cliente lista** separador.</span><span class="sxs-lookup"><span data-stu-id="32a0a-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="32a0a-232">Selecione Olá **utilizador** separador e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="32a0a-233">![Adicionar utilizador](./media/active-directory-saas-zendesk-tutorial/ic773632.png "adicionar utilizador")</span><span class="sxs-lookup"><span data-stu-id="32a0a-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="32a0a-234">Escreva o endereço de correio eletrónico Olá de uma conta do Azure AD existente que pretende tooprovision e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="32a0a-235">![Novo utilizador](./media/active-directory-saas-zendesk-tutorial/ic773633.png "novo utilizador")</span><span class="sxs-lookup"><span data-stu-id="32a0a-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="32a0a-236">Pode utilizar quaisquer outras Zendesk utilizador conta criação ferramentas ou APIs fornecidas pelo Zendesk tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="32a0a-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32a0a-237">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a0a-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32a0a-238">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooZendesk.</span><span class="sxs-lookup"><span data-stu-id="32a0a-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="32a0a-240">**tooassign Britta Simon tooZendesk, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="32a0a-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="32a0a-241">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="32a0a-243">Na lista de aplicações de Olá, selecione **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-243">In hello applications list, select **Zendesk**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="32a0a-245">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="32a0a-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="32a0a-247">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="32a0a-247">Click **Add** button.</span></span> <span data-ttu-id="32a0a-248">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32a0a-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="32a0a-250">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="32a0a-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32a0a-251">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32a0a-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32a0a-252">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32a0a-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32a0a-253">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="32a0a-253">Testing single sign-on</span></span>

<span data-ttu-id="32a0a-254">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="32a0a-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="32a0a-255">Ao clicar em mosaico do Zendesk Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Zendesk aplicação.</span><span class="sxs-lookup"><span data-stu-id="32a0a-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="32a0a-256">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="32a0a-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32a0a-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="32a0a-257">Additional resources</span></span>

* [<span data-ttu-id="32a0a-258">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32a0a-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32a0a-259">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32a0a-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
