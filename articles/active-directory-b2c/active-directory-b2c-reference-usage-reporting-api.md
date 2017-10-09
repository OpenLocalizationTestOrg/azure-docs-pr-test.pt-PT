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
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Ao aceder aos relatórios de utilização no Azure AD B2C através de Olá API do relatório

O Azure Active Directory B2C (Azure AD B2C) fornece autenticação com base na sessão do utilizador e do Azure multi-factor Authentication. A autenticação é fornecida para os utilizadores finais da sua família de aplicações através de fornecedores de identidade. Quando souber o número de Olá de utilizadores registados no inquilino Olá, fornecedores de Olá utilizaram tooregister e número de autenticações de Olá por tipo, pode responder a perguntas como:
* Quantos utilizadores a partir de cada tipo de fornecedor de identidade (por exemplo, uma conta Microsoft ou LinkedIn) registou no Olá últimos 10 dias?
* Quantos autenticações utilizando o multi-factor Authentication foram concluídos com êxito no Olá último mês?
* Autenticações de início de sessão baseada em quantos foram concluídas deste mês? Por dia? Por aplicação?
* Como estimar Olá esperado custo mensal do meu atividade de inquilino do Azure AD B2C?

Este artigo foca-se na atividade de toobilling de relatórios associadas, que se baseia no Olá número de utilizadores, autenticações de início de sessão baseada em sujeito a faturação e autenticações multifator.


## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, terá de passos Olá toocomplete [pré-requisitos tooaccess Olá relatórios do Azure AD APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Criar uma aplicação, obter um segredo para a mesma e conceder-aceder direitos de relatórios do inquilino tooyour do Azure AD B2C. *Scripts de bash* e *script de Python* exemplos também são fornecidos aqui. 

## <a name="powershell-script"></a>Script do PowerShell
Este script demonstra a criação de relatórios de utilização de quatro Olá utilizando Olá `TimeStamp` parâmetro e Olá `ApplicationId` filtro.

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


## <a name="usage-report-definitions"></a>Definições de relatórios de utilização
* **tenantUserCount**: Olá número de utilizadores no inquilino Olá pelo tipo de fornecedor de identidade, por dia na Olá últimos 30 dias. (Opcionalmente, um `TimeStamp` filtro fornece contagens de utilizadores a partir de uma data especificada toohello data atual). relatório de Olá fornece:
  * **TotalUserCount**: Olá número de todos os objetos de utilizador.
  * **OtherUserCount**: Olá número de utilizadores do Azure Active Directory (não do Azure AD B2C utilizadores).
  * **LocalUserCount**: Olá número de contas de utilizador do Azure AD B2C criadas com o inquilino do Azure AD B2C de toohello local de credenciais.

* **AlternateIdUserCount**: número de Olá de utilizadores do Azure AD B2C registado com fornecedores de identidade externas (por exemplo, Facebook, uma conta Microsoft ou outro inquilino do Azure Active Directory, também referido tooas um `OrgId`).

* **b2cAuthenticationCountSummary**: Resumo número Olá diária de autenticações facturável através de Olá últimos 30 dias, por dia e tipo de fluxo de autenticação.

* **b2cAuthenticationCount**: Olá o número de autenticações num período de tempo. predefinição de Olá é Olá últimos 30 dias.  (Opcional: Olá início e fim `TimeStamp` parâmetros definem um período de tempo específico.) inclui saída Olá `StartTimeStamp` (data mais recente da atividade para este inquilino) e `EndTimeStamp` (atualização mais recente).

* **b2cMfaRequestCountSummary**: Resumo de Olá diária número, a autenticação multifator, por dia e tipo (voz ou de SMS).


## <a name="limitations"></a>Limitações
Dados de contagem de utilizador são atualizados a cada 24 horas too48. Autenticações são atualizadas várias vezes num dia. Quando utilizar Olá `ApplicationId` filtro, uma resposta vazia relatório pode ser devida tooone das seguintes condições:
  * ID da aplicação Olá não existe no inquilino Olá. Certifique-se de que está correto.
  * ID da aplicação Olá existe, mas não foram encontrados dados no Olá período de relatório. Reveja os parâmetros de data/hora.


## <a name="next-steps"></a>Passos seguintes
### <a name="monthly-bill-estimates-for-azure-ad"></a>Calcula o fatura mensal para o Azure AD
Quando combinada com [hello mais recente do Azure AD B2C de preços disponíveis](https://azure.microsoft.com/pricing/details/active-directory-b2c/), pode fazer a estimativa diárias, semana e mensal consumo do Azure.  Uma estimativa é especialmente útil ao planear as alterações no comportamento do inquilino que poderá afetar o custo global. Pode rever os custos reais na sua [subscrição do Azure associada](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Opções para outros formatos de saída
Olá código seguinte mostra exemplos de envio tooJSON de saída, uma lista de valor de nome e XML:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
