---
title: "Recursos do Azure para impedir que as alterações de bloqueio | Microsoft Docs"
description: "Impedir que utilizadores atualizar ou eliminar os recursos do Azure críticos aplicando um bloqueio para todos os utilizadores e funções."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/03/2018
ms.author: tomfitz
ms.openlocfilehash: e25de0366126ceee988eb253b66d18c9b8b62e1f
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a>Recursos de bloqueio para impedir que as alterações inesperadas 

Como administrador, poderá ter de bloquear uma subscrição, grupo de recursos ou recursos para impedir que outros utilizadores na sua organização acidentalmente eliminem ou modificar a recursos críticos. Pode definir o bloqueio para **CanNotDelete** ou **ReadOnly**. 

* **CanNotDelete** significa que os utilizadores autorizados, podem ainda ler e modificar um recurso, mas não é possível eliminar o recurso. 
* **Só de leitura** significa que os utilizadores autorizados podem ler um recurso, mas não é possível eliminar ou atualizar o recurso. Aplicar esta bloqueio é semelhante ao restringir todos os utilizadores autorizados para as permissões concedidas à **leitor** função. 

## <a name="how-locks-are-applied"></a>Como os bloqueios são aplicados

Ao aplicar um bloqueio num âmbito principal, todos os recursos desse âmbito herdam o bloqueio do mesmo. Recursos mesmo que adicionar mais tarde herdam o bloqueio do principal. O bloqueio mais restritivo na herança tem precedência.

Ao contrário do controlo de acesso baseado em funções, utilize as bloqueios de gestão para aplicar uma restrição em todos os utilizadores e funções. Para saber mais sobre a definição de permissões de utilizadores e funções, consulte [controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-control-configure.md).

Bloqueios de Gestor de recursos são aplicadas apenas a operações acontecer na plane a gestão, que consiste em operações de envio para `https://management.azure.com`. Os bloqueios restringe como recursos executar as suas próprias funções. Alterações de recurso estão limitadas, mas as operações de recurso não estão restringidas. Por exemplo, um bloqueio de só de leitura de uma base de dados do SQL Server impede-o de eliminar ou modificar a base de dados, mas não o impede de criar, atualizar ou eliminar dados na base de dados. Transações de dados permitidas por essas operações não são enviadas para `https://management.azure.com`.

Aplicar **ReadOnly** pode originar resultados inesperados porque algumas operações que parecem como leitura operações, na verdade, necessitam de ações adicionais. Por exemplo, colocar uma **ReadOnly** bloqueio numa conta de armazenamento impede que todos os utilizadores listar as chaves. A lista de operação de chaves é processada através de um pedido POST porque as chaves devolvidas estão disponíveis para operações de escrita. Para obter outro exemplo, colocar uma **ReadOnly** bloqueio de um recurso de serviço de aplicações impede o Explorador de servidores do Visual Studio a apresentação de ficheiros para o recurso porque esse interação requer acesso de escrita.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Quem pode criar ou eliminar as bloqueios na sua organização
Para criar ou eliminar as bloqueios de gestão, tem de ter acesso a `Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações. Das funções incorporadas, apenas **proprietário** e **administrador de acesso de utilizador** concedidas essas ações.

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Modelo
O exemplo seguinte mostra um modelo que cria um plano do app service, um web site e um bloqueio no web site. O tipo de recurso do bloqueio é o tipo de recurso do recurso para bloquear e **/fornecedores/bloqueios**. O nome do bloqueio é criado pelo concatenar o nome de recurso com **/Microsoft.Authorization/** e o nome do bloqueio.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "hostingPlanName": {
            "type": "string"
        }
    },
    "variables": {
        "siteName": "[concat('ExampleSite', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "apiVersion": "2016-09-01",
            "type": "Microsoft.Web/serverfarms",
            "name": "[parameters('hostingPlanName')]",
            "location": "[resourceGroup().location]",
            "sku": {
                "tier": "Free",
                "name": "f1",
                "capacity": 0
            },
            "properties": {
                "targetWorkerCount": 1
            }
        },
        {
            "apiVersion": "2016-08-01",
            "name": "[variables('siteName')]",
            "type": "Microsoft.Web/sites",
            "location": "[resourceGroup().location]",
            "dependsOn": [
                "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
            ],
            "properties": {
                "serverFarmId": "[parameters('hostingPlanName')]"
            }
        },
        {
            "type": "Microsoft.Web/sites/providers/locks",
            "apiVersion": "2016-09-01",
            "name": "[concat(variables('siteName'), '/Microsoft.Authorization/siteLock')]",
            "dependsOn": [
                "[resourceId('Microsoft.Web/sites', variables('siteName'))]"
            ],
            "properties": {
                "level": "CanNotDelete",
                "notes": "Site should not be deleted."
            }
        }
    ]
}
```

