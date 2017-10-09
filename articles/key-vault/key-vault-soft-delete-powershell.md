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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>Como toouse Cofre de chaves configuração soft-eliminar com o PowerShell

Funcionalidade de eliminação de forma recuperável do Azure do Cofre de chaves permite a recuperação de cofres eliminados e objetos do cofre. Especificamente, as Olá endereços de eliminação de forma recuperável os seguintes cenários:

- Suporte para eliminação recuperável de um cofre de chaves
- Suporte para a eliminação de objetos do Cofre de chaves; recuperável chaves de segredos e, de certificados

## <a name="prerequisites"></a>Pré-requisitos

- O Azure PowerShell 4.0.0 ou posterior - se não tiver já nesta configuração, instalar o Azure PowerShell e associá-lo à sua subscrição do Azure, consulte o artigo [como tooinstall e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> Há uma versão desatualizada dos nossa saída do PowerShell do Cofre de chave formatação do ficheiro que **poderá** ser carregado para o seu ambiente, em vez da versão correta do Olá. Iremos são prevendo que uma versão atualizada do PowerShell toocontain Olá necessário correção para a saída de Olá formatação e vai actualizar este tópico nessa altura. Olá solução atual, deve ocorrer este problema formatação, é:
> - Olá de utilização seguintes consulta se reparar em que não está a ver a eliminação de forma recuperável Olá ativada propriedade descrita neste tópico: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Para informações de refernece específico do Cofre de chaves para o PowerShell, consulte [referência do PowerShell do Cofre de chaves do Azure](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

## <a name="required-permissions"></a>Permissões necessárias

Operações do Cofre de chaves separadamente geridas através de permissões de controlo (RBAC) de acesso baseado em funções da seguinte forma:

| Operação | Descrição | Permissão de utilizador |
|:--|:--|:--|
|Lista|Apresenta uma lista de eliminados cofres de chaves.|Microsoft.KeyVault/deletedVaults/read|
|Recuperar|Restaura um cofre de chaves foi eliminado.|Microsoft.KeyVault/vaults/write|
|Remover|Remove permanentemente um cofre de chaves eliminado e todo o respetivo conteúdo.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Para obter mais informações sobre o controlo de acesso e permissões, consulte [proteger o seu Cofre de chaves](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Ativar a eliminação de forma recuperável

toorecover capaz de toobe um cofre de chaves eliminado ou objetos armazenados numa chave de cofre, primeiro é necessário ativar a eliminação de forma recuperável para esse cofre de chaves.

### <a name="existing-key-vault"></a>Cofre de chaves

Para um cofre de chaves com o nome ContosoVault, ative a eliminação de forma recuperável da seguinte forma. 

>[!NOTE]
>Atualmente terá toouse Olá de escrita do Azure Resource Manager recursos manipulação toodirectly *enableSoftDelete* propriedade toohello recurso do Cofre de chaves.

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Novo cofre de chaves

Ativar a eliminação de forma recuperável para um novo cofre de chaves é efetuada no momento da criação, adicionando o sinalizador de ativação de eliminação de forma recuperável do Olá tooyour criar comando.

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Certifique-se a ativação da eliminação de forma recuperável

um cofre de chaves com eliminação de forma recuperável ativada, tooverify Olá execução *obter* de comandos e procure Olá "Recuperável eliminar Enabled?" atributo e a respetiva definição, true ou false.

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Eliminar um cofre de chaves protegido por eliminar de forma recuperável

Olá comando toodelete (ou remover) um cofre de chaves permanece Olá mesmo, mas as alterações do mesmo comportamento, dependendo se ativou a configuração soft-eliminar ou não.

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>Se executar o comando anterior do Olá para um cofre de chaves que não tenha ativada de eliminação de forma recuperável, irá eliminar permanentemente este Cofre de chaves e todo o respetivo conteúdo sem quaisquer opções de recuperação.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Como eliminar de forma recuperável protege os seus cofres de chaves

Com a eliminação de forma recuperável ativada:

- Quando é eliminado um cofre de chaves, é removido do respetivo grupo de recursos e colocada num espaço de nomes reservado que só está associado à localização de olá onde foi criado. 
- Objetos de uma chave eliminado cofre, tal como chaves, os segredos e certificados, não estão acessíveis e permanecem, enquanto as respetivas Cofre de chaves que contêm está no estado de Olá eliminado. 
- nome DNS de Olá para um cofre de chaves num Estado eliminado está ainda reservado, portanto, não é possível criar um novo cofre de chaves com o mesmo nome.  

Pode ver os cofres de chaves de estado eliminado, associados à subscrição, utilizando Olá os seguintes comandos:

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

Olá *ID de recurso* Olá saída refere-se toohello ID de recurso original de neste cofre. Uma vez que este Cofre de chaves agora num Estado eliminado, nenhum recurso existe com esse ID de recurso. Olá *Id* campo pode ser utilizado tooidentify Olá recurso quando recuperar ou remoção. Olá *data de remoção agendada* campo indica quando o Cofre de Olá serão permanentemente eliminado (removidos) se foi efetuada nenhuma ação para este cofre foi eliminado. Olá de toocalculate período, utilizada de retenção de predefinição Olá *data de remoção agendada*, é de 90 dias.

## <a name="recovering-a-key-vault"></a>Recuperar um cofre de chaves

toorecover um cofre de chaves, terá de nome de Cofre de chaves toospecify Olá, grupo de recursos e localização. Tenha em atenção Olá localização e o grupo de recursos de Olá do Cofre de chaves Olá eliminado conforme necessário estes para um processo de recuperação do Cofre de chaves.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

Quando um cofre de chaves é recuperado, o resultado de Olá é um novo recurso com o ID de recurso original Olá do Cofre de chaves Se tiver sido removido o grupo de recursos de olá onde o Cofre de chaves Olá existia, um novo grupo de recursos com o mesmo nome tem de ser criado para que o Cofre de chaves Olá pode ser recuperado.

## <a name="key-vault-objects-and-soft-delete"></a>Objetos do Cofre de chaves e eliminação de forma recuperável

Para uma chave, 'ContosoFirstKey', num cofre de chaves com o nome 'ContosoVault' com eliminação de forma recuperável ativada, aqui forma como deveria eliminá essa chave.

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

Com o seu Cofre de chaves ativado para eliminação de forma recuperável, uma chave eliminada continua a aparecer como é eliminado, exceto, ao listar explicitamente ou obter chaves eliminadas. A maioria das operações numa chave no estado de Olá eliminado irão falhar, exceto para listar uma chave eliminada, recuperação ou remoção-lo. 

Por exemplo, chaves de toolist eliminado toorequest no Cofre de chaves, utilizar Olá os seguintes comandos:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>Estado de transição 

Quando elimina uma chave de um cofre de chaves com eliminação de forma recuperável ativada, poderá demorar alguns segundos para Olá toocomplete de transição. Durante este estado de transição, pode aparecer que essa chave Olá não se encontra no Estado ativa Olá ou Olá eliminado. Este comando irá listar todas as chaves eliminadas no seu Cofre de chaves com o nome 'ContosoVault'.

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

### <a name="using-soft-delete-with-key-vault-objects"></a>Utilizar a eliminação de forma recuperável com objetos de Cofre de chaves

Apenas como cofres de chaves, uma chave eliminada, segredo ou certificado permanecerá no Estado eliminado para cópia de segurança too90 dias, exceto se recuperar ou removê-lo. 

#### <a name="keys"></a>Chaves

toorecover uma chave de eliminados:

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently eliminar uma chave:

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>Remover uma chave irá eliminá-la permanentemente, que significa que não serão recuperável.

Olá **recuperar** e **remover** ações permissões os seus próprios associado a uma política de acesso do Cofre de chaves. Para um tooexecute de capaz de principal toobe utilizador ou serviço um **recuperar** ou **remover** ação têm de ter permissão de respetivos Olá para esse objeto (chave ou segredo) na política de acesso do Cofre de chaves Olá. Por predefinição, Olá **remover** permissão não é adicionar política de acesso de tooa do Cofre de chaves quando hello atalho 'tudo' toogrant utilizado todos os utilizadores de tooa de permissões. Tem de conceder explicitamente **remover** permissão. Por exemplo, Olá o seguinte comando concede user@contoso.com permissão tooperform várias operações de chaves no *ContosoVault* incluindo **remover**.

#### <a name="set-a-key-vault-access-policy"></a>Definir uma política de acesso do Cofre de chaves

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Se tiver um cofre de chaves que apenas tenha tido a eliminação de forma recuperável ativada, poderá não ter **recuperar** e **remover** permissões.

#### <a name="secrets"></a>Segredos

Como as chaves, os segredos no Cofre de chaves são manipulados com os seus próprios comandos. A seguir, são comandos Olá para eliminar, listar, recuperar e remover segredos.

- Elimine um segredo designado SQLPassword: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Lista de eliminados todos os segredos no Cofre de chaves: 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Recupere um segredo no estado de Olá eliminado: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Remover um segredo no estado de eliminação: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>Remover um segredo irá eliminá-la permanentemente, que significa que não serão recuperável.

## <a name="purging-and-key-vaults"></a>Cofres de chaves e remoção

### <a name="key-vault-objects"></a>Objetos do Cofre de chaves

A remoção de uma chave de segredo ou certificado irá eliminá-la permanentemente, que significa que não serão recuperável. Cofre de chaves Olá continha Olá eliminada objeto contudo permanecerão intacto como serão todos os outros objetos no Cofre de chaves Olá. 

### <a name="key-vaults-as-containers"></a>Chave de cofres dos como contentores
Quando um cofre de chaves é removido, todo o conteúdo, incluindo as chaves, os segredos e certificados, são eliminados permanentemente. toopurge um cofre de chaves, utilize Olá `Remove-AzureRmKeyVault` comando com a opção de Olá `-InRemovedState` e especificando a localização de Olá do Cofre de chaves Olá eliminada com Olá `-Location location` argumento. Pode encontrar a localização de Olá de um cofre eliminado utilizando o comando de Olá `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
>Remover um cofre de chaves será permanentemente eliminada, que significa que não serão recuperável.

### <a name="purge-permissions-required"></a>Remover as permissões necessárias
- toopurge um cofre de chaves eliminado, para que o Cofre de Olá e todos os respetivos conteúdos permanentemente são removidos, Olá utilizador precisa de RBAC permissão tooperform um *Microsoft.KeyVault/locations/deletedVaults/purge/action* operação. 
- chave de Olá eliminado toolist, tem de cofre Olá um utilizador RBAC permissão tooperform *Microsoft.KeyVault/deletedVaults/read* permissão. 
- Por predefinição, apenas um administrador de subscrição tem as permissões. 

### <a name="scheduled-purge"></a>Remoção agendada

Listar os objetos eliminados Cofre de chaves mostra quando são toobe schedled removido pelo Cofre de chaves. Olá *data de remoção agendada* campo indica quando um objeto do Cofre de chaves serão permanentemente eliminado, se foi efetuada nenhuma ação. Por predefinição, o período de retenção de Olá para um objeto eliminado Cofre de chaves é 90 dias.

>[!NOTE]
>Um objeto de cofre removidos, acionado pela respetiva *data de remoção agendada* campo, é eliminado permanentemente. Não é recuperável.

## <a name="other-resources"></a>Outros recursos

- Para obter uma descrição geral da funcionalidade de eliminação de forma recuperável do Cofre de chaves, consulte [descrição geral da eliminação de forma recuperável do Cofre de chaves do Azure](key-vault-ovw-soft-delete.md).
- Para obter uma descrição geral da utilização do Cofre de chaves do Azure, consulte [introdução ao Cofre de chaves do Azure](key-vault-get-started.md).

