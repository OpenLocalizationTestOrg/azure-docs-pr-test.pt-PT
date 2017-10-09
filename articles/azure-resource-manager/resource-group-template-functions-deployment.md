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
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Funções de implementação de modelos Azure Resource Manager 

O Resource Manager fornece seguinte Olá funciona para obter os valores de secções de modelo de Olá e os valores relacionados toohello implementação:

* [implementação](#deployment)
* [parâmetros](#parameters)
* [variáveis](#variables)

valores de tooget de recursos, grupos de recursos ou subscrições, consulte [funções recursos](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>implementação
`deployment()`

Devolve informações sobre as operações de implementação Olá atual.

### <a name="return-value"></a>Valor devolvido

Esta função devolve o objeto de Olá que é transmitido durante a implementação. Propriedades de Olá no Olá devolvida objeto divergir com base nas se hello objeto de implementação é transmitido como uma ligação ou como um objeto na linha. Quando Olá implementação é transmitido um objeto na linha, tal como quando utilizar Olá **- TemplateFile** parâmetro no Azure PowerShell toopoint tooa ficheiro local, Olá devolveu o objeto tem Olá seguinte formato:

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

Quando é transmitido um objeto de Olá como uma hiperligação, por exemplo, quando utilizar Olá **- TemplateUri** parâmetro toopoint tooa remoto objeto objeto Olá é devolvido em Olá seguinte formato: 

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

### <a name="remarks"></a>Observações

Pode utilizar o modelo de tooanother deployment() toolink com base no Olá URI do modelo de principal de Olá.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Exemplo

Olá exemplo seguinte devolve um objeto de implementação de Olá:

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

Olá anterior exemplo Olá de devolve os seguintes objetos:

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

## <a name="parameters"></a>parâmetros
`parameters(parameterName)`

Devolve um valor de parâmetro. nome de parâmetro especificado do Olá deve ser definido na secção de parâmetros de Olá do modelo de Olá.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| parameterName |Sim |Cadeia |nome de Olá do Olá tooreturn de parâmetro. |

### <a name="return-value"></a>Valor devolvido

especificar o valor de Olá de Olá parâmetro.

### <a name="remarks"></a>Observações

Normalmente, utiliza valores de recursos de tooset de parâmetros. Olá exemplo a seguir define Olá nome do valor do parâmetro do web site toohello transmitido durante a implementação.

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

### <a name="example"></a>Exemplo

Olá exemplo seguinte mostra uma utilização da função de parâmetros de Olá simplificada.

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

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| stringOutput | Cadeia | opção 1 |
| intOutput | Int | 1 |
| objectOutput | Objeto | {"um": "a", "dois": "b"} |
| arrayOutput | Matriz | [1, 2, 3] |
| crossOutput | Cadeia | opção 1 |

<a id="variables" />

## <a name="variables"></a>variáveis
`variables(variableName)`

Devolve Olá valor da variável. o nome de variável especificado Olá tem de ser definido na secção de variáveis de Olá do modelo de Olá.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| variableName |Sim |Cadeia |nome de Olá do Olá tooreturn de variável. |

### <a name="return-value"></a>Valor devolvido

especificar o valor de Olá de Olá variável.

### <a name="remarks"></a>Observações

Normalmente, utiliza as variáveis toosimplify seu modelo por construir valores complexos apenas uma vez. Olá exemplo seguinte constrói um nome exclusivo para uma conta de armazenamento.

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

### <a name="example"></a>Exemplo

modelo de exemplo de Olá devolve diferentes valores de variáveis.

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

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| exampleOutput1 | Cadeia | myVariable |
| exampleOutput2 | Matriz | [1, 2, 3, 4] |
| exampleOutput3 | Cadeia | myVariable |
| exampleOutput4 |  Objeto | {"property1": "value1", "property2": "value2"} |

## <a name="next-steps"></a>Passos seguintes
* Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).
* toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md).