Para implementar este modelo de exemplo com o PowerShell, utilize:

```powershell
New-AzureRmResourceGroup -Name sitegroup -Location southcentralus
New-AzureRmResourceGroupDeployment -ResourceGroupName sitegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/lock.json -hostingPlanName plan0103
```

Para implementar este modelo de exemplo com a CLI do Azure, utilize:

```azurecli
az group create --name sitegroup --location southcentralus
az group deployment create --resource-group sitegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/lock.json --parameters hostingPlanName=plan0103
```

## <a name="powershell"></a>PowerShell
Bloqueio tiver implementado recursos com o Azure PowerShell utilizando o [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.

Para bloquear um recurso, forneça o nome de recurso, o tipo de recurso e o nome do grupo de recursos.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite -ResourceName examplesite -ResourceType Microsoft.Web/sites -ResourceGroupName exampleresourcegroup
```

Para bloquear um grupo de recursos, forneça o nome do grupo de recursos.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete -ResourceGroupName exampleresourcegroup
```

Para obter informações sobre um bloqueio, utilize [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). Para obter todos os bloqueios na sua subscrição, utilize:

```powershell
Get-AzureRmResourceLock
```

Para obter todos os bloqueios para um recurso, utilize:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites -ResourceGroupName exampleresourcegroup
```

Para obter todos os bloqueios para um grupo de recursos, utilize:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Para eliminar um bloqueio, utilize:

```powershell
$lockId = (Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup -ResourceName examplesite -ResourceType Microsoft.Web/sites).LockId
Remove-AzureRmResourceLock -LockId $lockId
```

## <a name="azure-cli"></a>CLI do Azure

Bloqueio tiver implementado recursos com a CLI do Azure utilizando o [bloqueio az criar](/cli/azure/lock#create) comando.

Para bloquear um recurso, forneça o nome de recurso, o tipo de recurso e o nome do grupo de recursos.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete --resource-group exampleresourcegroup --resource-name examplesite --resource-type Microsoft.Web/sites
```

Para bloquear um grupo de recursos, forneça o nome do grupo de recursos.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete --resource-group exampleresourcegroup
```

Para obter informações sobre um bloqueio, utilize [lista de bloqueio az](/cli/azure/lock#list). Para obter todos os bloqueios na sua subscrição, utilize:

```azurecli
az lock list
```

Para obter todos os bloqueios para um recurso, utilize:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite --namespace Microsoft.Web --resource-type sites --parent ""
```

Para obter todos os bloqueios para um grupo de recursos, utilize:

```azurecli
az lock list --resource-group exampleresourcegroup
```

Para eliminar um bloqueio, utilize:

```azurecli
lockid=$(az lock show --name LockSite --resource-group exampleresourcegroup --resource-type Microsoft.Web/sites --resource-name examplesite --output tsv --query id)
az lock delete --ids $lockid
```

## <a name="rest-api"></a>API REST
Pode bloquear recursos implementados com o [API REST para bloqueios gestão](https://docs.microsoft.com/rest/api/resources/managementlocks). A API REST permite-lhe criar e eliminar as bloqueios e obter informações sobre as bloqueios existentes.

Para criar um bloqueio, execute:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

O âmbito pode ser uma subscrição, o grupo de recursos ou o recurso. O nome de bloqueio é que pretende para chamar o bloqueio. Para uma versão de api, utilize **2015-01-01**.

O pedido de incluir um objeto JSON que especifica as propriedades para o bloqueio.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Passos Seguintes
* Para saber mais sobre como organizar logicamente os recursos, consulte [utilizando etiquetas para organizar os recursos](resource-group-using-tags.md)
* Para alterar o grupo de recursos, um recurso reside no, consulte [mover recursos para o novo grupo de recursos](resource-group-move-resources.md)
* Pode aplicar restrições e convenções a sua subscrição com políticas personalizadas. Para obter mais informações, veja [What is Azure Policy?](../azure-policy/azure-policy-introduction.md) (O que é o Azure Policy?).
* Para obter documentação de orientação sobre como as empresas podem utilizar o Resource Manager para gerir subscrições de forma eficaz, consulte [Azure enterprise scaffold - prescriptive subscription governance (Andaime empresarial do Azure - governação de subscrições prescritivas)](resource-manager-subscription-governance.md).

