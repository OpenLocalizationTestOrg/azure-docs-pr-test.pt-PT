---
title: "aaaManage VMs num conjunto de dimensionamento de Máquina Virtual | Microsoft Docs"
description: "Gerir máquinas virtuais num conjunto com o Azure PowerShell de dimensionamento de máquina virtual."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Gerir máquinas virtuais num conjunto de dimensionamento de máquina virtual
Utilize tarefas de Olá nas máquinas virtuais de toomanage artigo no seu conjunto de dimensionamento de máquina virtual.

Na maioria das tarefas de Olá que envolvam a gerir uma máquina virtual num conjunto de dimensionamento necessita que sabe o ID de instância de Olá da máquina de Olá que pretende que o toomanage. Pode utilizar [Explorador de recursos do Azure](https://resources.azure.com) toofind Olá ID de instância de uma máquina virtual num conjunto de dimensionamento. Também é utilizar o Explorador de recursos tooverify Olá Estado Olá tarefas que termina.

Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter informações sobre instalar Olá a versão mais recente do Azure PowerShell, selecionar a sua subscrição e início de sessão na conta tooyour.

## <a name="display-information-about-a-scale-set"></a>Apresentar informações sobre um conjunto de dimensionamento
Pode obter informações gerais sobre um conjunto de dimensionamento, que também seja vista de instância de Olá tooas referenciado. Em alternativa, pode obter informações mais específicas, tais como informações sobre recursos de Olá no conjunto de dimensionamento de Olá.

Substitua Olá entre aspas valores com o nome de Olá ou o grupo de recursos e a escala definido e, em seguida, execute o comando de Olá:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Devolve algo semelhante ao seguinte:

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de grupo e o dimensionamento do recurso. Substitua  *#*  com o identificador de instância de Olá da máquina virtual de Olá que pretende tooget informações sobre e, em seguida, executá-lo:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Devolve algo semelhante a este exemplo:

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Iniciar uma máquina virtual num conjunto de dimensionamento
Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de grupo e o dimensionamento do recurso. Substitua  *#*  com o identificador de Olá da máquina virtual de Olá que pretende toostart e, em seguida, executá-lo:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

No Explorador de recursos, é possível ver que Olá estado da instância de Olá é **executar**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

Pode começar a todas as máquinas de virtuais Olá na escala de Olá definida por não utilizar o parâmetro - InstanceId de Olá.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Parar uma máquina virtual num conjunto de dimensionamento
Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de grupo e o dimensionamento do recurso. Substitua  *#*  com o identificador de Olá da máquina virtual de Olá que pretende toostop e, em seguida, executá-lo:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

No Explorador de recursos, é possível ver que Olá estado da instância de Olá é **desalocada**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

toostop uma máquina virtual e não desalocá-lo, utilize o parâmetro - StayProvisioned de Olá. Pode parar todas as máquinas de virtuais de Olá Olá definido por não utilizar o parâmetro - InstanceId de Olá.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Reiniciar uma máquina virtual num conjunto de dimensionamento
Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de dimensionamento de grupo e Olá recursos. Substitua  *#*  com o identificador de Olá da máquina virtual de Olá que pretende toorestart e, em seguida, executá-lo:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Todas as máquinas de virtuais Olá pode ser reiniciado no Olá definido por não utilizar o parâmetro - InstanceId de Olá.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Remover uma máquina virtual a partir de um conjunto de dimensionamento
Substitua Olá entre aspas valores com o nome de Olá do seu conjunto de dimensionamento de grupo e Olá recursos. Substitua  *#*  com o identificador de Olá da máquina virtual de Olá que pretende tooremove e, em seguida, executá-lo:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

Pode remover o conjunto de dimensionamento de máquina virtual de Olá, uma vez por não utilizar o parâmetro - InstanceId de Olá.

## <a name="change-hello-capacity-of-a-scale-set"></a>Capacidade de Olá de alteração de um conjunto de dimensionamento
Pode adicionar ou remover máquinas virtuais alterando a capacidade de Olá do conjunto de Olá. Obter conjunto de dimensionamento de Olá que pretende que sejam toochange, conjunto Olá capacidade toowhat querer toobe e, em seguida, atualizar o conjunto de dimensionamento de Olá com a nova capacidade de Olá. Nestes comandos, substitua Olá entre aspas valores com o nome de Olá do seu conjunto de dimensionamento de grupo e Olá recursos.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Se estiver a remover máquinas virtuais do conjunto de dimensionamento de Olá, máquinas virtuais Olá com ids mais elevados de Olá são removidas pela primeira vez.

