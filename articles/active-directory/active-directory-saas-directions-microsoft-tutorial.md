---
title: "Tutorial: Integração do Azure Active Directory com instruções da Microsoft | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e as direções da Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 59a8b856fd2dc75a37e9bb8f46ced066bcd0fd56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="93678-103">Tutorial: Integração do Azure Active Directory com instruções da Microsoft</span><span class="sxs-lookup"><span data-stu-id="93678-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="93678-104">Neste tutorial, saiba como toointegrate indicações da Microsoft com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93678-104">In this tutorial, you learn how toointegrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93678-105">Integrar as direções da Microsoft com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="93678-105">Integrating Directions on Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="93678-106">Pode controlar no Azure AD que tenha acesso tooDirections da Microsoft</span><span class="sxs-lookup"><span data-stu-id="93678-106">You can control in Azure AD who has access tooDirections on Microsoft</span></span>
- <span data-ttu-id="93678-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooDirections da Microsoft (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93678-107">You can enable your users tooautomatically get signed-on tooDirections on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93678-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="93678-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="93678-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93678-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93678-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="93678-110">Prerequisites</span></span>

<span data-ttu-id="93678-111">integração do Azure AD com as direções no Microsoft tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="93678-111">tooconfigure Azure AD integration with Directions on Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="93678-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93678-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93678-113">Um indicações no Microsoft-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="93678-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93678-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="93678-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93678-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="93678-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93678-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="93678-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93678-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93678-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93678-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="93678-118">Scenario description</span></span>
<span data-ttu-id="93678-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="93678-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93678-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="93678-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93678-121">Adicionar as direções da Microsoft na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="93678-121">Adding Directions on Microsoft from hello gallery</span></span>
2. <span data-ttu-id="93678-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="93678-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-hello-gallery"></a><span data-ttu-id="93678-123">Adicionar as direções da Microsoft na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="93678-123">Adding Directions on Microsoft from hello gallery</span></span>
<span data-ttu-id="93678-124">integração de Olá tooconfigure das instruções da Microsoft com o Azure AD, é necessário tooadd indicações no Microsoft Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="93678-124">tooconfigure hello integration of Directions on Microsoft into Azure AD, you need tooadd Directions on Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93678-125">**tooadd indicações da Microsoft na Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="93678-125">**tooadd Directions on Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93678-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="93678-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93678-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="93678-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="93678-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="93678-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="93678-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="93678-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="93678-133">Na caixa de pesquisa de Olá, escreva **indicações no Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="93678-133">In hello search box, type **Directions on Microsoft**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="93678-135">No painel de resultados de Olá, selecione **indicações no Microsoft**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="93678-135">In hello results panel, select **Directions on Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93678-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="93678-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93678-138">Nesta secção, configurar e testar o Azure AD-início de sessão único com instruções da Microsoft com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="93678-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="93678-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá indicações da Microsoft é utilizador de tooa no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93678-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Directions on Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="93678-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá indicações da Microsoft necessita de toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="93678-140">In other words, a link relationship between an Azure AD user and hello related user in Directions on Microsoft needs toobe established.</span></span>

