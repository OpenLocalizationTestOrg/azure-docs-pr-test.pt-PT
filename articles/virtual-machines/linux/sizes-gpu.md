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
# <a name="gpu-linux-vm-sizes"></a>Tamanhos de VM com Linux de GPU

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

Para passos de instalação e a verificação de controladores, consulte [a configuração do controlador de série N para Linux](n-series-driver-setup.md).

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* Recomendamos que não instale X servidor ou outros sistemas que utilizem o controlador de nouveau Olá em Ubuntu NC VMs. Antes de instalar os controladores de NVIDIA GPU, terá de controlador do toodisable Olá nouveau.  

## <a name="other-sizes"></a>Outros tamanhos de
- [Fins gerais](sizes-general.md)
- [Com otimização de computação](sizes-compute.md)
- [Com otimização de memória](sizes-memory.md)
- [Com otimização de armazenamento](sizes-storage.md)
- [Computação de elevado desempenho](sizes-hpc.md)

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre como [unidades (ACU) de computação do Azure](acu.md) podem ajudar a comparar o desempenho de computação em SKUs do Azure.