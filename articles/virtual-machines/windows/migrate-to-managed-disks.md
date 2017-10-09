---
title: aaaMigrate VMs do Azure tooManaged discos | Microsoft Docs
description: "Migre máquinas virtuais do Azure criadas utilizar discos não geridos em contas de armazenamento toouse discos geridos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Migrar VMs do Azure tooManaged discos no Azure

Discos gerida do Azure simplifica a gestão de armazenamento, removendo a necessidade de Olá tooseparately gerir contas de armazenamento.  Também pode migrar o toobenefit de discos de tooManaged VMs do Azure existente de melhor fiabilidade das VMs num conjunto de disponibilidade. Garante que os discos de Olá de VMs diferentes num conjunto de disponibilidade será suficientemente isolados de cada outro tooavoid de ponto único de falhas. Coloca automaticamente discos de VMs diferentes num conjunto de disponibilidade em diferentes unidades de escala de armazenamento (carimbos) que limita o impacto de Olá de falhas de unidade de escala de armazenamento únicas provocado devido a falhas toohardware e de software.
Com base nas suas necessidades, pode escolher entre dois tipos de opções de armazenamento:

- [Os discos Premium geridos](../../storage/common/storage-premium-storage.md) -se a unidade de estado sólido (SSD) baseado no suporte de dados de armazenamento que disponibiliza highperformance, suporte de disco de baixa latência para máquinas virtuais em execução I/O intensivo cargas de trabalho. Pode tirar partido de velocidade de Olá e desempenho destes discos por migrar tooPremium geridos discos.

- [Discos padrão geridos](../../storage/common/storage-standard-storage.md) utilizar suportes de dados de armazenamento de disco rígido (HDD) com base e melhor se adequam Dev/Test e outras cargas de trabalho de acesso influxo são menos sensível tooperformance variabilidade.

Pode migrar tooManaged discos nos seguintes cenários:

| Migre...                                            | Ligação de documentação                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Converter autónomo VMs e VMs um conjunto de disponibilidade toomanaged dos discos   | [Converta os discos de toouse gerido de VMs](convert-unmanaged-to-managed-disks.md) |
| Uma única VM do clássico tooResource Manager em discos geridos     | [Migrar uma única VM](migrate-single-classic-to-resource-manager.md)  | 
| Todas as VMs de Olá numa vNet do clássico tooResource Manager em discos geridos     | [Migrar os recursos IaaS de tooResource clássico Manager](migration-classic-resource-manager-ps.md) e, em seguida, [converter uma VM de discos de toomanaged discos não gerido](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Planear a conversão de Olá tooManaged discos

Esta secção ajuda-o a decisão de melhor Olá toomake em tipos de disco e de VM.


## <a name="location"></a>Localização

Escolha uma localização onde discos gerida do Azure estão disponíveis. Se estiver a mover tooPremium geridos discos, certifique-se também que armazenamento Premium está disponível na região de olá onde estiver a planear toomove para. Consulte [serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas em localizações disponíveis.

## <a name="vm-sizes"></a>Tamanhos de VM

Se estiver a migrar discos geridos de tooPremium, tem de tamanho de Olá tooupdate de Olá VM tooPremium tamanho com capacidade de armazenamento disponível na região de olá onde está localizada a VM. Reveja os tamanhos de VM Olá que são compatíveis com o Premium Storage. as especificações de tamanho de VM do Azure Olá constam [tamanhos das virtual machines](sizes.md).
Reveja as características de desempenho de Olá de máquinas virtuais que funcionam com o Premium Storage e escolha Olá mais adequado tamanho da VM que melhor se adapta às sua carga de trabalho. Certifique-se de que existe largura de banda suficiente disponível no seu tráfego de disco do VM toodrive Olá.

## <a name="disk-sizes"></a>Tamanhos de disco

**Premium discos geridos**

Existem sete tipos de discos premium gerido que podem ser utilizados com a VM e cada um tem IOPs específicos e débito limites. Tenha em consideração estes limites ao escolher Olá tipo de disco Premium para VM com base nas necessidades de Olá da sua aplicação em termos de capacidade, desempenho, escalabilidade e carrega das horas de ponta.

| Tipo de discos Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamanho do disco           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPs por disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Débito por disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo |

**Discos geridos padrão**

Existem sete tipos de discos padrão geridos que podem ser utilizados com a VM. Cada um deles tem capacidade de diferentes, mas tem o mesmo IOPS e limites de débito. Escolha o tipo de Olá de gerido padrão discos com base nas necessidades de capacidade de Olá da sua aplicação.

| Tipo de Disco Standard  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Tamanho do disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| IOPs por disco       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Débito por disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 

## <a name="disk-caching-policy"></a>Política de colocação em cache em disco

**Premium discos geridos**

Por predefinição, o disco de política de colocação em cache é *só de leitura* para Olá todos os discos de dados Premium, e *leitura e escrita* para disco do sistema operativo Olá Premium ligados toohello VM. Esta definição de configuração é recomendada tooachieve Olá um desempenho ideal para IOs a aplicação. Pesado de escrita ou só de escrita para discos de dados (por exemplo, ficheiros de registo do SQL Server), desative a colocação em cache no disco, de modo a que pode alcançar um melhor desempenho de aplicações.

## <a name="pricing"></a>Preços

Olá revisão [preços para discos geridos](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Preços dos discos de geridos Premium é a mesmo Olá os discos Premium não gerido. Mas preços para os discos padrão geridos são diferente de discos padrão de não gerido.



## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre [discos geridos](managed-disks-overview.md)
