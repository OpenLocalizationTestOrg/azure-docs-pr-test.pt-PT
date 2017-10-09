---
title: "Tutorial: Integração do Azure Active Directory com Overdrive | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Overdrive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0aafacdedee25587132fc88ff93829f4367b0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive"></a><span data-ttu-id="6450b-103">Tutorial: Integração do Azure Active Directory com Overdrive</span><span class="sxs-lookup"><span data-stu-id="6450b-103">Tutorial: Azure Active Directory integration with Overdrive</span></span> 

<span data-ttu-id="6450b-104">Neste tutorial, saiba como toointegrate Overdrive com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6450b-104">In this tutorial, you learn how toointegrate Overdrive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6450b-105">Integrar Overdrive com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="6450b-105">Integrating Overdrive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6450b-106">Pode controlar no Azure AD que tenha acesso tooOverdrive</span><span class="sxs-lookup"><span data-stu-id="6450b-106">You can control in Azure AD who has access tooOverdrive</span></span> 
- <span data-ttu-id="6450b-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooOverdrive (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6450b-107">You can enable your users tooautomatically get signed-on tooOverdrive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6450b-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6450b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6450b-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6450b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6450b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6450b-110">Prerequisites</span></span>

<span data-ttu-id="6450b-111">integração do Azure AD com Overdrive tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6450b-111">tooconfigure Azure AD integration with Overdrive, you need hello following items:</span></span>

- <span data-ttu-id="6450b-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6450b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6450b-113">Um Overdrive-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="6450b-113">An Overdrive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6450b-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6450b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6450b-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6450b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6450b-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6450b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6450b-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6450b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6450b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6450b-118">Scenario description</span></span>
<span data-ttu-id="6450b-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6450b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6450b-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="6450b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6450b-121">Adicionar Overdrive da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6450b-121">Adding Overdrive from hello gallery</span></span>
2. <span data-ttu-id="6450b-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6450b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-overdrive-from-hello-gallery"></a><span data-ttu-id="6450b-123">Adicionar Overdrive da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6450b-123">Adding Overdrive from hello gallery</span></span>
<span data-ttu-id="6450b-124">integração de Olá tooconfigure de Overdrive com o Azure AD, é necessário tooadd Overdrive Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="6450b-124">tooconfigure hello integration of Overdrive into Azure AD, you need tooadd Overdrive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6450b-125">**tooadd Overdrive da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6450b-125">**tooadd Overdrive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6450b-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6450b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6450b-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6450b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6450b-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6450b-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="6450b-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6450b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="6450b-133">Na caixa de pesquisa de Olá, escreva **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="6450b-133">In hello search box, type **Overdrive**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_search.png)

5. <span data-ttu-id="6450b-135">No painel de resultados de Olá, selecione **Overdrive**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="6450b-135">In hello results panel, select **Overdrive**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6450b-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6450b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6450b-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Overdrive com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6450b-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6450b-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Overdrive é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6450b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Overdrive is tooa user in Azure AD.</span></span> <span data-ttu-id="6450b-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Overdrive tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6450b-140">In other words, a link relationship between an Azure AD user and hello related user in Overdrive needs toobe established.</span></span>

<span data-ttu-id="6450b-141">No Overdrive, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="6450b-141">In Overdrive, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6450b-142">tooconfigure e teste do Azure AD-início de sessão único com Overdrive, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6450b-142">tooconfigure and test Azure AD single sign-on with Overdrive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6450b-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="6450b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6450b-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6450b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6450b-145">**[Criar um utilizador de teste Overdrive](#creating-an-overdrive-test-user)**  -toohave um homólogo de Britta Simon no Overdrive é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="6450b-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - toohave a counterpart of Britta Simon in Overdrive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6450b-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6450b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6450b-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="6450b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6450b-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6450b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6450b-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Overdrive.</span><span class="sxs-lookup"><span data-stu-id="6450b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Overdrive  application.</span></span>

<span data-ttu-id="6450b-150">**tooconfigure do Azure AD-início de sessão único com Overdrive, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6450b-150">**tooconfigure Azure AD single sign-on with Overdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="6450b-151">No Olá portal do Azure, no Olá **Overdrive** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="6450b-151">In hello Azure portal, on hello **Overdrive** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="6450b-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6450b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_samlbase.png)

