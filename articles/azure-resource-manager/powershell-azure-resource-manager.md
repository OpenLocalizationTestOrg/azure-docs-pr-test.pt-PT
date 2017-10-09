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
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Gerir os recursos com o Azure PowerShell e do Resource Manager
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md)
> * [CLI do Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API REST](resource-manager-rest-api.md)
>
>

Neste artigo, saiba como toomanage as suas soluções com o Azure PowerShell e o Azure Resource Manager. Se não estiver familiarizado com o Resource Manager, consulte [descrição geral do Gestor de recursos](resource-group-overview.md). Este tópico centra-se nas tarefas de gestão. Irá:

1. Criar um grupo de recursos
2. Adicionar um grupo de recursos de toohello de recursos
3. Adicione um recurso de toohello etiquetas
4. Recursos com base nos valores de etiqueta ou nomes de consulta
5. Aplicar e remover um bloqueio num recurso Olá
6. Eliminar um grupo de recursos

Este artigo não mostrar como toodeploy uma subscrição de tooyour de modelo do Resource Manager. Para essas informações, consulte [implementar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md).

## <a name="get-started-with-azure-powershell"></a>Introdução ao Azure PowerShell

Se não tiver instalado o Azure PowerShell, consulte o artigo [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

Se tiver instalado o Azure PowerShell no passado Olá, mas não tiver atualizado-recentemente, considere instalar a versão mais recente Olá. Pode atualizar a versão de Olá através de Olá mesmo método que utilizou tooinstall-lo. Por exemplo, se utilizou Olá instalador de plataforma Web, inicie-o novamente e procurar por uma atualização.

utilizar a versão do Olá módulo de recursos do Azure, de toocheck Olá seguinte cmdlet:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Este tópico foi atualizado para a versão 3.3.0. Se tiver uma versão anterior, sua experiência pode não corresponder aos passos de Olá apresentados neste tópico. Para obter documentação sobre cmdlets Olá nesta versão, consulte [AzureRM.Resources módulo](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Inicie sessão no tooyour a conta do Azure
Antes de trabalhar na sua solução, tem de iniciar sessão na conta tooyour.

toolog no tooyour conta do Azure, utilize Olá **Login-AzureRmAccount** cmdlet.

```powershell
Login-AzureRmAccount
```

Olá pede-lhe as credenciais de início de sessão de Olá para a sua conta do Azure. Após iniciar sessão, transfere as definições de conta para que estejam disponível tooAzure do PowerShell.

Olá cmdlet devolve informações sobre o toouse de subscrição de conta e Olá para tarefas de Olá.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Se tiver mais do que uma subscrição, pode alternar tooa uma subscrição diferente. Em primeiro lugar, vamos ver todas as subscrições de Olá para a sua conta.

```powershell
Get-AzureRmSubscription
```

Devolve ativados e desativados subscrições.

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

tooswitch tooa uma subscrição diferente, forneça o nome da subscrição Olá com Olá **Set-AzureRmContext** cmdlet.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Antes de implementar qualquer subscrição tooyour de recursos, tem de criar um grupo de recursos que irá conter recursos Olá.

toocreate um grupo de recursos, utilize Olá **New-AzureRmResourceGroup** cmdlet. comando de Olá utiliza Olá **nome** parâmetro toospecify um nome para o grupo de recursos de Olá e Olá **localização** parâmetro toospecify respetiva localização.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

saída de Olá consta Olá seguinte formato:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Se precisar de grupo de recursos de Olá tooretrieve mais tarde, utilize Olá seguinte cmdlet:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget Olá todos os grupos de recursos na sua subscrição, não especifique um nome de:

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Adicionar grupo de recursos de tooa de recursos
um grupo de recursos do recurso toohello tooadd, pode utilizar Olá **New-AzureRmResource** cmdlet ou um cmdlet que faz toohello específico de tipo de recurso que está a criar (como **New-AzureRmStorageAccount**). Poderá achar mais fácil toouse um cmdlet que é o tipo de recurso específico tooa pois inclui os parâmetros para propriedades de Olá que são necessárias para o recurso novo Olá. toouse **New-AzureRmResource**, tem de conhecer todos os tooset de propriedades de Olá sem pedidos para os mesmos.

No entanto, a adição de um recurso através de cmdlets poderá causar confusão futura porque o recurso novo Olá não existe um modelo do Resource Manager. A Microsoft recomenda que define a infraestrutura de Olá para a sua solução do Azure num modelo do Resource Manager. Modelos permitem-lhe tooreliably e implementar repetidamente a solução. Para este tópico, criar uma conta de armazenamento com um cmdlet do PowerShell, mas mais tarde gerar um modelo do seu grupo de recursos.

Olá seguinte cmdlet cria uma conta de armazenamento. Em vez de utilizar o nome de Olá mostrado no exemplo de Olá, forneça um nome exclusivo para a conta de armazenamento Olá. nome de Olá tem de ter entre 3 e 24 carateres de comprimento e utilizar apenas números e letras minúsculas. Se utilizar o nome de Olá mostrado no exemplo Olá, receberá um erro porque este nome já se encontra em utilização.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Se precisar de tooretrieve este recurso mais tarde, utilize Olá seguinte cmdlet:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Adicionar uma etiqueta

As etiquetas permitem-lhe tooorganize os recursos de acordo com as propriedades de toodifferent. Por exemplo, pode ter vários recursos em grupos de recursos diferente que pertencem toohello mesmo departamento. Pode aplicar um departamento etiqueta e o valor toothose recursos toomark-las como pertencentes toohello mesma categoria. Em alternativa, pode marcá-se um recurso é utilizado num ambiente de teste ou de produção. Neste tópico aplicam-se as etiquetas tooonly um recurso, mas no seu ambiente provavelmente faz sentido tooapply etiquetas tooall os recursos.

Olá seguintes cmdlet aplica-se a conta de armazenamento de tooyour etiquetas duas:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

As etiquetas são atualizadas como um único objeto. tooadd um recurso de tooa etiquetas que já inclua etiquetas, obtenha primeiro etiquetas existente Olá. Adicione Olá nova etiqueta toohello objeto que contém etiquetas existente Olá e voltar a todos os recursos de toohello de etiquetas de Olá.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Procurar recursos

Olá utilize **localizar AzureRmResource** cmdlet tooretrieve recursos para condições de pesquisa diferentes.

* tooget um recurso de por nome, fornecer Olá **ResourceNameContains** parâmetro:

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget todos os recursos de Olá num grupo de recursos, fornecer Olá **ResourceGroupNameContains** parâmetro:

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget todos os recursos de Olá com um nome de tag e um valor, fornecer Olá **TagName** e **TagValue** parâmetros:

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* recursos de Olá tooall com um tipo de recurso específico, fornecer Olá **ResourceType** parâmetro:

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Um recurso de bloqueio

Quando precisar de toomake se um recurso crítico não acidentalmente eliminado ou modificado, aplicam-se um recurso de toohello de bloqueio. Pode especificar um um **CanNotDelete** ou **ReadOnly**.

toocreate ou eliminar bloqueios de gestão, tem de ter acesso demasiado`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações. Das funções incorporadas Olá, apenas o proprietário e o administrador de acesso de utilizador são concedidas essas ações.

tooapply um bloqueio, utilize Olá seguinte cmdlet:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Olá recurso bloqueado no Olá anterior exemplo não pode ser eliminado até que o bloqueio de Olá é removido. tooremove um bloqueio, utilize:

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Para obter mais informações sobre as bloqueios de definição, consulte [bloquear recursos com o Azure Resource Manager](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Remover recursos ou um grupo de recursos
Pode remover um recurso ou grupo de recursos. Quando remove um grupo de recursos, tem também de remover todos os recursos de Olá nesse grupo de recursos.

* toodelete um recurso do grupo de recursos de Olá, utilize Olá **remover AzureRmResource** cmdlet. Este cmdlet elimina recursos Olá, mas não eliminar o grupo de recursos de Olá.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete um grupo de recursos e os respetivos recursos, utilize Olá **Remove-AzureRmResourceGroup** cmdlet.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Para ambos os cmdlets, é-lhe perguntado tooconfirm que pretende recursos de Olá tooremove ou grupo de recursos. Se a operação de Olá elimina com êxito recursos Olá ou grupo de recursos, devolve **verdadeiro**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Executar scripts de Gestor de recursos com a automatização do Azure

Este tópico mostra como tooperform operações básicas nos seus recursos com o Azure PowerShell. Para cenários de gestão mais avançados, normalmente, pretende toocreate um script e reutilizar nesse script conforme necessário ou com base numa agenda. [A automatização do Azure](../automation/automation-intro.md) fornece uma forma para os scripts de tooautomate utilizada frequentemente que gerem as suas soluções do Azure.

Olá tópicos seguintes mostram como toouse da automatização do Azure, o Resource Manager e o PowerShell tooeffectively efetuam tarefas de gestão:

- Para obter informações sobre como criar um runbook, consulte [o meu primeiro runbook do PowerShell](../automation/automation-first-runbook-textual-powershell.md).
- Para obter informações sobre como trabalhar com galleries de scripts, consulte [galleries módulos e Runbooks de automatização do Azure](../automation/automation-runbook-gallery.md).
- Para os runbooks que iniciar e parar máquinas virtuais, consulte [cenário de automatização do Azure: toocreate etiquetas formatada em JSON utilizando uma agenda para a VM do Azure de arranque e encerramento](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Para os runbooks que iniciar e parar off-hours de máquinas virtuais, consulte [VMs de início/paragem durante a solução de off-hours na automatização](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Passos seguintes
* toolearn sobre a criação de modelos do Resource Manager, consulte [criação de modelos do Azure Resource Manager](resource-group-authoring-templates.md).
* toolearn sobre a implementação de modelos, consulte [implementar uma aplicação com o modelo do Azure Resource Manager](resource-group-template-deploy.md).
* Pode mover recursos tooa novo grupo de recursos existente. Para obter exemplos, consulte [mover recursos tooNew grupo de recursos ou subscrição](resource-group-move-resources.md).
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

