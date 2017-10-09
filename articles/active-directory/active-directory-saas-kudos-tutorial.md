---
title: "Tutorial: Integração do Azure Active Directory com Kudos | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: c1b481463574461f9948db2b83843fefa5d74e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="564dd-103">Tutorial: Integração do Azure Active Directory com Kudos</span><span class="sxs-lookup"><span data-stu-id="564dd-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="564dd-104">Neste tutorial, saiba como toointegrate Kudos com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="564dd-104">In this tutorial, you learn how toointegrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="564dd-105">Integrar Kudos com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="564dd-105">Integrating Kudos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="564dd-106">Pode controlar no Azure AD que tenha acesso tooKudos</span><span class="sxs-lookup"><span data-stu-id="564dd-106">You can control in Azure AD who has access tooKudos</span></span>
- <span data-ttu-id="564dd-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooKudos (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="564dd-107">You can enable your users tooautomatically get signed-on tooKudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="564dd-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="564dd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="564dd-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="564dd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="564dd-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="564dd-110">Prerequisites</span></span>

<span data-ttu-id="564dd-111">integração do Azure AD com Kudos tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="564dd-111">tooconfigure Azure AD integration with Kudos, you need hello following items:</span></span>

- <span data-ttu-id="564dd-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="564dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="564dd-113">Um Kudos-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="564dd-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="564dd-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="564dd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="564dd-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="564dd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="564dd-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="564dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="564dd-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="564dd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="564dd-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="564dd-118">Scenario description</span></span>
<span data-ttu-id="564dd-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="564dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="564dd-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="564dd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="564dd-121">Adicionar Kudos da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="564dd-121">Adding Kudos from hello gallery</span></span>
2. <span data-ttu-id="564dd-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="564dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-hello-gallery"></a><span data-ttu-id="564dd-123">Adicionar Kudos da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="564dd-123">Adding Kudos from hello gallery</span></span>
<span data-ttu-id="564dd-124">tooconfigure Olá integração de Kudos com o Azure AD, é necessário tooadd Kudos Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="564dd-124">tooconfigure hello integration of Kudos into Azure AD, you need tooadd Kudos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="564dd-125">**tooadd Kudos da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="564dd-125">**tooadd Kudos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="564dd-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="564dd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="564dd-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="564dd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="564dd-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="564dd-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="564dd-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="564dd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="564dd-133">Na caixa de pesquisa de Olá, escreva **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="564dd-133">In hello search box, type **Kudos**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="564dd-135">No painel de resultados de Olá, selecione **Kudos**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="564dd-135">In hello results panel, select **Kudos**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="564dd-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="564dd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="564dd-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Kudos com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="564dd-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="564dd-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Kudos é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="564dd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kudos is tooa user in Azure AD.</span></span> <span data-ttu-id="564dd-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Kudos tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="564dd-140">In other words, a link relationship between an Azure AD user and hello related user in Kudos needs toobe established.</span></span>

