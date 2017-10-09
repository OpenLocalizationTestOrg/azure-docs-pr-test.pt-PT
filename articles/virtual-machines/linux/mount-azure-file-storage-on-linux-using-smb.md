---
title: aaaMount File storage do Azure em VMs do Linux utilizando o SMB | Microsoft Docs
description: "Como toomount File storage do Azure em VMs do Linux utilizando o SMB com Olá Azure CLI 2.0"
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>Armazenamento de ficheiros do Azure de montagem em VMs do Linux utilizando o SMB

Este artigo mostra como tooutilize Olá serviço de armazenamento de ficheiros do Azure numa VM com Linux através de SMB montagem com Olá Azure CLI 2.0. File storage do Azure oferece partilhas de ficheiros na nuvem de Olá utilizando o protocolo SMB padrão do Olá. Também pode executar estes passos com Olá [CLI do Azure 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). requisitos de Olá são:

- [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
- [Ficheiros de chaves públicas e privadas SSH](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>Comandos Rápidos

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
toodo por isso, adicionar Olá seguinte linha toohello `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Instruções detalhadas

O File storage oferece partilhas de ficheiros na nuvem de Olá que utilizam o protocolo SMB padrão do Olá. Com a versão mais recente Olá do armazenamento de ficheiros, também é possível montar uma partilha de ficheiros de qualquer sistema operativo que suporta o SMB 3.0. Quando utiliza uma montagem SMB no Linux, obter cópias de segurança fácil tooa robusta, permanente arquivo local de armazenamento que é suportado por um SLA.

Mover os ficheiros de uma montagem SMB tooan VM que está alojada no armazenamento de ficheiros é que uma excelente forma toodebug registos. Isto acontece porque Olá partilha do SMB mesmo pode ser montado localmente tooyour estação de trabalho de Mac, Linux ou do Windows. SMB não é a melhor solução de Olá para transmissão em fluxo Linux ou os registos de aplicação em tempo real, porque não se encontra Olá protocolo SMB criada toohandle essas funções de registo pesada. Uma ferramenta de camada de registo dedicado, unificada como Fluentd seria uma melhor opção que SMB para a recolha de Linux e aplicação de registo de saída.

Nestas instruções detalhadas, iremos criar pré-requisitos Olá necessário toofirst criar partilha de armazenamento de ficheiros de Olá e, em seguida, monte-lo através de SMB numa VM com Linux.

1. Criar um grupo de recursos com [criar grupo az](/cli/azure/group#create) partilha de ficheiros de Olá toohold.

    com o nome de um grupo de recursos de toocreate `myResourceGroup` na localização "EUA Oeste" Olá, utilize o seguinte exemplo de Olá:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Criar uma conta de armazenamento do Azure com [criar conta de armazenamento az](/cli/azure/storage/account#create) toostore Olá ficheiros concretos.

    toocreate uma conta de armazenamento com o nome mystorageaccount utilizando o armazenamento de Standard_LRS Olá SKU, seguinte o exemplo de Olá de utilização:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Mostra chaves de conta de armazenamento Olá.

    Quando cria uma conta de armazenamento, chaves de conta Olá são criadas pares para que pode ser rotação sem qualquer interrupção do serviço. Quando mudar toohello segunda chave num par de Olá, crie um novo par de chaves. Chaves de conta de armazenamento novas sempre são criadas pares, assegurando que tem sempre, pelo menos, um armazenamento utilizado conta chave pronto tooswitch para.

    Visualizar chaves de conta de armazenamento Olá com Olá [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list). Olá, chaves de conta de armazenamento para Olá denominado `mystorageaccount` estão listados na seguinte o exemplo de Olá:

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract uma chave única, utilize Olá `--query` sinalizador. Olá exemplo seguinte extrai primeira chave de Olá (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Crie a partilha de armazenamento de ficheiros de Olá.

    partilha de ficheiros de armazenamento Olá contém Olá partilha do SMB com [criar partilha de armazenamento az](/cli/azure/storage/share#create). quota de Olá sempre é expresso em gigabytes (GB). Uma das chaves de Olá passar de Olá anterior `az storage account keys list` comando. Crie uma partilha denominada mystorageshare com uma quota de 10 GB ao utilizar o seguinte exemplo de Olá:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Crie um diretório do ponto de montagem.

    Crie um diretório local nas Olá de toomount ficheiros de Linux do Olá sistema partilha de SMB. Nada escritas ou ler a partir do diretório de montagem local Olá é reencaminhado toohello partilha do SMB que está alojado no armazenamento de ficheiros. toocreate um diretório local em/mnt/mymountdirectory, seguinte o exemplo de Olá de utilização:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Olá SMB partilha toohello local diretório de montagem.

    Forneça o seu próprio nome de utilizador de conta de armazenamento e a chave de conta de armazenamento para as credenciais de montagem Olá da seguinte forma:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. Manter Olá SMB montar através de reinícios.

    Quando reiniciar Olá VM com Linux, hello partilha SMB montada é desmontada durante o encerramento. Olá tooremount partilha do SMB no arranque, adicionar uma linha de toohello Linux /etc/fstab. Linux utiliza Olá fstab toolist Olá ficheiro sistemas de ficheiros que necessita de toomount durante o processo de arranque Olá. Adicionar partilha SMB Olá garante que partilha do File storage Olá é um sistema de ficheiros permanentemente montado para Olá VM com Linux. Nova VM adicionar Olá ficheiro armazenamento SMB partilha tooa é possível ao utilizar init de nuvem.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Passos seguintes

- [Nuvem init toocustomize uma VM com Linux a utilizar durante a criação](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Adicionar um disco tooa VM com Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Encriptar discos uma VM com Linux utilizando Olá CLI do Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
