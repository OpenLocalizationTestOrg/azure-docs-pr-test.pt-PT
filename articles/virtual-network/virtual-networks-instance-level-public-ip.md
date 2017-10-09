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
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="9d441-103">Instância pública IP (clássica) Descrição geral detalhada</span><span class="sxs-lookup"><span data-stu-id="9d441-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="9d441-104">Uma instância IP público ao nível (ILPIP) é um endereço IP público que pode atribuir diretamente instância de função VM ou Cloud Services tooa, em vez de serviço em nuvem toohello que a VM ou instância de função residem no.</span><span class="sxs-lookup"><span data-stu-id="9d441-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="9d441-105">Um ILPIP não ocorrer Olá de Olá IP virtual (VIP) atribuído tooyour o serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="9d441-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="9d441-106">Em vez disso, é um endereço IP adicional que pode utilizar tooconnect diretamente tooyour VM ou instância de função.</span><span class="sxs-lookup"><span data-stu-id="9d441-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d441-107">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d441-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="9d441-108">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="9d441-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="9d441-109">A Microsoft recomenda a criação de VMs através do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9d441-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="9d441-110">Certifique-se de que compreende como [endereços IP](virtual-network-ip-addresses-overview-classic.md) trabalho no Azure.</span><span class="sxs-lookup"><span data-stu-id="9d441-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Diferença entre ILPIP e VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="9d441-112">Como é mostrado na figura 1, o serviço em nuvem Olá é acedido através de um VIP, ao hello VMs individuais são normalmente acedidas através de VIP:&lt;número de porta&gt;.</span><span class="sxs-lookup"><span data-stu-id="9d441-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="9d441-113">Ao atribuir um tooa ILPIP VM específica, que a VM pode ser acedido diretamente com esse endereço IP.</span><span class="sxs-lookup"><span data-stu-id="9d441-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="9d441-114">Quando cria um serviço em nuvem no Azure, correspondentes DNS registos são criados automaticamente tooallow serviço de toohello de acesso através de um nome de domínio completamente qualificado (FQDN), em vez de utilizar VIP real Olá.</span><span class="sxs-lookup"><span data-stu-id="9d441-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="9d441-115">Olá acontece mesmo processo para um ILPIP, permitindo acesso toohello VM ou instância de função através do FQDN, em vez de Olá ILPIP.</span><span class="sxs-lookup"><span data-stu-id="9d441-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="9d441-116">Por exemplo, se criar um serviço em nuvem com o nome *contosoadservice*, e configurar uma função da web com o nome *contosoweb* com duas instâncias, Olá de registos do Azure após A regista para instâncias de Olá:</span><span class="sxs-lookup"><span data-stu-id="9d441-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="9d441-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="9d441-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="9d441-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="9d441-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="9d441-119">Pode atribuir ILPIP apenas um para cada VM ou instância de função.</span><span class="sxs-lookup"><span data-stu-id="9d441-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="9d441-120">Pode utilizar segurança too5 ILPIPs por subscrição.</span><span class="sxs-lookup"><span data-stu-id="9d441-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="9d441-121">ILPIPs não são suportadas para as VMs de vários NICs.</span><span class="sxs-lookup"><span data-stu-id="9d441-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="9d441-122">Por que motivo seria a pedir uma ILPIP?</span><span class="sxs-lookup"><span data-stu-id="9d441-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="9d441-123">Se quiser toobe tooconnect capaz de tooyour VM ou instância de função por um endereço IP atribuído diretamente tooit, em vez de utilizar a cloud Olá service VIP:&lt;número de porta&gt;, pedir um ILPIP para a VM ou instância de função.</span><span class="sxs-lookup"><span data-stu-id="9d441-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="9d441-124">**Active Directory FTP** -atribuindo um tooa ILPIP VM, pode receber tráfego em qualquer porta.</span><span class="sxs-lookup"><span data-stu-id="9d441-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="9d441-125">Pontos finais não são necessários para Olá tooreceive tráfego da VM.</span><span class="sxs-lookup"><span data-stu-id="9d441-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="9d441-126">Consulte [geral do protocolo FTP] (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) para obter detalhes sobre o protocolo de Olá FTP.</span><span class="sxs-lookup"><span data-stu-id="9d441-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="9d441-127">**Saída IP** - tráfego de saída provenientes de Olá VM se encontra mapeada toohello ILPIP como origem Olá e Olá ILPIP identifica exclusivamente entidades de tooexternal Olá VM.</span><span class="sxs-lookup"><span data-stu-id="9d441-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="9d441-128">No passado, Olá, um endereço ILPIP foi referenciado tooas um endereço IP (PIP) público.</span><span class="sxs-lookup"><span data-stu-id="9d441-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="9d441-129">Gerir um ILPIP para uma VM</span><span class="sxs-lookup"><span data-stu-id="9d441-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="9d441-130">Olá, seguindo as tarefas permitem-lhe toocreate, atribuir e remover ILPIPs de VMs:</span><span class="sxs-lookup"><span data-stu-id="9d441-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="9d441-131">Como toorequest um ILPIP durante a criação da VM com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d441-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="9d441-132">Olá seguinte script do PowerShell cria um serviço em nuvem com o nome *FTPService*, obtém uma imagem do Azure, cria uma VM chamada *FTPInstance* com imagem Olá obtido, define um ILPIP Olá VM toouse e adiciona o novo serviço de Olá VM toohello:</span><span class="sxs-lookup"><span data-stu-id="9d441-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="9d441-133">Como tooretrieve ILPIP as informações de uma VM</span><span class="sxs-lookup"><span data-stu-id="9d441-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="9d441-134">Olá tooview ILPIP as informações de Olá VM criados com scripts de anteriores Olá, execute o seguinte comando do PowerShell de Olá e observe os valores de Olá para *PublicIPAddress* e *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="9d441-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="9d441-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="9d441-135">Expected output:</span></span>
 
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

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="9d441-136">Como tooremove um ILPIP de uma VM</span><span class="sxs-lookup"><span data-stu-id="9d441-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="9d441-137">Olá tooremove ILPIP adicionadas toohello VM no script anterior Olá, execute o seguinte comando do PowerShell de Olá:</span><span class="sxs-lookup"><span data-stu-id="9d441-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="9d441-138">Como tooadd um tooan ILPIP VM existente</span><span class="sxs-lookup"><span data-stu-id="9d441-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="9d441-139">tooadd um toohello ILPIP VM criada utilizando o script de Olá anterior, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="9d441-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="9d441-140">Gerir um ILPIP para uma instância de função de serviços Cloud</span><span class="sxs-lookup"><span data-stu-id="9d441-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="9d441-141">tooadd uma instância de função do ILPIP tooa serviços em nuvem, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="9d441-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="9d441-142">Transferir o ficheiro. cscfg Olá para o serviço em nuvem Olá concluindo Olá os passos no Olá [como tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artigo.</span><span class="sxs-lookup"><span data-stu-id="9d441-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="9d441-143">Ficheiro. cscfg Olá atualização adicionando Olá `InstanceAddress` elemento.</span><span class="sxs-lookup"><span data-stu-id="9d441-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="9d441-144">Olá exemplo seguinte adiciona um ILPIP denominado *MyPublicIP* com o nome da instância de função tooa *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="9d441-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="9d441-145">Carregar ficheiro. cscfg Olá de serviço de nuvem Olá concluindo Olá os passos em Olá [como tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artigo.</span><span class="sxs-lookup"><span data-stu-id="9d441-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d441-146">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9d441-146">Next steps</span></span>
* <span data-ttu-id="9d441-147">Compreender como [endereçamento IP](virtual-network-ip-addresses-overview-classic.md) funciona no modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="9d441-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="9d441-148">Saiba mais sobre [reservado IPs](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="9d441-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
