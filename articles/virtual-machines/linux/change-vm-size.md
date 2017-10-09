---
title: "aaaHow tooresize uma VM com Linux com Olá Azure CLI 2.0 | Microsoft Docs"
description: "Como tooscale cópias de segurança ou escala para baixo de uma máquina virtual do Linux, alterando Olá tamanho da VM."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>Redimensionar uma máquina virtual de Linux utilizando a CLI 2.0

Depois de aprovisionar uma máquina virtual (VM), pode aumentar ou reduzir verticalmente a Olá VM alterando Olá [tamanho da VM][vm-sizes]. Em alguns casos, tem de Desalocação Olá VM primeiro. É necessário toodeallocate Olá VM, se assim o desejar Olá tamanho não está disponível no cluster de hardware de Olá que está a alojar Olá VM. Este artigo descreve em detalhe como tooresize uma VM com Linux com Olá Azure CLI 2.0. Também pode executar estes passos com Olá [CLI do Azure 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>Redimensionar uma VM
tooresize uma VM, terá de Olá mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).

1. Ver a lista de Olá da VM disponível tamanhos no cluster de hardware de olá onde Olá VM está alojado com [az vm-vm-redimensionamento-opções de lista](/cli/azure/vm#list-vm-resize-options). Olá exemplo seguinte apresenta uma lista de tamanhos de VM para VM com o nome de Olá `myVM` no grupo de recursos de Olá `myResourceGroup` região:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. Se Olá pretendido tamanho da VM está listado, redimensionar Olá VM com [az vm redimensionar](/cli/azure/vm#resize). Olá seguir redimensiona exemplo Olá VM com o nome `myVM` toohello `Standard_DS3_v2` tamanho:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Olá VM for reiniciado durante este processo. Após o reinício de Olá, o SO existente e os discos de dados são novamente mapeados. Nada no disco temporário Olá é perdido.

3. Se Olá pretendido tamanho da VM não estiver listado, é necessário toofirst desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate). Este processo permite Olá VM toothen ser dimensionado tooany tamanho disponível que Olá suporta a região e, em seguida, iniciado. Olá passos seguintes desalocar, redimensionar e, em seguida, iniciar Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Olá Desalocação VM também versões quaisquer endereços IP dinâmicos atribuídos toohello VM. Olá SO e discos de dados não são afetados.

## <a name="next-steps"></a>Passos seguintes
Para escalabilidade adicional, execute várias instâncias VM e aumentar horizontalmente. Para obter mais informações, consulte [Dimensionar automaticamente máquinas Linux de um conjunto de dimensionamento de Máquina Virtual][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
