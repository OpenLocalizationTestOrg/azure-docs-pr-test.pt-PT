---
title: "Tutorial: Integração do Azure Active Directory com LinkedIn Learning | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e LinkedIn Learning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a><span data-ttu-id="b010b-103">Tutorial: Integração do Azure Active Directory com LinkedIn Learning</span><span class="sxs-lookup"><span data-stu-id="b010b-103">Tutorial: Azure Active Directory integration with LinkedIn Learning</span></span>

<span data-ttu-id="b010b-104">Neste tutorial, saiba como toointegrate LinkedIn Learning no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b010b-104">In this tutorial, you learn how toointegrate LinkedIn Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b010b-105">Integrar o LinkedIn Learning com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="b010b-105">Integrating LinkedIn Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b010b-106">Pode controlar no Azure AD que tenha acesso tooLinkedIn de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="b010b-106">You can control in Azure AD who has access tooLinkedIn Learning</span></span>
- <span data-ttu-id="b010b-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooLinkedIn Learning (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b010b-107">You can enable your users tooautomatically get signed-on tooLinkedIn Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b010b-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b010b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b010b-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b010b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b010b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b010b-110">Prerequisites</span></span>

<span data-ttu-id="b010b-111">integração do Azure AD com o LinkedIn Learning tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="b010b-111">tooconfigure Azure AD integration with LinkedIn Learning, you need hello following items:</span></span>

- <span data-ttu-id="b010b-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b010b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b010b-113">Um LinkedIn Learning início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="b010b-113">A LinkedIn Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b010b-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b010b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b010b-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b010b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b010b-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b010b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b010b-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b010b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b010b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b010b-118">Scenario description</span></span>
<span data-ttu-id="b010b-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b010b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b010b-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="b010b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b010b-121">A adição de aprendizagem do LinkedIn da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="b010b-121">Adding LinkedIn Learning from hello gallery</span></span>
2. <span data-ttu-id="b010b-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="b010b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-learning-from-hello-gallery"></a><span data-ttu-id="b010b-123">A adição de aprendizagem do LinkedIn da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="b010b-123">Adding LinkedIn Learning from hello gallery</span></span>
<span data-ttu-id="b010b-124">tooconfigure Olá integração do LinkedIn Learning com o Azure AD, é necessário tooadd LinkedIn Learning Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="b010b-124">tooconfigure hello integration of LinkedIn Learning into Azure AD, you need tooadd LinkedIn Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b010b-125">**tooadd Learning LinkedIn da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b010b-125">**tooadd LinkedIn Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b010b-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="b010b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b010b-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b010b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b010b-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="b010b-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="b010b-131">Clique em **adicionar** botão na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="b010b-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="b010b-133">Na caixa de pesquisa de Olá, escreva **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="b010b-133">In hello search box, type **LinkedIn Learning**.</span></span> <span data-ttu-id="b010b-134">No painel de resultados, clique em **LinkedIn Learning** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="b010b-134">From results panel, click **LinkedIn Learning** tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b010b-136">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="b010b-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b010b-137">Nesta secção, configure e teste do Azure AD-início de sessão único com Learning LinkedIn com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b010b-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b010b-138">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá no LinkedIn Learning é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b010b-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="b010b-139">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá no LinkedIn Learning tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b010b-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Learning needs toobe established.</span></span>

<span data-ttu-id="b010b-140">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no LinkedIn Learning.</span><span class="sxs-lookup"><span data-stu-id="b010b-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Learning.</span></span>

