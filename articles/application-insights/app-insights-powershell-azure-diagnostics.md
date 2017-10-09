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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="41678-103">Utilizar o PowerShell tooset segurança Application Insights para uma aplicação web do Azure</span><span class="sxs-lookup"><span data-stu-id="41678-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="41678-104">[Microsoft Azure](https://azure.com) pode ser [configurado toosend Azure Diagnostics](app-insights-azure-diagnostics.md) demasiado[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41678-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="41678-105">diagnóstico de Olá refere-se tooAzure Cloud Services e as VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="41678-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="41678-106">Complementa a telemetria Olá que envia da aplicação Olá utilizando Olá Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="41678-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="41678-107">Como parte de automatizar o processo de Olá de criação de novos recursos no Azure, pode configurar o diagnóstico com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41678-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="41678-108">Modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="41678-108">Azure template</span></span>
<span data-ttu-id="41678-109">Se a aplicação de web de Olá está no Azure e criar os seus recursos através de um modelo Azure Resource Manager, pode configurar o Application Insights ao adicionar este nó de recursos toohello:</span><span class="sxs-lookup"><span data-stu-id="41678-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

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

* <span data-ttu-id="41678-110">`nameOfAIAppResource`-um nome para Olá recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="41678-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="41678-111">`myWebAppName`-id Olá da aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="41678-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="41678-112">Ativar a extensão de diagnóstico como parte da implementação de um Serviço Cloud</span><span class="sxs-lookup"><span data-stu-id="41678-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="41678-113">Olá `New-AzureDeployment` cmdlet tem um parâmetro `ExtensionConfiguration`, que assume uma matriz de configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="41678-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="41678-114">Estas podem ser criadas utilizando Olá `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41678-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="41678-115">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="41678-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="41678-116">Ativar a extensão de diagnóstico num Serviço Cloud existente</span><span class="sxs-lookup"><span data-stu-id="41678-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="41678-117">Num serviço existente, utilize `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="41678-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="41678-118">Obter a configuração atual da extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="41678-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="41678-119">Remover a extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="41678-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="41678-120">Se tiver ativado a extensão de diagnóstico de Olá com `Set-AzureServiceDiagnosticsExtension` ou `New-AzureServiceDiagnosticsExtensionConfig` sem o parâmetro de função Olá, em seguida, pode remover Olá extensão com `Remove-AzureServiceDiagnosticsExtension` sem o parâmetro de função Olá.</span><span class="sxs-lookup"><span data-stu-id="41678-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="41678-121">Se o parâmetro de função Olá foi utilizado ao ativar a extensão de Olá, em seguida, tem também de ser utilizado quando remover a extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="41678-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="41678-122">extensão de diagnóstico do Olá tooremove de cada função individual:</span><span class="sxs-lookup"><span data-stu-id="41678-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="41678-123">Consultar também</span><span class="sxs-lookup"><span data-stu-id="41678-123">See also</span></span>
* [<span data-ttu-id="41678-124">Monitor Azure Cloud Services apps with Application Insights (Monitorizar aplicações Serviços Cloud do Azure com o Application Insights)</span><span class="sxs-lookup"><span data-stu-id="41678-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="41678-125">Enviar diagnósticos do Azure tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="41678-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="41678-126">Automate configuring alerts (Automatizar alertas de configuração)</span><span class="sxs-lookup"><span data-stu-id="41678-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

