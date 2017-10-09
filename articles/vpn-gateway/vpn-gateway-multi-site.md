---
title: "Ligar a sites de toomultiple uma rede virtual com Gateway de VPN e o PowerShell: clássico | Microsoft Docs"
description: "Este artigo irá guiá-lo através de vários locais no local sites tooa rede virtual com um Gateway de VPN para o modelo de implementação clássica Olá a ligar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Adicionar um tooa de ligação de Site para Site VNet com uma ligação de gateway VPN existente (clássica)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (clássico)](vpn-gateway-multi-site.md)
>
>

Este artigo orienta-o através do PowerShell tooadd Site a Site (S2S) ligações tooa gateway de VPN que tenha uma ligação existente a utilizar. Este tipo de ligação é frequentemente referido tooas uma configuração de "multilocal". Olá passos neste artigo aplicam-se redes toovirtual criadas utilizando o modelo de implementação clássica Olá (também conhecido como a gestão de serviço). Estes passos não aplicar as configurações de ligação coexistentes tooExpressRoute/Site a Site.

### <a name="deployment-models-and-methods"></a>Métodos e modelos de implementação

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Atualizamos esta tabela medida que novos artigos e ferramentas adicionais ficam disponíveis para esta configuração. Quando estiver disponível um artigo, criamos uma ligação diretamente tooit desta tabela.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>Sobre a ligação

Pode ligar vários locais sites tooa única rede virtual. Isto é especialmente apelativo para a criação de soluções de nuvem híbrida. Criar um gateway de rede virtual do Azure de tooyour ligação multilocal é semelhante toocreating outras ligações Site a Site. Na verdade, pode utilizar um gateway de VPN do Azure existente, desde que o gateway de Olá for dinâmico (baseado na rota).

Se já tiver uma rede virtual do gateway estático tooyour ligado, pode alterar toodynamic de tipo de gateway Olá sem necessitar de rede virtual do toorebuild Olá em vários sites do ordem tooaccommodate. Antes de alterar o tipo de encaminhamento Olá, certifique-se de que o gateway de VPN no local suporta configurações de VPN baseado na rota.

![diagrama multilocal](./media/vpn-gateway-multi-site/multisite.png "multilocal")

## <a name="points-tooconsider"></a>Tooconsider pontos

**Não será capaz de toouse Olá portal toomake alterações toothis rede virtual.** Terá de ficheiro de configuração do toomake alterações toohello rede em vez de utilizar o portal de Olá. Se efetuar alterações no portal de Olá, estes irá substituir as definições de referência de vários sites para esta rede virtual.

Devem sentir-se confortáveis ao utilizar o ficheiro de configuração de rede de Olá dentro do tempo Olá concluiu procedimento de vários sites Olá. No entanto, se tiver várias pessoas na sua configuração de rede, terá de toomake certificar-se de que todas as pessoas conhece esta limitação. Isto não significa que não é possível utilizar o portal de Olá de todo. Pode utilizá-lo para tudo o resto, exceto efetuar configuração alterações toothis rede virtual específico.

## <a name="before-you-begin"></a>Antes de começar

Antes de iniciar a configuração, certifique-se de que dispõe Olá seguintes:

* Hardware VPN compatíveis para cada localização no local. Verifique [sobre dispositivos VPN para conectividade de rede Virtual](vpn-gateway-about-vpn-devices.md) tooverify se o dispositivo de Olá que pretende que o toouse é algo que é conhecido toobe compatível.
* Um com acesso exterior IPv4 endereço IP público para cada dispositivo VPN. endereço IP Olá não pode estar localizado atrás de um NAT. Este é o requisito.
* Terá a versão mais recente de Olá tooinstall de Olá cmdlets Azure PowerShell. Certifique-se que instalar a versão de gestão de serviço (SM) Olá na versão de Gestor de recursos de toohello de adição. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações.
* Alguém que proficient em configurar o hardware VPN. Terá de toohave uma forte compreender como tooconfigure o dispositivo VPN ou trabalhar com alguém que does.
* intervalos de endereços do IP de Olá que pretende que toouse na sua rede virtual (se não tiver já criado uma).
* intervalos de endereços IP de Olá para cada um dos sites de rede local de Olá que irá ser ligar. Terá de certificar-se de que os intervalos de endereços IP de Olá para cada um dos sites de rede local Olá que pretende que o tooconnect toodo sobreposição não toomake. Caso contrário, o portal de Olá ou Olá REST API irão rejeitar configuração Olá que está a ser carregada.<br>Por exemplo, se tiver dois sites de rede local que ambos contêm Olá IP endereço intervalo 10.2.3.0/24 e tiver um pacote com um endereço de destino 10.2.3.3, Azure não sabe que site pretende toosend Olá pacote toobecause Olá intervalos de endereços são sobreposição. problemas de encaminhamento tooprevent, Azure não permite-lhe tooupload um ficheiro de configuração que tenha intervalos sobrepostos.

