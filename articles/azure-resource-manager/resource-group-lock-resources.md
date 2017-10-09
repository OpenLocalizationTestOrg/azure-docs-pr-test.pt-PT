---
title: "alterações de tooprevent aaaLock recursos do Azure | Microsoft Docs"
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Bloquear recursos tooprevent alterações inesperadas 
Como administrador, poderá ser necessário toolock uma subscrição, grupo de recursos ou recursos tooprevent outros utilizadores na sua organização acidentalmente eliminem ou modificar a recursos críticos. Pode definir o nível de bloqueio de Olá demasiado**CanNotDelete** ou **ReadOnly**. 

* **CanNotDelete** significa que os utilizadores autorizados, podem ainda ler e modificar um recurso, mas não é possível eliminar o recurso de Olá. 
* **Só de leitura** significa que os utilizadores autorizados podem ler um recurso, mas não é possível eliminar ou atualizar o recurso de Olá. Aplicar esta bloqueio é semelhante toorestricting autorizado todas as permissões de toohello de utilizadores concedidas pelo Olá **leitor** função. 

## <a name="how-locks-are-applied"></a>Como os bloqueios são aplicados

Ao aplicar um bloqueio num âmbito principal, todos os recursos desse âmbito herdam Olá bloqueio mesmo. Recursos mesmo que adicionar mais tarde herdam bloqueio Olá principal Olá. bloqueio mais restritivo do Olá na herança Olá tem precedência.

Ao contrário do controlo de acesso baseado em funções, é possível utilizar gestão bloqueios tooapply uma restrição em todos os utilizadores e funções. toolearn sobre como definir permissões para utilizadores e funções, consulte [controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-control-configure.md).

Gestor de recursos bloqueios aplicam-se apenas toooperations acontecer na plane de gestão de Olá, que consiste em operações enviadas`https://management.azure.com`. bloqueios de Olá restringe como recursos executar as suas próprias funções. Alterações de recurso estão limitadas, mas as operações de recurso não estão restringidas. Por exemplo, um bloqueio de só de leitura de uma base de dados do SQL Server impede o eliminar ou modificar a base de dados de Olá, mas não o impede de criar, atualizar ou eliminar dados na base de dados de Olá. Transações de dados permitidas por essas operações não são enviadas demasiado`https://management.azure.com`.

Aplicar **ReadOnly** pode originar resultados toounexpected porque algumas operações que parecem como leitura operações, na verdade, necessitam de ações adicionais. Por exemplo, colocar uma **ReadOnly** bloqueio numa conta de armazenamento impede que todos os utilizadores listar chaves de Olá. lista de Olá operação de chaves é processada através de um pedido POST porque Olá devolveu chaves estão disponíveis para operações de escrita. Para obter outro exemplo, colocar uma **ReadOnly** bloqueio de um recurso de serviço de aplicações impede o Explorador de servidores do Visual Studio a apresentação de ficheiros para o recurso de Olá porque esse interação requer acesso de escrita.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Quem pode criar ou eliminar as bloqueios na sua organização
toocreate ou eliminar bloqueios de gestão, tem de ter acesso demasiado`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações. De Olá funções incorporadas, apenas **proprietário** e **administrador de acesso de utilizador** concedidas essas ações.

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Modelo
Olá exemplo seguinte mostra um modelo que cria um bloqueio numa conta de armazenamento. conta de armazenamento Olá em que tooapply bloqueio Olá é fornecido como parâmetro. Olá nome de bloqueio de Olá é criado pelo concatenar nome de recurso Olá com **/Microsoft.Authorization/** e Olá neste caso, o nome de bloqueio de Olá, **myLock**.

tipo de Olá fornecido é o tipo de recurso de toohello específico. Para armazenamento, defina Olá tipo too"Microsoft.Storage/storageaccounts/providers/locks".

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
Bloqueio tiver implementado recursos com o Azure PowerShell utilizando Olá [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.

toolock um recurso, forneça Olá nome do recurso de Olá, o tipo de recurso e o nome do grupo de recursos.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

toolock um grupo de recursos, forneça o nome de Olá Olá do grupo de recursos.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

tooget informações sobre um bloqueio, utilize [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget todos os bloqueios de Olá na sua subscrição, utilize:

```powershell
Get-AzureRmResourceLock
```

tooget todos os bloqueios de um recurso, utilize:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget todos os bloqueios para um grupo de recursos, utilize:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

O Azure PowerShell fornece outros comandos de bloqueios de trabalho, tais como [AzureRmResourceLock conjunto](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate um bloqueio e [remover AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete um bloqueio.

## <a name="azure-cli"></a>CLI do Azure

Bloqueio tiver implementado recursos com a CLI do Azure utilizando o Olá [bloqueio az criar](/cli/azure/lock#create) comando.

toolock um recurso, forneça Olá nome do recurso de Olá, o tipo de recurso e o nome do grupo de recursos.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

toolock um grupo de recursos, forneça o nome de Olá Olá do grupo de recursos.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

tooget informações sobre um bloqueio, utilize [lista de bloqueio az](/cli/azure/lock#list). tooget todos os bloqueios de Olá na sua subscrição, utilize:

```azurecli
az lock list
```

tooget todos os bloqueios de um recurso, utilize:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget todos os bloqueios para um grupo de recursos, utilize:

```azurecli
az lock list --resource-group exampleresourcegroup
```

CLI do Azure fornece outros comandos para bloqueios de trabalho, tais como [atualização de bloqueio az](/cli/azure/lock#update) tooupdate um bloqueio e [bloqueio az eliminar](/cli/azure/lock#delete) toodelete um bloqueio.

## <a name="rest-api"></a>API REST
Pode bloquear recursos implementados com Olá [API REST para bloqueios gestão](https://docs.microsoft.com/rest/api/resources/managementlocks). Olá REST API permite-lhe toocreate elimina bloqueios e obter informações sobre as bloqueios existentes.

toocreate um bloqueio, execute:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso. Olá nome de bloqueio é que pretende que o bloqueio de Olá toocall. Para uma versão de api, utilize **2015-01-01**.

No pedido de Olá, inclua um objeto JSON que especifica Olá propriedades para o bloqueio de Olá.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Passos seguintes
* Para obter mais informações sobre como trabalhar com as bloqueios de recursos, consulte [bloqueio baixo Your Azure recursos](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* toolearn sobre como organizar logicamente os recursos, consulte [utilizar etiquetas tooorganize os recursos](resource-group-using-tags.md)
* toochange reside de um recurso que grupo de recursos, consulte [grupo de recursos do mover recursos toonew](resource-group-move-resources.md)
* Pode aplicar restrições e convenções a sua subscrição com políticas personalizadas. Para obter mais informações, consulte [recursos toomanage de política de uso e controlar o acesso](resource-manager-policy.md).
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

