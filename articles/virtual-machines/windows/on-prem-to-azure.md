---
title: aaaMigrate do AWS e outra plataformas tooManaged discos no Azure | Microsoft Docs
description: "Criar VMs no Azure utilizando VHDs carregados a partir de outras nuvens como AWS ou outras plataformas de Virtualização e tirar partido dos discos gerida do Azure."
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
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Migrar a partir do Amazon Web Services (AWS) e outras plataformas tooManaged discos no Azure

Pode carregar ficheiros VHD AWS ou no local virtualização soluções tooAzure toocreate VMs tirar partido dos discos geridos. Discos do Azure gerida remove a necessidade de Olá toomanaging de contas de armazenamento para VMs IaaS do Azure. Tooonly especifique tipo Olá (Premium ou Standard) e o tamanho do disco tem de ter e Azure irá criar e gerir o disco de Olá por si. 

Pode carregar os VHDs generalizados e especializados. 
- **Generalizado VHD** -apresentou todas as informações da sua conta pessoal removidas utilizando Sysprep. 
- **Especializada VHD** -mantém as contas de utilizador Olá, aplicações e outros dados de estado de original VM. 

> [!IMPORTANT]
> Antes de carregar qualquer tooAzure VHD, deve seguir [preparar um tooAzure de tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| Cenário                                                                                                                         | Documentação                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Tiver uma instâncias AWS EC2 existente que pode pretender toomigrate tooAzure discos geridos                                     | [Mover uma VM de tooAzure Amazon Web Services (AWS)](aws-to-azure.md)                           |
| Tiver uma VM a partir e outra plataforma de Virtualização que gostaria de toouse toouse como uma imagem toocreate várias VMs do Azure. | [Carregar um VHD generalizado e utilizá-la toocreate um novas VMs no Azure](upload-generalized-managed.md) |
| Tiver uma VM de forma exclusiva personalizada que gostaria de toorecreate no Azure.                                                      | [Carregar um tooAzure especializada do VHD e criar uma nova VM](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Descrição geral dos discos geridos

Discos gerida do Azure simplifica a gestão de VM, removendo as contas de armazenamento do Olá necessidade toomanage. Discos geridos pelo também benefício da melhor fiabilidade das VMs num conjunto de disponibilidade. Garante que os discos de Olá de VMs diferentes num conjunto de disponibilidade será suficientemente isolados de cada outro tooavoid de ponto único de falhas. Coloca automaticamente discos de VMs diferentes num conjunto de disponibilidade em diferentes unidades de escala de armazenamento (carimbos) que limita o impacto de Olá de falhas de unidade de escala de armazenamento únicas provocado devido a falhas toohardware e de software. Com base nas suas necessidades, pode escolher entre dois tipos de opções de armazenamento: 
 
- [Os discos Premium geridos](../../storage/common/storage-premium-storage.md) -se a unidade de estado sólido (SSD) baseado no suporte de armazenamento de armazenamento que disponibiliza highperformance, suporte de disco de baixa latência para máquinas virtuais em execução I/O intensivo cargas de trabalho. Pode tirar partido de velocidade de Olá e desempenho destes discos por migrar tooPremium geridos discos.  

- [Discos padrão geridos](../../storage/common/storage-standard-storage.md) utilizar suportes de dados de armazenamento de disco rígido (HDD) com base e melhor se adequam Dev/Test e outras cargas de trabalho de acesso influxo são menos sensível tooperformance variabilidade.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planear a migração de Olá tooManaged discos

Esta secção ajuda-o a decisão de melhor Olá toomake em tipos de disco e de VM.


### <a name="location"></a>Localização

Escolha uma localização onde discos gerida do Azure estão disponíveis. Se estiver a migrar discos geridos de tooPremium, certifique-se também que armazenamento Premium está disponível na região de olá onde estiver a planear toomigrate para. Consulte [serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas em localizações disponíveis.

### <a name="vm-sizes"></a>Tamanhos de VM

Se estiver a migrar discos geridos de tooPremium, tem de tamanho de Olá tooupdate de Olá VM tooPremium tamanho com capacidade de armazenamento disponível na região de olá onde está localizada a VM. Reveja os tamanhos de VM Olá que são compatíveis com o Premium Storage. as especificações de tamanho de VM do Azure Olá constam [tamanhos das virtual machines](sizes.md).
Reveja as características de desempenho de Olá de máquinas virtuais que funcionam com o Premium Storage e escolha Olá mais adequado tamanho da VM que melhor se adapta às sua carga de trabalho. Certifique-se de que existe largura de banda suficiente disponível no seu tráfego de disco do VM toodrive Olá.

### <a name="disk-sizes"></a>Tamanhos de disco

**Premium discos geridos**

Existem três tipos de discos Premium gerido que podem ser utilizados com a VM e cada um tem IOPs específicos e débito limites. Quando escolher Olá tipo de disco Premium para VM com base nas necessidades de Olá da sua aplicação em termos de capacidade, desempenho, escalabilidade e carrega das horas de ponta, considere estes limites.

| Tipo de discos Premium  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| Tamanho do disco           | 128 GB            | 512 GB            | 1024 GB (1 TB)    |
| IOPs por disco       | 500               | 2300              | 5000              |
| Débito por disco | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo |

**Discos geridos padrão**

Existem cinco tipos de discos padrão gerido que podem ser utilizados com a VM. Cada um deles tem capacidade de diferentes, mas tem o mesmo IOPS e limites de débito. Escolha o tipo de Olá de gerido padrão discos com base nas necessidades de capacidade de Olá da sua aplicação.

| Tipo de Disco Standard  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| Tamanho do disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   |
| IOPs por disco       | 500              | 500              | 500              | 500              | 500              |
| Débito por disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo |

### <a name="disk-caching-policy"></a>Política de colocação em cache em disco 

**Premium discos geridos**

Por predefinição, o disco de política de colocação em cache é *só de leitura* para Olá todos os discos de dados Premium, e *leitura e escrita* para disco do sistema operativo Olá Premium ligados toohello VM. Esta definição de configuração é recomendada tooachieve Olá um desempenho ideal para IOs a aplicação. Pesado de escrita ou só de escrita para discos de dados (por exemplo, ficheiros de registo do SQL Server), desative a colocação em cache no disco, de modo a que pode alcançar um melhor desempenho de aplicações.

### <a name="pricing"></a>Preços

Olá revisão [preços para discos geridos](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Preços dos discos de geridos Premium é a mesmo Olá os discos Premium não gerido. Mas preços para os discos padrão geridos são diferente de discos padrão de não gerido.


## <a name="next-steps"></a>Passos Seguintes

- Antes de carregar qualquer tooAzure VHD, deve seguir [preparar um tooAzure de tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
