---
title: "Tutorial: Integração do Azure Active Directory com Allocadia | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a01c232f9dc50e690dd348430899db9c13f1564
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="df384-103">Tutorial: Integração do Azure Active Directory com Allocadia</span><span class="sxs-lookup"><span data-stu-id="df384-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="df384-104">Neste tutorial, saiba como toointegrate Allocadia com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df384-104">In this tutorial, you learn how toointegrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df384-105">Integrar Allocadia com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="df384-105">Integrating Allocadia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="df384-106">Pode controlar no Azure AD que tenha acesso tooAllocadia</span><span class="sxs-lookup"><span data-stu-id="df384-106">You can control in Azure AD who has access tooAllocadia</span></span>
- <span data-ttu-id="df384-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooAllocadia (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df384-107">You can enable your users tooautomatically get signed-on tooAllocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="df384-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="df384-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="df384-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df384-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df384-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="df384-110">Prerequisites</span></span>

<span data-ttu-id="df384-111">integração do Azure AD com Allocadia tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="df384-111">tooconfigure Azure AD integration with Allocadia, you need hello following items:</span></span>

- <span data-ttu-id="df384-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df384-112">An Azure AD subscription</span></span>
- <span data-ttu-id="df384-113">Um Allocadia início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="df384-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="df384-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="df384-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="df384-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="df384-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="df384-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="df384-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="df384-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df384-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df384-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="df384-118">Scenario description</span></span>
<span data-ttu-id="df384-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="df384-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="df384-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="df384-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df384-121">Adicionar Allocadia da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="df384-121">Adding Allocadia from hello gallery</span></span>
2. <span data-ttu-id="df384-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="df384-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-hello-gallery"></a><span data-ttu-id="df384-123">Adicionar Allocadia da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="df384-123">Adding Allocadia from hello gallery</span></span>
<span data-ttu-id="df384-124">tooconfigure Olá integração de Allocadia com o Azure AD, é necessário tooadd Allocadia Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="df384-124">tooconfigure hello integration of Allocadia into Azure AD, you need tooadd Allocadia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="df384-125">**tooadd Allocadia da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="df384-125">**tooadd Allocadia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="df384-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="df384-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="df384-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="df384-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="df384-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="df384-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="df384-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df384-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="df384-133">Na caixa de pesquisa de Olá, escreva **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="df384-133">In hello search box, type **Allocadia**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="df384-135">No painel de resultados de Olá, selecione **Allocadia**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="df384-135">In hello results panel, select **Allocadia**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df384-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="df384-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df384-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Allocadia com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="df384-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="df384-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Allocadia é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df384-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Allocadia is tooa user in Azure AD.</span></span> <span data-ttu-id="df384-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Allocadia tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="df384-140">In other words, a link relationship between an Azure AD user and hello related user in Allocadia needs toobe established.</span></span>

