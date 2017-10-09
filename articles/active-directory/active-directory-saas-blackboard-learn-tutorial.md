---
title: "Tutorial: Integração do Azure Active Directory com Blackboard Saiba | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Blackboard saber mais."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="1a13e-103">Tutorial: Integração do Azure Active Directory com Blackboard Saiba mais</span><span class="sxs-lookup"><span data-stu-id="1a13e-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="1a13e-104">Neste tutorial, saiba como toointegrate Blackboard Saiba com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a13e-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a13e-105">Saiba Blackboard a integração com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="1a13e-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1a13e-106">Pode controlar no Azure AD que tenha acesso tooBlackboard Saiba mais</span><span class="sxs-lookup"><span data-stu-id="1a13e-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="1a13e-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooBlackboard saiba (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a13e-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a13e-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1a13e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1a13e-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a13e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a13e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1a13e-110">Prerequisites</span></span>

<span data-ttu-id="1a13e-111">integração do Azure AD com Blackboard saiba tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="1a13e-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="1a13e-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a13e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a13e-113">Um Blackboard saiba-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="1a13e-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a13e-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1a13e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a13e-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1a13e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a13e-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1a13e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a13e-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a13e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a13e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1a13e-118">Scenario description</span></span>
<span data-ttu-id="1a13e-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1a13e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a13e-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="1a13e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a13e-121">A adição de mais Blackboard da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="1a13e-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="1a13e-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="1a13e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="1a13e-123">A adição de mais Blackboard da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="1a13e-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="1a13e-124">tooconfigure Olá integração de Blackboard Saiba com o Azure AD, é necessário tooadd Blackboard saiba Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="1a13e-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1a13e-125">**tooadd Blackboard saber a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1a13e-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a13e-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="1a13e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a13e-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1a13e-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="1a13e-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1a13e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="1a13e-133">Na caixa de pesquisa de Olá, escreva **Blackboard Saiba**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="1a13e-135">No painel de resultados de Olá, selecione **Blackboard Saiba**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="1a13e-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a13e-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="1a13e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a13e-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Blackboard Saiba com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="1a13e-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1a13e-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador Olá homólogo Blackboard saiba é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a13e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="1a13e-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Blackboard saiba tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1a13e-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="1a13e-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Blackboard saber mais.</span><span class="sxs-lookup"><span data-stu-id="1a13e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="1a13e-142">tooconfigure e teste do Azure AD-início de sessão único com Blackboard saber mais, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1a13e-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1a13e-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="1a13e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1a13e-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a13e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a13e-145">**[Criar um utilizador de teste Blackboard Saiba](#creating-a-blackboard-learn-test-user)**  -toohave um homólogo de Britta Simon no Blackboard saiba que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="1a13e-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a13e-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="1a13e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a13e-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="1a13e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a13e-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="1a13e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a13e-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação saiba Blackboard.</span><span class="sxs-lookup"><span data-stu-id="1a13e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="1a13e-150">**tooconfigure do Azure AD-início de sessão único com Blackboard saber, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1a13e-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a13e-151">No Olá portal do Azure, no Olá **Blackboard Saiba** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="1a13e-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="1a13e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="1a13e-155">No Olá **Blackboard saiba domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="1a13e-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="1a13e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a13e-157">a.</span></span> <span data-ttu-id="1a13e-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="1a13e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="1a13e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a13e-159">b.</span></span> <span data-ttu-id="1a13e-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="1a13e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="1a13e-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="1a13e-161">These values are not real.</span></span> <span data-ttu-id="1a13e-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="1a13e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1a13e-163">Contacte [equipa de suporte de cliente de saber Blackboard](https://www.blackboard.com/support/index.aspx) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="1a13e-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="1a13e-164">Aplicação de saiba blackboard espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="1a13e-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1a13e-165">Configure Olá seguintes afirmações para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="1a13e-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="1a13e-166">Pode gerir os valores de Olá destes atributos a partir de Olá **atributos de utilizador** secção na página de integração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="1a13e-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="1a13e-167">Olá seguinte captura de ecrã mostra um exemplo sobre o assunto.</span><span class="sxs-lookup"><span data-stu-id="1a13e-167">hello following screenshot shows an example about it.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="1a13e-169">No Olá **atributos de utilizador** secção no **de sessão único-** caixa de diálogo, configurar atributos token SAML, conforme mostrado na imagem de Olá e efetuar Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="1a13e-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="1a13e-170">Podemos ter mapeado Olá Userprincipalname como aqui o atributo de utilizador exclusivo Olá, mas é possível mapear valor adequado toohello, que distingue exclusivamente o utilizador Olá na organização de Olá e que mapeia o campo de nome de utilizador do tooBlackboard Saiba mais.</span><span class="sxs-lookup"><span data-stu-id="1a13e-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="1a13e-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="1a13e-171">Attribute Name</span></span> | <span data-ttu-id="1a13e-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="1a13e-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="1a13e-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="1a13e-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="1a13e-174">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="1a13e-174">user.userprincipalname</span></span> |

    <span data-ttu-id="1a13e-175">a.</span><span class="sxs-lookup"><span data-stu-id="1a13e-175">a.</span></span> <span data-ttu-id="1a13e-176">Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1a13e-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1a13e-179">b.</span><span class="sxs-lookup"><span data-stu-id="1a13e-179">b.</span></span> <span data-ttu-id="1a13e-180">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="1a13e-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="1a13e-181">c.</span><span class="sxs-lookup"><span data-stu-id="1a13e-181">c.</span></span> <span data-ttu-id="1a13e-182">De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="1a13e-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1a13e-183">d.</span><span class="sxs-lookup"><span data-stu-id="1a13e-183">d.</span></span> <span data-ttu-id="1a13e-184">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-184">Click **Ok**.</span></span>

4. <span data-ttu-id="1a13e-185">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="1a13e-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="1a13e-187">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="1a13e-187">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1a13e-189">No Olá **Blackboard saiba configuração** secção, clique em **configurar Blackboard Saiba** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="1a13e-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1a13e-190">Olá cópia **ID de entidade de SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="1a13e-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="1a13e-192">tooconfigure-início de sessão único em **Blackboard Saiba** lado, terá de Olá toosend transferido **XML de metadados** e **ID de entidade de SAML** demasiado[Blackboard Saiba mais suporta](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a13e-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="1a13e-193">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="1a13e-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1a13e-194">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a13e-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1a13e-195">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a13e-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a13e-196">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a13e-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a13e-197">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a13e-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="1a13e-199">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1a13e-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a13e-200">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="1a13e-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a13e-202">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a13e-204">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="1a13e-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a13e-206">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="1a13e-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a13e-208">a.</span><span class="sxs-lookup"><span data-stu-id="1a13e-208">a.</span></span> <span data-ttu-id="1a13e-209">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a13e-210">b.</span><span class="sxs-lookup"><span data-stu-id="1a13e-210">b.</span></span> <span data-ttu-id="1a13e-211">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a13e-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="1a13e-212">c.</span><span class="sxs-lookup"><span data-stu-id="1a13e-212">c.</span></span> <span data-ttu-id="1a13e-213">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1a13e-214">d.</span><span class="sxs-lookup"><span data-stu-id="1a13e-214">d.</span></span> <span data-ttu-id="1a13e-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="1a13e-216">Criar um utilizador de teste Blackboard Saiba mais</span><span class="sxs-lookup"><span data-stu-id="1a13e-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="1a13e-217">Nesta secção, vai criar um utilizador chamado Britta Simon Blackboard Saiba mais.</span><span class="sxs-lookup"><span data-stu-id="1a13e-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="1a13e-218">Aplicação de saiba blackboard suporta apenas no aprovisionamento de utilizadores de tempo.</span><span class="sxs-lookup"><span data-stu-id="1a13e-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="1a13e-219">Certifique-se de que configurou Olá afirmações conforme descrito na secção de Olá  **[configurar do Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="1a13e-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1a13e-220">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a13e-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1a13e-221">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooBlackboard Saiba mais.</span><span class="sxs-lookup"><span data-stu-id="1a13e-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="1a13e-223">**tooassign Britta Simon tooBlackboard mais informações, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="1a13e-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="1a13e-224">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="1a13e-226">Na lista de aplicações de Olá, selecione **Blackboard Saiba**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="1a13e-228">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1a13e-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="1a13e-230">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="1a13e-230">Click **Add** button.</span></span> <span data-ttu-id="1a13e-231">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1a13e-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="1a13e-233">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="1a13e-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1a13e-234">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1a13e-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a13e-235">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1a13e-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a13e-236">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="1a13e-236">Testing single sign-on</span></span>

<span data-ttu-id="1a13e-237">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="1a13e-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1a13e-238">Ao clicar em mosaico de Blackboard saiba Olá no painel de acesso de Olá, deve obter a aplicação de saber Blackboard tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="1a13e-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="1a13e-239">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1a13e-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1a13e-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1a13e-240">Additional resources</span></span>

* [<span data-ttu-id="1a13e-241">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a13e-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a13e-242">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1a13e-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

