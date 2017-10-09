---
title: "Tutorial: Integração do Azure Active Directory com Deputy | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Deputy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="4e4fb-103">Tutorial: Integração do Azure Active Directory com Deputy</span><span class="sxs-lookup"><span data-stu-id="4e4fb-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="4e4fb-104">Neste tutorial, saiba como toointegrate Deputy com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4e4fb-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4e4fb-105">Integrar Deputy com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4e4fb-106">Pode controlar no Azure AD que tenha acesso tooDeputy</span><span class="sxs-lookup"><span data-stu-id="4e4fb-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="4e4fb-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooDeputy (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e4fb-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4e4fb-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e4fb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4e4fb-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4e4fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e4fb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4e4fb-110">Prerequisites</span></span>

<span data-ttu-id="4e4fb-111">integração do Azure AD com Deputy tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="4e4fb-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e4fb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4e4fb-113">Um Deputy-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="4e4fb-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4e4fb-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4e4fb-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4e4fb-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4e4fb-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e4fb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4e4fb-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4e4fb-118">Scenario description</span></span>
<span data-ttu-id="4e4fb-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4e4fb-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4e4fb-121">Adicionar Deputy da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="4e4fb-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="4e4fb-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="4e4fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="4e4fb-123">Adicionar Deputy da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="4e4fb-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="4e4fb-124">tooconfigure Olá integração de Deputy com o Azure AD, é necessário tooadd Deputy Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4e4fb-125">**tooadd Deputy da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4e4fb-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e4fb-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4e4fb-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4e4fb-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="4e4fb-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="4e4fb-133">Na caixa de pesquisa de Olá, escreva **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-133">In hello search box, type **Deputy**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="4e4fb-135">No painel de resultados de Olá, selecione **Deputy**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4e4fb-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="4e4fb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4e4fb-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Deputy com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="4e4fb-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4e4fb-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Deputy é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="4e4fb-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Deputy tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="4e4fb-141">No Deputy, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4e4fb-142">tooconfigure e teste do Azure AD-início de sessão único com Deputy, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4e4fb-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4e4fb-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4e4fb-145">**[Criar um utilizador de teste Deputy](#creating-a-deputy-test-user)**  -toohave um homólogo de Britta Simon no Deputy é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4e4fb-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4e4fb-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4e4fb-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="4e4fb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4e4fb-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Deputy.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="4e4fb-150">**tooconfigure do Azure AD-início de sessão único com Deputy, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4e4fb-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e4fb-151">No Olá portal do Azure, no Olá **Deputy** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="4e4fb-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="4e4fb-155">No Olá **Deputy domínio e os URLs** secção, se desejar aplicação Olá tooconfigure **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="4e4fb-157">a.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-157">a.</span></span> <span data-ttu-id="4e4fb-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="4e4fb-159">b.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-159">b.</span></span> <span data-ttu-id="4e4fb-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="4e4fb-161">Verifique **Mostrar avançadas definições de URL**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="4e4fb-162">Se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="4e4fb-164">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="4e4fb-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="4e4fb-165">Sufixo de região Deputy é opcional, ou deve utilizar um destes: au | na | eu | como | la | af | um | ente au | ente na | ente eu | ente-como | Ente-la | Ente af | um Ente</span><span class="sxs-lookup"><span data-stu-id="4e4fb-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4e4fb-166">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-166">These values are not real.</span></span> <span data-ttu-id="4e4fb-167">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4e4fb-168">Contacte [equipa de suporte de Deputy](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="4e4fb-169">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="4e4fb-171">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-171">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="4e4fb-173">No Olá **Deputy configuração** secção, clique em **configurar Deputy** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4e4fb-174">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4e4fb-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="4e4fb-176">Navegue toohello seguinte URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="4e4fb-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="4e4fb-177">Aceda demasiado**definições de segurança** e clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="4e4fb-179">Neste **definições de segurança** página, execute passos abaixo.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="4e4fb-181">a.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-181">a.</span></span> <span data-ttu-id="4e4fb-182">Ativar **início de sessão de redes Social**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="4e4fb-183">b.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-183">b.</span></span> <span data-ttu-id="4e4fb-184">Abra o certificado codificado em Base64 transferido a partir do portal do Azure no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **OpenSSL certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="4e4fb-185">c.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-185">c.</span></span> <span data-ttu-id="4e4fb-186">Na caixa de texto de SAML SSO URL Olá, escreva`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="4e4fb-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="4e4fb-187">d.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-187">d.</span></span> <span data-ttu-id="4e4fb-188">Na caixa de texto de SAML SSO URL Olá, substitua `<your subdomain>` com o subdomínio.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="4e4fb-189">e.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-189">e.</span></span> <span data-ttu-id="4e4fb-190">Na caixa de texto de SAML SSO URL Olá, substitua `<saml sso url>` com Olá **único início de sessão no URL do serviço SAML** copiou do Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="4e4fb-191">f.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-191">f.</span></span> <span data-ttu-id="4e4fb-192">Clique em **guardar definições**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="4e4fb-193">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="4e4fb-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4e4fb-194">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4e4fb-195">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4e4fb-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4e4fb-196">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e4fb-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="4e4fb-197">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="4e4fb-199">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4e4fb-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e4fb-200">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4e4fb-202">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4e4fb-204">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4e4fb-206">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4e4fb-208">a.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-208">a.</span></span> <span data-ttu-id="4e4fb-209">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4e4fb-210">b.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-210">b.</span></span> <span data-ttu-id="4e4fb-211">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4e4fb-212">c.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-212">c.</span></span> <span data-ttu-id="4e4fb-213">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4e4fb-214">d.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-214">d.</span></span> <span data-ttu-id="4e4fb-215">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="4e4fb-216">Criar um utilizador de teste Deputy</span><span class="sxs-lookup"><span data-stu-id="4e4fb-216">Creating a Deputy test user</span></span>

<span data-ttu-id="4e4fb-217">tooenable do Azure AD os utilizadores toolog no tooDeputy, estes têm de ser aprovisionados para Deputy.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="4e4fb-218">Em caso de Deputy, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="4e4fb-219">tooprovision uma conta de utilizador, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="4e4fb-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="4e4fb-220">Inicie sessão no site da empresa tooyour Deputy como administrador.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="4e4fb-221">No painel de navegação superior Olá, clique em **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="4e4fb-222">![As pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "pessoas")</span><span class="sxs-lookup"><span data-stu-id="4e4fb-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="4e4fb-223">Clique em Olá **adicionar pessoas** botão e clique em **adicionar uma única pessoa**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="4e4fb-224">![Adicionar pessoas](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "adicionar pessoas")</span><span class="sxs-lookup"><span data-stu-id="4e4fb-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="4e4fb-225">Efetuar Olá os passos seguintes e clique em **Guardar & convidar**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="4e4fb-226">![Novo utilizador](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "novo utilizador")</span><span class="sxs-lookup"><span data-stu-id="4e4fb-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="4e4fb-227">a.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-227">a.</span></span> <span data-ttu-id="4e4fb-228">No Olá **nome** caixa de texto, nome do tipo de utilizador de Olá como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="4e4fb-229">b.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-229">b.</span></span> <span data-ttu-id="4e4fb-230">No Olá **E-Mail** caixa de texto, endereço de correio eletrónico de Olá de tipo de uma conta do Azure AD que pretende tooprovision.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="4e4fb-231">c.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-231">c.</span></span> <span data-ttu-id="4e4fb-232">No Olá **funcionam ao** caixa de texto, o nome do tipo Olá empresariais.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="4e4fb-233">d.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-233">d.</span></span> <span data-ttu-id="4e4fb-234">Clique em **Guardar & convidar** botão.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="4e4fb-235">o marcador de posição do Olá AAD conta recebe uma mensagem de e-mail e segue um tooconfirm ligação respetiva conta para ficar ativa.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="4e4fb-236">Pode utilizar quaisquer outras Deputy utilizador conta criação ferramentas ou APIs fornecidas pelo Deputy tooprovision AAD contas de utilizador.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4e4fb-237">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e4fb-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4e4fb-238">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooDeputy.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="4e4fb-240">**tooassign Britta Simon tooDeputy, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="4e4fb-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="4e4fb-241">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="4e4fb-243">Na lista de aplicações de Olá, selecione **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-243">In hello applications list, select **Deputy**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="4e4fb-245">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="4e4fb-247">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-247">Click **Add** button.</span></span> <span data-ttu-id="4e4fb-248">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="4e4fb-250">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4e4fb-251">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4e4fb-252">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4e4fb-253">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="4e4fb-253">Testing single sign-on</span></span>

<span data-ttu-id="4e4fb-254">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4e4fb-255">Ao clicar Olá Deputy na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour Deputy aplicação.</span><span class="sxs-lookup"><span data-stu-id="4e4fb-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4e4fb-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4e4fb-256">Additional resources</span></span>

* [<span data-ttu-id="4e4fb-257">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e4fb-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4e4fb-258">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4e4fb-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

