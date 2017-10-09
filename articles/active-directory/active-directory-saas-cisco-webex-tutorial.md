---
title: "Tutorial: Integração do Azure Active Directory com o Cisco Webex | Microsoft Docs"
description: "Saiba como toouse Cisco Webex com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="92594-103">Tutorial: Integração do Azure Active Directory com Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="92594-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="92594-104">o objetivo deste tutorial Olá é integração de Olá tooshow do Azure e Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="92594-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="92594-105">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="92594-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="92594-106">Uma subscrição do Azure válida</span><span class="sxs-lookup"><span data-stu-id="92594-106">A valid Azure subscription</span></span>
* <span data-ttu-id="92594-107">Um inquilino Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="92594-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="92594-108">Depois de concluir este tutorial, Olá utilizadores do Azure AD que atribuiu tooCisco Webex será toosingle capaz de início de sessão na aplicação Olá no site da sua empresa Cisco Webex (serviço fornecedor iniciada pelo início de sessão) ou utilizar Olá [toohello de introdução Aceder ao painel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92594-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="92594-109">cenário de Olá descrito neste tutorial consiste em Olá blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="92594-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="92594-110">Ativar a integração de aplicações de Olá para Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="92594-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="92594-111">Configurar início de sessão único (SSO)</span><span class="sxs-lookup"><span data-stu-id="92594-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="92594-112">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="92594-112">Configuring user provisioning</span></span>
* <span data-ttu-id="92594-113">Atribuir utilizadores</span><span class="sxs-lookup"><span data-stu-id="92594-113">Assigning users</span></span>

