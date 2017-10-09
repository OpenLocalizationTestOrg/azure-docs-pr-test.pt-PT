---
title: "elemento de IU de SizeSelector de aplicações geridas aaaAzure | Microsoft Docs"
description: "Descreve Olá elemento Microsoft.Compute.SizeSelector IU para aplicações geridas do Azure"
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Elemento de IU Microsoft.Compute.SizeSelector
Um controlo para selecionar um tamanho de uma ou mais instâncias de máquina virtual. Utilize este elemento quando [criar uma aplicação gerida do Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemplo de IU
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Observações
- `recommendedSizes`deve conter, pelo menos, um tamanho. em primeiro lugar, Olá recomendado tamanho é utilizado como predefinição de Olá.
- Se um tamanho recomendado não está disponível na localização de Olá selecionado, o tamanho de Olá automaticamente é ignorado. Em vez disso, hello seguinte tamanho recomendado é utilizado.
- Qualquer dimensão não especificado na Olá `constraints.allowedSizes` está oculto e qualquer dimensão não especificado na `constraints.excludedSizes` é apresentado.
`constraints.allowedSizes`e `constraints.excludedSizes` são opcionais, mas não podem ser utilizados em simultâneo. é possível determinar a lista de Olá de tamanhos disponíveis ao chamar [listar tamanhos de máquina virtual disponíveis para uma subscrição](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).
- `osPlatform`tem de ser especificado e pode ser **Windows** ou **Linux**. Utilizou os custos de hardware de Olá toodetermine das máquinas de virtuais Olá.
- `imageReference`for omitido para imagens originais, mas fornecido para imagens de terceiros. Utilizou o custos de software Olá toodetermine das máquinas de virtuais Olá.
- `count`é utilizado tooset Olá multiplicador adequado para o elemento de Olá. Suporta um valor estático, tal como **2**, ou como um valor dinâmico de outro elemento, `[steps('step1').vmCount]`. valor predefinido de Olá é **1**.

## <a name="sample-output"></a>Resultado da amostra
```json
"Standard_D1"
```

## <a name="next-steps"></a>Passos seguintes
* Para aplicações de toomanaged uma introdução, consulte [descrição geral do Azure gerida aplicações](managed-application-overview.md).
* Para definições de IU toocreating uma introdução, consulte [introdução CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para obter uma descrição de propriedades comuns de elementos de IU, consulte [CreateUiDefinition elementos](managed-application-createuidefinition-elements.md).
