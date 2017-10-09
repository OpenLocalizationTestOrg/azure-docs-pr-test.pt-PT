---
ms.assetid: 
title: "Cofre da chave de aaaAzure - como toouse configuração soft-eliminar com o PowerShell"
description: "Utilizar os exemplos de cenários de eliminação de forma recuperável com recortes de código do PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="e4bd2-103">Como toouse Cofre de chaves configuração soft-eliminar com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4bd2-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="e4bd2-104">Funcionalidade de eliminação de forma recuperável do Azure do Cofre de chaves permite a recuperação de cofres eliminados e objetos do cofre.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="e4bd2-105">Especificamente, as Olá endereços de eliminação de forma recuperável os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="e4bd2-106">Suporte para eliminação recuperável de um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="e4bd2-107">Suporte para a eliminação de objetos do Cofre de chaves; recuperável chaves de segredos e, de certificados</span><span class="sxs-lookup"><span data-stu-id="e4bd2-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4bd2-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e4bd2-108">Prerequisites</span></span>

- <span data-ttu-id="e4bd2-109">O Azure PowerShell 4.0.0 ou posterior - se não tiver já nesta configuração, instalar o Azure PowerShell e associá-lo à sua subscrição do Azure, consulte o artigo [como tooinstall e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4bd2-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="e4bd2-110">Há uma versão desatualizada dos nossa saída do PowerShell do Cofre de chave formatação do ficheiro que **poderá** ser carregado para o seu ambiente, em vez da versão correta do Olá.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="e4bd2-111">Iremos são prevendo que uma versão atualizada do PowerShell toocontain Olá necessário correção para a saída de Olá formatação e vai actualizar este tópico nessa altura.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="e4bd2-112">Olá solução atual, deve ocorrer este problema formatação, é:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="e4bd2-113">Olá de utilização seguintes consulta se reparar em que não está a ver a eliminação de forma recuperável Olá ativada propriedade descrita neste tópico: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="e4bd2-114">Para informações de refernece específico do Cofre de chaves para o PowerShell, consulte [referência do PowerShell do Cofre de chaves do Azure](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="e4bd2-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="e4bd2-115">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="e4bd2-115">Required permissions</span></span>

<span data-ttu-id="e4bd2-116">Operações do Cofre de chaves separadamente geridas através de permissões de controlo (RBAC) de acesso baseado em funções da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="e4bd2-117">Operação</span><span class="sxs-lookup"><span data-stu-id="e4bd2-117">Operation</span></span> | <span data-ttu-id="e4bd2-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="e4bd2-118">Description</span></span> | <span data-ttu-id="e4bd2-119">Permissão de utilizador</span><span class="sxs-lookup"><span data-stu-id="e4bd2-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="e4bd2-120">Lista</span><span class="sxs-lookup"><span data-stu-id="e4bd2-120">List</span></span>|<span data-ttu-id="e4bd2-121">Apresenta uma lista de eliminados cofres de chaves.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="e4bd2-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="e4bd2-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="e4bd2-123">Recuperar</span><span class="sxs-lookup"><span data-stu-id="e4bd2-123">Recover</span></span>|<span data-ttu-id="e4bd2-124">Restaura um cofre de chaves foi eliminado.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="e4bd2-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="e4bd2-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="e4bd2-126">Remover</span><span class="sxs-lookup"><span data-stu-id="e4bd2-126">Purge</span></span>|<span data-ttu-id="e4bd2-127">Remove permanentemente um cofre de chaves eliminado e todo o respetivo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="e4bd2-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="e4bd2-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="e4bd2-129">Para obter mais informações sobre o controlo de acesso e permissões, consulte [proteger o seu Cofre de chaves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e4bd2-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="e4bd2-130">Ativar a eliminação de forma recuperável</span><span class="sxs-lookup"><span data-stu-id="e4bd2-130">Enabling soft-delete</span></span>

<span data-ttu-id="e4bd2-131">toorecover capaz de toobe um cofre de chaves eliminado ou objetos armazenados numa chave de cofre, primeiro é necessário ativar a eliminação de forma recuperável para esse cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="e4bd2-132">Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-132">Existing key vault</span></span>

<span data-ttu-id="e4bd2-133">Para um cofre de chaves com o nome ContosoVault, ative a eliminação de forma recuperável da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="e4bd2-134">Atualmente terá toouse Olá de escrita do Azure Resource Manager recursos manipulação toodirectly *enableSoftDelete* propriedade toohello recurso do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="e4bd2-135">Novo cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-135">New key vault</span></span>

<span data-ttu-id="e4bd2-136">Ativar a eliminação de forma recuperável para um novo cofre de chaves é efetuada no momento da criação, adicionando o sinalizador de ativação de eliminação de forma recuperável do Olá tooyour criar comando.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="e4bd2-137">Certifique-se a ativação da eliminação de forma recuperável</span><span class="sxs-lookup"><span data-stu-id="e4bd2-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="e4bd2-138">um cofre de chaves com eliminação de forma recuperável ativada, tooverify Olá execução *obter* de comandos e procure Olá "Recuperável eliminar Enabled?"</span><span class="sxs-lookup"><span data-stu-id="e4bd2-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="e4bd2-139">atributo e a respetiva definição, true ou false.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="e4bd2-140">Eliminar um cofre de chaves protegido por eliminar de forma recuperável</span><span class="sxs-lookup"><span data-stu-id="e4bd2-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="e4bd2-141">Olá comando toodelete (ou remover) um cofre de chaves permanece Olá mesmo, mas as alterações do mesmo comportamento, dependendo se ativou a configuração soft-eliminar ou não.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="e4bd2-142">Se executar o comando anterior do Olá para um cofre de chaves que não tenha ativada de eliminação de forma recuperável, irá eliminar permanentemente este Cofre de chaves e todo o respetivo conteúdo sem quaisquer opções de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="e4bd2-143">Como eliminar de forma recuperável protege os seus cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="e4bd2-144">Com a eliminação de forma recuperável ativada:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="e4bd2-145">Quando é eliminado um cofre de chaves, é removido do respetivo grupo de recursos e colocada num espaço de nomes reservado que só está associado à localização de olá onde foi criado.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="e4bd2-146">Objetos de uma chave eliminado cofre, tal como chaves, os segredos e certificados, não estão acessíveis e permanecem, enquanto as respetivas Cofre de chaves que contêm está no estado de Olá eliminado.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="e4bd2-147">nome DNS de Olá para um cofre de chaves num Estado eliminado está ainda reservado, portanto, não é possível criar um novo cofre de chaves com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="e4bd2-148">Pode ver os cofres de chaves de estado eliminado, associados à subscrição, utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

<span data-ttu-id="e4bd2-149">Olá *ID de recurso* Olá saída refere-se toohello ID de recurso original de neste cofre.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="e4bd2-150">Uma vez que este Cofre de chaves agora num Estado eliminado, nenhum recurso existe com esse ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="e4bd2-151">Olá *Id* campo pode ser utilizado tooidentify Olá recurso quando recuperar ou remoção.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="e4bd2-152">Olá *data de remoção agendada* campo indica quando o Cofre de Olá serão permanentemente eliminado (removidos) se foi efetuada nenhuma ação para este cofre foi eliminado.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="e4bd2-153">Olá de toocalculate período, utilizada de retenção de predefinição Olá *data de remoção agendada*, é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="e4bd2-154">Recuperar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-154">Recovering a key vault</span></span>

<span data-ttu-id="e4bd2-155">toorecover um cofre de chaves, terá de nome de Cofre de chaves toospecify Olá, grupo de recursos e localização.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="e4bd2-156">Tenha em atenção Olá localização e o grupo de recursos de Olá do Cofre de chaves Olá eliminado conforme necessário estes para um processo de recuperação do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="e4bd2-157">Quando um cofre de chaves é recuperado, o resultado de Olá é um novo recurso com o ID de recurso original Olá do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="e4bd2-158">Se tiver sido removido o grupo de recursos de olá onde o Cofre de chaves Olá existia, um novo grupo de recursos com o mesmo nome tem de ser criado para que o Cofre de chaves Olá pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="e4bd2-159">Objetos do Cofre de chaves e eliminação de forma recuperável</span><span class="sxs-lookup"><span data-stu-id="e4bd2-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="e4bd2-160">Para uma chave, 'ContosoFirstKey', num cofre de chaves com o nome 'ContosoVault' com eliminação de forma recuperável ativada, aqui forma como deveria eliminá essa chave.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="e4bd2-161">Com o seu Cofre de chaves ativado para eliminação de forma recuperável, uma chave eliminada continua a aparecer como é eliminado, exceto, ao listar explicitamente ou obter chaves eliminadas.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="e4bd2-162">A maioria das operações numa chave no estado de Olá eliminado irão falhar, exceto para listar uma chave eliminada, recuperação ou remoção-lo.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="e4bd2-163">Por exemplo, chaves de toolist eliminado toorequest no Cofre de chaves, utilizar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="e4bd2-164">Estado de transição</span><span class="sxs-lookup"><span data-stu-id="e4bd2-164">Transition state</span></span> 

<span data-ttu-id="e4bd2-165">Quando elimina uma chave de um cofre de chaves com eliminação de forma recuperável ativada, poderá demorar alguns segundos para Olá toocomplete de transição.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="e4bd2-166">Durante este estado de transição, pode aparecer que essa chave Olá não se encontra no Estado ativa Olá ou Olá eliminado.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="e4bd2-167">Este comando irá listar todas as chaves eliminadas no seu Cofre de chaves com o nome 'ContosoVault'.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="e4bd2-168">Utilizar a eliminação de forma recuperável com objetos de Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="e4bd2-169">Apenas como cofres de chaves, uma chave eliminada, segredo ou certificado permanecerá no Estado eliminado para cópia de segurança too90 dias, exceto se recuperar ou removê-lo.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="e4bd2-170">Chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-170">Keys</span></span>

<span data-ttu-id="e4bd2-171">toorecover uma chave de eliminados:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="e4bd2-172">toopermanently eliminar uma chave:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="e4bd2-173">Remover uma chave irá eliminá-la permanentemente, que significa que não serão recuperável.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="e4bd2-174">Olá **recuperar** e **remover** ações permissões os seus próprios associado a uma política de acesso do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="e4bd2-175">Para um tooexecute de capaz de principal toobe utilizador ou serviço um **recuperar** ou **remover** ação têm de ter permissão de respetivos Olá para esse objeto (chave ou segredo) na política de acesso do Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="e4bd2-176">Por predefinição, Olá **remover** permissão não é adicionar política de acesso de tooa do Cofre de chaves quando hello atalho 'tudo' toogrant utilizado todos os utilizadores de tooa de permissões.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="e4bd2-177">Tem de conceder explicitamente **remover** permissão.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="e4bd2-178">Por exemplo, Olá o seguinte comando concede user@contoso.com permissão tooperform várias operações de chaves no *ContosoVault* incluindo **remover**.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="e4bd2-179">Definir uma política de acesso do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="e4bd2-180">Se tiver um cofre de chaves que apenas tenha tido a eliminação de forma recuperável ativada, poderá não ter **recuperar** e **remover** permissões.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="e4bd2-181">Segredos</span><span class="sxs-lookup"><span data-stu-id="e4bd2-181">Secrets</span></span>

<span data-ttu-id="e4bd2-182">Como as chaves, os segredos no Cofre de chaves são manipulados com os seus próprios comandos.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="e4bd2-183">A seguir, são comandos Olá para eliminar, listar, recuperar e remover segredos.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="e4bd2-184">Elimine um segredo designado SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="e4bd2-185">Lista de eliminados todos os segredos no Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="e4bd2-186">Recupere um segredo no estado de Olá eliminado:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="e4bd2-187">Remover um segredo no estado de eliminação:</span><span class="sxs-lookup"><span data-stu-id="e4bd2-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="e4bd2-188">Remover um segredo irá eliminá-la permanentemente, que significa que não serão recuperável.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="e4bd2-189">Cofres de chaves e remoção</span><span class="sxs-lookup"><span data-stu-id="e4bd2-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="e4bd2-190">Objetos do Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="e4bd2-190">Key vault objects</span></span>

<span data-ttu-id="e4bd2-191">A remoção de uma chave de segredo ou certificado irá eliminá-la permanentemente, que significa que não serão recuperável.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="e4bd2-192">Cofre de chaves Olá continha Olá eliminada objeto contudo permanecerão intacto como serão todos os outros objetos no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="e4bd2-193">Chave de cofres dos como contentores</span><span class="sxs-lookup"><span data-stu-id="e4bd2-193">Key vaults as containers</span></span>
<span data-ttu-id="e4bd2-194">Quando um cofre de chaves é removido, todo o conteúdo, incluindo as chaves, os segredos e certificados, são eliminados permanentemente.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="e4bd2-195">toopurge um cofre de chaves, utilize Olá `Remove-AzureRmKeyVault` comando com a opção de Olá `-InRemovedState` e especificando a localização de Olá do Cofre de chaves Olá eliminada com Olá `-Location location` argumento.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="e4bd2-196">Pode encontrar a localização de Olá de um cofre eliminado utilizando o comando de Olá `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="e4bd2-197">Remover um cofre de chaves será permanentemente eliminada, que significa que não serão recuperável.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="e4bd2-198">Remover as permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="e4bd2-198">Purge permissions required</span></span>
- <span data-ttu-id="e4bd2-199">toopurge um cofre de chaves eliminado, para que o Cofre de Olá e todos os respetivos conteúdos permanentemente são removidos, Olá utilizador precisa de RBAC permissão tooperform um *Microsoft.KeyVault/locations/deletedVaults/purge/action* operação.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="e4bd2-200">chave de Olá eliminado toolist, tem de cofre Olá um utilizador RBAC permissão tooperform *Microsoft.KeyVault/deletedVaults/read* permissão.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="e4bd2-201">Por predefinição, apenas um administrador de subscrição tem as permissões.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="e4bd2-202">Remoção agendada</span><span class="sxs-lookup"><span data-stu-id="e4bd2-202">Scheduled purge</span></span>

<span data-ttu-id="e4bd2-203">Listar os objetos eliminados Cofre de chaves mostra quando são toobe schedled removido pelo Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="e4bd2-204">Olá *data de remoção agendada* campo indica quando um objeto do Cofre de chaves serão permanentemente eliminado, se foi efetuada nenhuma ação.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="e4bd2-205">Por predefinição, o período de retenção de Olá para um objeto eliminado Cofre de chaves é 90 dias.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="e4bd2-206">Um objeto de cofre removidos, acionado pela respetiva *data de remoção agendada* campo, é eliminado permanentemente.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="e4bd2-207">Não é recuperável.</span><span class="sxs-lookup"><span data-stu-id="e4bd2-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="e4bd2-208">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="e4bd2-208">Other resources</span></span>

- <span data-ttu-id="e4bd2-209">Para obter uma descrição geral da funcionalidade de eliminação de forma recuperável do Cofre de chaves, consulte [descrição geral da eliminação de forma recuperável do Cofre de chaves do Azure](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="e4bd2-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="e4bd2-210">Para obter uma descrição geral da utilização do Cofre de chaves do Azure, consulte [introdução ao Cofre de chaves do Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e4bd2-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

