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
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="96c44-103">Redimensionar uma máquina virtual de Linux utilizando a CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="96c44-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="96c44-104">Depois de aprovisionar uma máquina virtual (VM), pode aumentar ou reduzir verticalmente a Olá VM alterando Olá [tamanho da VM][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="96c44-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="96c44-105">Em alguns casos, tem de Desalocação Olá VM primeiro.</span><span class="sxs-lookup"><span data-stu-id="96c44-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="96c44-106">É necessário toodeallocate Olá VM, se assim o desejar Olá tamanho não está disponível no cluster de hardware de Olá que está a alojar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="96c44-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="96c44-107">Este artigo descreve em detalhe como tooresize uma VM com Linux com Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="96c44-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="96c44-108">Também pode executar estes passos com Olá [CLI do Azure 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96c44-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="96c44-109">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="96c44-109">Resize a VM</span></span>
<span data-ttu-id="96c44-110">tooresize uma VM, terá de Olá mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) instalado e inicia sessão utilizando a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="96c44-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="96c44-111">Ver a lista de Olá da VM disponível tamanhos no cluster de hardware de olá onde Olá VM está alojado com [az vm-vm-redimensionamento-opções de lista](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="96c44-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="96c44-112">Olá exemplo seguinte apresenta uma lista de tamanhos de VM para VM com o nome de Olá `myVM` no grupo de recursos de Olá `myResourceGroup` região:</span><span class="sxs-lookup"><span data-stu-id="96c44-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="96c44-113">Se Olá pretendido tamanho da VM está listado, redimensionar Olá VM com [az vm redimensionar](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="96c44-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="96c44-114">Olá seguir redimensiona exemplo Olá VM com o nome `myVM` toohello `Standard_DS3_v2` tamanho:</span><span class="sxs-lookup"><span data-stu-id="96c44-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="96c44-115">Olá VM for reiniciado durante este processo.</span><span class="sxs-lookup"><span data-stu-id="96c44-115">hello VM restarts during this process.</span></span> <span data-ttu-id="96c44-116">Após o reinício de Olá, o SO existente e os discos de dados são novamente mapeados.</span><span class="sxs-lookup"><span data-stu-id="96c44-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="96c44-117">Nada no disco temporário Olá é perdido.</span><span class="sxs-lookup"><span data-stu-id="96c44-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="96c44-118">Se Olá pretendido tamanho da VM não estiver listado, é necessário toofirst desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="96c44-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="96c44-119">Este processo permite Olá VM toothen ser dimensionado tooany tamanho disponível que Olá suporta a região e, em seguida, iniciado.</span><span class="sxs-lookup"><span data-stu-id="96c44-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="96c44-120">Olá passos seguintes desalocar, redimensionar e, em seguida, iniciar Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="96c44-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="96c44-121">Olá Desalocação VM também versões quaisquer endereços IP dinâmicos atribuídos toohello VM.</span><span class="sxs-lookup"><span data-stu-id="96c44-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="96c44-122">Olá SO e discos de dados não são afetados.</span><span class="sxs-lookup"><span data-stu-id="96c44-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96c44-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="96c44-123">Next steps</span></span>
<span data-ttu-id="96c44-124">Para escalabilidade adicional, execute várias instâncias VM e aumentar horizontalmente. Para obter mais informações, consulte [Dimensionar automaticamente máquinas Linux de um conjunto de dimensionamento de Máquina Virtual][scale-set].</span><span class="sxs-lookup"><span data-stu-id="96c44-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
