---
title: aaaAvailability define para VMs do Windows no Azure | Microsoft Docs
description: "Saiba mais sobre Olá chaves design e implementação diretrizes para a implementação de conjuntos de disponibilidade nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f9449f58-664b-4d5d-82f6-84c5d083047f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cc35fd1e913434d9facb94116edb1b1c30447c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-windows-vms"></a>Diretrizes de conjuntos de disponibilidade do Azure para as VMs do Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Este artigo incida no Olá compreender necessário passos de planeamento para conjuntos de disponibilidade tooensure as aplicações permanecem acessíveis durante eventos planeados ou imprevistos.

## <a name="implementation-guidelines-for-availability-sets"></a>Diretrizes de implementação para conjuntos de disponibilidade
Decisões:

* Quantos conjuntos de disponibilidade necessita para Olá vários escalões e funções na sua infraestrutura de aplicação?

Tarefas:

* Defina o número de Olá de VMs em cada camada de aplicação que necessita.
* Determine se necessita de tooadjust Olá diversas toobe de domínios de falhas ou atualização utilizado para a sua aplicação.
* Definir os conjuntos de disponibilidade de Olá necessário utilizar a Convenção de nomenclatura e que as VMs residem nos mesmos. Uma VM só pode residir num conjunto de disponibilidade de um.

## <a name="availability-sets"></a>Conjuntos de disponibilidade
No Azure, as máquinas virtuais (VMs) podem ser colocadas num agrupamento lógico tooa chamado um conjunto de disponibilidade. Quando criar as VMs dentro de um conjunto de disponibilidade, Olá plataforma Azure distribui colocação Olá dessas VMS Olá subjacente infraestrutura. Não existe deve ser um toohello de evento de manutenção planeada plataforma do Azure ou um hardware subjacente / falhas de infraestrutura, utilização de Olá de conjuntos de disponibilidade garante que, pelo menos, uma VM permanece em execução.

Como melhor prática, aplicações não devem residir numa única VM. Um conjunto de disponibilidade que contém uma única VM não obtém qualquer proteção a partir de eventos planeadas ou imprevistas dentro Olá plataforma Azure. Olá [SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines) requer dois ou mais VMs dentro de uma disponibilidade conjunto tooallow Olá distribuição de VMs entre Olá subjacente infraestrutura. Se estiver a utilizar [Premium Storage do Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Olá SLA do Azure aplica-se tooa única VM.

infraestrutura subjacente do Olá no Azure está dividida em clusters de hardware toomultiple. Cada cluster de hardware pode suportar um tamanhos de intervalo de VM. Um conjunto de disponibilidade só pode ser alojado num cluster único hardware em qualquer ponto no tempo. Por conseguinte, tamanhos de intervalo de VM de Olá que podem existir num conjunto de disponibilidade único é tamanhos de intervalo de VM de toohello limitado suportados pelo cluster de hardware Olá. cluster de hardware Olá Olá para conjunto de disponibilidade está selecionada quando hello primeira implementação da VM no conjunto de disponibilidade de Olá ou quando iniciar Olá primeira VM num conjunto de disponibilidade em que todas as VMs estão atualmente no estado parado-desalocada de Olá. Olá seguinte comando do PowerShell pode ser utilizados toodetermine Olá intervalo de VM tamanhos disponíveis para um conjunto de disponibilidade: "Get-AzureRmVMSize - ResourceGroupName \<cadeia\> - AvailabilitySetName \<cadeia\> "

Cada cluster de hardware está dividido em domínios de atualização de toomultiple e domínios de falhas. Estes domínios são definidos pelos quais anfitriões partilhar um ciclo de actualização da comuns ou partilha semelhante infraestrutura física, tais como a rede e de energia. Azure distribui automaticamente as VMs dentro de um conjunto de disponibilidade de toomaintain de domínios e tolerância a falhas de disponibilidade. Dependendo do tamanho de Olá da sua aplicação e o número de Olá de VMs dentro de um conjunto de disponibilidade, pode ajustar o número de Olá dos domínios desejar toouse. Pode ler mais sobre [gerir a disponibilidade e a utilização de domínios de atualização e falhas](manage-availability.md).

Ao conceber a sua infraestrutura de aplicação, planeie camadas da aplicação Olá que utilizar. VMs de grupo que servem Olá mesmo objetivo tooavailability conjuntos, tais como um conjunto de disponibilidade para as VMs de front-end que executa o IIS. Crie uma separado conjunto de disponibilidade para as VMs do back-end com o SQL Server. o objetivo de Olá é tooensure que cada componente da aplicação está protegido por um conjunto de disponibilidade e, pelo menos, uma vez instância sempre permanece em execução.

Balanceadores de carga podem ser utilizados à frente de cada toowork de camada de aplicação juntamente com um conjunto de disponibilidade e certifique-se de que o tráfego sempre pode ser encaminhada tooa executar instância. Sem um balanceador de carga, as suas VMs podem continuar a ser executado em todos os eventos de manutenção planeado e imprevisto, mas o utilizador final não pode ser capaz de tooresolve os se hello VM principal não está disponível.

Crie uma aplicação para elevada disponibilidade na camada de armazenamento. Olá procedimento recomendado é demasiado[utilizar discos geridos para as VMs num conjunto de disponibilidade](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Se estiver a utilizar discos não geridos, recomendamos vivamente demasiado[converter VMs no conjunto de disponibilidade toouse geridos discos](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]
