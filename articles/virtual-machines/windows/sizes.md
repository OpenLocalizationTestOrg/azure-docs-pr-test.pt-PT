---
title: tamanhos aaaWindows VM no Azure | Microsoft Docs
description: "Apresenta uma lista de tamanhos diferentes Olá disponíveis para máquinas virtuais do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a>Tamanhos de máquinas virtuais do Windows no Azure

Este artigo descreve os tamanhos disponíveis Olá e opções para Olá máquinas virtuais do Azure, pode utilizar toorun as suas aplicações do Windows e cargas de trabalho. Também fornece toobe de considerações de implementação em consideração quando está a planear toouse estes recursos.  Este artigo também está disponível para [máquinas virtuais do Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


| Tipo                     | Tamanhos           |    Descrição       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Fins gerais](sizes-general.md)          | Dsv3, Dv3, série DSv2, Dv2, DS, D, Av2, A0 7 | Relação CPU/memória equilibrada. Ideal para teste e desenvolvimento, toomedium pequeno bases de dados e servidores de web de tráfego toomedium baixa. |
| [Com otimização de computação](sizes-compute.md)        | FS, F             | Relação CPU/memória elevada. Ideal para servidores Web com tráfego médio, aplicações de rede, processos em lote e servidores de aplicações.        |
| [Com otimização de memória](../virtual-machines-windows-sizes-memory.md)         | Esv3, Ev3, M, GS, G, série DSv2, DS, Dv2, D   | Rácio de memória a CPU elevado. Excelente para servidores de base de dados relacional, caches de toolarge média e análise de memória.                 |
| [Com otimização de armazenamento](../virtual-machines-windows-sizes-storage.md)        | Ls                | Débito e E/S de disco elevados. Ideal para bases de dados de Macrodados, SQL e NoSQL.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Especializadas máquinas virtuais de destino para composição de gráfico pesada e edição de vídeo. Disponível com GPUs único ou vários.       |
| [Computação de elevado desempenho](sizes-hpc.md) | H, A8-11          | As nossas máquinas virtuais com CPU mais rápidas e poderosas com interfaces de rede de alto débito (RDMA) opcionais. 

<br> 

- Para obter informações sobre os preços de Olá tamanhos diversos, consulte [preços das Virtual Machines](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows). 
- toosee limites geral em VMs do Azure, consulte [subscrição do Azure e limites de serviço, quotas e restrições](../../azure-subscription-service-limits.md).
- Os custos de armazenamento são calculados separadamente com base nas páginas utilizadas na conta do storage Olá. Para obter detalhes, [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/).
- Saiba mais sobre como [unidades (ACU) de computação do Azure](acu.md) podem ajudar a comparar o desempenho de computação em SKUs do Azure.



## <a name="rest-api"></a>REST API

Para informações sobre como utilizar Olá tooquery de REST API para tamanhos de VM, consulte o seguinte Olá:

- [Listar tamanhos de máquina virtual disponíveis para redimensionar](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [Listar tamanhos de máquina virtual disponíveis para uma subscrição](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [Listar tamanhos de máquina virtual disponíveis num conjunto de disponibilidade](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a>ACU

Saiba mais sobre como [unidades (ACU) de computação do Azure](acu.md) podem ajudar a comparar o desempenho de computação em SKUs do Azure.

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre Olá diferentes tamanhos de VM que estão disponíveis:
- [Fins gerais](sizes-general.md)
- [Com otimização de computação](sizes-compute.md)
- [Com otimização de memória](../virtual-machines-windows-sizes-memory.md)
- [Com otimização de armazenamento](../virtual-machines-windows-sizes-storage.md)
- [Com otimização de GPU](sizes-gpu.md)
- [Computação de elevado desempenho](sizes-hpc.md)



