---
title: aaaInstall MongoDB numa VM do Windows no Azure | Microsoft Docs
description: "Saiba como tooinstall MongoDB numa VM do Azure criado com o modelo de implementação clássica Olá com o Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Instalar MongoDB no Windows VM no Azure
> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).  Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. tooinstall e configurar o MongoDB utilizando o modelo de implementação do Resource Manager Olá, consulte [neste artigo](../install-mongodb.md).

[MongoDB] [ MongoDB] é um popular open source e de elevado desempenho base de dados NoSQL. Este artigo orienta-o ao longo da criação de computador Windows Server virtual (VM) utilizando Olá [portal do Azure][AzurePortal]. Em seguida, criar e anexar um toohello de disco de dados VM antes de instalar e configurar o MongoDB. Se tiver uma VM existente no Azure que pretende toouse, pode ir diretamente demasiado[instalar e configurar o MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Criar uma máquina virtual que executa o Windows Server
Siga estas instruções toocreate uma máquina virtual.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> Pode adicionar um ponto final para o MongoDB ao criar a máquina virtual de Olá e configurá-lo da seguinte forma: nome como **Mongo**, utilize **TCP** como Olá protocolo e conjunto de ambos os Olá portas públicas e privadas demasiado**27017**.
>
>

## <a name="attach-a-data-disk"></a>Anexar um disco de dados
armazenamento de tooprovide para a máquina virtual de Olá, anexar um disco de dados e inicializá-lo para que o Windows pode utilizá-lo. Se já tiver um disco de dados, pode anexar esse disco existente, ou pode anexar um disco vazio.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Para obter instruções sobre a inicializar disco Olá, consulte "como: iniciar um novo disco de dados no Windows Server" em [como tooattach dados de disco de máquina virtual do tooa Windows](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Instalar e executar MongoDB na máquina virtual de Olá
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Resumo
Neste tutorial, aprendeu como toocreate uma máquina virtual com o Windows Server, remotamente ligar tooit e anexar um disco de dados.  Também aprendeu como tooinstall e configurar o MongoDB na máquina de virtual baseado no Windows hello. Pode agora aceder MongoDB Olá baseados em Windows máquina virtual por seguintes Olá avançadas tópicos Olá [documentação do MongoDB][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

