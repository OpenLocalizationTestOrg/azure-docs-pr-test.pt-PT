---
title: "aaaCreate uma VM no Olá portal do Azure | Microsoft Docs"
description: "Crie uma máquina virtual do Windows no Olá portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Criar uma máquina virtual com o Windows hello portal do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](tutorial.md)
> * [PowerShell: Implementação clássica](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Saiba como demasiado[executar estes passos, utilizando o modelo de implementação do Resource Manager Olá](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) utilizando Olá **portal do Azure**.

Este tutorial mostra como toocreate um Azure máquina virtual (VM) com o Windows hello portal do Azure. Utilizaremos uma imagem do Windows Server como exemplo, mas esta é apenas uma das Olá muitas imagens ofertas do Azure. Tenha em atenção que as suas opções de imagem dependem da sua subscrição. Por exemplo, imagens de ambiente de trabalho do Windows podem ser subscritores tooMSDN disponíveis.

Esta secção mostra-lhe como toouse Olá **Dashboard** no Olá tooselect portal do Azure e, em seguida, criar máquina virtual de Olá.

Também pode criar VMs utilizando [as suas próprias imagens](createupload-vhd.md). toolearn acerca desta e de outros métodos, consulte [diferentes formas toocreate máquina virtual do Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Criar máquina virtual de Olá
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[criar uma VM utilizando o modelo de implementação do Resource Manager Olá](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) no Olá portal do Azure.
* Inicie sessão na máquina virtual de toohello. Para obter instruções, consulte [iniciar sessão na máquina de virtual tooa com o Windows Server](connect-logon.md).
* Anexe um toostore de dados do disco. Pode anexar vazios discos e os discos que contêm dados. Para obter instruções, consulte Olá [anexar dados disco tooa máquina virtual do Windows criada com o modelo de implementação clássica Olá](attach-disk.md).