<span data-ttu-id="564dd-141">No Kudos, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="564dd-141">In Kudos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="564dd-142">tooconfigure e teste do Azure AD-início de sessão único com Kudos, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="564dd-142">tooconfigure and test Azure AD single sign-on with Kudos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="564dd-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="564dd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="564dd-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="564dd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="564dd-145">**[Criar um utilizador de teste Kudos](#creating-a-kudos-test-user)**  -toohave um homólogo de Britta Simon no Kudos é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="564dd-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - toohave a counterpart of Britta Simon in Kudos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="564dd-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="564dd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="564dd-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="564dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="564dd-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="564dd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="564dd-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Kudos.</span><span class="sxs-lookup"><span data-stu-id="564dd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="564dd-150">**tooconfigure do Azure AD-início de sessão único com Kudos, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="564dd-150">**tooconfigure Azure AD single sign-on with Kudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="564dd-151">No Olá portal do Azure, no Olá **Kudos** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="564dd-151">In hello Azure portal, on hello **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="564dd-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="564dd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="564dd-155">No Olá **Kudos domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="564dd-155">On hello **Kudos Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="564dd-157">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="564dd-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="564dd-158">Este valor não é real.</span><span class="sxs-lookup"><span data-stu-id="564dd-158">This value is not real.</span></span> <span data-ttu-id="564dd-159">Atualizar este valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="564dd-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="564dd-160">Contacte [equipa de suporte de cliente Kudos](http://success.kudosnow.com/home) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="564dd-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) tooget this value.</span></span> 
 
4. <span data-ttu-id="564dd-161">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="564dd-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="564dd-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="564dd-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="564dd-165">No Olá **Kudos configuração** secção, clique em **configurar Kudos** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="564dd-165">On hello **Kudos Configuration** section, click **Configure Kudos** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="564dd-166">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="564dd-166">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="564dd-168">Numa janela do browser web diferente, inicie sessão no site da sua empresa Kudos como administrador.</span><span class="sxs-lookup"><span data-stu-id="564dd-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="564dd-169">No menu de Olá na parte superior do Olá, clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="564dd-169">In hello menu on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="564dd-170">![Definições](./media/active-directory-saas-kudos-tutorial/ic787806.png "definições")</span><span class="sxs-lookup"><span data-stu-id="564dd-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="564dd-171">Clique em **integrações \> SSO**.</span><span class="sxs-lookup"><span data-stu-id="564dd-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="564dd-172">No Olá **SSO** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="564dd-172">In hello **SSO** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="564dd-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="564dd-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="564dd-174">a.</span><span class="sxs-lookup"><span data-stu-id="564dd-174">a.</span></span> <span data-ttu-id="564dd-175">No **iniciar sessão no URL** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="564dd-175">In **Sign on URL** textbox, paste hello value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="564dd-176">b.</span><span class="sxs-lookup"><span data-stu-id="564dd-176">b.</span></span> <span data-ttu-id="564dd-177">Abra o certificado codificado base-64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado x. 509** caixa de texto</span><span class="sxs-lookup"><span data-stu-id="564dd-177">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="564dd-178">c.</span><span class="sxs-lookup"><span data-stu-id="564dd-178">c.</span></span> <span data-ttu-id="564dd-179">No **tooURL de fim de sessão**, cole o valor Olá **Sign-Out URL** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="564dd-179">In **Logout tooURL**, paste hello value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="564dd-180">d.</span><span class="sxs-lookup"><span data-stu-id="564dd-180">d.</span></span> <span data-ttu-id="564dd-181">No Olá **seu URL de Kudos** caixa de texto, escreva o nome da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="564dd-181">In hello **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="564dd-182">e.</span><span class="sxs-lookup"><span data-stu-id="564dd-182">e.</span></span> <span data-ttu-id="564dd-183">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="564dd-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="564dd-184">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="564dd-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="564dd-185">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="564dd-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="564dd-186">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="564dd-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="564dd-187">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="564dd-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="564dd-188">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="564dd-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="564dd-190">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="564dd-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="564dd-191">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="564dd-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="564dd-193">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="564dd-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="564dd-195">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="564dd-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="564dd-197">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="564dd-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="564dd-199">a.</span><span class="sxs-lookup"><span data-stu-id="564dd-199">a.</span></span> <span data-ttu-id="564dd-200">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="564dd-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="564dd-201">b.</span><span class="sxs-lookup"><span data-stu-id="564dd-201">b.</span></span> <span data-ttu-id="564dd-202">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="564dd-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="564dd-203">c.</span><span class="sxs-lookup"><span data-stu-id="564dd-203">c.</span></span> <span data-ttu-id="564dd-204">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="564dd-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="564dd-205">d.</span><span class="sxs-lookup"><span data-stu-id="564dd-205">d.</span></span> <span data-ttu-id="564dd-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="564dd-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="564dd-207">Criar um utilizador de teste Kudos</span><span class="sxs-lookup"><span data-stu-id="564dd-207">Creating a Kudos test user</span></span>

<span data-ttu-id="564dd-208">Na ordem tooenable do Azure AD os utilizadores toolog para Kudos, têm de ser aprovisionados para Kudos.</span><span class="sxs-lookup"><span data-stu-id="564dd-208">In order tooenable Azure AD users toolog into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="564dd-209">No caso de Olá da Kudos, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="564dd-209">In hello case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="564dd-210">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="564dd-210">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="564dd-211">Inicie sessão no tooyour **Kudos** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="564dd-211">Log in tooyour **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="564dd-212">No menu de Olá na parte superior do Olá, clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="564dd-212">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="564dd-213">![Definições](./media/active-directory-saas-kudos-tutorial/ic787806.png "definições")</span><span class="sxs-lookup"><span data-stu-id="564dd-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="564dd-214">Clique em **utilizador Admin**.</span><span class="sxs-lookup"><span data-stu-id="564dd-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="564dd-215">Clique em Olá **utilizadores** separador e, em seguida, clique em **adicionar um utilizador**.</span><span class="sxs-lookup"><span data-stu-id="564dd-215">Click hello **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="564dd-216">![Utilizador Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "utilizador Admin")</span><span class="sxs-lookup"><span data-stu-id="564dd-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="564dd-217">No Olá **adicionar um utilizador** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="564dd-217">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="564dd-218">![Adicionar um utilizador](./media/active-directory-saas-kudos-tutorial/ic787810.png "adicionar um utilizador")</span><span class="sxs-lookup"><span data-stu-id="564dd-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="564dd-219">a.</span><span class="sxs-lookup"><span data-stu-id="564dd-219">a.</span></span> <span data-ttu-id="564dd-220">Olá tipo **nome próprio**, **Apelido**, **E-Mail** e outros detalhes de uma conta válida do Azure Active Directory que pretende tooprovision Olá relacionadas com caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="564dd-220">Type hello **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   
    <span data-ttu-id="564dd-221">b.</span><span class="sxs-lookup"><span data-stu-id="564dd-221">b.</span></span> <span data-ttu-id="564dd-222">Clique em **criar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="564dd-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="564dd-223">Pode utilizar quaisquer outras Kudos utilizador conta criação ferramentas ou APIs fornecidas pelo Kudos tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="564dd-223">You can use any other Kudos user account creation tools or APIs provided by Kudos tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="564dd-224">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="564dd-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="564dd-225">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooKudos.</span><span class="sxs-lookup"><span data-stu-id="564dd-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKudos.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="564dd-227">**tooassign Britta Simon tooKudos, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="564dd-227">**tooassign Britta Simon tooKudos, perform hello following steps:**</span></span>

1. <span data-ttu-id="564dd-228">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="564dd-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="564dd-230">Na lista de aplicações de Olá, selecione **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="564dd-230">In hello applications list, select **Kudos**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="564dd-232">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="564dd-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="564dd-234">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="564dd-234">Click **Add** button.</span></span> <span data-ttu-id="564dd-235">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="564dd-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="564dd-237">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="564dd-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="564dd-238">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="564dd-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="564dd-239">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="564dd-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="564dd-240">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="564dd-240">Testing single sign-on</span></span>

<span data-ttu-id="564dd-241">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="564dd-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="564dd-242">Ao clicar em mosaico de Kudos Olá no painel de acesso de Olá, deve obter a aplicação de Kudos tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="564dd-242">When you click hello Kudos tile in hello Access Panel, you should get automatically signed-on tooyour Kudos application.</span></span> <span data-ttu-id="564dd-243">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="564dd-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="564dd-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="564dd-244">Additional resources</span></span>

* [<span data-ttu-id="564dd-245">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="564dd-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="564dd-246">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="564dd-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

