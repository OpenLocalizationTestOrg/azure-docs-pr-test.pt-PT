---
title: "Tutorial: Integração do Azure Active Directory com Questetra BPM Suite | Microsoft Docs"
description: "Saiba como tooconfigure de sessão único-entre o Azure Active Directory e Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="513b9-103">Tutorial: Integração do Azure Active Directory com Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="513b9-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="513b9-104">o objetivo deste tutorial Olá é tooshow como toointegrate Questetra BPM Suite com o Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="513b9-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="513b9-105">Integrar Questetra BPM Suite com o Azure AD fornece-lhe Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="513b9-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="513b9-106">Pode controlar no Azure AD que tenha acesso tooQuestetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="513b9-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="513b9-107">Pode ativar a utilizadores tooautomatically get com sessão iniciada tooQuestetra Suite BPM (Single Sign-On) com as respetivas contas do Azure AD</span><span class="sxs-lookup"><span data-stu-id="513b9-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="513b9-108">Pode gerir as contas numa localização central - Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="513b9-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="513b9-109">Se pretender tooknow mais detalhes sobre a integração de aplicações SaaS com o Azure AD, veja [que é o acesso a aplicações e início de sessão no Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="513b9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="513b9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="513b9-110">Prerequisites</span></span>
<span data-ttu-id="513b9-111">integração do Azure AD com Questetra BPM Suite tooconfigure, terá de Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="513b9-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="513b9-112">Uma subscrição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="513b9-112">An Azure AD subscription</span></span>
* <span data-ttu-id="513b9-113">Um [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) início de sessão único subscrição ativado</span><span class="sxs-lookup"><span data-stu-id="513b9-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="513b9-114">Olá tootest os passos neste tutorial, não recomendamos que utilize um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="513b9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="513b9-115">tootest Olá obter os passos neste tutorial, deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="513b9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="513b9-116">Não deve utilizar o seu ambiente de produção, a menos que isto é necessário.</span><span class="sxs-lookup"><span data-stu-id="513b9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="513b9-117">Se não tiver um ambiente de avaliação do Azure AD, pode obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="513b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="513b9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="513b9-118">Scenario Description</span></span>
<span data-ttu-id="513b9-119">o objetivo deste tutorial Olá é tooenable tootest do Azure AD-início de sessão único num ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="513b9-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="513b9-120">cenário de Olá descrito neste tutorial consiste em três blocos modulares principais:</span><span class="sxs-lookup"><span data-stu-id="513b9-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="513b9-121">Adicionar Questetra BPM Suite da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="513b9-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="513b9-122">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="513b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="513b9-123">Adicionar Questetra BPM Suite da Galeria de Olá</span><span class="sxs-lookup"><span data-stu-id="513b9-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="513b9-124">tooconfigure Olá integração do Questetra BPM Suite com o Azure AD, é necessário tooadd Questetra BPM Suite Olá Galeria tooyour na lista de aplicações SaaS geridas.</span><span class="sxs-lookup"><span data-stu-id="513b9-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="513b9-125">**tooadd Questetra BPM Suite da Galeria de Olá, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="513b9-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="513b9-126">No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="513b9-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="513b9-128">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="513b9-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="513b9-129">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="513b9-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplicações][2]

4. <span data-ttu-id="513b9-131">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="513b9-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplicações][3]

5. <span data-ttu-id="513b9-133">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="513b9-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplicações][4]

6. <span data-ttu-id="513b9-135">Na caixa de pesquisa de Olá, escreva **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="513b9-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Aplicações][5]