3. <span data-ttu-id="6450b-155">No Olá **Overdrive domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6450b-155">On hello **Overdrive Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_url.png)

    <span data-ttu-id="6450b-157">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`http://<subdomain>.libraryreserve.com`</span><span class="sxs-lookup"><span data-stu-id="6450b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<subdomain>.libraryreserve.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6450b-158">o valor de Olá não é real.</span><span class="sxs-lookup"><span data-stu-id="6450b-158">hello value is not real.</span></span> <span data-ttu-id="6450b-159">Atualização Olá valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="6450b-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="6450b-160">Contacte [equipa de suporte de cliente Overdrive](https://help.overdrive.com/) valor de Olá tooget.</span><span class="sxs-lookup"><span data-stu-id="6450b-160">Contact [Overdrive Client support team](https://help.overdrive.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="6450b-161">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6450b-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_certificate.png) 

5. <span data-ttu-id="6450b-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="6450b-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6450b-165">tooconfigure-início de sessão único em **Overdrive** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de Overdrive](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="6450b-165">tooconfigure single sign-on on **Overdrive** side, you need toosend hello downloaded **Metadata XML** too[Overdrive support team](https://help.overdrive.com/).</span></span> <span data-ttu-id="6450b-166">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="6450b-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="6450b-167">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="6450b-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6450b-168">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="6450b-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6450b-169">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6450b-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6450b-170">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6450b-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="6450b-171">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6450b-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="6450b-173">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6450b-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6450b-174">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6450b-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6450b-176">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="6450b-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6450b-178">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="6450b-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6450b-180">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6450b-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6450b-182">a.</span><span class="sxs-lookup"><span data-stu-id="6450b-182">a.</span></span> <span data-ttu-id="6450b-183">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6450b-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6450b-184">b.</span><span class="sxs-lookup"><span data-stu-id="6450b-184">b.</span></span> <span data-ttu-id="6450b-185">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6450b-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6450b-186">c.</span><span class="sxs-lookup"><span data-stu-id="6450b-186">c.</span></span> <span data-ttu-id="6450b-187">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="6450b-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6450b-188">d.</span><span class="sxs-lookup"><span data-stu-id="6450b-188">d.</span></span> <span data-ttu-id="6450b-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6450b-189">Click **Create**.</span></span>
 
### <a name="creating-an-overdrive-test-user"></a><span data-ttu-id="6450b-190">Criar um utilizador de teste Overdrive</span><span class="sxs-lookup"><span data-stu-id="6450b-190">Creating an Overdrive test user</span></span>

<span data-ttu-id="6450b-191">Não há nenhum item de ação para tooconfigure aprovisionamento de utilizadores tooOverDrive.</span><span class="sxs-lookup"><span data-stu-id="6450b-191">There is no action item for you tooconfigure user provisioning tooOverDrive.</span></span>  

<span data-ttu-id="6450b-192">Quando um toolog de tentativas de utilizador atribuído no tooOverDrive, uma conta de OverDrive é criada automaticamente se necessário.</span><span class="sxs-lookup"><span data-stu-id="6450b-192">When an assigned user tries toolog in tooOverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="6450b-193">Pode utilizar quaisquer outras OverDrive utilizador conta criação ferramentas ou APIs fornecidas pelo OverDrive tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="6450b-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive tooprovision AAD user accounts.</span></span>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6450b-194">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6450b-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6450b-195">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooOverdrive.</span><span class="sxs-lookup"><span data-stu-id="6450b-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOverdrive.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="6450b-197">**tooassign Britta Simon tooOverdrive, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6450b-197">**tooassign Britta Simon tooOverdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="6450b-198">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6450b-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="6450b-200">Na lista de aplicações de Olá, selecione **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="6450b-200">In hello applications list, select **Overdrive**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_app.png) 

3. <span data-ttu-id="6450b-202">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6450b-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="6450b-204">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="6450b-204">Click **Add** button.</span></span> <span data-ttu-id="6450b-205">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6450b-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="6450b-207">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="6450b-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6450b-208">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6450b-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6450b-209">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6450b-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6450b-210">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6450b-210">Testing single sign-on</span></span>

<span data-ttu-id="6450b-211">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="6450b-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6450b-212">Ao clicar em mosaico de Overdrive Olá no painel de acesso de Olá, deve obter a aplicação de Overdrive tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="6450b-212">When you click hello Overdrive tile in hello Access Panel, you should get automatically signed-on tooyour Overdrive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6450b-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6450b-213">Additional resources</span></span>

* [<span data-ttu-id="6450b-214">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6450b-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6450b-215">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6450b-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_203.png

