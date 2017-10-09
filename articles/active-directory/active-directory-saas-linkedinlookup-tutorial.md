---
title: "Tutorial: Integração do Azure Active Directory com LinkedIn pesquisa | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e LinkedIn pesquisa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a><span data-ttu-id="996e5-103">Tutorial: Integração do Azure Active Directory com LinkedIn pesquisa</span><span class="sxs-lookup"><span data-stu-id="996e5-103">Tutorial: Azure Active Directory integration with LinkedIn Lookup</span></span>

<span data-ttu-id="996e5-104">Neste tutorial, saiba como toointegrate LinkedIn pesquisa no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="996e5-104">In this tutorial, you learn how toointegrate LinkedIn Lookup with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="996e5-105">A integração de pesquisa de LinkedIn com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="996e5-105">Integrating LinkedIn Lookup with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="996e5-106">Pode controlar no Azure AD que tenha acesso tooLinkedIn pesquisa</span><span class="sxs-lookup"><span data-stu-id="996e5-106">You can control in Azure AD who has access tooLinkedIn Lookup</span></span>
- <span data-ttu-id="996e5-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooLinkedIn pesquisa (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="996e5-107">You can enable your users tooautomatically get signed-on tooLinkedIn Lookup (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="996e5-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="996e5-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="996e5-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="996e5-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="996e5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="996e5-110">Prerequisites</span></span>

<span data-ttu-id="996e5-111">integração do Azure AD com LinkedIn pesquisa tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="996e5-111">tooconfigure Azure AD integration with LinkedIn Lookup, you need hello following items:</span></span>

- <span data-ttu-id="996e5-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="996e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="996e5-113">Um pesquisa de LinkedIn início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="996e5-113">An LinkedIn Lookup single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="996e5-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="996e5-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="996e5-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="996e5-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="996e5-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="996e5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="996e5-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="996e5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="996e5-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="996e5-118">Scenario description</span></span>
<span data-ttu-id="996e5-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="996e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="996e5-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="996e5-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="996e5-121">A adição de pesquisa do LinkedIn da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="996e5-121">Adding LinkedIn Lookup from hello gallery</span></span>
2. <span data-ttu-id="996e5-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="996e5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-lookup-from-hello-gallery"></a><span data-ttu-id="996e5-123">A adição de pesquisa do LinkedIn da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="996e5-123">Adding LinkedIn Lookup from hello gallery</span></span>
<span data-ttu-id="996e5-124">tooconfigure Olá integração de pesquisa de LinkedIn com o Azure AD, é necessário tooadd LinkedIn pesquisa Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="996e5-124">tooconfigure hello integration of LinkedIn Lookup into Azure AD, you need tooadd LinkedIn Lookup from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="996e5-125">**tooadd pesquisa LinkedIn da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="996e5-125">**tooadd LinkedIn Lookup from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="996e5-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="996e5-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="996e5-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="996e5-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="996e5-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="996e5-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="996e5-131">Clique em **nova aplicação** botão na parte superior de Olá da nova aplicação tooadd da caixa de diálogo de Olá.</span><span class="sxs-lookup"><span data-stu-id="996e5-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="996e5-133">Na caixa de pesquisa de Olá, escreva **LinkedIn pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="996e5-133">In hello search box, type **LinkedIn Lookup**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. <span data-ttu-id="996e5-135">No painel de resultados de Olá, selecione **LinkedIn pesquisa**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="996e5-135">In hello results panel, select **LinkedIn Lookup**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="996e5-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="996e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="996e5-138">Nesta secção, configure e teste do Azure AD-início de sessão único com LinkedIn pesquisa com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="996e5-138">In this section, you configure and test Azure AD single sign-on with LinkedIn Lookup based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="996e5-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na pesquisa do LinkedIn é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="996e5-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Lookup is tooa user in Azure AD.</span></span> <span data-ttu-id="996e5-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na pesquisa do LinkedIn tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="996e5-140">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Lookup needs toobe established.</span></span>

<span data-ttu-id="996e5-141">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** na pesquisa do LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="996e5-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Lookup.</span></span>

