---
title: "Do Azure Active Directory B2C: Exemplos de API relatórios de utilização e as definições | Microsoft Docs"
description: "Guia e exemplos sobre a obtenção de relatórios no inquilino do Azure AD B2C utilizadores, as autenticações e autenticações multifator"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="029c2-103">Ao aceder aos relatórios de utilização no Azure AD B2C através de Olá API do relatório</span><span class="sxs-lookup"><span data-stu-id="029c2-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="029c2-104">O Azure Active Directory B2C (Azure AD B2C) fornece autenticação com base na sessão do utilizador e do Azure multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="029c2-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="029c2-105">A autenticação é fornecida para os utilizadores finais da sua família de aplicações através de fornecedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="029c2-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="029c2-106">Quando souber o número de Olá de utilizadores registados no inquilino Olá, fornecedores de Olá utilizaram tooregister e número de autenticações de Olá por tipo, pode responder a perguntas como:</span><span class="sxs-lookup"><span data-stu-id="029c2-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="029c2-107">Quantos utilizadores a partir de cada tipo de fornecedor de identidade (por exemplo, uma conta Microsoft ou LinkedIn) registou no Olá últimos 10 dias?</span><span class="sxs-lookup"><span data-stu-id="029c2-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="029c2-108">Quantos autenticações utilizando o multi-factor Authentication foram concluídos com êxito no Olá último mês?</span><span class="sxs-lookup"><span data-stu-id="029c2-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="029c2-109">Autenticações de início de sessão baseada em quantos foram concluídas deste mês?</span><span class="sxs-lookup"><span data-stu-id="029c2-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="029c2-110">Por dia?</span><span class="sxs-lookup"><span data-stu-id="029c2-110">Per day?</span></span> <span data-ttu-id="029c2-111">Por aplicação?</span><span class="sxs-lookup"><span data-stu-id="029c2-111">Per application?</span></span>
* <span data-ttu-id="029c2-112">Como estimar Olá esperado custo mensal do meu atividade de inquilino do Azure AD B2C?</span><span class="sxs-lookup"><span data-stu-id="029c2-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="029c2-113">Este artigo foca-se na atividade de toobilling de relatórios associadas, que se baseia no Olá número de utilizadores, autenticações de início de sessão baseada em sujeito a faturação e autenticações multifator.</span><span class="sxs-lookup"><span data-stu-id="029c2-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="029c2-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="029c2-114">Prerequisites</span></span>
<span data-ttu-id="029c2-115">Antes de começar, terá de passos Olá toocomplete [pré-requisitos tooaccess Olá relatórios do Azure AD APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="029c2-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="029c2-116">Criar uma aplicação, obter um segredo para a mesma e conceder-aceder direitos de relatórios do inquilino tooyour do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="029c2-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="029c2-117">*Scripts de bash* e *script de Python* exemplos também são fornecidos aqui.</span><span class="sxs-lookup"><span data-stu-id="029c2-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="029c2-118">Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="029c2-118">PowerShell script</span></span>
<span data-ttu-id="029c2-119">Este script demonstra a criação de relatórios de utilização de quatro Olá utilizando Olá `TimeStamp` parâmetro e Olá `ApplicationId` filtro.</span><span class="sxs-lookup"><span data-stu-id="029c2-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="029c2-120">Definições de relatórios de utilização</span><span class="sxs-lookup"><span data-stu-id="029c2-120">Usage report definitions</span></span>
* <span data-ttu-id="029c2-121">**tenantUserCount**: Olá número de utilizadores no inquilino Olá pelo tipo de fornecedor de identidade, por dia na Olá últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="029c2-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="029c2-122">(Opcionalmente, um `TimeStamp` filtro fornece contagens de utilizadores a partir de uma data especificada toohello data atual).</span><span class="sxs-lookup"><span data-stu-id="029c2-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="029c2-123">relatório de Olá fornece:</span><span class="sxs-lookup"><span data-stu-id="029c2-123">hello report provides:</span></span>
  * <span data-ttu-id="029c2-124">**TotalUserCount**: Olá número de todos os objetos de utilizador.</span><span class="sxs-lookup"><span data-stu-id="029c2-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="029c2-125">**OtherUserCount**: Olá número de utilizadores do Azure Active Directory (não do Azure AD B2C utilizadores).</span><span class="sxs-lookup"><span data-stu-id="029c2-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="029c2-126">**LocalUserCount**: Olá número de contas de utilizador do Azure AD B2C criadas com o inquilino do Azure AD B2C de toohello local de credenciais.</span><span class="sxs-lookup"><span data-stu-id="029c2-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="029c2-127">**AlternateIdUserCount**: número de Olá de utilizadores do Azure AD B2C registado com fornecedores de identidade externas (por exemplo, Facebook, uma conta Microsoft ou outro inquilino do Azure Active Directory, também referido tooas um `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="029c2-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="029c2-128">**b2cAuthenticationCountSummary**: Resumo número Olá diária de autenticações facturável através de Olá últimos 30 dias, por dia e tipo de fluxo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="029c2-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="029c2-129">**b2cAuthenticationCount**: Olá o número de autenticações num período de tempo.</span><span class="sxs-lookup"><span data-stu-id="029c2-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="029c2-130">predefinição de Olá é Olá últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="029c2-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="029c2-131">(Opcional: Olá início e fim `TimeStamp` parâmetros definem um período de tempo específico.) inclui saída Olá `StartTimeStamp` (data mais recente da atividade para este inquilino) e `EndTimeStamp` (atualização mais recente).</span><span class="sxs-lookup"><span data-stu-id="029c2-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="029c2-132">**b2cMfaRequestCountSummary**: Resumo de Olá diária número, a autenticação multifator, por dia e tipo (voz ou de SMS).</span><span class="sxs-lookup"><span data-stu-id="029c2-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="029c2-133">Limitações</span><span class="sxs-lookup"><span data-stu-id="029c2-133">Limitations</span></span>
<span data-ttu-id="029c2-134">Dados de contagem de utilizador são atualizados a cada 24 horas too48.</span><span class="sxs-lookup"><span data-stu-id="029c2-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="029c2-135">Autenticações são atualizadas várias vezes num dia.</span><span class="sxs-lookup"><span data-stu-id="029c2-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="029c2-136">Quando utilizar Olá `ApplicationId` filtro, uma resposta vazia relatório pode ser devida tooone das seguintes condições:</span><span class="sxs-lookup"><span data-stu-id="029c2-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="029c2-137">ID da aplicação Olá não existe no inquilino Olá.</span><span class="sxs-lookup"><span data-stu-id="029c2-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="029c2-138">Certifique-se de que está correto.</span><span class="sxs-lookup"><span data-stu-id="029c2-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="029c2-139">ID da aplicação Olá existe, mas não foram encontrados dados no Olá período de relatório.</span><span class="sxs-lookup"><span data-stu-id="029c2-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="029c2-140">Reveja os parâmetros de data/hora.</span><span class="sxs-lookup"><span data-stu-id="029c2-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="029c2-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="029c2-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="029c2-142">Calcula o fatura mensal para o Azure AD</span><span class="sxs-lookup"><span data-stu-id="029c2-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="029c2-143">Quando combinada com [hello mais recente do Azure AD B2C de preços disponíveis](https://azure.microsoft.com/pricing/details/active-directory-b2c/), pode fazer a estimativa diárias, semana e mensal consumo do Azure.</span><span class="sxs-lookup"><span data-stu-id="029c2-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="029c2-144">Uma estimativa é especialmente útil ao planear as alterações no comportamento do inquilino que poderá afetar o custo global.</span><span class="sxs-lookup"><span data-stu-id="029c2-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="029c2-145">Pode rever os custos reais na sua [subscrição do Azure associada](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="029c2-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="029c2-146">Opções para outros formatos de saída</span><span class="sxs-lookup"><span data-stu-id="029c2-146">Options for other output formats</span></span>
<span data-ttu-id="029c2-147">Olá código seguinte mostra exemplos de envio tooJSON de saída, uma lista de valor de nome e XML:</span><span class="sxs-lookup"><span data-stu-id="029c2-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
