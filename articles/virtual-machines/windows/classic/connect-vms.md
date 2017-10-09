---
title: "aaaConnect VMs do Windows num serviço em nuvem | Microsoft Docs"
description: "Ligar máquinas virtuais do Windows criadas com tooan de modelo de implementação clássica Olá serviço em nuvem do Azure ou de rede virtual."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c1cbc802-4352-4d2e-9e49-4ccbd955324b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: d19dc555694eab8a7e790c970cfb5e6a53aa7a7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-virtual-machines-created-with-hello-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a>Ligar máquinas virtuais do Windows criadas com o modelo de implementação clássica Olá com um serviço de nuvem ou de rede virtual
> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

Máquinas virtuais do Windows criadas com o modelo de implementação clássica Olá sempre são colocadas num serviço em nuvem. o serviço em nuvem Olá age como um contentor e fornece um nome exclusivo de DNS público, um endereço IP público e um conjunto de pontos finais tooaccess Olá máquina através de Olá Internet. serviço de nuvem de Olá pode estar numa rede virtual, mas que não é um requisito. Também pode [ligar máquinas virtuais do Linux com um serviço de nuvem ou de rede virtual](../../linux/classic/connect-vms.md).

Se não for um serviço em nuvem numa rede virtual, é chamado um *autónomo* serviço em nuvem. as máquinas virtuais de Olá num serviço autónomo em nuvem comunicam com outras máquinas virtuais utilizando Olá nomes DNS públicos dos outras máquinas virtuais e tráfego de Olá percorre Olá Internet. Se um serviço em nuvem numa rede virtual, Olá máquinas de virtuais na medida em que o serviço em nuvem pode comunicar com todas as outras máquinas virtuais na rede virtual Olá sem enviar qualquer tráfego através de Olá Internet.

Se colocar Olá, as máquinas virtuais no mesmo serviço de nuvem autónomo, pode continuar a utilizar o balanceamento de carga e conjuntos de disponibilidade. Para obter mais informações, consulte [máquinas virtuais de balanceamento de carga](../../virtual-machines-windows-load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gerir a disponibilidade de Olá das máquinas virtuais](../../virtual-machines-windows-manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). No entanto, não é possível organizar Olá máquinas de virtuais em sub-redes ou ligar uma rede de no local tooyour de serviço de nuvem de autónomo. Eis um exemplo:

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a>Passos seguintes
Depois de criar uma máquina virtual, é uma boa ideia demasiado[adicionar um disco de dados](attach-disk.md) para que os seus serviços e as cargas de trabalho tem dados de toostore uma localização.
