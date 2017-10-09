---
title: "aaaMutiple VIPs num serviço em nuvem"
description: "Descrição geral do multiVIP e como tooset vários VIPs num serviço em nuvem"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="74cb3-103">Configurar vários VIPs num serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="74cb3-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="74cb3-104">Pode aceder a serviços em nuvem do Azure através de Olá Internet pública, utilizando um endereço IP fornecida pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="74cb3-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="74cb3-105">Este endereço IP público é referenciado tooas um VIP (virtual IP), uma vez que está ligado toohello Azure Balanceador de carga e não Olá instâncias de Máquina Virtual (VM) no serviço de nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="74cb3-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="74cb3-106">Pode aceder a qualquer instância VM dentro de um serviço em nuvem através da utilização de um único VIP.</span><span class="sxs-lookup"><span data-stu-id="74cb3-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="74cb3-107">No entanto, existem cenários em que poderá ser necessário mais do que um VIP como um toohello de ponto de entrada mesmo serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="74cb3-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="74cb3-108">Por exemplo, o serviço em nuvem pode alojar vários sites que requeiram conectividade SSL com a porta predefinida Olá 443, como cada site é alojada para um cliente diferente ou inquilino.</span><span class="sxs-lookup"><span data-stu-id="74cb3-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="74cb3-109">Neste cenário, precisa de toohave um outro endereço IP destinado ao público para cada site.</span><span class="sxs-lookup"><span data-stu-id="74cb3-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="74cb3-110">Olá diagrama a seguir ilustra um típico web do multi-inquilino de alojamento com necessidade para SSL vários certificados em Olá mesmo Porta pública.</span><span class="sxs-lookup"><span data-stu-id="74cb3-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Cenário de várias VIP SSL](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="74cb3-112">No exemplo de Olá acima, todos os Olá de utilização de VIPs mesma porta pública (443) e o tráfego é tooone redirecionado ou mais VMs com balanceamento de uma porta privada exclusiva para Olá um endereço IP de todos os sites de Olá de alojamento do serviço de nuvem Olá de carga.</span><span class="sxs-lookup"><span data-stu-id="74cb3-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="74cb3-113">Outro Olá utilização da Olá necessitando do situação vários VIPs está a alojar vários escuta de grupo de Disponibilidade AlwaysOn de SQL no mesmo conjunto de máquinas virtuais de Olá.</span><span class="sxs-lookup"><span data-stu-id="74cb3-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="74cb3-114">VIPs são dinâmicas por predefinição, o que significa que Olá real endereço IP atribuído toohello o serviço em nuvem pode alterar ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="74cb3-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="74cb3-115">tooprevent que aconteça, pode reservar um VIP para o seu serviço.</span><span class="sxs-lookup"><span data-stu-id="74cb3-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="74cb3-116">toolearn mais informações sobre VIPs reservadas, consulte [reservado de IP público](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="74cb3-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="74cb3-117">Consulte [preços do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/) para obter informações sobre preços em VIPs e IPs reservados.</span><span class="sxs-lookup"><span data-stu-id="74cb3-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="74cb3-118">Pode utilizar o PowerShell tooverify Olá VIPs utilizados pelos seus serviços em nuvem, bem como adicionar e remover VIPs, associar um ponto final tooan de VIP e configurar um VIP específico de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="74cb3-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="74cb3-119">Limitações</span><span class="sxs-lookup"><span data-stu-id="74cb3-119">Limitations</span></span>

<span data-ttu-id="74cb3-120">Neste momento, a funcionalidade de várias VIP está limitado toohello os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="74cb3-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="74cb3-121">**Apenas IaaS**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-121">**IaaS only**.</span></span> <span data-ttu-id="74cb3-122">Só pode ativar várias VIP para serviços em nuvem que contêm as VMs.</span><span class="sxs-lookup"><span data-stu-id="74cb3-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="74cb3-123">Não é possível utilizar várias VIP em cenários de PaaS com instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="74cb3-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="74cb3-124">**PowerShell apenas**.</span><span class="sxs-lookup"><span data-stu-id="74cb3-124">**PowerShell only**.</span></span> <span data-ttu-id="74cb3-125">Só pode gerir várias VIP utilizando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74cb3-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="74cb3-126">Estas limitações são temporárias e podem ser alterados em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="74cb3-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="74cb3-127">Certifique-se toorevisit este alterações futuras de tooverify de página.</span><span class="sxs-lookup"><span data-stu-id="74cb3-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="74cb3-128">O serviço em nuvem tooa tooadd um VIP</span><span class="sxs-lookup"><span data-stu-id="74cb3-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="74cb3-129">no serviço de tooyour tooadd um VIP, execute o seguinte comando do PowerShell de Olá:</span><span class="sxs-lookup"><span data-stu-id="74cb3-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="74cb3-130">Este comando apresenta um resultado toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="74cb3-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="74cb3-131">Como tooremove um VIP de um serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="74cb3-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="74cb3-132">Olá tooremove VIP adicionadas tooyour serviço no exemplo de Olá acima, Olá executar seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="74cb3-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="74cb3-133">Apenas é possível remover um VIP caso não tooit pontos finais associados.</span><span class="sxs-lookup"><span data-stu-id="74cb3-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="74cb3-134">Como tooretrieve VIP informações a partir de um serviço em nuvem</span><span class="sxs-lookup"><span data-stu-id="74cb3-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="74cb3-135">Olá tooretrieve VIPs associados a um serviço em nuvem, execute Olá seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="74cb3-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="74cb3-136">script de Olá apresenta um resultado toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="74cb3-136">hello script displays a result similar toohello following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="74cb3-137">Neste exemplo, o serviço em nuvem Olá tem 3 VIPs:</span><span class="sxs-lookup"><span data-stu-id="74cb3-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="74cb3-138">**O Vip1** é Olá VIP predefinido, sabe que porque o valor de Olá para IsDnsProgrammedName é definido tootrue.</span><span class="sxs-lookup"><span data-stu-id="74cb3-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="74cb3-139">**Vip2** e **Vip3** não são utilizados como não têm quaisquer endereços IP.</span><span class="sxs-lookup"><span data-stu-id="74cb3-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="74cb3-140">Só irá ser utilizadas se associar um ponto final toohello VIP.</span><span class="sxs-lookup"><span data-stu-id="74cb3-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="74cb3-141">A subscrição só será cobrada por VIPs adicionais assim que estiverem associados um ponto final.</span><span class="sxs-lookup"><span data-stu-id="74cb3-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="74cb3-142">Para obter mais informações sobre preços, consulte [preços do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="74cb3-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="74cb3-143">Como ponto final de tooan tooassociate um VIP</span><span class="sxs-lookup"><span data-stu-id="74cb3-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="74cb3-144">tooassociate um VIP num nuvem tooan ponto final de serviço, execute o seguinte comando do PowerShell de Olá:</span><span class="sxs-lookup"><span data-stu-id="74cb3-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="74cb3-145">Olá comando cria um ponto final chamado toohello ligado VIP *Vip2* na porta *80*e associa-toohello VM com o nome *myVM1* num serviço em nuvem com o nome  *myService* utilizando *TCP* na porta *8080*.</span><span class="sxs-lookup"><span data-stu-id="74cb3-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="74cb3-146">configuração de Olá do tooverify, execute o seguinte comando do PowerShell de Olá:</span><span class="sxs-lookup"><span data-stu-id="74cb3-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="74cb3-147">saída de Olá procura toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="74cb3-147">hello output looks similar toohello following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="74cb3-148">Como tooenable balanceamento de carga num VIP específico</span><span class="sxs-lookup"><span data-stu-id="74cb3-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="74cb3-149">Pode associar um VIP único com várias máquinas virtuais para fins de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="74cb3-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="74cb3-150">Por exemplo, tiver um serviço em nuvem com o nome *myService*e duas máquinas virtuais com o nome *myVM1* e *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="74cb3-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="74cb3-151">E o serviço de nuvem tem vários VIPs, um com o nome *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="74cb3-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="74cb3-152">Se quiser tooensure que todo o tráfego tooport *81* no *Vip2* é equilibrados entre *myVM1* e *myVM2* na porta *8181* , execute hello seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="74cb3-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="74cb3-153">Também pode atualizar o seu toouse de Balanceador de carga um VIP diferentes.</span><span class="sxs-lookup"><span data-stu-id="74cb3-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="74cb3-154">Por exemplo, se executar Olá comando do PowerShell abaixo, irá alterar conjunto toouse um VIP Vip1 com o nome de balanceamento de carga Olá:</span><span class="sxs-lookup"><span data-stu-id="74cb3-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="74cb3-155">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="74cb3-155">Next Steps</span></span>

[<span data-ttu-id="74cb3-156">Análise de registos para balanceamento de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="74cb3-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="74cb3-157">Internet destinado ao balanceador descrição geral de carga</span><span class="sxs-lookup"><span data-stu-id="74cb3-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="74cb3-158">Começar a utilizar na Internet com o Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="74cb3-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="74cb3-159">Descrição geral da rede virtual</span><span class="sxs-lookup"><span data-stu-id="74cb3-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="74cb3-160">APIs REST do IP reservado</span><span class="sxs-lookup"><span data-stu-id="74cb3-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
