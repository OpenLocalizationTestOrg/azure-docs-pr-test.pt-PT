---
title: "aaaResource Gestor de funções de modelo | Microsoft Docs"
description: "Descreve Olá funções toouse um valores de tooretrieve de modelo do Azure Resource Manager, trabalhar com cadeias e números e obter informações de implementação."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="696fe-103">Funções de modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="696fe-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="696fe-104">Este tópico descreve todos os Olá funções que pode utilizar num modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="696fe-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="696fe-105">Adicione funções nos seus modelos por envolvente-los entre parênteses Retos: `[` e `]`, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="696fe-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="696fe-106">expressão de Olá é avaliada durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="696fe-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="696fe-107">Enquanto escritos como uma cadeia literal, resultado de Olá da avaliação de Olá expressão pode ser um tipo JSON diferente, tal como uma matriz, um objeto nem um número inteiro.</span><span class="sxs-lookup"><span data-stu-id="696fe-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="696fe-108">Apenas como em JavaScript, chamadas de função estejam formatadas como `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="696fe-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="696fe-109">Referenciar propriedades utilizando operadores de ponto e [Índice] Olá.</span><span class="sxs-lookup"><span data-stu-id="696fe-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="696fe-110">Uma expressão de modelo não pode exceder 24,576 carateres.</span><span class="sxs-lookup"><span data-stu-id="696fe-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="696fe-111">Funções de modelo e os respetivos parâmetros são sensível.</span><span class="sxs-lookup"><span data-stu-id="696fe-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="696fe-112">Por exemplo, o Gestor de recursos é resolvido **variables('var1')** e **VARIABLES('VAR1')** como Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="696fe-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="696fe-113">Quando avaliada, a menos que a função de Olá expressamente modifica caso (como toUpper ou toLower), a função Olá preserva caso Olá.</span><span class="sxs-lookup"><span data-stu-id="696fe-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="696fe-114">Determinados tipos de recurso podem ter requisitos de cenários independentemente da forma como são avaliadas as funções.</span><span class="sxs-lookup"><span data-stu-id="696fe-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="696fe-115">Funções de matriz e o objeto</span><span class="sxs-lookup"><span data-stu-id="696fe-115">Array and object functions</span></span>
<span data-ttu-id="696fe-116">O Resource Manager fornece várias funções para trabalhar com objetos e matrizes.</span><span class="sxs-lookup"><span data-stu-id="696fe-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="696fe-117">matriz</span><span class="sxs-lookup"><span data-stu-id="696fe-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="696fe-118">Unir</span><span class="sxs-lookup"><span data-stu-id="696fe-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="696fe-119">concat</span><span class="sxs-lookup"><span data-stu-id="696fe-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="696fe-120">contém</span><span class="sxs-lookup"><span data-stu-id="696fe-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="696fe-121">createArray</span><span class="sxs-lookup"><span data-stu-id="696fe-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="696fe-122">vazio</span><span class="sxs-lookup"><span data-stu-id="696fe-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="696fe-123">primeiro</span><span class="sxs-lookup"><span data-stu-id="696fe-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="696fe-124">intersecção</span><span class="sxs-lookup"><span data-stu-id="696fe-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="696fe-125">JSON</span><span class="sxs-lookup"><span data-stu-id="696fe-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="696fe-126">última</span><span class="sxs-lookup"><span data-stu-id="696fe-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="696fe-127">comprimento</span><span class="sxs-lookup"><span data-stu-id="696fe-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="696fe-128">Mín.</span><span class="sxs-lookup"><span data-stu-id="696fe-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="696fe-129">Máx.</span><span class="sxs-lookup"><span data-stu-id="696fe-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="696fe-130">intervalo</span><span class="sxs-lookup"><span data-stu-id="696fe-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="696fe-131">Ignorar</span><span class="sxs-lookup"><span data-stu-id="696fe-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="696fe-132">tirar</span><span class="sxs-lookup"><span data-stu-id="696fe-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="696fe-133">União</span><span class="sxs-lookup"><span data-stu-id="696fe-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="696fe-134">Funções de comparação</span><span class="sxs-lookup"><span data-stu-id="696fe-134">Comparison functions</span></span>
<span data-ttu-id="696fe-135">O Resource Manager fornece várias funções, para efetuar comparações nos seus modelos.</span><span class="sxs-lookup"><span data-stu-id="696fe-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="696fe-136">igual a</span><span class="sxs-lookup"><span data-stu-id="696fe-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="696fe-137">menor</span><span class="sxs-lookup"><span data-stu-id="696fe-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="696fe-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="696fe-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="696fe-139">maior</span><span class="sxs-lookup"><span data-stu-id="696fe-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="696fe-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="696fe-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="696fe-141">Funções de valor de implementação</span><span class="sxs-lookup"><span data-stu-id="696fe-141">Deployment value functions</span></span>
<span data-ttu-id="696fe-142">O Resource Manager fornece seguinte Olá funciona para obter os valores de secções de modelo de Olá e os valores relacionados toohello implementação:</span><span class="sxs-lookup"><span data-stu-id="696fe-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="696fe-143">implementação</span><span class="sxs-lookup"><span data-stu-id="696fe-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="696fe-144">parâmetros</span><span class="sxs-lookup"><span data-stu-id="696fe-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="696fe-145">variáveis</span><span class="sxs-lookup"><span data-stu-id="696fe-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="696fe-146">Funções lógicas</span><span class="sxs-lookup"><span data-stu-id="696fe-146">Logical functions</span></span>
<span data-ttu-id="696fe-147">O Resource Manager fornece Olá funções para trabalhar com condições lógicas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="696fe-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="696fe-148">e</span><span class="sxs-lookup"><span data-stu-id="696fe-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="696fe-149">bool</span><span class="sxs-lookup"><span data-stu-id="696fe-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="696fe-150">Se</span><span class="sxs-lookup"><span data-stu-id="696fe-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="696fe-151">não</span><span class="sxs-lookup"><span data-stu-id="696fe-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="696fe-152">ou</span><span class="sxs-lookup"><span data-stu-id="696fe-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="696fe-153">Funções numérico</span><span class="sxs-lookup"><span data-stu-id="696fe-153">Numeric functions</span></span>
<span data-ttu-id="696fe-154">O Resource Manager fornece Olá funções para trabalhar com números inteiros os seguintes:</span><span class="sxs-lookup"><span data-stu-id="696fe-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="696fe-155">Adicionar</span><span class="sxs-lookup"><span data-stu-id="696fe-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="696fe-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="696fe-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="696fe-157">Div</span><span class="sxs-lookup"><span data-stu-id="696fe-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="696fe-158">número de vírgula flutuante</span><span class="sxs-lookup"><span data-stu-id="696fe-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="696fe-159">Int</span><span class="sxs-lookup"><span data-stu-id="696fe-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="696fe-160">Mín.</span><span class="sxs-lookup"><span data-stu-id="696fe-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="696fe-161">Máx.</span><span class="sxs-lookup"><span data-stu-id="696fe-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="696fe-162">MOD</span><span class="sxs-lookup"><span data-stu-id="696fe-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="696fe-163">MUL</span><span class="sxs-lookup"><span data-stu-id="696fe-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="696fe-164">sub</span><span class="sxs-lookup"><span data-stu-id="696fe-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="696fe-165">Funções de recursos</span><span class="sxs-lookup"><span data-stu-id="696fe-165">Resource functions</span></span>
<span data-ttu-id="696fe-166">O Resource Manager fornece Olá funções para obter valores de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="696fe-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="696fe-167">listKeys e lista {Value}</span><span class="sxs-lookup"><span data-stu-id="696fe-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="696fe-168">fornecedores</span><span class="sxs-lookup"><span data-stu-id="696fe-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="696fe-169">referência</span><span class="sxs-lookup"><span data-stu-id="696fe-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="696fe-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="696fe-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="696fe-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="696fe-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="696fe-172">subscrição</span><span class="sxs-lookup"><span data-stu-id="696fe-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="696fe-173">Funções de cadeia</span><span class="sxs-lookup"><span data-stu-id="696fe-173">String functions</span></span>
<span data-ttu-id="696fe-174">O Resource Manager fornece Olá funções para trabalhar com cadeias os seguintes:</span><span class="sxs-lookup"><span data-stu-id="696fe-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="696fe-175">Base64</span><span class="sxs-lookup"><span data-stu-id="696fe-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="696fe-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="696fe-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="696fe-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="696fe-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="696fe-178">concat</span><span class="sxs-lookup"><span data-stu-id="696fe-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="696fe-179">contém</span><span class="sxs-lookup"><span data-stu-id="696fe-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="696fe-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="696fe-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="696fe-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="696fe-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="696fe-182">vazio</span><span class="sxs-lookup"><span data-stu-id="696fe-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="696fe-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="696fe-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="696fe-184">primeiro</span><span class="sxs-lookup"><span data-stu-id="696fe-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="696fe-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="696fe-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="696fe-186">última</span><span class="sxs-lookup"><span data-stu-id="696fe-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="696fe-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="696fe-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="696fe-188">comprimento</span><span class="sxs-lookup"><span data-stu-id="696fe-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="696fe-189">padleft do modelo</span><span class="sxs-lookup"><span data-stu-id="696fe-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="696fe-190">substituir</span><span class="sxs-lookup"><span data-stu-id="696fe-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="696fe-191">Ignorar</span><span class="sxs-lookup"><span data-stu-id="696fe-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="696fe-192">dividir</span><span class="sxs-lookup"><span data-stu-id="696fe-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="696fe-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="696fe-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="696fe-194">cadeia</span><span class="sxs-lookup"><span data-stu-id="696fe-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="696fe-195">subcadeia</span><span class="sxs-lookup"><span data-stu-id="696fe-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="696fe-196">tirar</span><span class="sxs-lookup"><span data-stu-id="696fe-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="696fe-197">toLower</span><span class="sxs-lookup"><span data-stu-id="696fe-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="696fe-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="696fe-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="696fe-199">limitação</span><span class="sxs-lookup"><span data-stu-id="696fe-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="696fe-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="696fe-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="696fe-201">URI</span><span class="sxs-lookup"><span data-stu-id="696fe-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="696fe-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="696fe-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="696fe-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="696fe-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="696fe-204">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="696fe-204">Next steps</span></span>
* <span data-ttu-id="696fe-205">Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="696fe-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="696fe-206">toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="696fe-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="696fe-207">tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Gestor de recursos do Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="696fe-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="696fe-208">toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="696fe-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

