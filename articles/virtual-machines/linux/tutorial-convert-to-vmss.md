---
title: aaaConvert um Azure tooa do conjunto de dimensionamento | Microsoft Docs
description: "Criar e implementar um dimensionamento da máquina virtual do Azure do Linux com Olá CLI do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="642cb-103">Converter um conjunto de dimensionamento de tooa de máquina virtual do Azure existente</span><span class="sxs-lookup"><span data-stu-id="642cb-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="642cb-104">Este tutorial mostra como toouse Azure CLI 2.0 tooconvert definir um dimensionamento de máquina virtual de tooa da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="642cb-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="642cb-105">Também Saiba como definir a configuração de Olá tooautomate das máquinas de virtuais Olá na escala de Olá.</span><span class="sxs-lookup"><span data-stu-id="642cb-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="642cb-106">Para mais informações sobre como tooinstall CLI do Azure 2.0, consulte o artigo [introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="642cb-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="642cb-107">Para mais informações sobre conjuntos de dimensionamento, consulte [conjuntos de dimensionamento de Máquina Virtual](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="642cb-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="642cb-108">Passo 1 – desaprovisionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="642cb-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="642cb-109">Utilize o SSH tooconnect toohello VM.</span><span class="sxs-lookup"><span data-stu-id="642cb-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="642cb-110">Olá deprovision VM Olá VM do Azure agente toodelete ficheiros e dados a utilizar.</span><span class="sxs-lookup"><span data-stu-id="642cb-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="642cb-111">Para obter uma descrição detalhada do desaprovisionamento, consulte [capturar uma máquina virtual Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="642cb-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="642cb-112">Passo 2 - capturar uma imagem de Olá VM</span><span class="sxs-lookup"><span data-stu-id="642cb-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="642cb-113">Para obter uma descrição detalhada de captura, consulte [capturar uma máquina virtual Linux](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="642cb-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="642cb-114">Desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="642cb-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="642cb-115">Generalizar Olá VM com [az vm Generalizar](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="642cb-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="642cb-116">Criar uma imagem do recurso de VM Olá com [criar imagem az](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="642cb-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="642cb-117">Passo 3 – criar conjunto de dimensionamento de Olá</span><span class="sxs-lookup"><span data-stu-id="642cb-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="642cb-118">Obter Olá **id** da imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="642cb-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="642cb-119">Criar uma VM a partir do seu recurso de imagem com [az vmss criar](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="642cb-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="642cb-120">Este comando também ligado um disco de dados de 10gb.</span><span class="sxs-lookup"><span data-stu-id="642cb-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="642cb-121">Tenha em atenção que, consoante Olá VM tamanho escolhida (utilizámos **Standard_DS1_v2**), número de Olá de discos de dados permitidas é diferente.</span><span class="sxs-lookup"><span data-stu-id="642cb-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="642cb-122">Para obter mais informações, consulte Olá [tamanhos de máquina virtual](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="642cb-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="642cb-123">Depois de o conjunto de dimensionamento de Olá depois de concluída, ligar tooit.</span><span class="sxs-lookup"><span data-stu-id="642cb-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="642cb-124">Obter uma lista de endereços IP para instâncias de Olá para SSH com [az vmss lista-instância--informações de ligação](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="642cb-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="642cb-125">Agora pode ligar o disco de dados de Olá instância tooinitialize toohello máquina virtual</span><span class="sxs-lookup"><span data-stu-id="642cb-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="642cb-126">Passo 4 - disco de dados de Olá inicializar</span><span class="sxs-lookup"><span data-stu-id="642cb-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="642cb-127">Enquanto a máquina virtual de toohello ligado, particionar o disco de Olá com `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="642cb-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="642cb-128">Escrever uma partição de toohello do sistema de ficheiros com Olá `mkfs` comando:</span><span class="sxs-lookup"><span data-stu-id="642cb-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="642cb-129">Monte o disco novo Olá para que seja acessível no sistema de operativo Olá:</span><span class="sxs-lookup"><span data-stu-id="642cb-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="642cb-130">disco Olá pode agora ser acede através de Olá datadrive pontodemontagem, que pode ser verificado com `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="642cb-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="642cb-131">Termine a sessão SSH Olá.</span><span class="sxs-lookup"><span data-stu-id="642cb-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="642cb-132">Passo 5 - configurar a firewall</span><span class="sxs-lookup"><span data-stu-id="642cb-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="642cb-133">Punch um negro através de Olá firewall toohello webserver alojada pelo conjunto de dimensionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="642cb-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="642cb-134">Quando foi criado o conjunto de dimensionamento de Olá, também foi criado a um balanceador de carga e utilizou- **SSH** toohello máquinas de virtuais individuais.</span><span class="sxs-lookup"><span data-stu-id="642cb-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="642cb-135">tooopen uma porta, terá de dois tipos de informações, que pode obter utilizando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="642cb-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="642cb-136">**Conjunto de endereços IP de front-end**</span><span class="sxs-lookup"><span data-stu-id="642cb-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="642cb-137">**Conjunto de endereços de IP back-end**</span><span class="sxs-lookup"><span data-stu-id="642cb-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="642cb-138">Com os dois nomes, pode abrir a porta **80**.</span><span class="sxs-lookup"><span data-stu-id="642cb-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="642cb-139">Passo 6 - automatizar a configuração</span><span class="sxs-lookup"><span data-stu-id="642cb-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="642cb-140">o disco de dados de Olá tem toobe configurada em cada instância de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="642cb-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="642cb-141">Iremos pode automatizar a configuração de Olá da máquina virtual de Olá com Olá **CustomScript** extensão.</span><span class="sxs-lookup"><span data-stu-id="642cb-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="642cb-142">Em primeiro lugar, crie um *.sh* script que inclui os comandos de formato de disco Olá.</span><span class="sxs-lookup"><span data-stu-id="642cb-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="642cb-143">Em seguida, carregue esse Olá de toowhere do ficheiro de script **CustomScript** extensão consegue aceder-lhe.</span><span class="sxs-lookup"><span data-stu-id="642cb-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="642cb-144">Uma cópia está disponível [aqui](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="642cb-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="642cb-145">Criar um ficheiro local com o nome **settings.json** e coloque hello os seguintes blocos JSON no mesmo.</span><span class="sxs-lookup"><span data-stu-id="642cb-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="642cb-146">Olá `flieUris` propriedade deve ser definida toowhere foi carregado o ficheiro de script para.</span><span class="sxs-lookup"><span data-stu-id="642cb-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="642cb-147">Implementar o dimensionamento de tooyour este comando com Olá **CustomScript** extensão, referenciar Olá **settings.json** ficheiro acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="642cb-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="642cb-148">Esta extensão é executado automaticamente em todas as instâncias atuais e quaisquer instâncias mais tarde criadas pelo dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="642cb-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="642cb-149">Passo 7 – configurar regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="642cb-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="642cb-150">Atualmente, as regras de dimensionamento automático não podem ser definidas na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="642cb-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="642cb-151">Olá utilize [portal do Azure](https://portal.azure.com) dimensionamento automático de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="642cb-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="642cb-152">Passo 8 - as tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="642cb-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="642cb-153">Ao longo do ciclo de vida de Olá de conjunto de dimensionamento de Olá, poderá ser necessário toorun uma ou mais tarefas de gestão.</span><span class="sxs-lookup"><span data-stu-id="642cb-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="642cb-154">Além disso, poderá ser útil toocreate scripts que automatizem várias tarefas de ciclo de vida e Olá CLI do Azure fornece uma forma rápida toodo essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="642cb-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="642cb-155">Seguem-se algumas tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="642cb-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="642cb-156">Obter as informações de ligação</span><span class="sxs-lookup"><span data-stu-id="642cb-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="642cb-157">Contagem de instâncias do conjunto (dimensionamento manual)</span><span class="sxs-lookup"><span data-stu-id="642cb-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="642cb-158">Eliminar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="642cb-158">Delete resource group</span></span>

<span data-ttu-id="642cb-159">Também eliminar um grupo de recursos elimina todos os recursos contidos.</span><span class="sxs-lookup"><span data-stu-id="642cb-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="642cb-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="642cb-160">Next steps</span></span>
<span data-ttu-id="642cb-161">toolearn mais informações sobre algumas das dimensionamento da máquina virtual Olá definir funcionalidades introduzidas neste tutorial, consulte Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="642cb-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="642cb-162">Descrição geral de conjuntos de dimensionamento de Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="642cb-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="642cb-163">Descrição Geral do Balanceador de Carga do Azure (Azure Load Balancer overview)</span><span class="sxs-lookup"><span data-stu-id="642cb-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="642cb-164">Controlar o fluxo de tráfego de rede com grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="642cb-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)