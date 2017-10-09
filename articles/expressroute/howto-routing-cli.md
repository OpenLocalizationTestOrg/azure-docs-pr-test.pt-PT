---
title: 'Como tooconfigure encaminhamento para um circuito ExpressRoute do Azure: CLI | Microsoft Docs'
description: "Este artigo ajuda-o a criar e aprovisionar Olá privado, público e peering da Microsoft de um circuito ExpressRoute. Este artigo mostra também como estado de Olá toocheck, atualizar ou eliminar peerings no seu circuito."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Criar e modificar o encaminhamento para um circuito ExpressRoute com a CLI

Este artigo ajuda-o a criar e gerir a configuração de encaminhamento para um circuito de ExpressRoute no modelo de implementação Resource Manager Olá com a CLI. Também pode verificar o estado de Olá, atualizar ou eliminar e retirar o aprovisionamento do peerings para um circuito ExpressRoute. Se quiser toouse toowork um método diferente com o seu circuito, selecione um artigo de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [CLI do Azure](howto-routing-cli.md)
> * [Vídeo - privada peering](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vídeo - peering público](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vídeo - peering da Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (clássico)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Pré-requisitos da configuração

* Antes de começar, instale a versão mais recente do Olá dos comandos da CLI Olá (2.0 ou posteriores). Para obter informações sobre a instalação de comandos da CLI Olá, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).
* Certifique-se de que reviu Olá [pré-requisitos](expressroute-prerequisites.md), [requisitos de encaminhamento](expressroute-routing.md), e [fluxo de trabalho](expressroute-workflows.md) páginas antes de iniciar a configuração.
* Deve ter um circuito ExpressRoute ativo. Siga as instruções de Olá demasiado[criar um circuito ExpressRoute](howto-circuit-cli.md) e ter circuito Olá ativado pelo seu fornecedor de conectividade antes de continuar. Olá circuito ExpressRoute tem de ser num Estado aprovisionado e ativado para que os comandos de Olá toorun capaz de toobe neste artigo.

Estas instruções aplicam-se apenas toocircuits criados com fornecedores de serviços de oferta de serviços de conectividade de camada 2. Se estiver a utilizar um fornecedor de serviço que oferece gerido Layer 3 serviços (normalmente, uma VPN de IP, como MPLS), o seu fornecedor de conectividade irá configurar e gerir encaminhamento por si.

Pode configurar um, dois ou todos os três peerings (Azure privado, Azure público e Microsoft) para um circuito ExpressRoute. Pode configurar peerings em qualquer ordem que escolha. No entanto, tem de se certificar de que concluir configuração Olá cada peering, um de cada vez.

## <a name="azure-private-peering"></a>Peering privado do Azure

Esta secção ajuda-o a criar, obter, atualizar e eliminar Olá configuração do peering privado do Azure para um circuito ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate peering privado do Azure

1. Instale a versão mais recente do Olá da CLI do Azure. Tem de utilizar Olá a versão mais recente do Olá Interface de linha de comandos do Azure (CLI). * Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.

  ```azurecli
  az login
  ```

  Selecione a subscrição de Olá pretende que o circuito de ExpressRoute toocreate

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Crie um circuito ExpressRoute. Siga Olá instruções toocreate um [circuito ExpressRoute](howto-circuit-cli.md) e solicite ao fornecedor de conectividade Olá.

  Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering privado do Azure. Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá. No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, continue a configuração utilizando os passos seguintes Olá.
3. Verifique toomake de circuito de ExpressRoute Olá se de que está aprovisionado e também ativado. Utilize o seguinte exemplo de Olá:

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  resposta Olá é semelhante toohello seguinte exemplo:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configure o peering privado do Azure para o circuito Olá. Certifique-se de que tem Olá seguintes itens antes de continuar com os passos seguintes Olá:

  * Um /30 sub-rede para a ligação primária Olá. a sub-rede de Olá não pode ser parte de qualquer espaço de endereços reservado para redes virtuais.
  * Um /30 sub-rede para a ligação secundária Olá. a sub-rede de Olá não pode ser parte de qualquer espaço de endereços reservado para redes virtuais.
  * Um tooestablish de ID de VLAN válido este peering. Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.
  * Número AS para peering. Pode utilizar números AS de 2 e 4 bytes. Pode utilizar um número AS privado para este peering. Assegure que não está a utilizar 65515.
  * **Opcional -** um hash MD5 se optar por toouse um.

  Utilize Olá seguir tooconfigure de exemplo para o seu circuito de peering privado do Azure:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Se optar por toouse um hash MD5, utilize o seguinte exemplo de Olá:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Assegure que especifica o seu número AS como ASN de peering, não cliente ASN.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview detalhes de peering privado do Azure

