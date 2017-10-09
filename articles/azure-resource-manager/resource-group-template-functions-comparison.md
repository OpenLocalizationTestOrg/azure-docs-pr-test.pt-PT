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
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Funções de comparação para modelos Azure Resource Manager

O Resource Manager fornece várias funções, para efetuar comparações nos seus modelos.

* [igual a](#equals)
* [maior](#greater)
* [greaterOrEquals](#greaterorequals)
* [menor](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>igual a
`equals(arg1, arg2)`

Verifica se os dois valores igual entre si.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |int, string, matriz ou objeto |Olá primeiro valor toocheck para igualdade. |
| arg2 |Sim |int, string, matriz ou objeto |Olá segundo valor toocheck para igualdade. |

### <a name="return-value"></a>Valor devolvido

Devolve **verdadeiro** se os valores de Olá forem igual; caso contrário, **falso**.

### <a name="remarks"></a>Observações

Olá é igual a função é frequentemente usada com Olá `condition` elemento tootest se um recurso é implementado.

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

### <a name="example"></a>Exemplo

modelo de exemplo de Olá verifica diferentes tipos de valores para igualdade. Todos os valores predefinidos de Olá devolvem True.

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

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | bool | Verdadeiro |
| checkStrings | bool | Verdadeiro |
| checkArrays | bool | Verdadeiro |
| checkObjects | bool | Verdadeiro |


Olá exemplo seguinte utiliza [não](resource-group-template-functions-logical.md#not) com **é igual a**.

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

saída de Olá de Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| checkNotEquals | bool | Verdadeiro |


## <a name="greater"></a>maior
`greater(arg1, arg2)`

Verifica se o primeiro valor Olá é superior ao valor segundo Olá.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |int ou cadeia |Olá primeiro valor de comparação de maior Olá. |
| arg2 |Sim |int ou cadeia |Olá segundo valor de comparação de maior Olá. |

### <a name="return-value"></a>Valor devolvido

Devolve **verdadeiro** se Olá o primeiro valor é superior ao valor segundo Olá; caso contrário, **falso**.

### <a name="example"></a>Exemplo

modelo de exemplo de Olá verifica se um valor de Olá é superior a Olá outro.

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

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | bool | Falso |
| checkStrings | bool | Verdadeiro |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Verifica se o primeiro valor Olá toohello igual ou maior do que o segundo valor.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |int ou cadeia |Olá primeiro valor de comparação de Olá igual ou maior. |
| arg2 |Sim |int ou cadeia |Olá segundo valor de comparação de Olá igual ou maior. |

### <a name="return-value"></a>Valor devolvido

Devolve **verdadeiro** se Olá primeiro valor for igual ou maior do que toohello segundo; caso contrário, **falso**.

### <a name="example"></a>Exemplo

modelo de exemplo de Olá verifica se um valor de Olá é maior que ou igual toohello outro.

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

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | bool | Falso |
| checkStrings | bool | Verdadeiro |



## <a name="less"></a>menor
`less(arg1, arg2)`

Verifica se o primeiro valor Olá é menor que Olá segundo valor.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |int ou cadeia |Olá primeiro valor de Olá menos comparação. |
| arg2 |Sim |int ou cadeia |Olá segundo valor para Olá menos comparação. |

### <a name="return-value"></a>Valor devolvido

Devolve **verdadeiro** segundo valor se o primeiro valor Olá for inferior a Olá; caso contrário, **falso**.

### <a name="example"></a>Exemplo

modelo de exemplo de Olá verifica se um valor de Olá inferior Olá outro.

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

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | bool | Verdadeiro |
| checkStrings | bool | Falso |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Verifica se o primeiro valor Olá é menor ou igual toohello segundo valor.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |int ou cadeia |Olá primeiro valor de Olá inferior ou igual a comparação. |
| arg2 |Sim |int ou cadeia |Olá segundo valor para Olá inferior ou igual a comparação. |

### <a name="return-value"></a>Valor devolvido

Devolve **verdadeiro** se o primeiro valor Olá é menor ou igual toohello segundo valor; caso contrário, **falso**.

### <a name="example"></a>Exemplo

Olá modelo de exemplo verifica se Olá um valor é menor ou igual toohello outro.

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

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | bool | Verdadeiro |
| checkStrings | bool | Falso |



## <a name="next-steps"></a>Passos seguintes
* Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).
* toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md).

