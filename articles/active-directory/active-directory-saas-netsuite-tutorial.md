---
title: "Tutorial: Integração do Azure Active Directory com Netsuite | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="8e5ff-103">Tutorial: Integração do Azure Active Directory com Netsuite</span><span class="sxs-lookup"><span data-stu-id="8e5ff-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="8e5ff-104">Neste tutorial, saiba como toointegrate Netsuite com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e5ff-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e5ff-105">Integrar Netsuite com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8e5ff-106">Pode controlar no Azure AD que tenha acesso tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="8e5ff-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="8e5ff-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooNetsuite (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e5ff-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e5ff-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8e5ff-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8e5ff-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e5ff-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e5ff-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8e5ff-110">Prerequisites</span></span>

<span data-ttu-id="8e5ff-111">integração do Azure AD com Netsuite tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="8e5ff-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e5ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e5ff-113">Um Netsuite início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="8e5ff-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e5ff-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e5ff-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e5ff-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e5ff-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e5ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e5ff-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="8e5ff-118">Scenario description</span></span>
<span data-ttu-id="8e5ff-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e5ff-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e5ff-121">Adicionar Netsuite da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="8e5ff-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="8e5ff-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="8e5ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="8e5ff-123">Adicionar Netsuite da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="8e5ff-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="8e5ff-124">tooconfigure Olá integração de Netsuite com o Azure AD, é necessário tooadd Netsuite Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8e5ff-125">**tooadd Netsuite da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8e5ff-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e5ff-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e5ff-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8e5ff-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="8e5ff-131">Clique em **nova aplicação** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="8e5ff-133">Na caixa de pesquisa de Olá, escreva **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-133">In hello search box, type **Netsuite**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="8e5ff-135">No painel de resultados de Olá, selecione **Netsuite**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e5ff-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="8e5ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e5ff-138">Nesta secção, configure e teste do Azure AD-início de sessão único com Netsuite com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8e5ff-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8e5ff-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Netsuite é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="8e5ff-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Netsuite tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="8e5ff-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="8e5ff-142">tooconfigure e teste do Azure AD-início de sessão único com Netsuite, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8e5ff-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8e5ff-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e5ff-145">**[Criar um utilizador de teste Netsuite](#creating-a-netsuite-test-user)**  -toohave um homólogo de Britta Simon no Netsuite é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e5ff-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e5ff-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e5ff-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="8e5ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e5ff-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="8e5ff-150">**tooconfigure do Azure AD-início de sessão único com Netsuite, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8e5ff-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e5ff-151">No Olá portal do Azure, no Olá **Netsuite** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="8e5ff-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="8e5ff-155">No Olá **Netsuite domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="8e5ff-157">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="8e5ff-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e5ff-158">Este valor não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-158">This value is not real value.</span></span> <span data-ttu-id="8e5ff-159">Atualização Olá valor com Olá real de resposta de URL.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="8e5ff-160">Contacte [equipa de suporte de Netsuite](http://www.netsuite.com/portal/services/support.shtml) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="8e5ff-161">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="8e5ff-163">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-163">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e5ff-165">No Olá **Netsuite configuração** secção, clique em **configurar Netsuite** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8e5ff-166">Olá cópia **único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="8e5ff-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="8e5ff-168">Abra um novo separador no seu browser e inicie sessão no site da sua empresa Netsuite como administrador.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="8e5ff-169">Na barra de ferramentas Olá em Olá parte superior da página Olá, clique em **configuração**, em seguida, clique em **Gestor de configuração**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="8e5ff-171">De Olá **tarefas de configuração** lista, selecione **integração**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="8e5ff-173">No Olá **Gerir autenticação** secção, clique em **SAML-início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="8e5ff-175">No Olá **configuração SAML** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="8e5ff-176">a.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-176">a.</span></span> <span data-ttu-id="8e5ff-177">Olá cópia **único início de sessão no URL do serviço SAML** valor a partir da **referência rápida** secção **configurar início de sessão** e cole-Olá **fornecedor de identidade Página de início de sessão** campo no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="8e5ff-179">b.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-179">b.</span></span> <span data-ttu-id="8e5ff-180">No Netsuite, selecione **método de autenticação principal**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="8e5ff-181">c.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-181">c.</span></span> <span data-ttu-id="8e5ff-182">Para o campo de Olá etiquetado **os metadados do fornecedor de identidade SAMLV2**, selecione **carregar ficheiro de metadados do IDP**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="8e5ff-183">Em seguida, clique em **procurar** ficheiro de metadados de Olá tooupload que transferiu a partir do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="8e5ff-185">d.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-185">d.</span></span> <span data-ttu-id="8e5ff-186">Clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-186">Click **Submit**.</span></span>

12. <span data-ttu-id="8e5ff-187">No Azure AD, clique em **ver e editar todos os outros atributos de utilizador** caixa de verificação e adicione o atributo.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="8e5ff-189">Para Olá **nome de atributo** campo, digite na `account`.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="8e5ff-190">Para Olá **valor do atributo** campo, escreva o ID de conta Netsuite. Este valor é constante e altere com a conta.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="8e5ff-191">Instruções sobre como toofind são incluída abaixo, o ID da conta:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-191">Instructions on how toofind your account ID are included below:</span></span>

      ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="8e5ff-193">a.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-193">a.</span></span> <span data-ttu-id="8e5ff-194">No Netsuite, clique em **configuração** a partir do menu de navegação superior Olá.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="8e5ff-195">b.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-195">b.</span></span> <span data-ttu-id="8e5ff-196">Em seguida, clique em Olá **tarefas de configuração** secção do menu de navegação esquerdo Olá, selecione de Olá **integração** secção e clique em **preferências de serviços Web**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="8e5ff-197">c.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-197">c.</span></span> <span data-ttu-id="8e5ff-198">Copie o seu ID de conta Netsuite e cole-o Olá **valor do atributo** campo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="8e5ff-200">Antes dos utilizadores podem efetuar o início de sessão único para Netsuite, estes tem primeiro de atribuir as permissões adequadas Olá no Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="8e5ff-201">Siga as instruções de Olá abaixo tooassign estas permissões.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="8e5ff-202">a.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-202">a.</span></span> <span data-ttu-id="8e5ff-203">No menu de navegação superior Olá, clique em **configuração**, em seguida, clique em **Gestor de configuração**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="8e5ff-205">b.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-205">b.</span></span> <span data-ttu-id="8e5ff-206">No menu de navegação esquerdo Olá, selecione **utilizadores/funções**, em seguida, clique em **gerir funções**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="8e5ff-208">c.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-208">c.</span></span> <span data-ttu-id="8e5ff-209">Clique em **nova função**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-209">Click **New Role**.</span></span>

    <span data-ttu-id="8e5ff-210">d.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-210">d.</span></span> <span data-ttu-id="8e5ff-211">Escreva um **nome** para a sua nova função e selecione Olá **único início de sessão só** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="8e5ff-213">e.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-213">e.</span></span> <span data-ttu-id="8e5ff-214">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-214">Click **Save**.</span></span>

    <span data-ttu-id="8e5ff-215">f.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-215">f.</span></span> <span data-ttu-id="8e5ff-216">No menu de Olá na parte superior do Olá, clique em **permissões**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="8e5ff-217">Em seguida, clique em **configuração**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-217">Then click **Setup**.</span></span>
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="8e5ff-219">g.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-219">g.</span></span> <span data-ttu-id="8e5ff-220">Selecione **definir segurança SAM Single Sign-on**e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="8e5ff-221">h.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-221">h.</span></span> <span data-ttu-id="8e5ff-222">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-222">Click **Save**.</span></span>

    <span data-ttu-id="8e5ff-223">posso.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-223">i.</span></span> <span data-ttu-id="8e5ff-224">No menu de navegação superior Olá, clique em **configuração**, em seguida, clique em **Gestor de configuração**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="8e5ff-226">j.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-226">j.</span></span> <span data-ttu-id="8e5ff-227">No menu de navegação esquerdo Olá, selecione **utilizadores/funções**, em seguida, clique em **gerir utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="8e5ff-229">k.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-229">k.</span></span> <span data-ttu-id="8e5ff-230">Selecione um utilizador de teste.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-230">Select a test user.</span></span> <span data-ttu-id="8e5ff-231">Em seguida, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-231">Then click **Edit**.</span></span>
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="8e5ff-233">l.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-233">l.</span></span> <span data-ttu-id="8e5ff-234">Na caixa de diálogo de funções Olá, selecione a função de Olá que criou e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![Configurar o início de sessão único](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="8e5ff-236">m.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-236">m.</span></span> <span data-ttu-id="8e5ff-237">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="8e5ff-238">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="8e5ff-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8e5ff-239">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8e5ff-240">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e5ff-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e5ff-241">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e5ff-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e5ff-242">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="8e5ff-244">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8e5ff-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e5ff-245">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="8e5ff-247">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e5ff-249">Na parte superior de Olá da caixa de diálogo Olá, clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e5ff-251">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="8e5ff-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e5ff-253">a.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-253">a.</span></span> <span data-ttu-id="8e5ff-254">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e5ff-255">b.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-255">b.</span></span> <span data-ttu-id="8e5ff-256">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e5ff-257">c.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-257">c.</span></span> <span data-ttu-id="8e5ff-258">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8e5ff-259">d.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-259">d.</span></span> <span data-ttu-id="8e5ff-260">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="8e5ff-261">Criar um utilizador de teste Netsuite</span><span class="sxs-lookup"><span data-stu-id="8e5ff-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="8e5ff-262">Nesta secção, é criado um utilizador chamado Britta Simon Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="8e5ff-263">Netsuite suporta o aprovisionamento de just-in-time, que está ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="8e5ff-264">Não há nenhum item de ação para si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-264">There is no action item for you in this section.</span></span> <span data-ttu-id="8e5ff-265">Se um utilizador já não existe na Netsuite, uma nova é criada quando tenta tooaccess Netsuite.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8e5ff-266">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e5ff-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8e5ff-267">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="8e5ff-269">**tooassign Britta Simon tooNetsuite, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="8e5ff-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e5ff-270">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="8e5ff-272">Na lista de aplicações de Olá, selecione **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-272">In hello applications list, select **Netsuite**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="8e5ff-274">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="8e5ff-276">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-276">Click **Add** button.</span></span> <span data-ttu-id="8e5ff-277">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="8e5ff-279">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8e5ff-280">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e5ff-281">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e5ff-282">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="8e5ff-282">Testing single sign-on</span></span>

<span data-ttu-id="8e5ff-283">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8e5ff-284">tootest Olá, as único início de sessão definições, abra o painel de acesso em [https://myapps.microsoft.com](https://myapps.microsoft.com/), iniciar sessão na conta de teste de Olá e, em **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="8e5ff-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e5ff-285">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8e5ff-285">Additional resources</span></span>

* [<span data-ttu-id="8e5ff-286">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e5ff-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e5ff-287">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e5ff-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8e5ff-288">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="8e5ff-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