Pode obter os detalhes de configuração utilizando o seguinte exemplo de Olá:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

Olá de saída é semelhante toohello seguinte exemplo:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuração do peering privado do Azure

Pode atualizar qualquer parte da configuração de Olá utilizando o seguinte exemplo de Olá. Neste exemplo, Olá ID de VLAN do circuito Olá está a ser atualizado de 100 too500.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete peering privado do Azure

Pode remover a sua configuração de peering executando o seguinte exemplo de Olá:

> [!WARNING]
> Tem de se certificar de que todas as redes virtuais são desassociadas do Olá circuito ExpressRoute antes de executar este exemplo. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Peering público do Azure

Esta secção ajuda-o a criar, obter, atualizar e eliminar Olá configuração do peering público do Azure para um circuito ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate peering público do Azure

1. Instale a versão mais recente do Olá da CLI do Azure. Tem de utilizar Olá a versão mais recente do Olá Interface de linha de comandos do Azure (CLI). * Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.

  ```azurecli
  az login
  ```

  Selecione a subscrição de Olá para o qual pretende que o circuito de ExpressRoute toocreate.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Crie um circuito ExpressRoute.  Siga Olá instruções toocreate um [circuito ExpressRoute](howto-circuit-cli.md) e solicite ao fornecedor de conectividade Olá.

  Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir que o seu fornecedor de conectividade permite peering privado do Azure por si. Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá. No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, continue a configuração utilizando os passos seguintes Olá.
3. Verifique Olá tooensure de circuito de ExpressRoute está aprovisionado e também ativado. Utilize o seguinte exemplo de Olá:

  ```azurecli
  az network express-route list
  ```

  resposta Olá é semelhante toohello seguinte exemplo:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configure o peering público do Azure para o circuito Olá. Certifique-se de que tem Olá seguintes informações antes de prosseguir.

  * Um /30 sub-rede para a ligação primária Olá. Esta tem de ser um prefixo IPv4 válido.
  * Um /30 sub-rede para a ligação secundária Olá. Esta tem de ser um prefixo IPv4 válido.
  * Um tooestablish de ID de VLAN válido este peering. Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.
  * Número AS para peering. Pode utilizar números AS de 2 e 4 bytes.
  * **Opcional -** um hash MD5 se optar por toouse um.

  Execute Olá seguir tooconfigure de exemplo para o seu circuito de peering público do Azure:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Se optar por toouse um hash MD5, utilize o seguinte exemplo de Olá:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Assegure que especifica o seu número AS como ASN de peering, não cliente ASN.

### <a name="tooview-azure-public-peering-details"></a>tooview detalhes de peering público do Azure

Pode obter os detalhes de configuração com o seguinte exemplo de Olá:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

Olá de saída é semelhante toohello seguinte exemplo:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuração do peering público do Azure

Pode atualizar qualquer parte da configuração de Olá utilizando o seguinte exemplo de Olá. Neste exemplo, Olá ID de VLAN do circuito Olá está a ser atualizado de 200 too600.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete peering público do Azure

Pode remover a sua configuração de peering executando o seguinte exemplo de Olá:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Peering da Microsoft

Esta secção ajuda-o a criar, obter, atualizar e eliminar Olá configuração peering da Microsoft para um circuito ExpressRoute.

