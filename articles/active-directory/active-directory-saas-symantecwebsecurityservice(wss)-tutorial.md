---
title: "Tutorial: Integração do Azure Active Directory com o serviço de segurança de Web do Symantec (WSS) | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e o serviço de segurança Web (WSS) da Symantec."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: f4575e6f5eb63cd0e1d63edd35e30be3cacc3382
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="42cf4-103">Tutorial: Integração do Azure Active Directory com o serviço de segurança de Web do Symantec (WSS)</span><span class="sxs-lookup"><span data-stu-id="42cf4-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="42cf4-104">Neste tutorial, saiba como toointegrate Symantec Web segurança serviço (WSS) com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42cf4-104">In this tutorial, you learn how toointegrate Symantec Web Security Service (WSS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42cf4-105">A integração de serviço de segurança Web (WSS) da Symantec com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="42cf4-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="42cf4-106">Pode controlar no Azure AD que tenha acesso tooSymantec serviço de segurança da Web (WSS)</span><span class="sxs-lookup"><span data-stu-id="42cf4-106">You can control in Azure AD who has access tooSymantec Web Security Service (WSS)</span></span>
- <span data-ttu-id="42cf4-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooSymantec serviço de segurança da Web (WSS) (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="42cf4-107">You can enable your users tooautomatically get signed-on tooSymantec Web Security Service (WSS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42cf4-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="42cf4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="42cf4-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42cf4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42cf4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42cf4-110">Prerequisites</span></span>

<span data-ttu-id="42cf4-111">tooconfigure integração do Azure AD com o serviço de segurança de Web do Symantec (WSS), terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="42cf4-111">tooconfigure Azure AD integration with Symantec Web Security Service (WSS), you need hello following items:</span></span>

- <span data-ttu-id="42cf4-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="42cf4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42cf4-113">Um serviço de segurança Web (WSS) da Symantec-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="42cf4-113">A Symantec Web Security Service (WSS) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42cf4-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="42cf4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42cf4-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="42cf4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42cf4-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="42cf4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42cf4-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42cf4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42cf4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="42cf4-118">Scenario description</span></span>
<span data-ttu-id="42cf4-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="42cf4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42cf4-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="42cf4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42cf4-121">Adicionar serviço de segurança Web (WSS) da Symantec da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="42cf4-121">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
2. <span data-ttu-id="42cf4-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="42cf4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a><span data-ttu-id="42cf4-123">Adicionar serviço de segurança Web (WSS) da Symantec da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="42cf4-123">Adding Symantec Web Security Service (WSS) from hello gallery</span></span>
<span data-ttu-id="42cf4-124">tooconfigure Olá integração de serviço de segurança de Web do Symantec (WSS) com o Azure AD, é necessário tooadd Symantec Web segurança serviço (WSS) Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="42cf4-124">tooconfigure hello integration of Symantec Web Security Service (WSS) into Azure AD, you need tooadd Symantec Web Security Service (WSS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="42cf4-125">**tooadd Symantec Web segurança serviço (WSS) na Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="42cf4-125">**tooadd Symantec Web Security Service (WSS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="42cf4-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="42cf4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42cf4-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="42cf4-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="42cf4-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42cf4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="42cf4-133">Na caixa de pesquisa de Olá, escreva **Symantec Web segurança serviço (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-133">In hello search box, type **Symantec Web Security Service (WSS)**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_search.png)

5. <span data-ttu-id="42cf4-135">No painel de resultados de Olá, selecione **Symantec Web segurança serviço (WSS)**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="42cf4-135">In hello results panel, select **Symantec Web Security Service (WSS)**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42cf4-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="42cf4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42cf4-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Symantec Web segurança serviço (WSS) com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="42cf4-138">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="42cf4-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que Olá homólogo no serviço de segurança de Web do Symantec (WSS) é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42cf4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Symantec Web Security Service (WSS) is tooa user in Azure AD.</span></span> <span data-ttu-id="42cf4-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e Olá relacionados com o utilizador no serviço de segurança de Web do Symantec (WSS) tem de toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="42cf4-140">In other words, a link relationship between an Azure AD user and hello related user in Symantec Web Security Service (WSS) needs toobe established.</span></span>

<span data-ttu-id="42cf4-141">Na Symantec Web segurança serviço (WSS), atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="42cf4-141">In Symantec Web Security Service (WSS), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="42cf4-142">tooconfigure e teste do Azure AD-início de sessão único com o serviço de segurança de Web do Symantec (WSS), terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="42cf4-142">tooconfigure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="42cf4-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="42cf4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="42cf4-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42cf4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42cf4-145">**[Criar um utilizador de teste do serviço de segurança Web (WSS) da Symantec](#creating-a-symantec-web-security-service-wss-test-user)**  -toohave um homólogo de Britta Simon na Symantec Web segurança serviço (WSS) que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="42cf4-145">**[Creating a Symantec Web Security Service (WSS) test user](#creating-a-symantec-web-security-service-wss-test-user)** - toohave a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="42cf4-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="42cf4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42cf4-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="42cf4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42cf4-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="42cf4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42cf4-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de serviço de segurança Web (WSS) da Symantec.</span><span class="sxs-lookup"><span data-stu-id="42cf4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="42cf4-150">**tooconfigure do Azure AD-início de sessão único com o Symantec Web segurança serviço (WSS), execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="42cf4-150">**tooconfigure Azure AD single sign-on with Symantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="42cf4-151">No Olá portal do Azure, no Olá **Symantec Web segurança serviço (WSS)** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-151">In hello Azure portal, on hello **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="42cf4-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="42cf4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="42cf4-155">No Olá **domínio de serviço (WSS) de segurança de Web da Symantec e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="42cf4-155">On hello **Symantec Web Security Service (WSS) Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="42cf4-157">a.</span><span class="sxs-lookup"><span data-stu-id="42cf4-157">a.</span></span> <span data-ttu-id="42cf4-158">No Olá **URL de início de sessão** caixa de texto, menção Olá url que pretende tooblock de acordo com a política de bloqueio de toohello de Olá Symantec Web segurança serviço (WSS).</span><span class="sxs-lookup"><span data-stu-id="42cf4-158">In hello **Sign-on URL** textbox, mention hello url, which you want tooblock according toohello blocking policy of hello Symantec Web Security Service (WSS).</span></span>  
    
    <span data-ttu-id="42cf4-159">b.</span><span class="sxs-lookup"><span data-stu-id="42cf4-159">b.</span></span> <span data-ttu-id="42cf4-160">No Olá **identificador** caixa de texto, tipo Olá URL:`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="42cf4-160">In hello **Identifier** textbox, type hello URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42cf4-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="42cf4-161">These values are not real.</span></span> <span data-ttu-id="42cf4-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="42cf4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="42cf4-163">Contacte [equipa de suporte de cliente do serviço de segurança Web (WSS) da Symantec](https://www.symantec.com/contact-us) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="42cf4-163">Contact [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="42cf4-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="42cf4-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="42cf4-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="42cf4-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42cf4-168">tooconfigure-início de sessão único em **Symantec Web segurança serviço (WSS)** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipasuportaroserviçodesegurançaWeb(WSS)daSymantec](https://www.symantec.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="42cf4-168">tooconfigure single sign-on on **Symantec Web Security Service (WSS)** side, you need toosend hello downloaded **Metadata XML** too[Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="42cf4-169">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="42cf4-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="42cf4-170">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="42cf4-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="42cf4-171">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42cf4-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42cf4-172">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="42cf4-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="42cf4-173">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="42cf4-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="42cf4-175">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="42cf4-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="42cf4-176">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="42cf4-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42cf4-178">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42cf4-180">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="42cf4-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42cf4-182">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="42cf4-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42cf4-184">a.</span><span class="sxs-lookup"><span data-stu-id="42cf4-184">a.</span></span> <span data-ttu-id="42cf4-185">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42cf4-186">b.</span><span class="sxs-lookup"><span data-stu-id="42cf4-186">b.</span></span> <span data-ttu-id="42cf4-187">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="42cf4-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="42cf4-188">c.</span><span class="sxs-lookup"><span data-stu-id="42cf4-188">c.</span></span> <span data-ttu-id="42cf4-189">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="42cf4-190">d.</span><span class="sxs-lookup"><span data-stu-id="42cf4-190">d.</span></span> <span data-ttu-id="42cf4-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-191">Click **Create**.</span></span>
 
### <a name="creating-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="42cf4-192">Criar um utilizador de teste do serviço de segurança Web (WSS) da Symantec</span><span class="sxs-lookup"><span data-stu-id="42cf4-192">Creating a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="42cf4-193">Nesta secção, vai criar um utilizador chamado Britta Simon no serviço de segurança de Web do Symantec (WSS).</span><span class="sxs-lookup"><span data-stu-id="42cf4-193">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="42cf4-194">Trabalhar com [equipa de suporte de serviço de segurança Web (WSS) da Symantec](https://www.symantec.com/contact-us) para adicionar utilizadores de Olá na plataforma de serviço de segurança Web (WSS) da Symantec Olá.</span><span class="sxs-lookup"><span data-stu-id="42cf4-194">Work with [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) to add hello users in hello Symantec Web Security Service (WSS) platform.</span></span> <span data-ttu-id="42cf4-195">Os utilizadores tem de ser criados e ativados antes de utilizar o início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="42cf4-195">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="42cf4-196">Também juntamente com Olá utilizador fornece detalhes sobre precisa de toosend Olá IPaddress público da máquina de Olá partir do qual está a tentar aplicação de Olá tooaccess.</span><span class="sxs-lookup"><span data-stu-id="42cf4-196">Also along with hello user details you need toosend hello public IPaddress of hello machine from which you are trying tooaccess hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="42cf4-197">. [Clique aqui](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget a máquina do pública IPaddress.</span><span class="sxs-lookup"><span data-stu-id="42cf4-197">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget your machine's public IPaddress.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="42cf4-198">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="42cf4-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="42cf4-199">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooSymantec serviço de segurança da Web (WSS).</span><span class="sxs-lookup"><span data-stu-id="42cf4-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSymantec Web Security Service (WSS).</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="42cf4-201">**tooassign Britta Simon tooSymantec serviço de segurança da Web (WSS), execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="42cf4-201">**tooassign Britta Simon tooSymantec Web Security Service (WSS), perform hello following steps:**</span></span>

1. <span data-ttu-id="42cf4-202">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="42cf4-204">Na lista de aplicações de Olá, selecione **Symantec Web segurança serviço (WSS)**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-204">In hello applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_symantecwebsecurityservicewss_app.png) 

3. <span data-ttu-id="42cf4-206">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="42cf4-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="42cf4-208">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="42cf4-208">Click **Add** button.</span></span> <span data-ttu-id="42cf4-209">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42cf4-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="42cf4-211">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="42cf4-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="42cf4-212">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42cf4-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42cf4-213">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="42cf4-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42cf4-214">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="42cf4-214">Testing single sign-on</span></span>

<span data-ttu-id="42cf4-215">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="42cf4-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="42cf4-216">Ao clicar Olá Symantec Web segurança serviço (WSS) na peça de mosaico Olá painel de acesso, obter toohello redirecionada bloquear a página para o qual foi configurado Olá bloquear a política.</span><span class="sxs-lookup"><span data-stu-id="42cf4-216">When you click hello Symantec Web Security Service (WSS) tile in hello Access Panel, you get redirected toohello blocking page for which hello blocking policy has been configured.</span></span>
<span data-ttu-id="42cf4-217">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="42cf4-217">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="42cf4-218">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="42cf4-218">Additional resources</span></span>

* [<span data-ttu-id="42cf4-219">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42cf4-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42cf4-220">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="42cf4-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantecwebsecurityservice(wss)-tutorial/tutorial_general_203.png

