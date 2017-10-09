---
title: 'Ligar a rede virtual tooanother VNet: CLI do Azure | Microsoft Docs'
description: "Este artigo explica como ligar redes virtuais entre si através do Azure Resource Manager e da CLI do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Configurar uma ligação de gateway de VPN de VNet a VNet com a CLI do Azure

Este artigo mostra como toocreate uma ligação de gateway VPN entre redes virtuais. Olá redes virtuais podem estar em Olá regiões idêntica ou diferentes e de Olá mesmo ou subscrições diferentes. Quando ao ligar VNets de diferentes subscrições, subscrições Olá não é necessário toobe associado Olá mesmo inquilino do Active Directory. 

passos de Olá neste artigo aplicam-se modelo de implementação do Resource Manager toohello e utilizam a CLI do Azure. Também pode criar esta configuração utilizando uma ferramenta de implementação diferentes ou modelo de implementação, selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI do Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Ligue diferentes modelos de implementação - portal do Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Ligue diferentes modelos de implementação - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Ligar a rede virtual tooanother rede virtual (VNet a VNet) é semelhante tooconnecting uma localização de site do VNet tooan no local. Ambos os tipos de conetividade utilizam um tooprovide de gateway VPN um túnel seguro através de IPsec/IKE. Se as suas VNets estiverem na Olá mesma região, poderá ser útil tooconsider ligá-las a utilização de VNet Peering. O VNet peering não utiliza um gateway de VPN. Para obter mais informações, veja [VNet peering](../virtual-network/virtual-network-peering-overview.md).

A comunicação VNet a VNet pode ser combinada com configurações multilocal. Isto permite-lhe estabelecer topologias de rede que combinam uma conectividade entre instalações com conectividade de rede intervirtual, como mostrado na Olá diagrama a seguir:

