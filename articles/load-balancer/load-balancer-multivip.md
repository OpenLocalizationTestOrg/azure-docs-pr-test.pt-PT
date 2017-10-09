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
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Configurar vários VIPs num serviço em nuvem

Pode aceder a serviços em nuvem do Azure através de Olá Internet pública, utilizando um endereço IP fornecida pelo Azure. Este endereço IP público é referenciado tooas um VIP (virtual IP), uma vez que está ligado toohello Azure Balanceador de carga e não Olá instâncias de Máquina Virtual (VM) no serviço de nuvem Olá. Pode aceder a qualquer instância VM dentro de um serviço em nuvem através da utilização de um único VIP.

No entanto, existem cenários em que poderá ser necessário mais do que um VIP como um toohello de ponto de entrada mesmo serviço em nuvem. Por exemplo, o serviço em nuvem pode alojar vários sites que requeiram conectividade SSL com a porta predefinida Olá 443, como cada site é alojada para um cliente diferente ou inquilino. Neste cenário, precisa de toohave um outro endereço IP destinado ao público para cada site. Olá diagrama a seguir ilustra um típico web do multi-inquilino de alojamento com necessidade para SSL vários certificados em Olá mesmo Porta pública.

![Cenário de várias VIP SSL](./media/load-balancer-multivip/Figure1.png)

No exemplo de Olá acima, todos os Olá de utilização de VIPs mesma porta pública (443) e o tráfego é tooone redirecionado ou mais VMs com balanceamento de uma porta privada exclusiva para Olá um endereço IP de todos os sites de Olá de alojamento do serviço de nuvem Olá de carga.

> [!NOTE]
> Outro Olá utilização da Olá necessitando do situação vários VIPs está a alojar vários escuta de grupo de Disponibilidade AlwaysOn de SQL no mesmo conjunto de máquinas virtuais de Olá.

VIPs são dinâmicas por predefinição, o que significa que Olá real endereço IP atribuído toohello o serviço em nuvem pode alterar ao longo do tempo. tooprevent que aconteça, pode reservar um VIP para o seu serviço. toolearn mais informações sobre VIPs reservadas, consulte [reservado de IP público](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Consulte [preços do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/) para obter informações sobre preços em VIPs e IPs reservados.

Pode utilizar o PowerShell tooverify Olá VIPs utilizados pelos seus serviços em nuvem, bem como adicionar e remover VIPs, associar um ponto final tooan de VIP e configurar um VIP específico de balanceamento de carga.

## <a name="limitations"></a>Limitações

Neste momento, a funcionalidade de várias VIP está limitado toohello os seguintes cenários:

* **Apenas IaaS**. Só pode ativar várias VIP para serviços em nuvem que contêm as VMs. Não é possível utilizar várias VIP em cenários de PaaS com instâncias de função.
* **PowerShell apenas**. Só pode gerir várias VIP utilizando o PowerShell.

Estas limitações são temporárias e podem ser alterados em qualquer altura. Certifique-se toorevisit este alterações futuras de tooverify de página.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>O serviço em nuvem tooa tooadd um VIP
no serviço de tooyour tooadd um VIP, execute o seguinte comando do PowerShell de Olá:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

Este comando apresenta um resultado toohello semelhante exemplo a seguir:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>Como tooremove um VIP de um serviço em nuvem
Olá tooremove VIP adicionadas tooyour serviço no exemplo de Olá acima, Olá executar seguinte comando do PowerShell:

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> Apenas é possível remover um VIP caso não tooit pontos finais associados.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>Como tooretrieve VIP informações a partir de um serviço em nuvem
Olá tooretrieve VIPs associados a um serviço em nuvem, execute Olá seguinte script do PowerShell:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

script de Olá apresenta um resultado toohello semelhante exemplo a seguir:

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

Neste exemplo, o serviço em nuvem Olá tem 3 VIPs:

* **O Vip1** é Olá VIP predefinido, sabe que porque o valor de Olá para IsDnsProgrammedName é definido tootrue.
* **Vip2** e **Vip3** não são utilizados como não têm quaisquer endereços IP. Só irá ser utilizadas se associar um ponto final toohello VIP.

> [!NOTE]
> A subscrição só será cobrada por VIPs adicionais assim que estiverem associados um ponto final. Para obter mais informações sobre preços, consulte [preços do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>Como ponto final de tooan tooassociate um VIP

tooassociate um VIP num nuvem tooan ponto final de serviço, execute o seguinte comando do PowerShell de Olá:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

Olá comando cria um ponto final chamado toohello ligado VIP *Vip2* na porta *80*e associa-toohello VM com o nome *myVM1* num serviço em nuvem com o nome  *myService* utilizando *TCP* na porta *8080*.

configuração de Olá do tooverify, execute o seguinte comando do PowerShell de Olá:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

saída de Olá procura toohello semelhante seguinte exemplo:

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>Como tooenable balanceamento de carga num VIP específico

Pode associar um VIP único com várias máquinas virtuais para fins de balanceamento de carga. Por exemplo, tiver um serviço em nuvem com o nome *myService*e duas máquinas virtuais com o nome *myVM1* e *myVM2*. E o serviço de nuvem tem vários VIPs, um com o nome *Vip2*. Se quiser tooensure que todo o tráfego tooport *81* no *Vip2* é equilibrados entre *myVM1* e *myVM2* na porta *8181* , execute hello seguinte script do PowerShell:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

Também pode atualizar o seu toouse de Balanceador de carga um VIP diferentes. Por exemplo, se executar Olá comando do PowerShell abaixo, irá alterar conjunto toouse um VIP Vip1 com o nome de balanceamento de carga Olá:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Passos Seguintes

[Análise de registos para balanceamento de carga do Azure](load-balancer-monitor-log.md)

[Internet destinado ao balanceador descrição geral de carga](load-balancer-internet-overview.md)

[Começar a utilizar na Internet com o Balanceador de carga](load-balancer-get-started-internet-arm-ps.md)

[Descrição geral da rede virtual](../virtual-network/virtual-networks-overview.md)

[APIs REST do IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx)
