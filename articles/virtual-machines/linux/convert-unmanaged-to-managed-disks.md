---
title: "aaaConvert máquina virtual com Linux no Azure de não discos discos toomanaged - discos gerida do Azure | Microsoft Docs"
description: "Como tooconvert uma VM com Linux a partir de discos não gerido toomanaged discos utilizando o Azure CLI 2.0 no modelo de implementação do Resource Manager Olá"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Converter uma máquina virtual Linux de discos de toomanaged discos não gerido

Se tiver existentes máquinas de virtuais de Linux (VMs) que utilizam discos não geridos, pode converter Olá VMs toouse gerido discos através de Olá [Azure geridos discos](../windows/managed-disks-overview.md) serviço. Este processo converte o disco de Olá SO e discos de dados anexados.

Este artigo mostra como tooconvert VMs utilizando Olá CLI do Azure. Se precisar de tooinstall ou atualizá-lo, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Antes de começar

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Converter a VMs de instância única
Esta secção abrange como tooconvert single-instance as VMs do Azure de não discos toomanaged discos. (Se as suas VMs num conjunto de disponibilidade, consulte o secção seguinte Olá.) Pode utilizar este processo tooconvert Olá VMs do premium (SSD) não gerido discos toopremium gerido discos ou de standard (HDD) não geridos discos toostandard gerido discos.

1. Desalocar Olá VM utilizando [az vm desalocar](/cli/azure/vm#deallocate). Olá exemplo seguinte deallocates Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Converta os discos de toomanaged VM de Olá utilizando [converter az vm](/cli/azure/vm#convert). Olá seguir o processo converte Olá VM com o nome `myVM`, incluindo disco Olá SO e discos de dados:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Iniciar Olá VM após a discos de toomanaged de conversão de Olá utilizando [início de vm az](/cli/azure/vm#start). Olá seguir iniciado o exemplo Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Converter VMs num conjunto de disponibilidade

Se Olá VMs que pretende que sejam tooconvert toomanaged discos estão num conjunto de disponibilidade, terá primeiro tooconvert Olá disponibilidade conjunto tooa gerido conjunto de disponibilidade.

Todas as VMs no conjunto de disponibilidade de Olá tem de ser desalocadas antes de converter o conjunto de disponibilidade de Olá. Tooconvert plano todos os discos de toomanaged VMs depois de disponibilidade de Olá definir próprio foi convertida tooa gerido conjunto de disponibilidade. Em seguida, iniciar todas as VMs de Olá e continuar a funcionar como normal.

1. Lista todas as VMs num conjunto através de disponibilidade [lista de conjunto de disponibilidade de vm az](/cli/azure/vm/availability-set#list). Olá exemplo seguinte apresenta uma lista de todas as VMs no conjunto nomeada de disponibilidade de Olá `myAvailabilitySet` no grupo de recursos de Olá designado `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Desalocar todas as VMs de Olá utilizando [az vm desalocar](/cli/azure/vm#deallocate). Olá exemplo seguinte deallocates Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Converter o conjunto através de disponibilidade de Olá [converter o conjunto de disponibilidade az vm](/cli/azure/vm/availability-set#convert). Olá exemplo seguinte converte conjunto nomeada de disponibilidade de Olá `myAvailabilitySet` no grupo de recursos de Olá designado `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Converter a todos os discos de toomanaged de VMs de Olá utilizando [converter az vm](/cli/azure/vm#convert). Olá seguir o processo converte Olá VM com o nome `myVM`, incluindo disco Olá SO e discos de dados:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Iniciar todas as VMs de Olá após discos de toomanaged de conversão de Olá utilizando [início de vm az](/cli/azure/vm#start). Olá seguir iniciado o exemplo Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre as opções de armazenamento, consulte [descrição geral do Azure gerida discos](../windows/managed-disks-overview.md).
