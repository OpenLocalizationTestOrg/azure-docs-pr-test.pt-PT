---
title: aaaAvailability define tutorial para VMs com Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá conjuntos de disponibilidade para VMs com Linux no Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="b8dde-103">Como disponibilidade toouse define</span><span class="sxs-lookup"><span data-stu-id="b8dde-103">How toouse availability sets</span></span>


<span data-ttu-id="b8dde-104">Neste tutorial, ficará a saber como disponibilidade de Olá tooincrease e a fiabilidade das suas soluções de Máquina Virtual no Azure através de uma capacidade chamado conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b8dde-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="b8dde-105">Conjuntos de disponibilidade Certifique-se de que Olá VMs implementar no Azure estão distribuídas em vários clusters hardware isolado.</span><span class="sxs-lookup"><span data-stu-id="b8dde-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="b8dde-106">Fazer isto garante que se ocorre uma falha de hardware ou software no Azure, apenas um conjunto secundárias das suas VMs será afetado e que a solução global permanecerá disponível e operacional da perspetiva de Olá dos seus clientes utilizá-la.</span><span class="sxs-lookup"><span data-stu-id="b8dde-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="b8dde-107">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="b8dde-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8dde-108">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b8dde-108">Create an availability set</span></span>
> * <span data-ttu-id="b8dde-109">Criar uma VM num conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b8dde-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="b8dde-110">Verifique os tamanhos VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="b8dde-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b8dde-111">Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b8dde-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b8dde-112">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="b8dde-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b8dde-113">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b8dde-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="b8dde-114">Descrição geral do conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b8dde-114">Availability set overview</span></span>

<span data-ttu-id="b8dde-115">Um conjunto de disponibilidade é uma capacidade de agrupamento lógico que pode utilizar no Azure tooensure que estão isolados umas das outras Olá VM recursos que colocar dentro do mesmo quando estão implementadas dentro de um datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8dde-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="b8dde-116">Azure garante que Olá VMs colocar dentro de um conjunto de disponibilidade sejam executadas em vários servidores físicos, computação bastidores, unidades de armazenamento e comutadores de rede.</span><span class="sxs-lookup"><span data-stu-id="b8dde-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="b8dde-117">Isto garante que no evento Olá de um hardware ou a falha de software do Azure, apenas um subconjunto das suas VMs será afetado, e global da sua aplicação irá manter cópias de segurança e continuar toobe tooyour disponíveis clientes.</span><span class="sxs-lookup"><span data-stu-id="b8dde-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="b8dde-118">Utilizar conjuntos de disponibilidade é um tooleverage capacidade essencial quando quiser toobuild soluções de nuvem fiável.</span><span class="sxs-lookup"><span data-stu-id="b8dde-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="b8dde-119">Vejamos uma típica VM solução baseada em que poderá ter 4 servidores de web de front-end e utilize 2 VMs de back-end que aloja uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="b8dde-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="b8dde-120">Com o Azure, seria aconselhável toodefine dois conjuntos de disponibilidade antes de implementar as suas VMs: conjunto de disponibilidade de uma camada de "web" Olá e um conjunto de disponibilidade para camada de "base de dados" Olá.</span><span class="sxs-lookup"><span data-stu-id="b8dde-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="b8dde-121">Quando cria uma nova VM, em seguida, pode especificar disponibilidade Olá definida como comando de criar uma vm do parâmetro toohello az e Azure será automaticamente Certifique-se de que Olá VMs que cria no Olá disponível conjunto são isoladas entre vários recursos de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="b8dde-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="b8dde-122">Isto significa que se o hardware físico Olá que o servidor Web ou VMs do servidor de base de dados está em execução no tem um problema, sabe que Olá outras instâncias do servidor Web e da base de dados VMs continuará em execução ajustar porque estão num hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="b8dde-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="b8dde-123">Deve sempre utilizar conjuntos de disponibilidade quando quiser toodeploy fiável VM soluções baseadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="b8dde-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="b8dde-124">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b8dde-124">Create an availability set</span></span>

