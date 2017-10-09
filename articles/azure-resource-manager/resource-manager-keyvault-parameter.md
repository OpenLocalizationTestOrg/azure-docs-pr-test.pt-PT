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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="4ddc6-103">Utilizar o valor de parâmetro segura de toopass do Cofre de chaves durante a implementação</span><span class="sxs-lookup"><span data-stu-id="4ddc6-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="4ddc6-104">Quando precisar de toopass um valor seguro (como uma palavra-passe) como um parâmetro durante a implementação, pode obter valor Olá um [Cofre de chaves do Azure](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ddc6-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="4ddc6-105">Obter o valor de Olá consultando o Cofre de chaves Olá e o segredo no seu ficheiro de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="4ddc6-106">valor de Olá nunca está exposta porque tem só fazem referência a um ID de Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="4ddc6-107">Não é necessário toomanually introduza Olá valor para o segredo de Olá sempre que implementar recursos Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="4ddc6-108">Pode existir Cofre de chaves Olá numa subscrição diferente ao grupo de recursos de Olá que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="4ddc6-109">Quando referenciar o Cofre de chaves Olá, incluir Olá ID da subscrição.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="4ddc6-110">Quando criar Cofre de chaves Olá, defina Olá *enabledForTemplateDeployment* propriedade demasiado*verdadeiro*.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="4ddc6-111">Ao definir este valor tootrue, é permitir o acesso a partir de modelos do Resource Manager durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="4ddc6-112">Implementar um cofre de chaves e um segredo</span><span class="sxs-lookup"><span data-stu-id="4ddc6-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="4ddc6-113">toocreate um cofre de chaves e o segredo, utilize o CLI do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="4ddc6-114">Tenha em atenção que Cofre de chaves Olá está ativada para a implementação do modelo.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="4ddc6-115">Para a CLI do Azure, utilize:</span><span class="sxs-lookup"><span data-stu-id="4ddc6-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="4ddc6-116">Para o PowerShell, utilize:</span><span class="sxs-lookup"><span data-stu-id="4ddc6-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="4ddc6-117">Ativar segredo toohello de acesso</span><span class="sxs-lookup"><span data-stu-id="4ddc6-117">Enable access toohello secret</span></span>

<span data-ttu-id="4ddc6-118">Se estiver a utilizar um cofre de chaves novo ou existente, certifique-se de que o utilizador Olá implementar a modelo Olá pode aceder segredo Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="4ddc6-119">implementar um modelo que referencia um segredo de utilizador de Olá tem de ter Olá `Microsoft.KeyVault/vaults/deploy/action` permissão para o Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="4ddc6-120">Olá [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) e [contribuinte](../active-directory/role-based-access-built-in-roles.md#contributor) funções ambos os conceder o acesso.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="4ddc6-121">Também pode criar um [função personalizada](../active-directory/role-based-access-control-custom-roles.md) que concede esta permissão e adicionar a função de toothat Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="4ddc6-122">Para obter informações sobre como adicionar uma função de tooa do utilizador, consulte [atribuir um utilizador tooadministrator funções no Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4ddc6-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="4ddc6-123">Referenciar um segredo com o ID estático</span><span class="sxs-lookup"><span data-stu-id="4ddc6-123">Reference a secret with static ID</span></span>

<span data-ttu-id="4ddc6-124">modelo de Olá que recebe um segredo do Cofre de chaves é como qualquer modelo.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="4ddc6-125">Isto acontece porque **referenciar o Cofre de chaves Olá no ficheiro de parâmetros de Olá, modelo de Olá não.**</span><span class="sxs-lookup"><span data-stu-id="4ddc6-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="4ddc6-126">Por exemplo, Olá seguir modelo implementa uma base de dados do SQL Server que inclui uma palavra-passe de administrador.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="4ddc6-127">parâmetro de palavra-passe de Olá está definido tooa de cadeia segura.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="4ddc6-128">No entanto, o modelo de Olá não especifica em que esse valor provém de.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="4ddc6-129">Agora, crie um ficheiro de parâmetros para Olá precedente modelo.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="4ddc6-130">No ficheiro de parâmetros de Olá, especifique um parâmetro que corresponda ao nome de Olá do parâmetro de Olá no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="4ddc6-131">Para o valor do parâmetro Olá, referência Olá segredo do Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="4ddc6-132">Referência segredo Olá transferindo o identificador de recurso de Olá do Cofre de chaves Olá e nome de Olá do segredo Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="4ddc6-133">No seguinte exemplo de Olá, segredo do Cofre de chaves de Olá já deve existir e é fornecer um valor estático para o ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="4ddc6-134">Referenciar um segredo com o dynamic ID</span><span class="sxs-lookup"><span data-stu-id="4ddc6-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="4ddc6-135">secção anterior Olá mostrou como toopass um ID de recurso estático para a chave de Olá cofre segredo.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="4ddc6-136">No entanto, alguns cenários, terá de tooreference um segredo do Cofre de chaves que varia com base na implementação atual Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="4ddc6-137">Nesse caso, não é possível codificar Olá ID de recurso no ficheiro de parâmetros de Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="4ddc6-138">Infelizmente, dinamicamente não é possível gerar o ID de recurso Olá no ficheiro de parâmetros de Olá porque expressões de modelo não são permitidas no ficheiro de parâmetros de Olá.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="4ddc6-139">toodynamically gerar Olá ID de recurso para um segredo do Cofre de chaves, tem de mover recursos Olá que tem o segredo de Olá a um modelo de aninhada.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="4ddc6-140">No modelo principal, adicione modelo aninhada Olá e transmitir um parâmetro que contém o ID de recurso Olá gerada dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="4ddc6-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4ddc6-141">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4ddc6-141">Next steps</span></span>
* <span data-ttu-id="4ddc6-142">Para obter informações gerais sobre cofres de chaves, consulte [introdução ao Cofre de chaves do Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4ddc6-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="4ddc6-143">Para obter exemplos completos de referenciar chaves segredos, consulte [exemplos do Cofre de chaves](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="4ddc6-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

