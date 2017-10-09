---
title: "aaaStatic clássico IP - VM do Azure - privado interno"
description: "Noções sobre IPs interno estático (DIPs) e como toomanage-las"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a>Como tooset um IP estático de privada interno endereços através do PowerShell (clássica)
Na maioria dos casos, não terá toospecify um endereço IP estático interno para a máquina virtual. As VMs numa rede virtual serão recebem automaticamente um endereço IP de um intervalo que especificou. Mas em certos casos, a especificação de um endereço IP estático para uma VM específica faz sentido. Por exemplo, se a VM está curso toorun DNS ou será um controlador de domínio. Um endereço IP estático interno permanece com Olá VM mesmo através de um Estado de paragem/desaprovisionamento. 

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que a maioria das implementações novas utilizem Olá [modelo de implementação do Resource Manager](virtual-networks-static-private-ip-arm-ps.md).
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a>Como tooverify esteja disponível um endereço IP específico
tooverify se hello endereço IP *10.0.0.7* está disponível numa vnet com o nome *TestVnet*, execute o seguinte comando do PowerShell de Olá e verifique o valor de Olá para *IsAvailable*:

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> Se pretender que o comando de Olá tootest acima num ambiente seguro, siga as diretrizes de Olá no [criar uma rede virtual (clássica)](virtual-networks-create-vnet-classic-pportal.md) toocreate uma vnet com o nome *TestVnet* e certifique-se de que utiliza Olá  *10.0.0.0/8* espaço de endereços.
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a>Como toospecify um IP internos estático ao criar uma VM
Olá script do PowerShell abaixo cria um novo serviço em nuvem com o nome *TestService*, em seguida, obtém uma imagem do Azure, em seguida, cria uma VM chamada *TestVM* no Olá novo serviço em nuvem utilizando a imagem Olá obtido, conjuntos de Olá toobe VM numa sub-rede com o nome *sub-rede 1*e define *10.0.0.7* como um IP estático interno para Olá VM:

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a>Como tooretrieve estáticas internas informações de IP para uma VM
tooview Olá estáticas internas informações de IP para Olá criada a VM com o script de Olá acima, execute o seguinte comando do PowerShell de Olá e observar os valores de Olá para *IpAddress*:

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a>Como tooremove um IP estático interno de uma VM
IP internos estáticos tooremove Olá adicionado toohello VM no script de Olá acima, execute Olá seguinte comando do PowerShell:

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a>Como tooadd um tooan IP estático interno VM existente
tooadd um toohello IP interno estático VM criada utilizando o script de Olá acima, runt tados os seguintes comandos:

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a>Passos seguintes
[IP reservado](virtual-networks-reserved-public-ip.md)

[IP público de nível de instância (ILPIP)](virtual-networks-instance-level-public-ip.md)

[APIs REST do IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx)

