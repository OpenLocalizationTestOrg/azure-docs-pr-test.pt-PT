---
title: aaaConfigure Balanceador de carga para o SQL always on | Microsoft Docs
description: "Configurar toowork de Balanceador de carga com o SQL Server sempre no e como tooleverage powershell toocreate Balanceador de carga para implementação do SQL Server de Olá"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="0d8d6-103">Configurar o Balanceador de carga para SQL Server sempre no</span><span class="sxs-lookup"><span data-stu-id="0d8d6-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="0d8d6-104">Grupos de Disponibilidade AlwaysOn do SQL Server podem agora ser executados com o ILB.</span><span class="sxs-lookup"><span data-stu-id="0d8d6-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="0d8d6-105">Grupo de disponibilidade está a solução de flagship do SQL Server para elevada disponibilidade e recuperação após desastre.</span><span class="sxs-lookup"><span data-stu-id="0d8d6-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="0d8d6-106">Olá escuta do grupo de disponibilidade permite que os cliente aplicações tooseamlessly ligar toohello réplica primária, independentemente do número de Olá de réplicas de Olá na configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d8d6-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="0d8d6-107">nome do serviço de escuta (DNS) Olá é o endereço IP de tooa mapeado com balanceamento de carga e Balanceador de carga do Azure direciona Olá receber tráfego tooonly Olá servidor primário no conjunto de réplicas Olá.</span><span class="sxs-lookup"><span data-stu-id="0d8d6-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="0d8d6-108">Pode utilizar o suporte do ILB para pontos finais do SQL Server AlwaysOn (serviço de escuta).</span><span class="sxs-lookup"><span data-stu-id="0d8d6-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="0d8d6-109">Agora tem controlo sobre acessibilidade Olá do serviço de escuta de Olá e pode escolher endereço IP com balanceamento de carga Olá uma sub-rede específica na sua rede Virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="0d8d6-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="0d8d6-110">Utilizando o ILB no serviço de escuta de Olá, Olá ponto final do SQL server (por exemplo, servidor = tcp:ListenerName, 1433; base de dados = DatabaseName) é acessível apenas a:</span><span class="sxs-lookup"><span data-stu-id="0d8d6-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="0d8d6-111">Olá, serviços e VMs na mesma rede Virtual</span><span class="sxs-lookup"><span data-stu-id="0d8d6-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="0d8d6-112">Os serviços e VMs a partir da rede ligados ao local</span><span class="sxs-lookup"><span data-stu-id="0d8d6-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="0d8d6-113">Os serviços e as VMs de VNets interligadas</span><span class="sxs-lookup"><span data-stu-id="0d8d6-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="0d8d6-115">Figura 1 - AlwaysOn de SQL Server configurada com Balanceador de carga para a Internet</span><span class="sxs-lookup"><span data-stu-id="0d8d6-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="0d8d6-116">Adicionar serviço de toohello do Balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="0d8d6-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="0d8d6-117">No seguinte exemplo de Olá, iremos irá configurar uma rede Virtual que contém uma sub-rede denominada 'Subnet-1':</span><span class="sxs-lookup"><span data-stu-id="0d8d6-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="0d8d6-118">Adicionar pontos finais de balanceamento de carga para o ILB em cada VM</span><span class="sxs-lookup"><span data-stu-id="0d8d6-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="0d8d6-119">No exemplo de Olá acima, tiver chamado "sqlsvc1" e "sqlsvc2" execução 2 VM na nuvem de Olá "Sqlsvc" do serviço.</span><span class="sxs-lookup"><span data-stu-id="0d8d6-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="0d8d6-120">Depois de criar Olá ILB com `DirectServerReturn` mudar, adicionar pontos finais com balanceamento toohello ILB tooallow SQL tooconfigure Olá os serviços de escuta Olá para grupos de disponibilidade de carga.</span><span class="sxs-lookup"><span data-stu-id="0d8d6-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="0d8d6-121">Para obter mais informações sobre o SQL AlwaysOn, consulte [configurar um balanceador de carga interno para um grupo de Disponibilidade AlwaysOn no Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="0d8d6-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0d8d6-122">Veja Também</span><span class="sxs-lookup"><span data-stu-id="0d8d6-122">See Also</span></span>
[<span data-ttu-id="0d8d6-123">Começar a configurar um balanceador de carga com acesso de Internet</span><span class="sxs-lookup"><span data-stu-id="0d8d6-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="0d8d6-124">Começar a configurar um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="0d8d6-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="0d8d6-125">Configurar um modo de distribuição de Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="0d8d6-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="0d8d6-126">Configurar definições de tempo limite TCP inativo para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="0d8d6-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
