---
title: "aaaAzure Resource Manager funções de modelo - lógicas | Microsoft Docs"
description: "Descreve as funções de Olá toouse um valores de lógica de toodetermine de modelo Azure Resource Manager."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="64ed5-103">Funções de lógicas de modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64ed5-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="64ed5-104">O Resource Manager fornece várias funções, para efetuar comparações nos seus modelos.</span><span class="sxs-lookup"><span data-stu-id="64ed5-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="64ed5-105">e</span><span class="sxs-lookup"><span data-stu-id="64ed5-105">and</span></span>](#and)
* [<span data-ttu-id="64ed5-106">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-106">bool</span></span>](#bool)
* [<span data-ttu-id="64ed5-107">Se</span><span class="sxs-lookup"><span data-stu-id="64ed5-107">if</span></span>](#if)
* [<span data-ttu-id="64ed5-108">não</span><span class="sxs-lookup"><span data-stu-id="64ed5-108">not</span></span>](#not)
* [<span data-ttu-id="64ed5-109">ou</span><span class="sxs-lookup"><span data-stu-id="64ed5-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="64ed5-110">e</span><span class="sxs-lookup"><span data-stu-id="64ed5-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="64ed5-111">Verifica se ambos os valores de parâmetro forem verdadeiros.</span><span class="sxs-lookup"><span data-stu-id="64ed5-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="64ed5-112">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="64ed5-112">Parameters</span></span>

| <span data-ttu-id="64ed5-113">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="64ed5-113">Parameter</span></span> | <span data-ttu-id="64ed5-114">Necessário</span><span class="sxs-lookup"><span data-stu-id="64ed5-114">Required</span></span> | <span data-ttu-id="64ed5-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-115">Type</span></span> | <span data-ttu-id="64ed5-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="64ed5-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64ed5-117">arg1</span><span class="sxs-lookup"><span data-stu-id="64ed5-117">arg1</span></span> |<span data-ttu-id="64ed5-118">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-118">Yes</span></span> |<span data-ttu-id="64ed5-119">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="64ed5-119">boolean</span></span> |<span data-ttu-id="64ed5-120">Olá toocheck do primeiro valor se for VERDADEIRO.</span><span class="sxs-lookup"><span data-stu-id="64ed5-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="64ed5-121">arg2</span><span class="sxs-lookup"><span data-stu-id="64ed5-121">arg2</span></span> |<span data-ttu-id="64ed5-122">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-122">Yes</span></span> |<span data-ttu-id="64ed5-123">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="64ed5-123">boolean</span></span> |<span data-ttu-id="64ed5-124">Olá toocheck do segundo valor se for VERDADEIRO.</span><span class="sxs-lookup"><span data-stu-id="64ed5-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64ed5-125">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="64ed5-125">Return value</span></span>

<span data-ttu-id="64ed5-126">Devolve **verdadeiro** se ambos os valores forem true; caso contrário, **falso**.</span><span class="sxs-lookup"><span data-stu-id="64ed5-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="64ed5-127">Exemplos</span><span class="sxs-lookup"><span data-stu-id="64ed5-127">Examples</span></span>

<span data-ttu-id="64ed5-128">Olá seguinte exemplo mostra como as funções de lógica de toouse.</span><span class="sxs-lookup"><span data-stu-id="64ed5-128">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="64ed5-129">saída de Olá de Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="64ed5-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="64ed5-130">Nome</span><span class="sxs-lookup"><span data-stu-id="64ed5-130">Name</span></span> | <span data-ttu-id="64ed5-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-131">Type</span></span> | <span data-ttu-id="64ed5-132">Valor</span><span class="sxs-lookup"><span data-stu-id="64ed5-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64ed5-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-133">andExampleOutput</span></span> | <span data-ttu-id="64ed5-134">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-134">Bool</span></span> | <span data-ttu-id="64ed5-135">Falso</span><span class="sxs-lookup"><span data-stu-id="64ed5-135">False</span></span> |
| <span data-ttu-id="64ed5-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-136">orExampleOutput</span></span> | <span data-ttu-id="64ed5-137">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-137">Bool</span></span> | <span data-ttu-id="64ed5-138">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="64ed5-138">True</span></span> |
| <span data-ttu-id="64ed5-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-139">notExampleOutput</span></span> | <span data-ttu-id="64ed5-140">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-140">Bool</span></span> | <span data-ttu-id="64ed5-141">Falso</span><span class="sxs-lookup"><span data-stu-id="64ed5-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="64ed5-142">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="64ed5-143">Converte Olá tooa parâmetro booleano.</span><span class="sxs-lookup"><span data-stu-id="64ed5-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="64ed5-144">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="64ed5-144">Parameters</span></span>

| <span data-ttu-id="64ed5-145">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="64ed5-145">Parameter</span></span> | <span data-ttu-id="64ed5-146">Necessário</span><span class="sxs-lookup"><span data-stu-id="64ed5-146">Required</span></span> | <span data-ttu-id="64ed5-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-147">Type</span></span> | <span data-ttu-id="64ed5-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="64ed5-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64ed5-149">arg1</span><span class="sxs-lookup"><span data-stu-id="64ed5-149">arg1</span></span> |<span data-ttu-id="64ed5-150">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-150">Yes</span></span> |<span data-ttu-id="64ed5-151">cadeia ou int</span><span class="sxs-lookup"><span data-stu-id="64ed5-151">string or int</span></span> |<span data-ttu-id="64ed5-152">Olá tooa tooconvert de valor booleano.</span><span class="sxs-lookup"><span data-stu-id="64ed5-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64ed5-153">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="64ed5-153">Return value</span></span>
<span data-ttu-id="64ed5-154">Um booleano de Olá converter o valor.</span><span class="sxs-lookup"><span data-stu-id="64ed5-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="64ed5-155">Exemplos</span><span class="sxs-lookup"><span data-stu-id="64ed5-155">Examples</span></span>

<span data-ttu-id="64ed5-156">Olá seguinte exemplo mostra como toouse bool com uma cadeia ou um número inteiro.</span><span class="sxs-lookup"><span data-stu-id="64ed5-156">hello following example shows how toouse bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="64ed5-157">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="64ed5-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="64ed5-158">Nome</span><span class="sxs-lookup"><span data-stu-id="64ed5-158">Name</span></span> | <span data-ttu-id="64ed5-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-159">Type</span></span> | <span data-ttu-id="64ed5-160">Valor</span><span class="sxs-lookup"><span data-stu-id="64ed5-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64ed5-161">trueString</span><span class="sxs-lookup"><span data-stu-id="64ed5-161">trueString</span></span> | <span data-ttu-id="64ed5-162">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-162">Bool</span></span> | <span data-ttu-id="64ed5-163">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="64ed5-163">True</span></span> |
| <span data-ttu-id="64ed5-164">falseString</span><span class="sxs-lookup"><span data-stu-id="64ed5-164">falseString</span></span> | <span data-ttu-id="64ed5-165">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-165">Bool</span></span> | <span data-ttu-id="64ed5-166">Falso</span><span class="sxs-lookup"><span data-stu-id="64ed5-166">False</span></span> |
| <span data-ttu-id="64ed5-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="64ed5-167">trueInt</span></span> | <span data-ttu-id="64ed5-168">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-168">Bool</span></span> | <span data-ttu-id="64ed5-169">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="64ed5-169">True</span></span> |
| <span data-ttu-id="64ed5-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="64ed5-170">falseInt</span></span> | <span data-ttu-id="64ed5-171">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-171">Bool</span></span> | <span data-ttu-id="64ed5-172">Falso</span><span class="sxs-lookup"><span data-stu-id="64ed5-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="64ed5-173">Se</span><span class="sxs-lookup"><span data-stu-id="64ed5-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="64ed5-174">Devolve um valor com base nas permissões de uma condição for true ou false.</span><span class="sxs-lookup"><span data-stu-id="64ed5-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="64ed5-175">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="64ed5-175">Parameters</span></span>

| <span data-ttu-id="64ed5-176">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="64ed5-176">Parameter</span></span> | <span data-ttu-id="64ed5-177">Necessário</span><span class="sxs-lookup"><span data-stu-id="64ed5-177">Required</span></span> | <span data-ttu-id="64ed5-178">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-178">Type</span></span> | <span data-ttu-id="64ed5-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="64ed5-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64ed5-180">Condição</span><span class="sxs-lookup"><span data-stu-id="64ed5-180">condition</span></span> |<span data-ttu-id="64ed5-181">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-181">Yes</span></span> |<span data-ttu-id="64ed5-182">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="64ed5-182">boolean</span></span> |<span data-ttu-id="64ed5-183">Olá toocheck valor se for VERDADEIRO.</span><span class="sxs-lookup"><span data-stu-id="64ed5-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="64ed5-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="64ed5-184">trueValue</span></span> |<span data-ttu-id="64ed5-185">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-185">Yes</span></span> | <span data-ttu-id="64ed5-186">cadeia, int, objetos ou matriz</span><span class="sxs-lookup"><span data-stu-id="64ed5-186">string, int, object, or array</span></span> |<span data-ttu-id="64ed5-187">Olá valor tooreturn quando a condição de Olá é verdadeira.</span><span class="sxs-lookup"><span data-stu-id="64ed5-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="64ed5-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="64ed5-188">falseValue</span></span> |<span data-ttu-id="64ed5-189">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-189">Yes</span></span> | <span data-ttu-id="64ed5-190">cadeia, int, objetos ou matriz</span><span class="sxs-lookup"><span data-stu-id="64ed5-190">string, int, object, or array</span></span> |<span data-ttu-id="64ed5-191">Olá valor tooreturn quando a condição de Olá é falsa.</span><span class="sxs-lookup"><span data-stu-id="64ed5-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64ed5-192">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="64ed5-192">Return value</span></span>

<span data-ttu-id="64ed5-193">Devolve o segundo parâmetro quando o primeiro parâmetro é **verdadeiro**; caso contrário, devolve o terceiro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="64ed5-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="64ed5-194">Observações</span><span class="sxs-lookup"><span data-stu-id="64ed5-194">Remarks</span></span>

<span data-ttu-id="64ed5-195">Pode utilizar este conjunto de tooconditionally função uma propriedade de recurso.</span><span class="sxs-lookup"><span data-stu-id="64ed5-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="64ed5-196">Olá exemplo seguinte não é um modelo completo, mas mostra as partes relevantes de Olá para definir o conjunto de disponibilidade de Olá condicionalmente.</span><span class="sxs-lookup"><span data-stu-id="64ed5-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="64ed5-197">Exemplos</span><span class="sxs-lookup"><span data-stu-id="64ed5-197">Examples</span></span>

<span data-ttu-id="64ed5-198">Olá seguinte exemplo mostra como toouse Olá `if` função.</span><span class="sxs-lookup"><span data-stu-id="64ed5-198">hello following example shows how toouse hello `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="64ed5-199">saída de Olá de Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="64ed5-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="64ed5-200">Nome</span><span class="sxs-lookup"><span data-stu-id="64ed5-200">Name</span></span> | <span data-ttu-id="64ed5-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-201">Type</span></span> | <span data-ttu-id="64ed5-202">Valor</span><span class="sxs-lookup"><span data-stu-id="64ed5-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64ed5-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-203">yesOutput</span></span> | <span data-ttu-id="64ed5-204">Cadeia</span><span class="sxs-lookup"><span data-stu-id="64ed5-204">String</span></span> | <span data-ttu-id="64ed5-205">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-205">yes</span></span> |
| <span data-ttu-id="64ed5-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-206">noOutput</span></span> | <span data-ttu-id="64ed5-207">Cadeia</span><span class="sxs-lookup"><span data-stu-id="64ed5-207">String</span></span> | <span data-ttu-id="64ed5-208">Não</span><span class="sxs-lookup"><span data-stu-id="64ed5-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="64ed5-209">não</span><span class="sxs-lookup"><span data-stu-id="64ed5-209">not</span></span>
`not(arg1)`

<span data-ttu-id="64ed5-210">Converte o valor booleano tooits opposite valor.</span><span class="sxs-lookup"><span data-stu-id="64ed5-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="64ed5-211">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="64ed5-211">Parameters</span></span>

| <span data-ttu-id="64ed5-212">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="64ed5-212">Parameter</span></span> | <span data-ttu-id="64ed5-213">Necessário</span><span class="sxs-lookup"><span data-stu-id="64ed5-213">Required</span></span> | <span data-ttu-id="64ed5-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-214">Type</span></span> | <span data-ttu-id="64ed5-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="64ed5-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64ed5-216">arg1</span><span class="sxs-lookup"><span data-stu-id="64ed5-216">arg1</span></span> |<span data-ttu-id="64ed5-217">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-217">Yes</span></span> |<span data-ttu-id="64ed5-218">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="64ed5-218">boolean</span></span> |<span data-ttu-id="64ed5-219">Olá tooconvert de valor.</span><span class="sxs-lookup"><span data-stu-id="64ed5-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="64ed5-220">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="64ed5-220">Return value</span></span>

<span data-ttu-id="64ed5-221">Devolve **verdadeiro** quando o parâmetro é **falso**.</span><span class="sxs-lookup"><span data-stu-id="64ed5-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="64ed5-222">Devolve **falso** quando o parâmetro é **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="64ed5-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="64ed5-223">Exemplos</span><span class="sxs-lookup"><span data-stu-id="64ed5-223">Examples</span></span>

<span data-ttu-id="64ed5-224">Olá seguinte exemplo mostra como as funções de lógica de toouse.</span><span class="sxs-lookup"><span data-stu-id="64ed5-224">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="64ed5-225">saída de Olá de Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="64ed5-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="64ed5-226">Nome</span><span class="sxs-lookup"><span data-stu-id="64ed5-226">Name</span></span> | <span data-ttu-id="64ed5-227">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-227">Type</span></span> | <span data-ttu-id="64ed5-228">Valor</span><span class="sxs-lookup"><span data-stu-id="64ed5-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64ed5-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-229">andExampleOutput</span></span> | <span data-ttu-id="64ed5-230">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-230">Bool</span></span> | <span data-ttu-id="64ed5-231">Falso</span><span class="sxs-lookup"><span data-stu-id="64ed5-231">False</span></span> |
| <span data-ttu-id="64ed5-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-232">orExampleOutput</span></span> | <span data-ttu-id="64ed5-233">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-233">Bool</span></span> | <span data-ttu-id="64ed5-234">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="64ed5-234">True</span></span> |
| <span data-ttu-id="64ed5-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-235">notExampleOutput</span></span> | <span data-ttu-id="64ed5-236">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-236">Bool</span></span> | <span data-ttu-id="64ed5-237">Falso</span><span class="sxs-lookup"><span data-stu-id="64ed5-237">False</span></span> |

<span data-ttu-id="64ed5-238">Olá exemplo seguinte utiliza **não** com [é igual a](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="64ed5-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="64ed5-239">saída de Olá de Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="64ed5-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="64ed5-240">Nome</span><span class="sxs-lookup"><span data-stu-id="64ed5-240">Name</span></span> | <span data-ttu-id="64ed5-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-241">Type</span></span> | <span data-ttu-id="64ed5-242">Valor</span><span class="sxs-lookup"><span data-stu-id="64ed5-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64ed5-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="64ed5-243">checkNotEquals</span></span> | <span data-ttu-id="64ed5-244">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-244">Bool</span></span> | <span data-ttu-id="64ed5-245">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="64ed5-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="64ed5-246">ou</span><span class="sxs-lookup"><span data-stu-id="64ed5-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="64ed5-247">Verifica se o valor do parâmetro é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="64ed5-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="64ed5-248">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="64ed5-248">Parameters</span></span>

| <span data-ttu-id="64ed5-249">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="64ed5-249">Parameter</span></span> | <span data-ttu-id="64ed5-250">Necessário</span><span class="sxs-lookup"><span data-stu-id="64ed5-250">Required</span></span> | <span data-ttu-id="64ed5-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-251">Type</span></span> | <span data-ttu-id="64ed5-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="64ed5-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="64ed5-253">arg1</span><span class="sxs-lookup"><span data-stu-id="64ed5-253">arg1</span></span> |<span data-ttu-id="64ed5-254">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-254">Yes</span></span> |<span data-ttu-id="64ed5-255">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="64ed5-255">boolean</span></span> |<span data-ttu-id="64ed5-256">Olá toocheck do primeiro valor se for VERDADEIRO.</span><span class="sxs-lookup"><span data-stu-id="64ed5-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="64ed5-257">arg2</span><span class="sxs-lookup"><span data-stu-id="64ed5-257">arg2</span></span> |<span data-ttu-id="64ed5-258">Sim</span><span class="sxs-lookup"><span data-stu-id="64ed5-258">Yes</span></span> |<span data-ttu-id="64ed5-259">Valor booleano</span><span class="sxs-lookup"><span data-stu-id="64ed5-259">boolean</span></span> |<span data-ttu-id="64ed5-260">Olá toocheck do segundo valor se for VERDADEIRO.</span><span class="sxs-lookup"><span data-stu-id="64ed5-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="64ed5-261">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="64ed5-261">Return value</span></span>

<span data-ttu-id="64ed5-262">Devolve **verdadeiro** se o valor for true; caso contrário, **falso**.</span><span class="sxs-lookup"><span data-stu-id="64ed5-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="64ed5-263">Exemplos</span><span class="sxs-lookup"><span data-stu-id="64ed5-263">Examples</span></span>

<span data-ttu-id="64ed5-264">Olá seguinte exemplo mostra como as funções de lógica de toouse.</span><span class="sxs-lookup"><span data-stu-id="64ed5-264">hello following example shows how toouse logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="64ed5-265">saída de Olá de Olá anterior exemplo é:</span><span class="sxs-lookup"><span data-stu-id="64ed5-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="64ed5-266">Nome</span><span class="sxs-lookup"><span data-stu-id="64ed5-266">Name</span></span> | <span data-ttu-id="64ed5-267">Tipo</span><span class="sxs-lookup"><span data-stu-id="64ed5-267">Type</span></span> | <span data-ttu-id="64ed5-268">Valor</span><span class="sxs-lookup"><span data-stu-id="64ed5-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="64ed5-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-269">andExampleOutput</span></span> | <span data-ttu-id="64ed5-270">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-270">Bool</span></span> | <span data-ttu-id="64ed5-271">Falso</span><span class="sxs-lookup"><span data-stu-id="64ed5-271">False</span></span> |
| <span data-ttu-id="64ed5-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-272">orExampleOutput</span></span> | <span data-ttu-id="64ed5-273">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-273">Bool</span></span> | <span data-ttu-id="64ed5-274">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="64ed5-274">True</span></span> |
| <span data-ttu-id="64ed5-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="64ed5-275">notExampleOutput</span></span> | <span data-ttu-id="64ed5-276">bool</span><span class="sxs-lookup"><span data-stu-id="64ed5-276">Bool</span></span> | <span data-ttu-id="64ed5-277">Falso</span><span class="sxs-lookup"><span data-stu-id="64ed5-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="64ed5-278">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="64ed5-278">Next steps</span></span>
* <span data-ttu-id="64ed5-279">Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="64ed5-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="64ed5-280">toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="64ed5-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="64ed5-281">tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="64ed5-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="64ed5-282">toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="64ed5-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

