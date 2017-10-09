---
title: "modelos de aaaLink para implementação do Azure | Microsoft Docs"
description: "Descreve como toouse ligado modelos num toocreate de modelo Azure Resource Manager uma solução de modelo modulares. Mostra como valores de parâmetros de toopass, especifique um ficheiro de parâmetros e criados dinamicamente URLs."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Utilizar modelos ligados ao implementar os recursos do Azure
De dentro de um modelo Azure Resource Manager, pode ligar tooanother modelo, que lhe permite toodecompose a implementação para um conjunto de modelos direcionados e com uma finalidade específica. Tal como acontece com decomposing uma aplicação em várias classes de código, decomposição proporciona vantagens em termos de teste, reutilização e facilitar a leitura.  

Pode passar os parâmetros a partir de um modelo de ligado tooa modelo principal e esses parâmetros diretamente podem mapear tooparameters ou variáveis expostas pelo Olá chamar o modelo. modelo ligado Olá também pode passar de um modelo de origem da variável toohello back-saída, ativar uma troca de dados bidirecional entre os modelos.

## <a name="linking-tooa-template"></a>Ligação tooa modelo
Criar uma ligação entre dois modelos, adicionando um recurso de implementação no modelo principal Olá esse toohello de pontos ligado modelo. Definir Olá **templateLink** propriedade toohello URI de modelo de Olá ligado. Pode fornecer valores de parâmetro de modelo ligado Olá diretamente no seu modelo ou um ficheiro de parâmetros. Olá exemplo seguinte utiliza Olá **parâmetros** propriedade toospecify diretamente um valor de parâmetro.

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

Como outros tipos de recursos, pode definir as dependências entre modelo ligado Olá e outros recursos. Por conseguinte, quando a outros recursos necessitam de um valor de saída do modelo ligado Olá, pode certificar-se modelo ligado Olá é implementado antes de lhes. Em alternativa, quando o modelo ligado Olá depende de outros recursos, pode certificar-se a que outros recursos são implementados antes do modelo ligado Olá. Pode obter um valor de um modelo ligado com Olá sintaxe:

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Olá serviço Gestor de recursos tem de ser modelo ligado do tooaccess capaz de Olá. Não é possível especificar um ficheiro local ou um ficheiro que só está disponível na sua rede local para o modelo de Olá ligado. Apenas pode fornecer um valor URI que inclui um **http** ou **https**. Uma das alternativas consiste tooplace seu modelo ligado numa conta de armazenamento e utilização hello URI para que o item, tal como mostrado no seguinte exemplo de Olá:

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Embora o modelo ligado Olá tem de estar disponível externamente, não é necessário toobe toohello geralmente disponível público. Pode adicionar a conta de armazenamento privada tooa de modelo que é proprietário da conta do storage Olá tooonly acessível. Em seguida, crie um acesso de token tooenable de assinatura (SAS) de acesso partilhado durante a implementação. Adicionar esse toohello de token SAS URI para o modelo de Olá ligado. Para obter passos sobre como configurar um modelo de uma conta de armazenamento e de gerar um token SAS, consulte [implementar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md) ou [implementar recursos com modelos do Resource Manager e CLI do Azure](resource-group-template-deploy-cli.md). 

Olá seguinte exemplo mostra um modelo de principal que o modelo tooanother ligações. modelo ligado Olá é acedido com um token SAS, que é transmitido como um parâmetro.

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

Apesar do token de Olá seja transmitido como uma cadeia segura, hello URI do modelo ligado Olá, incluindo o token SAS de Olá, é registado em operações de implementação de Olá. exposição toolimit, definir uma expiração do token de Olá.

O Resource Manager processa cada modelo ligado como uma implementação separada. No histórico de implementação de Olá Olá grupo de recursos, consulte implementações separadas para principal Olá e modelos aninhados.

![histórico de implementações](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Ligar o ficheiro de parâmetros tooa
utiliza o exemplo seguinte Olá Olá **parametersLink** ficheiro de parâmetros do propriedade toolink tooa.

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

Olá URI valor para o ficheiro de parâmetro ligado Olá não pode ser um ficheiro local e tem de incluir um **http** ou **https**. ficheiro de parâmetros de Olá também pode ser limitado tooaccess através de um token SAS.

## <a name="using-variables-toolink-templates"></a>Utilizar variáveis toolink modelos
exemplos anteriores Olá mostrou valores codificados de URL para ligações de modelo Olá. Esta abordagem poderá funcionar para um modelo simples, mas não funciona bem quando trabalhar com um grande conjunto de modelos modulares. Em vez disso, pode criar uma variável estática que armazena um URL de base para o modelo de Olá principal e, em seguida, criar dinamicamente os URLs para os modelos de Olá ligado desse URL base. benefício de Olá desta abordagem é que pode facilmente mover ou bifurcação modelo Olá porque precisa apenas de variável estática de Olá toochange no modelo principal Olá. modelo de principais de Olá transmite Olá URIs em toda a Olá decomposed modelo correto.

Olá exemplo seguinte mostra como toouse um toocreate URL base ligado dois URLs para modelos (**sharedTemplateUrl** e **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

Também pode utilizar [deployment()](resource-group-template-functions-deployment.md#deployment) tooget Olá URL base do modelo atual Olá e utilizar esse URL de Olá tooget para outros modelos de Olá mesma localização. Esta abordagem é útil se a localização do modelo for alterada (talvez devida tooversioning) ou se quiser tooavoid rígido codificação URLs no ficheiro de modelo Olá. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Exemplo completo
Olá, modelos de exemplo a seguir mostra uma disposição simplificada de modelos ligados tooillustrate muitos outros dos conceitos de Olá neste artigo. Parte do princípio de modelos de Olá foram adicionados toohello desativado mesmo contentor numa conta do storage com o acesso público. modelo ligado Olá transmite um modelo de principal do valor back toohello no Olá **produz** secção.

Olá **parent.json** ficheiro é composta por:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

Olá **helloworld.json** ficheiro é composta por:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

No PowerShell, obter um token para o contentor de Olá e implementem modelos Olá com:

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

No Azure CLI 2.0, obter um token para o contentor de Olá e implementar modelos de Olá com Olá seguinte código:

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a>Passos seguintes
* toolearn sobre Olá definir Olá ordem de implementação para os seus recursos, consulte [definir dependências nos modelos Azure Resource Manager](resource-group-define-dependencies.md)
* toolearn como toodefine um recurso, mas criar várias instâncias do mesmo, consulte [criar várias instâncias de recursos no Gestor de recursos do Azure](resource-group-create-multiple.md)

