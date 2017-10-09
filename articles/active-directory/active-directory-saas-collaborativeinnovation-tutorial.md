---
title: "Tutorial: Integração do Azure Active Directory com inovação colaboração | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e inovação colaboração."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="856d4-103">Tutorial: Integração do Azure Active Directory com inovação colaboração</span><span class="sxs-lookup"><span data-stu-id="856d4-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="856d4-104">Neste tutorial, saiba como toointegrate inovação colaboração com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="856d4-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="856d4-105">Integrar inovação colaboração com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="856d4-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="856d4-106">Pode controlar no Azure AD que tenha acesso tooCollaborative inovação</span><span class="sxs-lookup"><span data-stu-id="856d4-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="856d4-107">Pode ativar a sua utilizadores tooautomatically get com sessão iniciada tooCollaborative inovação (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="856d4-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="856d4-108">Pode gerir as contas numa localização central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="856d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="856d4-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="856d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="856d4-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="856d4-110">Prerequisites</span></span>

<span data-ttu-id="856d4-111">integração do Azure AD com inovação colaboração tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="856d4-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="856d4-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="856d4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="856d4-113">Um colaboração inovação início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="856d4-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="856d4-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="856d4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="856d4-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="856d4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="856d4-116">Não utilize o seu ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="856d4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="856d4-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="856d4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="856d4-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="856d4-118">Scenario description</span></span>
<span data-ttu-id="856d4-119">Neste tutorial, teste do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="856d4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="856d4-120">cenário de Olá descrito neste tutorial consiste em dois blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="856d4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="856d4-121">A adição de colaboração inovação de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="856d4-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="856d4-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="856d4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="856d4-123">A adição de colaboração inovação de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="856d4-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="856d4-124">tooconfigure Olá integração de inovação colaboração com o Azure AD, é necessário tooadd inovação colaboração Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="856d4-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="856d4-125">**tooadd inovação colaboração da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="856d4-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="856d4-126">No Olá  **[portal do Azure](https://portal.azure.com)**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="856d4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="856d4-128">Navegue demasiado**aplicações empresariais**.</span><span class="sxs-lookup"><span data-stu-id="856d4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="856d4-129">Em seguida, avance demasiado**todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="856d4-129">Then go too**All applications**.</span></span>

    ![Aplicações][2]
    
3. <span data-ttu-id="856d4-131">tooadd nova aplicação, clique em **nova aplicação** botão Olá parte superior da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="856d4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicações][3]

4. <span data-ttu-id="856d4-133">Na caixa de pesquisa de Olá, escreva **inovação colaboração**.</span><span class="sxs-lookup"><span data-stu-id="856d4-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="856d4-135">No painel de resultados de Olá, selecione **inovação colaboração**e, em seguida, clique em **adicionar** botão a aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="856d4-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="856d4-137">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="856d4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="856d4-138">Nesta secção, configure e teste do Azure AD-início de sessão único com inovação colaboração com base num utilizador de teste chamado "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="856d4-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="856d4-139">Para único início de sessão toowork, do Azure AD tem tooknow qual o utilizador que homólogo Olá na inovação colaboração é tooa utilizador no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="856d4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="856d4-140">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados do Olá na inovação colaboração tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="856d4-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="856d4-141">Na inovação colaboração, atribua o valor de Olá da Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** relação de ligação de Olá tooestablish.</span><span class="sxs-lookup"><span data-stu-id="856d4-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="856d4-142">tooconfigure e teste do Azure AD-início de sessão único com inovação colaboração, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="856d4-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="856d4-143">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="856d4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="856d4-144">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="856d4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="856d4-145">**[Criar um utilizador de teste de colaboração inovação](#creating-a-collaborative-innovation-test-user)**  -toohave um homólogo de Britta Simon na inovação colaboração que é toohello ligado do Azure AD de representação do utilizador.</span><span class="sxs-lookup"><span data-stu-id="856d4-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="856d4-146">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="856d4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="856d4-147">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="856d4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="856d4-148">Configurar o Azure AD-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="856d4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="856d4-149">Nesta secção, pode ativar do Azure AD-início de sessão único em Olá portal do Azure e configurar o início de sessão único na sua aplicação de colaboração inovação.</span><span class="sxs-lookup"><span data-stu-id="856d4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="856d4-150">**tooconfigure do Azure AD-início de sessão único com inovação colaboração, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="856d4-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="856d4-151">No Olá portal do Azure, no Olá **inovação colaboração** página de integração de aplicações, clique em **de sessão único-**.</span><span class="sxs-lookup"><span data-stu-id="856d4-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Configurar o início de sessão único][4]

2. <span data-ttu-id="856d4-153">No Olá **de sessão único-** caixa de diálogo, selecione **modo** como **baseados em SAML início de sessão** tooenable-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="856d4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar o início de sessão único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="856d4-155">No Olá **colaboração inovação domínio e os URLs** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="856d4-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="856d4-157">a.</span><span class="sxs-lookup"><span data-stu-id="856d4-157">a.</span></span> <span data-ttu-id="856d4-158">No Olá **URL de início de sessão** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="856d4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="856d4-159">b.</span><span class="sxs-lookup"><span data-stu-id="856d4-159">b.</span></span> <span data-ttu-id="856d4-160">No Olá **identificador** caixa de texto, escreva um URL Olá seguir o padrão de utilização:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="856d4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="856d4-161">Estes valores não estiverem reais.</span><span class="sxs-lookup"><span data-stu-id="856d4-161">These values are not real.</span></span> <span data-ttu-id="856d4-162">Atualizar estes valores com Olá real URL de início de sessão e o identificador.</span><span class="sxs-lookup"><span data-stu-id="856d4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="856d4-163">Contacte [equipa de suporte de colaboração inovação cliente](https://www.unilever.com/contact/) tooget estes valores.</span><span class="sxs-lookup"><span data-stu-id="856d4-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="856d4-164">Aplicação de inovação colaboração espera asserções de SAML Olá num formato específico.</span><span class="sxs-lookup"><span data-stu-id="856d4-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="856d4-165">Configure Olá seguintes afirmações para esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="856d4-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="856d4-166">Pode gerir os valores de Olá destes atributos a partir de Olá "**atributos de utilizador**" secção na página de integração de aplicações.</span><span class="sxs-lookup"><span data-stu-id="856d4-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="856d4-167">Olá seguinte captura de ecrã mostra um exemplo para este.</span><span class="sxs-lookup"><span data-stu-id="856d4-167">hello following screenshot shows an example for this.</span></span>
    
    ![Configurar o início de sessão único](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="856d4-169">Clique em **ver e editar todos os outros atributos de utilizador** caixa de verificação no Olá **atributos de utilizador** secção atributos de Olá tooexpand.</span><span class="sxs-lookup"><span data-stu-id="856d4-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="856d4-170">Efetuar Olá os seguintes passos em cada um dos atributos de Olá apresentado-</span><span class="sxs-lookup"><span data-stu-id="856d4-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="856d4-171">Nome do atributo</span><span class="sxs-lookup"><span data-stu-id="856d4-171">Attribute Name</span></span> | <span data-ttu-id="856d4-172">Valor do atributo</span><span class="sxs-lookup"><span data-stu-id="856d4-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="856d4-173">givenName</span><span class="sxs-lookup"><span data-stu-id="856d4-173">givenname</span></span> | <span data-ttu-id="856d4-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="856d4-174">user.givenname</span></span> |
    | <span data-ttu-id="856d4-175">Apelido</span><span class="sxs-lookup"><span data-stu-id="856d4-175">surname</span></span> | <span data-ttu-id="856d4-176">User.Surname</span><span class="sxs-lookup"><span data-stu-id="856d4-176">user.surname</span></span> |
    | <span data-ttu-id="856d4-177">endereço de correio eletrónico</span><span class="sxs-lookup"><span data-stu-id="856d4-177">emailaddress</span></span> | <span data-ttu-id="856d4-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="856d4-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="856d4-179">nome</span><span class="sxs-lookup"><span data-stu-id="856d4-179">name</span></span> | <span data-ttu-id="856d4-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="856d4-180">user.userprincipalname</span></span> |

    <span data-ttu-id="856d4-181">a.</span><span class="sxs-lookup"><span data-stu-id="856d4-181">a.</span></span> <span data-ttu-id="856d4-182">Clique em Olá do Olá atributo tooopen **Editar atributo** janela.</span><span class="sxs-lookup"><span data-stu-id="856d4-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="856d4-184">b.</span><span class="sxs-lookup"><span data-stu-id="856d4-184">b.</span></span> <span data-ttu-id="856d4-185">Eliminar o valor do URL de Olá da Olá **espaço de nomes**.</span><span class="sxs-lookup"><span data-stu-id="856d4-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="856d4-186">c.</span><span class="sxs-lookup"><span data-stu-id="856d4-186">c.</span></span> <span data-ttu-id="856d4-187">Clique em **Ok** definição de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="856d4-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="856d4-188">No Olá **certificado de assinatura de SAML** secção, clique em **XML de metadados** e, em seguida, guarde o ficheiro de metadados de Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="856d4-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="856d4-190">Clique em **guardar** botão.</span><span class="sxs-lookup"><span data-stu-id="856d4-190">Click **Save** button.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="856d4-192">tooconfigure-início de sessão único em **inovação colaboração** lado, terá de Olá toosend transferido **XML de metadados** demasiado[equipa de suporte de colaboração inovação](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="856d4-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="856d4-193">Configuram Olá de toohave esta definição corretamente em ambos os lados de ligação de SAML SSO.</span><span class="sxs-lookup"><span data-stu-id="856d4-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="856d4-194">Pode agora ler uma versão concisa destas instruções dentro Olá [portal do Azure](https://portal.azure.com), enquanto estiver a configurar aplicação Olá!</span><span class="sxs-lookup"><span data-stu-id="856d4-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="856d4-195">Depois de adicionar esta aplicação de Olá **do Active Directory > aplicações da empresa** secção, basta clicar em Olá **Single Sign-On** Olá separador e de acesso incorporados documentação através de Olá  **Configuração** secção na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="856d4-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="856d4-196">Pode ler mais sobre a funcionalidade de documentação incorporados de Olá aqui: [do Azure AD incorporado documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="856d4-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="856d4-197">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="856d4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="856d4-198">o objetivo desta secção Olá é toocreate um utilizador de teste Olá chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="856d4-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar utilizador do Azure AD][100]

<span data-ttu-id="856d4-200">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="856d4-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="856d4-201">No Olá **portal do Azure**, no painel de navegação esquerdo de Olá, clique em **do Azure Active Directory** ícone.</span><span class="sxs-lookup"><span data-stu-id="856d4-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="856d4-203">lista de Olá toodisplay de utilizadores, aceda demasiado**utilizadores e grupos** e clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="856d4-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="856d4-205">Olá tooopen **utilizador** caixa de diálogo, clique em **adicionar** na parte superior de Olá da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="856d4-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="856d4-207">No Olá **utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="856d4-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criar um utilizador de teste do Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="856d4-209">a.</span><span class="sxs-lookup"><span data-stu-id="856d4-209">a.</span></span> <span data-ttu-id="856d4-210">No Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="856d4-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="856d4-211">b.</span><span class="sxs-lookup"><span data-stu-id="856d4-211">b.</span></span> <span data-ttu-id="856d4-212">No Olá **nome de utilizador** caixa de texto, Olá tipo **endereço de correio eletrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="856d4-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="856d4-213">c.</span><span class="sxs-lookup"><span data-stu-id="856d4-213">c.</span></span> <span data-ttu-id="856d4-214">Selecione **mostrar palavra-passe** e anote o valor Olá Olá **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="856d4-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="856d4-215">d.</span><span class="sxs-lookup"><span data-stu-id="856d4-215">d.</span></span> <span data-ttu-id="856d4-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="856d4-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="856d4-217">Criar um utilizador de teste inovação colaboração</span><span class="sxs-lookup"><span data-stu-id="856d4-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="856d4-218">tooenable do Azure AD os utilizadores toolog no tooCollaborative inovação, estes têm de ser aprovisionados para colaboração inovação.</span><span class="sxs-lookup"><span data-stu-id="856d4-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="856d4-219">Em caso desta aplicação de aprovisionamento é automático como aplicação Olá apenas suporta o aprovisionamento de utilizadores de tempo.</span><span class="sxs-lookup"><span data-stu-id="856d4-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="856d4-220">Por isso, não há tooperform sem necessidade de quaisquer passos aqui.</span><span class="sxs-lookup"><span data-stu-id="856d4-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="856d4-221">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="856d4-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="856d4-222">Nesta secção, vai ativar Britta Simon toouse do Azure-início de sessão único, concedendo acesso tooCollaborative inovação.</span><span class="sxs-lookup"><span data-stu-id="856d4-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![Atribua o utilizador][200] 

<span data-ttu-id="856d4-224">**tooassign Britta Simon tooCollaborative inovação, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="856d4-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="856d4-225">No portal do Azure Olá, abra a vista de aplicações de Olá e, em seguida, navegue toohello vista de diretório e aceda demasiado**aplicações empresariais** , em seguida, clique em **todas as aplicações**.</span><span class="sxs-lookup"><span data-stu-id="856d4-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribua o utilizador][201] 

2. <span data-ttu-id="856d4-227">Na lista de aplicações de Olá, selecione **inovação colaboração**.</span><span class="sxs-lookup"><span data-stu-id="856d4-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![Configurar o início de sessão único](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="856d4-229">No menu de Olá Olá esquerda, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="856d4-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribua o utilizador][202] 

4. <span data-ttu-id="856d4-231">Clique em **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="856d4-231">Click **Add** button.</span></span> <span data-ttu-id="856d4-232">Em seguida, selecione **utilizadores e grupos** no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="856d4-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribua o utilizador][203]

5. <span data-ttu-id="856d4-234">No **utilizadores e grupos** caixa de diálogo, selecione **Britta Simon** na lista de utilizadores Olá.</span><span class="sxs-lookup"><span data-stu-id="856d4-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="856d4-235">Clique em **selecione** botão no **utilizadores e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="856d4-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="856d4-236">Clique em **atribuir** botão no **adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="856d4-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="856d4-237">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="856d4-237">Testing single sign-on</span></span>

<span data-ttu-id="856d4-238">Nesta secção, testar a configuração do Azure AD único início de sessão utilizando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="856d4-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="856d4-239">Ao clicar em mosaico de colaboração inovação Olá no painel de acesso de Olá, deve obter a página de início de sessão da aplicação de colaboração inovação.</span><span class="sxs-lookup"><span data-stu-id="856d4-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="856d4-240">Para mais informações sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="856d4-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="856d4-241">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="856d4-241">Additional resources</span></span>

* [<span data-ttu-id="856d4-242">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="856d4-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="856d4-243">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="856d4-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

