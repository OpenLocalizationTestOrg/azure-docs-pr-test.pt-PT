---
title: "Tutorial: Integração do Azure Active Directory com Datahug | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="a7dca-103">Tutorial: Integração do Azure Active Directory com Datahug</span><span class="sxs-lookup"><span data-stu-id="a7dca-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="a7dca-104">Neste tutorial, saiba como toointegrate Datahug com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7dca-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7dca-105">Integrar Datahug com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="a7dca-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a7dca-106">Pode controlar no Azure AD que tenha acesso tooDatahug</span><span class="sxs-lookup"><span data-stu-id="a7dca-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="a7dca-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooDatahug (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7dca-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7dca-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a7dca-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a7dca-109">Se pretender que tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, consulte o artigo.</span><span class="sxs-lookup"><span data-stu-id="a7dca-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="a7dca-110">[O que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7dca-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7dca-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a7dca-111">Prerequisites</span></span>

<span data-ttu-id="a7dca-112">integração do Azure AD com Datahug tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a7dca-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="a7dca-113">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7dca-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a7dca-114">Um Datahug início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="a7dca-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7dca-115">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a7dca-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7dca-116">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a7dca-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7dca-117">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a7dca-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7dca-118">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7dca-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7dca-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a7dca-119">Scenario description</span></span>
<span data-ttu-id="a7dca-120">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a7dca-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7dca-121">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="a7dca-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7dca-122">Adicionar Datahug da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a7dca-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="a7dca-123">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a7dca-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="a7dca-124">Adicionar Datahug da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="a7dca-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="a7dca-125">tooconfigure Olá integração de Datahug com o Azure AD, é necessário tooadd Datahug Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="a7dca-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a7dca-126">**tooadd Datahug da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dca-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dca-127">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a7dca-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7dca-129">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a7dca-130">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-130">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="a7dca-132">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dca-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="a7dca-134">Na caixa de pesquisa de Olá, escreva **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-134">In hello search box, type **Datahug**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="a7dca-136">No painel de resultados de Olá, selecione **Datahug**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="a7dca-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7dca-138">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="a7dca-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7dca-139">Nesta secção, configure e teste do Azure AD-início de sessão único com Datahug com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a7dca-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a7dca-140">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Datahug é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7dca-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="a7dca-141">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Datahug tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a7dca-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="a7dca-142">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Datahug.</span><span class="sxs-lookup"><span data-stu-id="a7dca-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="a7dca-143">tooconfigure e teste do Azure AD-início de sessão único com Datahug, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a7dca-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a7dca-144">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="a7dca-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a7dca-145">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7dca-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7dca-146">**[Criar um utilizador de teste Datahug](#creating-a-datahug-test-user)**  -toohave um homólogo de Britta Simon no Datahug é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="a7dca-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7dca-147">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a7dca-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7dca-148">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="a7dca-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7dca-149">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a7dca-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7dca-150">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Datahug.</span><span class="sxs-lookup"><span data-stu-id="a7dca-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="a7dca-151">**tooconfigure do Azure AD-início de sessão único com Datahug, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dca-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dca-152">No Olá portal do Azure, no Olá **Datahug** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="a7dca-154">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="a7dca-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="a7dca-156">No Olá **Datahug domínio e os URLs** secção, se desejar aplicação Olá tooconfigure **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="a7dca-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="a7dca-158">a.</span><span class="sxs-lookup"><span data-stu-id="a7dca-158">a.</span></span> <span data-ttu-id="a7dca-159">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="a7dca-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="a7dca-160">b.</span><span class="sxs-lookup"><span data-stu-id="a7dca-160">b.</span></span> <span data-ttu-id="a7dca-161">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="a7dca-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="a7dca-162">Verifique **Mostrar avançadas definições de URL**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="a7dca-163">Se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="a7dca-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="a7dca-165">No Olá **URL de início de sessão** caixa de texto, escreva um URL como:`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="a7dca-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="a7dca-166">Estes valores não estiverem Olá real.</span><span class="sxs-lookup"><span data-stu-id="a7dca-166">These values are not hello real.</span></span> <span data-ttu-id="a7dca-167">Atualize estes valores com o URL de identificador e resposta real no Olá.</span><span class="sxs-lookup"><span data-stu-id="a7dca-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="a7dca-168">Aqui sugerimos toouse Olá exclusivo valor da cadeia no Olá identificador e o URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="a7dca-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="a7dca-169">Contacte [equipa de suporte de cliente Datahug](http://datahug.com/about/contact-us/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="a7dca-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="a7dca-170">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a7dca-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="a7dca-172">Verifique **"Mostrar avançadas definições de assinatura de certificado"** e efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a7dca-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="a7dca-174">a.</span><span class="sxs-lookup"><span data-stu-id="a7dca-174">a.</span></span> <span data-ttu-id="a7dca-175">No **assinatura opção**, selecione **asserção SAML de início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="a7dca-176">b.</span><span class="sxs-lookup"><span data-stu-id="a7dca-176">b.</span></span> <span data-ttu-id="a7dca-177">No **algoritmo de assinatura**, selecione **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="a7dca-178">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="a7dca-178">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="a7dca-180">No Olá **Datahug configuração** secção, clique em **configurar Datahug** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="a7dca-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a7dca-181">Olá cópia **ID de entidade de SAML** e **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="a7dca-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="a7dca-183">tooconfigure-início de sessão único em **Datahug** lado, terá de Olá toosend transferido **XML de metadados**, **ID de entidade de SAML** e **SAML único início de sessão no serviço URL** demasiado[Datahug suporte](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="a7dca-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="a7dca-184">Se definir esta aplicação Olá toohave corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="a7dca-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a7dca-185">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="a7dca-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a7dca-186">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="a7dca-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a7dca-187">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a7dca-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7dca-188">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7dca-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7dca-189">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7dca-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="a7dca-191">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dca-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dca-192">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="a7dca-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7dca-194">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7dca-196">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="a7dca-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7dca-198">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a7dca-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7dca-200">a.</span><span class="sxs-lookup"><span data-stu-id="a7dca-200">a.</span></span> <span data-ttu-id="a7dca-201">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7dca-202">b.</span><span class="sxs-lookup"><span data-stu-id="a7dca-202">b.</span></span> <span data-ttu-id="a7dca-203">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7dca-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7dca-204">c.</span><span class="sxs-lookup"><span data-stu-id="a7dca-204">c.</span></span> <span data-ttu-id="a7dca-205">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a7dca-206">d.</span><span class="sxs-lookup"><span data-stu-id="a7dca-206">d.</span></span> <span data-ttu-id="a7dca-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="a7dca-208">Criar um utilizador de teste Datahug</span><span class="sxs-lookup"><span data-stu-id="a7dca-208">Creating a Datahug test user</span></span>

<span data-ttu-id="a7dca-209">tooenable do Azure AD os utilizadores toolog no tooDatahug, estes têm de ser aprovisionados para Datahug.</span><span class="sxs-lookup"><span data-stu-id="a7dca-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="a7dca-210">Quando Datahug, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="a7dca-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="a7dca-211">**tooprovision uma conta de utilizador, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dca-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dca-212">Inicie sessão no tooyour Datahug site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="a7dca-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="a7dca-213">Coloque o cursor sobre Olá **roda dentada** no canto superior direito Olá e clique em **definições**</span><span class="sxs-lookup"><span data-stu-id="a7dca-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Adicionar empregado](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="a7dca-215">Escolha **pessoas** e clique em Olá **adicionar utilizadores** separador</span><span class="sxs-lookup"><span data-stu-id="a7dca-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Adicionar empregado](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="a7dca-217">Tipo de correio eletrónico de Olá de pessoa Olá gostaria toocreate uma conta para e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Adicionar empregado](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="a7dca-219">Pode enviar o registo correio toouser selecionando **enviar correio eletrónico de boas-vindas** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="a7dca-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="a7dca-220">Se estiver a criar uma conta do Salesforce não enviar e-mail de boas-vindas Olá.</span><span class="sxs-lookup"><span data-stu-id="a7dca-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a7dca-221">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7dca-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a7dca-222">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooDatahug.</span><span class="sxs-lookup"><span data-stu-id="a7dca-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="a7dca-224">**tooassign Britta Simon tooDatahug, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="a7dca-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="a7dca-225">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="a7dca-227">Na lista de aplicações de Olá, selecione **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-227">In hello applications list, select **Datahug**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="a7dca-229">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a7dca-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="a7dca-231">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="a7dca-231">Click **Add** button.</span></span> <span data-ttu-id="a7dca-232">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dca-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="a7dca-234">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="a7dca-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a7dca-235">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dca-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7dca-236">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a7dca-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7dca-237">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a7dca-237">Testing single sign-on</span></span>

<span data-ttu-id="a7dca-238">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a7dca-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="a7dca-239">Ao clicar em mosaico de Datahug Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Datahug aplicação.</span><span class="sxs-lookup"><span data-stu-id="a7dca-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="a7dca-240">Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="a7dca-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a7dca-241">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a7dca-241">Additional resources</span></span>

* [<span data-ttu-id="a7dca-242">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7dca-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7dca-243">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7dca-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

