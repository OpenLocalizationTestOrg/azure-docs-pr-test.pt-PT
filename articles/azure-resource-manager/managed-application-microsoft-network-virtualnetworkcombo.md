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
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="dae40-103">Elemento de IU Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="dae40-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="dae40-104">Um grupo de controlos para selecionar uma rede virtual nova ou existente.</span><span class="sxs-lookup"><span data-stu-id="dae40-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="dae40-105">Utilize este elemento quando [criar uma aplicação gerida do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="dae40-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="dae40-106">Exemplo de IU</span><span class="sxs-lookup"><span data-stu-id="dae40-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="dae40-108">No modelo de arames superior de Olá, utilizador de Olá tiver selecionado uma nova rede virtual, para que o utilizador Olá pode personalizar o prefixo de nome e endereço de cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="dae40-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="dae40-109">Neste caso, a configuração de sub-redes é opcional.</span><span class="sxs-lookup"><span data-stu-id="dae40-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="dae40-110">No modelo de arames do Olá na parte inferior, utilizador Olá tenha selecionado uma rede virtual existente, para que o utilizador Olá tem de mapear cada modelo de implementação de Olá sub-rede requer tooan sub-rede existente.</span><span class="sxs-lookup"><span data-stu-id="dae40-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="dae40-111">Sub-redes neste caso, é necessário configurar.</span><span class="sxs-lookup"><span data-stu-id="dae40-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="dae40-112">Esquema</span><span class="sxs-lookup"><span data-stu-id="dae40-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="dae40-113">Observações</span><span class="sxs-lookup"><span data-stu-id="dae40-113">Remarks</span></span>
- <span data-ttu-id="dae40-114">Se for especificado, Olá prefixo de endereço sem se sobreporem primeiro tamanho `defaultValue.addressPrefixSize` é determinado automaticamente com base nas redes virtuais existentes na subscrição do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="dae40-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="dae40-115">Olá valor predefinido para `defaultValue.name` e `defaultValue.addressPrefixSize` é **nulo**.</span><span class="sxs-lookup"><span data-stu-id="dae40-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="dae40-116">`constraints.minAddressPrefixSize`tem de ser especificado.</span><span class="sxs-lookup"><span data-stu-id="dae40-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="dae40-117">As redes virtuais existentes com um espaço de endereços com tamanho inferior ao hello valor especificado não se encontram disponíveis para seleção.</span><span class="sxs-lookup"><span data-stu-id="dae40-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="dae40-118">`subnets`tem de ser especificado, e `constraints.minAddressPrefixSize` tem de ser especificado para cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="dae40-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="dae40-119">Ao criar uma nova rede virtual, o prefixo de endereço de cada sub-rede é calculado automaticamente com base no prefixo do endereço da rede virtual Olá e o respetivo `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="dae40-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="dae40-120">Quando utilizar um existente virtual de rede, quaisquer sub-redes menores do que o respetivo `constraints.minAddressPrefixSize` não estão disponíveis para seleção.</span><span class="sxs-lookup"><span data-stu-id="dae40-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="dae40-121">Além disso, se for especificado, as sub-redes que contenha, pelo menos, `minAddressCount` endereços disponíveis estão indisponíveis para seleção.</span><span class="sxs-lookup"><span data-stu-id="dae40-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="dae40-122">valor predefinido de Olá é **0**.</span><span class="sxs-lookup"><span data-stu-id="dae40-122">hello default value is **0**.</span></span> <span data-ttu-id="dae40-123">tooensure Olá endereços disponíveis são contíguo, especifique **verdadeiro** para `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="dae40-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="dae40-124">valor predefinido de Olá é **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="dae40-124">hello default value is **true**.</span></span>
- <span data-ttu-id="dae40-125">A criação de sub-redes na rede virtual existente não é suportada.</span><span class="sxs-lookup"><span data-stu-id="dae40-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="dae40-126">Se `options.hideExisting` é **verdadeiro**, utilizador de Olá não é possível escolher uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="dae40-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="dae40-127">valor predefinido de Olá é **falso**.</span><span class="sxs-lookup"><span data-stu-id="dae40-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="dae40-128">Resultado da amostra</span><span class="sxs-lookup"><span data-stu-id="dae40-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="dae40-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dae40-129">Next steps</span></span>
* <span data-ttu-id="dae40-130">Para aplicações de toomanaged uma introdução, consulte [descrição geral do Azure gerida aplicações](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dae40-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="dae40-131">Para definições de IU toocreating uma introdução, consulte [introdução CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dae40-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="dae40-132">Para obter uma descrição de propriedades comuns de elementos de IU, consulte [CreateUiDefinition elementos](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="dae40-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
