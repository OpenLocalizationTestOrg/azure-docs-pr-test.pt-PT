---
title: "Tutorial: Integração do Azure Active Directory com IQNavigator VMS | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e IQNavigator VMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a8a09b25-dfa5-4c31-aea2-53bf1853b365
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 5a5a7dd3f427acfba2f0ae10552a7179db730118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-iqnavigator-vms"></a><span data-ttu-id="3eb3f-103">Tutorial: Integração do Azure Active Directory com IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="3eb3f-103">Tutorial: Azure Active Directory integration with IQNavigator VMS</span></span>

<span data-ttu-id="3eb3f-104">Neste tutorial, saiba como toointegrate IQNavigator VMS no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3eb3f-104">In this tutorial, you learn how toointegrate IQNavigator VMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3eb3f-105">Integrar IQNavigator VMS com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-105">Integrating IQNavigator VMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3eb3f-106">Pode controlar no Azure AD que tenha acesso tooIQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="3eb3f-106">You can control in Azure AD who has access tooIQNavigator VMS</span></span>
- <span data-ttu-id="3eb3f-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooIQNavigator VMS (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb3f-107">You can enable your users tooautomatically get signed-on tooIQNavigator VMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3eb3f-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3eb3f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3eb3f-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3eb3f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3eb3f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3eb3f-110">Prerequisites</span></span>

<span data-ttu-id="3eb3f-111">integração do AD do Azure com IQNavigator VMS tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-111">tooconfigure Azure AD integration with IQNavigator VMS, you need hello following items:</span></span>

