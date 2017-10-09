---
title: "Tutorial: Integração do Azure Active Directory com Bambu por Sprout sociais | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Bambu por Sprout redes sociais."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="b51f1-103">Tutorial: Integração do Azure Active Directory com Bambu por Sprout redes sociais</span><span class="sxs-lookup"><span data-stu-id="b51f1-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="b51f1-104">Neste tutorial, saiba como toointegrate Bambu por Sprout sociais com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b51f1-104">In this tutorial, you learn how toointegrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b51f1-105">Integrar Bambu por Sprout sociais com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="b51f1-105">Integrating Bambu by Sprout Social with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b51f1-106">Pode controlar no Azure AD que tenha acesso tooBambu por Sprout redes sociais</span><span class="sxs-lookup"><span data-stu-id="b51f1-106">You can control in Azure AD who has access tooBambu by Sprout Social</span></span>
- <span data-ttu-id="b51f1-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooBambu por Sprout sociais (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b51f1-107">You can enable your users tooautomatically get signed-on tooBambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b51f1-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b51f1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b51f1-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b51f1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="b51f1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b51f1-110">Prerequisites</span></span>

<span data-ttu-id="b51f1-111">integração do Azure AD com Bambu por Sprout sociais tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b51f1-111">tooconfigure Azure AD integration with Bambu by Sprout Social, you need hello following items:</span></span>

- <span data-ttu-id="b51f1-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b51f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b51f1-113">Um Bambu por Sprout sociais início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="b51f1-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b51f1-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b51f1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b51f1-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b51f1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b51f1-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="b51f1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b51f1-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b51f1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b51f1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b51f1-118">Scenario description</span></span>
<span data-ttu-id="b51f1-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b51f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b51f1-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="b51f1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b51f1-121">Adicionar Bambu por Sprout sociais na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="b51f1-121">Adding Bambu by Sprout Social from hello gallery</span></span>
2. <span data-ttu-id="b51f1-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="b51f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a><span data-ttu-id="b51f1-123">Adicionar Bambu por Sprout sociais na Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="b51f1-123">Adding Bambu by Sprout Social from hello gallery</span></span>
<span data-ttu-id="b51f1-124">tooconfigure Olá integração de Bambu por Sprout sociais com o Azure AD, é necessário tooadd Bambu por Sprout sociais Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="b51f1-124">tooconfigure hello integration of Bambu by Sprout Social into Azure AD, you need tooadd Bambu by Sprout Social from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b51f1-125">**tooadd Bambu por Sprout sociais na Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b51f1-125">**tooadd Bambu by Sprout Social from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b51f1-126">No Olá  **[Portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="b51f1-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b51f1-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b51f1-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="b51f1-131">Clique em **nova aplicação** botão na parte superior de Olá da nova aplicação tooadd da caixa de diálogo de Olá.</span><span class="sxs-lookup"><span data-stu-id="b51f1-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="b51f1-133">Na caixa de pesquisa de Olá, escreva **Bambu por Sprout sociais**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-133">In hello search box, type **Bambu by Sprout Social**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="b51f1-135">No painel de resultados de Olá, selecione **Bambu por Sprout sociais**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="b51f1-135">In hello results panel, select **Bambu by Sprout Social**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b51f1-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="b51f1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b51f1-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Bambu por Sprout redes sociais com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b51f1-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b51f1-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Bambu por Sprout sociais é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b51f1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bambu by Sprout Social is tooa user in Azure AD.</span></span> <span data-ttu-id="b51f1-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Bambu por Sprout sociais tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b51f1-140">In other words, a link relationship between an Azure AD user and hello related user in Bambu by Sprout Social needs toobe established.</span></span>

