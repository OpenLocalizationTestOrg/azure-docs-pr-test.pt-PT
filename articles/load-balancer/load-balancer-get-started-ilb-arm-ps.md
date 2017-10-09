---
title: aaaCreate interno um Azure o Balanceador de carga - PowerShell | Microsoft Docs
description: Saiba como o com o PowerShell no Gestor de recursos de Balanceador de carga de toocreate um interno
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>Criar um balanceador de carga interno com o PowerShell

> [!div class="op_single_selector"]
> * [Portal do Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo abrange utilizando o modelo de implementação Resource Manager de Olá, que a Microsoft recomenda-se para a maioria das implementações de novo em vez de Olá [modelo de implementação clássica](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

Olá, os passos seguintes explica como o com o Azure Resource Manager com o PowerShell de Balanceador de carga de toocreate um interno. Com o Azure Resource Manager, os itens de Olá toocreate um balanceador de carga interno estão configurados individualmente e, em seguida, combinados toocreate um balanceador de carga.

É necessário toocreate e configurar Olá os seguintes objetos toodeploy um balanceador de carga:

* Configuração de IP de fim do FrontPage - irá configurar o endereço IP privado Olá receber tráfego de rede
* Conjunto de endereços de back-end - irá configurar as interfaces de rede de Olá que receberão tráfego com balanceamento de carga Olá do conjunto de IP de front-end
* Regras de balanceamento de carga - origem e de configuração da porta local para Olá o Balanceador de carga.
* As sondas - configura a pesquisa de estado de funcionamento de Olá para instâncias de Máquina Virtual de Olá.
* Regras NAT de entrada - configura acesso toodirectly de regras de porta de Olá uma das instâncias de Máquina Virtual de Olá.

Pode obter mais informações sobre os componentes do balanceador de carga com o Azure resource manager em [Suporte do Azure Resource Manager para o balanceador de carga](load-balancer-arm.md).

Olá passos seguintes explicam como tooconfigure um balanceador de carga entre duas máquinas virtuais.

## <a name="setup-powershell-toouse-resource-manager"></a>A configuração do PowerShell toouse Resource Manager

Certifique-se de que tem Olá versão de produção mais recente do Olá módulo do Azure para o PowerShell e ter o PowerShell configurar corretamente tooaccess a sua subscrição do Azure.

### <a name="step-1"></a>Passo 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Passo 2

Verifique Olá subscrições para a conta de Olá

```powershell
Get-AzureRmSubscription
```

Será pedido tooAuthenticate com as suas credenciais.

### <a name="step-3"></a>Passo 3

Escolha qual das suas toouse de subscrições do Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>Criar Grupo de Recursos do balanceador de carga

Crie um grupo de recursos (ignore este passo se estiver a utilizar um grupo de recursos existente)

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização, Isto é utilizado como localização predefinida de Olá para recursos nesse grupo de recursos. Certifique-se de que todos os comandos toocreate irá utilizar um balanceador de carga Olá mesmo grupo de recursos.

No Olá exemplo acima é criado um grupo de recursos denominado "NRP-RG" e a localização "EUA Oeste".

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>Criar Rede Virtual e um endereço IP privado para conjunto IP de front-end

Cria uma sub-rede para a rede virtual Olá e atribui toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

Criar uma rede virtual:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Cria Olá de rede virtual e adiciona a rede virtual do Olá sub-rede lb sub-rede ser toohello NRPVNet e atribui toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>Criar Conjunto IP de front-end e conjunto de endereços de back-end

Como configurar um conjunto IP de front-end para Olá entrada carga tráfego de rede do Balanceador e back-end endereço conjunto tooreceive Olá com balanceamento de carga do tráfego.

### <a name="step-1"></a>Passo 1

Crie um conjunto IP de front-end com o endereço IP privado Olá 10.0.2.5 para Olá sub-rede 10.0.2.0/24 que será Olá receber tráfego ponto final da rede.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>Passo 2

Configurar um conjunto de endereços de back-end utilizado tooreceive tráfego de entrada a partir do conjunto IP de front-end:

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>Criar regras LB, regras NAT, sonda e balanceador de carga

Depois de criar o conjunto IP de front-end Olá e conjunto de endereços de back-end Olá, terá de regras de Olá toocreate que irão pertencer toohello recurso de Balanceador de carga:

### <a name="step-1"></a>Passo 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

exemplo de Olá acima está a criar Olá seguintes itens:

* Regra NAT de que todos os receber tráfego tooport 3441 passará tooport 3389.
* uma segunda regra NAT que todos os receber tráfego tooport 3442 passará tooport 3389.
* uma regra de Balanceador de carga que irá carregar o balanceamento de todo o tráfego de entrada na porta pública 80 toolocal porta 80 conjunto de endereços de back-end Olá.
* uma regra de pesquisa que irá verificar o estado de funcionamento de Olá para o caminho "HealthProbe.aspx"

### <a name="step-2"></a>Passo 2

Crie Balanceador de carga Olá adicionar todos os objetos (regras NAT, as regras de Balanceador de carga, configurações de pesquisa) em conjunto:

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>Criar interfaces de rede

Depois de criar Balanceador de carga interno Olá, tem de definir as interfaces de rede irão receber Olá com balanceamento de carga tráfego de rede recebido, regras NAT e sonda. interface de rede Olá neste caso é configurada individualmente e pode ser atribuído tooa máquina mais tarde.

### <a name="step-1"></a>Passo 1

Obter o recurso de Olá virtuais interfaces de rede de toocreate de rede e sub-rede:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

Este passo cria uma interface de rede que irá pertencer o conjunto de back-end de Balanceador de carga toohello e associar a primeira regra NAT Olá para RDP para esta interface de rede:

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>Passo 2

Crie uma segunda interface de rede denominada LB-Nic2-BE:

Este passo cria uma interface de rede segundo, atribuir toohello mesmo Balanceador de carga novamente terminar agrupamento e associar a segunda regra NAT Olá criado para RDP:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

resultado final de Olá mostrará seguinte Olá:

    $backendnic1

Resultado esperado:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
                           "PublicIpAddress": {
                             "Id": null
                           },
                           "LoadBalancerBackendAddressPools": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                             }
                           ],
                           "LoadBalancerInboundNatRules": [
                             {
                               "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                             }
                           ],
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>Passo 3

Utilize Olá comando Add-AzureRmVMNetworkInterface tooassign Olá NIC tooa máquina virtual.

Pode encontrar Olá instruções passo a passo toocreate uma máquina virtual e atribua tooa NIC seguir documentação Olá: [criar uma VM do Azure com o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

## <a name="add-hello-network-interface"></a>Adicione Olá interface de rede

Se já tiver uma máquina virtual criada, pode adicionar a interface de rede Olá com Olá os seguintes passos:

### <a name="step-1"></a>Passo 1

Carregar o recurso de Balanceador de carga Olá numa variável (se ainda não o fez que ainda). variável de Olá utilizado é chamado $lb e Olá utilize nomes mesmos do recurso de Balanceador de carga Olá criados acima.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>Passo 2

Variável de tooa de configuração de back-end Olá de carga.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>Passo 3

Carregar a interface de rede Olá já criado para uma variável. o nome de variável Olá utilizado é NIC de $. nome de interface de rede de Olá utilizado é Olá mesmo do exemplo Olá acima.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>Passo 4

Alterar a configuração de back-end Olá na interface de rede Olá.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>Passo 5

Guarde o objeto de interface de rede de Olá.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

Depois de uma interface de rede é adicionada o conjunto de back-end de Balanceador de carga toohello, começa a receber tráfego de rede com base em regras para o recurso de Balanceador de carga de balanceamento de carga Olá.

## <a name="update-an-existing-load-balancer"></a>Atualizar um balanceador de carga existente

### <a name="step-1"></a>Passo 1
Utilizar o Balanceador de carga Olá do exemplo Olá acima, atribuir $slb utilizando Get-AzureRmLoadBalancer toovariable de objeto de Balanceador de carga

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>Passo 2

No seguinte exemplo de Olá, irá adicionar uma nova regra de NAT de entrada utilizando a porta 81 no front-end de Olá e porta 8181 para back Olá end de Balanceador de carga existente do conjunto tooan

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>Passo 3

Guardar a configuração de novo Olá utilizando Set-AzureLoadBalancer

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>Remover um balanceador de carga

Utilizar Olá comando Remove-AzureRmLoadBalancer toodelete um balanceador de carga criado anteriormente com o nome "NRP-LB" num grupo de recursos denominado "NRP-RG"

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Pode utilizar Olá opcional mudar - linha de comandos do Force tooavoid Olá para eliminação.

## <a name="next-steps"></a>Passos seguintes

[Configurar um modo de distribuição de Balanceador de carga](load-balancer-distribution-mode.md)

[Configurar definições de tempo limite TCP inativo para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
