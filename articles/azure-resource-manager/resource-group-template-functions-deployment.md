---
title: "funções de modelo do Resource Manager aaaAzure - implementação | Microsoft Docs"
description: "Descreve as funções de Olá toouse um informações de implementação do tooretrieve de modelo Azure Resource Manager."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="2e458-103">Funções de implementação de modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e458-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="2e458-104">O Resource Manager fornece seguinte Olá funciona para obter os valores de secções de modelo de Olá e os valores relacionados toohello implementação:</span><span class="sxs-lookup"><span data-stu-id="2e458-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="2e458-105">implementação</span><span class="sxs-lookup"><span data-stu-id="2e458-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="2e458-106">parâmetros</span><span class="sxs-lookup"><span data-stu-id="2e458-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="2e458-107">variáveis</span><span class="sxs-lookup"><span data-stu-id="2e458-107">variables</span></span>](#variables)

<span data-ttu-id="2e458-108">valores de tooget de recursos, grupos de recursos ou subscrições, consulte [funções recursos](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="2e458-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="2e458-109">implementação</span><span class="sxs-lookup"><span data-stu-id="2e458-109">deployment</span></span>
`deployment()`

<span data-ttu-id="2e458-110">Devolve informações sobre as operações de implementação Olá atual.</span><span class="sxs-lookup"><span data-stu-id="2e458-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="2e458-111">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="2e458-111">Return value</span></span>

<span data-ttu-id="2e458-112">Esta função devolve o objeto de Olá que é transmitido durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="2e458-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="2e458-113">Propriedades de Olá no Olá devolvida objeto divergir com base nas se hello objeto de implementação é transmitido como uma ligação ou como um objeto na linha.</span><span class="sxs-lookup"><span data-stu-id="2e458-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="2e458-114">Quando Olá implementação é transmitido um objeto na linha, tal como quando utilizar Olá **- TemplateFile** parâmetro no Azure PowerShell toopoint tooa ficheiro local, Olá devolveu o objeto tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="2e458-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="2e458-115">Quando é transmitido um objeto de Olá como uma hiperligação, por exemplo, quando utilizar Olá **- TemplateUri** parâmetro toopoint tooa remoto objeto objeto Olá é devolvido em Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="2e458-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="2e458-116">Observações</span><span class="sxs-lookup"><span data-stu-id="2e458-116">Remarks</span></span>

<span data-ttu-id="2e458-117">Pode utilizar o modelo de tooanother deployment() toolink com base no Olá URI do modelo de principal de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e458-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="2e458-118">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2e458-118">Example</span></span>

<span data-ttu-id="2e458-119">Olá exemplo seguinte devolve um objeto de implementação de Olá:</span><span class="sxs-lookup"><span data-stu-id="2e458-119">hello following example returns hello deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="2e458-120">Olá anterior exemplo Olá de devolve os seguintes objetos:</span><span class="sxs-lookup"><span data-stu-id="2e458-120">hello preceding example returns hello following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="2e458-121">parâmetros</span><span class="sxs-lookup"><span data-stu-id="2e458-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="2e458-122">Devolve um valor de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2e458-122">Returns a parameter value.</span></span> <span data-ttu-id="2e458-123">nome de parâmetro especificado do Olá deve ser definido na secção de parâmetros de Olá do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e458-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="2e458-124">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="2e458-124">Parameters</span></span>

| <span data-ttu-id="2e458-125">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="2e458-125">Parameter</span></span> | <span data-ttu-id="2e458-126">Necessário</span><span class="sxs-lookup"><span data-stu-id="2e458-126">Required</span></span> | <span data-ttu-id="2e458-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="2e458-127">Type</span></span> | <span data-ttu-id="2e458-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="2e458-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2e458-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="2e458-129">parameterName</span></span> |<span data-ttu-id="2e458-130">Sim</span><span class="sxs-lookup"><span data-stu-id="2e458-130">Yes</span></span> |<span data-ttu-id="2e458-131">Cadeia</span><span class="sxs-lookup"><span data-stu-id="2e458-131">string</span></span> |<span data-ttu-id="2e458-132">nome de Olá do Olá tooreturn de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2e458-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2e458-133">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="2e458-133">Return value</span></span>

<span data-ttu-id="2e458-134">especificar o valor de Olá de Olá parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2e458-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="2e458-135">Observações</span><span class="sxs-lookup"><span data-stu-id="2e458-135">Remarks</span></span>

<span data-ttu-id="2e458-136">Normalmente, utiliza valores de recursos de tooset de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="2e458-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="2e458-137">Olá exemplo a seguir define Olá nome do valor do parâmetro do web site toohello transmitido durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="2e458-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="2e458-138">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2e458-138">Example</span></span>

<span data-ttu-id="2e458-139">Olá exemplo seguinte mostra uma utilização da função de parâmetros de Olá simplificada.</span><span class="sxs-lookup"><span data-stu-id="2e458-139">hello following example shows a simplified use of hello parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="2e458-140">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="2e458-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2e458-141">Nome</span><span class="sxs-lookup"><span data-stu-id="2e458-141">Name</span></span> | <span data-ttu-id="2e458-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="2e458-142">Type</span></span> | <span data-ttu-id="2e458-143">Valor</span><span class="sxs-lookup"><span data-stu-id="2e458-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2e458-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="2e458-144">stringOutput</span></span> | <span data-ttu-id="2e458-145">Cadeia</span><span class="sxs-lookup"><span data-stu-id="2e458-145">String</span></span> | <span data-ttu-id="2e458-146">opção 1</span><span class="sxs-lookup"><span data-stu-id="2e458-146">option 1</span></span> |
| <span data-ttu-id="2e458-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="2e458-147">intOutput</span></span> | <span data-ttu-id="2e458-148">Int</span><span class="sxs-lookup"><span data-stu-id="2e458-148">Int</span></span> | <span data-ttu-id="2e458-149">1</span><span class="sxs-lookup"><span data-stu-id="2e458-149">1</span></span> |
| <span data-ttu-id="2e458-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="2e458-150">objectOutput</span></span> | <span data-ttu-id="2e458-151">Objeto</span><span class="sxs-lookup"><span data-stu-id="2e458-151">Object</span></span> | <span data-ttu-id="2e458-152">{"um": "a", "dois": "b"}</span><span class="sxs-lookup"><span data-stu-id="2e458-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="2e458-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2e458-153">arrayOutput</span></span> | <span data-ttu-id="2e458-154">Matriz</span><span class="sxs-lookup"><span data-stu-id="2e458-154">Array</span></span> | <span data-ttu-id="2e458-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="2e458-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="2e458-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="2e458-156">crossOutput</span></span> | <span data-ttu-id="2e458-157">Cadeia</span><span class="sxs-lookup"><span data-stu-id="2e458-157">String</span></span> | <span data-ttu-id="2e458-158">opção 1</span><span class="sxs-lookup"><span data-stu-id="2e458-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="2e458-159">variáveis</span><span class="sxs-lookup"><span data-stu-id="2e458-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="2e458-160">Devolve Olá valor da variável.</span><span class="sxs-lookup"><span data-stu-id="2e458-160">Returns hello value of variable.</span></span> <span data-ttu-id="2e458-161">o nome de variável especificado Olá tem de ser definido na secção de variáveis de Olá do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e458-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="2e458-162">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="2e458-162">Parameters</span></span>

| <span data-ttu-id="2e458-163">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="2e458-163">Parameter</span></span> | <span data-ttu-id="2e458-164">Necessário</span><span class="sxs-lookup"><span data-stu-id="2e458-164">Required</span></span> | <span data-ttu-id="2e458-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="2e458-165">Type</span></span> | <span data-ttu-id="2e458-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="2e458-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2e458-167">variableName</span><span class="sxs-lookup"><span data-stu-id="2e458-167">variableName</span></span> |<span data-ttu-id="2e458-168">Sim</span><span class="sxs-lookup"><span data-stu-id="2e458-168">Yes</span></span> |<span data-ttu-id="2e458-169">Cadeia</span><span class="sxs-lookup"><span data-stu-id="2e458-169">String</span></span> |<span data-ttu-id="2e458-170">nome de Olá do Olá tooreturn de variável.</span><span class="sxs-lookup"><span data-stu-id="2e458-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2e458-171">Valor devolvido</span><span class="sxs-lookup"><span data-stu-id="2e458-171">Return value</span></span>

<span data-ttu-id="2e458-172">especificar o valor de Olá de Olá variável.</span><span class="sxs-lookup"><span data-stu-id="2e458-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="2e458-173">Observações</span><span class="sxs-lookup"><span data-stu-id="2e458-173">Remarks</span></span>

<span data-ttu-id="2e458-174">Normalmente, utiliza as variáveis toosimplify seu modelo por construir valores complexos apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="2e458-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="2e458-175">Olá exemplo seguinte constrói um nome exclusivo para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2e458-175">hello following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="2e458-176">Exemplo</span><span class="sxs-lookup"><span data-stu-id="2e458-176">Example</span></span>

<span data-ttu-id="2e458-177">modelo de exemplo de Olá devolve diferentes valores de variáveis.</span><span class="sxs-lookup"><span data-stu-id="2e458-177">hello example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="2e458-178">Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:</span><span class="sxs-lookup"><span data-stu-id="2e458-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2e458-179">Nome</span><span class="sxs-lookup"><span data-stu-id="2e458-179">Name</span></span> | <span data-ttu-id="2e458-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="2e458-180">Type</span></span> | <span data-ttu-id="2e458-181">Valor</span><span class="sxs-lookup"><span data-stu-id="2e458-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2e458-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="2e458-182">exampleOutput1</span></span> | <span data-ttu-id="2e458-183">Cadeia</span><span class="sxs-lookup"><span data-stu-id="2e458-183">String</span></span> | <span data-ttu-id="2e458-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="2e458-184">myVariable</span></span> |
| <span data-ttu-id="2e458-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="2e458-185">exampleOutput2</span></span> | <span data-ttu-id="2e458-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="2e458-186">Array</span></span> | <span data-ttu-id="2e458-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="2e458-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="2e458-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="2e458-188">exampleOutput3</span></span> | <span data-ttu-id="2e458-189">Cadeia</span><span class="sxs-lookup"><span data-stu-id="2e458-189">String</span></span> | <span data-ttu-id="2e458-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="2e458-190">myVariable</span></span> |
| <span data-ttu-id="2e458-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="2e458-191">exampleOutput4</span></span> |  <span data-ttu-id="2e458-192">Objeto</span><span class="sxs-lookup"><span data-stu-id="2e458-192">Object</span></span> | <span data-ttu-id="2e458-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="2e458-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2e458-194">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2e458-194">Next steps</span></span>
* <span data-ttu-id="2e458-195">Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2e458-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2e458-196">toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2e458-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="2e458-197">tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2e458-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="2e458-198">toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2e458-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

