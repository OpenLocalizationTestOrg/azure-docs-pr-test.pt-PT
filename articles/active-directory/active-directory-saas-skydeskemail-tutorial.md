---
title: "Tutorial: Integração do Azure Active Directory com SkyDesk E-Mail | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e SkyDesk E-Mail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="450ba-103">Tutorial: Integração do Azure Active Directory com SkyDesk E-Mail</span><span class="sxs-lookup"><span data-stu-id="450ba-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="450ba-104">Neste tutorial, saiba como toointegrate SkyDesk E-Mail com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="450ba-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="450ba-105">Integrar SkyDesk E-Mail com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="450ba-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="450ba-106">Pode controlar no Azure AD que tenha acesso tooSkyDesk E-Mail</span><span class="sxs-lookup"><span data-stu-id="450ba-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="450ba-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooSkyDesk E-Mail (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="450ba-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="450ba-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="450ba-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="450ba-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="450ba-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="450ba-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="450ba-110">Prerequisites</span></span>

<span data-ttu-id="450ba-111">integração do Azure AD com o E-Mail SkyDesk tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="450ba-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="450ba-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="450ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="450ba-113">Um E-Mail SkyDesk-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="450ba-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="450ba-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="450ba-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="450ba-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="450ba-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="450ba-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="450ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="450ba-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="450ba-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="450ba-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="450ba-118">Scenario description</span></span>
<span data-ttu-id="450ba-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="450ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="450ba-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="450ba-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="450ba-121">Adicionar SkyDesk E-Mail a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="450ba-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="450ba-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="450ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="450ba-123">Adicionar SkyDesk E-Mail a partir da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="450ba-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="450ba-124">tooconfigure Olá integração de SkyDesk E-Mail com o Azure AD, é necessário tooadd SkyDesk E-Mail Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="450ba-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="450ba-125">**tooadd SkyDesk E-Mail na Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="450ba-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="450ba-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="450ba-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="450ba-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="450ba-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="450ba-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="450ba-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="450ba-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="450ba-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="450ba-133">Na caixa de pesquisa de Olá, escreva **SkyDesk E-Mail**.</span><span class="sxs-lookup"><span data-stu-id="450ba-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="450ba-135">No painel de resultados de Olá, selecione **SkyDesk E-Mail**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="450ba-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="450ba-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="450ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="450ba-138">Nesta secção, configura e teste do Azure AD-início de sessão único com SkyDesk E-Mail com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="450ba-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="450ba-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá no E-Mail de SkyDesk é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="450ba-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="450ba-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o Olá utilizador relacionados na mensagem de correio eletrónico SkyDesk tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="450ba-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="450ba-141">No E-Mail de SkyDesk, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="450ba-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="450ba-142">tooconfigure e teste do Azure AD-início de sessão único com SkyDesk E-Mail, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="450ba-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="450ba-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="450ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="450ba-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="450ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="450ba-145">**[Criar um utilizador de teste de E-Mail SkyDesk](#creating-a-skydesk-email-test-user)**  -toohave um homólogo de Britta Simon SkyDesk por correio eletrónico que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="450ba-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="450ba-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="450ba-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="450ba-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="450ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="450ba-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="450ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="450ba-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de E-Mail SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="450ba-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="450ba-150">**tooconfigure do Azure AD-início de sessão único com SkyDesk E-Mail, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="450ba-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="450ba-151">No Olá portal do Azure, no Olá **SkyDesk E-Mail** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="450ba-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="450ba-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="450ba-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="450ba-155">No Olá **URLs e de domínio de correio eletrónico SkyDesk** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="450ba-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="450ba-157">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="450ba-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="450ba-158">o valor de Olá não é real.</span><span class="sxs-lookup"><span data-stu-id="450ba-158">hello value is not real.</span></span> <span data-ttu-id="450ba-159">Atualização Olá valor com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="450ba-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="450ba-160">Contacte [equipa de suporte de cliente de E-Mail SkyDesk](https://www.skydesk.sg/support/) valor de Olá tooget.</span><span class="sxs-lookup"><span data-stu-id="450ba-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="450ba-161">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="450ba-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="450ba-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="450ba-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="450ba-165">No Olá **configuração do E-Mail SkyDesk** secção, clique em **configurar E-Mail de SkyDesk** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="450ba-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="450ba-166">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="450ba-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="450ba-168">tooenable SSO no **SkyDesk E-Mail**, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="450ba-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="450ba-169">a.</span><span class="sxs-lookup"><span data-stu-id="450ba-169">a.</span></span> <span data-ttu-id="450ba-170">Início de sessão tooyour conta de E-Mail de SkyDesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="450ba-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="450ba-171">b.</span><span class="sxs-lookup"><span data-stu-id="450ba-171">b.</span></span> <span data-ttu-id="450ba-172">No menu de Olá na parte superior do Olá, clique em **configuração**e selecione **Org**.</span><span class="sxs-lookup"><span data-stu-id="450ba-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="450ba-174">c.</span><span class="sxs-lookup"><span data-stu-id="450ba-174">c.</span></span> <span data-ttu-id="450ba-175">Clique em **domínios** partir do painel esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="450ba-175">Click on **Domains** from hello left panel.</span></span>
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="450ba-177">d.</span><span class="sxs-lookup"><span data-stu-id="450ba-177">d.</span></span> <span data-ttu-id="450ba-178">Clique em **Adicionar domínio**.</span><span class="sxs-lookup"><span data-stu-id="450ba-178">Click on **Add Domain**.</span></span>
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="450ba-180">e.</span><span class="sxs-lookup"><span data-stu-id="450ba-180">e.</span></span> <span data-ttu-id="450ba-181">Introduza o nome de domínio e, em seguida, certifique-se Olá domínio.</span><span class="sxs-lookup"><span data-stu-id="450ba-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="450ba-183">f.</span><span class="sxs-lookup"><span data-stu-id="450ba-183">f.</span></span> <span data-ttu-id="450ba-184">Clique em **autenticação SAML** partir do painel esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="450ba-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="450ba-186">No Olá **autenticação SAML** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="450ba-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="450ba-188">autenticação com base no toouse SAML, deve ter **domínio verificado** ou **portal URL** programa de configuração.</span><span class="sxs-lookup"><span data-stu-id="450ba-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="450ba-189">Pode definir portal Olá URL com nome exclusivo Olá.</span><span class="sxs-lookup"><span data-stu-id="450ba-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="450ba-191">a.</span><span class="sxs-lookup"><span data-stu-id="450ba-191">a.</span></span> <span data-ttu-id="450ba-192">No Olá **URL de início de sessão** caixa de texto, colar Olá valor **único início de sessão no URL do serviço SAML**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="450ba-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="450ba-193">b.</span><span class="sxs-lookup"><span data-stu-id="450ba-193">b.</span></span> <span data-ttu-id="450ba-194">No Olá **terminar** caixa de texto do URL, colar Olá valor **Sign-Out URL**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="450ba-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="450ba-195">c.</span><span class="sxs-lookup"><span data-stu-id="450ba-195">c.</span></span> <span data-ttu-id="450ba-196">**Altere o URL de palavra-passe** é opcional, por isso, pode deixar em branco.</span><span class="sxs-lookup"><span data-stu-id="450ba-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="450ba-197">d.</span><span class="sxs-lookup"><span data-stu-id="450ba-197">d.</span></span> <span data-ttu-id="450ba-198">Clique em **obter chave a partir de um ficheiro** tooselect o certificado transferido do portal do Azure e, em seguida, clique em **abra** certificado de Olá tooupload.</span><span class="sxs-lookup"><span data-stu-id="450ba-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="450ba-199">e.</span><span class="sxs-lookup"><span data-stu-id="450ba-199">e.</span></span> <span data-ttu-id="450ba-200">Como **algoritmo**, selecione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="450ba-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="450ba-201">f.</span><span class="sxs-lookup"><span data-stu-id="450ba-201">f.</span></span> <span data-ttu-id="450ba-202">Clique em **Ok** alterações de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="450ba-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="450ba-203">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="450ba-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="450ba-204">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="450ba-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="450ba-205">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="450ba-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="450ba-206">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="450ba-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="450ba-207">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="450ba-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="450ba-209">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="450ba-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="450ba-210">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="450ba-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="450ba-212">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="450ba-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="450ba-214">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="450ba-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="450ba-216">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="450ba-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="450ba-218">a.</span><span class="sxs-lookup"><span data-stu-id="450ba-218">a.</span></span> <span data-ttu-id="450ba-219">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="450ba-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="450ba-220">b.</span><span class="sxs-lookup"><span data-stu-id="450ba-220">b.</span></span> <span data-ttu-id="450ba-221">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="450ba-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="450ba-222">c.</span><span class="sxs-lookup"><span data-stu-id="450ba-222">c.</span></span> <span data-ttu-id="450ba-223">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="450ba-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="450ba-224">d.</span><span class="sxs-lookup"><span data-stu-id="450ba-224">d.</span></span> <span data-ttu-id="450ba-225">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="450ba-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="450ba-226">Criar um utilizador de teste SkyDesk E-Mail</span><span class="sxs-lookup"><span data-stu-id="450ba-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="450ba-227">Nesta secção, vai criar um utilizador chamado Britta Simon no E-Mail de SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="450ba-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="450ba-228">Clique em **acesso de utilizador** Olá deixado painel no E-Mail de SkyDesk e, em seguida, introduza o nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="450ba-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="450ba-230">Se precisar de utilizadores em massa de toocreate, terá de toocontact Olá [equipa de suporte de cliente de E-Mail SkyDesk](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="450ba-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="450ba-231">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="450ba-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="450ba-232">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSkyDesk E-Mail.</span><span class="sxs-lookup"><span data-stu-id="450ba-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="450ba-234">**tooassign Britta Simon tooSkyDesk E-Mail, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="450ba-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="450ba-235">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="450ba-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="450ba-237">Na lista de aplicações de Olá, selecione **SkyDesk E-Mail**.</span><span class="sxs-lookup"><span data-stu-id="450ba-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="450ba-239">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="450ba-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="450ba-241">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="450ba-241">Click **Add** button.</span></span> <span data-ttu-id="450ba-242">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="450ba-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="450ba-244">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="450ba-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="450ba-245">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="450ba-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="450ba-246">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="450ba-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="450ba-247">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="450ba-247">Testing single sign-on</span></span>

<span data-ttu-id="450ba-248">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="450ba-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="450ba-249">Ao clicar Olá SkyDesk E-Mail na peça de mosaico Olá painel de acesso, deve obter automaticamente com sessão iniciada tooyour aplicação SkyDesk E-Mail.</span><span class="sxs-lookup"><span data-stu-id="450ba-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="450ba-250">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="450ba-250">Additional resources</span></span>

* [<span data-ttu-id="450ba-251">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="450ba-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="450ba-252">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="450ba-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