7. <span data-ttu-id="513b9-137">No painel de resultados de Olá, selecione **Questetra BPM Suite**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="513b9-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="513b9-138">Configurar e testar o Azure AD de sessão único-</span><span class="sxs-lookup"><span data-stu-id="513b9-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="513b9-139">o objetivo desta secção Olá é tooshow que como tooconfigure e teste do Azure AD-início de sessão único com Questetra BPM Suite com base num utilizador de teste chamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="513b9-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="513b9-140">Para único início de sessão toowork, do Azure AD tem tooknow que utilizador do homólogo Olá utilizador de tooan Questetra BPM Suite no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="513b9-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="513b9-141">Por outras palavras, uma relação de ligação entre um utilizador do Azure AD e o utilizador relacionados Olá Questetra BPM Suite tem toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="513b9-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="513b9-142">Esta relação de ligação é estabelecida através da atribuição de valor Olá Olá **nome de utilizador** no Azure AD como valor Olá Olá **Username** no Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="513b9-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="513b9-143">tooconfigure e teste do Azure AD-início de sessão único com Questetra BPM Suite, terá de Olá toocomplete blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="513b9-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="513b9-144">**[Configurar o Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable sua toouse utilizadores esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="513b9-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="513b9-145">**[Criar um utilizador de teste do Azure AD](#creating-an-azure-ad-test-user)**  -tootest do Azure AD-início de sessão único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="513b9-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="513b9-146">**[Criar um utilizador de teste Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave um homólogo de Britta Simon no Questetra BPM Suite que é a representação de toohello ligado do Azure AD de forma.</span><span class="sxs-lookup"><span data-stu-id="513b9-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="513b9-147">**[Utilizador de teste de Olá do Azure AD atribuição](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse do Azure AD-início de sessão único.</span><span class="sxs-lookup"><span data-stu-id="513b9-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="513b9-148">**[Teste o início de sessão único](#testing-single-sign-on)**  -tooverify Olá se funciona de configuração.</span><span class="sxs-lookup"><span data-stu-id="513b9-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="513b9-149">Configurar o Azure AD início de sessão único</span><span class="sxs-lookup"><span data-stu-id="513b9-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="513b9-150">o objetivo desta secção Olá é tooenable do Azure AD início de sessão no portal clássico do Azure de Olá e tooconfigure-início de sessão único na sua aplicação Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="513b9-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="513b9-151">**tooconfigure do Azure AD-início de sessão único com Questetra BPM Suite, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="513b9-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="513b9-152">No Olá portal clássico do Azure, no Olá **Questetra BPM Suite** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar Single Sign-On**  caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="513b9-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurar o início de sessão único][8]

2. <span data-ttu-id="513b9-154">No Olá **como seria, como os utilizadores toosign no tooQuestetra BPM Suite** página, selecione **do Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="513b9-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD início de sessão único][9]

3. <span data-ttu-id="513b9-156">Numa janela do browser web diferente, inicie sessão no seu **Questetra BPM Suite** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="513b9-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="513b9-157">No menu de Olá na parte superior do Olá, clique em **definições do sistema**.</span><span class="sxs-lookup"><span data-stu-id="513b9-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Azure AD início de sessão único][10]

5. <span data-ttu-id="513b9-159">Olá tooopen **SingleSignOnSAML** página, clique em **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="513b9-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD início de sessão único][11]

6. <span data-ttu-id="513b9-161">No Olá portal clássico do Azure, no Olá **configurar definições de aplicação** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="513b9-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Configurar definições da aplicação][13]
   
    <span data-ttu-id="513b9-163">a.</span><span class="sxs-lookup"><span data-stu-id="513b9-163">a.</span></span> <span data-ttu-id="513b9-164">No **Questetra BPM Suite** site da empresa, no Olá secção de informações de SP, Olá cópia **ACS URL**e, em seguida, cole-o Olá **URL de início de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="513b9-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="513b9-165">b.</span><span class="sxs-lookup"><span data-stu-id="513b9-165">b.</span></span> <span data-ttu-id="513b9-166">No **Questetra BPM Suite** site da empresa, no Olá secção de informações de SP, Olá cópia **ID de entidade**e, em seguida, cole-o Olá **URL do emissor** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="513b9-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="513b9-167">c.</span><span class="sxs-lookup"><span data-stu-id="513b9-167">c.</span></span> <span data-ttu-id="513b9-168">No **Questetra BPM Suite** site da empresa, no Olá secção de informações de SP, Olá cópia **ACS URL**e, em seguida, cole-o Olá **URL de resposta** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="513b9-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="513b9-169">d.</span><span class="sxs-lookup"><span data-stu-id="513b9-169">d.</span></span> <span data-ttu-id="513b9-170">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="513b9-170">Click **Next**.</span></span>

7. <span data-ttu-id="513b9-171">No Olá **configurar o início de sessão único em Questetra BPM Suite** página, clique em **Transferir certificado**e, em seguida, guarde o ficheiro de certificado Olá localmente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="513b9-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configurar o início de sessão único][14]

