---
title: "aaaProblems tooan configurada para a palavra-passe de aplicação de galeria do Azure AD de início de sessão de sessão único-| Microsoft Docs"
description: "Aborda áreas problemáticas que fornecem orientações tootroubleshoot emite toosigning relacionado no tooAzure aplicações Galeria AD configuradas para a palavra-passe-início de sessão único"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="a9731-103">Problemas em iniciar sessão tooan configurada para a palavra-passe-início de sessão único de aplicação de galeria do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9731-103">Problems signing in tooan Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="a9731-104">Olá painel de acesso é um portal baseado na web que permitem que um utilizador que possua uma empresa ou escola da conta do Azure Active Directory (Azure AD) tooview e inicie baseado na nuvem aplicações esse administrador Olá do Azure AD concedeu-lhes acesso.</span><span class="sxs-lookup"><span data-stu-id="a9731-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="a9731-105">Um utilizador que possua as edições do Azure AD também pode utilizar grupos self-service e capacidades de gestão de aplicações através de Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a9731-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="a9731-106">Olá painel de acesso separado do Olá portal do Azure e não necessita que os utilizadores toohave uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9731-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="a9731-107">toouse baseada em palavra-passe-início de sessão único (SSO) no painel de acesso, Olá extensão do painel de acesso de Olá tem de estar instalado no browser do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="a9731-108">Esta extensão é transferida automaticamente quando um utilizador seleciona uma aplicação que está configurada para SSO baseada em palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="a9731-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="a9731-109">Que cumprem os requisitos de browser para Olá painel de acesso</span><span class="sxs-lookup"><span data-stu-id="a9731-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="a9731-110">Olá painel de acesso necessita de um browser que suporte JavaScript e ativou CSS.</span><span class="sxs-lookup"><span data-stu-id="a9731-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="a9731-111">toouse baseada em palavra-passe-início de sessão único (SSO) no painel de acesso, Olá extensão do painel de acesso de Olá tem de estar instalado no browser do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="a9731-112">Esta extensão é transferida automaticamente quando um utilizador seleciona uma aplicação que está configurada para SSO baseada em palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="a9731-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="a9731-113">Para SSO baseada em palavra-passe, podem ser browsers do utilizador final Olá:</span><span class="sxs-lookup"><span data-stu-id="a9731-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="a9731-114">Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior</span><span class="sxs-lookup"><span data-stu-id="a9731-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="a9731-115">Chrome – No Windows 7 ou posterior e no MacOS X ou posterior</span><span class="sxs-lookup"><span data-stu-id="a9731-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="a9731-116">Firefox 26.0 ou posterior – no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior</span><span class="sxs-lookup"><span data-stu-id="a9731-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="a9731-117">extensão SSO baseada em palavra-passe Olá fiquem disponíveis para Edge no Windows 10 quando as extensões de browser ficarem suportadas para o limite.</span><span class="sxs-lookup"><span data-stu-id="a9731-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="a9731-118">Como tooinstall Olá extensão de Browser do painel de acesso</span><span class="sxs-lookup"><span data-stu-id="a9731-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="a9731-119">Olá tooinstall extensão de Browser do painel de acesso, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="a9731-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="a9731-120">Abra Olá [painel de acesso](https://myapps.microsoft.com) dos browsers Olá suportado e inicie sessão como um **utilizador** no seu Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9731-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="a9731-121">Clique num **aplicação de palavra-passe SSO** no Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a9731-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="a9731-122">Olá prompt perguntar tooinstall Olá software, selecione **instalar agora**.</span><span class="sxs-lookup"><span data-stu-id="a9731-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="a9731-123">Com base no seu browser ser toohello direcionados hiperligação de transferência.</span><span class="sxs-lookup"><span data-stu-id="a9731-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="a9731-124">**Adicionar** browser de tooyour Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="a9731-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="a9731-125">Se o browser pede-lhe, selecione tooeither **ativar** ou **permitir** Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="a9731-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="a9731-126">Uma vez instalado, **reiniciar** a sessão do browser.</span><span class="sxs-lookup"><span data-stu-id="a9731-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="a9731-127">Inicie sessão no painel de acesso de Olá e veja se pode **iniciar** as aplicações de SSO de palavra-passe</span><span class="sxs-lookup"><span data-stu-id="a9731-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="a9731-128">Também pode transferir a extensão de Olá para Chrome e Firefox de hiperligações diretas Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="a9731-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="a9731-129">Extensão de painel de acesso do Chrome</span><span class="sxs-lookup"><span data-stu-id="a9731-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="a9731-130">Extensão de painel de acesso de Firefox</span><span class="sxs-lookup"><span data-stu-id="a9731-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="a9731-131">Configurar uma política de grupo para o Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a9731-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="a9731-132">Pode configurar uma política de grupo que lhe permitem extensão do tooremotely instalação Olá painel de acesso para o Internet Explorer em máquinas dos seus utilizadores.</span><span class="sxs-lookup"><span data-stu-id="a9731-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="a9731-133">Pré-requisitos de Olá incluem:</span><span class="sxs-lookup"><span data-stu-id="a9731-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="a9731-134">Configurou [serviços de domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e associar domínio de tooyour de máquinas dos seus utilizadores.</span><span class="sxs-lookup"><span data-stu-id="a9731-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="a9731-135">Tem de ter Olá "Editar as definições" permissão tooedit Olá objeto de política de grupo (GPO).</span><span class="sxs-lookup"><span data-stu-id="a9731-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="a9731-136">Por predefinição, os membros Olá seguintes grupos de segurança têm esta permissão: os administradores do domínio, administradores da empresa e proprietários de criador de política de grupo.</span><span class="sxs-lookup"><span data-stu-id="a9731-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="a9731-137">[Saiba mais](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9731-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="a9731-138">Siga o tutorial Olá [como tooDeploy Olá a extensão do painel de acesso para o Internet Explorer utilizando a política de grupo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) para instruções passo a passo sobre como tooconfigure Olá política de grupo e implementá-la toousers.</span><span class="sxs-lookup"><span data-stu-id="a9731-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="a9731-139">Resolver problemas de Olá painel de acesso no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="a9731-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="a9731-140">Siga Olá [Olá de resolução de problemas extensão do painel de acesso para o Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guia para acesso de uma ferramenta de diagnóstico e instruções passo a passo sobre como configurar a extensão de Olá de i/e.</span><span class="sxs-lookup"><span data-stu-id="a9731-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="a9731-141">Como a palavra-passe de tooconfigure único início de sessão para uma aplicação não Galeria</span><span class="sxs-lookup"><span data-stu-id="a9731-141">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="a9731-142">tooconfigure uma aplicação na galeria do Azure AD de Olá tem de:</span><span class="sxs-lookup"><span data-stu-id="a9731-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a9731-143">Adicionar uma aplicação não Galeria</span><span class="sxs-lookup"><span data-stu-id="a9731-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="a9731-144">Configurar aplicação Olá para palavra-passe-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a9731-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="a9731-145">Atribuir utilizadores toohello aplicação</span><span class="sxs-lookup"><span data-stu-id="a9731-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="a9731-146">Adicionar uma aplicação não Galeria</span><span class="sxs-lookup"><span data-stu-id="a9731-146">Add a non-gallery application</span></span>

<span data-ttu-id="a9731-147">tooadd uma aplicação Olá Galeria AD do Azure, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="a9731-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="a9731-148">Abra Olá [Portal do Azure](https://portal.azure.com) e inicie sessão como um **Administrador Global** ou **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="a9731-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="a9731-149">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a9731-150">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a9731-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a9731-151">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a9731-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a9731-152">Clique em Olá **adicionar** botão no canto superior direito de Olá no Olá **aplicações empresariais** painel</span><span class="sxs-lookup"><span data-stu-id="a9731-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="a9731-153">Clique em **aplicação não galeria.**</span><span class="sxs-lookup"><span data-stu-id="a9731-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="a9731-154">Introduza o nome de Olá da sua aplicação no Olá **nome** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a9731-154">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="a9731-155">Selecione **adicionar.**</span><span class="sxs-lookup"><span data-stu-id="a9731-155">Select **Add.**</span></span>

<span data-ttu-id="a9731-156">Após um curto período de tempo, ser painel de configuração da aplicação Olá toosee possível.</span><span class="sxs-lookup"><span data-stu-id="a9731-156">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="a9731-157">Configurar aplicação Olá para palavra-passe-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a9731-157">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="a9731-158">tooconfigure-início de sessão único para uma aplicação, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="a9731-158">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="a9731-159">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="a9731-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a9731-160">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a9731-161">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a9731-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a9731-162">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a9731-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a9731-163">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="a9731-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="a9731-164">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="a9731-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a9731-165">Selecionar aplicação Olá pretende tooconfigure-início de sessão único</span><span class="sxs-lookup"><span data-stu-id="a9731-165">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="a9731-166">Quando carrega a aplicação Olá, clique em Olá **de sessão único-** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-166">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a9731-167">Modo de Olá selecione **baseada em palavra-passe de início de sessão.**</span><span class="sxs-lookup"><span data-stu-id="a9731-167">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a9731-168">Introduza Olá **URL de início de sessão**.</span><span class="sxs-lookup"><span data-stu-id="a9731-168">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="a9731-169">Este é o URL de olá onde os utilizadores introduzem as respetivas toosign no nome de utilizador e palavra-passe para.</span><span class="sxs-lookup"><span data-stu-id="a9731-169">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="a9731-170">Certifique-se de que o início de sessão Olá nos campos está visíveis no URL Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-170">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="a9731-171">Atribua utilizadores toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="a9731-171">Assign users toohello application.</span></span>

11. <span data-ttu-id="a9731-172">Além disso, também pode fornecer as credenciais em nome de utilizador de Olá, selecionar linhas Olá de utilizadores de Olá e clicando na **credenciais de atualização** e introduzindo Olá nome de utilizador e palavra-passe em nome dos utilizadores de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-172">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="a9731-173">Caso contrário, os utilizadores ser tooenter pedido Olá credenciais próprios após iniciar.</span><span class="sxs-lookup"><span data-stu-id="a9731-173">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="a9731-174">Atribuir utilizadores toohello aplicação</span><span class="sxs-lookup"><span data-stu-id="a9731-174">Assign users toohello application</span></span>

<span data-ttu-id="a9731-175">tooassign um ou mais aplicações de tooan utilizadores diretamente, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="a9731-175">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="a9731-176">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="a9731-176">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a9731-177">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-177">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a9731-178">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a9731-178">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a9731-179">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a9731-179">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a9731-180">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="a9731-180">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="a9731-181">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="a9731-181">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a9731-182">Selecione aplicação Olá pretende tooassign uma lista de Olá de toofrom do utilizador.</span><span class="sxs-lookup"><span data-stu-id="a9731-182">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="a9731-183">Quando carrega a aplicação Olá, clique em **utilizadores e grupos** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="a9731-183">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a9731-184">Clique em Olá **adicionar** botão por cima Olá **utilizadores e grupos** Olá de tooopen lista **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="a9731-184">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a9731-185">Clique em Olá **utilizadores e grupos** Seletor de Olá **adicionar atribuição** painel.</span><span class="sxs-lookup"><span data-stu-id="a9731-185">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a9731-186">Tipo de Olá **nome completo** ou **endereço de correio eletrónico** do utilizador Olá estiver interessado em atribuir para Olá **pesquisa por nome ou endereço de e-mail** caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a9731-186">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a9731-187">Coloque o cursor sobre Olá **utilizador** no Olá lista tooreveal um **caixa de verificação**.</span><span class="sxs-lookup"><span data-stu-id="a9731-187">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="a9731-188">Clique em tooadd de fotografias ou logótipo do perfil do Olá caixa de verificação seguinte toohello utilizador seu utilizador toohello **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="a9731-188">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="a9731-189">**Opcional:** se gostaria demasiado**adicionar mais do que um utilizador**, tipo noutra **nome completo** ou **endereço de correio eletrónico** para Olá **pesquisar por nome ou o endereço de correio eletrónico** caixa de pesquisa e clique em Olá caixa de verificação tooadd toohello este utilizador **selecionados** lista.</span><span class="sxs-lookup"><span data-stu-id="a9731-189">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="a9731-190">Quando tiver terminado de selecionar utilizadores, clique em Olá **selecione** botão tooadd-los toohello lista de utilizadores e grupos toobe atribuído toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="a9731-190">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="a9731-191">**Opcional:** clique Olá **selecionar função** Seletor no Olá **adicionar atribuição** painel tooselect uma função tooassign toohello utilizadores que selecionou.</span><span class="sxs-lookup"><span data-stu-id="a9731-191">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="a9731-192">Clique em Olá **atribuir** botão tooassign Olá aplicação toohello utilizadores selecionados.</span><span class="sxs-lookup"><span data-stu-id="a9731-192">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="a9731-193">Após um curto período de tempo, os utilizadores Olá que selecionou ser capaz de toolaunch estas aplicações em Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="a9731-193">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="a9731-194">Se estes passos de resolução de problemas não Olá resolver o problema de Olá</span><span class="sxs-lookup"><span data-stu-id="a9731-194">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="a9731-195">Abra um pedido de suporte com Olá se disponíveis os seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="a9731-195">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="a9731-196">ID de correlação de erro</span><span class="sxs-lookup"><span data-stu-id="a9731-196">Correlation error ID</span></span>

-   <span data-ttu-id="a9731-197">UPN (endereço de e-mail do utilizador)</span><span class="sxs-lookup"><span data-stu-id="a9731-197">UPN (user email address)</span></span>

-   <span data-ttu-id="a9731-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="a9731-198">TenantID</span></span>

-   <span data-ttu-id="a9731-199">Tipo de browser</span><span class="sxs-lookup"><span data-stu-id="a9731-199">Browser type</span></span>

-   <span data-ttu-id="a9731-200">Fuso horário e tempo/período de tempo durante o erro ocorre</span><span class="sxs-lookup"><span data-stu-id="a9731-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="a9731-201">Rastreios de fiddler</span><span class="sxs-lookup"><span data-stu-id="a9731-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9731-202">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a9731-202">Next steps</span></span>
[<span data-ttu-id="a9731-203">Fornecer aplicações de tooyour de início de sessão único com o Proxy da aplicação</span><span class="sxs-lookup"><span data-stu-id="a9731-203">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

