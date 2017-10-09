---
title: "aaaAzure CLI Script de exemplo - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa numa região diferente | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa na subscrição idêntica ou diferente"
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
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Exportar/cópia gerido instantâneos como conta de armazenamento do VHD tooa numa região diferente com a CLI

Este script exporta uma conta de armazenamento do instantâneo gerido tooa numa região diferente. -Lo primeiro gera Olá URI de SAS do instantâneo Olá e, em seguida, utiliza-toocopy-tooa a conta de armazenamento numa região diferente. Utilize este script toomaintain de cópia de segurança aos discos geridos numa região diferente para a recuperação de desastre. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos toogenerate URI de SAS para um Olá gerido de instantâneos e cópias de instantâneos tooa conta de armazenamento com o URI de SAS. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [AZ instantâneo conceder acesso de leitura](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Gera SAS só de leitura, que é utilizado toocopy subjacente a conta de armazenamento de tooa de ficheiros VHD ou transferi-lo tooon local  |
| [iniciar a cópia de BLOBs de armazenamento AZ](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Copia um blob de forma assíncrona a partir de um tooanother de conta de armazenamento |

## <a name="next-steps"></a>Passos seguintes

[Criar um disco gerido a partir de um VHD](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Criar uma máquina virtual a partir de um disco gerido](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Máquina virtual adicional e discos geridos amostras de script da CLI podem ser encontrados na Olá [documentação de VM do Linux do Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
