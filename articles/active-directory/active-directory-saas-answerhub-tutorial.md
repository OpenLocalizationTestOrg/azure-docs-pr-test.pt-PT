---
title: "Tutorial: Integração do Azure Active Directory com AnswerHub | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="96449-103">Tutorial: Integração do Azure Active Directory com AnswerHub</span><span class="sxs-lookup"><span data-stu-id="96449-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="96449-104">Neste tutorial, saiba como toointegrate AnswerHub com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96449-104">In this tutorial, you learn how toointegrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96449-105">Integrar AnswerHub com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="96449-105">Integrating AnswerHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96449-106">Pode controlar no Azure AD que tenha acesso tooAnswerHub</span><span class="sxs-lookup"><span data-stu-id="96449-106">You can control in Azure AD who has access tooAnswerHub</span></span>
- <span data-ttu-id="96449-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooAnswerHub (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="96449-107">You can enable your users tooautomatically get signed-on tooAnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96449-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="96449-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="96449-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96449-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96449-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="96449-110">Prerequisites</span></span>

<span data-ttu-id="96449-111">integração do Azure AD com AnswerHub tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="96449-111">tooconfigure Azure AD integration with AnswerHub, you need hello following items:</span></span>

- <span data-ttu-id="96449-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="96449-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96449-113">Um AnswerHub-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="96449-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96449-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="96449-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96449-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="96449-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96449-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="96449-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96449-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96449-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96449-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="96449-118">Scenario description</span></span>
<span data-ttu-id="96449-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="96449-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96449-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="96449-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96449-121">Adicionar AnswerHub da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="96449-121">Adding AnswerHub from hello gallery</span></span>
2. <span data-ttu-id="96449-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="96449-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-hello-gallery"></a><span data-ttu-id="96449-123">Adicionar AnswerHub da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="96449-123">Adding AnswerHub from hello gallery</span></span>
<span data-ttu-id="96449-124">tooconfigure Olá integração de AnswerHub com o Azure AD, é necessário tooadd AnswerHub Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="96449-124">tooconfigure hello integration of AnswerHub into Azure AD, you need tooadd AnswerHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96449-125">**tooadd AnswerHub da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="96449-125">**tooadd AnswerHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96449-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="96449-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="96449-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="96449-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96449-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="96449-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="96449-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="96449-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="96449-133">Na caixa de pesquisa de Olá, escreva **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="96449-133">In hello search box, type **AnswerHub**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="96449-135">No painel de resultados de Olá, selecione **AnswerHub**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="96449-135">In hello results panel, select **AnswerHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96449-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="96449-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96449-138">Nesta secção, configure e teste do Azure AD-início de sessão único com AnswerHub com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="96449-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96449-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá AnswerHub é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96449-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AnswerHub is tooa user in Azure AD.</span></span> <span data-ttu-id="96449-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá AnswerHub tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="96449-140">In other words, a link relationship between an Azure AD user and hello related user in AnswerHub needs toobe established.</span></span>

