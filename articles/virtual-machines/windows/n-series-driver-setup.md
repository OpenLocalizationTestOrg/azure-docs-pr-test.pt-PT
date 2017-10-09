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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Configurar controladores GPU para VMs N série com o Windows Server
tootake partido das capacidades GPU Olá de série N do Azure VMs do Windows Server 2016 ou o Windows Server 2012 R2 em execução, instalação de controladores de gráficos NVIDIA suportado. Este artigo fornece os passos de configuração de controlador depois de implementar uma VM de série N. As informações de configuração do controlador também estão disponíveis para [VMs com Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Para especificações básicas, as capacidades de armazenamento e detalhes do disco, consulte [tamanhos de VM do Windows para a GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Instalação de controlador

1. Estabelecer ligação ao ambiente de trabalho remoto tooeach N série VM.

2. Transferir, extraia e instalar o controlador de Olá suportado para o sistema operativo Windows.

Em VMs do Azure NV, é necessário um reinício após a instalação de controlador. Em VMs do NC, não é necessário um reinício.

## <a name="verify-driver-installation"></a>Certifique-se a instalação de controlador

Pode verificar a instalação de controladores no Gestor de dispositivos. Olá exemplo seguinte mostra uma configuração com êxito do cartão de Olá Tesla K80 numa VM de NC do Azure.

![Propriedades do controlador GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

tooquery Olá estado do dispositivo para a GPU, execute Olá [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) instalado com o controlador de Olá o utilitário da linha de comandos.

1. Abra uma linha de comandos e altere toohello **c:\Programas\Microsoft Files\NVIDIA Corporation\NVSMI** diretório.

2. Executar **nvidia smi**. Se o controlador de Olá estiver instalado, verá toobelow semelhante de saída. Tenha em atenção que **GPU Util** mostra **0%** , exceto se estiver atualmente a executar uma carga de trabalho para a GPU no Olá VM.

![Estado do dispositivo NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>Rede RDMA para NC24r VMs

Conectividade de rede RDMA, pode ser ativada em VMs NC24r implementado na Olá mesmo conjunto de disponibilidade. tem de ser adicionado ao Hello HpcVmDrivers extensão tooinstall Windows rede controladores de dispositivo que ativar a conetividade RDMA. tooadd Olá VM extensão tooan NC24r VM, utilize [Azure PowerShell](/powershell/azure/overview) cmdlets do Azure Resource Manager.

> [!NOTE]
> Atualmente, apenas o Windows Server 2012 R2 suporta a rede RDMA Olá em NC24r VMs.
> 

tooinstall Olá mais recente versão 1.1 HpcVMDrivers extensão numa VM com capacidade RDMA existente com o nome myVM na região de EUA oeste Olá:
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Para obter mais informações, consulte [extensões de Máquina Virtual e funcionalidades para o Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

rede RDMA Olá suporta tráfego da Interface de passagem de mensagens (MPI) para aplicações em execução com [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou Intel MPI 5. x. 


## <a name="next-steps"></a>Passos seguintes

* Para mais informações sobre Olá NVIDIA GPUs Olá série N VMs, consulte:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (para VMs do Azure NC)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (para VMs do Azure NV)

* Os programadores criar aplicações para a GPU-acelerados para Olá NVIDIA Tesla GPUs também podem transferir e instalar Olá CUDA Toolkit 8 para [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Para obter mais informações, consulte Olá [guia de instalação CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