<span data-ttu-id="92594-114">![Cenário](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "cenário")</span><span class="sxs-lookup"><span data-stu-id="92594-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="92594-115">Ativar a integração de aplicação Olá para Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="92594-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="92594-116">o objetivo desta secção Olá é toooutline como integração de aplicações de Olá tooenable para Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="92594-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="92594-117">**integração de aplicações de Olá tooenable para Cisco Webex, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="92594-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="92594-118">No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92594-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="92594-119">![Do Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "do Active Directory")</span><span class="sxs-lookup"><span data-stu-id="92594-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="92594-120">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="92594-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="92594-121">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="92594-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="92594-122">![Aplicações](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "aplicações")</span><span class="sxs-lookup"><span data-stu-id="92594-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="92594-123">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="92594-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="92594-124">![Adicionar aplicação](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Adicionar aplicação")</span><span class="sxs-lookup"><span data-stu-id="92594-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="92594-125">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="92594-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="92594-126">![Adicionar uma aplicação de gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "adicionar uma aplicação de gallerry")</span><span class="sxs-lookup"><span data-stu-id="92594-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="92594-127">No Olá **caixa pesquisa**, tipo **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="92594-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="92594-128">![Galeria de aplicações](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galeria de aplicações")</span><span class="sxs-lookup"><span data-stu-id="92594-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="92594-129">No painel de resultados de Olá, selecione **Cisco Webex**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="92594-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="92594-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="92594-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="92594-131">Configurar o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="92594-131">Configure single sign-on</span></span>

<span data-ttu-id="92594-132">o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooCisco Webex à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.</span><span class="sxs-lookup"><span data-stu-id="92594-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="92594-133">Como parte deste procedimento, é necessário toocreate um certificado codificado base-64.</span><span class="sxs-lookup"><span data-stu-id="92594-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="92594-134">Se não estiver familiarizado com este procedimento, consulte [como tooconvert um binário de certificado para um ficheiro de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="92594-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="92594-135">**tooconfigure único início de sessão, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="92594-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="92594-136">No Olá portal clássico do Azure, no Olá **Cisco Webex** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="92594-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="92594-137">![Configurar o início de sessão único](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="92594-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="92594-138">No Olá **como seria, como os utilizadores toosign no tooCisco Webex** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="92594-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="92594-139">![Configurar o início de sessão único](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="92594-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="92594-140">No Olá **URL da aplicação configurar** página, execute os seguintes passos de Olá e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="92594-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="92594-141">![Configurar o URL da aplicação](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="92594-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="92594-142">No Olá **iniciar sessão no URL** caixa de texto, escreva o URL de inquilino Cisco Webex (por ex.: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="92594-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="92594-143">No Olá **URL de resposta do Cisco Webex** caixa de texto, tipo sua **Cisco Webex AssertionConsumerService URL** (por ex.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="92594-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="92594-144">No Olá **configurar o início de sessão único em Cisco Webex** página, toodownload o certificado, clique em **Transferir certificado**e, em seguida, guarde o ficheiro de certificado Olá no seu computador.</span><span class="sxs-lookup"><span data-stu-id="92594-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="92594-145">![Configurar o início de sessão único](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="92594-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="92594-146">Numa janela do browser web diferente, inicie sessão no site da sua empresa Cisco Webex como administrador.</span><span class="sxs-lookup"><span data-stu-id="92594-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="92594-147">No menu de Olá na parte superior do Olá, clique em **administração de sites**.</span><span class="sxs-lookup"><span data-stu-id="92594-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="92594-148">![Administração de sites](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "administração de sites")</span><span class="sxs-lookup"><span data-stu-id="92594-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="92594-149">No Olá **Gerir Site** secção, clique em **SSO configuração**.</span><span class="sxs-lookup"><span data-stu-id="92594-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="92594-150">![Configuração de SSO](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO configuração")</span><span class="sxs-lookup"><span data-stu-id="92594-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="92594-151">Na secção de configuração de SSO Web Federado Olá, efetue Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="92594-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="92594-152">![Federado SSO configuração](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "federado SSO configuração")</span><span class="sxs-lookup"><span data-stu-id="92594-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="92594-153">De Olá **protocolo Federation** lista, selecione **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="92594-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="92594-154">Criar um **com codificação Base 64** ficheiro a partir do seu certificado transferido.</span><span class="sxs-lookup"><span data-stu-id="92594-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="92594-155">Para obter mais detalhes, consulte [como tooconvert um binário de certificado para um ficheiro de texto](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="92594-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="92594-156">Abra o certificado codificado base-64 no bloco de notas e, em seguida, Olá copiar conteúdo do mesmo.</span><span class="sxs-lookup"><span data-stu-id="92594-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="92594-157">Clique em **importar metadados de SAML**e, em seguida, cole o certificado codificado base-64.</span><span class="sxs-lookup"><span data-stu-id="92594-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="92594-158">No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Cisco Webex** página da caixa de diálogo, Olá cópia **URL do emissor** valor e, em seguida, cole-o Olá **emissor para SAML (IdP ID)** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="92594-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="92594-159">No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Cisco Webex** página da caixa de diálogo, Olá cópia **URL de início de sessão remoto** valor e, em seguida, cole-o Olá **o início de sessão do cliente SSO serviço URL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="92594-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="92594-160">De Olá **NameID formato** lista, selecione **endereço de correio eletrónico**.</span><span class="sxs-lookup"><span data-stu-id="92594-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="92594-161">No Olá **AuthnContextClassRef** caixa de texto, tipo **urn: oasis: os nomes: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="92594-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="92594-162">No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Cisco Webex** página da caixa de diálogo, Olá cópia **URL de fim de sessão remoto** valor e, em seguida, cole-o Olá **fim de sessão do cliente SSO serviço URL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="92594-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="92594-163">Clique em **atualização**.</span><span class="sxs-lookup"><span data-stu-id="92594-163">Click **Update**.</span></span>
9. <span data-ttu-id="92594-164">No Olá portal clássico do Azure, no Olá **configurar o início de sessão único em Cisco Webex** página da caixa de diálogo, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída**.</span><span class="sxs-lookup"><span data-stu-id="92594-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="92594-165">![Configurar o início de sessão único](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="92594-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="92594-166">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="92594-166">Configure user provisioning</span></span>

<span data-ttu-id="92594-167">Na ordem tooenable do Azure AD os utilizadores toolog para Cisco Webex, têm de ser aprovisionados para Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="92594-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="92594-168">No caso de Olá da Cisco Webex, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="92594-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="92594-169">**executar de contas de utilizador, tooprovision Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="92594-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="92594-170">Inicie sessão no tooyour **Cisco Webex** inquilino.</span><span class="sxs-lookup"><span data-stu-id="92594-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="92594-171">Aceda demasiado**gerir utilizadores \> adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="92594-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="92594-172">![Adicionar utilizadores](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "adicionar utilizadores")</span><span class="sxs-lookup"><span data-stu-id="92594-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="92594-173">Na secção de adicionar utilizador Olá, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="92594-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="92594-174">![Adicionar utilizador](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "adicionar utilizador")</span><span class="sxs-lookup"><span data-stu-id="92594-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="92594-175">Como **tipo de conta**, selecione **anfitrião**.</span><span class="sxs-lookup"><span data-stu-id="92594-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="92594-176">Escreva as informações de Olá de um utilizador do Azure AD existente no Olá seguintes caixas de texto: **nome próprio, apelido**, **nome de utilizador**, **E-Mail**, **depalavra-passe**, **Confirmar palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="92594-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="92594-177">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="92594-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="92594-178">Pode utilizar quaisquer outras Cisco Webex utilizador conta criação ferramentas ou APIs fornecidas pelo Cisco Webex tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="92594-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="92594-179">Atribuir utilizadores</span><span class="sxs-lookup"><span data-stu-id="92594-179">Assign users</span></span>
<span data-ttu-id="92594-180">tootest a configuração, terá de toogrant Olá do Azure AD utilizadores tooallow utilizando o tooit de acesso de aplicação atribuindo-los.</span><span class="sxs-lookup"><span data-stu-id="92594-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="92594-181">**tooassign utilizadores tooCisco Webex, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="92594-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="92594-182">Olá portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="92594-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="92594-183">No Olá **Cisco Webex** página de integração de aplicações, clique em **atribuir utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="92594-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="92594-184">![Atribuir utilizadores](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "atribuir utilizadores")</span><span class="sxs-lookup"><span data-stu-id="92594-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="92594-185">Selecione o utilizador de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm a atribuição.</span><span class="sxs-lookup"><span data-stu-id="92594-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="92594-186">![Sim](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="92594-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="92594-187">Se quiser tootest as definições de início de sessão único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="92594-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="92594-188">Para obter mais detalhes sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92594-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