## <a name="1-create-a-site-to-site-vpn"></a>1. Criar uma Rede de VPNs
Se já tiver uma VPN de Site para Site com um gateway de encaminhamento dinâmico, great! Para poder continuar demasiado[exportar definições de configuração de rede virtual Olá](#export). Se não estiver, Olá a seguir:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Se já tiver uma rede virtual Site a Site, mas tem um gateway de encaminhamento estático (baseado em políticas):
1. Altere o encaminhamento de toodynamic de tipo do gateway. Uma VPN multilocal requer um gateway de encaminhamento dinâmico (também conhecido como baseado na rota). Escreva o seu gateway de toochange, irá precisar de gateway do toofirst eliminar Olá existente, em seguida, crie um novo. Para obter instruções, consulte [como toochange Olá o tipo de encaminhamento de VPN para o seu gateway](vpn-gateway-configure-vpn-gateway-mp.md).  
2. Configure o novo gateway e crie o túnel VPN. Para obter instruções, consulte [configurar um Gateway de VPN no Portal clássico do Azure de Olá](vpn-gateway-configure-vpn-gateway-mp.md). Em primeiro lugar, altere o encaminhamento de toodynamic de tipo do gateway.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Se não tiver uma rede virtual do Site para Site:
1. Criar a rede virtual do Site para Site a utilizar estas instruções: [criar uma rede Virtual com uma ligação de VPN de Site a Site no Portal clássico do Azure de Olá](vpn-gateway-site-to-site-create.md).  
2. Configurar um gateway de encaminhamento dinâmico a utilizar estas instruções: [configurar um Gateway de VPN](vpn-gateway-configure-vpn-gateway-mp.md). Ser tooselect se **encaminhamento dinâmico** para o seu tipo de gateway.

## <a name="export"></a>2. Exportar ficheiro de configuração de rede Olá
Exporte o ficheiro de configuração de rede do Azure executando Olá os seguintes comandos. Pode alterar a localização de Olá de Olá ficheiro tooexport tooa localização diferente se for necessário.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. Ficheiro de configuração de rede Olá aberta
Abra o ficheiro de configuração de rede Olá que transferiu no último passo de Olá. Utilize qualquer editor de xml que pretender. ficheiro de Olá deverá ter um aspeto semelhante toohello seguinte:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Adicionar várias referências de site
Quando adicionar ou remover informações de referência de site, terá de efetuar alterações de configuração toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef. Adicionar uma nova referência de local site aciona Azure toocreate um túnel de novo. No exemplo de Olá abaixo, a configuração de rede Olá é para uma ligação de site único. Guarde o ficheiro de Olá depois de terminar de efetuar as alterações.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

referências a sites adicionais tooadd (criar uma configuração de vários site), adicione simplesmente linhas adicionais "LocalNetworkSiteRef", conforme mostrado no exemplo Olá abaixo:

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. Ficheiro de configuração de rede de Olá de importação
Importar ficheiro de configuração de rede Olá. Quando importar este ficheiro com alterações de Olá, serão adicionados túneis Olá de novo. túneis Olá irão utilizar o gateway dinâmico Olá que criou anteriormente. Pode utilizar portal clássico Olá ou ficheiro de Olá tooimport do PowerShell.

## <a name="6-download-keys"></a>6. Transferir as chaves
Assim que foram adicionados os túneis novo, utilize Olá PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget Olá IPsec/IKE chaves pré-partilhadas para cada túnel.

Por exemplo:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

Se preferir, pode também utilizar Olá *obter Virtual rede Gateway chave partilhada* tooget de REST API Olá chaves pré-partilhadas.

## <a name="7-verify-your-connections"></a>7. Verifique as suas ligações
Verifique o estado de vários sites túnel Olá. Depois de transferir as chaves de Olá para cada túnel, poderá ser útil tooverify ligações. Utilize tooget 'Get-AzureVnetConnection' túneis uma lista de rede virtual, conforme mostrado no exemplo Olá abaixo. VNet1 é o nome de Olá do Olá VNet.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Exemplo de retorno:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre Gateways de VPN, consulte [acerca dos VPN Gateways](vpn-gateway-about-vpngateways.md).
