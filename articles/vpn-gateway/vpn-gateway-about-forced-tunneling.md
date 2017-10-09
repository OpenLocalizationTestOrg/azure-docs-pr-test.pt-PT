---
title: "Configurar a imposição do túnel para ligações do Azure Site a Site: clássico | Microsoft Docs"
description: "Como tooyour do tráfego de Internet vinculados back do tooredirect ou 'force' todos os localização no local."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Configurar a imposição do túnel utilizando o modelo de implementação clássica Olá

Imposição do túnel permite redirecionar ou "forçar" todos os vinculado à Internet tráfego back tooyour localização no local através de um túnel VPN Site a Site para inspeção e auditoria. Este é um requisito de segurança críticas para TI empresariais de maioria das políticas. Sem a imposição do túnel, o tráfego vinculado à Internet do seu VMs no Azure serão sempre atravessar da infraestrutura de rede do Azure diretamente saída toohello Internet, sem Olá opção tooallow, tráfego de Olá tooinspect ou auditoria. Acesso à Internet não autorizado pode provocar potencialmente tooinformation divulgação ou outros tipos de falhas de segurança.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Este artigo explica como configurar forçado túnel para redes virtuais criadas com o modelo de implementação clássica Olá. Imposição do túnel pode ser configurado utilizando o PowerShell, não através do portal Olá. Se quiser tooconfigure imposição do túnel para o modelo de implementação do Resource Manager Olá, selecione artigo clássico Olá na lista pendente a seguir:

> [!div class="op_single_selector"]
> * [PowerShell – Clássica](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell – Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Requisitos e considerações
Imposição do túnel no Azure está configurado através de rotas definidas pelo utilizador da rede virtual (UDR). Redirecionar o tráfego tooan no local site é expresso como um gateway de VPN do Azure de toohello de rota predefinida. Olá secção seguinte apresenta uma lista de limitação atual Olá de rotas e tabela de encaminhamento de Olá para uma rede Virtual do Azure:

* Cada sub-rede da rede virtual tem uma tabela de encaminhamento incorporada, do sistema. tabela de encaminhamento de sistema de Olá tem Olá seguintes três grupos de rotas:

  * **Rotas de VNet locais:** diretamente toohello destino VMs no Olá mesma rede virtual.
  * **No local rotas:** toohello VPN gateway do Azure.
  * **Rota predefinida:** toohello diretamente à Internet. Pacotes destinados a toohello endereços IP privados não abrangidos por rotas Olá dois anterior serão ignorados.
* Com a versão de Olá de rotas definidas pelo utilizador, pode criar um encaminhamento tooadd de tabela uma rota predefinida e, em seguida, associar Olá encaminhamento tabela tooyour VNet subnet(s) tooenable forçado túnel nessas sub-redes.
* É necessário tooset "site predefinido" entre a rede virtual do Olá em vários locais sites locais toohello ligado.
* Imposição do túnel tem de ser associado a uma VNet com um gateway VPN encaminhamento dinâmico (não um gateway estático).
* ExpressRoute imposição do túnel não está configurada através desta mecanismo, mas em vez disso, é ativado por uma rota predefinida através de Olá BGP de ExpressRoute de publicidade sessões de peering. Consulte Olá [documentação do ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) para obter mais informações.

## <a name="configuration-overview"></a>Descrição geral de configuração
No seguinte exemplo de Olá, Olá front-end sub-rede não está a ser forçada em túnel. Olá cargas de trabalho na sub-rede do front-end de Olá podem continuar tooaccept e responder a pedidos de toocustomer de Olá Internet diretamente. Olá sub-redes de camada média dimensão que e back-end são forçadas em túnel. Quaisquer ligações de saída do toohello duas sub-redes Internet será tooan forçada ou redirecionado novamente o site de no local através de um dos Olá que túneis S2S VPN.

Isto permite-lhe toorestrict e inspecionar o acesso à Internet das suas máquinas virtuais ou serviços em nuvem na Azure, ao continuar tooenable a arquitetura do serviço de várias camadas necessárias. Também pode aplicar forçada túnel toohello todo redes virtuais se existirem não cargas de trabalho para a Internet nas suas redes virtuais.

![Túnel Forçado](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Antes de começar
Certifique-se de que tem Olá seguintes itens antes da configuração do início.

* Uma subscrição do Azure. Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Uma rede virtual configurada. 
* versão mais recente Olá do Olá cmdlets Azure PowerShell. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre a instalação de cmdlets do PowerShell Olá.

## <a name="configure-forced-tunneling"></a>Configurar túnel forçado
Olá seguir o procedimento irá ajudar a especificar a imposição do túnel para uma rede virtual. passos de configuração de Olá correspondem o ficheiro de configuração de rede toohello VNet.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

Neste exemplo, Olá a rede virtual 'MultiTier VNet' tem três sub-redes: 'Front-end', 'Midtier' e 'Back-end' sub-redes, com ligações quatro locais cruzado: 'DefaultSiteHQ' e três ramos. 

passos de Olá irão definir Olá 'DefaultSiteHQ' como ligação de site Olá predefinido para a imposição do túnel e configurar Olá Midtier e back-end sub-redes toouse imposição do túnel.

1. Crie uma tabela de encaminhamento. Utilize Olá seguintes cmdlet toocreate a tabela de rota.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Adicione uma tabela de encaminhamento de toohello de rotas predefinidas. 

  Olá exemplo seguinte adiciona uma rota toohello tabela de encaminhamento predefinido criada no passo 1. Tenha em atenção que Olá apenas rota suportada é o prefixo de destino Olá de "0.0.0.0/0" toohello NextHop "O VPNGateway".

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Associe sub-redes de toohello de tabela Olá encaminhamento. 

  Depois de uma tabela de encaminhamento é criada e adicionado uma rota, utilize Olá tooadd de exemplo a seguir ou associar a sub-rede do Olá rota tabela tooa VNet. exemplo de Olá adiciona Olá rota tabela "MyRouteTable" toohello Midtier e back-end sub-redes da VNet MultiTier VNet.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Atribua um site predefinido para a imposição do túnel. 

  Olá precedente passo, scripts de cmdlet de exemplo de Olá criado Olá tabela de encaminhamento em associados Olá tootwo de tabela de rota de sub-redes de VNet Olá. passo restantes Olá é tooselect um site local entre as ligações de vários sites Olá da rede virtual do Olá como site de predefinido Olá ou túnel.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Cmdlets do PowerShell adicionais
### <a name="toodelete-a-route-table"></a>toodelete uma tabela de rota

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist uma tabela de rota

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete uma rota de uma tabela de rota

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove uma rota de sub-rede

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>tabela de rotas toolist Olá associada uma sub-rede

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>tooremove um site predefinido de um gateway de VPN da VNet

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```