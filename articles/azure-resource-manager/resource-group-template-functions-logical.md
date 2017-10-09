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
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Funções de lógicas de modelos Azure Resource Manager

O Resource Manager fornece várias funções, para efetuar comparações nos seus modelos.

* [e](#and)
* [bool](#bool)
* [Se](#if)
* [não](#not)
* [ou](#or)

## <a name="and"></a>e
`and(arg1, arg2)`

Verifica se ambos os valores de parâmetro forem verdadeiros.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |Valor booleano |Olá toocheck do primeiro valor se for VERDADEIRO. |
| arg2 |Sim |Valor booleano |Olá toocheck do segundo valor se for VERDADEIRO. |

### <a name="return-value"></a>Valor devolvido

Devolve **verdadeiro** se ambos os valores forem true; caso contrário, **falso**.

### <a name="examples"></a>Exemplos

Olá seguinte exemplo mostra como as funções de lógica de toouse.

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

saída de Olá de Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | bool | Falso |
| orExampleOutput | bool | Verdadeiro |
| notExampleOutput | bool | Falso |


## <a name="bool"></a>bool
`bool(arg1)`

Converte Olá tooa parâmetro booleano.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |cadeia ou int |Olá tooa tooconvert de valor booleano. |

### <a name="return-value"></a>Valor devolvido
Um booleano de Olá converter o valor.

### <a name="examples"></a>Exemplos

Olá seguinte exemplo mostra como toouse bool com uma cadeia ou um número inteiro.

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

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| trueString | bool | Verdadeiro |
| falseString | bool | Falso |
| trueInt | bool | Verdadeiro |
| falseInt | bool | Falso |

## <a name="if"></a>Se
`if(condition, trueValue, falseValue)`

Devolve um valor com base nas permissões de uma condição for true ou false.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| Condição |Sim |Valor booleano |Olá toocheck valor se for VERDADEIRO. |
| trueValue |Sim | cadeia, int, objetos ou matriz |Olá valor tooreturn quando a condição de Olá é verdadeira. |
| falseValue |Sim | cadeia, int, objetos ou matriz |Olá valor tooreturn quando a condição de Olá é falsa. |

### <a name="return-value"></a>Valor devolvido

Devolve o segundo parâmetro quando o primeiro parâmetro é **verdadeiro**; caso contrário, devolve o terceiro parâmetro.

### <a name="remarks"></a>Observações

Pode utilizar este conjunto de tooconditionally função uma propriedade de recurso. Olá exemplo seguinte não é um modelo completo, mas mostra as partes relevantes de Olá para definir o conjunto de disponibilidade de Olá condicionalmente.

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

### <a name="examples"></a>Exemplos

Olá seguinte exemplo mostra como toouse Olá `if` função.

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

saída de Olá de Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| yesOutput | Cadeia | Sim |
| noOutput | Cadeia | Não |


## <a name="not"></a>não
`not(arg1)`

Converte o valor booleano tooits opposite valor.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |Valor booleano |Olá tooconvert de valor. |


### <a name="return-value"></a>Valor devolvido

Devolve **verdadeiro** quando o parâmetro é **falso**. Devolve **falso** quando o parâmetro é **verdadeiro**.

### <a name="examples"></a>Exemplos

Olá seguinte exemplo mostra como as funções de lógica de toouse.

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

saída de Olá de Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | bool | Falso |
| orExampleOutput | bool | Verdadeiro |
| notExampleOutput | bool | Falso |

Olá exemplo seguinte utiliza **não** com [é igual a](resource-group-template-functions-comparison.md#equals).

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


## <a name="or"></a>ou
`or(arg1, arg2)`

Verifica se o valor do parâmetro é verdadeiro.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| arg1 |Sim |Valor booleano |Olá toocheck do primeiro valor se for VERDADEIRO. |
| arg2 |Sim |Valor booleano |Olá toocheck do segundo valor se for VERDADEIRO. |

### <a name="return-value"></a>Valor devolvido

Devolve **verdadeiro** se o valor for true; caso contrário, **falso**.

### <a name="examples"></a>Exemplos

Olá seguinte exemplo mostra como as funções de lógica de toouse.

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

saída de Olá de Olá anterior exemplo é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | bool | Falso |
| orExampleOutput | bool | Verdadeiro |
| notExampleOutput | bool | Falso |


## <a name="next-steps"></a>Passos seguintes
* Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).
* toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md).

