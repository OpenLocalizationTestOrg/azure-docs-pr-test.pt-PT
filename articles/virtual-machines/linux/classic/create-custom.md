---
title: "aaaCreate uma VM do Linux clássica utilizando Olá CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual do Linux com a utilização de Olá CLI do Azure 1.0 Olá modelo de implementação clássica"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>Como tooCreate uma VM com Linux clássico com Olá CLI do Azure 1.0
> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Para a versão do Gestor de recursos de Olá, consulte [aqui](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Este tópico descreve como toocreate Linux máquinas virtuais (VMS) com a utilização de Olá CLI do Azure 1.0 Olá modelo de implementação clássica. Utilizamos uma imagem de Linux do Olá disponível **imagens** no Azure. comandos de Olá CLI do Azure 1.0 dar Olá seguintes opções de configuração, entre outras pessoas:

* A ligação de rede virtual do Olá VM tooa
* Adicionar serviço de nuvem Olá VM tooan existente
* Adicionar conta de armazenamento Olá VM tooan existente
* Adicionar o conjunto de disponibilidade do Olá VM tooan ou localização

> [!IMPORTANT]
> Se pretender que a sua toouse VM numa rede virtual para que possa ligar tooit diretamente pelo nome de anfitrião ou configurar ligações entre locais, certifique-se de que especificar uma rede virtual Olá quando criar Olá VM. Uma VM pode ser configurado toojoin uma rede virtual, apenas quando são criados Olá VM. Para obter detalhes sobre redes virtuais, consulte [descrição geral de rede Virtual do Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>Como toocreate uma VM com Linux utilizando Olá modelo de implementação clássica
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

