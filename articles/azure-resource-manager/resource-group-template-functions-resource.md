---
title: "funções de modelo do Resource Manager aaaAzure - recursos | Microsoft Docs"
description: "Descreve as funções de Olá toouse um valores de tooretrieve de modelo do Azure Resource Manager sobre os recursos."
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
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Funções de recursos para os modelos Azure Resource Manager

O Resource Manager fornece Olá funções para obter valores de recursos a seguir:

* [listKeys e lista {Value}](#listkeys)
* [fornecedores](#providers)
* [referência](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [subscrição](#subscription)

tooget valores de parâmetros, variáveis ou implementação atual de Olá, consulte [das funções de valor de implementação](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys e lista {Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Devolve Olá valores para qualquer tipo de recurso que suporta a operação de lista de Olá. utilização de mais comuns de Olá é `listKeys`. 

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| resourceName ou resourceIdentifier |Sim |Cadeia |Identificador exclusivo para o recurso de Olá. |
| apiVersion |Sim |Cadeia |Versão de API do Estado de runtime do recurso. Normalmente, no formato de Olá, **aaaa-mm-dd**. |

### <a name="return-value"></a>Valor devolvido

Olá devolveu o objeto de listKeys tem Olá seguinte formato:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

Outras funções de lista têm formatos de retorno diferentes. formato de Olá toosee de uma função, incluí-la na secção de saídas Olá conforme mostrado no modelo de exemplo de Olá. 

### <a name="remarks"></a>Observações

Todas as operações que começa com **lista** pode ser utilizado como uma função no modelo. Olá operações disponíveis incluem não só listKeys, mas também operações como `list`, `listAdminKeys`, e `listStatus`. No entanto, não é possível utilizar **lista** operações que requerem valores de Olá corpo do pedido. Por exemplo, Olá [lista conta SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operação requer os parâmetros de corpo do pedido como *signedExpiry*, por isso, não é possível utilizá-lo dentro de um modelo.

toodetermine que tipos de recursos tem uma operação de lista, terá de Olá seguintes opções:

* Olá vista [operações de REST API](/rest/api/) para um fornecedor de recursos e procure para operações de lista. Por exemplo, contas de armazenamento tem Olá [listKeys operação](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Olá utilize [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) cmdlet do PowerShell. Olá exemplo seguinte obtém todas as operações de lista para contas de armazenamento:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Utilize Olá comando da CLI do Azure toofilter Olá apenas operações de lista a seguir:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Especificar recursos Olá utilizando qualquer um dos Olá [resourceId função](#resourceid), ou o formato de Olá `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Exemplo

Olá exemplo seguinte mostra como tooreturn Olá chaves primária e secundária de uma conta de armazenamento no Olá produz secção.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>fornecedores
`providers(providerNamespace, [resourceType])`

Devolve informações sobre um fornecedor de recursos e os respetivos tipos de recurso suportados. Se não fornecer um tipo de recurso, a função de Olá devolve todos os tipos de Olá suportado para o fornecedor de recursos de Olá.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| providerNamespace |Sim |Cadeia |Espaço de nomes do fornecedor de Olá |
| resourceType |Não |Cadeia |Olá o tipo de recurso dentro Olá especificado espaço de nomes. |

### <a name="return-value"></a>Valor devolvido

Cada tipo suportado é devolvido em Olá seguinte formato: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Ordenação de matriz de Olá devolveu valores não é garantida.

### <a name="example"></a>Exemplo

Olá seguinte exemplo mostra como toouse Olá a função de fornecedor:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

Olá anterior exemplo devolve um objeto numa Olá seguinte formato:

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>Referência
`reference(resourceName or resourceIdentifier, [apiVersion])`

Devolve um objeto que representa o estado do tempo de execução de um recurso.

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| resourceName ou resourceIdentifier |Sim |Cadeia |Nome ou o identificador exclusivo de um recurso. |
| apiVersion |Não |Cadeia |Versão de API do Olá recurso especificado. Inclua este parâmetro quando o recurso de Olá não está aprovisionado dentro do mesmo modelo. Normalmente, no formato de Olá, **aaaa-mm-dd**. |

### <a name="return-value"></a>Valor devolvido

Cada tipo de recurso devolve propriedades diferentes para a função de referência de Olá. função Olá não devolve um formato único e predefinido. Propriedades de Olá toosee para um tipo de recurso, devolver objeto Olá Olá produz secção conforme mostrado no exemplo de Olá.

### <a name="remarks"></a>Observações

função de referência de Olá deriva o respetivo valor a partir de um Estado de runtime e, por conseguinte, não pode ser utilizada na secção de variáveis de Olá. Pode ser utilizado na secção de saídas de um modelo. 

Ao utilizar a função de referência de Olá, implicitamente declarar que um recurso depende outro recurso, se o recurso de Olá referenciado é aprovisionado dentro do mesmo modelo. Não é necessário tooalso utilize Olá dependsOn a propriedade. Olá função não é avaliada até hello recurso referenciado concluiu a implementação.

os nomes de propriedade de Olá toosee e valores para um tipo de recurso, crie um modelo que devolve o objeto de Olá Olá saídas secção. Se tiver um recurso existente desse tipo, o seu modelo devolve o objeto de Olá sem a implementar quaisquer novos recursos. 

Normalmente, utiliza Olá **referência** funcionar tooreturn um valor específico de um objeto, tal como o ponto final do blob Olá URI ou o nome de domínio completamente qualificado.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>Exemplo

referência e toodeploy recurso Olá Olá mesmo modelo, utilize:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

Olá anterior exemplo devolve um objeto numa Olá seguinte formato:

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

Olá exemplo que se segue faz referência a uma conta de armazenamento que não seja implementada neste modelo. Olá conta de armazenamento já existe num Olá mesmo grupo de recursos.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

Devolve um objeto que representa o grupo de recursos atual Olá. 

### <a name="return-value"></a>Valor devolvido

Olá devolveu o objeto está no Olá seguinte formato:

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>Observações

Uma utilização comum da função de resourceGroup Olá é recursos toocreate Olá mesma localização do grupo de recursos de Olá. Olá exemplo seguinte utiliza Olá recursos localização tooassign Olá localização do grupo de para um web site.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>Exemplo

Olá modelo seguinte devolve as propriedades de Olá Olá do grupo de recursos.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

Olá anterior exemplo devolve um objeto numa Olá seguinte formato:

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Devolve Olá Identificador exclusivo de um recurso. Utilize esta função quando o nome de recurso Olá é ambíguo ou não aprovisionada no Olá mesmo modelo. 

### <a name="parameters"></a>Parâmetros

| Parâmetro | Necessário | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| subscriptionId |Não |cadeia (formato de GUID no) |Valor predefinido é subscrição atual Olá. Especificar este valor quando precisar de tooretrieve um recurso na outra subscrição. |
| resourceGroupName |Não |Cadeia |Valor predefinido é o grupo de recursos atual. Especificar este valor quando precisar de tooretrieve um recurso noutro grupo de recursos. |
| resourceType |Sim |Cadeia |Tipo de recurso, incluindo o espaço de nomes de fornecedor de recursos. |
| resourceName1 |Sim |Cadeia |Nome do recurso. |
| resourceName2 |Não |Cadeia |Recursos nome segmento seguinte se o recurso está aninhado. |

### <a name="return-value"></a>Valor devolvido

Identificador de Olá é devolvido em Olá seguinte formato:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Observações

Olá valores de parâmetros que especificou dependem se o recurso de Olá tem Olá mesmo grupo de recursos e subscrição implementação atual Olá.

ID de recurso de Olá tooget para uma conta de armazenamento no Olá mesma subscrição e grupo de recursos, utilize:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

Olá tooget Olá ID de recurso para uma conta do storage na mesma subscrição, mas um grupo de recursos diferente, utilize:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID de recurso de Olá tooget para uma conta de armazenamento numa subscrição diferente e o grupo de recursos, utilize:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

ID de recurso de Olá tooget para uma base de dados de um grupo de recursos diferente, utilize:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Muitas vezes, precisa de toouse esta função quando utilizar uma conta de armazenamento ou de rede virtual num grupo de recursos alternativo. Olá exemplo seguinte mostra como um recurso de um grupo de recursos externos pode facilmente ser utilizado:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>Exemplo

Olá exemplo seguinte devolve Olá ID de recurso para uma conta de armazenamento no grupo de recursos de Olá:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

Olá o resultado da Olá anterior exemplo com valores predefinidos de Olá é:

| Nome | Tipo | Valor |
| ---- | ---- | ----- |
| sameRGOutput | Cadeia | /subscriptions/{current-sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | Cadeia | /subscriptions/{current-sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | Cadeia | /subscriptions/{different-sub-ID}/resourceGroups/otherResourceGroup/Providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | Cadeia | /subscriptions/{current-sub-ID}/resourceGroups/examplegroup/Providers/Microsoft.SQL/Servers/serverName/Databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>subscrição
`subscription()`

Devolve detalhes sobre a subscrição de Olá para a implementação atual Olá. 

### <a name="return-value"></a>Valor devolvido

função de Olá devolve Olá seguinte formato:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Exemplo

Olá exemplo seguinte mostra a função de subscrição de Olá chamada Olá saídas secção. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>Passos seguintes
* Para obter uma descrição das secções Olá num modelo Azure Resource Manager, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).
* toomerge vários modelos, consulte [utilizar modelos ligados com o Azure Resource Manager](resource-group-linked-templates.md).
* tooiterate um número de vezes especificado ao criar um tipo de recurso, consulte [criar várias instâncias de recursos no Azure Resource Manager](resource-group-create-multiple.md).
* toosee como modelo de Olá toodeploy criou, consulte [implementar uma aplicação com o modelo Azure Resource Manager](resource-group-template-deploy.md).

