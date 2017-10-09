---
title: "Tutorial: Integração do Azure Active Directory com ADP eTime | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="1abcb-103">Tutorial: Integração do Azure Active Directory com ADP eTime</span><span class="sxs-lookup"><span data-stu-id="1abcb-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="1abcb-104">Neste tutorial, saiba como toointegrate ADP eTime com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1abcb-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1abcb-105">Integrar ADP eTime com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="1abcb-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1abcb-106">Pode controlar no Azure AD que tenha acesso tooADP eTime</span><span class="sxs-lookup"><span data-stu-id="1abcb-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="1abcb-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooADP eTime (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1abcb-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1abcb-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1abcb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1abcb-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1abcb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1abcb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1abcb-110">Prerequisites</span></span>

<span data-ttu-id="1abcb-111">integração do Azure AD com ADP eTime tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1abcb-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="1abcb-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1abcb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1abcb-113">Um ADP eTime-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="1abcb-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1abcb-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1abcb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1abcb-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1abcb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1abcb-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1abcb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1abcb-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1abcb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1abcb-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1abcb-118">Scenario description</span></span>
<span data-ttu-id="1abcb-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1abcb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1abcb-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="1abcb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1abcb-121">Adicionar ADP eTime da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="1abcb-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="1abcb-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="1abcb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="1abcb-123">Adicionar ADP eTime da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="1abcb-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="1abcb-124">tooconfigure Olá integração de ADP eTime com o Azure AD, é necessário tooadd ADP eTime Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="1abcb-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1abcb-125">**tooadd ADP eTime da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1abcb-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1abcb-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="1abcb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1abcb-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1abcb-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="1abcb-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1abcb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="1abcb-133">Na caixa de pesquisa de Olá, escreva **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-133">In hello search box, type **ADP eTime**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="1abcb-135">No painel de resultados de Olá, selecione **ADP eTime**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="1abcb-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1abcb-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="1abcb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1abcb-138">Nesta secção, configure e teste do Azure AD-início de sessão único com eTime ADP com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1abcb-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1abcb-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá ADP eTime é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1abcb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="1abcb-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá ADP eTime tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1abcb-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="1abcb-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="1abcb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="1abcb-142">tooconfigure e teste do Azure AD-início de sessão único com ADP eTime, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1abcb-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1abcb-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="1abcb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1abcb-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1abcb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1abcb-145">**[Criar um utilizador de teste de eTime ADP](#creating-an-adp-etime-test-user)**  -toohave um homólogo de Britta Simon no eTime ADP que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="1abcb-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1abcb-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="1abcb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1abcb-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="1abcb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1abcb-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="1abcb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1abcb-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="1abcb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="1abcb-150">**tooconfigure do Azure AD-início de sessão único com ADP eTime, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1abcb-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="1abcb-151">No Olá portal do Azure, no Olá **ADP eTime** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="1abcb-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="1abcb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="1abcb-155">No Olá **ADP eTime domínio e os URLs** secção, execute Olá passo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1abcb-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="1abcb-157">a.</span><span class="sxs-lookup"><span data-stu-id="1abcb-157">a.</span></span> <span data-ttu-id="1abcb-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="1abcb-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="1abcb-159">b.</span><span class="sxs-lookup"><span data-stu-id="1abcb-159">b.</span></span> <span data-ttu-id="1abcb-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="1abcb-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="1abcb-161">Estes valores não estiverem Olá real.</span><span class="sxs-lookup"><span data-stu-id="1abcb-161">These values are not hello real.</span></span> <span data-ttu-id="1abcb-162">Atualize estes valores com o URL de resposta real Olá e o identificador.</span><span class="sxs-lookup"><span data-stu-id="1abcb-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="1abcb-163">Contacte [equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="1abcb-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="1abcb-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="1abcb-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="1abcb-166">Olá aplicação de eTime ADP espera asserções de SAML Olá num formato específico, que requer tooadd atributo personalizado mapeamentos tooyour configuração SAML do token de atributos.</span><span class="sxs-lookup"><span data-stu-id="1abcb-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="1abcb-167">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="1abcb-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="1abcb-168">Olá afirmação nome será sempre **"PersonImmutableID"** e valor Olá que podemos ter mapeado os tooExtensionAttribute2 que contém Olá campo IDdeEmpregado do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="1abcb-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="1abcb-169">Aqui mapeamento de utilizador de Olá do Azure AD tooADP eTime será efetuado em Olá campo IDdeEmpregado, mas pode mapear este valor diferente de tooa também com base nas suas definições de aplicação.</span><span class="sxs-lookup"><span data-stu-id="1abcb-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="1abcb-170">Por isso, consulte o trabalho com [equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx) toouse primeiro Olá identificador correto de um utilizador e esse valor com Olá do mapa **"PersonImmutableID"** de afirmação.</span><span class="sxs-lookup"><span data-stu-id="1abcb-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="1abcb-172">No Olá **atributos de utilizador** secção em Olá **de sessão único-** caixa de diálogo, configurar atributos token SAML, conforme mostrado na imagem de Olá e efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="1abcb-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="1abcb-173">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="1abcb-173">Attribute Name</span></span> | <span data-ttu-id="1abcb-174">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="1abcb-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="1abcb-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="1abcb-175">PersonImmutableID</span></span> | <span data-ttu-id="1abcb-176">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="1abcb-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="1abcb-177">a.</span><span class="sxs-lookup"><span data-stu-id="1abcb-177">a.</span></span> <span data-ttu-id="1abcb-178">Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1abcb-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1abcb-181">b.</span><span class="sxs-lookup"><span data-stu-id="1abcb-181">b.</span></span> <span data-ttu-id="1abcb-182">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="1abcb-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="1abcb-183">c.</span><span class="sxs-lookup"><span data-stu-id="1abcb-183">c.</span></span> <span data-ttu-id="1abcb-184">De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="1abcb-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1abcb-185">d.</span><span class="sxs-lookup"><span data-stu-id="1abcb-185">d.</span></span> <span data-ttu-id="1abcb-186">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1abcb-187">Antes de poder configurar de asserção SAML Olá, terá de toocontact sua [equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx) e valor de Olá do atributo de identificador exclusivo de Olá de pedido para o seu inquilino.</span><span class="sxs-lookup"><span data-stu-id="1abcb-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="1abcb-188">É necessário este valor tooconfigure Olá afirmação personalizada para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="1abcb-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="1abcb-189">No Olá **ADP eTime configuração** secção, clique em **configurar ADP eTime** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="1abcb-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="1abcb-191">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="1abcb-191">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="1abcb-193">tooconfigure-início de sessão único em **ADP eTime** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="1abcb-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="1abcb-194">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="1abcb-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1abcb-195">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="1abcb-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1abcb-196">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1abcb-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1abcb-197">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1abcb-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="1abcb-198">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1abcb-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="1abcb-200">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1abcb-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1abcb-201">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="1abcb-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1abcb-203">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1abcb-205">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="1abcb-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1abcb-207">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="1abcb-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1abcb-209">a.</span><span class="sxs-lookup"><span data-stu-id="1abcb-209">a.</span></span> <span data-ttu-id="1abcb-210">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1abcb-211">b.</span><span class="sxs-lookup"><span data-stu-id="1abcb-211">b.</span></span> <span data-ttu-id="1abcb-212">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1abcb-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1abcb-213">c.</span><span class="sxs-lookup"><span data-stu-id="1abcb-213">c.</span></span> <span data-ttu-id="1abcb-214">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1abcb-215">d.</span><span class="sxs-lookup"><span data-stu-id="1abcb-215">d.</span></span> <span data-ttu-id="1abcb-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="1abcb-217">Criar um utilizador de teste de eTime ADP</span><span class="sxs-lookup"><span data-stu-id="1abcb-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="1abcb-218">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="1abcb-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="1abcb-219">Trabalhar com [equipa de suporte de eTime ADP](https://www.adp.com/contact-us/overview.aspx) utilizadores de Olá tooadd na conta de eTime Olá ADP.</span><span class="sxs-lookup"><span data-stu-id="1abcb-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1abcb-220">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1abcb-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1abcb-221">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooADP eTime.</span><span class="sxs-lookup"><span data-stu-id="1abcb-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="1abcb-223">**tooassign Britta Simon tooADP eTime, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1abcb-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="1abcb-224">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="1abcb-226">Na lista de aplicações de Olá, selecione **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="1abcb-228">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1abcb-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="1abcb-230">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="1abcb-230">Click **Add** button.</span></span> <span data-ttu-id="1abcb-231">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1abcb-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="1abcb-233">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="1abcb-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1abcb-234">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1abcb-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1abcb-235">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1abcb-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1abcb-236">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="1abcb-236">Testing single sign-on</span></span>

<span data-ttu-id="1abcb-237">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="1abcb-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1abcb-238">Ao clicar em mosaico de eTime ADP Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour ADP eTime aplicação.</span><span class="sxs-lookup"><span data-stu-id="1abcb-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="1abcb-239">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1abcb-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1abcb-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1abcb-240">Additional resources</span></span>

* [<span data-ttu-id="1abcb-241">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1abcb-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1abcb-242">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1abcb-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

