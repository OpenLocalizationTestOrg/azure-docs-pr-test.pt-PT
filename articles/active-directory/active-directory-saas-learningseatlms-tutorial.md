---
title: "Tutorial: Integração do Azure Active Directory com Learning posto de trabalho LMS | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e LMS de postos de trabalho de aprendizagem."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="7e9d4-103">Tutorial: Integração do Azure Active Directory com LMS de postos de trabalho de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="7e9d4-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="7e9d4-104">Neste tutorial, saiba como toointegrate Learning LMS de postos de trabalho com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e9d4-104">In this tutorial, you learn how toointegrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e9d4-105">Integrar Learning LMS de postos de trabalho com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="7e9d4-105">Integrating Learning Seat LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e9d4-106">Pode controlar no Azure AD que tenha acesso tooLearning LMS posto de trabalho</span><span class="sxs-lookup"><span data-stu-id="7e9d4-106">You can control in Azure AD who has access tooLearning Seat LMS</span></span>
- <span data-ttu-id="7e9d4-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooLearning LMS posto de trabalho (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e9d4-107">You can enable your users tooautomatically get signed-on tooLearning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e9d4-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7e9d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7e9d4-109">Se pretender que tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="7e9d4-110">[O que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e9d4-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e9d4-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7e9d4-111">Prerequisites</span></span>

<span data-ttu-id="7e9d4-112">tooconfigure integração do Azure AD com LMS de postos de trabalho do Learning, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7e9d4-112">tooconfigure Azure AD integration with Learning Seat LMS, you need hello following items:</span></span>

- <span data-ttu-id="7e9d4-113">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e9d4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="7e9d4-114">Um Learning posto de trabalho LMS início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="7e9d4-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e9d4-115">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e9d4-116">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="7e9d4-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e9d4-117">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e9d4-118">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e9d4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e9d4-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="7e9d4-119">Scenario description</span></span>
<span data-ttu-id="7e9d4-120">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e9d4-121">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="7e9d4-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e9d4-122">A adição de aprendizagem posto de trabalho LMS de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="7e9d4-122">Adding Learning Seat LMS from hello gallery</span></span>
2. <span data-ttu-id="7e9d4-123">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="7e9d4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-hello-gallery"></a><span data-ttu-id="7e9d4-124">A adição de aprendizagem posto de trabalho LMS de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="7e9d4-124">Adding Learning Seat LMS from hello gallery</span></span>
<span data-ttu-id="7e9d4-125">tooconfigure Olá integração do Learning LMS de postos de trabalho com o Azure AD, é necessário tooadd Learning posto de trabalho LMS Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-125">tooconfigure hello integration of Learning Seat LMS into Azure AD, you need tooadd Learning Seat LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e9d4-126">**tooadd LMS de postos de trabalho de aprendizagem da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7e9d4-126">**tooadd Learning Seat LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e9d4-127">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7e9d4-129">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e9d4-130">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-130">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="7e9d4-132">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="7e9d4-134">Na caixa de pesquisa de Olá, escreva **Learning posto de trabalho LMS**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-134">In hello search box, type **Learning Seat LMS**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="7e9d4-136">No painel de resultados de Olá, selecione **Learning posto de trabalho LMS**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-136">In hello results panel, select **Learning Seat LMS**, and then click **Add** button tooadd hello application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e9d4-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="7e9d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e9d4-138">Nesta secção, configure e teste do Azure AD-início de sessão único com LMS de postos de trabalho do Learning com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="7e9d4-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7e9d4-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Learning posto de trabalho LMS é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learning Seat LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="7e9d4-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no Learning posto de trabalho LMS tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-140">In other words, a link relationship between an Azure AD user and hello related user in Learning Seat LMS needs toobe established.</span></span>