<span data-ttu-id="b010b-141">tooconfigure e teste do Azure AD-início de sessão único com o LinkedIn Learning, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="b010b-141">tooconfigure and test Azure AD single sign-on with LinkedIn Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b010b-142">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="b010b-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b010b-143">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b010b-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b010b-144">**[Criar um utilizador de teste de aprendizagem do LinkedIn](#creating-a-linkedin-learning-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b010b-144">**[Creating a LinkedIn Learning test user](#creating-a-linkedin-learning-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="b010b-145">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="b010b-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b010b-146">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="b010b-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b010b-147">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="b010b-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b010b-148">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de aprendizagem do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b010b-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Learning application.</span></span>

<span data-ttu-id="b010b-149">**tooconfigure do Azure AD-início de sessão único com LinkedIn aprendizagem, efetue Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b010b-149">**tooconfigure Azure AD single sign-on with LinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b010b-150">No Olá portal do Azure, no Olá **LinkedIn Learning** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="b010b-150">In hello Azure portal, on hello **LinkedIn Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="b010b-152">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="b010b-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="b010b-154">Numa janela do browser web diferente, inquilino de aprendizagem do LinkedIn tooyour início de sessão como administrador.</span><span class="sxs-lookup"><span data-stu-id="b010b-154">In a different web browser window, sign-on tooyour LinkedIn Learning tenant as an administrator.</span></span>

4. <span data-ttu-id="b010b-155">No **Centro de contas**, clique em **definições globais** em **definições**.</span><span class="sxs-lookup"><span data-stu-id="b010b-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="b010b-156">Além disso, selecione **Learning - predefinição** na lista pendente de Olá.</span><span class="sxs-lookup"><span data-stu-id="b010b-156">Also, select **Learning - Default** from hello dropdown list.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="b010b-158">Clique em **ou clique aqui tooload e copiar campos individuais de formulário de Olá** e copie **Id de entidade** e **Url de acesso de consumidor da asserção (ACS)**</span><span class="sxs-lookup"><span data-stu-id="b010b-158">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="b010b-160">No portal do Azure, em **LinkedIn Learning domínio e os URLs**, efetuar Olá os passos seguintes se quiser tooconfigure SSO no **IdP iniciada** modo</span><span class="sxs-lookup"><span data-stu-id="b010b-160">On Azure portal, under **LinkedIn Learning Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="b010b-162">a.</span><span class="sxs-lookup"><span data-stu-id="b010b-162">a.</span></span> <span data-ttu-id="b010b-163">No Olá **identificador** caixa de texto, introduza Olá **ID de entidade** copiados a partir do LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="b010b-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="b010b-164">b.</span><span class="sxs-lookup"><span data-stu-id="b010b-164">b.</span></span> <span data-ttu-id="b010b-165">No Olá **URL de resposta** caixa de texto, introduza Olá **Url de acesso de consumidor da asserção (ACS)** copiados a partir do LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="b010b-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="b010b-166">Se quiser tooconfigure SSO no **SP iniciada**, em seguida, clique opção de definição de mostrar URL avançado na secção de configuração de Olá e configurar o URL de início de sessão Olá com Olá seguir o padrão de:</span><span class="sxs-lookup"><span data-stu-id="b010b-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign-on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. <span data-ttu-id="b010b-168">A aplicação de aprendizagem do LinkedIn espera asserções de SAML Olá num formato específico, que requer tooadd atributo personalizado mapeamentos tooyour configuração SAML do token de atributos.</span><span class="sxs-lookup"><span data-stu-id="b010b-168">Your LinkedIn Learning application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="b010b-169">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="b010b-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="b010b-170">Olá valor predefinido de **identificador de utilizador** é **user.userprincipalname** mas LinkedIn Learning espera este toobe mapeado com o endereço de correio eletrónico do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="b010b-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Learning expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="b010b-171">Para que pode utilizar **user.mail** atributo da lista de Olá ou utilize o valor do atributo adequado Olá com base na configuração da sua organização.</span><span class="sxs-lookup"><span data-stu-id="b010b-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. <span data-ttu-id="b010b-173">No **atributos de utilizador** secção, clique em **ver e editar todos os outros atributos de utilizador** e defina os atributos de Olá.</span><span class="sxs-lookup"><span data-stu-id="b010b-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="b010b-174">afirmações de quatro tooadd com o nome tem de utilizador de Olá **e-mail**, **departamento**, **firstname**, e **lastname** e valor de Olá é toobe mapeado com **user.mail**, **user.department**, **user.givenname**, e **user.surname** respetivamente</span><span class="sxs-lookup"><span data-stu-id="b010b-174">hello user needs tooadd four claims named **email**, **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="b010b-175">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="b010b-175">Attribute Name</span></span> | <span data-ttu-id="b010b-176">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="b010b-176">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="b010b-177">Correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="b010b-177">email</span></span>| <span data-ttu-id="b010b-178">User.Mail</span><span class="sxs-lookup"><span data-stu-id="b010b-178">user.mail</span></span> |    
    | <span data-ttu-id="b010b-179">Departamento</span><span class="sxs-lookup"><span data-stu-id="b010b-179">department</span></span>| <span data-ttu-id="b010b-180">User.Department</span><span class="sxs-lookup"><span data-stu-id="b010b-180">user.department</span></span> |
    | <span data-ttu-id="b010b-181">nome próprio</span><span class="sxs-lookup"><span data-stu-id="b010b-181">firstname</span></span>| <span data-ttu-id="b010b-182">User.givenName</span><span class="sxs-lookup"><span data-stu-id="b010b-182">user.givenname</span></span> |
    | <span data-ttu-id="b010b-183">Apelido</span><span class="sxs-lookup"><span data-stu-id="b010b-183">lastname</span></span>| <span data-ttu-id="b010b-184">User.Surname</span><span class="sxs-lookup"><span data-stu-id="b010b-184">user.surname</span></span> |
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    <span data-ttu-id="b010b-186">a.</span><span class="sxs-lookup"><span data-stu-id="b010b-186">a.</span></span> <span data-ttu-id="b010b-187">Clique em **adicionar atributo** caixa de diálogo do tooopen Olá atributo.</span><span class="sxs-lookup"><span data-stu-id="b010b-187">Click **Add Attribute** tooopen hello attribute dialog.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="b010b-190">b.</span><span class="sxs-lookup"><span data-stu-id="b010b-190">b.</span></span> <span data-ttu-id="b010b-191">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="b010b-191">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b010b-192">c.</span><span class="sxs-lookup"><span data-stu-id="b010b-192">c.</span></span> <span data-ttu-id="b010b-193">De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="b010b-193">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b010b-194">d.</span><span class="sxs-lookup"><span data-stu-id="b010b-194">d.</span></span> <span data-ttu-id="b010b-195">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="b010b-195">Click **Ok**</span></span>

10. <span data-ttu-id="b010b-196">Efetuar Olá os seguintes passos no Olá **nome** atributo -</span><span class="sxs-lookup"><span data-stu-id="b010b-196">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="b010b-197">a.</span><span class="sxs-lookup"><span data-stu-id="b010b-197">a.</span></span> <span data-ttu-id="b010b-198">Clique em Olá do Olá atributo tooopen **Editar atributo** janela.</span><span class="sxs-lookup"><span data-stu-id="b010b-198">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    <span data-ttu-id="b010b-200">b.</span><span class="sxs-lookup"><span data-stu-id="b010b-200">b.</span></span> <span data-ttu-id="b010b-201">Eliminar o valor do URL de Olá da Olá **espaço de nomes**.</span><span class="sxs-lookup"><span data-stu-id="b010b-201">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="b010b-202">c.</span><span class="sxs-lookup"><span data-stu-id="b010b-202">c.</span></span> <span data-ttu-id="b010b-203">Clique em **Ok** definição de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="b010b-203">Click **Ok** toosave hello setting.</span></span>

11. <span data-ttu-id="b010b-204">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="b010b-204">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. <span data-ttu-id="b010b-206">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b010b-206">Click **Save**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. <span data-ttu-id="b010b-208">Aceda demasiado**definições de administrador do LinkedIn** secção.</span><span class="sxs-lookup"><span data-stu-id="b010b-208">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="b010b-209">Carregar ficheiro XML de Olá que transferiu a partir do portal do Azure de Olá clicando a opção de ficheiro XML de carregar Olá.</span><span class="sxs-lookup"><span data-stu-id="b010b-209">Upload hello XML file you downloaded from hello Azure portal by clicking hello Upload XML file option.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. <span data-ttu-id="b010b-211">Clique em **no** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="b010b-211">Click **On** tooenable SSO.</span></span> <span data-ttu-id="b010b-212">Estado SSO é alterado de **não ligado** demasiado**ligado**</span><span class="sxs-lookup"><span data-stu-id="b010b-212">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b010b-214">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b010b-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="b010b-215">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b010b-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="b010b-217">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b010b-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b010b-218">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="b010b-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b010b-220">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="b010b-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b010b-222">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="b010b-222">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b010b-224">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="b010b-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b010b-226">a.</span><span class="sxs-lookup"><span data-stu-id="b010b-226">a.</span></span> <span data-ttu-id="b010b-227">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b010b-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b010b-228">b.</span><span class="sxs-lookup"><span data-stu-id="b010b-228">b.</span></span> <span data-ttu-id="b010b-229">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b010b-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b010b-230">c.</span><span class="sxs-lookup"><span data-stu-id="b010b-230">c.</span></span> <span data-ttu-id="b010b-231">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="b010b-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b010b-232">d.</span><span class="sxs-lookup"><span data-stu-id="b010b-232">d.</span></span> <span data-ttu-id="b010b-233">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b010b-233">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-learning-test-user"></a><span data-ttu-id="b010b-234">Criar um utilizador de teste de aprendizagem do LinkedIn</span><span class="sxs-lookup"><span data-stu-id="b010b-234">Creating a LinkedIn Learning test user</span></span>

<span data-ttu-id="b010b-235">Suporta a aplicação de aprendizagem ligado.</span><span class="sxs-lookup"><span data-stu-id="b010b-235">Linked Learning Application supports.</span></span> <span data-ttu-id="b010b-236">Apenas no aprovisionamento de utilizadores de tempo após a autenticação de utilizadores são criados e na aplicação Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b010b-236">Just in time user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="b010b-237">Na página de definições de administrador Olá no comutador de portal Olá flip Olá LinkedIn Learning **automaticamente atribuir licenças** tooactive tooenable apenas no tempo de aprovisionamento e isto também irão atribuir um utilizador de toohello de licença.</span><span class="sxs-lookup"><span data-stu-id="b010b-237">On hello admin settings page on hello LinkedIn Learning portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>
   
   ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b010b-239">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b010b-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b010b-240">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooLinkedIn de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="b010b-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Learning.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="b010b-242">**tooassign Britta Simon tooLinkedIn de aprendizagem, efetue Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="b010b-242">**tooassign Britta Simon tooLinkedIn Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b010b-243">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="b010b-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="b010b-245">Na lista de aplicações de Olá, selecione **LinkedIn Learning**.</span><span class="sxs-lookup"><span data-stu-id="b010b-245">In hello applications list, select **LinkedIn Learning**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. <span data-ttu-id="b010b-247">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b010b-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="b010b-249">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="b010b-249">Click **Add** button.</span></span> <span data-ttu-id="b010b-250">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b010b-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="b010b-252">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="b010b-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b010b-253">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b010b-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b010b-254">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b010b-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b010b-255">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="b010b-255">Testing single sign-on</span></span>

<span data-ttu-id="b010b-256">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="b010b-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b010b-257">Ao clicar em mosaico de aprendizagem do LinkedIn Olá no Olá painel de acesso, pode ser obtido a página Olá o início de sessão do Azure e no após o início de sessão com êxito, pode ser obtido na sua aplicação de aprendizagem do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="b010b-257">When you click hello LinkedIn Learning tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b010b-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b010b-258">Additional resources</span></span>

* [<span data-ttu-id="b010b-259">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b010b-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b010b-260">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b010b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png