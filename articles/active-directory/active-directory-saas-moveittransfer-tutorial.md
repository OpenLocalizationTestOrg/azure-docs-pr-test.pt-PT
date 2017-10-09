---
title: "Tutorial: Integração do Azure Active Directory com MOVEit transferência - a integração do Azure AD | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e transferência MOVEit - a integração do Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="26b29-103">Tutorial: Integração do Azure Active Directory com MOVEit transferência - a integração do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b29-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="26b29-104">Neste tutorial, saiba como toointegrate MOVEit transferência - integração do Azure AD com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26b29-104">In this tutorial, you learn how toointegrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26b29-105">Integrar MOVEit transferência - integração do Azure AD com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="26b29-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="26b29-106">Pode controlar no Azure AD que tenha acesso tooMOVEit transferência - a integração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b29-106">You can control in Azure AD who has access tooMOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="26b29-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooMOVEit transferência - integração do Azure AD (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b29-107">You can enable your users tooautomatically get signed-on tooMOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="26b29-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b29-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="26b29-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="26b29-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26b29-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="26b29-110">Prerequisites</span></span>

<span data-ttu-id="26b29-111">tooconfigure integração do Azure AD com MOVEit transferência - integração do AD do Azure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="26b29-111">tooconfigure Azure AD integration with MOVEit Transfer - Azure AD integration, you need hello following items:</span></span>

- <span data-ttu-id="26b29-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26b29-113">Transferência de MOVEit - do Azure AD integração início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="26b29-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26b29-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="26b29-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26b29-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="26b29-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26b29-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="26b29-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26b29-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26b29-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26b29-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="26b29-118">Scenario description</span></span>
<span data-ttu-id="26b29-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="26b29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26b29-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="26b29-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26b29-121">Transferência de MOVEit - integração do Azure AD da Galeria de Olá a adicionar</span><span class="sxs-lookup"><span data-stu-id="26b29-121">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
2. <span data-ttu-id="26b29-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="26b29-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a><span data-ttu-id="26b29-123">Transferência de MOVEit - integração do Azure AD da Galeria de Olá a adicionar</span><span class="sxs-lookup"><span data-stu-id="26b29-123">Adding MOVEit Transfer - Azure AD integration from hello gallery</span></span>
<span data-ttu-id="26b29-124">integração de Olá tooconfigure de transferência de MOVEit - integração do Azure AD com o Azure AD, é necessário tooadd MOVEit transferência - integração do Azure AD Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="26b29-124">tooconfigure hello integration of MOVEit Transfer - Azure AD integration into Azure AD, you need tooadd MOVEit Transfer - Azure AD integration from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="26b29-125">**tooadd MOVEit transferência - integração do Azure AD da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="26b29-125">**tooadd MOVEit Transfer - Azure AD integration from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="26b29-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="26b29-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="26b29-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="26b29-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="26b29-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="26b29-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="26b29-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26b29-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="26b29-133">Na caixa de pesquisa de Olá, escreva **MOVEit transferência - a integração do Azure AD**, selecione **MOVEit transferência - a integração do Azure AD** partir do painel de resultados, em seguida, clique em **adicionar** Olá tooadd de botão aplicação.</span><span class="sxs-lookup"><span data-stu-id="26b29-133">In hello search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Transferência de MOVEit - integração do Azure AD na lista de resultados de Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="26b29-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="26b29-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="26b29-136">Nesta secção, configure e teste do Azure AD-início de sessão único com MOVEit transferência - integração do Azure AD com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26b29-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26b29-137">Para único início de sessão toowork, do Azure AD tem do utilizador de homólogo Olá na transferência MOVEit tooknow - a integração do Azure AD é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b29-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MOVEit Transfer - Azure AD integration is tooa user in Azure AD.</span></span> <span data-ttu-id="26b29-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na transferência MOVEit - a integração do Azure AD tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="26b29-138">In other words, a link relationship between an Azure AD user and hello related user in MOVEit Transfer - Azure AD integration needs toobe established.</span></span>

<span data-ttu-id="26b29-139">Na transferência MOVEit - integração do AD do Azure, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="26b29-139">In MOVEit Transfer - Azure AD integration, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="26b29-140">tooconfigure e teste do Azure AD-início de sessão único com MOVEit transferência - integração do AD do Azure, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="26b29-140">tooconfigure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="26b29-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="26b29-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="26b29-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26b29-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="26b29-143">**[Criar uma transferência MOVEit - utilizador de teste de integração do Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave um homólogo de Britta Simon na transferência MOVEit - integração com o AD do Azure que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="26b29-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - toohave a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="26b29-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="26b29-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="26b29-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="26b29-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="26b29-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="26b29-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="26b29-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua transferência MOVEit - a aplicação de integração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b29-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="26b29-148">**tooconfigure do Azure AD-início de sessão único com MOVEit transferência - integração do Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="26b29-148">**tooconfigure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="26b29-149">No Olá portal do Azure, no Olá **MOVEit transferência - a integração do Azure AD** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="26b29-149">In hello Azure portal, on hello **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="26b29-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="26b29-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="26b29-153">No Olá **MOVEit transferência - URLs e integração com o Azure AD domínio** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="26b29-153">On hello **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="26b29-155">a.</span><span class="sxs-lookup"><span data-stu-id="26b29-155">a.</span></span> <span data-ttu-id="26b29-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="26b29-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="26b29-157">b.</span><span class="sxs-lookup"><span data-stu-id="26b29-157">b.</span></span> <span data-ttu-id="26b29-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="26b29-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="26b29-159">c.</span><span class="sxs-lookup"><span data-stu-id="26b29-159">c.</span></span> <span data-ttu-id="26b29-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="26b29-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="26b29-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="26b29-161">These values are not real.</span></span> <span data-ttu-id="26b29-162">Atualizar estes valores com Olá real identificador, o URL de resposta e o URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="26b29-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="26b29-163">Pode consultar estes valores mais tarde em **URL de metadados do fornecedor de serviço** secção ou contacte [MOVEit transferência - a equipa de suporte de cliente de integração do Azure AD](https://community.ipswitch.com/s/support) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="26b29-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) tooget these values.</span></span>

