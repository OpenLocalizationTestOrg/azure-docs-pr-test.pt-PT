---
title: "configuração de controlador aaaAzure N série para Windows | Microsoft Docs"
description: "Como tooset segurança controladores NVIDIA GPU série N VMs do Windows em execução no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="564d0-103">Configurar controladores GPU para VMs N série com o Windows Server</span><span class="sxs-lookup"><span data-stu-id="564d0-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="564d0-104">tootake partido das capacidades GPU Olá de série N do Azure VMs do Windows Server 2016 ou o Windows Server 2012 R2 em execução, instalação de controladores de gráficos NVIDIA suportado.</span><span class="sxs-lookup"><span data-stu-id="564d0-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="564d0-105">Este artigo fornece os passos de configuração de controlador depois de implementar uma VM de série N.</span><span class="sxs-lookup"><span data-stu-id="564d0-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="564d0-106">As informações de configuração do controlador também estão disponíveis para [VMs com Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="564d0-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="564d0-107">Para especificações básicas, as capacidades de armazenamento e detalhes do disco, consulte [tamanhos de VM do Windows para a GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="564d0-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="564d0-108">Instalação de controlador</span><span class="sxs-lookup"><span data-stu-id="564d0-108">Driver installation</span></span>

1. <span data-ttu-id="564d0-109">Estabelecer ligação ao ambiente de trabalho remoto tooeach N série VM.</span><span class="sxs-lookup"><span data-stu-id="564d0-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="564d0-110">Transferir, extraia e instalar o controlador de Olá suportado para o sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="564d0-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="564d0-111">Em VMs do Azure NV, é necessário um reinício após a instalação de controlador.</span><span class="sxs-lookup"><span data-stu-id="564d0-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="564d0-112">Em VMs do NC, não é necessário um reinício.</span><span class="sxs-lookup"><span data-stu-id="564d0-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="564d0-113">Certifique-se a instalação de controlador</span><span class="sxs-lookup"><span data-stu-id="564d0-113">Verify driver installation</span></span>

<span data-ttu-id="564d0-114">Pode verificar a instalação de controladores no Gestor de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="564d0-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="564d0-115">Olá exemplo seguinte mostra uma configuração com êxito do cartão de Olá Tesla K80 numa VM de NC do Azure.</span><span class="sxs-lookup"><span data-stu-id="564d0-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![Propriedades do controlador GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="564d0-117">tooquery Olá estado do dispositivo para a GPU, execute Olá [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o controlador de Olá o utilitário da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="564d0-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="564d0-118">Abra uma linha de comandos e altere toohello **c:\Programas\Microsoft Files\NVIDIA Corporation\NVSMI** diretório.</span><span class="sxs-lookup"><span data-stu-id="564d0-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="564d0-119">Executar **nvidia smi**.</span><span class="sxs-lookup"><span data-stu-id="564d0-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="564d0-120">Se o controlador de Olá estiver instalado, verá toobelow semelhante de saída.</span><span class="sxs-lookup"><span data-stu-id="564d0-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="564d0-121">Tenha em atenção que **GPU Util** mostra **0%** , exceto se estiver atualmente a executar uma carga de trabalho para a GPU no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="564d0-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![Estado do dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="564d0-123">Rede RDMA para NC24r VMs</span><span class="sxs-lookup"><span data-stu-id="564d0-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="564d0-124">Conectividade de rede RDMA, pode ser ativada em VMs NC24r implementado na Olá mesmo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="564d0-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="564d0-125">tem de ser adicionado ao Hello HpcVmDrivers extensão tooinstall Windows rede controladores de dispositivo que ativar a conetividade RDMA.</span><span class="sxs-lookup"><span data-stu-id="564d0-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="564d0-126">tooadd Olá VM extensão tooan NC24r VM, utilize [Azure PowerShell](/powershell/azure/overview) cmdlets do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="564d0-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="564d0-127">Atualmente, apenas o Windows Server 2012 R2 suporta a rede RDMA Olá em NC24r VMs.</span><span class="sxs-lookup"><span data-stu-id="564d0-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="564d0-128">tooinstall Olá mais recente versão 1.1 HpcVMDrivers extensão numa VM com capacidade RDMA existente com o nome myVM na região de EUA oeste Olá:</span><span class="sxs-lookup"><span data-stu-id="564d0-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="564d0-129">Para obter mais informações, consulte [extensões de Máquina Virtual e funcionalidades para o Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="564d0-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="564d0-130">rede RDMA Olá suporta tráfego da Interface de passagem de mensagens (MPI) para aplicações em execução com [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou Intel MPI 5. x.</span><span class="sxs-lookup"><span data-stu-id="564d0-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="564d0-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="564d0-131">Next steps</span></span>

* <span data-ttu-id="564d0-132">Para mais informações sobre Olá NVIDIA GPUs Olá série N VMs, consulte:</span><span class="sxs-lookup"><span data-stu-id="564d0-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="564d0-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para VMs do Azure NC)</span><span class="sxs-lookup"><span data-stu-id="564d0-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="564d0-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para VMs do Azure NV)</span><span class="sxs-lookup"><span data-stu-id="564d0-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="564d0-135">Os programadores criar aplicações para a GPU-acelerados para Olá NVIDIA Tesla GPUs também podem transferir e instalar Olá CUDA Toolkit 8 para [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="564d0-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="564d0-136">Para obter mais informações, consulte Olá [guia de instalação CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="564d0-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


