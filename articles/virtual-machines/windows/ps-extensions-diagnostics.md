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
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="dba4d-103">Utilizar o PowerShell tooenable do diagnóstico do Azure numa máquina virtual com o Windows</span><span class="sxs-lookup"><span data-stu-id="dba4d-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="dba4d-104">Diagnóstico do Azure é a capacidade de Olá no Azure que permite a recolha de Olá de dados de diagnóstico sobre uma aplicação implementada.</span><span class="sxs-lookup"><span data-stu-id="dba4d-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="dba4d-105">Pode utilizar Olá diagnóstico extensão toocollect dados de diagnóstico, como os registos de aplicações ou os contadores de desempenho de uma máquina virtual (VM) do Azure que está a executar o Windows.</span><span class="sxs-lookup"><span data-stu-id="dba4d-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="dba4d-106">Este artigo descreve como toouse do Windows PowerShell tooenable hello a extensão de diagnóstico para uma VM.</span><span class="sxs-lookup"><span data-stu-id="dba4d-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="dba4d-107">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para pré-requisitos Olá necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="dba4d-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="dba4d-108">Ativar a extensão de diagnóstico de Olá, se utilizar o modelo de implementação do Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="dba4d-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="dba4d-109">Pode ativar a extensão de diagnóstico de Olá enquanto cria uma VM do Windows através do modelo de implementação Azure Resource Manager Olá adicionando o modelo do Olá extensão configuração toohello do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dba4d-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="dba4d-110">Consulte [criar máquina virtual do Windows com a monitorização e diagnóstico utilizando o modelo do Azure Resource Manager Olá](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dba4d-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="dba4d-111">extensão de diagnóstico do Olá tooenable numa VM existente que tenha sido criada através do modelo de implementação do Resource Manager Olá, pode utilizar Olá [conjunto AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) cmdlet do PowerShell, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="dba4d-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="dba4d-112">*$diagnosticsconfig_path* é Olá caminho toohello ficheiro que contém a configuração de diagnósticos de Olá em XML, conforme descrito no Olá [exemplo](#sample-diagnostics-configuration) abaixo.</span><span class="sxs-lookup"><span data-stu-id="dba4d-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="dba4d-113">Se o ficheiro de configuração de diagnósticos de Olá Especifica um **StorageAccount** elemento com um nome de conta de armazenamento, em seguida, Olá *conjunto AzureRMVMDiagnosticsExtension* script irá definir automaticamente Olá diagnóstico extensão toosend dados de diagnóstico toothat conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dba4d-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="dba4d-114">Para este toowork, conta de armazenamento Olá tem toobe no Olá mesma subscrição, conforme Olá VM.</span><span class="sxs-lookup"><span data-stu-id="dba4d-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="dba4d-115">Se não **StorageAccount** foi especificado na configuração de diagnósticos de Olá, em seguida, terá de toopass no Olá *StorageAccountName* parâmetro toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dba4d-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="dba4d-116">Se hello *StorageAccountName* parâmetro for especificado, em seguida, Olá cmdlet irá utilizar sempre a conta de armazenamento Olá, que é especificada no parâmetro de Olá e não Olá aquele que está especificado no ficheiro de configuração de diagnósticos de Olá.</span><span class="sxs-lookup"><span data-stu-id="dba4d-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="dba4d-117">Se passar diagnóstico Olá conta de armazenamento está numa subscrição diferente de Olá VM, em seguida, terá de tooexplicitly Olá *StorageAccountName* e *StorageAccountKey* parâmetros toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dba4d-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="dba4d-118">Olá *StorageAccountKey* parâmetro não é necessária quando o diagnóstico de Olá conta de armazenamento está a ser Olá mesma subscrição, conforme Olá cmdlet automaticamente pode consultar e defina o valor de chave de Olá ao ativar a extensão de diagnóstico de Olá.</span><span class="sxs-lookup"><span data-stu-id="dba4d-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="dba4d-119">No entanto, se Olá conta de armazenamento do diagnostics está numa subscrição diferente, em seguida, Olá cmdlet poderá não ser tooget capaz de chave de Olá automaticamente, sendo necessário tooexplicitly especificar Olá chave através de Olá *StorageAccountKey* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="dba4d-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="dba4d-120">Quando a extensão de diagnóstico de Olá estiver ativada numa VM, pode obter as definições atuais de Olá utilizando Olá [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dba4d-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="dba4d-121">Olá cmdlet devolve *PublicSettings*, que contém a configuração de diagnósticos de Olá.</span><span class="sxs-lookup"><span data-stu-id="dba4d-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="dba4d-122">Existem dois tipos de configuração é suportada, WadCfg e xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="dba4d-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="dba4d-123">WadCfg é a configuração de JSON, não sendo xmlCfg configuração XML num formato com codificação Base64.</span><span class="sxs-lookup"><span data-stu-id="dba4d-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="dba4d-124">tooread Olá XML, terá de toodecode-lo.</span><span class="sxs-lookup"><span data-stu-id="dba4d-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="dba4d-125">Olá [remover AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet pode ser utilizado tooremove Olá extensão de diagnóstico de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="dba4d-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="dba4d-126">Ativar a extensão de diagnóstico de Olá, se utilizar o modelo de implementação clássica Olá</span><span class="sxs-lookup"><span data-stu-id="dba4d-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="dba4d-127">Pode utilizar Olá [conjunto AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable uma extensão de diagnóstico numa VM que criar através do modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="dba4d-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="dba4d-128">Olá exemplo seguinte mostra como toocreate uma nova VM através do modelo de implementação clássica Olá com a extensão de diagnóstico de Olá ativada.</span><span class="sxs-lookup"><span data-stu-id="dba4d-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="dba4d-129">extensão de diagnóstico de Olá tooenable numa VM existente que tenha sido criada através do modelo de implementação clássica Olá, primeira utilização Olá [Get-AzureVM](/powershell/module/azure/get-azurevm) configuração de VM do cmdlet tooget Olá.</span><span class="sxs-lookup"><span data-stu-id="dba4d-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="dba4d-130">Em seguida, atualize a extensão de diagnóstico de Olá configuração tooinclude Olá VM utilizando Olá [conjunto AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dba4d-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="dba4d-131">Por fim, aplicar Olá atualizada configuração toohello VM utilizando [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="dba4d-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="dba4d-132">Configuração de diagnósticos de exemplo</span><span class="sxs-lookup"><span data-stu-id="dba4d-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="dba4d-133">Olá que XML seguinte pode ser utilizado para a configuração pública de diagnóstico Olá com Olá acima scripts.</span><span class="sxs-lookup"><span data-stu-id="dba4d-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="dba4d-134">Este exemplo de configuração irá transferir vários desempenho contadores toohello diagnóstico conta do storage, juntamente com erros de aplicação Olá, segurança e canais de sistema nos registos de eventos do Windows hello e quaisquer erros de diagnóstico Olá registos da infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="dba4d-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="dba4d-135">configuração de Olá tem seguinte de Olá toobe tooinclude atualizadas:</span><span class="sxs-lookup"><span data-stu-id="dba4d-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="dba4d-136">Olá *resourceID* atributo de Olá **métricas** toobe atualizada com o ID de recurso Olá para Olá VM tem de elemento.</span><span class="sxs-lookup"><span data-stu-id="dba4d-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="dba4d-137">Olá ID pode ser construído utilizando Olá seguir o padrão de recurso: "/ subscrições / {*ID de subscrição para a subscrição de Olá com Olá VM*} /resourceGroups/ {*nome resourcegroup Olá Olá VM*} / providers/Microsoft.Compute/virtualMachines/ {*Olá nome da VM*} ".</span><span class="sxs-lookup"><span data-stu-id="dba4d-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="dba4d-138">Por exemplo, se hello o ID de subscrição para a subscrição de olá onde hello VM está em execução é **11111111-1111-1111-1111-111111111111**, é o nome do grupo de recursos Olá para o grupo de recursos de Olá **MyResourceGroup**, sendo hello nome da VM **MyWindowsVM**, Olá, em seguida, o valor para *resourceID* seria:</span><span class="sxs-lookup"><span data-stu-id="dba4d-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="dba4d-139">Para obter mais informações sobre como as métricas são os contadores de desempenho gerada Olá com base no e a configuração de métricas, consulte [tabela de métricas de diagnóstico do Azure no armazenamento](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="dba4d-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="dba4d-140">Olá **StorageAccount** toobe atualizado com o nome de Olá Olá diagnóstico da conta de armazenamento necessita de elemento.</span><span class="sxs-lookup"><span data-stu-id="dba4d-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
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

## <a name="next-steps"></a><span data-ttu-id="dba4d-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dba4d-141">Next steps</span></span>
* <span data-ttu-id="dba4d-142">Para obter orientações adicionais sobre como utilizar a capacidade de diagnóstico do Azure Olá e outros problemas de tootroubleshoot técnicas, consulte [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="dba4d-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="dba4d-143">[Esquema de configurações de diagnóstico](https://msdn.microsoft.com/library/azure/mt634524.aspx) explica Olá opções diversas configurações de XML para extensão de diagnóstico de Olá.</span><span class="sxs-lookup"><span data-stu-id="dba4d-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