- <span data-ttu-id="3eb3f-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3eb3f-113">Um IQNavigator VMS-início de sessão único ativada subscrição</span><span class="sxs-lookup"><span data-stu-id="3eb3f-113">A IQNavigator VMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3eb3f-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3eb3f-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3eb3f-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3eb3f-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês aqui [oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3eb3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3eb3f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3eb3f-118">Scenario description</span></span>
<span data-ttu-id="3eb3f-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3eb3f-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3eb3f-121">Adicionar IQNavigator VMS da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="3eb3f-121">Adding IQNavigator VMS from hello gallery</span></span>
2. <span data-ttu-id="3eb3f-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="3eb3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-iqnavigator-vms-from-hello-gallery"></a><span data-ttu-id="3eb3f-123">Adicionar IQNavigator VMS da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="3eb3f-123">Adding IQNavigator VMS from hello gallery</span></span>
<span data-ttu-id="3eb3f-124">tooconfigure Olá integração de IQNavigator VMS com o Azure AD, é necessário tooadd IQNavigator VMS Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-124">tooconfigure hello integration of IQNavigator VMS into Azure AD, you need tooadd IQNavigator VMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3eb3f-125">**tooadd IQNavigator VMS na Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3eb3f-125">**tooadd IQNavigator VMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3eb3f-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3eb3f-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3eb3f-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="3eb3f-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="3eb3f-133">Na caixa de pesquisa de Olá, escreva **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-133">In hello search box, type **IQNavigator VMS**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_search.png)

5. <span data-ttu-id="3eb3f-135">No painel de resultados de Olá, selecione **IQNavigator VMS**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-135">In hello results panel, select **IQNavigator VMS**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3eb3f-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="3eb3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3eb3f-138">Nesta secção, configure e teste do Azure AD-início de sessão único com IQNavigator VMS baseado na chamado "Britta Simon" um utilizador de teste.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-138">In this section, you configure and test Azure AD single sign-on with IQNavigator VMS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3eb3f-139">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador homólogo Olá IQNavigator VMS é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IQNavigator VMS is tooa user in Azure AD.</span></span> <span data-ttu-id="3eb3f-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá IQNavigator VMS tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-140">In other words, a link relationship between an Azure AD user and hello related user in IQNavigator VMS needs toobe established.</span></span>

<span data-ttu-id="3eb3f-141">Em IQNavigator VMS, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-141">In IQNavigator VMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3eb3f-142">tooconfigure e teste do Azure AD-início de sessão único com IQNavigator VMS, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-142">tooconfigure and test Azure AD single sign-on with IQNavigator VMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3eb3f-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3eb3f-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3eb3f-145">**[Criar um utilizador de teste de IQNavigator VMS](#creating-a-iqnavigator-vms-test-user)**  -toohave um homólogo de Britta Simon em VMS IQNavigator que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-145">**[Creating a IQNavigator VMS test user](#creating-a-iqnavigator-vms-test-user)** - toohave a counterpart of Britta Simon in IQNavigator VMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3eb3f-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3eb3f-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3eb3f-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="3eb3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3eb3f-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IQNavigator VMS application.</span></span>

<span data-ttu-id="3eb3f-150">**tooconfigure do Azure AD-início de sessão único com IQNavigator VMS, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3eb3f-150">**tooconfigure Azure AD single sign-on with IQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="3eb3f-151">No Olá portal do Azure, no Olá **IQNavigator VMS** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-151">In hello Azure portal, on hello **IQNavigator VMS** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="3eb3f-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_samlbase.png)

3. <span data-ttu-id="3eb3f-155">No Olá **IQNavigator VMS domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-155">On hello **IQNavigator VMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url.png)

    <span data-ttu-id="3eb3f-157">a.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-157">a.</span></span> <span data-ttu-id="3eb3f-158">No Olá **identificador** caixa de texto, tipo Olá URL:`iqn.com`</span><span class="sxs-lookup"><span data-stu-id="3eb3f-158">In hello **Identifier** textbox, type hello URL:`iqn.com`</span></span>

    <span data-ttu-id="3eb3f-159">b.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-159">b.</span></span> <span data-ttu-id="3eb3f-160">No Olá **URL de resposta** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="3eb3f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.iqnavigator.com/security/login?client_name=https://sts.window.net/<instance name>`</span></span>

4. <span data-ttu-id="3eb3f-161">Verifique **Mostrar avançadas definições de URL**, efetuar Olá passo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-161">Check **Show advanced URL settings**, perform hello following step:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_url1.png)

    <span data-ttu-id="3eb3f-163">No Olá **reencaminhamento estado** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<subdomain>.iqnavigator.com`</span><span class="sxs-lookup"><span data-stu-id="3eb3f-163">In hello **Relay state** textbox, type a URL using hello following pattern:`https://<subdomain>.iqnavigator.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3eb3f-164">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-164">These values are not real.</span></span> <span data-ttu-id="3eb3f-165">Atualize estes valores com o estado de URL de resposta e reencaminhamento real no Olá.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-165">Update these values with hello actual Reply URL and Relay state.</span></span> <span data-ttu-id="3eb3f-166">Contacte [equipa de suporte de cliente de VMS IQNavigator](https://www.beeline.com/iqn-product-support/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-166">Contact [IQNavigator VMS Client support team](https://www.beeline.com/iqn-product-support/) tooget these values.</span></span> 

5. <span data-ttu-id="3eb3f-167">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-167">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3eb3f-169">Olá toogenerate **metadados** url, efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-169">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="3eb3f-170">a.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-170">a.</span></span> <span data-ttu-id="3eb3f-171">Clique em **registos de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-171">Click **App registrations**.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appregistrations.png)
   
    <span data-ttu-id="3eb3f-173">b.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-173">b.</span></span> <span data-ttu-id="3eb3f-174">Clique em **pontos finais** tooopen **pontos finais** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-174">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpointicon.png)

    <span data-ttu-id="3eb3f-176">c.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-176">c.</span></span> <span data-ttu-id="3eb3f-177">Clique em Olá cópia botão toocopy **documento de METADADOS de Federação** url e cole-o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-177">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_endpoint.png)
     
    <span data-ttu-id="3eb3f-179">d.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-179">d.</span></span> <span data-ttu-id="3eb3f-180">Agora, a página de propriedades de toohello de **IQNavigator VMS** e Olá cópia **Id da aplicação** utilizando **cópia** botão e cole-o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-180">Now go toohello property page of **IQNavigator VMS** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_appid.png)

    <span data-ttu-id="3eb3f-182">e.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-182">e.</span></span> <span data-ttu-id="3eb3f-183">Gerar Olá **URL de metadados** Olá seguir o padrão de utilização:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="3eb3f-183">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

7. <span data-ttu-id="3eb3f-184">Aplicação de IQNavigator esperar valor do identificador de utilizador exclusivo Olá na afirmação de identificador de nome de Olá.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-184">IQNavigator application expect hello unique user identifier value in hello Name Identifier claim.</span></span> <span data-ttu-id="3eb3f-185">Cliente pode mapear o valor correto Olá Olá afirmação de identificador de nome.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-185">Customer can map hello correct value for hello Name Identifier claim.</span></span> <span data-ttu-id="3eb3f-186">Neste caso, podemos ter mapeado utilizador Olá. UserPrincipalName para fins de demonstração de Olá.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-186">In this case we have mapped hello user.UserPrincipalName for hello demo purpose.</span></span> <span data-ttu-id="3eb3f-187">Mas, de acordo com tooyour definições de organização deve mapear o valor correto Olá para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-187">But according tooyour organization settings you should map hello correct value for it.</span></span>   

    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_attribute.png)

