---
title: Segredo do Cofre de chaves com o modelo Azure Resource Manager | Microsoft Docs
description: "Mostra como passar um segredo a partir de um cofre de chaves como um parâmetro durante a implementação."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/30/2017
ms.author: tomfitz
ms.openlocfilehash: 7e02bd9c6130ef8b120282fafa9f0ee517890d0d
ms.sourcegitcommit: be0d1aaed5c0bbd9224e2011165c5515bfa8306c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="use-azure-key-vault-to-pass-secure-parameter-value-during-deployment"></a>Utilizar o Cofre de chaves do Azure para passar o valor do parâmetro seguro durante a implementação

Quando precisar de transferir um valor seguro (como uma palavra-passe) como um parâmetro durante a implementação, pode obter o valor de um [Cofre de chaves do Azure](../key-vault/key-vault-whatis.md). Obter o valor ao consultar o Cofre de chaves e um segredo no seu ficheiro de parâmetros. O valor nunca está exposto porque tem só fazem referência a um ID de Cofre de chaves. Não é necessário introduzir manualmente o valor para o segredo sempre que implementar os recursos. O Cofre da chave pode existir numa subscrição diferente do grupo de recursos que está a implementar. Quando referenciar o Cofre de chaves, incluem o ID da subscrição.

Quando criar o Cofre de chaves, defina o *enabledForTemplateDeployment* propriedade *verdadeiro*. Por definição deste valor como VERDADEIRO, é permitir o acesso a partir de modelos do Resource Manager durante a implementação.

## <a name="deploy-a-key-vault-and-secret"></a>Implementar um cofre de chaves e um segredo

Para criar um cofre de chaves e o segredo, utilize o CLI do Azure ou o PowerShell. Tenha em atenção que o Cofre de chaves está ativado para implementação do modelo. 

Para a CLI do Azure, utilize:

```azurecli-interactive
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create \
  --name $vaultname \
  --resource-group examplegroup \
  --location 'South Central US' \
  --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

Para o PowerShell, utilize:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault `
  -VaultName $vaultname `
  -ResourceGroupName examplegroup `
  -Location "South Central US" `
  -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-to-the-secret"></a>Ativar o acesso para o segredo

Se estiver a utilizar um cofre de chaves novo ou existente, certifique-se de que o utilizador a implementar o modelo possa aceder o segredo. O utilizador ao implementar um modelo que referencia um segredo tem de ter o `Microsoft.KeyVault/vaults/deploy/action` permissão para o Cofre de chaves. O [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) e [contribuinte](../active-directory/role-based-access-built-in-roles.md#contributor) funções ambos os conceder o acesso.

## <a name="reference-a-secret-with-static-id"></a>Referenciar um segredo com o ID estático

O modelo que recebe um segredo do Cofre de chaves é como qualquer modelo. Isto acontece porque **referenciar o Cofre de chaves no ficheiro de parâmetros, não o modelo.** A imagem seguinte mostra como o ficheiro de parâmetros referencia o segredo e transfere esse valor para o modelo.

![ID estático](./media/resource-manager-keyvault-parameter/statickeyvault.png)

Por exemplo, o [seguintes modelo](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/keyvaultparameter/sqlserver.json) implementa uma base de dados do SQL Server que inclui uma palavra-passe de administrador. O parâmetro de palavra-passe está definido como uma cadeia segura. No entanto, o modelo não especifica onde vêm esse valor.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminLogin": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    },
    "sqlServerName": {
      "type": "string"
    }
  },
  "resources": [
    {
      "name": "[parameters('sqlServerName')]",
      "type": "Microsoft.Sql/servers",
      "apiVersion": "2015-05-01-preview",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
        "administratorLogin": "[parameters('adminLogin')]",
        "administratorLoginPassword": "[parameters('adminPassword')]",
        "version": "12.0"
      }
    }
  ],
  "outputs": {
  }
}
```

