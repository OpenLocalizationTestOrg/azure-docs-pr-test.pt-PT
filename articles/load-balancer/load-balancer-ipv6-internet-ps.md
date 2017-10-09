---
title: "Balanceador de carga aaaCreate um Azure através da Internet com o IPv6 - PowerShell | Microsoft Docs"
description: "Saiba como toocreate um para a Internet carregar balanceador com o IPv6 através do PowerShell para o Resource Manager"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, o Balanceador de carga do azure, pilha dupla, ip público, ipv6 nativo, móveis, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a>Começar a criar uma com acesso à Balanceador de carga com o IPv6 através do PowerShell para o Gestor de recursos de Internet

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [CLI do Azure](load-balancer-ipv6-internet-cli.md)
> * [Modelo](load-balancer-ipv6-internet-template.md)

Um balanceador de carga do Azure é um balanceador de carga de Camada 4 (TCP, UDP). Balanceador de carga Olá fornece elevada disponibilidade por distribuição de tráfego de entrada entre instâncias de bom estado de funcionamento de serviço nos serviços em nuvem ou de máquinas virtuais num conjunto de Balanceador de carga. O Balanceador de Carga do Azure pode também apresentar esses serviços em várias portas, vários endereços IP ou ambos.

## <a name="example-deployment-scenario"></a>Cenário de implementação de exemplo

Olá diagrama seguinte ilustra a ser implementada neste artigo de solução de balanceamento de carga Olá.

![Cenário do Balanceador de carga](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

Neste cenário, irá criar Olá os seguintes recursos do Azure:

* um balanceador de carga com acesso à Internet com o endereço IP público de IPv6 e IPv4
* dois carregar balanceamento regras toomap Olá VIPs toohello privados pontos finais públicos
* um toothat do conjunto de disponibilidade contém Olá duas VMs
* duas máquinas virtuais (VMs)
* interface de rede virtual para cada VM com endereços IPv4 e IPv6 atribuído

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a>Implementar a solução Olá utilizando Olá Azure PowerShell

Olá, os passos seguintes mostra como o com o Azure Resource Manager com o PowerShell de Balanceador de carga de toocreate um para a Internet. Com o Azure Resource Manager, cada recurso é criado e configurado individualmente, em seguida, juntar toocreate um recurso.

toodeploy um balanceador de carga, criar e configurar Olá seguintes objetos:

* Configuração de IP front-end - contém os endereços IP públicos para o tráfego de rede recebido.
* Conjunto de endereços de back-end - contém interfaces de rede (NICs) Olá máquinas virtuais tooreceive tráfego de rede do Balanceador de carga Olá.
* Regras de balanceamento de carga - contém regras de mapeamento de uma porta pública no Olá tooport de Balanceador de carga no conjunto de endereços de back-end de Olá.
* Regras NAT de entrada - contém regras de mapeamento de uma porta pública na porta tooa de Balanceador de carga do Olá para uma máquina virtual específica num conjunto de endereços de back-end de Olá.
* As sondas - contém o estado de funcionamento das sondas utilizadas toocheck disponibilidade de instâncias de máquinas virtuais num conjunto de endereços de back-end de Olá.

Para obter mais informações, veja [Suporte do Azure Resource Manager para o Load Balancer](load-balancer-arm.md).

## <a name="set-up-powershell-toouse-resource-manager"></a>Configurar toouse do PowerShell do Resource Manager

Certifique-se de que dispõe Olá versão de produção mais recente do módulo do Azure Resource Manager Olá para o PowerShell.

1. Inicie sessão no Azure

    ```powershell
    Login-AzureRmAccount
    ```

    Introduza as credenciais quando lhe for pedido.

2. Verifique Olá subscrições para a conta de Olá

    ```powershell
    Get-AzureRmSubscription
    ```

3. Escolha qual das suas toouse de subscrições do Azure.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. Criar um grupo de recursos (ignore este passo se utilizar um grupo de recursos existente)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Criar uma rede virtual e um endereço IP público para o conjunto IP Front-end Olá

1. Crie uma rede virtual com uma sub-rede.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Crie recursos de (PIP) do conjunto de endereços IP Front-end Olá de endereço IP público do Azure.

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > Balanceador de carga Olá utiliza etiqueta de Olá de domínio do IP público Olá como prefixo para o FQDN. Neste exemplo, são Olá FQDNs *lbnrpipv4.westus.cloudapp.azure.com* e *lbnrpipv6.westus.cloudapp.azure.com*.

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a>Criar configurações de IP de front-end e um conjunto de endereços de Back-End

1. Crie a configuração do endereço front-end que utiliza endereços de IP público Olá que criou.

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. Crie conjuntos de endereços de back-end.

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a>Criar regras LB, regras NAT, uma pesquisa e um balanceador de carga

Este exemplo cria Olá seguintes itens:

* regra de um NAT tootranslate todo o tráfego de entrada na porta 443 tooport 4443
* um toobalance de regra de Balanceador de carga todo o tráfego de entrada na porta 80 tooport 80 no Olá endereços no conjunto de back-end Olá.
* uma carga balanceador regra tooallow RDP ligação toohello VMs na porta 3389.
* um Estado de funcionamento do sonda regra toocheck Olá numa página com o nome *HealthProbe.aspx* ou um serviço na porta 8080
* um balanceador de carga que utiliza os objetos

1. Crie Olá regras NAT.

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. Crie uma sonda de estado de funcionamento. Existem duas formas tooconfigure uma sonda:

    Sonda HTTP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    ou sonda TCP

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    Neste exemplo, vamos Olá toouse que sondas de TCP.

3. Crie uma regra de balanceador de carga.

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. Crie Balanceador de carga de Olá utilizando objetos de Olá criado anteriormente.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a>Criar o NICs para Olá VMs do back-end

1. Obter Olá rede Virtual e a sub-rede de rede Virtual, onde Olá NICs têm toobe criado.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Crie configurações de IP e NICs para Olá VMs.

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a>Criar máquinas virtuais e atribuir Olá recém-criado NICs

Para obter mais informações sobre como criar uma VM, consulte [criar e pré-configurar uma Máquina Virtual do Windows com o Resource Manager e o Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Criar uma conta de armazenamento e de conjunto de disponibilidade

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. Criar cada VM e atribuir Olá anterior criado NICs

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a>Passos seguintes

[Começar a configurar um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição de balanceador de carga](load-balancer-distribution-mode.md)

[Configurar definições de tempo limite TCP inativo para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
