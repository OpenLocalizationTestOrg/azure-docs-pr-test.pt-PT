---
title: aaaDeploy recursos com o PowerShell e o modelo | Microsoft Docs
description: "Utilize o Azure Resource Manager e o Azure PowerShell toodeploy um tooAzure de recursos. recursos de Olá são definidos num modelo do Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Implementar recursos com modelos do Resource Manager e do Azure PowerShell

Este tópico explica como toouse Azure PowerShell com toodeploy de modelos do Resource Manager a tooAzure de recursos. Se não estiver familiarizado com conceitos de Olá implementar e gerir as suas soluções do Azure, consulte [descrição geral do Azure Resource Manager](resource-group-overview.md).

modelo do Resource Manager Olá implementar possível ser um ficheiro no seu computador local ou um ficheiro externo que está localizado num repositório como GitHub. modelo de Olá implementar neste artigo está disponível no Olá [modelo de exemplo](#sample-template) secção, ou como [modelo de conta de armazenamento no GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Implementar um modelo a partir do seu computador local

Quando implementar tooAzure de recursos, pode:

1. Inicie sessão no tooyour a conta do Azure
2. Crie um grupo de recursos que funciona como contentor Olá recursos Olá implementado. nome de Olá Olá do grupo de recursos só pode incluir carateres alfanuméricos, pontos, carateres de sublinhado, hífenes e parênteses. Pode ser a cópia de segurança too90 carateres. Não pode terminar num período.
3. Implementar a modelo Olá de grupo de recursos de toohello que define Olá recursos toocreate

Um modelo pode incluir os parâmetros que permitem a implementação de Olá toocustomize. Por exemplo, pode fornecer valores que são adaptados para um ambiente específico (por exemplo, o desenvolvimento, teste e produção). modelo de exemplo de Olá define um parâmetro da conta de armazenamento Olá SKU.

Olá seguinte exemplo cria um grupo de recursos e implementa um modelo a partir do seu computador local:

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

implementação de Olá pode demorar alguns minutos toocomplete. Quando terminar, verá uma mensagem que inclui o resultado de Olá:

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Implementar um modelo a partir de uma origem externa

Em vez de armazenar modelos do Resource Manager no seu computador local, pode preferir toostore-las numa localização externa. Pode armazenar modelos num repositório de controlo de origem (por exemplo, o GitHub). Em alternativa, pode armazená-las numa conta de armazenamento do Azure para acesso partilhado na sua organização.

toodeploy um modelo externo, utilize Olá **TemplateUri** parâmetro. Utilize Olá URI no modelo de exemplo do Olá exemplo toodeploy Olá a partir do GitHub.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Olá anterior exemplo requer um URI acessível publicamente para modelo de Olá, que funciona para a maioria dos cenários, porque o modelo não deve incluir dados confidenciais. Se precisar de toospecify dados confidenciais (por exemplo, uma palavra-passe de administrador), passe esse valor como um parâmetro seguro. No entanto, se não pretender que o modelo toobe acessível publicamente, pode protegê-lo armazenando-o num contentor de armazenamento privada. Para obter informações sobre a implementação de um modelo que necessita de um token de assinatura (SAS) de acesso partilhado, consulte [implementar a modelo privado com o SAS token](resource-manager-powershell-sas-token.md).

## <a name="parameter-files"></a>Ficheiros de parâmetro

Em vez de a transmitir parâmetros como valores de inline no script, pode encontrá-lo mais fácil toouse um ficheiro JSON que contém os valores de parâmetros de Olá. ficheiro de parâmetros de Olá tem de constar Olá seguinte formato:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

Tenha em atenção que a secção de parâmetros de Olá inclui um nome de parâmetro que corresponda ao parâmetro Olá definido no seu modelo (storageAccountType). ficheiro de parâmetros de Olá contém um valor para parâmetro Olá. Este valor é automaticamente transmitido toohello modelo durante a implementação. Pode criar vários ficheiros de parâmetro para diferentes cenários de implementação e, então, passe no ficheiro de parâmetro adequado Olá. 

Copie Olá anterior exemplo e guarde-o como um ficheiro denominado `storage.parameters.json`.

toopass um ficheiro de parâmetros local, utilizar Olá **TemplateParameterFile** parâmetro:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

toopass um ficheiro de parâmetros externos, utilize Olá **TemplateParameterUri** parâmetro:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

Pode utilizar parâmetros inline e um parâmetro de local ficheiros Olá mesma operação de implementação. Por exemplo, pode especificar alguns valores no ficheiro de parâmetro de local de Olá e adicionar outro inline valores durante a implementação. Se fornecer valores para um parâmetro num ficheiro de parâmetro de local de Olá e inline, o valor de inline Olá tem precedência.

No entanto, quando utiliza um ficheiro de parâmetros externos, não poder passar outros valores ou inline ou a partir de um ficheiro local. Quando especificar um ficheiro de parâmetros no Olá **TemplateParameterUri** parâmetro, inline todos os parâmetros são ignorados. Fornece todos os valores de parâmetros no ficheiro externo Olá. Se o seu modelo incluir um valor confidencial que não pode incluir no ficheiro de parâmetros de Olá, adicione o Cofre de chaves de tooa esse valor ou fornecer dinamicamente a todas as inline de valores de parâmetro.

Se o seu modelo inclui um parâmetro com o mesmo nome como um dos parâmetros Olá Olá comando do PowerShell de Olá, PowerShell apresenta o parâmetro de Olá a partir do seu modelo com o sufixo de Olá **FromTemplate**. Por exemplo, um parâmetro com o nome **ResourceGroupName** no seu conflitos de modelo com Olá **ResourceGroupName** parâmetro Olá [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet. São tooprovide pedido um valor para **ResourceGroupNameFromTemplate**. Em geral, deve evitar este confusão ao nomear não parâmetros com Olá mesmo nome como parâmetros utilizada para operações de implementação.

## <a name="test-a-template-deployment"></a>Testar um modelo de implementação

Utilize os valores de parâmetros de modelo e sem a implementar, na verdade, quaisquer recursos, de tootest [teste-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Se forem detetados sem erros, o comando de Olá terminar sem uma resposta. Se for detetado um erro, o comando de Olá devolve uma mensagem de erro. Por exemplo, se tentar toopass um valor incorreto para a conta de armazenamento Olá SKU, devolve Olá seguinte erro:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Se o seu modelo tem um erro de sintaxe, o comando de Olá devolve um erro que indica que não foi possível analisar o modelo de Olá. mensagem de saudação indica o número de linha de Olá e posição de Olá erro de análise.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

modo de toouse concluída, utilize Olá `Mode` parâmetro:

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a>Modelo de exemplo

Olá seguinte modelo é utilizado para obter exemplos de Olá neste tópico. Copie e guarde-o como um ficheiro denominado storage.json. toounderstand como toocreate este modelo, consulte [criar o primeiro modelo Azure Resource Manager](resource-manager-create-first-template.md).  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>Passos seguintes
* Exemplos de Olá neste artigo implementar o grupo de recursos de tooa recursos na sua subscrição predefinida. toouse uma subscrição diferente, consulte [gerir várias subscrições do Azure](/powershell/azure/manage-subscriptions-azureps).
* Para um script de exemplo completo que implementa um modelo, consulte [script de implementação de modelos do Resource Manager](resource-manager-samples-powershell-deploy.md).
* toounderstand como toodefine parâmetros no modelo, consulte [compreender a sintaxe de modelos Azure Resource Manager e estrutura Olá](resource-group-authoring-templates.md).
* Para sugestões sobre como resolver erros comuns de implementação, consulte [resolver erros comuns de implementação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Para obter informações sobre a implementação de um modelo que necessita de um token SAS, consulte [implementar a modelo privado com o SAS token](resource-manager-powershell-sas-token.md).
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

