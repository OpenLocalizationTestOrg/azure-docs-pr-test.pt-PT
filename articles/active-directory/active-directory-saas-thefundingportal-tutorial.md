---
title: "Tutorial: Integração do Azure Active Directory com Olá financiar Portal | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Olá financiar Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="81ea4-103">Tutorial: Integração do Azure Active Directory com Olá financiar Portal</span><span class="sxs-lookup"><span data-stu-id="81ea4-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="81ea4-104">Neste tutorial, saiba como toointegrate Olá financiar Portal no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81ea4-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81ea4-105">Integrar Olá financiar Portal com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="81ea4-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="81ea4-106">Pode controlar no Azure AD que tenha acesso toohello Funding Portal</span><span class="sxs-lookup"><span data-stu-id="81ea4-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="81ea4-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada toohello Funding Portal (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ea4-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81ea4-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="81ea4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="81ea4-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81ea4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81ea4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="81ea4-110">Prerequisites</span></span>

<span data-ttu-id="81ea4-111">integração de tooconfigure do Azure AD com Olá Funding Portal, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="81ea4-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="81ea4-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ea4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81ea4-113">Um Olá financiar Portal-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="81ea4-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81ea4-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="81ea4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81ea4-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="81ea4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81ea4-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="81ea4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81ea4-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81ea4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81ea4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="81ea4-118">Scenario description</span></span>
<span data-ttu-id="81ea4-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="81ea4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81ea4-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="81ea4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81ea4-121">Adicionar Olá Funding Portal na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="81ea4-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="81ea4-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="81ea4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="81ea4-123">Adicionar Olá Funding Portal na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="81ea4-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="81ea4-124">tooconfigure Olá integração de Olá Funding Portal com o Azure AD, é necessário tooadd Olá Funding Portal Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="81ea4-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="81ea4-125">**tooadd Olá financiar Portal a partir da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="81ea4-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="81ea4-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="81ea4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="81ea4-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="81ea4-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="81ea4-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81ea4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="81ea4-133">Na caixa de pesquisa de Olá, escreva **Olá financiar Portal**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="81ea4-135">No painel de resultados de Olá, selecione **Olá financiar Portal**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="81ea4-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81ea4-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="81ea4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81ea4-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Olá que financiar Portal baseia-se um utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="81ea4-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81ea4-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador homólogo Olá Olá financiar Portal é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81ea4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="81ea4-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Olá financiar Portal tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="81ea4-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="81ea4-141">No Olá financiar Portal, atribua o valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="81ea4-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="81ea4-142">tooconfigure e teste do Azure AD-início de sessão único com Olá Funding Portal, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="81ea4-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="81ea4-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="81ea4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="81ea4-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="81ea4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81ea4-145">**[Criar utilizador de teste de Portal financiar Olá](#creating-the-funding-portal-test-user)**  -toohave um homólogo de Britta Simon no Olá Portal Funding toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="81ea4-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="81ea4-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="81ea4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81ea4-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="81ea4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81ea4-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="81ea4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81ea4-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de Portal financiar de Olá.</span><span class="sxs-lookup"><span data-stu-id="81ea4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="81ea4-150">**tooconfigure do Azure AD-início de sessão único com Olá financiar Portal, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="81ea4-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="81ea4-151">No Olá portal do Azure, no Olá **Olá financiar Portal** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="81ea4-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="81ea4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="81ea4-155">No Olá **Olá financiar domínio de Portal e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="81ea4-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="81ea4-157">a.</span><span class="sxs-lookup"><span data-stu-id="81ea4-157">a.</span></span> <span data-ttu-id="81ea4-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="81ea4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="81ea4-159">b.</span><span class="sxs-lookup"><span data-stu-id="81ea4-159">b.</span></span> <span data-ttu-id="81ea4-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="81ea4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81ea4-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="81ea4-161">These values are not real.</span></span> <span data-ttu-id="81ea4-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="81ea4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="81ea4-163">Contacte [Olá equipa de suporte de cliente de Portal financiar](mailto:info@regenteducation.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="81ea4-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="81ea4-164">Olá aplicação de Portal financiar espera Olá SAML asserções toocontain um atributo com o nome "externalId1".</span><span class="sxs-lookup"><span data-stu-id="81ea4-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="81ea4-165">valor Olá "externalId1" deve ser um studentID reconhecido.</span><span class="sxs-lookup"><span data-stu-id="81ea4-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="81ea4-166">Configure afirmações de Olá "externalId1" para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="81ea4-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="81ea4-167">Pode gerir os valores de Olá destes atributos a partir de Olá **atributos de utilizador** da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="81ea4-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="81ea4-168">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="81ea4-168">hello following screenshot shows an example for this.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="81ea4-170">No Olá **atributos de utilizador** secção em Olá **de sessão único-** caixa de diálogo, configurar atributos token SAML, conforme mostrado na imagem de Olá e efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="81ea4-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="81ea4-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="81ea4-171">Attribute Name</span></span> | <span data-ttu-id="81ea4-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="81ea4-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="81ea4-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="81ea4-173">externalId1</span></span> | <span data-ttu-id="81ea4-174">User.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="81ea4-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="81ea4-175">a.</span><span class="sxs-lookup"><span data-stu-id="81ea4-175">a.</span></span> <span data-ttu-id="81ea4-176">Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81ea4-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Configurar o início de sessão único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="81ea4-179">b.</span><span class="sxs-lookup"><span data-stu-id="81ea4-179">b.</span></span> <span data-ttu-id="81ea4-180">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="81ea4-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="81ea4-181">c.</span><span class="sxs-lookup"><span data-stu-id="81ea4-181">c.</span></span> <span data-ttu-id="81ea4-182">De Olá **valor do atributo** lista, o atributo de Olá selecione pretende toouse para a implementação.</span><span class="sxs-lookup"><span data-stu-id="81ea4-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="81ea4-183">Por exemplo, se tiver armazenado Olá StudentID valor no Olá ExtensionAttribute1, em seguida, selecione user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="81ea4-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="81ea4-184">d.</span><span class="sxs-lookup"><span data-stu-id="81ea4-184">d.</span></span> <span data-ttu-id="81ea4-185">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="81ea4-186">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="81ea4-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="81ea4-188">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="81ea4-188">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="81ea4-190">tooconfigure-início de sessão único em **Olá financiar Portal** lado, terá de Olá toosend transferido **XML de metadados** demasiado[Olá equipa de suporte de Portal financiar](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="81ea4-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="81ea4-191">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="81ea4-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="81ea4-192">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="81ea4-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="81ea4-193">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="81ea4-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="81ea4-194">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81ea4-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81ea4-195">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ea4-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="81ea4-196">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="81ea4-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="81ea4-198">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="81ea4-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="81ea4-199">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="81ea4-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81ea4-201">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81ea4-203">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="81ea4-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81ea4-205">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="81ea4-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81ea4-207">a.</span><span class="sxs-lookup"><span data-stu-id="81ea4-207">a.</span></span> <span data-ttu-id="81ea4-208">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81ea4-209">b.</span><span class="sxs-lookup"><span data-stu-id="81ea4-209">b.</span></span> <span data-ttu-id="81ea4-210">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="81ea4-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81ea4-211">c.</span><span class="sxs-lookup"><span data-stu-id="81ea4-211">c.</span></span> <span data-ttu-id="81ea4-212">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="81ea4-213">d.</span><span class="sxs-lookup"><span data-stu-id="81ea4-213">d.</span></span> <span data-ttu-id="81ea4-214">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="81ea4-215">Criação de utilizador de teste de Portal financiar Olá</span><span class="sxs-lookup"><span data-stu-id="81ea4-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="81ea4-216">Nesta secção, vai criar um utilizador chamado Britta Simon Olá Funding Portal.</span><span class="sxs-lookup"><span data-stu-id="81ea4-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="81ea4-217">Trabalhar com [Olá equipa de suporte de Portal financiar](mailto:info@regenteducation.com) tooadd Olá utilizador de teste e ativar a SSO.</span><span class="sxs-lookup"><span data-stu-id="81ea4-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="81ea4-218">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="81ea4-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="81ea4-219">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso toohello Funding Portal.</span><span class="sxs-lookup"><span data-stu-id="81ea4-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="81ea4-221">**tooassign Britta Simon toohello Funding Portal, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="81ea4-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="81ea4-222">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="81ea4-224">Na lista de aplicações de Olá, selecione **Olá financiar Portal**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="81ea4-226">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="81ea4-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="81ea4-228">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="81ea4-228">Click **Add** button.</span></span> <span data-ttu-id="81ea4-229">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81ea4-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="81ea4-231">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="81ea4-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="81ea4-232">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81ea4-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81ea4-233">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="81ea4-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81ea4-234">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="81ea4-234">Testing single sign-on</span></span>

<span data-ttu-id="81ea4-235">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="81ea4-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="81ea4-236">Ao clicar em mosaico de Portal financiar Olá Olá no painel de acesso de Olá, deve obter a aplicação de Portal financiar de Olá tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="81ea4-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81ea4-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="81ea4-237">Additional resources</span></span>

* [<span data-ttu-id="81ea4-238">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81ea4-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81ea4-239">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81ea4-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

