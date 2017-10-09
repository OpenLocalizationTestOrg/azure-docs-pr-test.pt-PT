---
title: "Tutorial: Integração do Azure Active Directory com myPolicies | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="d4bdd-103">Tutorial: Integração do Azure Active Directory com myPolicies</span><span class="sxs-lookup"><span data-stu-id="d4bdd-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="d4bdd-104">Neste tutorial, saiba como toointegrate myPolicies com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d4bdd-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d4bdd-105">Integrar myPolicies com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="d4bdd-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d4bdd-106">Pode controlar no Azure AD que tenha acesso toomyPolicies</span><span class="sxs-lookup"><span data-stu-id="d4bdd-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="d4bdd-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada toomyPolicies (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4bdd-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d4bdd-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d4bdd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d4bdd-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d4bdd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4bdd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4bdd-110">Prerequisites</span></span>

<span data-ttu-id="d4bdd-111">integração do Azure AD com myPolicies tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d4bdd-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="d4bdd-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4bdd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d4bdd-113">Um myPolicies-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="d4bdd-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d4bdd-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d4bdd-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d4bdd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d4bdd-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d4bdd-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4bdd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d4bdd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d4bdd-118">Scenario description</span></span>
<span data-ttu-id="d4bdd-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d4bdd-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="d4bdd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d4bdd-121">Adicionar myPolicies da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="d4bdd-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="d4bdd-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="d4bdd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="d4bdd-123">Adicionar myPolicies da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="d4bdd-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="d4bdd-124">tooconfigure Olá integração de myPolicies com o Azure AD, é necessário tooadd myPolicies Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d4bdd-125">**tooadd myPolicies da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d4bdd-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4bdd-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d4bdd-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d4bdd-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="d4bdd-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="d4bdd-133">Na caixa de pesquisa de Olá, escreva **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-133">In hello search box, type **myPolicies**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="d4bdd-135">No painel de resultados de Olá, selecione **myPolicies**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d4bdd-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="d4bdd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d4bdd-138">Nesta secção, configure e teste do Azure AD-início de sessão único com myPolicies com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d4bdd-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d4bdd-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá myPolicies é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="d4bdd-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá myPolicies tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="d4bdd-141">No myPolicies, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d4bdd-142">tooconfigure e teste do Azure AD-início de sessão único com myPolicies, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d4bdd-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d4bdd-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d4bdd-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d4bdd-145">**[Criar um utilizador de teste myPolicies](#creating-a-mypolicies-test-user)**  -toohave um homólogo de Britta Simon no myPolicies é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d4bdd-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d4bdd-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d4bdd-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d4bdd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d4bdd-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação myPolicies.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="d4bdd-150">**tooconfigure do Azure AD-início de sessão único com myPolicies, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d4bdd-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4bdd-151">No Olá portal do Azure, no Olá **myPolicies** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="d4bdd-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="d4bdd-155">No Olá **myPolicies domínios e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="d4bdd-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="d4bdd-157">a.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-157">a.</span></span> <span data-ttu-id="d4bdd-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="d4bdd-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="d4bdd-159">b.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-159">b.</span></span> <span data-ttu-id="d4bdd-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="d4bdd-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d4bdd-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-161">These values are not real.</span></span> <span data-ttu-id="d4bdd-162">Atualize estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="d4bdd-163">Contacte [myPolicies suporta equipa](mailto:support@mypolicies.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="d4bdd-164">aplicação de myPolicies Olá espera asserções de SAML Olá num formato específico, que requer tooadd atributo personalizado mapeamentos tooyour configuração SAML do token de atributos.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="d4bdd-165">Configure Olá seguintes afirmações para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="d4bdd-166">Pode gerir os valores de Olá destes atributos a partir de Olá "**atributos de utilizador**" secção na página de integração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="d4bdd-167">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-167">hello following screenshot shows an example for this.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="d4bdd-169">Clique em **ver e editar todos os outros atributos de utilizador** caixa de verificação no Olá **atributos de utilizador** secção atributos de Olá tooexpand.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="d4bdd-170">Efetuar Olá os seguintes passos em cada um dos atributos de Olá apresentado-</span><span class="sxs-lookup"><span data-stu-id="d4bdd-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="d4bdd-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="d4bdd-171">Attribute Name</span></span> | <span data-ttu-id="d4bdd-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="d4bdd-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="d4bdd-173">givenName</span><span class="sxs-lookup"><span data-stu-id="d4bdd-173">givenname</span></span> | <span data-ttu-id="d4bdd-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="d4bdd-174">user.givenname</span></span> |
    | <span data-ttu-id="d4bdd-175">Apelido</span><span class="sxs-lookup"><span data-stu-id="d4bdd-175">surname</span></span> | <span data-ttu-id="d4bdd-176">User.Surname</span><span class="sxs-lookup"><span data-stu-id="d4bdd-176">user.surname</span></span> |
    | <span data-ttu-id="d4bdd-177">endereço de correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="d4bdd-177">emailaddress</span></span> | <span data-ttu-id="d4bdd-178">User.Mail</span><span class="sxs-lookup"><span data-stu-id="d4bdd-178">user.mail</span></span> |
    | <span data-ttu-id="d4bdd-179">nome</span><span class="sxs-lookup"><span data-stu-id="d4bdd-179">name</span></span> | <span data-ttu-id="d4bdd-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="d4bdd-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="d4bdd-181">a.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-181">a.</span></span> <span data-ttu-id="d4bdd-182">Clique em Olá do Olá atributo tooopen **Editar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="d4bdd-184">b.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-184">b.</span></span> <span data-ttu-id="d4bdd-185">Eliminar o valor do URL de Olá da Olá **espaço de nomes**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="d4bdd-186">c.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-186">c.</span></span> <span data-ttu-id="d4bdd-187">Clique em **Ok** definição de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="d4bdd-188">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="d4bdd-190">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-190">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d4bdd-192">No Olá **myPolicies configuração** secção, clique em **configurar myPolicies** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d4bdd-193">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="d4bdd-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="d4bdd-195">tooconfigure-início de sessão único em **myPolicies** lado, terá de Olá toosend transferido **Certificate(Base64)** e **único início de sessão no URL do serviço SAML** demasiado[myPolicies suporta equipa](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="d4bdd-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="d4bdd-196">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="d4bdd-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d4bdd-197">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d4bdd-198">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d4bdd-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d4bdd-199">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4bdd-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="d4bdd-200">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="d4bdd-202">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d4bdd-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4bdd-203">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d4bdd-205">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d4bdd-207">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d4bdd-209">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="d4bdd-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d4bdd-211">a.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-211">a.</span></span> <span data-ttu-id="d4bdd-212">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d4bdd-213">b.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-213">b.</span></span> <span data-ttu-id="d4bdd-214">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d4bdd-215">c.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-215">c.</span></span> <span data-ttu-id="d4bdd-216">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d4bdd-217">d.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-217">d.</span></span> <span data-ttu-id="d4bdd-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="d4bdd-219">Criar um utilizador de teste myPolicies</span><span class="sxs-lookup"><span data-stu-id="d4bdd-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="d4bdd-220">Nesta secção, vai criar um utilizador chamado Britta Simon myPolicies.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="d4bdd-221">Trabalhar com [myPolicies suporta equipa](mailto:support@mypolicies.com) para adicionar utilizadores de Olá na plataforma de myPolicies Olá.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="d4bdd-222">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d4bdd-223">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4bdd-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d4bdd-224">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso toomyPolicies.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="d4bdd-226">**tooassign Britta Simon toomyPolicies, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d4bdd-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4bdd-227">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="d4bdd-229">Na lista de aplicações de Olá, selecione **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-229">In hello applications list, select **myPolicies**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="d4bdd-231">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="d4bdd-233">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-233">Click **Add** button.</span></span> <span data-ttu-id="d4bdd-234">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="d4bdd-236">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d4bdd-237">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d4bdd-238">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d4bdd-239">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d4bdd-239">Testing single sign-on</span></span>

<span data-ttu-id="d4bdd-240">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d4bdd-241">Ao clicar Olá myPolicies na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour myPolicies aplicação.</span><span class="sxs-lookup"><span data-stu-id="d4bdd-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="d4bdd-242">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d4bdd-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d4bdd-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d4bdd-243">Additional resources</span></span>

* [<span data-ttu-id="d4bdd-244">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4bdd-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d4bdd-245">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d4bdd-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

