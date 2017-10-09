---
title: "Tutorial: Integração do Azure Active Directory com Evidence.com | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="c05c7-103">Tutorial: Integração do Azure Active Directory com Evidence.com</span><span class="sxs-lookup"><span data-stu-id="c05c7-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="c05c7-104">Neste tutorial, saiba como toointegrate Evidence.com com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c05c7-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c05c7-105">Integrar Evidence.com com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="c05c7-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c05c7-106">Pode controlar no Azure AD que tenha acesso tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="c05c7-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="c05c7-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooEvidence.com (Single Sign-On) com as respetivas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c05c7-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c05c7-108">Pode gerir as contas numa localização central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c05c7-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="c05c7-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c05c7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c05c7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c05c7-110">Prerequisites</span></span>

<span data-ttu-id="c05c7-111">integração do Azure AD com Evidence.com tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c05c7-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="c05c7-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c05c7-113">Um Evidence.com-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="c05c7-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c05c7-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c05c7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c05c7-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c05c7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c05c7-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c05c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c05c7-117">Se não tiver um ambiente de avaliação do Azure AD, pode [obtenha uma avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c05c7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c05c7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c05c7-118">Scenario description</span></span>
<span data-ttu-id="c05c7-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c05c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c05c7-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="c05c7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c05c7-121">Adicionar Evidence.com da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="c05c7-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="c05c7-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="c05c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="c05c7-123">Adicionar Evidence.com da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="c05c7-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="c05c7-124">tooconfigure Olá integração de Evidence.com com o Azure AD, é necessário tooadd Evidence.com Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="c05c7-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c05c7-125">**tooadd Evidence.com da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="c05c7-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05c7-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="c05c7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Azure Active Directory Olá][1]

2. <span data-ttu-id="c05c7-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c05c7-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-129">Then go too**All applications**.</span></span>

    ![Painel de aplicações do Olá Enterprise][2]
    
3. <span data-ttu-id="c05c7-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c05c7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botão de aplicação nova Olá][3]

4. <span data-ttu-id="c05c7-133">Na caixa de pesquisa de Olá, escreva **Evidence.com**, selecione **Evidence.com** partir do painel de resultados, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="c05c7-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evidence.com na lista de resultados de Olá](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c05c7-135">Configurar e testar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="c05c7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c05c7-136">Nesta secção, configure e teste do Azure AD-início de sessão único com Evidence.com com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c05c7-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c05c7-137">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá Evidence.com é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c05c7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="c05c7-138">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Evidence.com tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c05c7-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="c05c7-139">No Evidence.com, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="c05c7-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c05c7-140">tooconfigure e teste do Azure AD-início de sessão único com Evidence.com, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c05c7-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c05c7-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="c05c7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c05c7-142">**[Criar um utilizador de teste do Azure AD](#create-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c05c7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c05c7-143">**[Criar um utilizador de teste Evidence.com](#create-a-evidencecom-test-user)**  -toohave um homólogo de Britta Simon no Evidence.com é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="c05c7-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c05c7-144">**[Atribua o utilizador de teste de Olá do Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="c05c7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c05c7-145">**[Teste o início de sessão único](#test-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="c05c7-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c05c7-146">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="c05c7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c05c7-147">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="c05c7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="c05c7-148">**tooconfigure do Azure AD-início de sessão único com Evidence.com, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="c05c7-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05c7-149">No Olá portal do Azure, no Olá **Evidence.com** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurar a ligação de início de sessão único][4]

2. <span data-ttu-id="c05c7-151">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="c05c7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo de início de sessão único](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="c05c7-153">No Olá **Evidence.com domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="c05c7-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Domínio Evidence.com e os URLs únicos de informações de início de sessão](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="c05c7-155">a.</span><span class="sxs-lookup"><span data-stu-id="c05c7-155">a.</span></span> <span data-ttu-id="c05c7-156">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="c05c7-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="c05c7-157">b.</span><span class="sxs-lookup"><span data-stu-id="c05c7-157">b.</span></span> <span data-ttu-id="c05c7-158">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="c05c7-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c05c7-159">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="c05c7-159">These values are not real.</span></span> <span data-ttu-id="c05c7-160">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="c05c7-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c05c7-161">Contacte [equipa de suporte de cliente Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="c05c7-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="c05c7-162">No Olá **certificado de assinatura de SAML** secção, clique em **Certificate(Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="c05c7-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![ligação de transferência do certificado Olá](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="c05c7-164">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="c05c7-164">Click **Save** button.</span></span>

    ![Configurar botão único início de sessão guardar](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c05c7-166">No Olá **Evidence.com configuração** secção, clique em **configurar Evidence.com** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="c05c7-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c05c7-167">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c05c7-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração de Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="c05c7-169">Numa janela do browser web separado, o início de sessão tooyour Evidence.com como um administrador de inquilino e navegue demasiado**Admin** separador</span><span class="sxs-lookup"><span data-stu-id="c05c7-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="c05c7-170">Clique em **Agência início de sessão único**</span><span class="sxs-lookup"><span data-stu-id="c05c7-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="c05c7-171">Selecione **SAML baseia início de sessão único**</span><span class="sxs-lookup"><span data-stu-id="c05c7-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="c05c7-172">Olá cópia **ID de entidade de SAML**, **único início de sessão no URL do serviço SAML** e **Sign-Out URL** valores apresentados nas Olá portal do Azure e toohello campos correspondente no Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="c05c7-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="c05c7-173">Abra o ficheiro transferido do Certificate(Base64) no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-toohello **certificado de segurança** caixa.</span><span class="sxs-lookup"><span data-stu-id="c05c7-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="c05c7-174">Guarde a configuração de Olá no Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="c05c7-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="c05c7-175">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="c05c7-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c05c7-176">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="c05c7-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c05c7-177">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c05c7-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c05c7-178">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05c7-178">Create an Azure AD test user</span></span>

<span data-ttu-id="c05c7-179">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c05c7-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um utilizador de teste do Azure AD][100]

<span data-ttu-id="c05c7-181">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="c05c7-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05c7-182">No Olá portal do Azure, no painel esquerdo Olá, clique em Olá **do Azure Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="c05c7-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Azure Active Directory Olá](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c05c7-184">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos**e, em seguida, clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Utilizadores e grupos" e "Todos os utilizadores" ligações](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c05c7-186">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** , Olá parte superior do Olá **todos os utilizadores** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c05c7-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão de adição de Olá](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c05c7-188">No Olá **utilizador** diálogo caixa, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="c05c7-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo utilizador Olá](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c05c7-190">a.</span><span class="sxs-lookup"><span data-stu-id="c05c7-190">a.</span></span> <span data-ttu-id="c05c7-191">No Olá **nome** caixa, escreva **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c05c7-192">b.</span><span class="sxs-lookup"><span data-stu-id="c05c7-192">b.</span></span> <span data-ttu-id="c05c7-193">No Olá **nome de utilizador** caixa, tipo Olá endereço de correio eletrónico do utilizador Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c05c7-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="c05c7-194">c.</span><span class="sxs-lookup"><span data-stu-id="c05c7-194">c.</span></span> <span data-ttu-id="c05c7-195">Selecione Olá **mostrar palavra-passe** caixa de verificação e, em seguida, anote o valor de Olá que é apresentado no Olá **palavra-passe** caixa.</span><span class="sxs-lookup"><span data-stu-id="c05c7-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="c05c7-196">d.</span><span class="sxs-lookup"><span data-stu-id="c05c7-196">d.</span></span> <span data-ttu-id="c05c7-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="c05c7-198">Criar um utilizador de teste Evidence.com</span><span class="sxs-lookup"><span data-stu-id="c05c7-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="c05c7-199">Para o Azure AD os utilizadores toobe capaz de toosign no, têm de ser aprovisionados para acesso no interior Olá Evidence.com aplicação.</span><span class="sxs-lookup"><span data-stu-id="c05c7-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="c05c7-200">Esta secção descreve como contas de utilizador toocreate do Azure AD dentro Evidence.com</span><span class="sxs-lookup"><span data-stu-id="c05c7-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="c05c7-201">**uma conta de utilizador no Evidence.com tooprovision:**</span><span class="sxs-lookup"><span data-stu-id="c05c7-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="c05c7-202">Numa janela do browser web, inicie sessão no site da sua empresa Evidence.com como administrador.</span><span class="sxs-lookup"><span data-stu-id="c05c7-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="c05c7-203">Navegue demasiado**Admin** separador.</span><span class="sxs-lookup"><span data-stu-id="c05c7-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="c05c7-204">Clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="c05c7-205">Clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="c05c7-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="c05c7-206">Olá **endereço de correio eletrónico** de Olá adicionar utilizador tem de corresponder ao nome de utilizador Olá de utilizadores de Olá no Azure AD que pretende toogive acesso.</span><span class="sxs-lookup"><span data-stu-id="c05c7-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="c05c7-207">Se Olá nome de utilizador e endereço de e-mail não são hello mesmo valor na sua organização, pode utilizar Olá **Evidence.com > atributos > Single Sign-On** secção Olá toochange portal do Azure Olá nameidenitifer enviado endereço de e-mail do tooEvidence.com toobe Olá.</span><span class="sxs-lookup"><span data-stu-id="c05c7-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c05c7-208">Atribua o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c05c7-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c05c7-209">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="c05c7-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Atribuir a função de utilizador Olá][200] 

<span data-ttu-id="c05c7-211">**tooassign Britta Simon tooEvidence.com, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="c05c7-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="c05c7-212">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="c05c7-214">Na lista de aplicações de Olá, selecione **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-214">In hello applications list, select **Evidence.com**.</span></span>

    ![ligação de Evidence.com Olá na lista de aplicações de Olá](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="c05c7-216">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c05c7-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![ligação de "Utilizadores e grupos" Olá][202]

4. <span data-ttu-id="c05c7-218">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="c05c7-218">Click **Add** button.</span></span> <span data-ttu-id="c05c7-219">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c05c7-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição de adicionar Olá][203]

5. <span data-ttu-id="c05c7-221">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="c05c7-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c05c7-222">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c05c7-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c05c7-223">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c05c7-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c05c7-224">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="c05c7-224">Test single sign-on</span></span>

<span data-ttu-id="c05c7-225">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="c05c7-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c05c7-226">Ao clicar em mosaico de Evidence.com Olá no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour Evidence.com aplicação.</span><span class="sxs-lookup"><span data-stu-id="c05c7-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="c05c7-227">Para mais informações sobre o painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c05c7-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c05c7-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c05c7-228">Additional resources</span></span>

* [<span data-ttu-id="c05c7-229">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c05c7-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c05c7-230">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c05c7-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

