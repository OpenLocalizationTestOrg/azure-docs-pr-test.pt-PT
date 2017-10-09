---
title: "endereços de IP público (clássica) aaaAzure nível de instância | Microsoft Docs"
description: "Compreender os endereços de IP (ILPIP) de públicos nível de instância e como toomanage-las através do PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a>Instância pública IP (clássica) Descrição geral detalhada
Uma instância IP público ao nível (ILPIP) é um endereço IP público que pode atribuir diretamente instância de função VM ou Cloud Services tooa, em vez de serviço em nuvem toohello que a VM ou instância de função residem no. Um ILPIP não ocorrer Olá de Olá IP virtual (VIP) atribuído tooyour o serviço em nuvem. Em vez disso, é um endereço IP adicional que pode utilizar tooconnect diretamente tooyour VM ou instância de função.

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda a criação de VMs através do Resource Manager. Certifique-se de que compreende como [endereços IP](virtual-network-ip-addresses-overview-classic.md) trabalho no Azure.

![Diferença entre ILPIP e VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

Como é mostrado na figura 1, o serviço em nuvem Olá é acedido através de um VIP, ao hello VMs individuais são normalmente acedidas através de VIP:&lt;número de porta&gt;. Ao atribuir um tooa ILPIP VM específica, que a VM pode ser acedido diretamente com esse endereço IP.

Quando cria um serviço em nuvem no Azure, correspondentes DNS registos são criados automaticamente tooallow serviço de toohello de acesso através de um nome de domínio completamente qualificado (FQDN), em vez de utilizar VIP real Olá. Olá acontece mesmo processo para um ILPIP, permitindo acesso toohello VM ou instância de função através do FQDN, em vez de Olá ILPIP. Por exemplo, se criar um serviço em nuvem com o nome *contosoadservice*, e configurar uma função da web com o nome *contosoweb* com duas instâncias, Olá de registos do Azure após A regista para instâncias de Olá:

* contosoweb\_IN_0.contosoadservice.cloudapp.net
* contosoweb\_IN_1.contosoadservice.cloudapp.net 

> [!NOTE]
> Pode atribuir ILPIP apenas um para cada VM ou instância de função. Pode utilizar segurança too5 ILPIPs por subscrição. ILPIPs não são suportadas para as VMs de vários NICs.
> 
> 

## <a name="why-would-i-request-an-ilpip"></a>Por que motivo seria a pedir uma ILPIP?
Se quiser toobe tooconnect capaz de tooyour VM ou instância de função por um endereço IP atribuído diretamente tooit, em vez de utilizar a cloud Olá service VIP:&lt;número de porta&gt;, pedir um ILPIP para a VM ou instância de função.

* **Active Directory FTP** -atribuindo um tooa ILPIP VM, pode receber tráfego em qualquer porta. Pontos finais não são necessários para Olá tooreceive tráfego da VM.  Consulte [geral do protocolo FTP] (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) para obter detalhes sobre o protocolo de Olá FTP.
* **Saída IP** - tráfego de saída provenientes de Olá VM se encontra mapeada toohello ILPIP como origem Olá e Olá ILPIP identifica exclusivamente entidades de tooexternal Olá VM.

> [!NOTE]
> No passado, Olá, um endereço ILPIP foi referenciado tooas um endereço IP (PIP) público.
> 

## <a name="manage-an-ilpip-for-a-vm"></a>Gerir um ILPIP para uma VM
Olá, seguindo as tarefas permitem-lhe toocreate, atribuir e remover ILPIPs de VMs:

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a>Como toorequest um ILPIP durante a criação da VM com o PowerShell
Olá seguinte script do PowerShell cria um serviço em nuvem com o nome *FTPService*, obtém uma imagem do Azure, cria uma VM chamada *FTPInstance* com imagem Olá obtido, define um ILPIP Olá VM toouse e adiciona o novo serviço de Olá VM toohello:

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a>Como tooretrieve ILPIP as informações de uma VM
Olá tooview ILPIP as informações de Olá VM criados com scripts de anteriores Olá, execute o seguinte comando do PowerShell de Olá e observe os valores de Olá para *PublicIPAddress* e *PublicIPName*:

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

Resultado esperado:
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a>Como tooremove um ILPIP de uma VM
Olá tooremove ILPIP adicionadas toohello VM no script anterior Olá, execute o seguinte comando do PowerShell de Olá:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a>Como tooadd um tooan ILPIP VM existente
tooadd um toohello ILPIP VM criada utilizando o script de Olá anterior, execute Olá os seguintes comandos:

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a>Gerir um ILPIP para uma instância de função de serviços Cloud

tooadd uma instância de função do ILPIP tooa serviços em nuvem, Olá concluir os seguintes passos:

1. Transferir o ficheiro. cscfg Olá para o serviço em nuvem Olá concluindo Olá os passos no Olá [como tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artigo.
2. Ficheiro. cscfg Olá atualização adicionando Olá `InstanceAddress` elemento. Olá exemplo seguinte adiciona um ILPIP denominado *MyPublicIP* com o nome da instância de função tooa *WebRole1*: 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. Carregar ficheiro. cscfg Olá de serviço de nuvem Olá concluindo Olá os passos em Olá [como tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artigo.

## <a name="next-steps"></a>Passos seguintes
* Compreender como [endereçamento IP](virtual-network-ip-addresses-overview-classic.md) funciona no modelo de implementação clássica Olá.
* Saiba mais sobre [reservado IPs](virtual-networks-reserved-public-ip.md).
