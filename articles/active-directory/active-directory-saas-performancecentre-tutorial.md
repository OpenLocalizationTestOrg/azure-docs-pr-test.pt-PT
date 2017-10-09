---
title: "Tutorial: Integração do Azure Active Directory com PerformanceCentre | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 19781c0087093a67c70dc90072cf1a119bb2ade0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="0ba46-103">Tutorial: Integração do Azure Active Directory com PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="0ba46-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="0ba46-104">Neste tutorial, saiba como toointegrate PerformanceCentre com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ba46-104">In this tutorial, you learn how toointegrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0ba46-105">Integrar PerformanceCentre com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="0ba46-105">Integrating PerformanceCentre with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0ba46-106">Pode controlar no Azure AD que tenha acesso tooPerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="0ba46-106">You can control in Azure AD who has access tooPerformanceCentre</span></span>
- <span data-ttu-id="0ba46-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooPerformanceCentre (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ba46-107">You can enable your users tooautomatically get signed-on tooPerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0ba46-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0ba46-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0ba46-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0ba46-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ba46-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0ba46-110">Prerequisites</span></span>

<span data-ttu-id="0ba46-111">integração do Azure AD com PerformanceCentre tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0ba46-111">tooconfigure Azure AD integration with PerformanceCentre, you need hello following items:</span></span>

- <span data-ttu-id="0ba46-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ba46-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0ba46-113">Um PerformanceCentre-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="0ba46-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0ba46-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="0ba46-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0ba46-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="0ba46-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0ba46-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="0ba46-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0ba46-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ba46-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0ba46-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="0ba46-118">Scenario description</span></span>
<span data-ttu-id="0ba46-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="0ba46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0ba46-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="0ba46-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0ba46-121">Adicionar PerformanceCentre da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="0ba46-121">Adding PerformanceCentre from hello gallery</span></span>
2. <span data-ttu-id="0ba46-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="0ba46-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-hello-gallery"></a><span data-ttu-id="0ba46-123">Adicionar PerformanceCentre da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="0ba46-123">Adding PerformanceCentre from hello gallery</span></span>
<span data-ttu-id="0ba46-124">tooconfigure Olá integração de PerformanceCentre com o Azure AD, é necessário tooadd PerformanceCentre Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="0ba46-124">tooconfigure hello integration of PerformanceCentre into Azure AD, you need tooadd PerformanceCentre from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0ba46-125">**tooadd PerformanceCentre da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0ba46-125">**tooadd PerformanceCentre from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ba46-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="0ba46-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0ba46-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0ba46-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="0ba46-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ba46-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="0ba46-133">Na caixa de pesquisa de Olá, escreva **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-133">In hello search box, type **PerformanceCentre**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="0ba46-135">No painel de resultados de Olá, selecione **PerformanceCentre**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="0ba46-135">In hello results panel, select **PerformanceCentre**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0ba46-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="0ba46-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0ba46-138">Nesta secção, configure e teste do Azure AD-início de sessão único com PerformanceCentre com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0ba46-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0ba46-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá PerformanceCentre é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ba46-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in PerformanceCentre is tooa user in Azure AD.</span></span> <span data-ttu-id="0ba46-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá PerformanceCentre tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0ba46-140">In other words, a link relationship between an Azure AD user and hello related user in PerformanceCentre needs toobe established.</span></span>

<span data-ttu-id="0ba46-141">No PerformanceCentre, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="0ba46-141">In PerformanceCentre, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0ba46-142">tooconfigure e teste do Azure AD-início de sessão único com PerformanceCentre, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0ba46-142">tooconfigure and test Azure AD single sign-on with PerformanceCentre, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0ba46-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="0ba46-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0ba46-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0ba46-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0ba46-145">**[Criar um utilizador de teste PerformanceCentre](#creating-a-performancecentre-test-user)**  -toohave um homólogo de Britta Simon no PerformanceCentre é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="0ba46-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - toohave a counterpart of Britta Simon in PerformanceCentre that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0ba46-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="0ba46-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0ba46-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="0ba46-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0ba46-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="0ba46-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0ba46-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="0ba46-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="0ba46-150">**tooconfigure do Azure AD-início de sessão único com PerformanceCentre, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0ba46-150">**tooconfigure Azure AD single sign-on with PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ba46-151">No Olá portal do Azure, no Olá **PerformanceCentre** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-151">In hello Azure portal, on hello **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="0ba46-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="0ba46-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="0ba46-155">No Olá **PerformanceCentre domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0ba46-155">On hello **PerformanceCentre Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="0ba46-157">a.</span><span class="sxs-lookup"><span data-stu-id="0ba46-157">a.</span></span> <span data-ttu-id="0ba46-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="0ba46-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="0ba46-159">b.</span><span class="sxs-lookup"><span data-stu-id="0ba46-159">b.</span></span> <span data-ttu-id="0ba46-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="0ba46-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0ba46-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="0ba46-161">These values are not real.</span></span> <span data-ttu-id="0ba46-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="0ba46-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0ba46-163">Contacte [equipa de suporte de cliente PerformanceCentre](https://www.performancecentre.com/contact-us/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="0ba46-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) tooget these values.</span></span> 

4. <span data-ttu-id="0ba46-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="0ba46-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="0ba46-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="0ba46-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0ba46-168">No Olá **PerformanceCentre configuração** secção, clique em **configurar PerformanceCentre** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="0ba46-168">On hello **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0ba46-169">Olá cópia **ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="0ba46-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="0ba46-171">Início de sessão tooyour **PerformanceCentre** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="0ba46-171">Sign-on tooyour **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="0ba46-172">No separador de Olá no lado esquerdo Olá, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-172">In hello tab on hello left side, click **Configure**.</span></span>
   
    ![Azure AD início de sessão único][10]

9. <span data-ttu-id="0ba46-174">No separador de Olá no lado esquerdo Olá, clique em **diversos**e, em seguida, clique em **início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-174">In hello tab on hello left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Azure AD início de sessão único][11]

10. <span data-ttu-id="0ba46-176">Como **protocolo**, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Azure AD início de sessão único][12]

