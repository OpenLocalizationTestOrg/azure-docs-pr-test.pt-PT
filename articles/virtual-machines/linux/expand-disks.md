---
title: "discos rígidos virtuais aaaExpand numa VM com Linux no Azure | Microsoft Docs"
description: "Saiba como discos rígidos virtuais tooexpand numa VM com Linux Olá Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Como discos rígidos virtuais tooexpand numa VM com Linux Olá CLI do Azure
tamanho de disco rígido virtual Olá predefinido para o sistema de operativo Olá (SO) é, geralmente, 30 GB numa máquina virtual (VM) do Linux no Azure. Pode [adicionar discos de dados](add-disk.md) tooprovide para espaço de armazenamento adicional, mas também pode desejar tooexpand um disco de dados existente. Este artigo descreve em detalhe como tooexpand geridos discos para uma VM com Linux com Olá Azure CLI 2.0. Também pode expandir o disco do SO Olá não gerido com Olá [CLI do Azure 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Certificar-se sempre de que a cópia de segurança os dados antes de executar disco redimensiona operações. Para obter mais informações, consulte [cópia de segurança VMs com Linux no Azure](tutorial-backup-vms.md).

## <a name="expand-disk"></a>Expanda o disco
Certifique-se de que tem mais recente Olá [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).

Este artigo requer uma VM existente no Azure pelo menos um disco de dados ligada e está preparado. Se ainda não tiver uma VM que pode utilizar, consulte [criar e preparar uma VM com discos de dados](tutorial-manage-disks.md#create-and-attach-disks).

No Olá amostras seguintes, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes dos parâmetros de exemplo incluem *myResourceGroup* e *myVM*.

1. Não não possível efetuar operações em discos rígidos virtuais com Olá VM em execução. Desalocar a VM com [az vm desalocar](/cli/azure/vm#deallocate). Olá exemplo seguinte deallocates Olá VM com o nome *myVM* no grupo de recursos de Olá designado *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`não disponibilizar recursos de computação Olá. toorelease recursos de computação, utilize `az vm deallocate`. Olá VM tem de ser desalocada tooexpand Olá disco de rígido virtual.

2. Ver uma lista de discos geridos num grupo de recursos com [lista de discos az](/cli/azure/disk#list). Olá exemplo seguinte mostra uma lista de discos geridos no grupo de recursos de Olá designado *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Expanda o disco de necessário Olá com [atualização de disco az](/cli/azure/disk#update). Olá exemplo seguinte expande disco geridos Olá chamado *myDataDisk* toobe *200*tamanho Gb:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Ao expandir um disco gerido, o tamanho de Olá atualizado é mapeada toohello mais próximo do tamanho de disco gerido. Para uma tabela de camadas e tamanhos de disco gerido disponível Olá, consulte [geridos discos descrição geral do Azure - preços e faturação](../windows/managed-disks-overview.md#pricing-and-billing).

3. Iniciar a VM com [início de vm az](/cli/azure/vm#start). Olá seguir iniciado o exemplo Olá VM com o nome *myVM* no grupo de recursos de Olá designado *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM com as credenciais adequadas Olá. Pode obter o endereço IP público Olá da sua VM com [mostrar de vm az](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. Olá toouse expandir disco, tem de partição subjacente do tooexpand Olá e sistema de ficheiros.

    a. Se já montado, desmonte disco Olá:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Utilize `parted` tooview do disco e redimensione partição Olá:

    ```bash
    sudo parted /dev/sdc
    ```

    Ver informações sobre o esquema de existente partição Olá com `print`. Olá de saída é semelhante toohello seguinte o exemplo, que mostra o disco subjacente Olá é 215Gb de tamanho:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Expanda a partição com o Olá `resizepart`. Introduza o número de partição Olá, *1*e um tamanho de partição nova Olá:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, introduza`quit`

5. Com partição de Olá redimensionada, verificar a consistência de partição de Olá com `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Redimensionar agora Olá filesystem com `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Montagem Olá partição toohello pretendido localização, tais como `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. foi redimensionado tooverify disco de SO de Olá, utilize `df -h`. Olá saídas de exemplo a seguir mostra a unidade de dados de Olá, */dev/sdc1*, está agora 200 GB:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Passos seguintes
Se precisar de armazenamento adicional, também [adicionar discos de dados tooa VM com Linux](add-disk.md). Para obter mais informações sobre a encriptação de disco, consulte [discos encriptar uma VM com Linux utilizando Olá CLI do Azure](encrypt-disks.md).