<span data-ttu-id="996e5-142">tooconfigure e teste do Azure AD-início de sessão único com LinkedIn pesquisa, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="996e5-142">tooconfigure and test Azure AD single sign-on with LinkedIn Lookup, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="996e5-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="996e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="996e5-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="996e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="996e5-145">**[Criar um utilizador de teste de pesquisa de LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave um homólogo de Britta Simon na pesquisa de LinkedIn que é a representação de toohello ligado do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="996e5-145">**[Creating an LinkedIn Lookup test user](#creating-an-linkedin-lookup-test-user)** - toohave a counterpart of Britta Simon in LinkedIn Lookup that is linked toohello Azure AD representation.</span></span>
4. <span data-ttu-id="996e5-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="996e5-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="996e5-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="996e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="996e5-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="996e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="996e5-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de pesquisa de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="996e5-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LinkedIn Lookup application.</span></span>

<span data-ttu-id="996e5-150">**tooconfigure do Azure AD-início de sessão único com LinkedIn pesquisa, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="996e5-150">**tooconfigure Azure AD single sign-on with LinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="996e5-151">No Olá portal do Azure, no Olá **LinkedIn pesquisa** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="996e5-151">In hello Azure portal, on hello **LinkedIn Lookup** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="996e5-153">No Olá **de sessão único-** caixa de diálogo, em **modo** selecione **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="996e5-153">On hello **Single sign-on** dialog, in **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. <span data-ttu-id="996e5-155">Numa janela do browser web diferente, início de sessão tooyour **LinkedIn pesquisa** Web site como um administrador.</span><span class="sxs-lookup"><span data-stu-id="996e5-155">In a different web browser window, sign-on tooyour **LinkedIn Lookup** website as an administrator.</span></span>

4. <span data-ttu-id="996e5-156">No **Centro de contas**, clique em **definições globais** em **definições**.</span><span class="sxs-lookup"><span data-stu-id="996e5-156">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="996e5-157">Além disso, selecione **pesquisa** na lista pendente de Olá.</span><span class="sxs-lookup"><span data-stu-id="996e5-157">Also, select **Lookup** from hello dropdown list.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. <span data-ttu-id="996e5-159">Clique em **ou clique aqui tooload e copiar campos individuais de formulário de Olá** e copie **Id de entidade** e **Url de acesso de consumidor da asserção (ACS)**</span><span class="sxs-lookup"><span data-stu-id="996e5-159">Click **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. <span data-ttu-id="996e5-161">No portal do Azure, em **LinkedIn pesquisa de domínio e os URLs** secção, execute os passos seguintes se quiser aplicação Olá tooconfigure de Olá **IDP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="996e5-161">On Azure portal, under **LinkedIn Lookup Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    <span data-ttu-id="996e5-163">a.</span><span class="sxs-lookup"><span data-stu-id="996e5-163">a.</span></span> <span data-ttu-id="996e5-164">No Olá **identificador** caixa de texto, introduza Olá **ID de entidade** copiados a partir do LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="996e5-164">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="996e5-165">b.</span><span class="sxs-lookup"><span data-stu-id="996e5-165">b.</span></span> <span data-ttu-id="996e5-166">No Olá **URL de resposta** caixa de texto, introduza Olá **Url de acesso de consumidor da asserção (ACS)** copiados a partir do LinkedIn Portal</span><span class="sxs-lookup"><span data-stu-id="996e5-166">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="996e5-167">Verifique **Mostrar avançadas definições de URL**, se desejar aplicação Olá tooconfigure **SP** iniciada modo:</span><span class="sxs-lookup"><span data-stu-id="996e5-167">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    <span data-ttu-id="996e5-169">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span><span class="sxs-lookup"><span data-stu-id="996e5-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="996e5-170">Não se trata de valor real.</span><span class="sxs-lookup"><span data-stu-id="996e5-170">This is not real value.</span></span> <span data-ttu-id="996e5-171">utilizador Olá tem tooupdate estes valores com Olá real URL de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="996e5-171">hello user has tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="996e5-172">Contacte [equipa de suporte de cliente de pesquisa do LinkedIn](https://business.LinkedIn.com/lookup) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="996e5-172">Contact [LinkedIn Lookup Client support team](https://business.LinkedIn.com/lookup) tooget this value.</span></span>

8. <span data-ttu-id="996e5-173">O **LinkedIn pesquisa** aplicação espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="996e5-173">Your **LinkedIn Lookup** application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="996e5-174">utilizador Olá tem a configuração de atributos de tokens de SAML mapeamentos toohello tooadd atributo personalizado.</span><span class="sxs-lookup"><span data-stu-id="996e5-174">hello user has tooadd custom attribute mappings toohello SAML token attributes configuration.</span></span> <span data-ttu-id="996e5-175">Olá seguinte captura de ecrã mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="996e5-175">hello following screenshot shows an example.</span></span> <span data-ttu-id="996e5-176">Olá valor predefinido de **identificador de utilizador** é **user.userprincipalname** mas LinkedIn pesquisa espera este toobe mapeado com o endereço de correio eletrónico do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="996e5-176">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Lookup expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="996e5-177">Pode utilizar **user.mail** atributo da lista de Olá ou utilize o valor do atributo adequado Olá com base na configuração da sua organização.</span><span class="sxs-lookup"><span data-stu-id="996e5-177">You can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. <span data-ttu-id="996e5-179">No **atributos de utilizador** secção, clique em **ver e editar todos os outros atributos de utilizador** e defina os atributos de Olá.</span><span class="sxs-lookup"><span data-stu-id="996e5-179">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="996e5-180">afirmações de quatro tooadd com o nome tem de utilizador de Olá **e-mail**, **departamento**, **firstname**, e **lastname** e valor de Olá é toobe mapeado com **user.mail**, **user.department**, **user.givenname**, e **user.surname** respetivamente</span><span class="sxs-lookup"><span data-stu-id="996e5-180">hello user needs tooadd four claims named **email**,  **department**, **firstname**, and **lastname** and hello value is toobe mapped with **user.mail**, **user.department**, **user.givenname**, and **user.surname** respectively</span></span>

    | <span data-ttu-id="996e5-181">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="996e5-181">Attribute Name</span></span> | <span data-ttu-id="996e5-182">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="996e5-182">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="996e5-183">Correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="996e5-183">email</span></span>| <span data-ttu-id="996e5-184">User.Mail</span><span class="sxs-lookup"><span data-stu-id="996e5-184">user.mail</span></span> |    
    | <span data-ttu-id="996e5-185">Departamento</span><span class="sxs-lookup"><span data-stu-id="996e5-185">department</span></span>| <span data-ttu-id="996e5-186">User.Department</span><span class="sxs-lookup"><span data-stu-id="996e5-186">user.department</span></span> |
    | <span data-ttu-id="996e5-187">nome próprio</span><span class="sxs-lookup"><span data-stu-id="996e5-187">firstname</span></span>| <span data-ttu-id="996e5-188">User.givenName</span><span class="sxs-lookup"><span data-stu-id="996e5-188">user.givenname</span></span> |
    | <span data-ttu-id="996e5-189">Apelido</span><span class="sxs-lookup"><span data-stu-id="996e5-189">lastname</span></span>| <span data-ttu-id="996e5-190">User.Surname</span><span class="sxs-lookup"><span data-stu-id="996e5-190">user.surname</span></span> |

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    <span data-ttu-id="996e5-192">a.</span><span class="sxs-lookup"><span data-stu-id="996e5-192">a.</span></span> <span data-ttu-id="996e5-193">Clique em **adicionar atributo** tooopen Olá **adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="996e5-193">Click **Add Attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    <span data-ttu-id="996e5-196">b.</span><span class="sxs-lookup"><span data-stu-id="996e5-196">b.</span></span> <span data-ttu-id="996e5-197">No Olá **nome** caixa de texto, nome de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="996e5-197">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="996e5-198">c.</span><span class="sxs-lookup"><span data-stu-id="996e5-198">c.</span></span> <span data-ttu-id="996e5-199">De Olá **valor** lista, o valor de atributo do tipo Olá mostrado para essa linha.</span><span class="sxs-lookup"><span data-stu-id="996e5-199">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="996e5-200">d.</span><span class="sxs-lookup"><span data-stu-id="996e5-200">d.</span></span> <span data-ttu-id="996e5-201">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="996e5-201">Click **Ok**</span></span>

10. <span data-ttu-id="996e5-202">Efetuar Olá os seguintes passos no Olá **nome** atributo -</span><span class="sxs-lookup"><span data-stu-id="996e5-202">Perform hello following steps on hello **name** attribute-</span></span>

    <span data-ttu-id="996e5-203">a.</span><span class="sxs-lookup"><span data-stu-id="996e5-203">a.</span></span> <span data-ttu-id="996e5-204">Clique em Olá do Olá atributo tooopen **Editar atributo** janela.</span><span class="sxs-lookup"><span data-stu-id="996e5-204">Click on hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    <span data-ttu-id="996e5-206">b.</span><span class="sxs-lookup"><span data-stu-id="996e5-206">b.</span></span> <span data-ttu-id="996e5-207">Eliminar o valor do URL de Olá da Olá **espaço de nomes**.</span><span class="sxs-lookup"><span data-stu-id="996e5-207">Delete hello URL value from hello **namespace**.</span></span>
    
    <span data-ttu-id="996e5-208">c.</span><span class="sxs-lookup"><span data-stu-id="996e5-208">c.</span></span> <span data-ttu-id="996e5-209">Clique em **Ok** definição de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="996e5-209">Click **Ok** toosave hello setting.</span></span>

10. <span data-ttu-id="996e5-210">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro XML de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="996e5-210">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. <span data-ttu-id="996e5-212">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="996e5-212">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="996e5-214">Aceda demasiado**definições de administrador do LinkedIn** secção.</span><span class="sxs-lookup"><span data-stu-id="996e5-214">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="996e5-215">Ficheiro XML Olá de carregamento transferiu a partir do portal do Azure de Olá clicando Olá **ficheiro XML de carregar** opção.</span><span class="sxs-lookup"><span data-stu-id="996e5-215">Upload hello XML file you downloaded from hello Azure portal by clicking hello **Upload XML file** option.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. <span data-ttu-id="996e5-217">Clique em **no** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="996e5-217">Click **On** tooenable SSO.</span></span> <span data-ttu-id="996e5-218">Estado SSO é alterado de **não ligado** demasiado**ligado**</span><span class="sxs-lookup"><span data-stu-id="996e5-218">SSO status changes from **Not Connected** too**Connected**</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> <span data-ttu-id="996e5-220">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="996e5-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="996e5-221">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="996e5-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="996e5-222">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="996e5-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="996e5-223">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="996e5-223">Creating an Azure AD test user</span></span>
<span data-ttu-id="996e5-224">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="996e5-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="996e5-226">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="996e5-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="996e5-227">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="996e5-227">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="996e5-229">Aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="996e5-229">Go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="996e5-231">Clique em **adicionar** tooopen Olá **utilizador** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="996e5-231">Click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="996e5-233">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="996e5-233">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="996e5-235">a.</span><span class="sxs-lookup"><span data-stu-id="996e5-235">a.</span></span> <span data-ttu-id="996e5-236">No Olá **nome** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="996e5-236">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="996e5-237">b.</span><span class="sxs-lookup"><span data-stu-id="996e5-237">b.</span></span> <span data-ttu-id="996e5-238">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="996e5-238">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="996e5-239">c.</span><span class="sxs-lookup"><span data-stu-id="996e5-239">c.</span></span> <span data-ttu-id="996e5-240">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="996e5-240">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="996e5-241">d.</span><span class="sxs-lookup"><span data-stu-id="996e5-241">d.</span></span> <span data-ttu-id="996e5-242">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="996e5-242">Click **Create**.</span></span>
 
### <a name="creating-an-linkedin-lookup-test-user"></a><span data-ttu-id="996e5-243">Criar um utilizador de teste de pesquisa de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="996e5-243">Creating an LinkedIn Lookup test user</span></span>

<span data-ttu-id="996e5-244">Aplicação de pesquisa ligado suporta apenas no tempo (JIT) de aprovisionamento de utilizador e de utilizadores de autenticação são criados na aplicação Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="996e5-244">Linked Lookup Application supports Just in Time (JIT) user provisioning and after authentication users are created in hello application automatically.</span></span> <span data-ttu-id="996e5-245">Ativar **automaticamente atribuir licenças** tooassign um utilizador de toohello de licença.</span><span class="sxs-lookup"><span data-stu-id="996e5-245">Activate **Automatically assign licenses** tooassign a license toohello user.</span></span>
   
   ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="996e5-247">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="996e5-247">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="996e5-248">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooLinkedIn pesquisa.</span><span class="sxs-lookup"><span data-stu-id="996e5-248">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLinkedIn Lookup.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="996e5-250">**tooassign Britta Simon tooLinkedIn pesquisa, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="996e5-250">**tooassign Britta Simon tooLinkedIn Lookup, perform hello following steps:**</span></span>

1. <span data-ttu-id="996e5-251">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="996e5-251">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="996e5-253">Na lista de aplicações de Olá, selecione **LinkedIn pesquisa**.</span><span class="sxs-lookup"><span data-stu-id="996e5-253">In hello applications list, select **LinkedIn Lookup**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. <span data-ttu-id="996e5-255">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="996e5-255">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="996e5-257">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="996e5-257">Click **Add** button.</span></span> <span data-ttu-id="996e5-258">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="996e5-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="996e5-260">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="996e5-260">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="996e5-261">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="996e5-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="996e5-262">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="996e5-262">Click **Assign** button on **Add Assignment** dialog.</span></span>

    
### <a name="testing-single-sign-on"></a><span data-ttu-id="996e5-263">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="996e5-263">Testing single sign-on</span></span>

<span data-ttu-id="996e5-264">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="996e5-264">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="996e5-265">Ao clicar Olá LinkedIn pesquisa na peça de mosaico Olá painel de acesso, deve ser página tooOrganizational redirecionada onde tiver tooprovide detalhes da sua conta LinkedIn pessoais.</span><span class="sxs-lookup"><span data-stu-id="996e5-265">When you click hello LinkedIn Lookup tile in hello Access Panel, you should be redirected tooOrganizational page where you have tooprovide your personal LinkedIn account details.</span></span> <span data-ttu-id="996e5-266">-Liga a sua conta pessoal com a sua conta de negócio LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="996e5-266">It links your personal account with your LinkedIn business account.</span></span> 

<span data-ttu-id="996e5-267">Para mais informações sobre o painel de acesso, consulte [introdução ao painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="996e5-267">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="996e5-268">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="996e5-268">Additional resources</span></span>

* [<span data-ttu-id="996e5-269">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="996e5-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="996e5-270">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="996e5-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

