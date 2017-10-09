---
title: "Tutorial: Integração do Azure Active Directory com o ato de Learningpool | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Learningpool Act."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: f343623f08bb60e143aaff07d93e4ef773232e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="92fd4-103">Tutorial: Integração do Azure Active Directory com Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="92fd4-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="92fd4-104">Neste tutorial, saiba como toointegrate Learningpool funcionar com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92fd4-104">In this tutorial, you learn how toointegrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92fd4-105">Integrar Learningpool Act com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="92fd4-105">Integrating Learningpool Act with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="92fd4-106">Pode controlar no Azure AD que tenha acesso tooLearningpool Act</span><span class="sxs-lookup"><span data-stu-id="92fd4-106">You can control in Azure AD who has access tooLearningpool Act</span></span>
- <span data-ttu-id="92fd4-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooLearningpool Act (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="92fd4-107">You can enable your users tooautomatically get signed-on tooLearningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92fd4-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="92fd4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="92fd4-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="92fd4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92fd4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="92fd4-110">Prerequisites</span></span>

<span data-ttu-id="92fd4-111">integração do Azure AD com o ato de Learningpool tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="92fd4-111">tooconfigure Azure AD integration with Learningpool Act, you need hello following items:</span></span>

- <span data-ttu-id="92fd4-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="92fd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92fd4-113">Um ATO Learningpool-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="92fd4-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92fd4-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="92fd4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92fd4-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="92fd4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92fd4-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="92fd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92fd4-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92fd4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92fd4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="92fd4-118">Scenario description</span></span>
<span data-ttu-id="92fd4-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="92fd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92fd4-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="92fd4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92fd4-121">A adição de Learningpool ato de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="92fd4-121">Adding Learningpool Act from hello gallery</span></span>
2. <span data-ttu-id="92fd4-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="92fd4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-hello-gallery"></a><span data-ttu-id="92fd4-123">A adição de Learningpool ato de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="92fd4-123">Adding Learningpool Act from hello gallery</span></span>
<span data-ttu-id="92fd4-124">tooconfigure Olá integração do Learningpool Act com o Azure AD, é necessário tooadd Learningpool Act Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="92fd4-124">tooconfigure hello integration of Learningpool Act into Azure AD, you need tooadd Learningpool Act from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="92fd4-125">**tooadd Learningpool ATO da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="92fd4-125">**tooadd Learningpool Act from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="92fd4-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="92fd4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92fd4-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="92fd4-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="92fd4-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92fd4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="92fd4-133">Na caixa de pesquisa de Olá, escreva **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-133">In hello search box, type **Learningpool Act**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="92fd4-135">No painel de resultados de Olá, selecione **Learningpool Act**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="92fd4-135">In hello results panel, select **Learningpool Act**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92fd4-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="92fd4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92fd4-138">Nesta secção, configura e teste do Azure AD-início de sessão único com Learningpool Act com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="92fd4-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92fd4-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Learningpool Act é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92fd4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learningpool Act is tooa user in Azure AD.</span></span> <span data-ttu-id="92fd4-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Learningpool Act tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="92fd4-140">In other words, a link relationship between an Azure AD user and hello related user in Learningpool Act needs toobe established.</span></span>

