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
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>Ativar o diagnóstico nos serviços de nuvem do Azure com o PowerShell
É possível recolher dados de diagnóstico, como os registos de aplicações, etc. a partir de um serviço em nuvem, utilizando os contadores de desempenho Olá extensão de diagnóstico do Azure. Este artigo descreve como tooenable hello a extensão de diagnóstico do Azure para um serviço em nuvem com o PowerShell.  Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para pré-requisitos Olá necessários para este artigo.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Ativar a extensão de diagnóstico como parte da implementação de um Serviço Cloud
Esta abordagem é o tipo de integração de toocontinuous aplicável dos cenários, onde o diagnóstico de Olá extensão pode ser ativada como parte da implementação Olá serviço em nuvem. Ao criar uma nova implementação de serviço em nuvem pode ativar a extensão de diagnóstico de Olá mediante a transmissão no Olá *ExtensionConfiguration* parâmetro toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet. Olá *ExtensionConfiguration* parâmetro assume uma matriz de configurações de diagnóstico que podem ser criadas utilizando Olá [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.

Olá exemplo seguinte mostra como pode ativar o diagnóstico num serviço em nuvem com um WebRole e WorkerRole, cada um com uma configuração de diagnósticos diferentes.

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

Se o ficheiro de configuração de diagnósticos de Olá Especifica um `StorageAccount` elemento com um nome de conta de armazenamento, em seguida, Olá `New-AzureServiceDiagnosticsExtensionConfig` cmdlet automaticamente irá utilizar essa conta de armazenamento. Para este toowork, conta de armazenamento Olá tem toobe no Olá mesma subscrição, conforme Olá serviço em nuvem que está a ser implementada.

Do Azure SDK 2.6 publicar ficheiros de configuração de extensão de Olá onward gerados pelo Olá MSBuild saída do destino irão incluir o nome da conta de armazenamento de Olá com base na cadeia de configuração de diagnósticos de Olá especificada no ficheiro de configuração de serviço Olá (. cscfg). script de Olá abaixo mostra como os ficheiros de configuração do tooparse Olá extensão de Olá publicar o resultado de destino e configurar a extensão de diagnóstico para cada função quando implementar o serviço em nuvem Olá.

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

Visual Studio Online utiliza uma abordagem semelhante para implementações automatizadas dos serviços em nuvem com a extensão de diagnóstico de Olá. Consulte [publicar AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) para obter um exemplo completo.

Se não `StorageAccount` foi especificado na configuração de diagnósticos de Olá, em seguida, terá de toopass no Olá *StorageAccountName* parâmetro toohello cmdlet. Se hello *StorageAccountName* parâmetro for especificado, em seguida, Olá cmdlet irá utilizar sempre a conta de armazenamento Olá, que é especificada no parâmetro de Olá e não Olá aquele que está especificado no ficheiro de configuração de diagnósticos de Olá.

Se passar diagnóstico Olá conta de armazenamento está numa subscrição diferente de Olá serviço em nuvem, em seguida, terá de tooexplicitly Olá *StorageAccountName* e *StorageAccountKey* parâmetros toohello cmdlet. Olá *StorageAccountKey* parâmetro não é necessária quando o diagnóstico de Olá conta de armazenamento está a ser Olá mesma subscrição, conforme Olá cmdlet automaticamente pode consultar e defina o valor de chave de Olá ao ativar a extensão de diagnóstico de Olá. No entanto, se Olá conta de armazenamento do diagnostics está numa subscrição diferente, em seguida, Olá cmdlet poderá não ser tooget capaz de chave de Olá automaticamente, sendo necessário tooexplicitly especificar Olá chave através de Olá *StorageAccountKey* parâmetro.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Ativar a extensão de diagnóstico num Serviço Cloud existente
Pode utilizar Olá [conjunto AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) configuração de diagnósticos de tooenable ou atualização cmdlet num serviço em nuvem que já está em execução.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>Obter a configuração atual da extensão de diagnóstico
Olá utilize [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget Olá diagnóstico configuração atual para um serviço em nuvem.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>Remover a extensão de diagnóstico
tooturn desativar diagnóstico numa nuvem de serviço pode utilizar Olá [remover AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Se tiver ativado a extensão de diagnóstico de Olá com *conjunto AzureServiceDiagnosticsExtension* ou Olá *New-AzureServiceDiagnosticsExtensionConfig* sem Olá *função* parâmetro, em seguida, que pode remover a extensão de Olá com *remover AzureServiceDiagnosticsExtension* sem Olá *função* parâmetro. Se hello *função* parâmetro foi utilizado ao ativar a extensão de Olá, em seguida, este tem também de ser utilizada ao remover a extensão de Olá.

extensão de diagnóstico do Olá tooremove de cada função individual:

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Passos Seguintes
* Para obter orientações adicionais sobre como utilizar o diagnóstico do Azure e outros problemas de tootroubleshoot técnicas, consulte [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](cloud-services-dotnet-diagnostics.md).
* Olá [esquema de configuração de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) explica Olá opções diversas configurações de xml para extensão de diagnóstico de Olá.
* toolearn como extensão de diagnóstico de Olá tooenable para máquinas virtuais, consulte [criar uma Máquina Virtual do Windows com a monitorização e diagnóstico com o modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md)
