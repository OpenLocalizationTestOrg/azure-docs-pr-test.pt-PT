---
title: "aaaGet dados utilizando Olá API do Azure AD Reporting com certificados | Microsoft Docs"
description: "Explica como toouse Olá API do Azure AD Reporting com dados tooget de credenciais de certificado de diretórios sem intervenção do utilizador."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="c6fd4-103">Obter dados utilizando a API de relatórios do Azure AD Olá com certificados</span><span class="sxs-lookup"><span data-stu-id="c6fd4-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="c6fd4-104">Este artigo aborda como toouse Olá API do Azure AD Reporting com dados tooget de credenciais de certificado de diretórios sem intervenção do utilizador.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="c6fd4-105">Olá, utilize a API de relatórios de AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c6fd4-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="c6fd4-106">A API de relatórios de AD do Azure requer que conclua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="c6fd4-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="c6fd4-107">Pré-requisitos da instalação</span><span class="sxs-lookup"><span data-stu-id="c6fd4-107">Install prerequisites</span></span>
 *  <span data-ttu-id="c6fd4-108">Defina o certificado de Olá na sua aplicação</span><span class="sxs-lookup"><span data-stu-id="c6fd4-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="c6fd4-109">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="c6fd4-109">Get an access token</span></span>
 *  <span data-ttu-id="c6fd4-110">Utilizar Olá de token toocall de acesso de Olá Graph API</span><span class="sxs-lookup"><span data-stu-id="c6fd4-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="c6fd4-111">Para obter informações sobre o código de origem, veja [Leverage Report API Module (Tirar Partido do Módulo da API de Relatório)](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span><span class="sxs-lookup"><span data-stu-id="c6fd4-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="c6fd4-112">Pré-requisitos da instalação</span><span class="sxs-lookup"><span data-stu-id="c6fd4-112">Install prerequisites</span></span>
<span data-ttu-id="c6fd4-113">Precisa de toohave Azure AD PowerShell V2 e AzureADUtils module instalada.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="c6fd4-114">Transfira e instale o Azure AD Powershell V2, seguir instruções Olá em [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="c6fd4-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="c6fd4-115">Transferir o módulo do Azure AD Utils Olá da [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="c6fd4-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="c6fd4-116">Este módulo disponibiliza vários cmdlets de utilitário, incluindo:</span><span class="sxs-lookup"><span data-stu-id="c6fd4-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="c6fd4-117">versão mais recente do Olá da ADAL com Nuget</span><span class="sxs-lookup"><span data-stu-id="c6fd4-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="c6fd4-118">Tokens de acesso de utilizador, chaves de aplicação e certificados, através da ADAL</span><span class="sxs-lookup"><span data-stu-id="c6fd4-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="c6fd4-119">Graph API que processa resultados paginados</span><span class="sxs-lookup"><span data-stu-id="c6fd4-119">Graph API handling paged results</span></span>

<span data-ttu-id="c6fd4-120">**módulo do Azure AD Utils de Olá tooinstall:**</span><span class="sxs-lookup"><span data-stu-id="c6fd4-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="c6fd4-121">Criar um diretório toosave Olá utilitários módulo (por exemplo, c:\azureAD) e transferir o módulo Olá a partir do GitHub.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="c6fd4-122">Abra uma sessão do PowerShell e aceda diretório toohello que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="c6fd4-123">Importar o módulo Olá e instalá-la no caminho de módulo Olá PowerShell utilizando o cmdlet Olá AzureADUtilsModule de instalação.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="c6fd4-124">sessão de Olá deve ter um aspeto semelhante toothis ecrã:</span><span class="sxs-lookup"><span data-stu-id="c6fd4-124">hello session should look similar toothis screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="c6fd4-126">Defina o certificado de Olá na sua aplicação</span><span class="sxs-lookup"><span data-stu-id="c6fd4-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="c6fd4-127">Se já tiver uma aplicação, obter o ID de objeto de Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="c6fd4-129">Abra uma sessão do PowerShell e ligue tooAzure AD utilizando o cmdlet Olá Connect-AzureAD.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="c6fd4-131">Utilize o cmdlet New-AzureADApplicationCertificateCredential de Olá de AzureADUtils tooadd tooit de credencial um certificado.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="c6fd4-132">Precisa de aplicação de Olá tooprovide ID de objeto capturadas anteriormente, bem como Olá objeto certificado (obter esta utilizando Olá Cert: unidade).</span><span class="sxs-lookup"><span data-stu-id="c6fd4-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Portal do Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="c6fd4-134">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="c6fd4-134">Get an access token</span></span>

<span data-ttu-id="c6fd4-135">tooget um token de acesso, utilize o cmdlet de Get-AzureADGraphAPIAccessTokenFromCert Olá de AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="c6fd4-136">É necessário toouse Olá ID da aplicação em vez de Olá ID de objeto que utilizou na secção último Olá.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="c6fd4-138">Utilizar Olá de token toocall de acesso de Olá Graph API</span><span class="sxs-lookup"><span data-stu-id="c6fd4-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="c6fd4-139">Agora, pode criar script de Olá.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-139">Now you can create hello script.</span></span> <span data-ttu-id="c6fd4-140">Abaixo está um exemplo utilizando o cmdlet Invoke-AzureADGraphAPIQuery de Olá de Olá AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="c6fd4-141">Este cmdlet processa resultados paginados múltiplos e, em seguida, envia do pipeline de PowerShell esses resultados toohello.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="c6fd4-143">Agora está pronto tooexport tooa CSV e guardar o sistema do tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="c6fd4-144">Pode também moldar o script no tooget tarefa agendada dados do Azure AD do seu inquilino periodicamente sem ter de chaves de aplicação toostore no código de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="c6fd4-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c6fd4-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c6fd4-145">Next steps</span></span>
[<span data-ttu-id="c6fd4-146">Olá Noções básicas de gestão de identidades do Azure</span><span class="sxs-lookup"><span data-stu-id="c6fd4-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



