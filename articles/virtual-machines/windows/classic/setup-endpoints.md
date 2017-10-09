---
title: "aaaSet dos pontos finais numa VM Windows clássico | Microsoft Docs"
description: "Saiba tooset dos pontos finais para uma VM do Windows no Olá comunicação tooallow de portal clássico do Azure com uma máquina virtual do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Como tooset dos pontos finais na máquina virtual clássico do Windows no Azure
Olá Windows todas as máquinas virtuais que criar no Azure utilizando o modelo de implementação clássica Olá automaticamente pode comunicar através de um canal de rede privada com outras máquinas virtuais no mesmo serviço em nuvem ou de rede virtual. No entanto, os computadores no Olá Internet ou outras redes virtuais necessitam pontos finais toodirect Olá rede entrada tráfego tooa máquina virtual. Este artigo também está disponível para [máquinas virtuais do Linux](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

No Olá **Resource Manager** modelo de implementação, pontos finais são configurados utilizando **grupos de segurança de rede (NSGs)**. Para obter mais informações, consulte [permitir acesso externo tooyour VM utilizando Olá portal do Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Quando cria uma máquina virtual do Windows no portal do Azure de Olá, pontos finais comuns, como os referentes ao ambiente de trabalho remoto e a comunicação remota do Windows PowerShell são normalmente criados por si automaticamente. Pode configurar os pontos finais adicionais ao criar a máquina virtual de Olá ou posteriormente, conforme necessário.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Passos seguintes
* toouse um tooset de cmdlet do PowerShell do Azure se um ponto final de VM, consulte [adicionar AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* toouse um toomanage de cmdlet do PowerShell do Azure uma ACL num ponto final, consulte [gerir acesso listas de controlo (ACLs) para pontos finais utilizando o PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* Se tiver criado uma máquina virtual no modelo de implementação do Resource Manager Olá, pode utilizar o Azure PowerShell demasiado[criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol tráfego toohello VM.
