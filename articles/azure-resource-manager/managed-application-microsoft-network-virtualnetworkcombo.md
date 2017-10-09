---
title: "elemento de IU de VirtualNetworkCombo de aplicações geridas aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Network.VirtualNetworkCombo IU para aplicações geridas do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Elemento de IU Microsoft.Network.VirtualNetworkCombo
Um grupo de controlos para selecionar uma rede virtual nova ou existente. Utilize este elemento quando [criar uma aplicação gerida do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de IU
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- No modelo de arames superior de Olá, utilizador de Olá tiver selecionado uma nova rede virtual, para que o utilizador Olá pode personalizar o prefixo de nome e endereço de cada sub-rede. Neste caso, a configuração de sub-redes é opcional.
- No modelo de arames do Olá na parte inferior, utilizador Olá tenha selecionado uma rede virtual existente, para que o utilizador Olá tem de mapear cada modelo de implementação de Olá sub-rede requer tooan sub-rede existente. Sub-redes neste caso, é necessário configurar.

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>Observações
- Se for especificado, Olá prefixo de endereço sem se sobreporem primeiro tamanho `defaultValue.addressPrefixSize` é determinado automaticamente com base nas redes virtuais existentes na subscrição do utilizador Olá.
- Olá valor predefinido para `defaultValue.name` e `defaultValue.addressPrefixSize` é **nulo**.
- `constraints.minAddressPrefixSize`tem de ser especificado. As redes virtuais existentes com um espaço de endereços com tamanho inferior ao hello valor especificado não se encontram disponíveis para seleção.
- `subnets`tem de ser especificado, e `constraints.minAddressPrefixSize` tem de ser especificado para cada sub-rede.
- Ao criar uma nova rede virtual, o prefixo de endereço de cada sub-rede é calculado automaticamente com base no prefixo do endereço da rede virtual Olá e o respetivo `addressPrefixSize`.
- Quando utilizar um existente virtual de rede, quaisquer sub-redes menores do que o respetivo `constraints.minAddressPrefixSize` não estão disponíveis para seleção. Além disso, se for especificado, as sub-redes que contenha, pelo menos, `minAddressCount` endereços disponíveis estão indisponíveis para seleção.
valor predefinido de Olá é **0**. tooensure Olá endereços disponíveis são contíguo, especifique **verdadeiro** para `requireContiguousAddresses`. valor predefinido de Olá é **verdadeiro**.
- A criação de sub-redes na rede virtual existente não é suportada.
- Se `options.hideExisting` é **verdadeiro**, utilizador de Olá não é possível escolher uma rede virtual existente. valor predefinido de Olá é **falso**.

## <a name="sample-output"></a>Resultado da amostra
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>Passos seguintes
* Para aplicações de toomanaged uma introdução, consulte [descrição geral do Azure gerida aplicações](managed-application-overview.md).
* Para definições de IU toocreating uma introdução, consulte [introdução CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição de propriedades comuns de elementos de IU, consulte [CreateUiDefinition elementos](managed-application-createuidefinition-elements.md).
