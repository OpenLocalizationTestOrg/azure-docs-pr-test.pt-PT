---
title: "aaaAzure CLI Script de exemplo - criar um disco gerido a partir de um instantâneo | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar um disco gerido a partir de um instantâneo"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Criar um disco gerido a partir de um instantâneo com o CLI

Este script cria um disco gerido a partir de um instantâneo. Utilizá-lo toorestore uma máquina virtual de instantâneos de discos de dados e SO. Crie o SO e discos geridos dos respetivos instantâneos de dados e, em seguida, criar uma nova máquina virtual ligando discos geridos. Também pode restaurar os discos de dados de uma VM existente ao anexar a criação de instantâneos de discos de dados.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos toocreate um disco gerido a partir de um instantâneo. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Mostrar de instantâneo AZ](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtém todas as propriedades de Olá de um instantâneo com o nome de Olá e propriedades do grupo de recursos de instantâneo Olá. Propriedade de ID é utilizado toocreate de disco gerido.  |
| [criar disco de AZ](https://docs.microsoft.com/cli/azure/disk#create) | Cria um geridos utilizando o disco de instantâneos Id de um instantâneo gerido |

## <a name="next-steps"></a>Passos seguintes

[Criar uma máquina virtual ao anexar um disco gerido como disco do SO](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Máquina virtual adicional e discos geridos amostras de script da CLI podem ser encontrados na Olá [documentação de VM do Linux do Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