11. <span data-ttu-id="0ba46-178">Abra o ficheiro de metadados transferido no bloco de notas, cópia Olá conteúdo, cole-o Olá **metadados do fornecedor de identidade** caixa de texto e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-178">Open your downloaded metadata file in notepad, copy hello content, paste it into hello **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Azure AD início de sessão único][13]

12. <span data-ttu-id="0ba46-180">Certifique-se de que os valores de Olá para Olá **URL de Base de entidade** e **URL de ID de entidade** estão corretos.</span><span class="sxs-lookup"><span data-stu-id="0ba46-180">Verify that hello values for hello **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Azure AD início de sessão único][14]

> [!TIP]
> <span data-ttu-id="0ba46-182">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="0ba46-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0ba46-183">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ba46-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0ba46-184">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0ba46-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0ba46-185">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ba46-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="0ba46-186">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ba46-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="0ba46-188">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0ba46-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ba46-189">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="0ba46-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0ba46-191">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0ba46-193">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="0ba46-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0ba46-195">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0ba46-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0ba46-197">a.</span><span class="sxs-lookup"><span data-stu-id="0ba46-197">a.</span></span> <span data-ttu-id="0ba46-198">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0ba46-199">b.</span><span class="sxs-lookup"><span data-stu-id="0ba46-199">b.</span></span> <span data-ttu-id="0ba46-200">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0ba46-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0ba46-201">c.</span><span class="sxs-lookup"><span data-stu-id="0ba46-201">c.</span></span> <span data-ttu-id="0ba46-202">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0ba46-203">d.</span><span class="sxs-lookup"><span data-stu-id="0ba46-203">d.</span></span> <span data-ttu-id="0ba46-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="0ba46-205">Criar um utilizador de teste PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="0ba46-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="0ba46-206">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="0ba46-206">hello objective of this section is toocreate a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="0ba46-207">**toocreate um utilizador chamar Britta Simon PerformanceCentre, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0ba46-207">**toocreate a user called Britta Simon in PerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ba46-208">Início de sessão tooyour PerformanceCentre site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="0ba46-208">Sign on tooyour PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="0ba46-209">No menu de Olá Olá esquerda, clique em **Interrelate**e, em seguida, clique em **criar participante**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-209">In hello menu on hello left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Criar utilizador][400]

3. <span data-ttu-id="0ba46-211">No Olá **Interrelate - criar participante** caixa de diálogo, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0ba46-211">On hello **Interrelate - Create Participant** dialog, perform hello following steps:</span></span>
   
    ![Criar utilizador][401]
    
    <span data-ttu-id="0ba46-213">a.</span><span class="sxs-lookup"><span data-stu-id="0ba46-213">a.</span></span> <span data-ttu-id="0ba46-214">Tipo de atributos de Olá necessário para Britta Simon para caixas de texto relacionadas.</span><span class="sxs-lookup"><span data-stu-id="0ba46-214">Type hello required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="0ba46-215">Nome de utilizador de Britta tem de ser um atributo no PerformanceCentre Olá igual ao hello do nome de utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ba46-215">Britta's User Name attribute in PerformanceCentre must be hello same as hello User Name in Azure AD.</span></span>
    
    <span data-ttu-id="0ba46-216">b.</span><span class="sxs-lookup"><span data-stu-id="0ba46-216">b.</span></span> <span data-ttu-id="0ba46-217">Selecione **cliente administrador** como **escolha função**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="0ba46-218">c.</span><span class="sxs-lookup"><span data-stu-id="0ba46-218">c.</span></span> <span data-ttu-id="0ba46-219">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-219">Click **Save**.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0ba46-220">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ba46-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0ba46-221">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooPerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="0ba46-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerformanceCentre.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="0ba46-223">**tooassign Britta Simon tooPerformanceCentre, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="0ba46-223">**tooassign Britta Simon tooPerformanceCentre, perform hello following steps:**</span></span>

1. <span data-ttu-id="0ba46-224">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="0ba46-226">Na lista de aplicações de Olá, selecione **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-226">In hello applications list, select **PerformanceCentre**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="0ba46-228">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0ba46-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="0ba46-230">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="0ba46-230">Click **Add** button.</span></span> <span data-ttu-id="0ba46-231">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ba46-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="0ba46-233">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="0ba46-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0ba46-234">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ba46-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0ba46-235">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0ba46-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0ba46-236">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="0ba46-236">Testing single sign-on</span></span>

<span data-ttu-id="0ba46-237">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="0ba46-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="0ba46-238">Ao clicar em mosaico de PerformanceCentre Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour PerformanceCentre aplicação.</span><span class="sxs-lookup"><span data-stu-id="0ba46-238">When you click hello PerformanceCentre tile in hello Access Panel, you should get automatically signed-on tooyour PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0ba46-239">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0ba46-239">Additional resources</span></span>

* [<span data-ttu-id="0ba46-240">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ba46-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0ba46-241">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0ba46-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

