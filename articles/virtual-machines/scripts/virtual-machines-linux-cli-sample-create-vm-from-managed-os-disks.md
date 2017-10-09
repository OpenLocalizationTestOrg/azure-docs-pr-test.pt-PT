---
title: aaaAzure CLI Script de exemplo - criar uma VM ao anexar um disco como disco de SO gerido | Microsoft Docs
description: Script CLI do Azure de exemplo - criar uma VM ao anexar um disco gerido como disco do SO
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a>Criar uma máquina virtual utilizando um disco de SO gerido existente com a CLI

Este script cria uma máquina virtual, anexar um disco existente gerido como disco do SO. Utilize este script no precedente cenários:
* Criar uma VM a partir de um disco de SO gerido existente que foi copiado a partir de um disco gerido numa subscrição diferente
* Criar uma VM a partir de um disco gerido existente criada a partir do ficheiro VHD especializado 
* Criar uma VM a partir de um disco de SO gerido existente que foi criado a partir de um instantâneo 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá seguintes propriedades de disco de tooget gerido de comandos, anexar um disco gerido tooa nova VM e criar uma VM. Cada item na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Mostrar de disco AZ](https://docs.microsoft.com/cli/azure/disk#show) | Obtém as propriedades de disco gerido com o nome do disco e o nome do grupo de recursos. Propriedade de ID é utilizado tooattach tooa um disco gerido nova VM |
| [Criar AZ vm](https://docs.microsoft.com/cli/azure/vm#create) | Cria uma VM a utilizar um disco de SO gerido |
## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
