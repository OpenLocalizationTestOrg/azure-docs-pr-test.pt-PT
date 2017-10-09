---
title: "aaaSet dos pontos finais de uma VM com Linux clássico | Microsoft Docs"
description: "Saiba mais tooset dos pontos finais para uma VM com Linux no Olá comunicação tooallow de portal clássico do Azure com uma máquina virtual do Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a>Como tooset dos pontos finais numa máquina virtual clássico Linux no Azure
Todas as máquinas virtuais do Linux que criar no Azure utilizando o modelo de implementação clássica Olá automaticamente comunicar através de um canal de rede privada com outras máquinas virtuais na Olá que mesma rede virtual ou serviço da nuvem. No entanto, os computadores no Olá Internet ou outras redes virtuais necessitam pontos finais toodirect Olá rede entrada tráfego tooa máquina virtual. Este artigo também está disponível para [máquinas virtuais Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

No Olá **Resource Manager** modelo de implementação, pontos finais são configurados utilizando **grupos de segurança de rede (NSGs)**. Para obter mais informações, consulte [abrir portas e os pontos finais](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Quando cria uma máquina virtual Linux no Olá portal do Azure, um ponto final de Secure Shell (SSH) é normalmente criado automaticamente. Pode configurar os pontos finais adicionais ao criar a máquina virtual de Olá ou posteriormente, conforme necessário.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Passos seguintes
* Também pode criar um ponto final da VM utilizando Olá [Interface de linha de comandos do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). Executar Olá **criar o ponto final de vm do azure** comando.
* Se tiver criado uma máquina virtual no modelo de implementação do Resource Manager Olá, pode utilizar Olá CLI do Azure no modo Resource Manager demasiado[criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol tráfego toohello VM.