8. <span data-ttu-id="513b9-173">No **Questetra BPM Suite** da empresa site, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="513b9-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Configurar o início de sessão único][15]
   
    <span data-ttu-id="513b9-175">a.</span><span class="sxs-lookup"><span data-stu-id="513b9-175">a.</span></span> <span data-ttu-id="513b9-176">Selecione **ativar o início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="513b9-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="513b9-177">b.</span><span class="sxs-lookup"><span data-stu-id="513b9-177">b.</span></span> <span data-ttu-id="513b9-178">No portal clássico do Azure Olá, copie Olá **URL do emissor** valor e, em seguida, cole-o Olá **ID de entidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="513b9-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="513b9-179">c.</span><span class="sxs-lookup"><span data-stu-id="513b9-179">c.</span></span> <span data-ttu-id="513b9-180">No portal clássico do Azure Olá, copie Olá **URL Single Sign-On serviço** valor e, em seguida, cole-o Olá **URL de página de início de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="513b9-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="513b9-181">d.</span><span class="sxs-lookup"><span data-stu-id="513b9-181">d.</span></span> <span data-ttu-id="513b9-182">No portal clássico do Azure Olá, copie Olá **único URL de serviço Sign-Out** valor e, em seguida, cole-o Olá **URL da página de início de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="513b9-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="513b9-183">e.</span><span class="sxs-lookup"><span data-stu-id="513b9-183">e.</span></span> <span data-ttu-id="513b9-184">No Olá **NameID formato** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:1.1:nameid-formato: endereço de correio eletrónico**.</span><span class="sxs-lookup"><span data-stu-id="513b9-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="513b9-185">f.</span><span class="sxs-lookup"><span data-stu-id="513b9-185">f.</span></span> <span data-ttu-id="513b9-186">Crie um ficheiro codificado base-64 do seu certificado transferido.</span><span class="sxs-lookup"><span data-stu-id="513b9-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="513b9-187">Para obter mais detalhes, consulte [como tooconvert um binário de certificado para um ficheiro de texto](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="513b9-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="513b9-188">g.</span><span class="sxs-lookup"><span data-stu-id="513b9-188">g.</span></span> <span data-ttu-id="513b9-189">Abra o certificado codificado base-64 no bloco de notas, Olá copiar conteúdo-lo na sua área de transferência e, em seguida, cole-o Olá **certificado validação** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="513b9-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="513b9-190">h.</span><span class="sxs-lookup"><span data-stu-id="513b9-190">h.</span></span> <span data-ttu-id="513b9-191">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="513b9-191">Click **Save**.</span></span>

1. <span data-ttu-id="513b9-192">No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="513b9-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![O que é o Azure AD Connect][17]

2. <span data-ttu-id="513b9-194">No Olá **único início de sessão confirmação** página, clique em **concluída**.</span><span class="sxs-lookup"><span data-stu-id="513b9-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![O que é o Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="513b9-196">Criar um utilizador de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="513b9-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="513b9-197">o objetivo desta secção Olá é toocreate um utilizador de teste no portal clássico do Azure chamado Britta Simon de Olá.</span><span class="sxs-lookup"><span data-stu-id="513b9-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="513b9-198">**toocreate um utilizador de teste no Azure AD, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="513b9-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="513b9-199">No Olá **portal clássico do Azure**, no painel de navegação esquerdo de Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="513b9-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Criar utilizador de teste do Azure AD][100] 

2. <span data-ttu-id="513b9-201">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="513b9-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="513b9-202">lista de Olá toodisplay de utilizadores, no menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="513b9-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Criar utilizador de teste do Azure AD][101] 

4. <span data-ttu-id="513b9-204">Olá tooopen **adicionar utilizador** caixa de diálogo, na barra de ferramentas de Olá na parte inferior do Olá, clique em **adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="513b9-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Criar utilizador de teste do Azure AD][102] 

5. <span data-ttu-id="513b9-206">No Olá **diga-nos informações sobre este utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="513b9-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Criar utilizador de teste do Azure AD][103]
   
    <span data-ttu-id="513b9-208">a.</span><span class="sxs-lookup"><span data-stu-id="513b9-208">a.</span></span> <span data-ttu-id="513b9-209">Como **tipo de utilizador**, selecione **novo utilizador na sua organização**.</span><span class="sxs-lookup"><span data-stu-id="513b9-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="513b9-210">b.</span><span class="sxs-lookup"><span data-stu-id="513b9-210">b.</span></span> <span data-ttu-id="513b9-211">No nome de utilizador de Olá **textbox**, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="513b9-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="513b9-212">c.</span><span class="sxs-lookup"><span data-stu-id="513b9-212">c.</span></span> <span data-ttu-id="513b9-213">Clique em Seguinte.</span><span class="sxs-lookup"><span data-stu-id="513b9-213">Click Next.</span></span>

6. <span data-ttu-id="513b9-214">No Olá **perfil de utilizador** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="513b9-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Criar utilizador de teste do Azure AD][104] 
   
    <span data-ttu-id="513b9-216">a.</span><span class="sxs-lookup"><span data-stu-id="513b9-216">a.</span></span> <span data-ttu-id="513b9-217">No Olá **nome próprio** caixa de texto, tipo **Britta**.</span><span class="sxs-lookup"><span data-stu-id="513b9-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="513b9-218">b.</span><span class="sxs-lookup"><span data-stu-id="513b9-218">b.</span></span> <span data-ttu-id="513b9-219">No Olá **Apelido** caixa de texto, tipo, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="513b9-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="513b9-220">c.</span><span class="sxs-lookup"><span data-stu-id="513b9-220">c.</span></span> <span data-ttu-id="513b9-221">No Olá **nome a apresentar** caixa de texto, tipo **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="513b9-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="513b9-222">d.</span><span class="sxs-lookup"><span data-stu-id="513b9-222">d.</span></span> <span data-ttu-id="513b9-223">No Olá **função** lista, selecione **utilizador**.</span><span class="sxs-lookup"><span data-stu-id="513b9-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="513b9-224">e.</span><span class="sxs-lookup"><span data-stu-id="513b9-224">e.</span></span> <span data-ttu-id="513b9-225">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="513b9-225">Click **Next**.</span></span>

