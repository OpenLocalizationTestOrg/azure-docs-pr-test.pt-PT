---
title: "aaaAzure CLI Script de exemplo - cópia (mover) geridos toosame de discos ou outra subscrição | Microsoft Docs"
description: "Azure CLI Script de exemplo - toosame de discos de cópia (mover) gerida ou uma subscrição diferente"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Copiar discos geridos toosame ou outra subscrição com a CLI

Este script copia um toosame de disco gerido ou uma subscrição diferente, mas no Olá mesma região. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos toocreate um novo disco gerido na utilização de subscrição de destino de Olá Olá Id da origem de Olá de gerido disco. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Mostrar de disco AZ](https://docs.microsoft.com/cli/azure/disk#show) | Obtém todas as propriedades de Olá de um disco gerido utilizando as propriedades do grupo de recursos e nome Olá de disco Olá de gerido. Propriedade de ID é utilizado toocopy Olá gerido disco toodifferent subscrição.  |
| [criar disco de AZ](https://docs.microsoft.com/cli/azure/disk#create) | Copia um disco gerido através da criação de um novo disco gerido na subscrição diferentes com o Id e nome principal de Olá geridos disco.  |

## <a name="next-steps"></a>Passos seguintes

[Criar uma máquina virtual a partir de um disco gerido](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Máquina virtual adicional e discos geridos amostras de script da CLI podem ser encontrados na Olá [documentação de VM do Linux do Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
