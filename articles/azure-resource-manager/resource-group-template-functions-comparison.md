---
title: "funções de modelo do Resource Manager aaaAzure - comparação | Microsoft Docs"
description: "Descreve as funções de Olá toouse um valores de toocompare de modelo do Azure Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="6fd6c-103">Funções de comparação para modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6fd6c-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="6fd6c-104">O Resource Manager fornece várias funções, para efetuar comparações nos seus modelos.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="6fd6c-105">igual a</span><span class="sxs-lookup"><span data-stu-id="6fd6c-105">equals</span></span>](#equals)
* [<span data-ttu-id="6fd6c-106">maior</span><span class="sxs-lookup"><span data-stu-id="6fd6c-106">greater</span></span>](#greater)
* [<span data-ttu-id="6fd6c-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="6fd6c-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="6fd6c-108">menor</span><span class="sxs-lookup"><span data-stu-id="6fd6c-108">less</span></span>](#less)
* [<span data-ttu-id="6fd6c-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="6fd6c-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="6fd6c-110">igual a</span><span class="sxs-lookup"><span data-stu-id="6fd6c-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="6fd6c-111">Verifica se os dois valores igual entre si.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="6fd6c-112">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fd6c-112">Parameters</span></span>

| <span data-ttu-id="6fd6c-113">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-113">Parameter</span></span> | <span data-ttu-id="6fd6c-114">Necessário</span><span class="sxs-lookup"><span data-stu-id="6fd6c-114">Required</span></span> | <span data-ttu-id="6fd6c-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-115">Type</span></span> | <span data-ttu-id="6fd6c-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fd6c-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6fd6c-117">arg1</span><span class="sxs-lookup"><span data-stu-id="6fd6c-117">arg1</span></span> |<span data-ttu-id="6fd6c-118">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-118">Yes</span></span> |<span data-ttu-id="6fd6c-119">int, string, matriz ou objeto</span><span class="sxs-lookup"><span data-stu-id="6fd6c-119">int, string, array, or object</span></span> |<span data-ttu-id="6fd6c-120">Olá primeiro valor toocheck para igualdade.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="6fd6c-121">arg2</span><span class="sxs-lookup"><span data-stu-id="6fd6c-121">arg2</span></span> |<span data-ttu-id="6fd6c-122">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-122">Yes</span></span> |<span data-ttu-id="6fd6c-123">int, string, matriz ou objeto</span><span class="sxs-lookup"><span data-stu-id="6fd6c-123">int, string, array, or object</span></span> |<span data-ttu-id="6fd6c-124">Olá segundo valor toocheck para igualdade.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6fd6c-125">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="6fd6c-125">Return value</span></span>

<span data-ttu-id="6fd6c-126">Devolve **verdadeiro** se os valores de Olá forem igual; caso contrário, **falso**.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="6fd6c-127">Observações</span><span class="sxs-lookup"><span data-stu-id="6fd6c-127">Remarks</span></span>

<span data-ttu-id="6fd6c-128">Olá é igual a função é frequentemente usada com Olá `condition` elemento tootest se um recurso é implementado.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a><span data-ttu-id="6fd6c-129">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-129">Example</span></span>

<span data-ttu-id="6fd6c-130">modelo de exemplo de Olá verifica diferentes tipos de valores para igualdade.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="6fd6c-131">Todos os valores predefinidos de Olá devolvem True.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-131">All hello default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="6fd6c-132">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="6fd6c-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6fd6c-133">Nome</span><span class="sxs-lookup"><span data-stu-id="6fd6c-133">Name</span></span> | <span data-ttu-id="6fd6c-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-134">Type</span></span> | <span data-ttu-id="6fd6c-135">Valor</span><span class="sxs-lookup"><span data-stu-id="6fd6c-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6fd6c-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="6fd6c-136">checkInts</span></span> | <span data-ttu-id="6fd6c-137">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-137">Bool</span></span> | <span data-ttu-id="6fd6c-138">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-138">True</span></span> |
| <span data-ttu-id="6fd6c-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="6fd6c-139">checkStrings</span></span> | <span data-ttu-id="6fd6c-140">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-140">Bool</span></span> | <span data-ttu-id="6fd6c-141">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-141">True</span></span> |
| <span data-ttu-id="6fd6c-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="6fd6c-142">checkArrays</span></span> | <span data-ttu-id="6fd6c-143">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-143">Bool</span></span> | <span data-ttu-id="6fd6c-144">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-144">True</span></span> |
| <span data-ttu-id="6fd6c-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="6fd6c-145">checkObjects</span></span> | <span data-ttu-id="6fd6c-146">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-146">Bool</span></span> | <span data-ttu-id="6fd6c-147">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-147">True</span></span> |


<span data-ttu-id="6fd6c-148">Olá exemplo seguinte utiliza [não](resource-group-template-functions-logical.md#not) com **é igual a**.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="6fd6c-149">saída de Olá de Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="6fd6c-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="6fd6c-150">Nome</span><span class="sxs-lookup"><span data-stu-id="6fd6c-150">Name</span></span> | <span data-ttu-id="6fd6c-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-151">Type</span></span> | <span data-ttu-id="6fd6c-152">Valor</span><span class="sxs-lookup"><span data-stu-id="6fd6c-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6fd6c-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="6fd6c-153">checkNotEquals</span></span> | <span data-ttu-id="6fd6c-154">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-154">Bool</span></span> | <span data-ttu-id="6fd6c-155">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="6fd6c-156">maior</span><span class="sxs-lookup"><span data-stu-id="6fd6c-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="6fd6c-157">Verifica se o primeiro valor Olá é superior ao valor segundo Olá.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="6fd6c-158">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fd6c-158">Parameters</span></span>

| <span data-ttu-id="6fd6c-159">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-159">Parameter</span></span> | <span data-ttu-id="6fd6c-160">Necessário</span><span class="sxs-lookup"><span data-stu-id="6fd6c-160">Required</span></span> | <span data-ttu-id="6fd6c-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-161">Type</span></span> | <span data-ttu-id="6fd6c-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fd6c-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6fd6c-163">arg1</span><span class="sxs-lookup"><span data-stu-id="6fd6c-163">arg1</span></span> |<span data-ttu-id="6fd6c-164">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-164">Yes</span></span> |<span data-ttu-id="6fd6c-165">int ou cadeia</span><span class="sxs-lookup"><span data-stu-id="6fd6c-165">int or string</span></span> |<span data-ttu-id="6fd6c-166">Olá primeiro valor de comparação de maior Olá.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="6fd6c-167">arg2</span><span class="sxs-lookup"><span data-stu-id="6fd6c-167">arg2</span></span> |<span data-ttu-id="6fd6c-168">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-168">Yes</span></span> |<span data-ttu-id="6fd6c-169">int ou cadeia</span><span class="sxs-lookup"><span data-stu-id="6fd6c-169">int or string</span></span> |<span data-ttu-id="6fd6c-170">Olá segundo valor de comparação de maior Olá.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6fd6c-171">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="6fd6c-171">Return value</span></span>

<span data-ttu-id="6fd6c-172">Devolve **verdadeiro** se Olá o primeiro valor é superior ao valor segundo Olá; caso contrário, **falso**.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="6fd6c-173">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-173">Example</span></span>

<span data-ttu-id="6fd6c-174">modelo de exemplo de Olá verifica se um valor de Olá é superior a Olá outro.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-174">hello example template checks whether hello one value is greater than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="6fd6c-175">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="6fd6c-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6fd6c-176">Nome</span><span class="sxs-lookup"><span data-stu-id="6fd6c-176">Name</span></span> | <span data-ttu-id="6fd6c-177">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-177">Type</span></span> | <span data-ttu-id="6fd6c-178">Valor</span><span class="sxs-lookup"><span data-stu-id="6fd6c-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6fd6c-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="6fd6c-179">checkInts</span></span> | <span data-ttu-id="6fd6c-180">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-180">Bool</span></span> | <span data-ttu-id="6fd6c-181">Falso</span><span class="sxs-lookup"><span data-stu-id="6fd6c-181">False</span></span> |
| <span data-ttu-id="6fd6c-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="6fd6c-182">checkStrings</span></span> | <span data-ttu-id="6fd6c-183">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-183">Bool</span></span> | <span data-ttu-id="6fd6c-184">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="6fd6c-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="6fd6c-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="6fd6c-186">Verifica se o primeiro valor Olá toohello igual ou maior do que o segundo valor.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="6fd6c-187">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fd6c-187">Parameters</span></span>

| <span data-ttu-id="6fd6c-188">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-188">Parameter</span></span> | <span data-ttu-id="6fd6c-189">Necessário</span><span class="sxs-lookup"><span data-stu-id="6fd6c-189">Required</span></span> | <span data-ttu-id="6fd6c-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-190">Type</span></span> | <span data-ttu-id="6fd6c-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fd6c-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6fd6c-192">arg1</span><span class="sxs-lookup"><span data-stu-id="6fd6c-192">arg1</span></span> |<span data-ttu-id="6fd6c-193">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-193">Yes</span></span> |<span data-ttu-id="6fd6c-194">int ou cadeia</span><span class="sxs-lookup"><span data-stu-id="6fd6c-194">int or string</span></span> |<span data-ttu-id="6fd6c-195">Olá primeiro valor de comparação de Olá igual ou maior.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="6fd6c-196">arg2</span><span class="sxs-lookup"><span data-stu-id="6fd6c-196">arg2</span></span> |<span data-ttu-id="6fd6c-197">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-197">Yes</span></span> |<span data-ttu-id="6fd6c-198">int ou cadeia</span><span class="sxs-lookup"><span data-stu-id="6fd6c-198">int or string</span></span> |<span data-ttu-id="6fd6c-199">Olá segundo valor de comparação de Olá igual ou maior.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6fd6c-200">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="6fd6c-200">Return value</span></span>

<span data-ttu-id="6fd6c-201">Devolve **verdadeiro** se Olá primeiro valor for igual ou maior do que toohello segundo; caso contrário, **falso**.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="6fd6c-202">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-202">Example</span></span>

<span data-ttu-id="6fd6c-203">modelo de exemplo de Olá verifica se um valor de Olá é maior que ou igual toohello outro.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="6fd6c-204">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="6fd6c-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6fd6c-205">Nome</span><span class="sxs-lookup"><span data-stu-id="6fd6c-205">Name</span></span> | <span data-ttu-id="6fd6c-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-206">Type</span></span> | <span data-ttu-id="6fd6c-207">Valor</span><span class="sxs-lookup"><span data-stu-id="6fd6c-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6fd6c-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="6fd6c-208">checkInts</span></span> | <span data-ttu-id="6fd6c-209">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-209">Bool</span></span> | <span data-ttu-id="6fd6c-210">Falso</span><span class="sxs-lookup"><span data-stu-id="6fd6c-210">False</span></span> |
| <span data-ttu-id="6fd6c-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="6fd6c-211">checkStrings</span></span> | <span data-ttu-id="6fd6c-212">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-212">Bool</span></span> | <span data-ttu-id="6fd6c-213">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="6fd6c-214">menor</span><span class="sxs-lookup"><span data-stu-id="6fd6c-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="6fd6c-215">Verifica se o primeiro valor Olá é menor que Olá segundo valor.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="6fd6c-216">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fd6c-216">Parameters</span></span>

| <span data-ttu-id="6fd6c-217">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-217">Parameter</span></span> | <span data-ttu-id="6fd6c-218">Necessário</span><span class="sxs-lookup"><span data-stu-id="6fd6c-218">Required</span></span> | <span data-ttu-id="6fd6c-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-219">Type</span></span> | <span data-ttu-id="6fd6c-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fd6c-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6fd6c-221">arg1</span><span class="sxs-lookup"><span data-stu-id="6fd6c-221">arg1</span></span> |<span data-ttu-id="6fd6c-222">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-222">Yes</span></span> |<span data-ttu-id="6fd6c-223">int ou cadeia</span><span class="sxs-lookup"><span data-stu-id="6fd6c-223">int or string</span></span> |<span data-ttu-id="6fd6c-224">Olá primeiro valor de Olá menos comparação.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="6fd6c-225">arg2</span><span class="sxs-lookup"><span data-stu-id="6fd6c-225">arg2</span></span> |<span data-ttu-id="6fd6c-226">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-226">Yes</span></span> |<span data-ttu-id="6fd6c-227">int ou cadeia</span><span class="sxs-lookup"><span data-stu-id="6fd6c-227">int or string</span></span> |<span data-ttu-id="6fd6c-228">Olá segundo valor para Olá menos comparação.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6fd6c-229">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="6fd6c-229">Return value</span></span>

<span data-ttu-id="6fd6c-230">Devolve **verdadeiro** segundo valor se o primeiro valor Olá for inferior a Olá; caso contrário, **falso**.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="6fd6c-231">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-231">Example</span></span>

<span data-ttu-id="6fd6c-232">modelo de exemplo de Olá verifica se um valor de Olá inferior Olá outro.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-232">hello example template checks whether hello one value is less than hello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="6fd6c-233">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="6fd6c-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6fd6c-234">Nome</span><span class="sxs-lookup"><span data-stu-id="6fd6c-234">Name</span></span> | <span data-ttu-id="6fd6c-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-235">Type</span></span> | <span data-ttu-id="6fd6c-236">Valor</span><span class="sxs-lookup"><span data-stu-id="6fd6c-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6fd6c-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="6fd6c-237">checkInts</span></span> | <span data-ttu-id="6fd6c-238">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-238">Bool</span></span> | <span data-ttu-id="6fd6c-239">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-239">True</span></span> |
| <span data-ttu-id="6fd6c-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="6fd6c-240">checkStrings</span></span> | <span data-ttu-id="6fd6c-241">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-241">Bool</span></span> | <span data-ttu-id="6fd6c-242">Falso</span><span class="sxs-lookup"><span data-stu-id="6fd6c-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="6fd6c-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="6fd6c-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="6fd6c-244">Verifica se o primeiro valor Olá é menor ou igual toohello segundo valor.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="6fd6c-245">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fd6c-245">Parameters</span></span>

| <span data-ttu-id="6fd6c-246">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-246">Parameter</span></span> | <span data-ttu-id="6fd6c-247">Necessário</span><span class="sxs-lookup"><span data-stu-id="6fd6c-247">Required</span></span> | <span data-ttu-id="6fd6c-248">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-248">Type</span></span> | <span data-ttu-id="6fd6c-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="6fd6c-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6fd6c-250">arg1</span><span class="sxs-lookup"><span data-stu-id="6fd6c-250">arg1</span></span> |<span data-ttu-id="6fd6c-251">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-251">Yes</span></span> |<span data-ttu-id="6fd6c-252">int ou cadeia</span><span class="sxs-lookup"><span data-stu-id="6fd6c-252">int or string</span></span> |<span data-ttu-id="6fd6c-253">Olá primeiro valor de Olá inferior ou igual a comparação.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="6fd6c-254">arg2</span><span class="sxs-lookup"><span data-stu-id="6fd6c-254">arg2</span></span> |<span data-ttu-id="6fd6c-255">Sim</span><span class="sxs-lookup"><span data-stu-id="6fd6c-255">Yes</span></span> |<span data-ttu-id="6fd6c-256">int ou cadeia</span><span class="sxs-lookup"><span data-stu-id="6fd6c-256">int or string</span></span> |<span data-ttu-id="6fd6c-257">Olá segundo valor para Olá inferior ou igual a comparação.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6fd6c-258">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="6fd6c-258">Return value</span></span>

<span data-ttu-id="6fd6c-259">Devolve **verdadeiro** se o primeiro valor Olá é menor ou igual toohello segundo valor; caso contrário, **falso**.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="6fd6c-260">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-260">Example</span></span>

<span data-ttu-id="6fd6c-261">Olá modelo de exemplo verifica se Olá um valor é menor ou igual toohello outro.</span><span class="sxs-lookup"><span data-stu-id="6fd6c-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="6fd6c-262">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="6fd6c-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6fd6c-263">Nome</span><span class="sxs-lookup"><span data-stu-id="6fd6c-263">Name</span></span> | <span data-ttu-id="6fd6c-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="6fd6c-264">Type</span></span> | <span data-ttu-id="6fd6c-265">Valor</span><span class="sxs-lookup"><span data-stu-id="6fd6c-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6fd6c-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="6fd6c-266">checkInts</span></span> | <span data-ttu-id="6fd6c-267">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-267">Bool</span></span> | <span data-ttu-id="6fd6c-268">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6fd6c-268">True</span></span> |
| <span data-ttu-id="6fd6c-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="6fd6c-269">checkStrings</span></span> | <span data-ttu-id="6fd6c-270">bool</span><span class="sxs-lookup"><span data-stu-id="6fd6c-270">Bool</span></span> | <span data-ttu-id="6fd6c-271">Falso</span><span class="sxs-lookup"><span data-stu-id="6fd6c-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="6fd6c-272">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6fd6c-272">Next steps</span></span>
* <span data-ttu-id="6fd6c-273">Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6fd6c-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="6fd6c-274">toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6fd6c-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="6fd6c-275">tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6fd6c-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="6fd6c-276">toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6fd6c-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