<span data-ttu-id="92fd4-141">No Learningpool Act, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="92fd4-141">In Learningpool Act, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="92fd4-142">tooconfigure e teste do Azure AD-início de sessão único com o ato de Learningpool, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="92fd4-142">tooconfigure and test Azure AD single sign-on with Learningpool Act, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="92fd4-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="92fd4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="92fd4-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92fd4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92fd4-145">**[Criar um utilizador de teste Learningpool Act](#creating-a-learningpool-act-test-user)**  -toohave um homólogo de Britta Simon no Learningpool Act que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="92fd4-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - toohave a counterpart of Britta Simon in Learningpool Act that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="92fd4-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="92fd4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92fd4-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="92fd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92fd4-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="92fd4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92fd4-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="92fd4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="92fd4-150">**tooconfigure do Azure AD-início de sessão único com o ato de Learningpool, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="92fd4-150">**tooconfigure Azure AD single sign-on with Learningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="92fd4-151">No Olá portal do Azure, no Olá **Learningpool Act** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-151">In hello Azure portal, on hello **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="92fd4-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="92fd4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="92fd4-155">No Olá **Learningpool Act domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="92fd4-155">On hello **Learningpool Act Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="92fd4-157">a.</span><span class="sxs-lookup"><span data-stu-id="92fd4-157">a.</span></span> <span data-ttu-id="92fd4-158">No Olá **URL de início de sessão** caixa de texto, tipo Olá URL:`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="92fd4-158">In hello **Sign-on URL** textbox, type hello URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="92fd4-159">b.</span><span class="sxs-lookup"><span data-stu-id="92fd4-159">b.</span></span> <span data-ttu-id="92fd4-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:</span><span class="sxs-lookup"><span data-stu-id="92fd4-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="92fd4-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="92fd4-161">These values are not real.</span></span> <span data-ttu-id="92fd4-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="92fd4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="92fd4-163">Contacte [equipa de suporte de cliente de Act Learningpool](https://www.Learningpool.com/support) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="92fd4-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="92fd4-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="92fd4-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="92fd4-166">Aplicação de Learningpool Act espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="92fd4-166">Learningpool Act application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="92fd4-167">Configure Olá seguintes afirmações para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="92fd4-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="92fd4-168">Pode gerir os valores de Olá destes atributos a partir de Olá **"Atrribute"** separador da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="92fd4-168">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="92fd4-169">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="92fd4-169">hello following screenshot shows an example for this.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="92fd4-171">No Olá **atributos de utilizador** secção em Olá **de sessão único-** caixa de diálogo, configurar atributos token SAML, conforme mostrado na imagem de Olá e efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="92fd4-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="92fd4-172">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="92fd4-172">Attribute Name</span></span> | <span data-ttu-id="92fd4-173">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="92fd4-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="92fd4-174">urn: oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="92fd4-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="92fd4-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="92fd4-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="92fd4-176">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="92fd4-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="92fd4-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="92fd4-177">user.givenname</span></span> |
    | <span data-ttu-id="92fd4-178">urn: oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="92fd4-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="92fd4-179">User.Mail</span><span class="sxs-lookup"><span data-stu-id="92fd4-179">user.mail</span></span> |    
    | <span data-ttu-id="92fd4-180">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="92fd4-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="92fd4-181">User.Surname</span><span class="sxs-lookup"><span data-stu-id="92fd4-181">user.surname</span></span> |
    
    <span data-ttu-id="92fd4-182">a.</span><span class="sxs-lookup"><span data-stu-id="92fd4-182">a.</span></span> <span data-ttu-id="92fd4-183">Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92fd4-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Configurar o início de sessão único](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="92fd4-186">b.</span><span class="sxs-lookup"><span data-stu-id="92fd4-186">b.</span></span> <span data-ttu-id="92fd4-187">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="92fd4-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="92fd4-188">c.</span><span class="sxs-lookup"><span data-stu-id="92fd4-188">c.</span></span> <span data-ttu-id="92fd4-189">De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="92fd4-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="92fd4-190">d.</span><span class="sxs-lookup"><span data-stu-id="92fd4-190">d.</span></span> <span data-ttu-id="92fd4-191">Deixe Olá **espaço de nomes** em branco.</span><span class="sxs-lookup"><span data-stu-id="92fd4-191">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="92fd4-192">e.</span><span class="sxs-lookup"><span data-stu-id="92fd4-192">e.</span></span> <span data-ttu-id="92fd4-193">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-193">Click **Ok**.</span></span>

7. <span data-ttu-id="92fd4-194">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="92fd4-194">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="92fd4-196">tooconfigure-início de sessão único em **Learningpool Act** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte do Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="92fd4-196">tooconfigure single sign-on on **Learningpool Act** side, you need toosend hello downloaded **Metadata XML** too[Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="92fd4-197">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="92fd4-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="92fd4-198">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="92fd4-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="92fd4-199">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="92fd4-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="92fd4-200">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92fd4-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92fd4-201">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="92fd4-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="92fd4-202">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="92fd4-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="92fd4-204">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="92fd4-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="92fd4-205">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="92fd4-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92fd4-207">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92fd4-209">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="92fd4-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92fd4-211">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="92fd4-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92fd4-213">a.</span><span class="sxs-lookup"><span data-stu-id="92fd4-213">a.</span></span> <span data-ttu-id="92fd4-214">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92fd4-215">b.</span><span class="sxs-lookup"><span data-stu-id="92fd4-215">b.</span></span> <span data-ttu-id="92fd4-216">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92fd4-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92fd4-217">c.</span><span class="sxs-lookup"><span data-stu-id="92fd4-217">c.</span></span> <span data-ttu-id="92fd4-218">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="92fd4-219">d.</span><span class="sxs-lookup"><span data-stu-id="92fd4-219">d.</span></span> <span data-ttu-id="92fd4-220">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="92fd4-221">Criar um utilizador de teste Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="92fd4-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="92fd4-222">tooenable do Azure AD os utilizadores toolog no tooLearningpool Act, estes têm de ser aprovisionados para Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="92fd4-222">tooenable Azure AD users toolog in tooLearningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="92fd4-223">Não há nenhum item de ação para tooconfigure utilizador tooLearningpool ato de aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="92fd4-223">There is no action item for you tooconfigure user provisioning tooLearningpool Act.</span></span>  
<span data-ttu-id="92fd4-224">Os utilizadores precisam de toobe criado pelo seu [equipa de suporte do Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="92fd4-224">Users need toobe created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="92fd4-225">Pode utilizar quaisquer outras Learningpool Act utilizador conta criação ferramentas ou APIs fornecidas pelo Learningpool Act tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="92fd4-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="92fd4-226">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="92fd4-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="92fd4-227">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="92fd4-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearningpool Act.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="92fd4-229">**tooassign Britta Simon tooLearningpool Act, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="92fd4-229">**tooassign Britta Simon tooLearningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="92fd4-230">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="92fd4-232">Na lista de aplicações de Olá, selecione **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-232">In hello applications list, select **Learningpool Act**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="92fd4-234">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="92fd4-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="92fd4-236">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="92fd4-236">Click **Add** button.</span></span> <span data-ttu-id="92fd4-237">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92fd4-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="92fd4-239">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="92fd4-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="92fd4-240">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92fd4-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92fd4-241">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92fd4-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92fd4-242">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="92fd4-242">Testing single sign-on</span></span>

<span data-ttu-id="92fd4-243">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="92fd4-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="92fd4-244">Ao clicar Olá Learningpool Act na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="92fd4-244">When you click hello Learningpool Act tile in hello Access Panel, you should get automatically signed-on tooyour Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92fd4-245">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="92fd4-245">Additional resources</span></span>

* [<span data-ttu-id="92fd4-246">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92fd4-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92fd4-247">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92fd4-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

