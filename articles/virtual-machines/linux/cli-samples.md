---
title: aaaAzure amostras CLI | Microsoft Docs
description: Exemplos da CLI do Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a>Exemplos da CLI do Azure para máquinas virtuais do Linux

Olá tabela que se segue inclui ligações toobash scripts compiladas com Olá CLI do Azure.

| | |
|---|---|
|**Criar máquinas virtuais**||
| [Criar uma máquina virtual](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual Linux com configuração mínima. |
| [Criar uma máquina virtual totalmente configurada](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um grupo de recursos, a máquina virtual e todos os recursos relacionados.|
| [Criar máquinas virtuais altamente disponíveis](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | Cria várias máquinas virtuais da elevada disponibilidade e a configuração de balanceamento de carga. |
| [Criar uma VM com o Docker ativada](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual, configura esta VM como um anfitrião do Docker e executa um contentor NGINX. |
| [Criar uma VM e executar o script de configuração](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual e utiliza tooinstall de extensão de Script personalizado de Azure Olá NGINX. |
| [Criar uma VM com o WordPress instalado](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual e utiliza tooinstall de extensão de Script personalizado de Azure Olá WordPress. |
| [Criar uma VM a partir de um disco de SO gerido](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | Cria uma máquina virtual, anexar um disco existente geridos como disco do SO. |
| [Criar uma VM a partir de um instantâneo](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Cria uma máquina virtual a partir de um instantâneo ao primeiro criar um disco gerido de instantâneo e, em seguida, a anexar o disco geridos novo Olá como disco do SO. |
|**Gerir o armazenamento**||
| [Criar disco gerido a partir de um VHD](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | Cria um disco gerido a partir de um VHD especializado, como um disco do SO ou a partir de um VHD como disco de dados de dados.  |
| [Criar um disco gerido a partir de um instantâneo](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Cria um disco gerido a partir de um instantâneo. |
| [Copie o disco gerido toosame ou uma subscrição diferente](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Cópias geridas disco toosame ou uma subscrição diferente, mas no Olá mesma região principal Olá geridos disco. 
| [Exportar um instantâneo como conta de armazenamento do VHD tooa](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | Exporta um instantâneo gerido como conta de armazenamento do VHD tooa numa região diferente. |
| [Copiar toosame de instantâneo ou uma subscrição diferente](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Cópias instantâneo toosame ou outra subscrição mas no mesmo Olá região como instantâneo do Olá principal. |
|**Máquinas virtuais da rede**||
| [Proteger o tráfego de rede entre as máquinas virtuais](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | Cria duas máquinas virtuais, relacionados todos os recursos e uma grupos de segurança de rede internos e externos (NSG). |
|**Proteger máquinas virtuais**||
| [Encriptar uma VM e discos de dados](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Cria um cofre de chaves do Azure, uma chave de encriptação e um principal de serviço, em seguida, encripta uma VM. |
|**Monitorizar máquinas virtuais**||
| [Monitorizar uma VM com o Operations Management Suite](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | Cria uma máquina virtual, instala o agente do Operations Management Suite Olá e inscreve Olá VM com uma área de trabalho do OMS.  |
|**Resolver problemas relacionados com máquinas virtuais**||
| [Resolver problemas de um disco de sistema operativo de VMs](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | Monta disco do sistema operativo Olá a partir de uma VM como um disco de dados numa VM segundo. |
| | |