<span data-ttu-id="df384-141">No Allocadia, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="df384-141">In Allocadia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="df384-142">tooconfigure e teste do Azure AD-início de sessão único com Allocadia, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="df384-142">tooconfigure and test Azure AD single sign-on with Allocadia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="df384-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="df384-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="df384-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df384-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df384-145">**[Criar um utilizador de teste Allocadia](#creating-an-allocadia-test-user)**  -toohave um homólogo de Britta Simon no Allocadia é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="df384-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - toohave a counterpart of Britta Simon in Allocadia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="df384-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="df384-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df384-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="df384-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="df384-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="df384-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="df384-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Allocadia.</span><span class="sxs-lookup"><span data-stu-id="df384-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="df384-150">**tooconfigure do Azure AD-início de sessão único com Allocadia, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="df384-150">**tooconfigure Azure AD single sign-on with Allocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="df384-151">No Olá portal do Azure, no Olá **Allocadia** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="df384-151">In hello Azure portal, on hello **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="df384-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="df384-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="df384-155">No Olá **Allocadia domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="df384-155">On hello **Allocadia Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="df384-157">a.</span><span class="sxs-lookup"><span data-stu-id="df384-157">a.</span></span> <span data-ttu-id="df384-158">No Olá **identificador** caixa de texto, escreva um URL através de Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="df384-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
       
     <span data-ttu-id="df384-159">Para o ambiente de teste-`https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="df384-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="df384-160">Para o ambiente de produção-`https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="df384-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="df384-161">b.</span><span class="sxs-lookup"><span data-stu-id="df384-161">b.</span></span> <span data-ttu-id="df384-162">No Olá **URL de resposta** caixa de texto, escreva um URL através de Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="df384-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
     <span data-ttu-id="df384-163">Para o ambiente de teste-`https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="df384-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="df384-164">Para o ambiente de produção-`https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="df384-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="df384-165">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="df384-165">These values are not real.</span></span> <span data-ttu-id="df384-166">Atualize estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="df384-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="df384-167">Contacte [equipa de suporte de Allocadia](mailTo:support@allocadia.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="df384-167">Contact [Allocadia support team](mailTo:support@allocadia.com) tooget these values.</span></span>

4. <span data-ttu-id="df384-168">Aplicação de Allocadia espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="df384-168">Allocadia application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="df384-169">Configure Olá seguintes afirmações para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="df384-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="df384-170">Pode gerir os valores de Olá destes atributos a partir de Olá "**atributos de utilizador**" secção na página de integração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="df384-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="df384-171">Olá seguinte captura de ecrã mostra um exemplo para esta configuração.</span><span class="sxs-lookup"><span data-stu-id="df384-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="df384-173">No Olá **atributos de utilizador** secção em Olá **de sessão único-** caixa de diálogo, configurar atributos token SAML, conforme mostrado na imagem de Olá e efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="df384-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="df384-174">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="df384-174">Attribute Name</span></span> | <span data-ttu-id="df384-175">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="df384-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="df384-176">nome próprio</span><span class="sxs-lookup"><span data-stu-id="df384-176">firstname</span></span> | <span data-ttu-id="df384-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="df384-177">user.givenname</span></span> |
    | <span data-ttu-id="df384-178">Apelido</span><span class="sxs-lookup"><span data-stu-id="df384-178">lastname</span></span> | <span data-ttu-id="df384-179">User.Surname</span><span class="sxs-lookup"><span data-stu-id="df384-179">user.surname</span></span> |
    | <span data-ttu-id="df384-180">Correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="df384-180">email</span></span> | <span data-ttu-id="df384-181">User.Mail</span><span class="sxs-lookup"><span data-stu-id="df384-181">user.mail</span></span> |
    
    <span data-ttu-id="df384-182">a.</span><span class="sxs-lookup"><span data-stu-id="df384-182">a.</span></span> <span data-ttu-id="df384-183">Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df384-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="df384-185">b.</span><span class="sxs-lookup"><span data-stu-id="df384-185">b.</span></span> <span data-ttu-id="df384-186">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="df384-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="df384-188">c.</span><span class="sxs-lookup"><span data-stu-id="df384-188">c.</span></span> <span data-ttu-id="df384-189">De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="df384-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
 
    <span data-ttu-id="df384-190">d.</span><span class="sxs-lookup"><span data-stu-id="df384-190">d.</span></span> <span data-ttu-id="df384-191">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="df384-191">Click **Ok**.</span></span>



6. <span data-ttu-id="df384-192">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="df384-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="df384-194">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="df384-194">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="df384-196">tooconfigure-início de sessão único em **Allocadia** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="df384-196">tooconfigure single sign-on on **Allocadia** side, you need toosend hello downloaded **Metadata XML** too[Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="df384-197">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="df384-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="df384-198">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="df384-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="df384-199">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="df384-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="df384-200">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="df384-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="df384-201">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df384-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="df384-202">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="df384-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="df384-204">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="df384-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="df384-205">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="df384-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="df384-207">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="df384-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="df384-209">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="df384-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="df384-211">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="df384-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="df384-213">a.</span><span class="sxs-lookup"><span data-stu-id="df384-213">a.</span></span> <span data-ttu-id="df384-214">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df384-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="df384-215">b.</span><span class="sxs-lookup"><span data-stu-id="df384-215">b.</span></span> <span data-ttu-id="df384-216">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="df384-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="df384-217">c.</span><span class="sxs-lookup"><span data-stu-id="df384-217">c.</span></span> <span data-ttu-id="df384-218">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="df384-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="df384-219">d.</span><span class="sxs-lookup"><span data-stu-id="df384-219">d.</span></span> <span data-ttu-id="df384-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="df384-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="df384-221">Criar um utilizador de teste Allocadia</span><span class="sxs-lookup"><span data-stu-id="df384-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="df384-222">Aplicação suporta apenas o aprovisionamento de utilizadores de tempo.</span><span class="sxs-lookup"><span data-stu-id="df384-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="df384-223">Após a autenticação de utilizadores são criados na aplicação Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="df384-223">After authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="df384-224">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df384-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="df384-225">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooAllocadia.</span><span class="sxs-lookup"><span data-stu-id="df384-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAllocadia.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="df384-227">**tooassign Britta Simon tooAllocadia, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="df384-227">**tooassign Britta Simon tooAllocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="df384-228">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="df384-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="df384-230">Na lista de aplicações de Olá, selecione **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="df384-230">In hello applications list, select **Allocadia**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="df384-232">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="df384-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="df384-234">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="df384-234">Click **Add** button.</span></span> <span data-ttu-id="df384-235">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df384-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="df384-237">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="df384-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="df384-238">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df384-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="df384-239">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="df384-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="df384-240">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="df384-240">Testing single sign-on</span></span>

<span data-ttu-id="df384-241">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="df384-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="df384-242">Ao clicar em mosaico de Allocadia Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Allocadia aplicação.</span><span class="sxs-lookup"><span data-stu-id="df384-242">When you click hello Allocadia tile in hello Access Panel, you should get automatically signed-on tooyour Allocadia application.</span></span>
<span data-ttu-id="df384-243">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="df384-243">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df384-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="df384-244">Additional resources</span></span>

* [<span data-ttu-id="df384-245">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df384-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df384-246">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df384-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