> [!IMPORTANT]
> Peering da Microsoft dos circuitos ExpressRoute que foram configuradas tooAugust anterior 1, 2017 terá todos os serviço prefixos anunciados através do peering da Microsoft hello, mesmo se os filtros de rota não estão definidos. Peering da Microsoft dos circuitos ExpressRoute que estão configurados em ou após 1 de Agosto de 2017 não terão qualquer prefixos anunciados até que está ligado um filtro de rota toohello circuito. Para obter mais informações, consulte [configurar um filtro de rota para peering da Microsoft](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate peering da Microsoft

1. Instale a versão mais recente do Olá da CLI do Azure. Versão mais recente do Olá de utilização de Olá Interface de linha de comandos do Azure (CLI). * Olá revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de iniciar a configuração.

  ```azurecli
  az login
  ```

  Selecione a subscrição de Olá para o qual pretende que o circuito de ExpressRoute toocreate.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Crie um circuito ExpressRoute. Siga Olá instruções toocreate um [circuito ExpressRoute](howto-circuit-cli.md) e solicite ao fornecedor de conectividade Olá.

  Se o seu fornecedor de conectividade oferecer serviços geridos de camada 3, pode pedir o tooenable de fornecedor de conectividade para si de peering privado do Azure. Nesse caso, não terá das instruções de toofollow indicadas nas secções seguintes Olá. No entanto, se o seu fornecedor de conectividade não gerir encaminhamento por si, depois de criar o seu circuito, continue a configuração utilizando os passos seguintes Olá.

3. Verifique toomake de circuito de ExpressRoute Olá se de que está aprovisionado e também ativado. Utilize o seguinte exemplo de Olá:

  ```azurecli
  az network express-route list
  ```

  resposta Olá é semelhante toohello seguinte exemplo:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configure o peering da Microsoft para o circuito Olá. Certifique-se de que tem Olá seguintes informações antes de continuar.

  * Um /30 sub-rede para a ligação primária Olá. Esta tem de ser um prefixo IPv4 público válido detido por si e registado num RIR/TIR.
  * Um /30 sub-rede para a ligação secundária Olá. Esta tem de ser um prefixo IPv4 público válido detido por si e registado num RIR/TIR.
  * Um tooestablish de ID de VLAN válido este peering. Certifique-se de que nenhum outro peering no circuito de Olá utiliza Olá mesmo ID de VLAN.
  * Número AS para peering. Pode utilizar números AS de 2 e 4 bytes.
  * Prefixos anunciados: tem de fornecer uma lista de todos os prefixos planear tooadvertise através de sessão de BGP Olá. São aceites apenas prefixos de endereços IP públicos. Se planear toosend um conjunto de prefixos, pode enviar uma lista separada por vírgulas. Estes prefixos têm de ser registado tooyou num RIR / TIR.
  * **Opcional -** cliente ASN: Se estiver a anunciar prefixos que não são registado toohello número AS de peering, pode especificar Olá como número toowhich estão registados.
  * Nome do registo de encaminhamento: Pode especificar Olá RIR / IRR em relação a que Olá como número e prefixos são registados.
  * **Opcional -** um hash MD5 se optar por toouse um.

   Execute o seguinte exemplo tooconfigure peering da Microsoft para o seu circuito de Olá:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>Detalhes do tooget Microsoft peering

Pode obter os detalhes de configuração utilizando o seguinte exemplo de Olá:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

Olá de saída é semelhante toohello seguinte exemplo:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configuração do peering da Microsoft tooupdate

Pode atualizar qualquer parte da configuração de Olá. Olá anunciados prefixos do circuito Olá estão a ser atualizados de 123.1.0.0/24 too124.1.0.0/24 no seguinte exemplo de Olá:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete peering da Microsoft

Pode remover a sua configuração de peering executando o seguinte exemplo de Olá:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Passos seguintes

Passo seguinte, [ligação tooan uma VNet circuito ExpressRoute](howto-linkvnet-cli.md).

* Para obter mais informações sobre o fluxo de trabalho do ExpressRoute, veja [Fluxos de trabalho do ExpressRoute](expressroute-workflows.md).
* Para obter mais informações sobre peering do circuito, veja [Circuitos ExpressRoute e domínios de encaminhamento](expressroute-circuit-peerings.md).
* Para obter mais informações sobre como trabalhar com redes virtuais, veja [Descrição geral da rede virtual](../virtual-network/virtual-networks-overview.md).