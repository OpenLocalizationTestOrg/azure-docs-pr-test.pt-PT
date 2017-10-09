---
title: tamanhos de aaaAzure VM com Linux - GPU | Microsoft Docs
description: "Apresenta uma lista de Olá diferentes GPU com otimização de tamanhos disponíveis para computadores virtuais Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="55468-103">Tamanhos de VM com Linux de GPU</span><span class="sxs-lookup"><span data-stu-id="55468-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="55468-104">Para passos de instalação e a verificação de controladores, consulte [a configuração do controlador de série N para Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="55468-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="55468-105">Recomendamos que não instale X servidor ou outros sistemas que utilizem o controlador de nouveau Olá em Ubuntu NC VMs.</span><span class="sxs-lookup"><span data-stu-id="55468-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="55468-106">Antes de instalar os controladores de NVIDIA GPU, terá de controlador do toodisable Olá nouveau.</span><span class="sxs-lookup"><span data-stu-id="55468-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="55468-107">Outros tamanhos de</span><span class="sxs-lookup"><span data-stu-id="55468-107">Other sizes</span></span>
- [<span data-ttu-id="55468-108">Fins gerais</span><span class="sxs-lookup"><span data-stu-id="55468-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="55468-109">Com otimização de computação</span><span class="sxs-lookup"><span data-stu-id="55468-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="55468-110">Com otimização de memória</span><span class="sxs-lookup"><span data-stu-id="55468-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="55468-111">Com otimização de armazenamento</span><span class="sxs-lookup"><span data-stu-id="55468-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="55468-112">Computação de elevado desempenho</span><span class="sxs-lookup"><span data-stu-id="55468-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="55468-113">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="55468-113">Next steps</span></span>
<span data-ttu-id="55468-114">Saiba mais sobre como [unidades (ACU) de computação do Azure](acu.md) podem ajudar a comparar o desempenho de computação em SKUs do Azure.</span><span class="sxs-lookup"><span data-stu-id="55468-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>