7. <span data-ttu-id="513b9-226">No Olá **Get palavra-passe temporária** página da caixa de diálogo, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="513b9-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Criar utilizador de teste do Azure AD][105]  

8. <span data-ttu-id="513b9-228">No Olá **Get palavra-passe temporária** diálogo página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="513b9-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Criar utilizador de teste do Azure AD][106]   
   
    <span data-ttu-id="513b9-230">a.</span><span class="sxs-lookup"><span data-stu-id="513b9-230">a.</span></span> <span data-ttu-id="513b9-231">Anote o valor Olá Olá **nova palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="513b9-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="513b9-232">b.</span><span class="sxs-lookup"><span data-stu-id="513b9-232">b.</span></span> <span data-ttu-id="513b9-233">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="513b9-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="513b9-234">Criar um utilizador de teste Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="513b9-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="513b9-235">o objetivo desta secção Olá é toocreate um utilizador chamado Britta Simon no Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="513b9-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="513b9-236">**toocreate um utilizador chamar Britta Simon Questetra BPM Suite, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="513b9-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="513b9-237">Início de sessão tooyour Questetra BPM Suite site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="513b9-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="513b9-238">Aceda demasiado**definições do sistema > lista de utilizadores > novo utilizador**.</span><span class="sxs-lookup"><span data-stu-id="513b9-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="513b9-239">Na caixa de diálogo de novo utilizador Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="513b9-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Criar utilizador de teste][300] 
   
    <span data-ttu-id="513b9-241">a.</span><span class="sxs-lookup"><span data-stu-id="513b9-241">a.</span></span> <span data-ttu-id="513b9-242">No Olá **nome** caixa de texto, escreva o nome de utilizador de Britta no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="513b9-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="513b9-243">b.</span><span class="sxs-lookup"><span data-stu-id="513b9-243">b.</span></span> <span data-ttu-id="513b9-244">No Olá **E-Mail** caixa de texto, escreva o nome de utilizador de Britta no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="513b9-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="513b9-245">c.</span><span class="sxs-lookup"><span data-stu-id="513b9-245">c.</span></span> <span data-ttu-id="513b9-246">No Olá **palavra-passe** caixa de texto, escreva um palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="513b9-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="513b9-247">Clique em **adicionar novo utilizador**.</span><span class="sxs-lookup"><span data-stu-id="513b9-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="513b9-248">Atribuir o utilizador de teste de Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="513b9-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="513b9-249">o objetivo desta secção Olá é tooenabling Britta Simon toouse do Azure-início de sessão único, concedendo tooQuestetra respetivo acesso BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="513b9-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![O que é o Azure AD Connect][200]

<span data-ttu-id="513b9-251">**tooassign Britta Simon tooQuestetra BPM Suite, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="513b9-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="513b9-252">Olá, Azure portal clássico, a vista de aplicações Olá tooopen, na vista de diretório Olá, clique em **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="513b9-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![O que é o Azure AD Connect][201]
2. <span data-ttu-id="513b9-254">Na lista de aplicações de Olá, selecione **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="513b9-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![O que é o Azure AD Connect][205]
3. <span data-ttu-id="513b9-256">No menu de Olá na parte superior do Olá, clique em **utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="513b9-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![O que é o Azure AD Connect][202]
4. <span data-ttu-id="513b9-258">Na lista de utilizadores Olá, selecione **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="513b9-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![O que é o Azure AD Connect][203]
5. <span data-ttu-id="513b9-260">Na barra de ferramentas Olá na parte inferior de Olá, clique em **atribuir**.</span><span class="sxs-lookup"><span data-stu-id="513b9-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![O que é o Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="513b9-262">Teste o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="513b9-262">Testing Single Sign-On</span></span>
<span data-ttu-id="513b9-263">o objetivo desta secção Olá é tootest a configuração de início de sessão único do Azure AD com Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="513b9-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="513b9-264">Ao clicar em mosaico de Questetra BPM Suite Olá no painel de acesso de Olá, deve obter a aplicação de Questetra BPM Suite tooyour automaticamente com sessão iniciada.</span><span class="sxs-lookup"><span data-stu-id="513b9-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="513b9-265">Recursos Adicionais</span><span class="sxs-lookup"><span data-stu-id="513b9-265">Additional Resources</span></span>
* [<span data-ttu-id="513b9-266">Lista de tutoriais sobre como tooIntegrate aplicações SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="513b9-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="513b9-267">O que é o acesso a aplicações e início de sessão no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="513b9-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
