---
title: "aaaAccess e segurança nos modelos do Azure para VMs com Linux | Microsoft Docs"
description: "Tutorial do DotNet núcleos de Máquina Virtual do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 07e47189-680e-4102-a8d4-5a8eb9c00213
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88fedc8287c1f8ab8397a03ddefe1e60a686815e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a>Acesso e segurança de modelos Azure Resource Manager para VMs com Linux

Aplicações alojadas no Azure necessidade provável toobe acesso através de Olá internet ou uma VPN / ligação Expressroute com o Azure. Exemplo de aplicação do Olá loja de música, Olá web site é disponibilizada no Olá internet com um endereço IP público. Com acesso estabelecido, devem ser protegidos ligações toohello aplicação e acesso toohello recursos da máquina virtual próprios. Esta segurança de acesso é fornecida com um grupo de segurança de rede. 

Este documento fornece detalhes sobre como Olá aplicação da loja de música está protegida no modelo de Gestor de recursos do Azure de exemplo de Olá. Todas as dependências e configurações exclusivas são realçadas. Para uma experiência otimizada Olá, pré-implemente uma instância de trabalho, juntamente com o modelo do Azure Resource Manager Olá e Olá solução tooyour subscrição do Azure. modelo completo Olá pode ser encontrado aqui – [a implementação da loja de música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="public-ip-address"></a>Endereço IP público
tooprovide acesso público tooan recursos do Azure, um recurso de endereço IP público pode ser utilizado. Endereço IP público pode ser configurado com um endereço IP estático ou dinâmico. Se é utilizado um endereço dinâmico e a máquina virtual de Olá está parada e desalocada, endereços de Olá é removido. Quando a máquina de Olá é iniciada novamente, poderá atribuído um endereço IP público diferentes. tooprevent um IP endereços de alteração, pode ser utilizado um endereço IP reservado. 

Um endereço IP público pode ser adicionado o modelo do Azure Resource Manager tooan utilizando Olá Visual Studio Adicionar Assistente de novos recursos, ou por inserir um JSON válido de um modelo. 

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [endereço IP público](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicipaddressName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "public-ip-front"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Um endereço IP público pode ser associado com um adaptador de rede Virtual ou um balanceador de carga. Neste exemplo, uma vez Olá Web site da loja de música é balanceamento de carga em várias máquinas de virtuais, Olá endereço IP público é anexado toohello Balanceador de carga.

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [associação de endereço IP público com Balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Olá endereço IP público, como visto a partir de Olá portal do Azure. Repare que o endereço IP público Olá é Balanceador de carga tooa associados e não uma máquina virtual. Balanceadores de carga de rede estão descritos no documento seguinte do Olá desta série.

![Endereço IP público](./media/dotnet-core-3-access-security/pubip.png)

Para obter mais informações sobre os endereços IP públicos do Azure, consulte [endereços IP no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Grupo de segurança de rede
Depois do acesso foi estabelecida tooAzure recursos, este acesso deve ser limitado. Máquinas virtuais do Azure, proteger o acesso é realizado através de um grupo de segurança de rede. Exemplo de aplicação do arquivo de música Olá, todas as máquinas de toohello acesso é restrito, exceto para através da porta 80 para acesso http e a porta 22 para SSH acesso. Um grupo de segurança de rede podem ser adicionado modelo do Azure Resource Manager tooan utilizando Olá Visual Studio Adicionar Assistente de novos recursos, ou por inserir um JSON válido de um modelo.

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [grupo de segurança de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('nsgfront')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "nsg-front"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
}
```

Neste exemplo, o grupo de segurança de rede de Olá está associado ao objeto de sub-rede Olá declarado no recurso de rede Virtual Olá. 

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [associação de grupo de segurança de rede com a rede Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
```

Eis o grupo de segurança de rede que Olá aspeto do Olá portal do Azure. Tenha em atenção que pode ser associar um NSG com uma interface de sub-rede e / ou rede. Neste caso, Olá NSG é associado tooa sub-rede. Nesta configuração, hello regras de entrada aplicam tooall máquinas virtuais ligadas toohello sub-rede.

![Grupo de segurança de rede](./media/dotnet-core-3-access-security/nsg.png)

Para obter informações aprofundadas sobre grupos de segurança de rede, consulte [que é um grupo de segurança de rede](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Passo seguinte
<hr>

[Passo 3 - disponibilidade e dimensionamento em modelos Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

