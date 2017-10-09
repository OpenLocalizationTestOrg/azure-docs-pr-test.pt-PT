---
title: tamanhos aaaLinux VM no Azure | Microsoft Docs
description: "Apresenta uma lista de tamanhos diferentes Olá disponíveis para computadores virtuais Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a>Tamanhos de máquinas virtuais do Linux no Azure
Este artigo descreve os tamanhos disponíveis Olá e opções para Olá máquinas virtuais do Azure, pode utilizar toorun as suas aplicações de Linux e cargas de trabalho. Também fornece toobe de considerações de implementação em consideração quando está a planear toouse estes recursos. Este artigo também está disponível para [máquinas virtuais Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


| Tipo                     | Tamanhos           |    Descrição       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Fins gerais](sizes-general.md)          | Dsv3, Dv3, série DSv2, Dv2, DS, D, Av2, A0-7  | Relação CPU/memória equilibrada. Ideal para teste e desenvolvimento, toomedium pequeno bases de dados e servidores de web de tráfego toomedium baixa. |
| [Com otimização de computação](sizes-compute.md)        | FS, F             | Relação CPU/memória elevada. Boa para servidores de web de média de tráfego, os dispositivos de rede, processos bath e servidores de aplicações.        |
| [Com otimização de memória](sizes-memory.md)         | Esv3, Ev3, M, GS, G, série DSv2, DS, Dv2, D   | Rácio de memória a CPU elevado. Excelente para servidores de base de dados relacional, caches de toolarge média e análise de memória.                 |
| [Com otimização de armazenamento](sizes-storage.md)        | Ls                | Débito e E/S de disco elevados. Ideal para bases de dados de Macrodados, SQL e NoSQL.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Especializadas máquinas virtuais de destino para composição de gráfico pesada e edição de vídeo. Disponível com GPUs único ou vários.       |
| [Computação de elevado desempenho](sizes-hpc.md) | H, A8-11          | As nossas máquinas virtuais com CPU mais rápidas e poderosas com interfaces de rede de alto débito (RDMA) opcionais. 

<br>

- Para obter informações sobre os preços de Olá tamanhos diversos, consulte [preços das Virtual Machines](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux). 
- Para disponibilidade de tamanhos de VM em regiões do Azure, consulte [produtos disponíveis por região](https://azure.microsoft.com/regions/services/).
- toosee limites geral em VMs do Azure, consulte [subscrição do Azure e limites de serviço, quotas e restrições](../../azure-subscription-service-limits.md).
- Saiba mais sobre como [unidades (ACU) de computação do Azure](../windows/acu.md) podem ajudar a comparar o desempenho de computação em SKUs do Azure.


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
- [Com otimização de memória](sizes-memory.md)
- [Com otimização de armazenamento](sizes-storage.md)
- [GPU](sizes-gpu.md)
- [Computação de elevado desempenho](sizes-hpc.md)



