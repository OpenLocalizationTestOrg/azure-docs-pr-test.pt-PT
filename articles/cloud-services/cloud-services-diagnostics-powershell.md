---
title: "diagnóstico de aaaEnable nos serviços de nuvem do Azure com o PowerShell | Microsoft Docs"
description: "Saiba como tooenable diagnóstico para a nuvem de serviços com o PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="ba104-103">Ativar o diagnóstico nos serviços de nuvem do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba104-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="ba104-104">É possível recolher dados de diagnóstico, como os registos de aplicações, etc. a partir de um serviço em nuvem, utilizando os contadores de desempenho Olá extensão de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba104-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="ba104-105">Este artigo descreve como tooenable hello a extensão de diagnóstico do Azure para um serviço em nuvem com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba104-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="ba104-106">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para pré-requisitos Olá necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="ba104-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="ba104-107">Ativar a extensão de diagnóstico como parte da implementação de um Serviço Cloud</span><span class="sxs-lookup"><span data-stu-id="ba104-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="ba104-108">Esta abordagem é o tipo de integração de toocontinuous aplicável dos cenários, onde o diagnóstico de Olá extensão pode ser ativada como parte da implementação Olá serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ba104-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="ba104-109">Ao criar uma nova implementação de serviço em nuvem pode ativar a extensão de diagnóstico de Olá mediante a transmissão no Olá *ExtensionConfiguration* parâmetro toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba104-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="ba104-110">Olá *ExtensionConfiguration* parâmetro assume uma matriz de configurações de diagnóstico que podem ser criadas utilizando Olá [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba104-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="ba104-111">Olá exemplo seguinte mostra como pode ativar o diagnóstico num serviço em nuvem com um WebRole e WorkerRole, cada um com uma configuração de diagnósticos diferentes.</span><span class="sxs-lookup"><span data-stu-id="ba104-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

<span data-ttu-id="ba104-112">Se o ficheiro de configuração de diagnósticos de Olá Especifica um `StorageAccount` elemento com um nome de conta de armazenamento, em seguida, Olá `New-AzureServiceDiagnosticsExtensionConfig` cmdlet automaticamente irá utilizar essa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ba104-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="ba104-113">Para este toowork, conta de armazenamento Olá tem toobe no Olá mesma subscrição, conforme Olá serviço em nuvem que está a ser implementada.</span><span class="sxs-lookup"><span data-stu-id="ba104-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="ba104-114">Do Azure SDK 2.6 publicar ficheiros de configuração de extensão de Olá onward gerados pelo Olá MSBuild saída do destino irão incluir o nome da conta de armazenamento de Olá com base na cadeia de configuração de diagnósticos de Olá especificada no ficheiro de configuração de serviço Olá (. cscfg).</span><span class="sxs-lookup"><span data-stu-id="ba104-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="ba104-115">script de Olá abaixo mostra como os ficheiros de configuração do tooparse Olá extensão de Olá publicar o resultado de destino e configurar a extensão de diagnóstico para cada função quando implementar o serviço em nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="ba104-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

<span data-ttu-id="ba104-116">Visual Studio Online utiliza uma abordagem semelhante para implementações automatizadas dos serviços em nuvem com a extensão de diagnóstico de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba104-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="ba104-117">Consulte [publicar AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) para obter um exemplo completo.</span><span class="sxs-lookup"><span data-stu-id="ba104-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="ba104-118">Se não `StorageAccount` foi especificado na configuração de diagnósticos de Olá, em seguida, terá de toopass no Olá *StorageAccountName* parâmetro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba104-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="ba104-119">Se hello *StorageAccountName* parâmetro for especificado, em seguida, Olá cmdlet irá utilizar sempre a conta de armazenamento Olá, que é especificada no parâmetro de Olá e não Olá aquele que está especificado no ficheiro de configuração de diagnósticos de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba104-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="ba104-120">Se passar diagnóstico Olá conta de armazenamento está numa subscrição diferente de Olá serviço em nuvem, em seguida, terá de tooexplicitly Olá *StorageAccountName* e *StorageAccountKey* parâmetros toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba104-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="ba104-121">Olá *StorageAccountKey* parâmetro não é necessária quando o diagnóstico de Olá conta de armazenamento está a ser Olá mesma subscrição, conforme Olá cmdlet automaticamente pode consultar e defina o valor de chave de Olá ao ativar a extensão de diagnóstico de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba104-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="ba104-122">No entanto, se Olá conta de armazenamento do diagnostics está numa subscrição diferente, em seguida, Olá cmdlet poderá não ser tooget capaz de chave de Olá automaticamente, sendo necessário tooexplicitly especificar Olá chave através de Olá *StorageAccountKey* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ba104-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="ba104-123">Ativar a extensão de diagnóstico num Serviço Cloud existente</span><span class="sxs-lookup"><span data-stu-id="ba104-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="ba104-124">Pode utilizar Olá [conjunto AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) configuração de diagnósticos de tooenable ou atualização cmdlet num serviço em nuvem que já está em execução.</span><span class="sxs-lookup"><span data-stu-id="ba104-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="ba104-125">Obter a configuração atual da extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ba104-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="ba104-126">Olá utilize [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget Olá diagnóstico configuração atual para um serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ba104-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="ba104-127">Remover a extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ba104-127">Remove diagnostics extension</span></span>
<span data-ttu-id="ba104-128">tooturn desativar diagnóstico numa nuvem de serviço pode utilizar Olá [remover AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ba104-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="ba104-129">Se tiver ativado a extensão de diagnóstico de Olá com *conjunto AzureServiceDiagnosticsExtension* ou Olá *New-AzureServiceDiagnosticsExtensionConfig* sem Olá *função* parâmetro, em seguida, que pode remover a extensão de Olá com *remover AzureServiceDiagnosticsExtension* sem Olá *função* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ba104-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="ba104-130">Se hello *função* parâmetro foi utilizado ao ativar a extensão de Olá, em seguida, este tem também de ser utilizada ao remover a extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba104-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="ba104-131">extensão de diagnóstico do Olá tooremove de cada função individual:</span><span class="sxs-lookup"><span data-stu-id="ba104-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="ba104-132">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="ba104-132">Next Steps</span></span>
* <span data-ttu-id="ba104-133">Para obter orientações adicionais sobre como utilizar o diagnóstico do Azure e outros problemas de tootroubleshoot técnicas, consulte [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ba104-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="ba104-134">Olá [esquema de configuração de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) explica Olá opções diversas configurações de xml para extensão de diagnóstico de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba104-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="ba104-135">toolearn como extensão de diagnóstico de Olá tooenable para máquinas virtuais, consulte [criar uma Máquina Virtual do Windows com a monitorização e diagnóstico com o modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="ba104-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