![Acerca das ligações](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Por que motivo ligar redes virtuais?

Poderá pretender redes virtuais tooconnect para Olá seguintes motivos:

* **Geopresença e georredundância entre várias regiões**

  * Pode configurar a sua própria georreplicação ou sincronização com uma conetividade segura sem passar por pontos finais com acesso à Internet.
  * Com o Gestor de Tráfego e o Balanceador de Carga do Azure, pode configurar uma carga de trabalho de elevada disponibilidade com georredundância em várias regiões do Azure. Um exemplo importante consiste tooset cópias de segurança SQL Always On com grupos de disponibilidade propagando-se em várias regiões do Azure.
* **Aplicações multicamadas regionais com isolamento ou limites administrativos**

  * Olá da mesma região, pode configurar aplicações de várias camadas com várias redes virtuais ligadas em conjunto devido tooisolation ou a requisitos administrativos.

Para obter mais informações sobre ligações VNet a VNet, consulte Olá [FAQ de VNet a VNet](#faq) no fim de Olá deste artigo.

### <a name="which-set-of-steps-should-i-use"></a>Que conjunto de passos devo utilizar?

Neste artigo, verá dois conjuntos de passos diferentes. Um conjunto de passos para [Olá de VNets que residem na mesma subscrição](#samesub)e outra para [VNets que residem em subscrições diferentes](#difsub).

## <a name="samesub"></a>Ligar VNets que estão no Olá mesma subscrição

![Diagrama v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Antes de começar

Antes de começar, instale a versão mais recente do Olá dos comandos da CLI Olá (2.0 ou posteriores). Para obter informações sobre a instalação de comandos da CLI Olá, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).

### <a name="Plan"></a>Planear os intervalos de endereços IP

Olá os passos seguintes, vamos criar duas redes virtuais juntamente com as respetivas sub-redes de gateway e configurações. Em seguida, criamos uma ligação VPN entre Olá duas VNets. É importante tooplan intervalos de endereços IP Olá para a sua configuração de rede. Nota: precisa confirmar que nenhum dos intervalos de VNet ou intervalos de rede local se sobrepõe de modo algum. Nestes exemplos, não incluímos um servidor DNS. Se pretender a resolução de nomes para as suas redes virtuais, veja [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Resolução de nomes).

Podemos utilizar Olá valores nos exemplos de Olá os seguintes:

**Valores da TestVNet1:**

* Nome da VNet: TestVNet1
* Grupo de Recursos: TestRG1
* Localização: EUA Leste
* TestVNet1: 10.11.0.0/16 e 10.12.0.0/16
* Front-End: 10.11.0.0/24
* Back-End: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* IP Público: VNet1GWIP
* VPNType: RouteBased
* Ligação (1 a 4): VNet1toVNet4
* Ligação (1 a 5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Valores da TestVNet4:**

* Nome da VNet: TestVNet4
* TestVNet2: 10.41.0.0/16 e 10.42.0.0/16
* Front-End: 10.41.0.0/24
* Back-End: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Grupo de Recursos: TestRG4
* Localização: EUA Oeste
* GatewayName: VNet4GW
* IP Público: VNet4GWIP
* VPNType: RouteBased
* Ligação: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Connect"></a>Passo 1 – ligar tooyour subscrição

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Passo 2 - Criar e configurar a TestVNet1

1. Crie um grupo de recursos.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. Crie a TestVNet1 e Olá sub-redes da TestVNet1. Este exemplo cria uma rede virtual com o nome TestVNet1 e uma sub-rede, com o nome FrontEnd.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Crie um espaço de endereços adicionais para a sub-rede de back-end Olá. Tenha em atenção que neste passo, vamos especificar ambos os espaços de endereços de Olá criamos anteriormente e Olá espaço de endereços adicionais que queremos tooadd. Isto acontece porque Olá [atualização de vnet az rede](https://docs.microsoft.com/cli/azure/network/vnet#update) comando substitui definições anteriores Olá. Certifique-se toospecify todos os prefixos de endereço Olá quando utilizar este comando.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Crie a sub-rede de back-end Olá.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Crie a sub-rede do gateway Olá. Tenha em atenção de que essa sub-rede de gateway Olá com o nome "GatewaySubnet". Este nome é obrigatório. Neste exemplo, a sub-rede do gateway Olá é utilizar/27. Embora seja possível toocreate uma sub-rede do gateway tão pequena como/29, recomendamos que crie uma sub-rede maior que inclua endereços mais ao selecionar, pelo menos, / 28 ou /27. Isto permitirá para suficiente endereços tooaccommodate possíveis configurações adicionais que poderá ser útil no Olá futuras.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Pedir um público IP endereço toobe toohello alocado gateway que será criado para a sua VNet. Repare que Olá AllocationMethod é dinâmico. Não é possível especificar o endereço IP Olá que pretende que o toouse. É gateway tooyour alocada dinamicamente.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. Crie gateway de rede virtual Olá da TestVNet1. As configurações VNet a VNet requerem um VpnType RouteBased. Se executar este comando utilizando Olá parâmetro '- sem - espera', não vir quaisquer comentários ou saída. Olá '- sem - espera' parâmetro permite que Olá gateway toocreate em segundo plano de Olá. Não significa desse gateway VPN Olá acaba de criar de imediato. Criar um gateway, muitas vezes, pode demorar 45 minutos ou mais, dependendo Olá SKU de gateway que utilizar.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>Passo 3 – Criar e configurar TestVNet4

1. Crie um grupo de recursos.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. Criar a TestVNet4.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. Crie sub-redes adicionais para TestVNet4.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Crie a sub-rede do gateway Olá.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Peça um Endereço IP público.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Crie gateway de rede virtual Olá TestVNet4.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Passo 4 – criar ligações Olá

Agora, tem duas VNets com gateways de VPN. Olá passo seguinte consiste em ligações de gateway VPN toocreate entre os gateways de rede virtual Olá. Se utilizou exemplos Olá acima, os gateways de VNet estão em grupos de recursos diferente. Quando gateways estão em grupos de recursos diferente, tem de tooidentify e especifique os IDs de recurso Olá para cada gateway quando efetuar uma nova ligação. Se as suas VNets estiverem na Olá mesmo grupo de recursos, pode utilizar Olá [segundo conjunto de instruções](#samerg) porque não precisa de IDs de recurso de Olá toospecify.

### <a name="diffrg"></a>tooconnect VNets que residem nos grupos de recursos diferente

1. Obter Olá ID de recurso dos VNet1GW do resultado Olá Olá os seguintes comandos:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  No resultado de Olá, determinar Olá "id:" linha. os valores de Olá nos aspas Olá são toocreate necessários Olá ligação na secção seguinte, Olá. Copie o editor de texto de tooa estes valores, como o Notepad, para que pode facilmente cole-os ao criar a ligação.

  Exemplo de saída:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Copie os valores de Olá após **"id":** dentro de aspas Olá.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Obter Olá ID de recurso dos VNet4GW e copie Olá valores tooa editor de texto.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Crie Olá TestVNet1 tooTestVNet4 ligação. Neste passo, criará Olá ligação da TestVNet1 tooTestVNet4. Há uma chave partilhada referenciada nos exemplos de Olá. Pode utilizar os seus próprios valores para a chave partilhada Olá. Olá coisa que essa chave partilhada Olá, é importante tem de corresponder ao ambas as ligações. Criar uma ligação demora uns toocomplete breves instantes.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Crie Olá TestVNet4 tooTestVNet1 ligação. Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet4 tooTestVNet1. Certifique-se de chaves de Olá partilhada correspondem. Demora alguns minutos ligação de Olá tooestablish.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Verifique as suas ligações. Veja [Verificar a ligação](#verify).

### <a name="samerg"></a>tooconnect VNets que residem no Olá mesmo grupo de recursos

1. Crie Olá TestVNet1 tooTestVNet4 ligação. Neste passo, criará Olá ligação da TestVNet1 tooTestVNet4. Grupos de recursos do aviso Olá são Olá mesmo nos exemplos de Olá. Pode também ver uma chave partilhada referenciada nos exemplos de Olá. Pode utilizar os seus próprios valores para a chave partilhada Olá, no entanto, tem de corresponder chave partilhada Olá ambas as ligações. Criar uma ligação demora uns toocomplete breves instantes.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Crie Olá TestVNet4 tooTestVNet1 ligação. Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet4 tooTestVNet1. Certifique-se de chaves de Olá partilhada correspondem. Demora alguns minutos ligação de Olá tooestablish.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Verifique as suas ligações. Veja [Verificar a ligação](#verify).

## <a name="difsub"></a>Ligar VNets que estão em subscrições diferentes

![Diagrama v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

Neste cenário, vamos ligar TestVNet1 e TestVNet5. Olá VNets residirem subscrições diferentes. subscrições de Olá não é necessário toobe associado Olá mesmo inquilino do Active Directory. Olá os passos para esta configuração de adicionar uma ligação VNet a VNet adicional na ordem tooconnect TestVNet1 tooTestVNet5.

### <a name="TestVNet1diff"></a>Passo 5 - Criar e configurar TestVNet1

Estas instruções continuam dos passos de Olá no Olá precedente secções. Tem de concluir [passo 1](#Connect) e [passo 2](#TestVNet1) toocreate e configurar a TestVNet1 e hello do VPN Gateway da TestVNet1. Para esta configuração, não são necessária toocreate TestVNet4 da secção anterior Olá, embora se criá-la, este será não entrar em conflito com estes passos. Depois de concluir o Passo 1 e o Passo 2, avance para o Passo 6 (abaixo).

### <a name="verifyranges"></a>Passo 6 – Certifique-se de intervalos de endereços IP Olá

Ao criar ligações adicionais, é importante tooverify que o espaço de endereços IP Olá da nova rede virtual Olá não se sobreponha a nenhum dos outros intervalos de Vnets ou intervalos de gateway de rede local. Para este exercício, pode utilizar Olá os seguintes valores para Olá TestVNet5:

**Valores da TestVNet5:**

* Nome da VNet: TestVNet5
* Grupo de Recursos: TestRG5
* Localização: Leste do Japão
* TestVNet5: 10.51.0.0/16 e 10.52.0.0/16
* Front-End: 10.51.0.0/24
* Back-End: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* IP Público: VNet5GWIP
* VPNType: RouteBased
* Ligação: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="TestVNet5"></a>Passo 7 – Criar e configurar TestVNet5

Este passo tem de ser efetuado no contexto de Olá de Olá nova subscrição, subscrição 5. Esta parte pode ser realizada pelo administrador de Olá numa organização diferente proprietária da subscrição Olá. tooswitch entre subscrições utilize ' lista de contas az – todos os ' toolist Olá conta tooyour disponíveis de subscrições, em seguida, utilize ' az conta set - subscrição <subscriptionID>' tooswitch toohello subscrição que pretende que o toouse.

1. Certifique-se de que está ligado tooSubscription 5, em seguida, cria um grupo de recursos.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. Criar a TestVNet5.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Adicione sub-redes.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Adicione sub-rede do gateway Olá.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Solicitar um endereço IP público.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Criar o gateway da TestVNet5 de Olá

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Passo 8 - criar ligações Olá

Iremos dividir este passo para duas sessões CLI marcada como **[subscrição 1]**, e **[subscrição 5]** porque gateways Olá estão em subscrições diferentes Olá. tooswitch entre subscrições utilize ' lista de contas az – todos os ' toolist Olá conta tooyour disponíveis de subscrições, em seguida, utilize ' az conta set - subscrição <subscriptionID>' tooswitch toohello subscrição que pretende que o toouse.

1. **[Subscrição 1]**  Iniciar sessão e ligar tooSubscription 1. Seguinte Olá executar comando tooget Olá nome e um ID de Olá Gateway da saída de Olá:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Copiar resultado da Olá para "id:". Envie Olá ID e nome de Olá de Olá VNet gateway (VNet1GW) toohello administrador da subscrição 5 por e-mail ou outro método.

  Exemplo de saída:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Subscrição 5]**  Iniciar sessão e ligar tooSubscription 5. Seguinte Olá executar comando tooget Olá nome e um ID de Olá Gateway da saída de Olá:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Copiar resultado da Olá para "id:". Envie Olá ID e nome de Olá de Olá VNet gateway (VNet5GW) toohello administrador da subscrição 1 por e-mail ou outro método.

3. **[Subscrição 1]**  Neste passo, poderá cria Olá ligação da TestVNet1 tooTestVNet5. Pode utilizar os seus próprios valores para a chave partilhada Olá, no entanto, tem de corresponder chave partilhada Olá ambas as ligações. Criar uma ligação pode demorar uns toocomplete breves instantes. Certifique-se que ligar tooSubscription 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Subscrição 5]**  Este passo é semelhante toohello um acima, exceto que está a criar ligação Olá da TestVNet5 tooTestVNet1. Certifique-se de que Olá partilhado chaves correspondem e que o se ligar tooSubscription 5.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Verifique as ligações de Olá
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>FAQ da ligação VNet a VNet
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Passos seguintes

* Assim que a ligação estiver concluída, pode adicionar redes virtuais do tooyour máquinas virtuais. Para obter mais informações, consulte Olá [documentação de Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Para informações sobre o BGP, consulte Olá [descrição geral do BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
