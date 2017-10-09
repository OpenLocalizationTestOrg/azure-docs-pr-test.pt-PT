---
title: aaaAzure CLI Script de exemplo - criar uma VM com um VHD | Microsoft Docs
description: "Script CLI do Azure de exemplo - criar uma VM utilizando um disco rígido virtual."
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
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Criar uma VM com um disco rígido virtual

Este exemplo cria uma máquina virtual utilizando um VHD.
Cria um grupo de recursos, uma conta do storage e um contentor, em seguida, cria uma VM através do carregamento de contentor de toohello Olá VHD.
Substitui Olá ssh pública da chave com a chave pública para que tenha acesso toohello VM.

Irá precisar de um VHD de arranque.
Pode transferir Olá VHD que utilizámos do https://azclisamples.blob.core.windows.net/vhds/sample.vhd ou utilizar o seu próprio VHD. script de Olá procura `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [lista de contas de armazenamento AZ](https://docs.microsoft.com/cli/azure/storage/account#list) | Apresenta uma lista de contas de armazenamento |
| [verificação de conta de armazenamento de AZ-name](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Verifica se um nome de conta de armazenamento é válido e que já não existe |
| [lista de chaves de conta de armazenamento AZ](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Apresenta uma lista de chaves Olá contas do storage |
| [blob de armazenamento AZ existe](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Verifica a existência de blob Olá |
| [Criar contentor de armazenamento AZ](https://docs.microsoft.com/cli/azure/storage/container#create) | Cria um contentor numa conta do storage. |
| [carregamento de blob de armazenamento AZ](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Cria um blob no contentor de Olá, carregamento Olá VHD. |
| [lista de vm AZ](https://docs.microsoft.com/cli/azure/vm#list) | Utilizado com `--query` Verifique se o nome da VM Olá está em utilização. | 
| [Criar AZ vm](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Cria Olá máquinas de virtuais. |
| [AZ vm acesso conjunto linux-utilizador](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Repõe Olá SSH toogive chave Olá atual utilizador acesso toohello VM. |
| [AZ vm lista--endereços ip](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Obtém o endereço IP Olá Olá VM que foi criado. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
