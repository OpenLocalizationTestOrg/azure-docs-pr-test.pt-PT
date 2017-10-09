---
title: "aaaUse diagnósticos de tooenable do Azure PowerShell numa VM do Windows | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "Saiba como toouse PowerShell tooenable diagnósticos do Azure numa máquina virtual com o Windows"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Utilizar o PowerShell tooenable do diagnóstico do Azure numa máquina virtual com o Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Diagnóstico do Azure é a capacidade de Olá no Azure que permite a recolha de Olá de dados de diagnóstico sobre uma aplicação implementada. Pode utilizar Olá diagnóstico extensão toocollect dados de diagnóstico, como os registos de aplicações ou os contadores de desempenho de uma máquina virtual (VM) do Azure que está a executar o Windows. Este artigo descreve como toouse do Windows PowerShell tooenable hello a extensão de diagnóstico para uma VM. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para pré-requisitos Olá necessários para este artigo.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Ativar a extensão de diagnóstico de Olá, se utilizar o modelo de implementação do Resource Manager Olá
Pode ativar a extensão de diagnóstico de Olá enquanto cria uma VM do Windows através do modelo de implementação Azure Resource Manager Olá adicionando o modelo do Olá extensão configuração toohello do Resource Manager. Consulte [criar máquina virtual do Windows com a monitorização e diagnóstico utilizando o modelo do Azure Resource Manager Olá](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

extensão de diagnóstico do Olá tooenable numa VM existente que tenha sido criada através do modelo de implementação do Resource Manager Olá, pode utilizar Olá [conjunto AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) cmdlet do PowerShell, conforme mostrado abaixo.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* é Olá caminho toohello ficheiro que contém a configuração de diagnósticos de Olá em XML, conforme descrito no Olá [exemplo](#sample-diagnostics-configuration) abaixo.  

Se o ficheiro de configuração de diagnósticos de Olá Especifica um **StorageAccount** elemento com um nome de conta de armazenamento, em seguida, Olá *conjunto AzureRMVMDiagnosticsExtension* script irá definir automaticamente Olá diagnóstico extensão toosend dados de diagnóstico toothat conta de armazenamento. Para este toowork, conta de armazenamento Olá tem toobe no Olá mesma subscrição, conforme Olá VM.

Se não **StorageAccount** foi especificado na configuração de diagnósticos de Olá, em seguida, terá de toopass no Olá *StorageAccountName* parâmetro toohello cmdlet. Se hello *StorageAccountName* parâmetro for especificado, em seguida, Olá cmdlet irá utilizar sempre a conta de armazenamento Olá, que é especificada no parâmetro de Olá e não Olá aquele que está especificado no ficheiro de configuração de diagnósticos de Olá.

Se passar diagnóstico Olá conta de armazenamento está numa subscrição diferente de Olá VM, em seguida, terá de tooexplicitly Olá *StorageAccountName* e *StorageAccountKey* parâmetros toohello cmdlet. Olá *StorageAccountKey* parâmetro não é necessária quando o diagnóstico de Olá conta de armazenamento está a ser Olá mesma subscrição, conforme Olá cmdlet automaticamente pode consultar e defina o valor de chave de Olá ao ativar a extensão de diagnóstico de Olá. No entanto, se Olá conta de armazenamento do diagnostics está numa subscrição diferente, em seguida, Olá cmdlet poderá não ser tooget capaz de chave de Olá automaticamente, sendo necessário tooexplicitly especificar Olá chave através de Olá *StorageAccountKey* parâmetro.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Quando a extensão de diagnóstico de Olá estiver ativada numa VM, pode obter as definições atuais de Olá utilizando Olá [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Olá cmdlet devolve *PublicSettings*, que contém a configuração de diagnósticos de Olá. Existem dois tipos de configuração é suportada, WadCfg e xmlCfg. WadCfg é a configuração de JSON, não sendo xmlCfg configuração XML num formato com codificação Base64. tooread Olá XML, terá de toodecode-lo.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Olá [remover AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet pode ser utilizado tooremove Olá extensão de diagnóstico de Olá VM.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Ativar a extensão de diagnóstico de Olá, se utilizar o modelo de implementação clássica Olá
Pode utilizar Olá [conjunto AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable uma extensão de diagnóstico numa VM que criar através do modelo de implementação clássica Olá. Olá exemplo seguinte mostra como toocreate uma nova VM através do modelo de implementação clássica Olá com a extensão de diagnóstico de Olá ativada.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

extensão de diagnóstico de Olá tooenable numa VM existente que tenha sido criada através do modelo de implementação clássica Olá, primeira utilização Olá [Get-AzureVM](/powershell/module/azure/get-azurevm) configuração de VM do cmdlet tooget Olá. Em seguida, atualize a extensão de diagnóstico de Olá configuração tooinclude Olá VM utilizando Olá [conjunto AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet. Por fim, aplicar Olá atualizada configuração toohello VM utilizando [Update-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Configuração de diagnósticos de exemplo
Olá que XML seguinte pode ser utilizado para a configuração pública de diagnóstico Olá com Olá acima scripts. Este exemplo de configuração irá transferir vários desempenho contadores toohello diagnóstico conta do storage, juntamente com erros de aplicação Olá, segurança e canais de sistema nos registos de eventos do Windows hello e quaisquer erros de diagnóstico Olá registos da infraestrutura.

configuração de Olá tem seguinte de Olá toobe tooinclude atualizadas:

* Olá *resourceID* atributo de Olá **métricas** toobe atualizada com o ID de recurso Olá para Olá VM tem de elemento.
  
  * Olá ID pode ser construído utilizando Olá seguir o padrão de recurso: "/ subscrições / {*ID de subscrição para a subscrição de Olá com Olá VM*} /resourceGroups/ {*nome resourcegroup Olá Olá VM*} / providers/Microsoft.Compute/virtualMachines/ {*Olá nome da VM*} ".
  * Por exemplo, se hello o ID de subscrição para a subscrição de olá onde hello VM está em execução é **11111111-1111-1111-1111-111111111111**, é o nome do grupo de recursos Olá para o grupo de recursos de Olá **MyResourceGroup**, sendo hello nome da VM **MyWindowsVM**, Olá, em seguida, o valor para *resourceID* seria:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Para obter mais informações sobre como as métricas são os contadores de desempenho gerada Olá com base no e a configuração de métricas, consulte [tabela de métricas de diagnóstico do Azure no armazenamento](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Olá **StorageAccount** toobe atualizado com o nome de Olá Olá diagnóstico da conta de armazenamento necessita de elemento.
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for hello VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a>Passos seguintes
* Para obter orientações adicionais sobre como utilizar a capacidade de diagnóstico do Azure Olá e outros problemas de tootroubleshoot técnicas, consulte [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Esquema de configurações de diagnóstico](https://msdn.microsoft.com/library/azure/mt634524.aspx) explica Olá opções diversas configurações de XML para extensão de diagnóstico de Olá.

