---
title: "aaaManage Azure soluções com o PowerShell | Microsoft Docs"
description: Utilize o Azure PowerShell e do Resource Manager toomanage os recursos.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="aa95a-103">Gerir os recursos com o Azure PowerShell e do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="aa95a-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa95a-104">Portal</span><span class="sxs-lookup"><span data-stu-id="aa95a-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="aa95a-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aa95a-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="aa95a-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa95a-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="aa95a-107">API REST</span><span class="sxs-lookup"><span data-stu-id="aa95a-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="aa95a-108">Neste artigo, saiba como toomanage as suas soluções com o Azure PowerShell e o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aa95a-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="aa95a-109">Se não estiver familiarizado com o Resource Manager, consulte [descrição geral do Gestor de recursos](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="aa95a-110">Este tópico centra-se nas tarefas de gestão.</span><span class="sxs-lookup"><span data-stu-id="aa95a-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="aa95a-111">Irá:</span><span class="sxs-lookup"><span data-stu-id="aa95a-111">You will:</span></span>

1. <span data-ttu-id="aa95a-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="aa95a-112">Create a resource group</span></span>
2. <span data-ttu-id="aa95a-113">Adicionar um grupo de recursos de toohello de recursos</span><span class="sxs-lookup"><span data-stu-id="aa95a-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="aa95a-114">Adicione um recurso de toohello etiquetas</span><span class="sxs-lookup"><span data-stu-id="aa95a-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="aa95a-115">Recursos com base nos valores de etiqueta ou nomes de consulta</span><span class="sxs-lookup"><span data-stu-id="aa95a-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="aa95a-116">Aplicar e remover um bloqueio num recurso Olá</span><span class="sxs-lookup"><span data-stu-id="aa95a-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="aa95a-117">Eliminar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="aa95a-117">Delete a resource group</span></span>

<span data-ttu-id="aa95a-118">Este artigo não mostrar como toodeploy uma subscrição de tooyour de modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aa95a-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="aa95a-119">Para essas informações, consulte [implementar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="aa95a-120">Introdução ao Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa95a-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="aa95a-121">Se não tiver instalado o Azure PowerShell, consulte o artigo [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aa95a-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="aa95a-122">Se tiver instalado o Azure PowerShell no passado Olá, mas não tiver atualizado-recentemente, considere instalar a versão mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="aa95a-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="aa95a-123">Pode atualizar a versão de Olá através de Olá mesmo método que utilizou tooinstall-lo.</span><span class="sxs-lookup"><span data-stu-id="aa95a-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="aa95a-124">Por exemplo, se utilizou Olá instalador de plataforma Web, inicie-o novamente e procurar por uma atualização.</span><span class="sxs-lookup"><span data-stu-id="aa95a-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="aa95a-125">utilizar a versão do Olá módulo de recursos do Azure, de toocheck Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="aa95a-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="aa95a-126">Este tópico foi atualizado para a versão 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="aa95a-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="aa95a-127">Se tiver uma versão anterior, sua experiência pode não corresponder aos passos de Olá apresentados neste tópico.</span><span class="sxs-lookup"><span data-stu-id="aa95a-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="aa95a-128">Para obter documentação sobre cmdlets Olá nesta versão, consulte [AzureRM.Resources módulo](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="aa95a-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="aa95a-129">Inicie sessão no tooyour a conta do Azure</span><span class="sxs-lookup"><span data-stu-id="aa95a-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="aa95a-130">Antes de trabalhar na sua solução, tem de iniciar sessão na conta tooyour.</span><span class="sxs-lookup"><span data-stu-id="aa95a-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="aa95a-131">toolog no tooyour conta do Azure, utilize Olá **Login-AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa95a-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="aa95a-132">Olá pede-lhe as credenciais de início de sessão de Olá para a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa95a-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="aa95a-133">Após iniciar sessão, transfere as definições de conta para que estejam disponível tooAzure do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa95a-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="aa95a-134">Olá cmdlet devolve informações sobre o toouse de subscrição de conta e Olá para tarefas de Olá.</span><span class="sxs-lookup"><span data-stu-id="aa95a-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="aa95a-135">Se tiver mais do que uma subscrição, pode alternar tooa uma subscrição diferente.</span><span class="sxs-lookup"><span data-stu-id="aa95a-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="aa95a-136">Em primeiro lugar, vamos ver todas as subscrições de Olá para a sua conta.</span><span class="sxs-lookup"><span data-stu-id="aa95a-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="aa95a-137">Devolve ativados e desativados subscrições.</span><span class="sxs-lookup"><span data-stu-id="aa95a-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="aa95a-138">tooswitch tooa uma subscrição diferente, forneça o nome da subscrição Olá com Olá **Set-AzureRmContext** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa95a-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="aa95a-139">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="aa95a-139">Create a resource group</span></span>
<span data-ttu-id="aa95a-140">Antes de implementar qualquer subscrição tooyour de recursos, tem de criar um grupo de recursos que irá conter recursos Olá.</span><span class="sxs-lookup"><span data-stu-id="aa95a-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="aa95a-141">toocreate um grupo de recursos, utilize Olá **New-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa95a-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="aa95a-142">comando de Olá utiliza Olá **nome** parâmetro toospecify um nome para o grupo de recursos de Olá e Olá **localização** parâmetro toospecify respetiva localização.</span><span class="sxs-lookup"><span data-stu-id="aa95a-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="aa95a-143">saída de Olá consta Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="aa95a-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="aa95a-144">Se precisar de grupo de recursos de Olá tooretrieve mais tarde, utilize Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="aa95a-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="aa95a-145">tooget Olá todos os grupos de recursos na sua subscrição, não especifique um nome de:</span><span class="sxs-lookup"><span data-stu-id="aa95a-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="aa95a-146">Adicionar grupo de recursos de tooa de recursos</span><span class="sxs-lookup"><span data-stu-id="aa95a-146">Add resources tooa resource group</span></span>
<span data-ttu-id="aa95a-147">um grupo de recursos do recurso toohello tooadd, pode utilizar Olá **New-AzureRmResource** cmdlet ou um cmdlet que faz toohello específico de tipo de recurso que está a criar (como **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="aa95a-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="aa95a-148">Poderá achar mais fácil toouse um cmdlet que é o tipo de recurso específico tooa pois inclui os parâmetros para propriedades de Olá que são necessárias para o recurso novo Olá.</span><span class="sxs-lookup"><span data-stu-id="aa95a-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="aa95a-149">toouse **New-AzureRmResource**, tem de conhecer todos os tooset de propriedades de Olá sem pedidos para os mesmos.</span><span class="sxs-lookup"><span data-stu-id="aa95a-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="aa95a-150">No entanto, a adição de um recurso através de cmdlets poderá causar confusão futura porque o recurso novo Olá não existe um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aa95a-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="aa95a-151">A Microsoft recomenda que define a infraestrutura de Olá para a sua solução do Azure num modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aa95a-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="aa95a-152">Modelos permitem-lhe tooreliably e implementar repetidamente a solução.</span><span class="sxs-lookup"><span data-stu-id="aa95a-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="aa95a-153">Para este tópico, criar uma conta de armazenamento com um cmdlet do PowerShell, mas mais tarde gerar um modelo do seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aa95a-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="aa95a-154">Olá seguinte cmdlet cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="aa95a-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="aa95a-155">Em vez de utilizar o nome de Olá mostrado no exemplo de Olá, forneça um nome exclusivo para a conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="aa95a-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="aa95a-156">nome de Olá tem de ter entre 3 e 24 carateres de comprimento e utilizar apenas números e letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="aa95a-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="aa95a-157">Se utilizar o nome de Olá mostrado no exemplo Olá, receberá um erro porque este nome já se encontra em utilização.</span><span class="sxs-lookup"><span data-stu-id="aa95a-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="aa95a-158">Se precisar de tooretrieve este recurso mais tarde, utilize Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="aa95a-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="aa95a-159">Adicionar uma etiqueta</span><span class="sxs-lookup"><span data-stu-id="aa95a-159">Add a tag</span></span>

<span data-ttu-id="aa95a-160">As etiquetas permitem-lhe tooorganize os recursos de acordo com as propriedades de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="aa95a-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="aa95a-161">Por exemplo, pode ter vários recursos em grupos de recursos diferente que pertencem toohello mesmo departamento.</span><span class="sxs-lookup"><span data-stu-id="aa95a-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="aa95a-162">Pode aplicar um departamento etiqueta e o valor toothose recursos toomark-las como pertencentes toohello mesma categoria.</span><span class="sxs-lookup"><span data-stu-id="aa95a-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="aa95a-163">Em alternativa, pode marcá-se um recurso é utilizado num ambiente de teste ou de produção.</span><span class="sxs-lookup"><span data-stu-id="aa95a-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="aa95a-164">Neste tópico aplicam-se as etiquetas tooonly um recurso, mas no seu ambiente provavelmente faz sentido tooapply etiquetas tooall os recursos.</span><span class="sxs-lookup"><span data-stu-id="aa95a-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="aa95a-165">Olá seguintes cmdlet aplica-se a conta de armazenamento de tooyour etiquetas duas:</span><span class="sxs-lookup"><span data-stu-id="aa95a-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="aa95a-166">As etiquetas são atualizadas como um único objeto.</span><span class="sxs-lookup"><span data-stu-id="aa95a-166">Tags are updated as a single object.</span></span> <span data-ttu-id="aa95a-167">tooadd um recurso de tooa etiquetas que já inclua etiquetas, obtenha primeiro etiquetas existente Olá.</span><span class="sxs-lookup"><span data-stu-id="aa95a-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="aa95a-168">Adicione Olá nova etiqueta toohello objeto que contém etiquetas existente Olá e voltar a todos os recursos de toohello de etiquetas de Olá.</span><span class="sxs-lookup"><span data-stu-id="aa95a-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="aa95a-169">Procurar recursos</span><span class="sxs-lookup"><span data-stu-id="aa95a-169">Search for resources</span></span>

<span data-ttu-id="aa95a-170">Olá utilize **localizar AzureRmResource** cmdlet tooretrieve recursos para condições de pesquisa diferentes.</span><span class="sxs-lookup"><span data-stu-id="aa95a-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="aa95a-171">tooget um recurso de por nome, fornecer Olá **ResourceNameContains** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="aa95a-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="aa95a-172">tooget todos os recursos de Olá num grupo de recursos, fornecer Olá **ResourceGroupNameContains** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="aa95a-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="aa95a-173">tooget todos os recursos de Olá com um nome de tag e um valor, fornecer Olá **TagName** e **TagValue** parâmetros:</span><span class="sxs-lookup"><span data-stu-id="aa95a-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="aa95a-174">recursos de Olá tooall com um tipo de recurso específico, fornecer Olá **ResourceType** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="aa95a-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="aa95a-175">Um recurso de bloqueio</span><span class="sxs-lookup"><span data-stu-id="aa95a-175">Lock a resource</span></span>

<span data-ttu-id="aa95a-176">Quando precisar de toomake se um recurso crítico não acidentalmente eliminado ou modificado, aplicam-se um recurso de toohello de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="aa95a-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="aa95a-177">Pode especificar um um **CanNotDelete** ou **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="aa95a-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="aa95a-178">toocreate ou eliminar bloqueios de gestão, tem de ter acesso demasiado`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações.</span><span class="sxs-lookup"><span data-stu-id="aa95a-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="aa95a-179">Das funções incorporadas Olá, apenas o proprietário e o administrador de acesso de utilizador são concedidas essas ações.</span><span class="sxs-lookup"><span data-stu-id="aa95a-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="aa95a-180">tooapply um bloqueio, utilize Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="aa95a-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="aa95a-181">Olá recurso bloqueado no Olá anterior exemplo não pode ser eliminado até que o bloqueio de Olá é removido.</span><span class="sxs-lookup"><span data-stu-id="aa95a-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="aa95a-182">tooremove um bloqueio, utilize:</span><span class="sxs-lookup"><span data-stu-id="aa95a-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="aa95a-183">Para obter mais informações sobre as bloqueios de definição, consulte [bloquear recursos com o Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="aa95a-184">Remover recursos ou um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="aa95a-184">Remove resources or resource group</span></span>
<span data-ttu-id="aa95a-185">Pode remover um recurso ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aa95a-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="aa95a-186">Quando remove um grupo de recursos, tem também de remover todos os recursos de Olá nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aa95a-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="aa95a-187">toodelete um recurso do grupo de recursos de Olá, utilize Olá **remover AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa95a-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="aa95a-188">Este cmdlet elimina recursos Olá, mas não eliminar o grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="aa95a-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="aa95a-189">toodelete um grupo de recursos e os respetivos recursos, utilize Olá **Remove-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa95a-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="aa95a-190">Para ambos os cmdlets, é-lhe perguntado tooconfirm que pretende recursos de Olá tooremove ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aa95a-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="aa95a-191">Se a operação de Olá elimina com êxito recursos Olá ou grupo de recursos, devolve **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="aa95a-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="aa95a-192">Executar scripts de Gestor de recursos com a automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="aa95a-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="aa95a-193">Este tópico mostra como tooperform operações básicas nos seus recursos com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa95a-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="aa95a-194">Para cenários de gestão mais avançados, normalmente, pretende toocreate um script e reutilizar nesse script conforme necessário ou com base numa agenda.</span><span class="sxs-lookup"><span data-stu-id="aa95a-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="aa95a-195">[A automatização do Azure](../automation/automation-intro.md) fornece uma forma para os scripts de tooautomate utilizada frequentemente que gerem as suas soluções do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa95a-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="aa95a-196">Olá tópicos seguintes mostram como toouse da automatização do Azure, o Resource Manager e o PowerShell tooeffectively efetuam tarefas de gestão:</span><span class="sxs-lookup"><span data-stu-id="aa95a-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="aa95a-197">Para obter informações sobre como criar um runbook, consulte [o meu primeiro runbook do PowerShell](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="aa95a-198">Para obter informações sobre como trabalhar com galleries de scripts, consulte [galleries módulos e Runbooks de automatização do Azure](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="aa95a-199">Para os runbooks que iniciar e parar máquinas virtuais, consulte [cenário de automatização do Azure: toocreate etiquetas formatada em JSON utilizando uma agenda para a VM do Azure de arranque e encerramento](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="aa95a-200">Para os runbooks que iniciar e parar off-hours de máquinas virtuais, consulte [VMs de início/paragem durante a solução de off-hours na automatização](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa95a-201">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="aa95a-201">Next steps</span></span>
* <span data-ttu-id="aa95a-202">toolearn sobre a criação de modelos do Resource Manager, consulte [criação de modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="aa95a-203">toolearn sobre a implementação de modelos, consulte [implementar uma aplicação com o modelo do Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="aa95a-204">Pode mover recursos tooa novo grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="aa95a-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="aa95a-205">Para obter exemplos, consulte [mover recursos tooNew grupo de recursos ou subscrição](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="aa95a-206">Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="aa95a-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