Agora, crie um ficheiro de parâmetros para o modelo anterior. No ficheiro de parâmetros, especifique um parâmetro que corresponda ao nome do parâmetro no modelo. Para o valor do parâmetro, consulte o segredo do Cofre de chaves. Referenciar o segredo transferindo o identificador de recurso do Cofre de chaves e o nome do segredo. No [seguinte ficheiro de parâmetros](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/keyvaultparameter/sqlserver.parameters.json), o segredo do Cofre de chaves tem de existir e fornecer um valor estático para o ID de recurso. Copie este ficheiro localmente e definir o ID de subscrição, o nome do cofre e o nome do SQL Server.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminLogin": {
            "value": "exampleadmin"
        },
        "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/<subscription-id>/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/<vault-name>"
              },
              "secretName": "examplesecret"
            }
        },
        "sqlServerName": {
            "value": "<your-server-name>"
        }
    }
}
```

Agora, implemente o modelo e passar o ficheiro de parâmetros. Pode utilizar o modelo de exemplo a partir do GitHub, mas tem de utilizar um ficheiro de parâmetros local com os valores definidos para o seu ambiente.

Para a CLI do Azure, utilize:

```azurecli-interactive
az group create --name datagroup --location "South Central US"
az group deployment create \
    --name exampledeployment \
    --resource-group datagroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/keyvaultparameter/sqlserver.json \
    --parameters @sqlserver.parameters.json
```

Para o PowerShell, utilize:

```powershell
New-AzureRmResourceGroup -Name datagroup -Location "South Central US"
New-AzureRmResourceGroupDeployment `
  -Name exampledeployment `
  -ResourceGroupName datagroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/keyvaultparameter/sqlserver.json `
  -TemplateParameterFile sqlserver.parameters.json
```

## <a name="reference-a-secret-with-dynamic-id"></a>Referenciar um segredo com o dynamic ID

A secção anterior mostrou como transmitir um ID de recurso estático para o segredo do Cofre de chaves. No entanto, em alguns cenários, tem de referenciar um segredo do Cofre de chaves que varia com base na implementação atual. Nesse caso, não é possível codificar o ID de recurso no ficheiro de parâmetros. Infelizmente, dinamicamente não é possível gerar o ID de recurso no ficheiro de parâmetros porque expressões de modelo não são permitidas no ficheiro de parâmetros.

Para gerar dinamicamente o ID de recurso para um segredo do Cofre de chaves, terá de mover os recursos que tem o segredo a um modelo de ligado. No modelo principal, adicione o modelo ligado e transmitir um parâmetro que contém o ID de recurso gerado dinamicamente. A imagem seguinte mostra como um parâmetro no modelo ligado referencia o segredo.

![Dynamic ID](./media/resource-manager-keyvault-parameter/dynamickeyvault.png)

O modelo ligado tem de estar disponível através de um URI externo. Normalmente, adicione o seu modelo para uma conta de armazenamento e aceder através do URI, como `https://<storage-name>.blob.core.windows.net/templatecontainer/sqlserver.json`.

O [seguintes modelo](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/keyvaultparameter/sqlserver-dynamic-id.json) dinamicamente cria o ID de Cofre de chaves e passa-o como um parâmetro. -Contém ligações para um [modelo de exemplo](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/keyvaultparameter/sqlserver.json) no GitHub.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "vaultResourceGroup": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      },
      "adminLogin": {
        "type": "string"
      },
      "sqlServerName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/keyvaultparameter/sqlserver.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[resourceId(subscription().subscriptionId,  parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          },
          "adminLogin": { "value": "[parameters('adminLogin')]" },
          "sqlServerName": {"value": "[parameters('sqlServerName')]"}
        }
      }
    }],
    "outputs": {}
}
```

Implementar o modelo anterior e forneça valores para os parâmetros. Pode utilizar o modelo de exemplo a partir do GitHub, mas tem de fornecer valores de parâmetro para o seu ambiente.

Para a CLI do Azure, utilize:

```azurecli-interactive
az group create --name datagroup --location "South Central US"
az group deployment create \
    --name exampledeployment \
    --resource-group datagroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/keyvaultparameter/sqlserver-dynamic-id.json \
    --parameters vaultName=<your-vault> vaultResourceGroup=examplegroup secretName=examplesecret adminLogin=exampleadmin sqlServerName=<server-name>
```

Para o PowerShell, utilize:

```powershell
New-AzureRmResourceGroup -Name datagroup -Location "South Central US"
New-AzureRmResourceGroupDeployment `
  -Name exampledeployment `
  -ResourceGroupName datagroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/keyvaultparameter/sqlserver-dynamic-id.json `
  -vaultName <your-vault> -vaultResourceGroup examplegroup -secretName examplesecret -adminLogin exampleadmin -sqlServerName <server-name>
```

## <a name="next-steps"></a>Passos seguintes
* Para obter informações gerais sobre cofres de chaves, consulte [introdução ao Cofre de chaves do Azure](../key-vault/key-vault-get-started.md).
* Para obter exemplos completos de referenciar chaves segredos, consulte [exemplos do Cofre de chaves](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