4. <span data-ttu-id="26b29-164">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="26b29-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="26b29-166">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="26b29-166">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="26b29-168">Início de sessão tooyour MOVEit transferência inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="26b29-168">Sign on tooyour MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="26b29-169">No painel de navegação esquerdo Olá, clique em **definições**.</span><span class="sxs-lookup"><span data-stu-id="26b29-169">On hello left navigation pane, click **Settings**.</span></span>

    ![Lado de secção na aplicação de definições](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="26b29-171">Clique em **Signon único** ligação, que está sob **políticas de segurança -> utilizador Auth**.</span><span class="sxs-lookup"><span data-stu-id="26b29-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![Lado de políticas em aplicações de segurança](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="26b29-173">Clique em documento de metadados de Olá ligação toodownload Olá URL de metadados.</span><span class="sxs-lookup"><span data-stu-id="26b29-173">Click hello Metadata URL link toodownload hello metadata document.</span></span>

    ![URL de metadados do fornecedor de serviço](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="26b29-175">Certifique-se **entityID** corresponde **identificador** no Olá **MOVEit transferência - URLs e integração com o Azure AD domínio** secção.</span><span class="sxs-lookup"><span data-stu-id="26b29-175">Verify **entityID** matches **Identifier** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="26b29-176">Certifique-se **AssertionConsumerService** corresponde ao URL de localização **URL de resposta** no Olá **MOVEit transferência - URLs e integração com o Azure AD domínio** secção.</span><span class="sxs-lookup"><span data-stu-id="26b29-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in hello **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![Configurar lado único início de sessão na aplicação](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="26b29-178">Clique em **Adicionar fornecedor de identidade** botão tooadd um novo fornecedor de identidade federada.</span><span class="sxs-lookup"><span data-stu-id="26b29-178">Click **Add Identity Provider** button tooadd a new Federated Identity Provider.</span></span>

    ![Adicione o fornecedor de identidade](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="26b29-180">Clique em **procurar...**  tooselect Olá o ficheiro de metadados do que transferiu a partir do portal do Azure, em seguida, clique em **Adicionar fornecedor de identidade** Olá tooupload transferido o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="26b29-180">Click **Browse...** tooselect hello metadata file which you downloaded from Azure portal, then click **Add Identity Provider** tooupload hello downloaded file.</span></span>

    ![Fornecedor de identidade](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="26b29-182">Selecione "**Sim**" como **ativado** no Olá **editar definições do fornecedor de identidade federada...**  página e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="26b29-182">Select "**Yes**" as **Enabled** in hello **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![Definições do fornecedor de identidade federada](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="26b29-184">No Olá **editar federado identidade do utilizador as definições do fornecedor** página, execute Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="26b29-184">In hello **Edit Federated Identity Provider User Settings** page, perform hello following actions:</span></span>
    
    ![Editar as definições do fornecedor de identidade federada](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="26b29-186">a.</span><span class="sxs-lookup"><span data-stu-id="26b29-186">a.</span></span> <span data-ttu-id="26b29-187">Selecione **SAML NameID** como **nome de início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="26b29-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="26b29-188">b.</span><span class="sxs-lookup"><span data-stu-id="26b29-188">b.</span></span> <span data-ttu-id="26b29-189">Selecione **outros** como **nome completo** e no Olá **nome de atributo** textbox colocar o valor de Olá: `http://schemas.microsoft.com/identity/claims/displayname`.</span><span class="sxs-lookup"><span data-stu-id="26b29-189">Select **Other** as **Full name** and in hello **Attribute name** textbox put hello value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="26b29-190">c.</span><span class="sxs-lookup"><span data-stu-id="26b29-190">c.</span></span> <span data-ttu-id="26b29-191">Selecione **outros** como **E-Mail** e no Olá **nome de atributo** textbox colocar o valor de Olá: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="26b29-191">Select **Other** as **Email** and in hello **Attribute name** textbox put hello value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="26b29-192">d.</span><span class="sxs-lookup"><span data-stu-id="26b29-192">d.</span></span> <span data-ttu-id="26b29-193">Selecione **Sim** como **Auto-criar conta no signon**.</span><span class="sxs-lookup"><span data-stu-id="26b29-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="26b29-194">e.</span><span class="sxs-lookup"><span data-stu-id="26b29-194">e.</span></span> <span data-ttu-id="26b29-195">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="26b29-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="26b29-196">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="26b29-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="26b29-197">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="26b29-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="26b29-198">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="26b29-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="26b29-199">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b29-199">Create an Azure AD test user</span></span>

<span data-ttu-id="26b29-200">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b29-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="26b29-202">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="26b29-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="26b29-203">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="26b29-203">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="26b29-205">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="26b29-205">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="26b29-207">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26b29-207">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="26b29-209">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="26b29-209">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="26b29-211">a.</span><span class="sxs-lookup"><span data-stu-id="26b29-211">a.</span></span> <span data-ttu-id="26b29-212">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26b29-212">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26b29-213">b.</span><span class="sxs-lookup"><span data-stu-id="26b29-213">b.</span></span> <span data-ttu-id="26b29-214">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26b29-214">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="26b29-215">c.</span><span class="sxs-lookup"><span data-stu-id="26b29-215">c.</span></span> <span data-ttu-id="26b29-216">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="26b29-216">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="26b29-217">d.</span><span class="sxs-lookup"><span data-stu-id="26b29-217">d.</span></span> <span data-ttu-id="26b29-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="26b29-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="26b29-219">Criar uma transferência MOVEit - utilizador de teste de integração do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b29-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="26b29-220">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon na transferência MOVEit - a integração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b29-220">hello objective of this section is toocreate a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="26b29-221">Transferência de MOVEit - integração do AD do Azure suporta just-in-time o aprovisionamento, que tiver ativado.</span><span class="sxs-lookup"><span data-stu-id="26b29-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="26b29-222">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="26b29-222">There is no action item for you in this section.</span></span> <span data-ttu-id="26b29-223">Um novo utilizador é criado durante uma tentativa tooaccess MOVEit transferência - se de que não existe ainda a integração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="26b29-223">A new user is created during an attempt tooaccess MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="26b29-224">Se precisar de um utilizador de toocreate manualmente, terá de toocontact Olá [MOVEit transferência - a equipa de suporte de cliente de integração do Azure AD](https://community.ipswitch.com/s/support).</span><span class="sxs-lookup"><span data-stu-id="26b29-224">If you need toocreate a user manually, you need toocontact hello [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="26b29-225">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="26b29-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="26b29-226">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooMOVEit transferência - a integração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b29-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMOVEit Transfer - Azure AD integration.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="26b29-228">**tooassign Britta Simon tooMOVEit transferência - integração do Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="26b29-228">**tooassign Britta Simon tooMOVEit Transfer - Azure AD integration, perform hello following steps:**</span></span>

1. <span data-ttu-id="26b29-229">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="26b29-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="26b29-231">Na lista de aplicações de Olá, selecione **MOVEit transferência - a integração do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="26b29-231">In hello applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![ligação de integração do Azure AD Hello MOVEit transferência - na lista de aplicações de Olá](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="26b29-233">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="26b29-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="26b29-235">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="26b29-235">Click **Add** button.</span></span> <span data-ttu-id="26b29-236">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26b29-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="26b29-238">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="26b29-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="26b29-239">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26b29-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="26b29-240">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26b29-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="26b29-241">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="26b29-241">Test single sign-on</span></span>

<span data-ttu-id="26b29-242">o objetivo desta secção Olá é tootest a configuração de SSO do Azure AD utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="26b29-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="26b29-243">Ao clicar em Olá MOVEit transferência - mosaico de integração do Azure AD no painel de acesso Olá, deve obter automaticamente com sessão iniciada tooyour MOVEit transferência - a aplicação de integração do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26b29-243">When you click hello MOVEit Transfer - Azure AD integration tile in hello Access Panel, you should get automatically signed-on tooyour MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="26b29-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="26b29-244">Additional resources</span></span>

* [<span data-ttu-id="26b29-245">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26b29-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="26b29-246">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26b29-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