<span data-ttu-id="96449-141">No AnswerHub, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="96449-141">In AnswerHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="96449-142">tooconfigure e teste do Azure AD-início de sessão único com AnswerHub, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="96449-142">tooconfigure and test Azure AD single sign-on with AnswerHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96449-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="96449-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96449-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96449-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96449-145">**[Criar um utilizador de teste AnswerHub](#creating-an-answerhub-test-user)**  -toohave um homólogo de Britta Simon no AnswerHub é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="96449-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - toohave a counterpart of Britta Simon in AnswerHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="96449-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="96449-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96449-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="96449-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96449-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="96449-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96449-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="96449-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="96449-150">**tooconfigure do Azure AD-início de sessão único com AnswerHub, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="96449-150">**tooconfigure Azure AD single sign-on with AnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="96449-151">No Olá portal do Azure, no Olá **AnswerHub** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="96449-151">In hello Azure portal, on hello **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="96449-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="96449-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="96449-155">No Olá **AnswerHub domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="96449-155">On hello **AnswerHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="96449-157">a.</span><span class="sxs-lookup"><span data-stu-id="96449-157">a.</span></span> <span data-ttu-id="96449-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="96449-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="96449-159">b.</span><span class="sxs-lookup"><span data-stu-id="96449-159">b.</span></span> <span data-ttu-id="96449-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="96449-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96449-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="96449-161">These values are not real.</span></span> <span data-ttu-id="96449-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="96449-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="96449-163">Contacte [equipa de suporte de cliente AnswerHub](mailto:success@answerhub.com) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="96449-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="96449-164">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="96449-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="96449-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="96449-166">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96449-168">No Olá **AnswerHub configuração** secção, clique em **configurar AnswerHub** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="96449-168">On hello **AnswerHub Configuration** section, click **Configure AnswerHub** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="96449-169">Olá cópia **Sign-Out URL e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="96449-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="96449-171">Numa janela do browser web diferente, inicie sessão no site da sua empresa AnswerHub como administrador.</span><span class="sxs-lookup"><span data-stu-id="96449-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="96449-172">Se precisar de ajuda para configurar AnswerHub, contacte [equipa de suporte do AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="96449-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="96449-173">Aceda demasiado**administração**.</span><span class="sxs-lookup"><span data-stu-id="96449-173">Go too**Administration**.</span></span>

9. <span data-ttu-id="96449-174">Clique em Olá **utilizador e grupo** separador.</span><span class="sxs-lookup"><span data-stu-id="96449-174">Click hello **User and Group** tab.</span></span>

10. <span data-ttu-id="96449-175">No painel de navegação de Olá no Olá left lado, nos Olá **definições de redes sociais** secção, clique em **configuração SAML**.</span><span class="sxs-lookup"><span data-stu-id="96449-175">In hello navigation pane on hello left side, in hello **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="96449-176">Clique em **IDP configuração** separador.</span><span class="sxs-lookup"><span data-stu-id="96449-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="96449-177">No Olá **IDP configuração** separador, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="96449-177">On hello **IDP Config** tab, perform hello following steps:</span></span>

     <span data-ttu-id="96449-178">![A configuração SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="96449-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="96449-179">a.</span><span class="sxs-lookup"><span data-stu-id="96449-179">a.</span></span> <span data-ttu-id="96449-180">No **URL de início de sessão do IDP** caixa de texto, colar **único início de sessão no URL do serviço SAML** que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="96449-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="96449-181">b.</span><span class="sxs-lookup"><span data-stu-id="96449-181">b.</span></span> <span data-ttu-id="96449-182">No **URL de fim de sessão do IDP** caixa de texto, colar **Sign-Out URL** valor que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="96449-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="96449-183">c.</span><span class="sxs-lookup"><span data-stu-id="96449-183">c.</span></span> <span data-ttu-id="96449-184">No **formato do identificador de nome de IDP** caixa de texto, introduza o utilizador Olá identificador valor mesmo como seleccionado no portal do Azure no **atributos de utilizador** secção.</span><span class="sxs-lookup"><span data-stu-id="96449-184">In **IDP Name Identifier Format** textbox, enter hello user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="96449-185">d.</span><span class="sxs-lookup"><span data-stu-id="96449-185">d.</span></span> <span data-ttu-id="96449-186">Clique em **chaves e certificados**.</span><span class="sxs-lookup"><span data-stu-id="96449-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="96449-187">No separador de chaves e certificados de Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="96449-187">On hello Keys and Certificates tab, perform hello following steps:</span></span>
    
     <span data-ttu-id="96449-188">![As chaves e certificados](./media/active-directory-saas-answerhub-tutorial/ic785173.png "chaves e certificados")</span><span class="sxs-lookup"><span data-stu-id="96449-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="96449-189">a.</span><span class="sxs-lookup"><span data-stu-id="96449-189">a.</span></span> <span data-ttu-id="96449-190">Abra o seu certificado codificado de base-64 que transferiu a partir do portal do Azure no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência, e, em seguida, cole-toohello **chave pública do IDP (x 509 formato)** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="96449-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="96449-191">b.</span><span class="sxs-lookup"><span data-stu-id="96449-191">b.</span></span> <span data-ttu-id="96449-192">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="96449-192">Click **Save**.</span></span>

14. <span data-ttu-id="96449-193">No Olá **IDP configuração** separador, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="96449-193">On hello **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="96449-194">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="96449-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96449-195">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="96449-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96449-196">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96449-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96449-197">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="96449-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="96449-198">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="96449-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="96449-200">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="96449-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96449-201">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="96449-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96449-203">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="96449-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96449-205">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="96449-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96449-207">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="96449-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96449-209">a.</span><span class="sxs-lookup"><span data-stu-id="96449-209">a.</span></span> <span data-ttu-id="96449-210">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96449-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96449-211">b.</span><span class="sxs-lookup"><span data-stu-id="96449-211">b.</span></span> <span data-ttu-id="96449-212">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96449-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96449-213">c.</span><span class="sxs-lookup"><span data-stu-id="96449-213">c.</span></span> <span data-ttu-id="96449-214">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="96449-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="96449-215">d.</span><span class="sxs-lookup"><span data-stu-id="96449-215">d.</span></span> <span data-ttu-id="96449-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="96449-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="96449-217">Criar um utilizador de teste AnswerHub</span><span class="sxs-lookup"><span data-stu-id="96449-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="96449-218">tooenable do Azure AD os utilizadores toolog no tooAnswerHub, estes têm de ser aprovisionados para AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="96449-218">tooenable Azure AD users toolog in tooAnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="96449-219">No caso de Olá da AnswerHub, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="96449-219">In hello case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="96449-220">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="96449-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="96449-221">Inicie sessão no tooyour **AnswerHub** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="96449-221">Log in tooyour **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="96449-222">Aceda demasiado**administração**.</span><span class="sxs-lookup"><span data-stu-id="96449-222">Go too**Administration**.</span></span>

3. <span data-ttu-id="96449-223">Clique em Olá **utilizadores e grupos** separador.</span><span class="sxs-lookup"><span data-stu-id="96449-223">Click hello **Users & Groups** tab.</span></span>

4. <span data-ttu-id="96449-224">No painel de navegação de Olá no Olá left lado, nos Olá **gerir utilizadores** secção, clique em **criar ou importar utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="96449-224">In hello navigation pane on hello left side, in hello **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="96449-225">![Utilizadores e grupos](./media/active-directory-saas-answerhub-tutorial/ic785175.png "utilizadores e grupos")</span><span class="sxs-lookup"><span data-stu-id="96449-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="96449-226">Olá tipo **endereço de correio eletrónico**, **Username** e **palavra-passe** de um Azure válido conta do Active Directory que pretende tooprovision Olá relacionadas com caixas de texto e, em seguida, clique em  **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="96449-226">Type hello **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want tooprovision into hello related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="96449-227">Pode utilizar quaisquer outras AnswerHub utilizador conta criação ferramentas ou APIs fornecidas pelo AnswerHub tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="96449-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96449-228">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="96449-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="96449-229">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooAnswerHub.</span><span class="sxs-lookup"><span data-stu-id="96449-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnswerHub.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="96449-231">**tooassign Britta Simon tooAnswerHub, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="96449-231">**tooassign Britta Simon tooAnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="96449-232">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="96449-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="96449-234">Na lista de aplicações de Olá, selecione **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="96449-234">In hello applications list, select **AnswerHub**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="96449-236">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="96449-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="96449-238">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="96449-238">Click **Add** button.</span></span> <span data-ttu-id="96449-239">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="96449-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="96449-241">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="96449-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96449-242">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="96449-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96449-243">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="96449-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96449-244">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="96449-244">Testing single sign-on</span></span>

<span data-ttu-id="96449-245">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="96449-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96449-246">Ao clicar em mosaico de AnswerHub Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour AnswerHub aplicação.</span><span class="sxs-lookup"><span data-stu-id="96449-246">When you click hello AnswerHub tile in hello Access Panel, you should get automatically signed-on tooyour AnswerHub application.</span></span>
<span data-ttu-id="96449-247">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="96449-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96449-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="96449-248">Additional resources</span></span>

* [<span data-ttu-id="96449-249">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96449-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96449-250">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96449-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

