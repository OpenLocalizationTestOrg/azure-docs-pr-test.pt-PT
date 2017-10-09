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
# <a name="configure-load-balancer-for-sql-always-on"></a>Configurar o Balanceador de carga para SQL Server sempre no

Grupos de Disponibilidade AlwaysOn do SQL Server podem agora ser executados com o ILB. Grupo de disponibilidade está a solução de flagship do SQL Server para elevada disponibilidade e recuperação após desastre. Olá escuta do grupo de disponibilidade permite que os cliente aplicações tooseamlessly ligar toohello réplica primária, independentemente do número de Olá de réplicas de Olá na configuração de Olá.

nome do serviço de escuta (DNS) Olá é o endereço IP de tooa mapeado com balanceamento de carga e Balanceador de carga do Azure direciona Olá receber tráfego tooonly Olá servidor primário no conjunto de réplicas Olá.

Pode utilizar o suporte do ILB para pontos finais do SQL Server AlwaysOn (serviço de escuta). Agora tem controlo sobre acessibilidade Olá do serviço de escuta de Olá e pode escolher endereço IP com balanceamento de carga Olá uma sub-rede específica na sua rede Virtual (VNet).

Utilizando o ILB no serviço de escuta de Olá, Olá ponto final do SQL server (por exemplo, servidor = tcp:ListenerName, 1433; base de dados = DatabaseName) é acessível apenas a:

* Olá, serviços e VMs na mesma rede Virtual
* Os serviços e VMs a partir da rede ligados ao local
* Os serviços e as VMs de VNets interligadas

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Figura 1 - AlwaysOn de SQL Server configurada com Balanceador de carga para a Internet

## <a name="add-internal-load-balancer-toohello-service"></a>Adicionar serviço de toohello do Balanceador de carga interno

1. No seguinte exemplo de Olá, iremos irá configurar uma rede Virtual que contém uma sub-rede denominada 'Subnet-1':

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Adicionar pontos finais de balanceamento de carga para o ILB em cada VM

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    No exemplo de Olá acima, tiver chamado "sqlsvc1" e "sqlsvc2" execução 2 VM na nuvem de Olá "Sqlsvc" do serviço. Depois de criar Olá ILB com `DirectServerReturn` mudar, adicionar pontos finais com balanceamento toohello ILB tooallow SQL tooconfigure Olá os serviços de escuta Olá para grupos de disponibilidade de carga.

Para obter mais informações sobre o SQL AlwaysOn, consulte [configurar um balanceador de carga interno para um grupo de Disponibilidade AlwaysOn no Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>Veja Também
[Começar a configurar um balanceador de carga com acesso de Internet](load-balancer-get-started-internet-arm-ps.md)

[Começar a configurar um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição de Balanceador de carga](load-balancer-distribution-mode.md)

[Configurar definições de tempo limite TCP inativo para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
