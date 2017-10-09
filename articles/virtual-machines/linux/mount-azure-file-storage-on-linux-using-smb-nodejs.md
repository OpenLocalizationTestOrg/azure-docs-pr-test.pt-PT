---
title: aaaMount File storage do Azure em VMs do Linux utilizando o SMB com a CLI do Azure 1.0 | Microsoft Docs
description: Como toomount File storage do Azure em VMs do Linux utilizando o SMB
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Montagem File storage do Azure em VMs do Linux utilizando o SMB com a CLI do Azure 1.0

Este artigo mostra como toomount File storage do Azure numa VM com Linux utilizando Olá protocolo Server Message Block (SMB). O File storage oferece partilhas de ficheiros na nuvem de Olá através do protocolo SMB padrão do Olá. requisitos de Olá são:

* Um [conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
* [Secure Shell (SSH) pública e privada dos ficheiros de chaves](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a>CLI versões toouse
Pode concluir tarefas Olá utilizando um dos Olá seguintes versões de interface de linha de comandos (CLI):

- [Azure CLI 1.0](#quick-commands) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)
- [Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá


## <a name="quick-commands"></a>Comandos rápidos
tarefas de Olá tooaccomplish rapidamente, siga os passos Olá nesta secção. Para obter mais informações e contexto, início às Olá ["Instruções detalhadas"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) secção.

### <a name="prerequisites"></a>Pré-requisitos
* Um grupo de recursos
* Uma rede virtual do Azure
* Um grupo de segurança de rede com um SSH entrada
* Uma sub-rede
* Uma conta de armazenamento do Azure
* Chaves de conta de armazenamento do Azure
* Uma partilha de armazenamento de ficheiros do Azure
* Uma VM com Linux

Substitua qualquer exemplos as suas próprias definições.

### <a name="create-a-directory-for-hello-local-mount"></a>Criar um diretório de montagem local Olá

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Olá ficheiro armazenamento SMB partilha toohello montagem ponto de montagem

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Manter Olá montagem após um reinício
Adicionar Olá seguinte linha demasiado`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Instruções detalhadas

O File storage oferece partilhas de ficheiros na nuvem de Olá que utilizam o protocolo SMB padrão do Olá. Com a versão mais recente Olá do armazenamento de ficheiros, também é possível montar uma partilha de ficheiros de qualquer sistema operativo que suporta o SMB 3.0. Quando utiliza uma montagem SMB no Linux, obter cópias de segurança fácil tooa robusta, permanente arquivo local de armazenamento que é suportado por um SLA.

Mover os ficheiros de uma montagem SMB tooan VM que está alojada no armazenamento de ficheiros é que uma excelente forma toodebug registos. Isto acontece porque Olá partilha do SMB mesmo pode ser montado localmente tooyour estação de trabalho de Mac, Linux ou do Windows. SMB não é a melhor solução de Olá para transmissão em fluxo Linux ou os registos de aplicação em tempo real, porque não se encontra Olá protocolo SMB criada toohandle essas funções de registo pesada. Uma ferramenta de camada de registo dedicado, unificada como Fluentd seria uma melhor opção que SMB para a recolha de Linux e aplicação de registo de saída.

Nestas instruções detalhadas, iremos criar pré-requisitos Olá necessário toofirst criar partilha de armazenamento de ficheiros de Olá e, em seguida, monte-lo através de SMB numa VM com Linux.

1. Crie uma conta de armazenamento do Azure utilizando Olá seguinte código:

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Mostra chaves de conta de armazenamento Olá.

    Quando cria uma conta de armazenamento, chaves de conta Olá são criadas pares para que pode ser rotação sem qualquer interrupção do serviço. Quando mudar toohello segunda chave num par de Olá, crie um novo par de chaves. Chaves de conta de armazenamento novas sempre são criadas pares, assegurando que tem sempre, pelo menos, um armazenamento não utilizadas chaves pronto tooswitch para. chaves de conta de armazenamento de Olá tooshow, utilize Olá seguinte código:

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Crie a partilha de armazenamento de ficheiros de Olá.

    partilha de ficheiros de armazenamento Olá contém partilha do SMB Olá. quota de Olá sempre é expresso em gigabytes (GB). toocreate Olá partilha do File storage, utilize Olá seguinte código:

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Crie o diretório de ponto de montagem de Olá.

    Tem de criar um diretório local as Olá de toomount ficheiros de Linux do Olá sistema partilha de SMB. Nada escritas ou ler a partir do diretório de montagem local Olá é reencaminhado toohello partilha do SMB que está alojado no armazenamento de ficheiros. diretório de Olá toocreate, Olá utilize seguinte código:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. Monte Olá partilha do SMB utilizando Olá seguinte código:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. Manter Olá SMB montar através de reinícios.

    Quando reiniciar Olá VM com Linux, hello partilha SMB montada é desmontada durante o encerramento. tooremount Olá partilha SMB arranque, tem de adicionar uma linha de toohello Linux /etc/fstab. Linux utiliza Olá fstab toolist Olá ficheiro sistemas de ficheiros que necessita de toomount durante o processo de arranque Olá. Adicionar partilha SMB Olá garante que partilha do File storage Olá é um sistema de ficheiros permanentemente montado para Olá VM com Linux. Nova VM adicionar Olá ficheiro armazenamento SMB partilha tooa é possível ao utilizar init de nuvem.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Passos seguintes

- [Nuvem init toocustomize uma VM com Linux a utilizar durante a criação](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Adicionar um disco tooa VM com Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Encriptar discos uma VM com Linux utilizando Olá CLI do Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