<span data-ttu-id="93678-141">Nas direções da Microsoft, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="93678-141">In Directions on Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="93678-142">tooconfigure e teste do Azure AD-início de sessão único com instruções da Microsoft, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="93678-142">tooconfigure and test Azure AD single sign-on with Directions on Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93678-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="93678-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93678-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93678-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93678-145">**[Criar um instruções de utilizador de teste do Microsoft](#creating-a-directions-on-microsoft-test-user)**  -toohave um homólogo de Britta Simon nas direções da Microsoft que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="93678-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - toohave a counterpart of Britta Simon in Directions on Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="93678-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="93678-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93678-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="93678-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93678-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="93678-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93678-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua indicações sobre aplicações da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93678-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="93678-150">**tooconfigure do Azure AD-início de sessão único com instruções da Microsoft, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="93678-150">**tooconfigure Azure AD single sign-on with Directions on Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="93678-151">No Olá portal do Azure, no Olá **indicações no Microsoft** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="93678-151">In hello Azure portal, on hello **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="93678-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="93678-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="93678-155">No Olá **indicações no Microsoft Domain e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="93678-155">On hello **Directions on Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="93678-157">a.</span><span class="sxs-lookup"><span data-stu-id="93678-157">a.</span></span> <span data-ttu-id="93678-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:</span><span class="sxs-lookup"><span data-stu-id="93678-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="93678-159">b.</span><span class="sxs-lookup"><span data-stu-id="93678-159">b.</span></span> <span data-ttu-id="93678-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:</span><span class="sxs-lookup"><span data-stu-id="93678-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="93678-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="93678-161">These values are not real.</span></span> <span data-ttu-id="93678-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="93678-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="93678-163">Contacte [indicações no cliente da Microsoft suportam equipa](mailto:service@DirectionsOnMicrosoft.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="93678-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="93678-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="93678-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="93678-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="93678-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93678-168">tooconfigure-início de sessão único em **indicações no Microsoft** lado, terá de Olá toosend transferido **XML de metadados** demasiado[indicações da Microsoft suportam equipa](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="93678-168">tooconfigure single sign-on on **Directions on Microsoft** side, you need toosend hello downloaded **Metadata XML** too[Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="93678-169">Olá tooenable indicações da Microsoft suportar equipa toolocate a associação do site federado, incluir informações da sua empresa no seu correio eletrónico.</span><span class="sxs-lookup"><span data-stu-id="93678-169">tooenable hello Directions on Microsoft support team toolocate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="93678-170">Início de sessão único para as direções da Microsoft necessita de toobe ativado por Olá [indicações no cliente da Microsoft suportam equipa](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="93678-170">Single sign-on for Directions on Microsoft needs toobe enabled by hello [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="93678-171">Irá receber uma notificação quando o início de sessão único foi ativado.</span><span class="sxs-lookup"><span data-stu-id="93678-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="93678-172">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="93678-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="93678-173">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="93678-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="93678-174">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93678-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93678-175">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93678-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="93678-176">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="93678-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="93678-178">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="93678-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93678-179">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="93678-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93678-181">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="93678-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93678-183">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="93678-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93678-185">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="93678-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93678-187">a.</span><span class="sxs-lookup"><span data-stu-id="93678-187">a.</span></span> <span data-ttu-id="93678-188">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93678-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93678-189">b.</span><span class="sxs-lookup"><span data-stu-id="93678-189">b.</span></span> <span data-ttu-id="93678-190">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="93678-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93678-191">c.</span><span class="sxs-lookup"><span data-stu-id="93678-191">c.</span></span> <span data-ttu-id="93678-192">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="93678-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="93678-193">d.</span><span class="sxs-lookup"><span data-stu-id="93678-193">d.</span></span> <span data-ttu-id="93678-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="93678-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="93678-195">Criar um indicações no utilizador de teste da Microsoft</span><span class="sxs-lookup"><span data-stu-id="93678-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="93678-196">Não há nenhum item de ação para tooconfigure aprovisionamento de utilizadores tooDirections da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93678-196">There is no action item for you tooconfigure user provisioning tooDirections on Microsoft.</span></span>  

<span data-ttu-id="93678-197">Quando um utilizador atribuído tenta toolog no tooDirections no Microsoft a utilizar o painel de acesso de Olá, instruções da Microsoft verifica se o utilizador Olá existe.</span><span class="sxs-lookup"><span data-stu-id="93678-197">When an assigned user tries toolog in tooDirections on Microsoft using hello access panel, Directions on Microsoft checks whether hello user exists.</span></span> <span data-ttu-id="93678-198">Se não existe nenhuma conta de utilizador ainda estão disponíveis, é criado automaticamente pelo indicações da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93678-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="93678-199">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93678-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="93678-200">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooDirections da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93678-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirections on Microsoft.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="93678-202">**tooassign Britta Simon tooDirections da Microsoft, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="93678-202">**tooassign Britta Simon tooDirections on Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="93678-203">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="93678-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="93678-205">Na lista de aplicações de Olá, selecione **indicações no Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="93678-205">In hello applications list, select **Directions on Microsoft**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="93678-207">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="93678-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="93678-209">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="93678-209">Click **Add** button.</span></span> <span data-ttu-id="93678-210">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="93678-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="93678-212">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="93678-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="93678-213">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="93678-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93678-214">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="93678-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="93678-215">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="93678-215">Testing single sign-on</span></span>

<span data-ttu-id="93678-216">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="93678-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="93678-217">Ao clicar em instruções Olá no mosaico da Microsoft no painel de acesso de Olá, deve obter indicações de tooyour automaticamente com sessão iniciada em aplicações da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93678-217">When you click hello Directions on Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour Directions on Microsoft application.</span></span>

<span data-ttu-id="93678-218">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="93678-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="93678-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="93678-219">Additional resources</span></span>

* [<span data-ttu-id="93678-220">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93678-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93678-221">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="93678-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

