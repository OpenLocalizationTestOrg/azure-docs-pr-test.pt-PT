---
title: "Tutorial: Integração do Azure Active Directory a área de trabalho por Facebook | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e à área de trabalho por Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="6636b-103">Tutorial: Integração do Azure Active Directory a área de trabalho por Facebook</span><span class="sxs-lookup"><span data-stu-id="6636b-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="6636b-104">Neste tutorial, saiba como toointegrate à área de trabalho por Facebook no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6636b-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6636b-105">Área de trabalho por Facebook a integração com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="6636b-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6636b-106">Pode controlar no Azure AD que tenha acesso tooWorkplace por Facebook</span><span class="sxs-lookup"><span data-stu-id="6636b-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="6636b-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooWorkplace por Facebook (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6636b-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6636b-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6636b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6636b-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6636b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6636b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6636b-110">Prerequisites</span></span>

<span data-ttu-id="6636b-111">integração do Azure AD a área de trabalho por Facebook tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6636b-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="6636b-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6636b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6636b-113">Uma área de trabalho por Facebook-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="6636b-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6636b-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="6636b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6636b-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="6636b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6636b-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="6636b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6636b-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6636b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6636b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="6636b-118">Scenario description</span></span>
<span data-ttu-id="6636b-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="6636b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6636b-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="6636b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6636b-121">Adicionar à área de trabalho por Facebook da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6636b-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="6636b-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6636b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="6636b-123">Adicionar à área de trabalho por Facebook da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="6636b-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="6636b-124">tooconfigure Olá integração da área de trabalho por Facebook com o Azure AD, é necessário tooadd à área de trabalho por Facebook Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="6636b-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6636b-125">**tooadd à área de trabalho por Facebook da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6636b-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6636b-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6636b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6636b-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="6636b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6636b-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6636b-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="6636b-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6636b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="6636b-133">Na caixa de pesquisa de Olá, escreva **à área de trabalho por Facebook**.</span><span class="sxs-lookup"><span data-stu-id="6636b-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="6636b-135">No painel de resultados de Olá, selecione **à área de trabalho por Facebook**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="6636b-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6636b-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="6636b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6636b-138">Nesta secção, configurar e testar o Azure AD-início de sessão único a área de trabalho por Facebook com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6636b-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6636b-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na área de trabalho por Facebook é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6636b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="6636b-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na área de trabalho por Facebook tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="6636b-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="6636b-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** na área de trabalho por Facebook.</span><span class="sxs-lookup"><span data-stu-id="6636b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="6636b-142">tooconfigure e teste do Azure AD-início de sessão único, a área de trabalho, Facebook, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6636b-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6636b-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="6636b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6636b-144">**[Configurar a frequência de reautenticação](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt de área de trabalho para uma verificação SAML.</span><span class="sxs-lookup"><span data-stu-id="6636b-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="6636b-145">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6636b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="6636b-146">**[Criar uma área de trabalho por utilizador de teste do Facebook](#creating-a-workplace-by-facebook-test-user)**  -toohave um homólogo de Britta Simon na área de trabalho por Facebook é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="6636b-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="6636b-147">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6636b-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="6636b-148">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="6636b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6636b-149">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6636b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6636b-150">Nesta secção, ativar o Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua área de trabalho por aplicação do Facebook.</span><span class="sxs-lookup"><span data-stu-id="6636b-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="6636b-151">**tooconfigure do Azure AD-início de sessão único a área de trabalho, Facebook, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6636b-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="6636b-152">No Olá portal do Azure, no Olá **à área de trabalho por Facebook** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="6636b-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="6636b-154">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="6636b-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="6636b-156">No Olá **à área de trabalho ao domínio do Facebook e URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6636b-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="6636b-158">a.</span><span class="sxs-lookup"><span data-stu-id="6636b-158">a.</span></span> <span data-ttu-id="6636b-159">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="6636b-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="6636b-160">b.</span><span class="sxs-lookup"><span data-stu-id="6636b-160">b.</span></span> <span data-ttu-id="6636b-161">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="6636b-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6636b-162">Estes valores não estiverem Olá real.</span><span class="sxs-lookup"><span data-stu-id="6636b-162">These values are not hello real.</span></span> <span data-ttu-id="6636b-163">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="6636b-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6636b-164">Contacte [à área de trabalho pela equipa de suporte de cliente do Facebook](https://workplace.fb.com/faq/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="6636b-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="6636b-165">No Olá **certificado de assinatura de SAML** secção, clique em **certificado (Base64)** e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6636b-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="6636b-167">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="6636b-167">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6636b-169">No Olá **à área de trabalho pela configuração do Facebook** secção, clique em **configurar área de trabalho por Facebook** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="6636b-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="6636b-170">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="6636b-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="6636b-172">Numa janela do browser web diferente, tooyour de início de sessão à área de trabalho por site de empresa do Facebook como administrador.</span><span class="sxs-lookup"><span data-stu-id="6636b-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="6636b-173">Como parte do Olá processo de autenticação SAML, à área de trabalho pode utilizar cadeias de consulta de cópia de segurança too2.5 quilobytes em tamanho em ordem toopass parâmetros tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="6636b-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="6636b-174">No Olá **Dashboard da empresa**, aceda a toohello **autenticação** separador.</span><span class="sxs-lookup"><span data-stu-id="6636b-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="6636b-175">Em **autenticação SAML**, selecione **SSO apenas** de Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="6636b-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="6636b-176">Os valores de entrada Olá copiados **à área de trabalho pela configuração do Facebook** secção Olá portal do Azure em campos correspondente Olá:</span><span class="sxs-lookup"><span data-stu-id="6636b-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="6636b-177">No **SAML URL** caixa de texto, colar Olá valor **URL Single Sign-On serviço**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6636b-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="6636b-178">No **caixa de texto do URL do emissor de SAML**, cole o valor de Olá de **ID de entidade de SAML**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6636b-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="6636b-179">No **redirecionamento de fim de sessão SAML** (opcional), cole o valor Olá **Sign-Out URL**, que copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6636b-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="6636b-180">Abra o **certificado com codificação base 64** no bloco de notas transferido a partir do portal do Azure, copiar o conteúdo de Olá-lo na sua área de transferência e, em seguida, cole-toothe **SAML certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6636b-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="6636b-181">Poderá ser necessário tooenter Olá URL público-alvo, URL de destinatário, e o URL de ACS (serviço de consumidor asserção) listados em Olá **configuração SAML** secção.</span><span class="sxs-lookup"><span data-stu-id="6636b-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="6636b-182">Desloque-se na parte inferior de toohello da secção de Olá e clique em Olá **teste SSO** botão.</span><span class="sxs-lookup"><span data-stu-id="6636b-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="6636b-183">Isto resulta numa janela de pop-up apresentação com a página de início de sessão do Azure AD apresentados.</span><span class="sxs-lookup"><span data-stu-id="6636b-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="6636b-184">Introduza as suas credenciais como normal tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="6636b-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="6636b-185">**Resolução de problemas:** endereço de correio eletrónico Olá Certifique-se de que está a ser devolvido atrás do Azure AD é Olá igual ao hello conta à área de trabalho, o qual iniciou sessão com.</span><span class="sxs-lookup"><span data-stu-id="6636b-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="6636b-186">Depois de teste de Olá foi concluída com êxito, desloque-se toohello inferior da página Olá e clique em Olá **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="6636b-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="6636b-187">Todos os utilizadores usem à área de trabalho serão agora apresentados com a página de início de sessão do Azure AD para autenticação.</span><span class="sxs-lookup"><span data-stu-id="6636b-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="6636b-188">**Redirecionamento de fim de sessão de SAML (opcional)** -</span><span class="sxs-lookup"><span data-stu-id="6636b-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="6636b-189">Pode escolher toooptionally configurar um Url de fim de sessão SAML, que pode ser utilizado toopoint na página de fim de sessão do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6636b-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="6636b-190">Quando esta definição está ativada e configurada, o utilizador Olá deixará de estar página de fim de sessão do toohello direcionados à área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6636b-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="6636b-191">Em vez disso, o utilizador Olá será redirecionada toohello url que foi adicionado na definição de redirecionamento de fim de sessão SAML Olá.</span><span class="sxs-lookup"><span data-stu-id="6636b-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="6636b-192">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="6636b-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6636b-193">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="6636b-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6636b-194">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6636b-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="6636b-195">Configurar a frequência de reautenticação rápida</span><span class="sxs-lookup"><span data-stu-id="6636b-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="6636b-196">Pode configurar tooprompt à área de trabalho para uma verificação SAML diariamente, três dias, semanas, duas semanas, meses ou nunca.</span><span class="sxs-lookup"><span data-stu-id="6636b-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="6636b-197">Olá valor mínimo para a verificação SAML Olá em aplicações móveis está definido tooone semana.</span><span class="sxs-lookup"><span data-stu-id="6636b-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="6636b-198">Pode também forçar um SAML repor para todos os utilizadores com o botão de Olá: exigir autenticação SAML para todos os utilizadores agora.</span><span class="sxs-lookup"><span data-stu-id="6636b-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6636b-199">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6636b-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="6636b-200">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6636b-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="6636b-202">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6636b-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6636b-203">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="6636b-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6636b-205">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="6636b-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6636b-207">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="6636b-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6636b-209">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="6636b-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6636b-211">a.</span><span class="sxs-lookup"><span data-stu-id="6636b-211">a.</span></span> <span data-ttu-id="6636b-212">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6636b-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6636b-213">b.</span><span class="sxs-lookup"><span data-stu-id="6636b-213">b.</span></span> <span data-ttu-id="6636b-214">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6636b-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6636b-215">c.</span><span class="sxs-lookup"><span data-stu-id="6636b-215">c.</span></span> <span data-ttu-id="6636b-216">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="6636b-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6636b-217">d.</span><span class="sxs-lookup"><span data-stu-id="6636b-217">d.</span></span> <span data-ttu-id="6636b-218">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6636b-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="6636b-219">Criar uma área de trabalho por utilizador de teste do Facebook</span><span class="sxs-lookup"><span data-stu-id="6636b-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="6636b-220">Nesta secção, um utilizador chamado Britta Simon é criado na área de trabalho por Facebook.</span><span class="sxs-lookup"><span data-stu-id="6636b-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="6636b-221">Área de trabalho por Facebook suporta o aprovisionamento de just-in-time, que está ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="6636b-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="6636b-222">Não há nenhuma ação por si nesta secção.</span><span class="sxs-lookup"><span data-stu-id="6636b-222">There is no action for you in this section.</span></span> <span data-ttu-id="6636b-223">Se um utilizador não existe na área de trabalho, Facebook, uma nova é criada quando tenta tooaccess à área de trabalho por Facebook.</span><span class="sxs-lookup"><span data-stu-id="6636b-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="6636b-224">Se precisar de toocreate manualmente, contacte um utilizador [à área de trabalho pela equipa de suporte de cliente do Facebook](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="6636b-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6636b-225">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6636b-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6636b-226">Nesta secção, ative Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooWorkplace por Facebook.</span><span class="sxs-lookup"><span data-stu-id="6636b-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="6636b-228">**tooassign Britta Simon tooWorkplace por Facebook, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="6636b-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="6636b-229">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="6636b-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="6636b-231">Na lista de aplicações de Olá, selecione **à área de trabalho por Facebook**.</span><span class="sxs-lookup"><span data-stu-id="6636b-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="6636b-233">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="6636b-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="6636b-235">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="6636b-235">Click **Add** button.</span></span> <span data-ttu-id="6636b-236">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6636b-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="6636b-238">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="6636b-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6636b-239">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6636b-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6636b-240">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6636b-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6636b-241">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="6636b-241">Testing single sign-on</span></span>

<span data-ttu-id="6636b-242">Se quiser tootest as definições de início de sessão único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="6636b-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="6636b-243">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6636b-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6636b-244">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="6636b-244">Additional resources</span></span>

* [<span data-ttu-id="6636b-245">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6636b-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6636b-246">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6636b-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="6636b-247">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="6636b-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

