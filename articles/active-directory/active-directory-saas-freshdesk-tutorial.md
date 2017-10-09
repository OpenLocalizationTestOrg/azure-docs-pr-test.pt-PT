---
title: "Tutorial: Integração do Azure Active Directory com FreshDesk | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="f140c-103">Tutorial: Integração do Azure Active Directory com FreshDesk</span><span class="sxs-lookup"><span data-stu-id="f140c-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="f140c-104">Neste tutorial, saiba como toointegrate FreshDesk com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f140c-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f140c-105">Integrar FreshDesk com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="f140c-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f140c-106">Pode controlar no Azure AD que tenha acesso tooFreshDesk</span><span class="sxs-lookup"><span data-stu-id="f140c-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="f140c-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooFreshDesk (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f140c-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f140c-108">Pode gerir as contas numa localização central - portal de gestão do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="f140c-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="f140c-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f140c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f140c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f140c-110">Prerequisites</span></span>

<span data-ttu-id="f140c-111">integração do Azure AD com FreshDesk tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f140c-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="f140c-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f140c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f140c-113">Um FreshDesk início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="f140c-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f140c-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="f140c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f140c-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="f140c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f140c-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="f140c-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f140c-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f140c-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f140c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="f140c-118">Scenario description</span></span>
<span data-ttu-id="f140c-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="f140c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f140c-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="f140c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f140c-121">Adicionar FreshDesk da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f140c-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="f140c-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f140c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="f140c-123">Adicionar FreshDesk da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="f140c-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="f140c-124">tooconfigure Olá integração de FreshDesk com o Azure AD, é necessário tooadd FreshDesk Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="f140c-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f140c-125">**tooadd FreshDesk da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f140c-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f140c-126">No Olá  **[Azure Management Portal](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f140c-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f140c-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f140c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f140c-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f140c-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="f140c-131">Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="f140c-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="f140c-133">Na caixa de pesquisa de Olá, escreva **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="f140c-133">In hello search box, type **FreshDesk**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="f140c-135">No painel de resultados de Olá, selecione **FreshDesk**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="f140c-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f140c-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="f140c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f140c-138">Nesta secção, configure e teste do Azure AD-início de sessão único com FreshDesk com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f140c-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f140c-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá FreshDesk é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f140c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="f140c-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá FreshDesk tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f140c-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="f140c-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="f140c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="f140c-142">tooconfigure e teste do Azure AD-início de sessão único com FreshDesk, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f140c-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f140c-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f140c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f140c-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f140c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f140c-145">**[Criar um utilizador de teste FreshDesk](#creating-a-freshdesk-test-user)**  -toohave um homólogo de Britta Simon no FreshDesk é-lhe representação toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f140c-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="f140c-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f140c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f140c-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="f140c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f140c-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f140c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f140c-149">Nesta secção, pode ativar do Azure AD início de sessão no portal de gestão do Azure Olá e configurar o início de sessão único na sua aplicação FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="f140c-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="f140c-150">**tooconfigure do Azure AD-início de sessão único com FreshDesk, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f140c-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="f140c-151">No portal de gestão do Azure de Olá, no Olá **FreshDesk** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="f140c-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="f140c-153">No Olá **de sessão único-** caixa de diálogo, como **modo** selecione **baseados em SAML início de sessão** tooenable início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="f140c-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="f140c-155">No Olá **FreshDesk domínio e os URLs** secção, introduza Olá **URL de início de sessão** como: `https://<tenant-name>.freshdesk.com` ou qualquer outro valor Freshdesk tem sugeridos.</span><span class="sxs-lookup"><span data-stu-id="f140c-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="f140c-157">Tenha em atenção que isto não é o valor real.</span><span class="sxs-lookup"><span data-stu-id="f140c-157">Please note that this is not the real value.</span></span> <span data-ttu-id="f140c-158">Tem de atualizar o valor com o URL de início de sessão real.</span><span class="sxs-lookup"><span data-stu-id="f140c-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="f140c-159">Contacte [equipa de suporte de cliente FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) para obter este valor.</span><span class="sxs-lookup"><span data-stu-id="f140c-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="f140c-160">No Olá **certificado de assinatura de SAML** secção, clique em **certificado** e, em seguida, guarde o certificado de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="f140c-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="f140c-162">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="f140c-162">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f140c-164">No Olá **FreshDesk configuração** secção, clique em **configurar FreshDesk** janela tooopen configurar início de sessão.</span><span class="sxs-lookup"><span data-stu-id="f140c-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="f140c-165">Copiar Olá único início de sessão no URL do serviço SAML e o URL de Sign-Out de Olá **referência rápida** secção.</span><span class="sxs-lookup"><span data-stu-id="f140c-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="f140c-167">Numa janela do browser web diferente, inicie sessão no site da sua empresa Freshdesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="f140c-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="f140c-168">No menu de Olá na parte superior do Olá, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f140c-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="f140c-169">![Administração](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f140c-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="f140c-170">No Olá **definições gerais** separador, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="f140c-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="f140c-171">![Segurança](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "segurança")</span><span class="sxs-lookup"><span data-stu-id="f140c-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="f140c-172">No Olá **segurança** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f140c-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f140c-173">![Início de sessão único](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="f140c-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="f140c-174">a.</span><span class="sxs-lookup"><span data-stu-id="f140c-174">a.</span></span> <span data-ttu-id="f140c-175">Para **único início de sessão (SSO)**, selecione **no**.</span><span class="sxs-lookup"><span data-stu-id="f140c-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="f140c-176">b.</span><span class="sxs-lookup"><span data-stu-id="f140c-176">b.</span></span> <span data-ttu-id="f140c-177">Selecione **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="f140c-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="f140c-178">c.</span><span class="sxs-lookup"><span data-stu-id="f140c-178">c.</span></span> <span data-ttu-id="f140c-179">Olá tipo **único início de sessão no URL do serviço SAML** copiados a partir do portal do Azure para Olá **URL de início de sessão SAML** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f140c-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="f140c-180">d.</span><span class="sxs-lookup"><span data-stu-id="f140c-180">d.</span></span> <span data-ttu-id="f140c-181">Olá tipo **Sign-Out URL** copiados a partir do portal do Azure para Olá **URL de fim de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f140c-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="f140c-182">e.</span><span class="sxs-lookup"><span data-stu-id="f140c-182">e.</span></span> <span data-ttu-id="f140c-183">Olá cópia **Thumbprint** valor do certificado de Olá transferido a partir do portal do Azure e cole-o Olá **impressão digital do certificado de segurança** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="f140c-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="f140c-184">Para obter mais detalhes, consulte [como tooretrieve valor do thumbprint do certificado](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="f140c-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="f140c-185">f.</span><span class="sxs-lookup"><span data-stu-id="f140c-185">f.</span></span> <span data-ttu-id="f140c-186">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f140c-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f140c-187">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f140c-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f140c-188">o objetivo desta secção Olá é toocreate um utilizador de teste no portal de gestão do Azure de Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f140c-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="f140c-190">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f140c-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f140c-191">No Olá **portal de gestão do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="f140c-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f140c-193">Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores** lista de Olá toodisplay de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="f140c-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f140c-195">Na parte superior de Olá da caixa de diálogo Olá clique **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f140c-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f140c-197">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f140c-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f140c-199">a.</span><span class="sxs-lookup"><span data-stu-id="f140c-199">a.</span></span> <span data-ttu-id="f140c-200">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f140c-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f140c-201">b.</span><span class="sxs-lookup"><span data-stu-id="f140c-201">b.</span></span> <span data-ttu-id="f140c-202">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f140c-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f140c-203">c.</span><span class="sxs-lookup"><span data-stu-id="f140c-203">c.</span></span> <span data-ttu-id="f140c-204">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="f140c-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f140c-205">d.</span><span class="sxs-lookup"><span data-stu-id="f140c-205">d.</span></span> <span data-ttu-id="f140c-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f140c-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="f140c-207">Criar um utilizador de teste FreshDesk</span><span class="sxs-lookup"><span data-stu-id="f140c-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="f140c-208">Na ordem tooenable do Azure AD os utilizadores toolog para FreshDesk, têm de ser aprovisionados para FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="f140c-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="f140c-209">No caso de Olá da FreshDesk, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="f140c-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="f140c-210">**executar de contas de utilizador, tooprovision Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f140c-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="f140c-211">Inicie sessão no tooyour **Freshdesk** inquilino.</span><span class="sxs-lookup"><span data-stu-id="f140c-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="f140c-212">No menu de Olá na parte superior do Olá, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="f140c-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="f140c-213">![Administração](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="f140c-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="f140c-214">No Olá **definições gerais** separador, clique em **agentes**.</span><span class="sxs-lookup"><span data-stu-id="f140c-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="f140c-215">![Agentes](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "agentes")</span><span class="sxs-lookup"><span data-stu-id="f140c-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="f140c-216">Clique em **novo agente**.</span><span class="sxs-lookup"><span data-stu-id="f140c-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="f140c-217">![Novo agente](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "novo agente")</span><span class="sxs-lookup"><span data-stu-id="f140c-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="f140c-218">Na caixa de diálogo de informações de agentes Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f140c-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="f140c-219">![Informações de agentes](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "informações de agentes")</span><span class="sxs-lookup"><span data-stu-id="f140c-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="f140c-220">a.</span><span class="sxs-lookup"><span data-stu-id="f140c-220">a.</span></span> <span data-ttu-id="f140c-221">No Olá **nome completo** caixa de texto, nome do tipo Olá da conta de Olá do Azure AD que pretende tooprovision.</span><span class="sxs-lookup"><span data-stu-id="f140c-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="f140c-222">b.</span><span class="sxs-lookup"><span data-stu-id="f140c-222">b.</span></span> <span data-ttu-id="f140c-223">No Olá **E-Mail** caixa de texto, Olá de tipo do Azure AD endereço de e-mail da conta de Olá do Azure AD que pretende tooprovision.</span><span class="sxs-lookup"><span data-stu-id="f140c-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="f140c-224">c.</span><span class="sxs-lookup"><span data-stu-id="f140c-224">c.</span></span> <span data-ttu-id="f140c-225">No Olá **título** caixa de texto, tipo Olá título da conta de Olá do Azure AD que pretende tooprovision.</span><span class="sxs-lookup"><span data-stu-id="f140c-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="f140c-226">d.</span><span class="sxs-lookup"><span data-stu-id="f140c-226">d.</span></span> <span data-ttu-id="f140c-227">Selecione **função agentes**e, em seguida, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="f140c-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="f140c-228">e.</span><span class="sxs-lookup"><span data-stu-id="f140c-228">e.</span></span> <span data-ttu-id="f140c-229">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="f140c-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="f140c-230">titular da conta do Olá do Azure AD irá receber uma mensagem de e-mail que inclui uma conta de Olá tooconfirm ligação antes de ser ativado.</span><span class="sxs-lookup"><span data-stu-id="f140c-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="f140c-231">Pode utilizar quaisquer outras Freshdesk utilizador conta criação ferramentas ou APIs fornecidas pelo Freshdesk tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="f140c-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="f140c-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="f140c-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f140c-233">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f140c-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f140c-234">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo utras tooBox de acesso.</span><span class="sxs-lookup"><span data-stu-id="f140c-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="f140c-236">**tooassign Britta Simon tooFreshDesk, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="f140c-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="f140c-237">No portal de gestão do Azure de Olá, abra a vista de aplicações de Olá e, em seguida, navegue até a vista de diretório toohello e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="f140c-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="f140c-239">Na lista de aplicações de Olá, selecione **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="f140c-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="f140c-241">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f140c-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="f140c-243">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="f140c-243">Click **Add** button.</span></span> <span data-ttu-id="f140c-244">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f140c-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="f140c-246">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="f140c-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f140c-247">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f140c-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f140c-248">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f140c-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f140c-249">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="f140c-249">Testing single sign-on</span></span>

<span data-ttu-id="f140c-250">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="f140c-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f140c-251">Ao clicar em mosaico de FreshDesk Olá no painel de acesso de Olá, deve obter início de sessão página tooget com sessão iniciada tooyour FreshDesk aplicação.</span><span class="sxs-lookup"><span data-stu-id="f140c-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f140c-252">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f140c-252">Additional resources</span></span>

* [<span data-ttu-id="f140c-253">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f140c-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f140c-254">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f140c-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

