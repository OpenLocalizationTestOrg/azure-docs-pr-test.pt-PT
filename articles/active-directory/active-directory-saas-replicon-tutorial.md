---
title: "Tutorial: Integração do Azure Active Directory com Replicon | Microsoft Docs"
description: "Saiba como toouse Replicon com o Azure Active Directory tooenable único início de sessão, aprovisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="d1912-103">Tutorial: Integração do Azure Active Directory com Replicon</span><span class="sxs-lookup"><span data-stu-id="d1912-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="d1912-104">o objetivo deste tutorial Olá é integração de Olá tooshow do Azure e Replicon.</span><span class="sxs-lookup"><span data-stu-id="d1912-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="d1912-105">cenário de Olá descrito neste tutorial pressupõe que já tenha Olá seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d1912-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="d1912-106">Uma subscrição do Azure válida</span><span class="sxs-lookup"><span data-stu-id="d1912-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d1912-107">Um inquilino Replicon</span><span class="sxs-lookup"><span data-stu-id="d1912-107">A Replicon tenant</span></span>

<span data-ttu-id="d1912-108">Depois de concluir este tutorial, os utilizadores Olá do Azure AD que atribuiu tooReplicon será toosingle capazes sessão numa aplicação Olá no site da sua empresa Replicon (serviço fornecedor iniciada pelo início de sessão) ou utilizar Olá [introdução toohello acesso Painel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1912-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="d1912-109">cenário de Olá descrito neste tutorial consiste em Olá blocos modulares os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d1912-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="d1912-110">Ativar a integração de aplicações de Olá para Replicon</span><span class="sxs-lookup"><span data-stu-id="d1912-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="d1912-111">Configurar início de sessão único (SSO)</span><span class="sxs-lookup"><span data-stu-id="d1912-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="d1912-112">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="d1912-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="d1912-113">Atribuir utilizadores</span><span class="sxs-lookup"><span data-stu-id="d1912-113">Assigning users</span></span>

<span data-ttu-id="d1912-114">![Cenário](./media/active-directory-saas-replicon-tutorial/IC777798.png "cenário")</span><span class="sxs-lookup"><span data-stu-id="d1912-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="d1912-115">Ativar a integração de aplicação Olá para Replicon</span><span class="sxs-lookup"><span data-stu-id="d1912-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="d1912-116">o objetivo desta secção Olá é toooutline como integração de aplicações de Olá tooenable para Replicon.</span><span class="sxs-lookup"><span data-stu-id="d1912-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="d1912-117">**integração de aplicações de Olá tooenable para Replicon, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d1912-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1912-118">No Olá portal clássico do Azure, no painel de navegação esquerdo Olá, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d1912-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="d1912-119">![Do Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "do Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d1912-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d1912-120">De Olá **diretório** lista, o diretório de Olá Selecione para o qual pretende a integração de diretórios tooenable.</span><span class="sxs-lookup"><span data-stu-id="d1912-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="d1912-121">Clique em vista de aplicações Olá tooopen, na vista de diretório Olá, **aplicações** no menu superior Olá.</span><span class="sxs-lookup"><span data-stu-id="d1912-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="d1912-122">![Aplicações](./media/active-directory-saas-replicon-tutorial/IC700994.png "aplicações")</span><span class="sxs-lookup"><span data-stu-id="d1912-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d1912-123">Clique em **adicionar** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="d1912-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="d1912-124">![Adicionar aplicação](./media/active-directory-saas-replicon-tutorial/IC749321.png "Adicionar aplicação")</span><span class="sxs-lookup"><span data-stu-id="d1912-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d1912-125">No Olá **que itens pretende toodo** caixa de diálogo, clique em **adicionar uma aplicação na Galeria de Olá**.</span><span class="sxs-lookup"><span data-stu-id="d1912-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="d1912-126">![Adicionar uma aplicação de gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "adicionar uma aplicação de gallerry")</span><span class="sxs-lookup"><span data-stu-id="d1912-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d1912-127">No Olá **caixa pesquisa**, tipo **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="d1912-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="d1912-128">![Galeria de aplicações](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galeria de aplicações")</span><span class="sxs-lookup"><span data-stu-id="d1912-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="d1912-129">No painel de resultados de Olá, selecione **Replicon**e, em seguida, clique em **concluída** aplicação de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="d1912-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="d1912-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="d1912-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d1912-131">Configurar o início de sessão único</span><span class="sxs-lookup"><span data-stu-id="d1912-131">Configure single sign-on</span></span>

<span data-ttu-id="d1912-132">o objetivo desta secção Olá é toooutline como tooenable utilizadores tooauthenticate tooReplicon à respetiva conta no Azure AD com Federação com base no protocolo SAML Olá.</span><span class="sxs-lookup"><span data-stu-id="d1912-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="d1912-133">**tooconfigure único início de sessão, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d1912-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1912-134">No Olá portal clássico do Azure, no Olá **Replicon** página de integração de aplicações, clique em **configurar o início de sessão único** tooopen Olá **configurar início de sessão único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d1912-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="d1912-135">![Configurar o início de sessão único](./media/active-directory-saas-replicon-tutorial/IC777801.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="d1912-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="d1912-136">No Olá **como seria, como os utilizadores toosign no tooReplicon** página, selecione **Microsoft Azure AD Single Sign-On**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="d1912-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="d1912-137">![Configurar o início de sessão único](./media/active-directory-saas-replicon-tutorial/IC777802.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="d1912-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="d1912-138">No Olá **URL da aplicação configurar** página, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="d1912-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="d1912-139">![Configurar o URL da aplicação](./media/active-directory-saas-replicon-tutorial/IC777803.png "configurar o URL da aplicação")</span><span class="sxs-lookup"><span data-stu-id="d1912-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="d1912-140">No Olá **Replicon no URL sessão** caixa de texto, escreva o URL de inquilino Replicon (por ex.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="d1912-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="d1912-141">No Olá **URL de resposta de Replicon** caixa de texto, escreva o seu Replicon **AssertionConsumerService** URL (por ex.: *https://global.replicon.com/! / saml2/empresa/sso/post*).</span><span class="sxs-lookup"><span data-stu-id="d1912-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="d1912-142">Pode obter Olá URL de metadados de Replicon Olá em: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="d1912-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="d1912-143">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="d1912-143">Click **Next**.</span></span>

4. <span data-ttu-id="d1912-144">No Olá **configurar o início de sessão único em Replicon** página, toodownload os seus metadados, clique em **transferir metadados**e, em seguida, guarde Olá metadados no seu computador.</span><span class="sxs-lookup"><span data-stu-id="d1912-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="d1912-145">![Configurar o início de sessão único](./media/active-directory-saas-replicon-tutorial/IC777804.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="d1912-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="d1912-146">Numa janela do browser web diferente, inicie sessão no site da sua empresa Replicon como administrador.</span><span class="sxs-lookup"><span data-stu-id="d1912-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="d1912-147">tooconfigure SAML 2.0, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="d1912-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="d1912-148">![Ativar a autenticação SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "autenticação ativar SAML")</span><span class="sxs-lookup"><span data-stu-id="d1912-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="d1912-149">Olá toodisplay **EnableSAML Authentication2** caixa de diálogo, acrescentar Olá os seguintes tooyour URL, após a sua chave de empresa: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="d1912-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="d1912-150">seguinte Olá mostra esquema Olá do URL de conclusão de Olá:</span><span class="sxs-lookup"><span data-stu-id="d1912-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="d1912-151">**https://Na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="d1912-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="d1912-152">Clique em Olá  **+**  tooexpand Olá **v20Configuration** secção.</span><span class="sxs-lookup"><span data-stu-id="d1912-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="d1912-153">Clique em Olá  **+**  tooexpand Olá **metaDataConfiguration** secção.</span><span class="sxs-lookup"><span data-stu-id="d1912-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="d1912-154">Clique em **Escolher ficheiro**, tooselect o ficheiro de XML de metadados de fornecedor de identidade e clique em **submeter**.</span><span class="sxs-lookup"><span data-stu-id="d1912-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="d1912-155">No portal clássico do Azure Olá, selecione a confirmação de configuração de início de sessão único Olá e, em seguida, clique em **concluída** tooclose Olá **configurar início de sessão único** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d1912-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="d1912-156">![Configurar o início de sessão único](./media/active-directory-saas-replicon-tutorial/IC778418.png "configurar o início de sessão único")</span><span class="sxs-lookup"><span data-stu-id="d1912-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="d1912-157">Configurar o aprovisionamento de utilizadores</span><span class="sxs-lookup"><span data-stu-id="d1912-157">Configure user provisioning</span></span>

<span data-ttu-id="d1912-158">Na ordem tooenable do Azure AD os utilizadores toolog para Replicon, têm de ser aprovisionados para Replicon.</span><span class="sxs-lookup"><span data-stu-id="d1912-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="d1912-159">No caso de Olá da Replicon, o aprovisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="d1912-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="d1912-160">**tooconfigure aprovisionamento de utilizadores, execute Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d1912-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1912-161">Numa janela do browser web, inicie sessão no site da sua empresa Replicon como administrador.</span><span class="sxs-lookup"><span data-stu-id="d1912-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="d1912-162">Aceda demasiado**administração \> utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="d1912-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="d1912-163">![Os utilizadores](./media/active-directory-saas-replicon-tutorial/IC777806.png "utilizadores")</span><span class="sxs-lookup"><span data-stu-id="d1912-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="d1912-164">Clique em **+ adicionar utilizador**.</span><span class="sxs-lookup"><span data-stu-id="d1912-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="d1912-165">![Adicionar utilizador](./media/active-directory-saas-replicon-tutorial/IC777807.png "adicionar utilizador")</span><span class="sxs-lookup"><span data-stu-id="d1912-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="d1912-166">No Olá **perfil de utilizador** secção, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="d1912-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="d1912-167">![Perfil de utilizador](./media/active-directory-saas-replicon-tutorial/IC777808.png "perfil de utilizador")</span><span class="sxs-lookup"><span data-stu-id="d1912-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="d1912-168">No Olá **nome de início de sessão** caixa de texto, Olá de tipo do Azure AD endereço de e-mail do utilizador Olá do Azure AD que pretende tooprovision.</span><span class="sxs-lookup"><span data-stu-id="d1912-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="d1912-169">Como **tipo de autenticação**, selecione **SSO**.</span><span class="sxs-lookup"><span data-stu-id="d1912-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="d1912-170">No Olá **departamento** caixa de texto, escreva o departamento de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="d1912-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="d1912-171">Como **empregado tipo**, selecione **administrador**.</span><span class="sxs-lookup"><span data-stu-id="d1912-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="d1912-172">Clique em **guardar o perfil de utilizador**.</span><span class="sxs-lookup"><span data-stu-id="d1912-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="d1912-173">Pode utilizar quaisquer outras Replicon utilizador conta criação ferramentas ou APIs fornecidas pelo Replicon tooprovision contas de utilizador do AAD.</span><span class="sxs-lookup"><span data-stu-id="d1912-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="d1912-174">Atribuir utilizadores</span><span class="sxs-lookup"><span data-stu-id="d1912-174">Assign users</span></span>
<span data-ttu-id="d1912-175">tootest a configuração, terá de toogrant Olá do Azure AD utilizadores tooallow utilizando o tooit de acesso de aplicação atribuindo-los.</span><span class="sxs-lookup"><span data-stu-id="d1912-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="d1912-176">**tooassign tooReplicon de utilizadores, efetuar Olá os seguintes passos:**</span><span class="sxs-lookup"><span data-stu-id="d1912-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1912-177">Olá portal clássico do Azure, crie uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="d1912-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="d1912-178">No Olá **Replicon** página de integração de aplicações, clique em **atribuir utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="d1912-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="d1912-179">![Atribuir utilizadores](./media/active-directory-saas-replicon-tutorial/IC777809.png "atribuir utilizadores")</span><span class="sxs-lookup"><span data-stu-id="d1912-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="d1912-180">Selecione o utilizador de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm a atribuição.</span><span class="sxs-lookup"><span data-stu-id="d1912-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="d1912-181">![Sim](./media/active-directory-saas-replicon-tutorial/IC767830.png "Sim")</span><span class="sxs-lookup"><span data-stu-id="d1912-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d1912-182">Se quiser tootest as definições de início de sessão único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="d1912-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="d1912-183">Para obter mais detalhes sobre Olá painel de acesso, consulte [introdução toohello painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d1912-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