8. <span data-ttu-id="3eb3f-189">No Olá **IQNavigator VMS configuração** secção, clique em **configurar VMS de IQNavigator** tooopen **configurar início de sessão** janela.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-189">On hello **IQNavigator VMS Configuration** section, click **Configure IQNavigator VMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3eb3f-190">Olá cópia **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** de Olá **secção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="3eb3f-190">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_configure.png) 

9. <span data-ttu-id="3eb3f-192">tooconfigure-início de sessão único em **IQNavigator VMS** lado a lado, terá de toosend Olá **URL de metadados**, **Sign-Out URL, o ID de entidade de SAML e o único início de sessão no URL do serviço SAML** demasiado [Equipa de suporte de IQNavigator VMS](https://www.beeline.com/iqn-product-support/).</span><span class="sxs-lookup"><span data-stu-id="3eb3f-192">tooconfigure single sign-on on **IQNavigator VMS** side, you need toosend hello **Metadata URL**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/).</span></span> <span data-ttu-id="3eb3f-193">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3eb3f-194">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="3eb3f-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3eb3f-195">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3eb3f-196">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3eb3f-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3eb3f-197">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb3f-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="3eb3f-198">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="3eb3f-200">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3eb3f-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3eb3f-201">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3eb3f-203">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3eb3f-205">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3eb3f-207">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="3eb3f-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-iqnavigatorvms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3eb3f-209">a.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-209">a.</span></span> <span data-ttu-id="3eb3f-210">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3eb3f-211">b.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-211">b.</span></span> <span data-ttu-id="3eb3f-212">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3eb3f-213">c.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-213">c.</span></span> <span data-ttu-id="3eb3f-214">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3eb3f-215">d.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-215">d.</span></span> <span data-ttu-id="3eb3f-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-216">Click **Create**.</span></span>
 
### <a name="creating-a-iqnavigator-vms-test-user"></a><span data-ttu-id="3eb3f-217">Criar um utilizador de teste IQNavigator VMS</span><span class="sxs-lookup"><span data-stu-id="3eb3f-217">Creating a IQNavigator VMS test user</span></span>

<span data-ttu-id="3eb3f-218">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon em IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-218">hello objective of this section is toocreate a user called Britta Simon in IQNavigator VMS.</span></span> <span data-ttu-id="3eb3f-219">Trabalhar com [equipa de suporte de IQNavigator VMS](https://www.beeline.com/iqn-product-support/) tooadd utilizadores Olá Olá conta IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-219">Work with  [IQNavigator VMS support team](https://www.beeline.com/iqn-product-support/) tooadd hello users in hello IQNavigator VMS account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3eb3f-220">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb3f-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3eb3f-221">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooIQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIQNavigator VMS.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="3eb3f-223">**tooassign Britta Simon tooIQNavigator VMS, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="3eb3f-223">**tooassign Britta Simon tooIQNavigator VMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="3eb3f-224">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="3eb3f-226">Na lista de aplicações de Olá, selecione **IQNavigator VMS**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-226">In hello applications list, select **IQNavigator VMS**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_iqnavigatorvms_app.png) 

3. <span data-ttu-id="3eb3f-228">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="3eb3f-230">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-230">Click **Add** button.</span></span> <span data-ttu-id="3eb3f-231">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="3eb3f-233">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3eb3f-234">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3eb3f-235">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3eb3f-236">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="3eb3f-236">Testing single sign-on</span></span>

<span data-ttu-id="3eb3f-237">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3eb3f-238">Ao clicar Olá mosaico IQNavigator VMS no painel de acesso de Olá, deve obter automaticamente com sessão iniciada tooyour aplicação IQNavigator VMS.</span><span class="sxs-lookup"><span data-stu-id="3eb3f-238">When you click hello IQNavigator VMS tile in hello Access Panel, you should get automatically signed-on tooyour IQNavigator VMS application.</span></span>
<span data-ttu-id="3eb3f-239">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3eb3f-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3eb3f-240">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3eb3f-240">Additional resources</span></span>

* [<span data-ttu-id="3eb3f-241">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3eb3f-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3eb3f-242">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3eb3f-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-iqnavigatorvms-tutorial/tutorial_general_203.png

