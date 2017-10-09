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
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="cb1a1-103">Instalar MongoDB no Windows VM no Azure</span><span class="sxs-lookup"><span data-stu-id="cb1a1-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cb1a1-104">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="cb1a1-105">Este artigo abrange utilizando o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="cb1a1-106">A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="cb1a1-107">tooinstall e configurar o MongoDB utilizando o modelo de implementação do Resource Manager Olá, consulte [neste artigo](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="cb1a1-108">[MongoDB] [ MongoDB] é um popular open source e de elevado desempenho base de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="cb1a1-109">Este artigo orienta-o ao longo da criação de computador Windows Server virtual (VM) utilizando Olá [portal do Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="cb1a1-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="cb1a1-110">Em seguida, criar e anexar um toohello de disco de dados VM antes de instalar e configurar o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="cb1a1-111">Se tiver uma VM existente no Azure que pretende toouse, pode ir diretamente demasiado[instalar e configurar o MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="cb1a1-112">Criar uma máquina virtual que executa o Windows Server</span><span class="sxs-lookup"><span data-stu-id="cb1a1-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="cb1a1-113">Siga estas instruções toocreate uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="cb1a1-114">Pode adicionar um ponto final para o MongoDB ao criar a máquina virtual de Olá e configurá-lo da seguinte forma: nome como **Mongo**, utilize **TCP** como Olá protocolo e conjunto de ambos os Olá portas públicas e privadas demasiado**27017**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="cb1a1-115">Anexar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="cb1a1-115">Attach a data disk</span></span>
<span data-ttu-id="cb1a1-116">armazenamento de tooprovide para a máquina virtual de Olá, anexar um disco de dados e inicializá-lo para que o Windows pode utilizá-lo.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="cb1a1-117">Se já tiver um disco de dados, pode anexar esse disco existente, ou pode anexar um disco vazio.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="cb1a1-118">Para obter instruções sobre a inicializar disco Olá, consulte "como: iniciar um novo disco de dados no Windows Server" em [como tooattach dados de disco de máquina virtual do tooa Windows](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="cb1a1-119">Instalar e executar MongoDB na máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="cb1a1-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="cb1a1-120">Resumo</span><span class="sxs-lookup"><span data-stu-id="cb1a1-120">Summary</span></span>
<span data-ttu-id="cb1a1-121">Neste tutorial, aprendeu como toocreate uma máquina virtual com o Windows Server, remotamente ligar tooit e anexar um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="cb1a1-122">Também aprendeu como tooinstall e configurar o MongoDB na máquina de virtual baseado no Windows hello.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="cb1a1-123">Pode agora aceder MongoDB Olá baseados em Windows máquina virtual por seguintes Olá avançadas tópicos Olá [documentação do MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="cb1a1-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

