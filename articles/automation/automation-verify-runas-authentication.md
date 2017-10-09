---
title: "configuração de conta de automatização do Azure aaaValidate | Microsoft Docs"
description: "Este artigo descreve como configuração de Olá tooconfirm da sua conta de automatização está configurada corretamente."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a>Testar a autenticação da conta Run As de Automatização do Azure
Depois de uma conta de automatização é criada com êxito, pode realizar uma tooconfirm de teste simples poderá toosuccessfully autenticar no Azure Resource Manager ou implementação clássica do Azure com a conta Run As de automatização recentemente criada ou actualizada.    

## <a name="automation-run-as-authentication"></a>Autenticação Run As de Automatização
Utilizar o código de exemplo de Olá abaixo demasiado[criar um runbook de PowerShell](automation-creating-importing-runbook.md) autenticação tooverify utilizando Olá executado como conta e também no seu tooauthenticate runbooks personalizados e gerir recursos do Resource Manager com a sua conta de automatização.   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

Tenha em atenção Olá cmdlet utilizado para autenticar no runbook Olá - **Add-AzureRmAccount**, utiliza Olá *ServicePrincipalCertificate* conjunto de parâmetros.  Autentica utilizando o certificado de serviço principal, não as credenciais.  

Quando a [executar Olá runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate a conta Run As, um [tarefa de runbook](automation-runbook-execution.md) é criado, é apresentado o painel de tarefas Olá e estado da tarefa Olá apresentados na Olá **resumo da tarefa**mosaico. Estado da tarefa Olá começará como *em fila* indicando que está a aguardar para um runbook worker no Olá toobecome de nuvem disponível. Em seguida, irá mudar demasiado*inicial* quando uma função de trabalho tarefa Olá e, em seguida, *executar* quando runbook Olá, na verdade, entra em execução.  Quando tiver concluído a tarefa de runbook Olá, vemos um Estado de **concluído**.

toosee Olá resultados detalhados do runbook Olá, clique em Olá **saída** mosaico.  No Olá **saída** painel, deverá ver que foi autenticado com êxito e devolve uma lista de todos os recursos em todos os grupos de recursos na sua subscrição.  

Esqueça bloco de Olá tooremove de código de carateres começadas comentários de Olá `#Get all ARM resources from all resource groups` quando reutilizar o código de Olá para os runbooks.

## <a name="classic-run-as-authentication"></a>Autenticação Run As clássica
Utilizar o código de exemplo de Olá abaixo demasiado[criar um runbook de PowerShell](automation-creating-importing-runbook.md) tooverify autenticação utilizando Olá clássico executado como conta e também no seu tooauthenticate runbooks personalizados e gerir recursos no modelo de implementação clássica Olá.  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

Quando a [executar Olá runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate a conta Run As, um [tarefa de runbook](automation-runbook-execution.md) é criado, é apresentado o painel de tarefas Olá e estado da tarefa Olá apresentados na Olá **resumo da tarefa**mosaico. Estado da tarefa Olá começará como *em fila* indicando que está a aguardar para um runbook worker no Olá toobecome de nuvem disponível. Em seguida, irá mudar demasiado*inicial* quando uma função de trabalho tarefa Olá e, em seguida, *executar* quando runbook Olá, na verdade, entra em execução.  Quando tiver concluído a tarefa de runbook Olá, vemos um Estado de **concluído**.

toosee Olá resultados detalhados do runbook Olá, clique em Olá **saída** mosaico.  No Olá **saída** painel, deverá ver que foi autenticado com êxito e devolve uma lista de todas as VMs do Azure por VMName que são implementadas na sua subscrição.  

Esqueça tooremove Olá cmdlet **Get-AzureVM** quando reutilizar o código de Olá para os runbooks.

## <a name="next-steps"></a>Passos seguintes
* tooget iniciado com runbooks do PowerShell, consulte [o meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).
* toolearn mais informações sobre a criação de gráficos, consulte [a criação de gráficos na automatização do Azure](automation-graphical-authoring-intro.md).
