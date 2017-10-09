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
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="7e229-103">Bloquear recursos tooprevent alterações inesperadas</span><span class="sxs-lookup"><span data-stu-id="7e229-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="7e229-104">Como administrador, poderá ser necessário toolock uma subscrição, grupo de recursos ou recursos tooprevent outros utilizadores na sua organização acidentalmente eliminem ou modificar a recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="7e229-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="7e229-105">Pode definir o nível de bloqueio de Olá demasiado**CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="7e229-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="7e229-106">**CanNotDelete** significa que os utilizadores autorizados, podem ainda ler e modificar um recurso, mas não é possível eliminar o recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e229-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="7e229-107">**Só de leitura** significa que os utilizadores autorizados podem ler um recurso, mas não é possível eliminar ou atualizar o recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e229-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="7e229-108">Aplicar esta bloqueio é semelhante toorestricting autorizado todas as permissões de toohello de utilizadores concedidas pelo Olá **leitor** função.</span><span class="sxs-lookup"><span data-stu-id="7e229-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="7e229-109">Como os bloqueios são aplicados</span><span class="sxs-lookup"><span data-stu-id="7e229-109">How locks are applied</span></span>

<span data-ttu-id="7e229-110">Ao aplicar um bloqueio num âmbito principal, todos os recursos desse âmbito herdam Olá bloqueio mesmo.</span><span class="sxs-lookup"><span data-stu-id="7e229-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="7e229-111">Recursos mesmo que adicionar mais tarde herdam bloqueio Olá principal Olá.</span><span class="sxs-lookup"><span data-stu-id="7e229-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="7e229-112">bloqueio mais restritivo do Olá na herança Olá tem precedência.</span><span class="sxs-lookup"><span data-stu-id="7e229-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="7e229-113">Ao contrário do controlo de acesso baseado em funções, é possível utilizar gestão bloqueios tooapply uma restrição em todos os utilizadores e funções.</span><span class="sxs-lookup"><span data-stu-id="7e229-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="7e229-114">toolearn sobre como definir permissões para utilizadores e funções, consulte [controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7e229-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="7e229-115">Gestor de recursos bloqueios aplicam-se apenas toooperations acontecer na plane de gestão de Olá, que consiste em operações enviadas`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="7e229-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="7e229-116">bloqueios de Olá restringe como recursos executar as suas próprias funções.</span><span class="sxs-lookup"><span data-stu-id="7e229-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="7e229-117">Alterações de recurso estão limitadas, mas as operações de recurso não estão restringidas.</span><span class="sxs-lookup"><span data-stu-id="7e229-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="7e229-118">Por exemplo, um bloqueio de só de leitura de uma base de dados do SQL Server impede o eliminar ou modificar a base de dados de Olá, mas não o impede de criar, atualizar ou eliminar dados na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e229-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="7e229-119">Transações de dados permitidas por essas operações não são enviadas demasiado`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="7e229-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="7e229-120">Aplicar **ReadOnly** pode originar resultados toounexpected porque algumas operações que parecem como leitura operações, na verdade, necessitam de ações adicionais.</span><span class="sxs-lookup"><span data-stu-id="7e229-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="7e229-121">Por exemplo, colocar uma **ReadOnly** bloqueio numa conta de armazenamento impede que todos os utilizadores listar chaves de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e229-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="7e229-122">lista de Olá operação de chaves é processada através de um pedido POST porque Olá devolveu chaves estão disponíveis para operações de escrita.</span><span class="sxs-lookup"><span data-stu-id="7e229-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="7e229-123">Para obter outro exemplo, colocar uma **ReadOnly** bloqueio de um recurso de serviço de aplicações impede o Explorador de servidores do Visual Studio a apresentação de ficheiros para o recurso de Olá porque esse interação requer acesso de escrita.</span><span class="sxs-lookup"><span data-stu-id="7e229-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="7e229-124">Quem pode criar ou eliminar as bloqueios na sua organização</span><span class="sxs-lookup"><span data-stu-id="7e229-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="7e229-125">toocreate ou eliminar bloqueios de gestão, tem de ter acesso demasiado`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações.</span><span class="sxs-lookup"><span data-stu-id="7e229-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="7e229-126">De Olá funções incorporadas, apenas **proprietário** e **administrador de acesso de utilizador** concedidas essas ações.</span><span class="sxs-lookup"><span data-stu-id="7e229-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="7e229-127">Portal</span><span class="sxs-lookup"><span data-stu-id="7e229-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="7e229-128">Modelo</span><span class="sxs-lookup"><span data-stu-id="7e229-128">Template</span></span>
<span data-ttu-id="7e229-129">Olá exemplo seguinte mostra um modelo que cria um bloqueio numa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7e229-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="7e229-130">conta de armazenamento Olá em que tooapply bloqueio Olá é fornecido como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7e229-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="7e229-131">Olá nome de bloqueio de Olá é criado pelo concatenar nome de recurso Olá com **/Microsoft.Authorization/** e Olá neste caso, o nome de bloqueio de Olá, **myLock**.</span><span class="sxs-lookup"><span data-stu-id="7e229-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="7e229-132">tipo de Olá fornecido é o tipo de recurso de toohello específico.</span><span class="sxs-lookup"><span data-stu-id="7e229-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="7e229-133">Para armazenamento, defina Olá tipo too"Microsoft.Storage/storageaccounts/providers/locks".</span><span class="sxs-lookup"><span data-stu-id="7e229-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="7e229-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e229-134">PowerShell</span></span>
<span data-ttu-id="7e229-135">Bloqueio tiver implementado recursos com o Azure PowerShell utilizando Olá [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.</span><span class="sxs-lookup"><span data-stu-id="7e229-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="7e229-136">toolock um recurso, forneça Olá nome do recurso de Olá, o tipo de recurso e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7e229-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="7e229-137">toolock um grupo de recursos, forneça o nome de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7e229-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="7e229-138">tooget informações sobre um bloqueio, utilize [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="7e229-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="7e229-139">tooget todos os bloqueios de Olá na sua subscrição, utilize:</span><span class="sxs-lookup"><span data-stu-id="7e229-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="7e229-140">tooget todos os bloqueios de um recurso, utilize:</span><span class="sxs-lookup"><span data-stu-id="7e229-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="7e229-141">tooget todos os bloqueios para um grupo de recursos, utilize:</span><span class="sxs-lookup"><span data-stu-id="7e229-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="7e229-142">O Azure PowerShell fornece outros comandos de bloqueios de trabalho, tais como [AzureRmResourceLock conjunto](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate um bloqueio e [remover AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete um bloqueio.</span><span class="sxs-lookup"><span data-stu-id="7e229-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="7e229-143">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7e229-143">Azure CLI</span></span>

<span data-ttu-id="7e229-144">Bloqueio tiver implementado recursos com a CLI do Azure utilizando o Olá [bloqueio az criar](/cli/azure/lock#create) comando.</span><span class="sxs-lookup"><span data-stu-id="7e229-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="7e229-145">toolock um recurso, forneça Olá nome do recurso de Olá, o tipo de recurso e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7e229-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="7e229-146">toolock um grupo de recursos, forneça o nome de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7e229-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="7e229-147">tooget informações sobre um bloqueio, utilize [lista de bloqueio az](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="7e229-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="7e229-148">tooget todos os bloqueios de Olá na sua subscrição, utilize:</span><span class="sxs-lookup"><span data-stu-id="7e229-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="7e229-149">tooget todos os bloqueios de um recurso, utilize:</span><span class="sxs-lookup"><span data-stu-id="7e229-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="7e229-150">tooget todos os bloqueios para um grupo de recursos, utilize:</span><span class="sxs-lookup"><span data-stu-id="7e229-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="7e229-151">CLI do Azure fornece outros comandos para bloqueios de trabalho, tais como [atualização de bloqueio az](/cli/azure/lock#update) tooupdate um bloqueio e [bloqueio az eliminar](/cli/azure/lock#delete) toodelete um bloqueio.</span><span class="sxs-lookup"><span data-stu-id="7e229-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="7e229-152">API REST</span><span class="sxs-lookup"><span data-stu-id="7e229-152">REST API</span></span>
<span data-ttu-id="7e229-153">Pode bloquear recursos implementados com Olá [API REST para bloqueios gestão](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="7e229-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="7e229-154">Olá REST API permite-lhe toocreate elimina bloqueios e obter informações sobre as bloqueios existentes.</span><span class="sxs-lookup"><span data-stu-id="7e229-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="7e229-155">toocreate um bloqueio, execute:</span><span class="sxs-lookup"><span data-stu-id="7e229-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="7e229-156">âmbito de Olá pode ser uma subscrição, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="7e229-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="7e229-157">Olá nome de bloqueio é que pretende que o bloqueio de Olá toocall.</span><span class="sxs-lookup"><span data-stu-id="7e229-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="7e229-158">Para uma versão de api, utilize **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="7e229-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="7e229-159">No pedido de Olá, inclua um objeto JSON que especifica Olá propriedades para o bloqueio de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e229-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="7e229-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7e229-160">Next steps</span></span>
* <span data-ttu-id="7e229-161">Para obter mais informações sobre como trabalhar com as bloqueios de recursos, consulte [bloqueio baixo Your Azure recursos](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="7e229-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="7e229-162">toolearn sobre como organizar logicamente os recursos, consulte [utilizar etiquetas tooorganize os recursos](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="7e229-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="7e229-163">toochange reside de um recurso que grupo de recursos, consulte [grupo de recursos do mover recursos toonew](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="7e229-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="7e229-164">Pode aplicar restrições e convenções a sua subscrição com políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="7e229-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="7e229-165">Para obter mais informações, consulte [recursos toomanage de política de uso e controlar o acesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7e229-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="7e229-166">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="7e229-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