<span data-ttu-id="7e9d4-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Learning LMS de postos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="7e9d4-142">tooconfigure e teste do Azure AD-início de sessão único com LMS de postos de trabalho do Learning, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7e9d4-142">tooconfigure and test Azure AD single sign-on with Learning Seat LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e9d4-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e9d4-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e9d4-145">**[Criar um utilizador de teste de aprendizagem posto de trabalho LMS](#creating-a-learnconnect-test-user)**  -toohave um homólogo de Britta Simon no Learning LMS de postos de trabalho que está ligado toohello do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - toohave a counterpart of Britta Simon in Learning Seat LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e9d4-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e9d4-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e9d4-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7e9d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7e9d4-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação LMS de postos de trabalho de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="7e9d4-150">**tooconfigure do Azure AD-início de sessão único com LMS de postos de trabalho de aprendizagem, efetue Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7e9d4-150">**tooconfigure Azure AD single sign-on with Learning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e9d4-151">No Olá portal do Azure, no Olá **Learning posto de trabalho LMS** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-151">In hello Azure portal, on hello **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="7e9d4-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="7e9d4-155">No Olá **Learning posto de trabalho LMS domínio e os URLs** secção, execute os passos seguintes se quiser aplicação Olá tooconfigure de Olá **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="7e9d4-155">On hello **Learning Seat LMS Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="7e9d4-157">a.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-157">a.</span></span> <span data-ttu-id="7e9d4-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="7e9d4-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="7e9d4-159">b.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-159">b.</span></span> <span data-ttu-id="7e9d4-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span><span class="sxs-lookup"><span data-stu-id="7e9d4-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="7e9d4-161">Verifique **Mostrar avançadas definições de URL**, se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="7e9d4-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="7e9d4-163">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="7e9d4-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="7e9d4-164">Estes valores não são valores reais Olá.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-164">These values are not hello real values.</span></span> <span data-ttu-id="7e9d4-165">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-165">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="7e9d4-166">Contacte [equipa de suporte de postos de trabalho do Learning](http://help.learningseatlms.com/help) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) tooget these values.</span></span> 

5. <span data-ttu-id="7e9d4-167">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="7e9d4-169">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-169">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7e9d4-171">tooconfigure-início de sessão único em **Learning posto de trabalho LMS** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de postos de trabalho do Learning](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="7e9d4-171">tooconfigure single sign-on on **Learning Seat LMS** side, you need toosend hello downloaded **Metadata XML** too[Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="7e9d4-172">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="7e9d4-172">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e9d4-173">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e9d4-174">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e9d4-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e9d4-175">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e9d4-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="7e9d4-176">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="7e9d4-178">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7e9d4-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e9d4-179">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e9d4-181">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e9d4-183">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e9d4-185">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7e9d4-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e9d4-187">a.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-187">a.</span></span> <span data-ttu-id="7e9d4-188">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e9d4-189">b.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-189">b.</span></span> <span data-ttu-id="7e9d4-190">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7e9d4-191">c.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-191">c.</span></span> <span data-ttu-id="7e9d4-192">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7e9d4-193">d.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-193">d.</span></span> <span data-ttu-id="7e9d4-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="7e9d4-195">Criar um utilizador de teste LMS de postos de trabalho de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="7e9d4-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="7e9d4-196">Nesta secção, vai criar um utilizador chamado Britta Simon no Learning LMS de postos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="7e9d4-197">Contacte [equipa de suporte de postos de trabalho do Learning](http://help.learningseatlms.com/help) com todos os Olá utilizador informações tooadd Olá utilizadores Olá aplicação LMS de postos de trabalho de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all hello user information tooadd hello users in hello Learning Seat LMS application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7e9d4-198">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e9d4-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7e9d4-199">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooLearning LMS posto de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearning Seat LMS.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="7e9d4-201">**tooassign Britta Simon tooLearning LMS posto de trabalho, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="7e9d4-201">**tooassign Britta Simon tooLearning Seat LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e9d4-202">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="7e9d4-204">Na lista de aplicações de Olá, selecione **Learning posto de trabalho LMS**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-204">In hello applications list, select **Learning Seat LMS**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="7e9d4-206">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="7e9d4-208">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-208">Click **Add** button.</span></span> <span data-ttu-id="7e9d4-209">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="7e9d4-211">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e9d4-212">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e9d4-213">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7e9d4-214">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="7e9d4-214">Testing single sign-on</span></span>

<span data-ttu-id="7e9d4-215">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> 

<span data-ttu-id="7e9d4-216">Clique em Olá Learning posto de trabalho LMS na peça de mosaico Olá painel de acesso, será aplicações de aprendizagem posto de trabalho LMS tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="7e9d4-216">Click hello Learning Seat LMS tile in hello Access Panel, you will be automatically signed-on tooyour Learning Seat LMS application.</span></span> <span data-ttu-id="7e9d4-217">Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="7e9d4-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e9d4-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7e9d4-218">Additional resources</span></span>

* [<span data-ttu-id="7e9d4-219">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e9d4-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e9d4-220">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e9d4-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

