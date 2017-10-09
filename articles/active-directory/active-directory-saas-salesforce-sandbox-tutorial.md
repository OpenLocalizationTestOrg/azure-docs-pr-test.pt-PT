---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce Sandbox | Microsoft Docs"
description: "Saiba como toouse Salesforce Sandbox com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="01925-103">Tutorial: Integração do Azure Active Directory com o Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="01925-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="01925-104">o objetivo deste tutorial Olá é integração de Olá tooshow do Azure e a Salesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="01925-104">hello objective of this tutorial is tooshow hello integration of Azure and Salesforce Sandbox.</span></span>  

>[!TIP]
><span data-ttu-id="01925-105">Para comentários, consulte Olá [página de suporte do Azure](http://go.microsoft.com/fwlink/?LinkId=521878).</span><span class="sxs-lookup"><span data-stu-id="01925-105">For feedback, see hello [Azure support page](http://go.microsoft.com/fwlink/?LinkId=521878).</span></span> 
> 

<span data-ttu-id="01925-106">Forneça sandboxes que Olá toocreate de capacidade que várias cópias da sua organização em ambientes diferentes para diversos fins, tal como o desenvolvimento, teste e de preparação, sem comprometer a dados Olá e as aplicações na produção Salesforce organização.</span><span class="sxs-lookup"><span data-stu-id="01925-106">Sandboxes give you hello ability toocreate multiple copies of your organization in separate environments for a variety of purposes, such as development, testing, and training, without compromising hello data and applications in your Salesforce production organization.</span></span>  

<span data-ttu-id="01925-107">Para obter mais detalhes, consulte [Sandbox descrição-geral](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span><span class="sxs-lookup"><span data-stu-id="01925-107">For more details, see [Sandbox Overview](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)</span></span>

<span data-ttu-id="01925-108">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="01925-108">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="01925-109">Uma subscrição do Azure válida</span><span class="sxs-lookup"><span data-stu-id="01925-109">A valid Azure subscription</span></span>
* <span data-ttu-id="01925-110">Uma sandbox no site Salesforce.com</span><span class="sxs-lookup"><span data-stu-id="01925-110">A sandbox in Salesforce.com</span></span>

<span data-ttu-id="01925-111">Se ainda não tiver uma sandbox válida no site Salesforce.com, terá de toocontact Salesforce.</span><span class="sxs-lookup"><span data-stu-id="01925-111">If you don’t have a valid sandbox in Salesforce.com yet, you need toocontact Salesforce.</span></span>

<span data-ttu-id="01925-112">cenário de Olá descrito neste tutorial consiste em Olá blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="01925-112">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="01925-113">Ativar a integração de aplicações de Olá do Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="01925-113">Enabling hello application integration for Salesforce Sandbox</span></span>
2. <span data-ttu-id="01925-114">Configurar início de sessão único (SSO)</span><span class="sxs-lookup"><span data-stu-id="01925-114">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="01925-115">Ativar o seu domínio</span><span class="sxs-lookup"><span data-stu-id="01925-115">Enabling your domain</span></span>
4. <span data-ttu-id="01925-116">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="01925-116">Configuring user provisioning</span></span>
5. <span data-ttu-id="01925-117">Atribuir utilizadores</span><span class="sxs-lookup"><span data-stu-id="01925-117">Assigning users</span></span>

<span data-ttu-id="01925-118">![Cenário](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "cenário")</span><span class="sxs-lookup"><span data-stu-id="01925-118">![Scenario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a><span data-ttu-id="01925-119">Ativar a integração de aplicação Olá para Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="01925-119">Enable hello application integration for Salesforce Sandbox</span></span>
<span data-ttu-id="01925-120">o objetivo desta secção Olá é toooutline como integração de aplicações de Olá tooenable do Salesforce sandbox.</span><span class="sxs-lookup"><span data-stu-id="01925-120">hello objective of this section is toooutline how tooenable hello application integration for Salesforce sandbox.</span></span>

<span data-ttu-id="01925-121">**integração de aplicações de Olá tooenable do Salesforce sandbox, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="01925-121">**tooenable hello application integration for Salesforce sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="01925-122">No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01925-122">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="01925-123">![Do Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "do Active Directory")</span><span class="sxs-lookup"><span data-stu-id="01925-123">![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="01925-124">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="01925-124">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="01925-125">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="01925-125">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="01925-126">![Aplicações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "aplicações")</span><span class="sxs-lookup"><span data-stu-id="01925-126">![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="01925-127">Olá tooopen **Galeria de aplicações**, clique em **adicionar uma aplicação**e, em seguida, clique em **adicionar uma aplicação para a minha organização toouse**.</span><span class="sxs-lookup"><span data-stu-id="01925-127">tooopen hello **Application Gallery**, click **Add An App**, and then click **Add an application for my organization toouse**.</span></span>
   
   <span data-ttu-id="01925-128">![O que fazer pretende toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Que itens pretende toodo?")</span><span class="sxs-lookup"><span data-stu-id="01925-128">![What do you want toodo?](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "What do you want toodo?")</span></span>
5. <span data-ttu-id="01925-129">No Olá **caixa pesquisa**, tipo **Salesforce Sandbox**.</span><span class="sxs-lookup"><span data-stu-id="01925-129">In hello **search box**, type **Salesforce Sandbox**.</span></span>
   
   <span data-ttu-id="01925-130">![Galeria de aplicações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galeria de aplicações")</span><span class="sxs-lookup"><span data-stu-id="01925-130">![Application Gallery](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Application Gallery")</span></span>
6. <span data-ttu-id="01925-131">No painel de resultados de Olá, selecione **Salesforce Sandbox**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="01925-131">In hello results pane, select **Salesforce Sandbox**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="01925-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="01925-132">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")</span></span>
   
## <a name="configur-single-sign-on-sso"></a><span data-ttu-id="01925-133">Configur-início de sessão único (SSO)</span><span class="sxs-lookup"><span data-stu-id="01925-133">Configur single sign-on (SSO)</span></span>

<span data-ttu-id="01925-134">o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooSalesforce à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.</span><span class="sxs-lookup"><span data-stu-id="01925-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSalesforce with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="01925-135">**tooconfigure único início de sessão, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="01925-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="01925-136">No Olá portal clássico do Azure, no Olá **Salesforce Sandbox** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01925-136">In hello Azure classic portal, on hello **Salesforce Sandbox** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="01925-137">![Configurar o início de sessão único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="01925-137">![Configure single sign-on](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="01925-138">No Olá **como seria, como os utilizadores toosign no tooSalesforce Sandbox** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="01925-138">On hello **How would you like users toosign on tooSalesforce Sandbox** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="01925-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="01925-139">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")</span></span>
3. <span data-ttu-id="01925-140">No Olá **URL da aplicação configurar** página, numa Olá **URL de início de sessão** caixa de texto, escreva o URL utilizando Olá seguir o padrão `http://company.my.salesforce.com`e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="01925-140">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type your URL using hello following pattern `http://company.my.salesforce.com`, and then click **Next**.</span></span>
   
   <span data-ttu-id="01925-141">![Configurar o URL da aplicação](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="01925-141">![Configure App URL](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configure App URL")</span></span>
4. <span data-ttu-id="01925-142">Se já tiver configurado início de sessão único para outra instância do Salesforce Sandbox no seu diretório, em seguida, também tem de configurar Olá **identificador** toohave Olá mesmo valor que Olá **iniciar sessão no URL**.</span><span class="sxs-lookup"><span data-stu-id="01925-142">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure hello **Identifier** toohave hello same value as hello **Sign on URL**.</span></span> 
 * <span data-ttu-id="01925-143">Olá **identificador** campo pode ser encontrado verificando Olá **mostrar as definições avançadas** caixa de verificação no Olá **URL da aplicação configurar** página da caixa de diálogo Olá.</span><span class="sxs-lookup"><span data-stu-id="01925-143">hello **Identifier** field can be found by checking hello **Show advanced settings** checkbox on hello **Configure App URL** page of hello dialog.</span></span>
5. <span data-ttu-id="01925-144">No Olá **configurar o início de sessão único em Salesforce Sandbox** página, clique em **Transferir certificado**e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="01925-144">On hello **Configure single sign-on at Salesforce Sandbox** page, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="01925-145">![Configurar o início de sessão único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="01925-145">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="01925-146">Numa janela do browser web diferente, inicie sessão no seu sandbox Salesforce como administrador.</span><span class="sxs-lookup"><span data-stu-id="01925-146">In a different web browser window, log into your Salesforce sandbox as an administrator.</span></span>
7. <span data-ttu-id="01925-147">No menu de Olá na parte superior do Olá, clique em **configuração**.</span><span class="sxs-lookup"><span data-stu-id="01925-147">In hello menu on hello top, click **Setup**.</span></span>
   
   <span data-ttu-id="01925-148">![A configuração](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "programa de configuração")</span><span class="sxs-lookup"><span data-stu-id="01925-148">![Setup](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Setup")</span></span>
8. <span data-ttu-id="01925-149">No painel de navegação de Olá Olá esquerda, clique em **controlos de segurança**e, em seguida, clique em **as definições de início de sessão único**.</span><span class="sxs-lookup"><span data-stu-id="01925-149">In hello navigation pane on hello left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
   
   <span data-ttu-id="01925-150">![Single Sign-On definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "único as definições de início de sessão")</span><span class="sxs-lookup"><span data-stu-id="01925-150">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Single Sign-On Settings")</span></span>
9. <span data-ttu-id="01925-151">Na secção de definições de início de sessão único Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="01925-151">On hello Single Sign-On Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="01925-152">![Single Sign-On definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "único as definições de início de sessão")</span><span class="sxs-lookup"><span data-stu-id="01925-152">![Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Single Sign-On Settings")</span></span>  
 1.  <span data-ttu-id="01925-153">Selecione **SAML ativada**.</span><span class="sxs-lookup"><span data-stu-id="01925-153">Select **SAML Enabled**.</span></span> 
 2.  <span data-ttu-id="01925-154">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="01925-154">Click **New**.</span></span>
10. <span data-ttu-id="01925-155">No Olá SAML único início de sessão da secção definições, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="01925-155">On hello SAML Single Sign-On Settings section, perform hello following steps:</span></span>
    
    <span data-ttu-id="01925-156">![SAML único início de sessão definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML único início de sessão definições")</span><span class="sxs-lookup"><span data-stu-id="01925-156">![SAML Single Sign-On Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign-On Settings")</span></span>  
 1. <span data-ttu-id="01925-157">Na caixa de texto do Olá nome, escreva o nome de Olá da configuração de Olá (por ex.: *SPSSOWAAD\_teste*).</span><span class="sxs-lookup"><span data-stu-id="01925-157">In hello Name textbox, type hello name of hello configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 
 2. <span data-ttu-id="01925-158">No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Salesforce Sandbox** página de diálogo, Olá cópia **URL do emissor** valor e, em seguida, cole-o Olá **emissor**caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="01925-158">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Issuer URL** value, and then paste it into hello **Issuer** textbox.</span></span>
 3. <span data-ttu-id="01925-159">No Olá **Id de entidade** caixa de texto, tipo **https://test.salesforce.com** se se tratar de Olá primeira Salesforce Sandbox instância que está a adicionar tooyour diretório.</span><span class="sxs-lookup"><span data-stu-id="01925-159">In hello **Entity Id** textbox, type **https://test.salesforce.com** if this is hello first Salesforce Sandbox instance that you are adding tooyour directory.</span></span> <span data-ttu-id="01925-160">Se já tiver adicionado uma instância do Salesforce Sandbox, em seguida, para Olá **ID de entidade** tipo na Olá **URL de início de sessão**, que deve ter este formato:`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="01925-160">If you have already added an instance of Salesforce Sandbox, then for hello **Entity ID** type in hello **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>   
 4. <span data-ttu-id="01925-161">Clique em **procurar** Olá tooupload transferido o certificado.</span><span class="sxs-lookup"><span data-stu-id="01925-161">Click **Browse** tooupload hello downloaded certificate.</span></span>  
 5. <span data-ttu-id="01925-162">Como **tipo de identidade de SAML**, selecione **asserção contém Olá Federação ID do objeto de utilizador Olá**.</span><span class="sxs-lookup"><span data-stu-id="01925-162">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span> 
 6. <span data-ttu-id="01925-163">Como **SAML identidade localização**, selecione **é de identidade no elemento de NameIdentifier Olá do Olá instrução requerente**.</span><span class="sxs-lookup"><span data-stu-id="01925-163">As **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
 7. <span data-ttu-id="01925-164">No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Salesforce Sandbox** página de diálogo, Olá cópia **URL de início de sessão remoto** valor e, em seguida, cole-o Olá **fornecedor de identidade URL de início de sessão** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="01925-164">In hello Azure classic portal, on hello **Configure single sign-on at Salesforce Sandbox** dialogue page, copy hello **Remote Login URL** value, and then paste it into hello **Identity Provider Login URL** textbox.</span></span> 
 8. <span data-ttu-id="01925-165">SFDC não suporta a fim de sessão SAML.</span><span class="sxs-lookup"><span data-stu-id="01925-165">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="01925-166">Como solução, cole 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' para Olá **URL de fim de sessão do fornecedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="01925-166">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into hello **Identity Provider Logout URL** textbox.</span></span>
 9. <span data-ttu-id="01925-167">Como **fornecedor iniciada pedido vínculo de serviço**, selecione **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="01925-167">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 
 10. <span data-ttu-id="01925-168">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="01925-168">Click **Save**.</span></span>
11. <span data-ttu-id="01925-169">No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída** tooclose Olá **configurar início de sessão único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01925-169">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="01925-170">![Configurar o início de sessão único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="01925-170">![Configure Single Sign-On](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configure Single Sign-On")</span></span>

## <a name="enable-your-domain"></a><span data-ttu-id="01925-171">Ativar o seu domínio</span><span class="sxs-lookup"><span data-stu-id="01925-171">Enable your domain</span></span>
<span data-ttu-id="01925-172">Esta secção assume que já criou um domínio.</span><span class="sxs-lookup"><span data-stu-id="01925-172">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="01925-173">Para obter mais detalhes, consulte [definir o nome de domínio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span><span class="sxs-lookup"><span data-stu-id="01925-173">For more details, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="01925-174">**tooenable o domínio, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="01925-174">**tooenable your domain, perform hello following steps:**</span></span>

1. <span data-ttu-id="01925-175">No painel de navegação esquerdo Olá, clique em **gestão de domínios**e, em seguida, clique em **meu domínio.**</span><span class="sxs-lookup"><span data-stu-id="01925-175">In hello left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
   <span data-ttu-id="01925-176">![O meu domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "meu domínio")</span><span class="sxs-lookup"><span data-stu-id="01925-176">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "My Domain")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="01925-177">Certifique-se que o seu domínio foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="01925-177">Please make sure that your domain has been configured correctly.</span></span> 
   > 
2. <span data-ttu-id="01925-178">No Olá **definições de páginas de início de sessão** secção, clique em **editar**, em seguida, como **serviço de autenticação**, selecione nome Olá Olá SAML único início de sessão na definição de Olá anterior secção e, finalmente, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="01925-178">In hello **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select hello name of hello SAML Single Sign-On Setting from hello previous section, and finally click **Save**.</span></span>
   
   <span data-ttu-id="01925-179">![O meu domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "meu domínio")</span><span class="sxs-lookup"><span data-stu-id="01925-179">![My Domain](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "My Domain")</span></span>

<span data-ttu-id="01925-180">Assim que tiver um domínio configurado, os utilizadores devem utilizar sandbox Salesforce de toohello toologin Olá domínio URL.</span><span class="sxs-lookup"><span data-stu-id="01925-180">As soon as you have a domain configured, your users should use hello domain URL toologin toohello Salesforce sandbox.</span></span>  

<span data-ttu-id="01925-181">valor de Olá tooget do URL de Olá, clique em perfil SSO Olá que criou na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="01925-181">tooget hello value of hello URL, click hello SSO profile you have created in hello previous section.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="01925-182">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="01925-182">Configure user provisioning</span></span>
<span data-ttu-id="01925-183">o objetivo desta secção Olá é toooutline como tooenable aprovisionamento de utilizadores do utilizador do Active Directory contas tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="01925-183">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooSalesforce Sandbox.</span></span>

<span data-ttu-id="01925-184">**tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="01925-184">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="01925-185">No portal do Salesforce Olá, na barra de navegação superior Olá, selecione o nome tooexpand o menu de utilizador:</span><span class="sxs-lookup"><span data-stu-id="01925-185">In hello Salesforce portal, in hello top navigation bar, select your name tooexpand your user menu:</span></span>
   
   <span data-ttu-id="01925-186">![As minhas definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "as minhas definições")</span><span class="sxs-lookup"><span data-stu-id="01925-186">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings")</span></span>
2. <span data-ttu-id="01925-187">No menu do utilizador, selecione **as minhas definições** tooopen sua **as minhas definições** página.</span><span class="sxs-lookup"><span data-stu-id="01925-187">From your user menu, select **My Settings** tooopen your **My Settings** page.</span></span>
3. <span data-ttu-id="01925-188">No painel esquerdo Olá, clique em **pessoais** tooexpand Olá secção pessoal e, em seguida, clique em **repor o meu Token de segurança**:</span><span class="sxs-lookup"><span data-stu-id="01925-188">In hello left pane, click **Personal** tooexpand hello Personal section, and then click **Reset My Security Token**:</span></span>
   
   <span data-ttu-id="01925-189">![As minhas definições](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "as minhas definições")</span><span class="sxs-lookup"><span data-stu-id="01925-189">![My Settings](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings")</span></span>
4. <span data-ttu-id="01925-190">No Olá **repor o meu Token de segurança** página, clique em **repor o Token de segurança** toorequest uma mensagem de e-mail que contém o token de segurança em Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="01925-190">On hello **Reset My Security Token** page, click **Reset Security Token** toorequest an email that contains your Salesforce.com security token.</span></span>
   
   <span data-ttu-id="01925-191">![Novo Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "novo Token")</span><span class="sxs-lookup"><span data-stu-id="01925-191">![New Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token")</span></span>
5. <span data-ttu-id="01925-192">Verifique a pasta a receber de correio eletrónico para uma mensagem de e-mail em Salesforce.com com "**confirmação de segurança salesforce.com.com**" como requerente.</span><span class="sxs-lookup"><span data-stu-id="01925-192">Check your email inbox for an email from Salesforce.com with “**salesforce.com.com security confirmation**” as subject.</span></span>
6. <span data-ttu-id="01925-193">Rever este e-mail e copie Olá segurança token valor.</span><span class="sxs-lookup"><span data-stu-id="01925-193">Review this email and copy hello security token value.</span></span>
7. <span data-ttu-id="01925-194">No Olá portal clássico do Azure, no Olá **salesforce Sandbox** página de integração de aplicações, clique em **configurar o aprovisionamento de utilizadores** tooopen Olá **configurar o aprovisionamento de utilizadores**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="01925-194">In hello Azure classic portal, on hello **salesforce Sandbox** application integration page, click **Configure user provisioning** tooopen hello **Configure User Provisioning** dialog.</span></span>
   
   <span data-ttu-id="01925-195">![Configurar o aprovisionamento de utilizadores](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "configurar o aprovisionamento de utilizadores")</span><span class="sxs-lookup"><span data-stu-id="01925-195">![Configure user provisioning](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configure user provisioning")</span></span>
8. <span data-ttu-id="01925-196">No Olá **introduza aprovisionamento de utilizadores automático o Salesforce Sandbox credenciais tooenable** , indique Olá seguintes definições de configuração:</span><span class="sxs-lookup"><span data-stu-id="01925-196">On hello **Enter your Salesforce Sandbox credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
   <span data-ttu-id="01925-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span><span class="sxs-lookup"><span data-stu-id="01925-197">![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")</span></span>   
 1. <span data-ttu-id="01925-198">No Olá **nome de utilizador de Admin do Salesforce Sandbox** caixa de texto, tipo de nome que tem Olá de conta de uma sandbox Salesforce **administrador de sistema** perfil no site Salesforce.com atribuído.</span><span class="sxs-lookup"><span data-stu-id="01925-198">In hello **Salesforce Sandbox Admin User Name** textbox, type a Salesforce sandbox account name that has hello **System Administrator** profile in Salesforce.com assigned.</span></span>
 2. <span data-ttu-id="01925-199">No Olá **palavra-passe de administrador do Salesforce Sandbox** caixa de texto, tipo Olá palavra-passe desta conta.</span><span class="sxs-lookup"><span data-stu-id="01925-199">In hello **Salesforce Sandbox Admin Password** textbox, type hello password for this account.</span></span>
 3. <span data-ttu-id="01925-200">No Olá **Token de segurança do utilizador** caixa de texto, valor de token de segurança de Olá de colar.</span><span class="sxs-lookup"><span data-stu-id="01925-200">In hello **User Security Token** textbox, paste hello security token value.</span></span>
 4. <span data-ttu-id="01925-201">Clique em **validar** tooverify a configuração.</span><span class="sxs-lookup"><span data-stu-id="01925-201">Click **Validate** tooverify your configuration.</span></span>
 5. <span data-ttu-id="01925-202">Clique em Olá **seguinte** Olá do botão tooopen **confirmação** página.</span><span class="sxs-lookup"><span data-stu-id="01925-202">Click hello **Next** button tooopen hello **Confirmation** page.</span></span>
9. <span data-ttu-id="01925-203">No Olá **confirmação** página, clique em **concluída** toosave a configuração.</span><span class="sxs-lookup"><span data-stu-id="01925-203">On hello **Confirmation** page, click **Complete** toosave your configuration.</span></span>
   
## <a name="assigning-users"></a><span data-ttu-id="01925-204">Atribuir utilizadores</span><span class="sxs-lookup"><span data-stu-id="01925-204">Assigning users</span></span>

<span data-ttu-id="01925-205">tootest a configuração, terá de toogrant Olá do Azure AD utilizadores tooallow utilizando o tooit de acesso de aplicação atribuindo-los.</span><span class="sxs-lookup"><span data-stu-id="01925-205">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="01925-206">**tooassign utilizadores tooSalesforce Sandbox, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="01925-206">**tooassign users tooSalesforce Sandbox, perform hello following steps:**</span></span>

1. <span data-ttu-id="01925-207">Olá portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="01925-207">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="01925-208">No Olá * * Salesforce Sandbox * * página de integração de aplicações, clique em **atribuir utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="01925-208">On hello **Salesforce Sandbox **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="01925-209">![Atribuir utilizadores](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "atribuir utilizadores")</span><span class="sxs-lookup"><span data-stu-id="01925-209">![Assign users](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Assign users")</span></span>
3. <span data-ttu-id="01925-210">Selecione o utilizador de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm a atribuição.</span><span class="sxs-lookup"><span data-stu-id="01925-210">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="01925-211">![Sim](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="01925-211">![Yes](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="01925-212">Deve agora Aguarde 10 minutos e certifique-se de que a conta de Olá foi sincronizado tooSalesforce Sandbox.</span><span class="sxs-lookup"><span data-stu-id="01925-212">You should now wait for 10 minutes and verify that hello account has been synchronized tooSalesforce Sandbox.</span></span>

<span data-ttu-id="01925-213">Se quiser tootest as definições de SSO, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="01925-213">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="01925-214">Para obter mais detalhes sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="01925-214">For more details about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

