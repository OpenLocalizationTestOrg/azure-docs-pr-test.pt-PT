---
title: segredo do cofre aaaKey com o modelo do Resource Manager | Microsoft Docs
description: "Mostra como toopass um segredo de uma chave de cofre como um parâmetro durante a implementação."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Utilizar o valor de parâmetro segura de toopass do Cofre de chaves durante a implementação

Quando precisar de toopass um valor seguro (como uma palavra-passe) como um parâmetro durante a implementação, pode obter valor Olá um [Cofre de chaves do Azure](../key-vault/key-vault-whatis.md). Obter o valor de Olá consultando o Cofre de chaves Olá e o segredo no seu ficheiro de parâmetros. valor de Olá nunca está exposta porque tem só fazem referência a um ID de Cofre de chaves. Não é necessário toomanually introduza Olá valor para o segredo de Olá sempre que implementar recursos Olá. Pode existir Cofre de chaves Olá numa subscrição diferente ao grupo de recursos de Olá que estiver a implementar. Quando referenciar o Cofre de chaves Olá, incluir Olá ID da subscrição.

Quando criar Cofre de chaves Olá, defina Olá *enabledForTemplateDeployment* propriedade demasiado*verdadeiro*. Ao definir este valor tootrue, é permitir o acesso a partir de modelos do Resource Manager durante a implementação.  

## <a name="deploy-a-key-vault-and-secret"></a>Implementar um cofre de chaves e um segredo

toocreate um cofre de chaves e o segredo, utilize o CLI do Azure ou o PowerShell. Tenha em atenção que Cofre de chaves Olá está ativada para a implementação do modelo. 

Para a CLI do Azure, utilize:

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

Para o PowerShell, utilize:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Ativar segredo toohello de acesso

Se estiver a utilizar um cofre de chaves novo ou existente, certifique-se de que o utilizador Olá implementar a modelo Olá pode aceder segredo Olá. implementar um modelo que referencia um segredo de utilizador de Olá tem de ter Olá `Microsoft.KeyVault/vaults/deploy/action` permissão para o Cofre de chaves Olá. Olá [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) e [contribuinte](../active-directory/role-based-access-built-in-roles.md#contributor) funções ambos os conceder o acesso. Também pode criar um [função personalizada](../active-directory/role-based-access-control-custom-roles.md) que concede esta permissão e adicionar a função de toothat Olá utilizador. Para obter informações sobre como adicionar uma função de tooa do utilizador, consulte [atribuir um utilizador tooadministrator funções no Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Referenciar um segredo com o ID estático

modelo de Olá que recebe um segredo do Cofre de chaves é como qualquer modelo. Isto acontece porque **referenciar o Cofre de chaves Olá no ficheiro de parâmetros de Olá, modelo de Olá não.** Por exemplo, Olá seguir modelo implementa uma base de dados do SQL Server que inclui uma palavra-passe de administrador. parâmetro de palavra-passe de Olá está definido tooa de cadeia segura. No entanto, o modelo de Olá não especifica em que esse valor provém de.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

Agora, crie um ficheiro de parâmetros para Olá precedente modelo. No ficheiro de parâmetros de Olá, especifique um parâmetro que corresponda ao nome de Olá do parâmetro de Olá no modelo de Olá. Para o valor do parâmetro Olá, referência Olá segredo do Cofre de chaves Olá. Referência segredo Olá transferindo o identificador de recurso de Olá do Cofre de chaves Olá e nome de Olá do segredo Olá. No seguinte exemplo de Olá, segredo do Cofre de chaves de Olá já deve existir e é fornecer um valor estático para o ID de recurso.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>Referenciar um segredo com o dynamic ID

secção anterior Olá mostrou como toopass um ID de recurso estático para a chave de Olá cofre segredo. No entanto, alguns cenários, terá de tooreference um segredo do Cofre de chaves que varia com base na implementação atual Olá. Nesse caso, não é possível codificar Olá ID de recurso no ficheiro de parâmetros de Olá. Infelizmente, dinamicamente não é possível gerar o ID de recurso Olá no ficheiro de parâmetros de Olá porque expressões de modelo não são permitidas no ficheiro de parâmetros de Olá.

toodynamically gerar Olá ID de recurso para um segredo do Cofre de chaves, tem de mover recursos Olá que tem o segredo de Olá a um modelo de aninhada. No modelo principal, adicione modelo aninhada Olá e transmitir um parâmetro que contém o ID de recurso Olá gerada dinamicamente.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
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
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>Passos seguintes
* Para obter informações gerais sobre cofres de chaves, consulte [introdução ao Cofre de chaves do Azure](../key-vault/key-vault-get-started.md).
* Para obter exemplos completos de referenciar chaves segredos, consulte [exemplos do Cofre de chaves](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