<span data-ttu-id="b51f1-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Bambu por Sprout redes sociais.</span><span class="sxs-lookup"><span data-stu-id="b51f1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="b51f1-142">tooconfigure e teste do Azure AD-início de sessão único com Bambu por Sprout sociais, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="b51f1-142">tooconfigure and test Azure AD single sign-on with Bambu by Sprout Social, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b51f1-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="b51f1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b51f1-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b51f1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b51f1-145">**[Criar um Bambu pelo utilizador de teste Sprout sociais](#creating-a-bambu-by-sprout-social-test-user)**  -toohave um homólogo de Britta Simon no Bambu por Sprout sociais que é a representação de toohello ligado do Azure AD de forma.</span><span class="sxs-lookup"><span data-stu-id="b51f1-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - toohave a counterpart of Britta Simon in Bambu by Sprout Social that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b51f1-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="b51f1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b51f1-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="b51f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b51f1-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="b51f1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b51f1-149">Nesta secção, ativar o Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua Bambu por aplicação Sprout redes sociais.</span><span class="sxs-lookup"><span data-stu-id="b51f1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="b51f1-150">**tooconfigure do Azure AD-início de sessão único com Bambu por Sprout redes sociais, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b51f1-150">**tooconfigure Azure AD single sign-on with Bambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="b51f1-151">No Olá portal do Azure, no Olá **Bambu por Sprout sociais** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-151">In hello Azure portal, on hello **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="b51f1-153">No Olá **de sessão único-** caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="b51f1-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="b51f1-155">No Olá **Bambu Sprout domínio redes sociais e URLs** secção, hello utilizador não tem tooperform quaisquer passos conforme Olá aplicação já está pré-integrada com o Azure.</span><span class="sxs-lookup"><span data-stu-id="b51f1-155">On hello **Bambu by Sprout Social Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="b51f1-157">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="b51f1-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="b51f1-159">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="b51f1-159">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="b51f1-161">No Olá **Bambu pela configuração de redes sociais Sprout** secção, clique em **configurar Bambu por Sprout sociais** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="b51f1-161">On hello **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b51f1-162">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b51f1-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="b51f1-164">tooconfigure-início de sessão único em **Bambu por Sprout sociais** lado, terá de Olá toosend transferido **XML de metadados** e **único início de sessão no URL do serviço SAML** demasiado[Bambu pelo suporte Sprout sociais](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="b51f1-164">tooconfigure single sign-on on **Bambu by Sprout Social** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="b51f1-165">Estes irão configurar esta no Olá de toohave ordem corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="b51f1-165">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b51f1-166">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="b51f1-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b51f1-167">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="b51f1-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click on hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b51f1-168">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b51f1-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b51f1-169">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b51f1-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="b51f1-170">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b51f1-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="b51f1-172">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b51f1-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b51f1-173">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="b51f1-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b51f1-175">Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="b51f1-175">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b51f1-177">Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b51f1-177">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b51f1-179">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="b51f1-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b51f1-181">a.</span><span class="sxs-lookup"><span data-stu-id="b51f1-181">a.</span></span> <span data-ttu-id="b51f1-182">No Olá **nome** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-182">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="b51f1-183">b.</span><span class="sxs-lookup"><span data-stu-id="b51f1-183">b.</span></span> <span data-ttu-id="b51f1-184">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b51f1-184">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b51f1-185">c.</span><span class="sxs-lookup"><span data-stu-id="b51f1-185">c.</span></span> <span data-ttu-id="b51f1-186">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b51f1-187">d.</span><span class="sxs-lookup"><span data-stu-id="b51f1-187">d.</span></span> <span data-ttu-id="b51f1-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="b51f1-189">Criar um Bambu pelo utilizador de teste Sprout redes sociais</span><span class="sxs-lookup"><span data-stu-id="b51f1-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="b51f1-190">Aplicação suporta apenas no tempo de aprovisionamento de utilizador e de utilizadores de autenticação serão criados na aplicação Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b51f1-190">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b51f1-191">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b51f1-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b51f1-192">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooBambu acesso por Sprout redes sociais.</span><span class="sxs-lookup"><span data-stu-id="b51f1-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBambu by Sprout Social.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="b51f1-194">**tooassign Britta Simon tooBambu por Sprout redes sociais, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b51f1-194">**tooassign Britta Simon tooBambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="b51f1-195">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="b51f1-197">Na lista de aplicações de Olá, selecione **Bambu por Sprout sociais**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-197">In hello applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="b51f1-199">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b51f1-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="b51f1-201">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="b51f1-201">Click **Add** button.</span></span> <span data-ttu-id="b51f1-202">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b51f1-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="b51f1-204">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="b51f1-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b51f1-205">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b51f1-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b51f1-206">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b51f1-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b51f1-207">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="b51f1-207">Testing single sign-on</span></span>

<span data-ttu-id="b51f1-208">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="b51f1-208">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b51f1-209">Ao clicar Olá Bambu pelo mosaico Sprout sociais no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Bambu por aplicação Sprout redes sociais.</span><span class="sxs-lookup"><span data-stu-id="b51f1-209">When you click hello Bambu by Sprout Social tile in hello Access Panel, you should get automatically signed-on tooyour Bambu by Sprout Social application.</span></span> <span data-ttu-id="b51f1-210">Para obter mais detalhes sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b51f1-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b51f1-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b51f1-211">Additional resources</span></span>

* [<span data-ttu-id="b51f1-212">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b51f1-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b51f1-213">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b51f1-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

