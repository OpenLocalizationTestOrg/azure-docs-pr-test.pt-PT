---
title: aaaAzure CLI Script de exemplo - VMs reiniciar | Microsoft Docs
description: "Exemplo de Script CLI do Azure - reinício VMs por tag e ID"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Reinício de VMs

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Este exemplo mostra algumas formas tooget algumas VMs e reiniciá-las.

Olá reinicia primeiro todas as VMs de Olá no grupo de recursos de Olá.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

Olá segundo obtém Olá etiquetados VMs utilizando `az resouce list` filtra toohello recursos que são as VMs e reinicia esses VMs.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Este exemplo funciona numa shell de deteção. Para opções sobre a execução de scripts da CLI do Azure num cliente Windows, consulte [Olá CLI do Azure a executar no Windows](../windows/cli-options.md).


## <a name="sample-script"></a>Script de exemplo

exemplo de Olá tem três scripts.
Olá máquinas de virtuais de Olá aprovisiona um primeiro.
Utiliza a opção de não-aguardar Olá pelo comando Olá devolve sem aguardar a resposta de cada toobe VM aprovisionado.
Olá aguarda segundo Olá VMs toobe totalmente aprovisionado.
script terceiro Olá reiniciado todas as VMs de Olá que tenham sido aprovisionadas e, em seguida, Olá apenas etiquetados VMs.

### <a name="provision-hello-vms"></a>Aprovisionar Olá VMs

Este script cria um grupo de recursos e, em seguida, cria três toorestart de VMs.
Dois dos mesmos são etiquetados.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Wait

Este script verifica-se no estado de aprovisionamento cada 20 segundos até que todos os três VMs são aprovisionadas ou um deles falha tooprovision de Olá.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Reiniciar Olá VMs

Este script reiniciado todas as VMs de Olá no grupo de recursos de Olá e, em seguida, reinicia-apenas Olá etiquetado VMs.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Depois de executar o script de exemplo Olá, Olá os seguintes comandos pode ser utilizados tooremove Olá os grupos de recursos, VMs e recursos relacionados todos os.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar AZ vm](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Cria Olá máquinas de virtuais.  |
| [lista de vm AZ](https://docs.microsoft.com/cli/azure/vm#list) | Utilizado com `--query` tooensure Olá VMs são aprovisionados antes de reiniciá-los e, em seguida, tooget Olá IDs de Olá VMs toorestart-los. |
| [lista de recursos de AZ](https://docs.microsoft.com/cli/azure/vm#list) | Utilizado com `--query` tooget Olá IDs de VMs de Olá utilizar Olá tag. |
| [reinício de vm AZ](https://docs.microsoft.com/cli/azure/vm#list) | Reinicia Olá VMs. |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
