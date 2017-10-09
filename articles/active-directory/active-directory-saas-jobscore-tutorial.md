---
title: "Tutorial: Integração do Azure Active Directory com JobScore | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e JobScore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6693a5fd96bfd7fbcd7197983b5f04d061970bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="def15-103">Tutorial: Integração do Azure Active Directory com JobScore</span><span class="sxs-lookup"><span data-stu-id="def15-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="def15-104">Neste tutorial, saiba como toointegrate JobScore com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="def15-104">In this tutorial, you learn how toointegrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="def15-105">Integrar JobScore com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="def15-105">Integrating JobScore with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="def15-106">Pode controlar no Azure AD que tenha acesso tooJobScore</span><span class="sxs-lookup"><span data-stu-id="def15-106">You can control in Azure AD who has access tooJobScore</span></span>
- <span data-ttu-id="def15-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooJobScore (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="def15-107">You can enable your users tooautomatically get signed-on tooJobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="def15-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="def15-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="def15-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="def15-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="def15-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="def15-110">Prerequisites</span></span>

<span data-ttu-id="def15-111">integração do Azure AD com JobScore tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="def15-111">tooconfigure Azure AD integration with JobScore, you need hello following items:</span></span>

- <span data-ttu-id="def15-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="def15-112">An Azure AD subscription</span></span>
- <span data-ttu-id="def15-113">Um JobScore-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="def15-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="def15-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="def15-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="def15-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="def15-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="def15-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="def15-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="def15-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="def15-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="def15-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="def15-118">Scenario description</span></span>
<span data-ttu-id="def15-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="def15-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="def15-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="def15-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="def15-121">Adicionar JobScore da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="def15-121">Adding JobScore from hello gallery</span></span>
2. <span data-ttu-id="def15-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="def15-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-hello-gallery"></a><span data-ttu-id="def15-123">Adicionar JobScore da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="def15-123">Adding JobScore from hello gallery</span></span>
<span data-ttu-id="def15-124">tooconfigure Olá integração de JobScore com o Azure AD, é necessário tooadd JobScore Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="def15-124">tooconfigure hello integration of JobScore into Azure AD, you need tooadd JobScore from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="def15-125">**tooadd JobScore da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="def15-125">**tooadd JobScore from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="def15-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="def15-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="def15-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="def15-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="def15-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="def15-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="def15-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="def15-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="def15-133">Na caixa de pesquisa de Olá, escreva **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="def15-133">In hello search box, type **JobScore**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="def15-135">No painel de resultados de Olá, selecione **JobScore**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="def15-135">In hello results panel, select **JobScore**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="def15-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="def15-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="def15-138">Nesta secção, configure e teste do Azure AD-início de sessão único com JobScore com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="def15-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="def15-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá JobScore é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="def15-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JobScore is tooa user in Azure AD.</span></span> <span data-ttu-id="def15-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá JobScore tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="def15-140">In other words, a link relationship between an Azure AD user and hello related user in JobScore needs toobe established.</span></span>

<span data-ttu-id="def15-141">No JobScore, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="def15-141">In JobScore, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="def15-142">tooconfigure e teste do Azure AD-início de sessão único com JobScore, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="def15-142">tooconfigure and test Azure AD single sign-on with JobScore, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="def15-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="def15-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="def15-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="def15-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="def15-145">**[Criar um utilizador de teste JobScore](#creating-a-jobscore-test-user)**  -toohave um homólogo de Britta Simon no JobScore é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="def15-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - toohave a counterpart of Britta Simon in JobScore that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="def15-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="def15-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="def15-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="def15-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="def15-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="def15-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="def15-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação JobScore.</span><span class="sxs-lookup"><span data-stu-id="def15-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="def15-150">**tooconfigure do Azure AD-início de sessão único com JobScore, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="def15-150">**tooconfigure Azure AD single sign-on with JobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="def15-151">No Olá portal do Azure, no Olá **JobScore** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="def15-151">In hello Azure portal, on hello **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="def15-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="def15-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="def15-155">No Olá **JobScore domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="def15-155">On hello **JobScore Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="def15-157">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="def15-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="def15-158">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="def15-158">This value is not real.</span></span> <span data-ttu-id="def15-159">Atualizar este valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="def15-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="def15-160">Contacte [equipa de suporte de cliente JobScore](mailto:support@jobscore.com) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="def15-160">Contact [JobScore Client support team](mailto:support@jobscore.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="def15-161">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="def15-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="def15-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="def15-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="def15-165">tooconfigure-início de sessão único em **JobScore** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de JobScore](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="def15-165">tooconfigure single sign-on on **JobScore** side, you need toosend hello downloaded **Metadata XML** too[JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="def15-166">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="def15-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="def15-167">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="def15-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="def15-168">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="def15-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="def15-169">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="def15-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="def15-170">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="def15-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="def15-172">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="def15-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="def15-173">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="def15-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="def15-175">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="def15-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="def15-177">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="def15-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="def15-179">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="def15-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="def15-181">a.</span><span class="sxs-lookup"><span data-stu-id="def15-181">a.</span></span> <span data-ttu-id="def15-182">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="def15-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="def15-183">b.</span><span class="sxs-lookup"><span data-stu-id="def15-183">b.</span></span> <span data-ttu-id="def15-184">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="def15-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="def15-185">c.</span><span class="sxs-lookup"><span data-stu-id="def15-185">c.</span></span> <span data-ttu-id="def15-186">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="def15-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="def15-187">d.</span><span class="sxs-lookup"><span data-stu-id="def15-187">d.</span></span> <span data-ttu-id="def15-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="def15-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="def15-189">Criar um utilizador de teste JobScore</span><span class="sxs-lookup"><span data-stu-id="def15-189">Creating a JobScore test user</span></span>

<span data-ttu-id="def15-190">Nesta secção, vai criar um utilizador chamado Britta Simon JobScore.</span><span class="sxs-lookup"><span data-stu-id="def15-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="def15-191">Trabalhar com [equipa de suporte de JobScore](mailto:support@jobscore.com) utilizadores de Olá tooadd na plataforma de JobScore Olá.</span><span class="sxs-lookup"><span data-stu-id="def15-191">Work with [JobScore support team](mailto:support@jobscore.com) tooadd hello users in hello JobScore platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="def15-192">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="def15-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="def15-193">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooJobScore.</span><span class="sxs-lookup"><span data-stu-id="def15-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobScore.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="def15-195">**tooassign Britta Simon tooJobScore, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="def15-195">**tooassign Britta Simon tooJobScore, perform hello following steps:**</span></span>

1. <span data-ttu-id="def15-196">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="def15-196">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="def15-198">Na lista de aplicações de Olá, selecione **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="def15-198">In hello applications list, select **JobScore**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="def15-200">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="def15-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="def15-202">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="def15-202">Click **Add** button.</span></span> <span data-ttu-id="def15-203">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="def15-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="def15-205">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="def15-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="def15-206">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="def15-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="def15-207">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="def15-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="def15-208">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="def15-208">Testing single sign-on</span></span>

<span data-ttu-id="def15-209">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="def15-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="def15-210">Ao clicar em mosaico de JobScore Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour JobScore aplicação.</span><span class="sxs-lookup"><span data-stu-id="def15-210">When you click hello JobScore tile in hello Access Panel, you should get automatically signed-on tooyour JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="def15-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="def15-211">Additional resources</span></span>

* [<span data-ttu-id="def15-212">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="def15-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="def15-213">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="def15-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