<span data-ttu-id="b8dde-125">Pode criar um conjunto através de disponibilidade [az vm conjunto de disponibilidade criar](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="b8dde-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="b8dde-126">Neste exemplo, vamos definir ambos os número de Olá de domínios de atualização e de falhas em *2* para o conjunto nomeada de disponibilidade de Olá *myAvailabilitySet* no Olá *myResourceGroupAvailability*grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8dde-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="b8dde-127">Crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8dde-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="b8dde-128">Conjuntos de disponibilidade permitem-lhe tooisolate recursos em "domínios de falhas" e "domínios de atualização".</span><span class="sxs-lookup"><span data-stu-id="b8dde-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="b8dde-129">A **domínio de falhas** representa uma coleção isolada do servidor + rede + armazenamento recursos.</span><span class="sxs-lookup"><span data-stu-id="b8dde-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="b8dde-130">Nos Olá anterior exemplo, vamos indicar que queremos que nosso disponibilidade definido toobe distribuído, pelo menos, dois domínios de falhas quando os nossas VMs são implementadas.</span><span class="sxs-lookup"><span data-stu-id="b8dde-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="b8dde-131">Também iremos indicar que queremos nosso conjunto distribuída em dois de disponibilidade **domínios de atualização**.</span><span class="sxs-lookup"><span data-stu-id="b8dde-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="b8dde-132">Dois domínios de atualização Certifique-se de que quando o Azure executa as atualizações de software nosso recursos VM isolados, impedir de todo o software Olá executando por baixo do nosso VM a partir de que está a ser atualizada no Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="b8dde-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="b8dde-133">Configurar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="b8dde-133">Configure virtual network</span></span>
<span data-ttu-id="b8dde-134">Antes de implementar algumas VMs e pode testar o seu balanceador, crie Olá suporte recursos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b8dde-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="b8dde-135">Para obter mais informações sobre as redes virtuais, consulte Olá [gerir redes virtuais do Azure](tutorial-virtual-network.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b8dde-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="b8dde-136">Criar recursos de rede</span><span class="sxs-lookup"><span data-stu-id="b8dde-136">Create network resources</span></span>
<span data-ttu-id="b8dde-137">Criar uma rede virtual com [az rede vnet criar](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="b8dde-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="b8dde-138">Olá exemplo seguinte cria uma rede virtual denominada *myVnet* com uma sub-rede denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="b8dde-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="b8dde-139">NICs virtuais são criados com [nic da rede az criar](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b8dde-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="b8dde-140">Olá exemplo seguinte cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="b8dde-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="b8dde-141">(Uma NIC virtual para cada VM criar para a aplicação no Olá seguindo os passos).</span><span class="sxs-lookup"><span data-stu-id="b8dde-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="b8dde-142">Pode criar o NICs virtuais adicionais e VMs em qualquer altura e adicioná-los toohello Balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="b8dde-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="b8dde-143">Criar VMs dentro de um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b8dde-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="b8dde-144">As VMs têm de ser criadas no toomake de conjunto de disponibilidade de Olá se que corretamente estão distribuídos hardware Olá.</span><span class="sxs-lookup"><span data-stu-id="b8dde-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="b8dde-145">Não é possível adicionar um existente VM tooan conjunto de disponibilidade depois de criado.</span><span class="sxs-lookup"><span data-stu-id="b8dde-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="b8dde-146">Quando cria uma VM utilizando [az vm criar](/cli/azure/vm#create) especificar disponibilidade Olá definida utilizando Olá `--availability-set` toospecify Olá o nome do parâmetro de conjunto de disponibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="b8dde-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="b8dde-147">Iremos agora, tem duas máquinas virtuais no nosso conjunto de disponibilidade criado recentemente.</span><span class="sxs-lookup"><span data-stu-id="b8dde-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="b8dde-148">Porque estão em Olá mesmo conjunto de disponibilidade, o Azure irá garantir que VMs Olá e todos os respetivos recursos (incluindo os discos de dados) estão distribuídos isolado hardware físico.</span><span class="sxs-lookup"><span data-stu-id="b8dde-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="b8dde-149">Esta distribuição ajuda Certifique-se muito maior disponibilidade da nossa solução global de VM.</span><span class="sxs-lookup"><span data-stu-id="b8dde-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="b8dde-150">Um aspeto que poderá encontrar à medida que adiciona VMs é que um determinado tamanho da VM já não está disponível toouse dentro do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b8dde-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="b8dde-151">Este problema pode ocorrer se já não é suficiente tooadd de capacidade, mantendo o conjunto de disponibilidade do Olá isolamento regras Olá impõe.</span><span class="sxs-lookup"><span data-stu-id="b8dde-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="b8dde-152">Pode verificar toosee os tamanhos VM são toouse disponível dentro de um conjunto utilizando Olá de disponibilidade existente `--availability-set list-sizes` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b8dde-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="b8dde-153">Verifique a existência de tamanhos VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="b8dde-153">Check for available VM sizes</span></span> 

<span data-ttu-id="b8dde-154">Pode adicionar mais VMs toohello conjunto de disponibilidade mais tarde, mas tem tooknow tamanhos de VM que estão disponíveis no hardware de Olá.</span><span class="sxs-lookup"><span data-stu-id="b8dde-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="b8dde-155">Utilize [lista-tamanhos do conjunto de disponibilidade de vm az](/cli/azure/availability-set#list-sizes) toolist todos os tamanhos disponíveis Olá no hardware de Olá cluster Olá para conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b8dde-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="b8dde-156">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b8dde-156">Next steps</span></span>

<span data-ttu-id="b8dde-157">Neste tutorial, ficou a saber como:</span><span class="sxs-lookup"><span data-stu-id="b8dde-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8dde-158">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b8dde-158">Create an availability set</span></span>
> * <span data-ttu-id="b8dde-159">Criar uma VM num conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="b8dde-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="b8dde-160">Verifique os tamanhos VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="b8dde-160">Check available VM sizes</span></span>

<span data-ttu-id="b8dde-161">Produzir toohello seguinte toolearn tutorial sobre conjuntos de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b8dde-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b8dde-162">Criar um conjunto de dimensionamento de VM</span><span class="sxs-lookup"><span data-stu-id="b8dde-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

