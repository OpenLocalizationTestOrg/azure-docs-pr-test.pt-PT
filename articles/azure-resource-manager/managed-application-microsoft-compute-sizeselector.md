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
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="9edb9-103">Elemento de IU Microsoft.Compute.SizeSelector</span><span class="sxs-lookup"><span data-stu-id="9edb9-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="9edb9-104">Um controlo para selecionar um tamanho de uma ou mais instâncias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9edb9-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="9edb9-105">Utilize este elemento quando [criar uma aplicação gerida do Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9edb9-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9edb9-106">Exemplo de IU</span><span class="sxs-lookup"><span data-stu-id="9edb9-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="9edb9-108">Esquema</span><span class="sxs-lookup"><span data-stu-id="9edb9-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="9edb9-109">Observações</span><span class="sxs-lookup"><span data-stu-id="9edb9-109">Remarks</span></span>
- <span data-ttu-id="9edb9-110">`recommendedSizes`deve conter, pelo menos, um tamanho.</span><span class="sxs-lookup"><span data-stu-id="9edb9-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="9edb9-111">em primeiro lugar, Olá recomendado tamanho é utilizado como predefinição de Olá.</span><span class="sxs-lookup"><span data-stu-id="9edb9-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="9edb9-112">Se um tamanho recomendado não está disponível na localização de Olá selecionado, o tamanho de Olá automaticamente é ignorado.</span><span class="sxs-lookup"><span data-stu-id="9edb9-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="9edb9-113">Em vez disso, hello seguinte tamanho recomendado é utilizado.</span><span class="sxs-lookup"><span data-stu-id="9edb9-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="9edb9-114">Qualquer dimensão não especificado na Olá `constraints.allowedSizes` está oculto e qualquer dimensão não especificado na `constraints.excludedSizes` é apresentado.</span><span class="sxs-lookup"><span data-stu-id="9edb9-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="9edb9-115">`constraints.allowedSizes`e `constraints.excludedSizes` são opcionais, mas não podem ser utilizados em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="9edb9-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="9edb9-116">é possível determinar a lista de Olá de tamanhos disponíveis ao chamar [listar tamanhos de máquina virtual disponíveis para uma subscrição](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="9edb9-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="9edb9-117">`osPlatform`tem de ser especificado e pode ser **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="9edb9-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="9edb9-118">Utilizou os custos de hardware de Olá toodetermine das máquinas de virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="9edb9-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="9edb9-119">`imageReference`for omitido para imagens originais, mas fornecido para imagens de terceiros.</span><span class="sxs-lookup"><span data-stu-id="9edb9-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="9edb9-120">Utilizou o custos de software Olá toodetermine das máquinas de virtuais Olá.</span><span class="sxs-lookup"><span data-stu-id="9edb9-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="9edb9-121">`count`é utilizado tooset Olá multiplicador adequado para o elemento de Olá.</span><span class="sxs-lookup"><span data-stu-id="9edb9-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="9edb9-122">Suporta um valor estático, tal como **2**, ou como um valor dinâmico de outro elemento, `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="9edb9-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="9edb9-123">valor predefinido de Olá é **1**.</span><span class="sxs-lookup"><span data-stu-id="9edb9-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="9edb9-124">Resultado da amostra</span><span class="sxs-lookup"><span data-stu-id="9edb9-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="9edb9-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9edb9-125">Next steps</span></span>
* <span data-ttu-id="9edb9-126">Para aplicações de toomanaged uma introdução, consulte [descrição geral do Azure gerida aplicações](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9edb9-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9edb9-127">Para definições de IU toocreating uma introdução, consulte [introdução CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9edb9-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9edb9-128">Para obter uma descrição de propriedades comuns de elementos de IU, consulte [CreateUiDefinition elementos](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="9edb9-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
