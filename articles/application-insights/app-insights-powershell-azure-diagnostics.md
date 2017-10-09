---
title: aaaUsing PowerShell toosetup Application Insights numa do Azure | Microsoft Docs
description: "Automatizar tooApplication configurar diagnósticos do Azure de toopipe Insights."
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Utilizar o PowerShell tooset segurança Application Insights para uma aplicação web do Azure
[Microsoft Azure](https://azure.com) pode ser [configurado toosend Azure Diagnostics](app-insights-azure-diagnostics.md) demasiado[Azure Application Insights](app-insights-overview.md). diagnóstico de Olá refere-se tooAzure Cloud Services e as VMs do Azure. Complementa a telemetria Olá que envia da aplicação Olá utilizando Olá Application Insights SDK. Como parte de automatizar o processo de Olá de criação de novos recursos no Azure, pode configurar o diagnóstico com o PowerShell.

## <a name="azure-template"></a>Modelo do Azure
Se a aplicação de web de Olá está no Azure e criar os seus recursos através de um modelo Azure Resource Manager, pode configurar o Application Insights ao adicionar este nó de recursos toohello:

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* `nameOfAIAppResource`-um nome para Olá recurso do Application Insights
* `myWebAppName`-id Olá da aplicação web de Olá

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Ativar a extensão de diagnóstico como parte da implementação de um Serviço Cloud
Olá `New-AzureDeployment` cmdlet tem um parâmetro `ExtensionConfiguration`, que assume uma matriz de configurações de diagnóstico. Estas podem ser criadas utilizando Olá `New-AzureServiceDiagnosticsExtensionConfig` cmdlet. Por exemplo:

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Ativar a extensão de diagnóstico num Serviço Cloud existente
Num serviço existente, utilize `Set-AzureServiceDiagnosticsExtension`.

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a>Obter a configuração atual da extensão de diagnóstico
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Remover a extensão de diagnóstico
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Se tiver ativado a extensão de diagnóstico de Olá com `Set-AzureServiceDiagnosticsExtension` ou `New-AzureServiceDiagnosticsExtensionConfig` sem o parâmetro de função Olá, em seguida, pode remover Olá extensão com `Remove-AzureServiceDiagnosticsExtension` sem o parâmetro de função Olá. Se o parâmetro de função Olá foi utilizado ao ativar a extensão de Olá, em seguida, tem também de ser utilizado quando remover a extensão de Olá.

extensão de diagnóstico do Olá tooremove de cada função individual:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Consultar também
* [Monitor Azure Cloud Services apps with Application Insights (Monitorizar aplicações Serviços Cloud do Azure com o Application Insights)](app-insights-cloudservices.md)
* [Enviar diagnósticos do Azure tooApplication Insights](app-insights-azure-diagnostics.md)
* [Automate configuring alerts (Automatizar alertas de configuração)](app-insights-powershell-alerts.md)

