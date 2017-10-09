---
title: "aaaCreate conjuntos de dimensionamento de Máquina Virtual para Linux no Azure | Microsoft Docs"
description: "Criar e implementar uma aplicação altamente disponível em VMs do Linux utilizando um conjunto de dimensionamento de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="9797c-103">Criar um conjunto de dimensionamento de Máquina Virtual e implementar uma aplicação altamente disponível no Linux</span><span class="sxs-lookup"><span data-stu-id="9797c-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="9797c-104">Um conjunto de dimensionamento de máquina virtual permite-lhe toodeploy e gerir um conjunto de máquinas virtuais idênticas de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="9797c-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="9797c-105">Pode dimensionar o número de Olá de VMs no conjunto de dimensionamento de Olá manualmente ou definir tooautoscale regras com base na utilização de CPU, a pedido de memória ou tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="9797c-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="9797c-106">Neste tutorial, implementa um conjunto no Azure de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9797c-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="9797c-107">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="9797c-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9797c-108">Utilizar a cloud init toocreate tooscale uma aplicação</span><span class="sxs-lookup"><span data-stu-id="9797c-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="9797c-109">Criar um conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9797c-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="9797c-110">Aumentar ou diminuir o número de Olá de instâncias de um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="9797c-111">Ver informações de ligação para as instâncias do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="9797c-112">Utilizar discos de dados num conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9797c-113">Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9797c-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9797c-114">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="9797c-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9797c-115">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9797c-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="9797c-116">Descrição geral do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-116">Scale Set overview</span></span>
<span data-ttu-id="9797c-117">Um conjunto de dimensionamento de máquina virtual permite-lhe toodeploy e gerir um conjunto de máquinas virtuais idênticas de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="9797c-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="9797c-118">Conjuntos de dimensionamento Olá utilize componentes mesmos como aprendeu sobre tutorial anterior Olá demasiado[criar VMs de elevada](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="9797c-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="9797c-119">As VMs num conjunto de dimensionamento são criadas num conjunto e distribuídos por domínios de falhas e de atualização de lógica de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="9797c-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="9797c-120">As VMs são criadas conforme necessário de um conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9797c-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="9797c-121">Definir dimensionamento automático regras toocontrol como e quando VMs são adicionadas ou removidas do conjunto de dimensionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="9797c-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="9797c-122">Estas regras podem acionar com base nas métricas, tais como a carga de CPU, utilização de memória ou tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="9797c-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="9797c-123">Os conjuntos de dimensionamento suporte cópias de segurança too1, 000 VMs ao utilizar uma imagem de plataforma do Azure.</span><span class="sxs-lookup"><span data-stu-id="9797c-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="9797c-124">Para cargas de trabalho de produção, pode ser útil demasiado[criar uma imagem VM personalizada](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="9797c-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="9797c-125">Pode criar cópias de segurança too100 VMs na escala definido quando utilizar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="9797c-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="9797c-126">Criar uma aplicação tooscale</span><span class="sxs-lookup"><span data-stu-id="9797c-126">Create an app tooscale</span></span>
<span data-ttu-id="9797c-127">Para utilização em produção, pode ser útil demasiado[criar uma imagem VM personalizada](tutorial-custom-images.md) que inclui a aplicação instalada e configurada.</span><span class="sxs-lookup"><span data-stu-id="9797c-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="9797c-128">Para este tutorial, permite personalizar Olá que VMS no primeiro arranque tooquickly ver um conjunto em ação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9797c-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="9797c-129">Um tutorial anterior, aprendeu [como toocustomize uma máquina virtual do Linux no primeiro arranque](tutorial-automate-vm-deployment.md) com init de nuvem.</span><span class="sxs-lookup"><span data-stu-id="9797c-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="9797c-130">Pode utilizar Olá tooinstall de ficheiro mesma configuração de nuvem init NGINX e executar uma aplicação Node.js "Olá, mundo" simples.</span><span class="sxs-lookup"><span data-stu-id="9797c-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="9797c-131">Na sua shell atual, crie um ficheiro denominado *nuvem init.txt* e colar Olá seguindo a configuração.</span><span class="sxs-lookup"><span data-stu-id="9797c-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="9797c-132">Por exemplo, crie o ficheiro de Olá no Olá Shell na nuvem não no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="9797c-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="9797c-133">Introduza `sensible-editor cloud-init.txt` toocreate Olá ficheiro e ver uma lista de editores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="9797c-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="9797c-134">Certifique-se de que o ficheiro init de nuvem todo Olá foi corretamente copiado, Olá especialmente a primeira linha:</span><span class="sxs-lookup"><span data-stu-id="9797c-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a><span data-ttu-id="9797c-135">Criar um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-135">Create a scale set</span></span>
<span data-ttu-id="9797c-136">Antes de poder criar um conjunto de dimensionamento, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9797c-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9797c-137">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupScaleSet* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="9797c-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="9797c-138">Agora criar um conjunto com de dimensionamento de máquina virtual [az vmss criar](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="9797c-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="9797c-139">Olá exemplo seguinte cria um conjunto nomeado de dimensionamento *myScaleSet*, utiliza Olá do Olá nuvem init ficheiro toocustomize VM e gera chaves SSH, caso não existam:</span><span class="sxs-lookup"><span data-stu-id="9797c-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="9797c-140">Este demora alguns minutos toocreate e configurar todos os recursos de conjunto de dimensionamento de Olá e VMs.</span><span class="sxs-lookup"><span data-stu-id="9797c-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="9797c-141">Existem tarefas em segundo plano que continue toorun após Olá CLI do Azure devolve toohello linha.</span><span class="sxs-lookup"><span data-stu-id="9797c-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="9797c-142">Pode ser outro alguns minutos antes de poder aceder Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="9797c-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="9797c-143">Permitir o tráfego da web</span><span class="sxs-lookup"><span data-stu-id="9797c-143">Allow web traffic</span></span>
<span data-ttu-id="9797c-144">Foi criado automaticamente como parte do conjunto de dimensionamento de máquina virtual de Olá a um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="9797c-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="9797c-145">Balanceador de carga Olá distribui o tráfego por um conjunto de VMs definidos através de regras de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="9797c-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="9797c-146">Pode saber mais sobre conceitos de Balanceador de carga e a configuração no próximo tutorial Olá, [como tooload equilibrar as máquinas virtuais no Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="9797c-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="9797c-147">tooallow tráfego tooreach Olá web app, crie uma regra com [criar regra de lb az rede](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="9797c-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="9797c-148">Olá exemplo seguinte cria uma regra com o nome *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="9797c-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="9797c-149">Testar a aplicação</span><span class="sxs-lookup"><span data-stu-id="9797c-149">Test your app</span></span>
<span data-ttu-id="9797c-150">toosee à aplicação Node.js na web Olá, obter o endereço IP público de Olá do seu Balanceador de carga com [mostrar de ip público de rede az](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="9797c-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="9797c-151">Olá exemplo seguinte obtém o endereço IP Olá *myScaleSetLBPublicIP* criada como parte do conjunto de dimensionamento de Olá:</span><span class="sxs-lookup"><span data-stu-id="9797c-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="9797c-152">Introduza o endereço IP público Olá no tooa browser.</span><span class="sxs-lookup"><span data-stu-id="9797c-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="9797c-153">aplicação de Olá é apresentada, incluindo o nome de anfitrião de Olá do Olá VM que Olá de carga do tráfego do Balanceador distribuída para:</span><span class="sxs-lookup"><span data-stu-id="9797c-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Aplicação Node.js em execução](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="9797c-155">toosee Olá conjunto de dimensionamento em ação, pode forçar atualização a carga do web browser toosee Olá balanceador distribuir o tráfego entre todas as VMs de Olá executar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="9797c-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="9797c-156">Tarefas de gestão</span><span class="sxs-lookup"><span data-stu-id="9797c-156">Management tasks</span></span>
<span data-ttu-id="9797c-157">Ao longo do ciclo de vida de Olá de conjunto de dimensionamento de Olá, poderá ser necessário toorun uma ou mais tarefas de gestão.</span><span class="sxs-lookup"><span data-stu-id="9797c-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="9797c-158">Além disso, poderá ser útil toocreate scripts que automatizem várias tarefas de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="9797c-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="9797c-159">Olá 2.0 de CLI do Azure fornece uma forma rápida toodo essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="9797c-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="9797c-160">Seguem-se algumas tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="9797c-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="9797c-161">Vista VMs num conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-161">View VMs in a scale set</span></span>
<span data-ttu-id="9797c-162">definir uma lista de VMs em execução no seu dimensionamento de tooview, utilize [az vmss-instâncias da lista](/cli/azure/vmss#list-instances) da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="9797c-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="9797c-163">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9797c-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="9797c-164">Aumentar ou diminuir instâncias de VM</span><span class="sxs-lookup"><span data-stu-id="9797c-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="9797c-165">toosee Olá diversas instâncias atualmente tem num conjunto de dimensionamento, utilize [mostrar de vmss az](/cli/azure/vmss#show) e consultar no *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="9797c-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="9797c-166">Pode, em seguida, manualmente aumentar ou diminuir o número de Olá das máquinas virtuais em conjunto com de dimensionamento de Olá [escala de vmss az](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="9797c-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="9797c-167">Olá exemplo a seguir define Olá número de VMs no seu dimensionamento definido demasiado*5*:</span><span class="sxs-lookup"><span data-stu-id="9797c-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="9797c-168">Regras de dimensionamento automático permitem-lhe definir como tooscale ou reduzir verticalmente o número de Olá de VMs no seu dimensionamento definido na resposta toodemand como tráfego de rede ou a utilização da CPU.</span><span class="sxs-lookup"><span data-stu-id="9797c-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="9797c-169">Atualmente, estas regras não podem ser definidas no Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="9797c-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="9797c-170">Olá utilize [portal do Azure](https://portal.azure.com) dimensionamento automático de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="9797c-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="9797c-171">Obter as informações de ligação</span><span class="sxs-lookup"><span data-stu-id="9797c-171">Get connection info</span></span>
<span data-ttu-id="9797c-172">as informações da ligação tooobtain sobre Olá VMs no seu conjuntos de dimensionamento, utilize [az vmss lista-instância--informações de ligação](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="9797c-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="9797c-173">Este comando devolve o endereço IP público Olá e a porta para cada VM que permite-lhe tooconnect com SSH:</span><span class="sxs-lookup"><span data-stu-id="9797c-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="9797c-174">Utilizar discos de dados com conjuntos de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-174">Use data disks with scale sets</span></span>
<span data-ttu-id="9797c-175">Pode criar e utilizar discos de dados com conjuntos de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9797c-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="9797c-176">Um tutorial anterior, aprendeu como demasiado[discos Azure gerir](tutorial-manage-disks.md) que destaca Olá melhores práticas e melhorias de desempenho para a criação de aplicações em discos de dados em vez de disco Olá SO.</span><span class="sxs-lookup"><span data-stu-id="9797c-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="9797c-177">Criar conjunto de dimensionamento com discos de dados</span><span class="sxs-lookup"><span data-stu-id="9797c-177">Create scale set with data disks</span></span>
<span data-ttu-id="9797c-178">toocreate uma escala definido e anexe discos de dados, adicionar Olá `--data-disk-sizes-gb` parâmetro toohello [az vmss criar](/cli/azure/vmss#create) comando.</span><span class="sxs-lookup"><span data-stu-id="9797c-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="9797c-179">Olá exemplo seguinte cria um conjunto com de dimensionamento *50*discos de dados de Gb ligados tooeach instância:</span><span class="sxs-lookup"><span data-stu-id="9797c-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="9797c-180">Quando instâncias são removidas de um conjunto de dimensionamento, também são removidos quaisquer discos de dados anexados.</span><span class="sxs-lookup"><span data-stu-id="9797c-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="9797c-181">Adicionar discos de dados</span><span class="sxs-lookup"><span data-stu-id="9797c-181">Add data disks</span></span>
<span data-ttu-id="9797c-182">definir um tooinstances de disco de dados no seu dimensionamento de tooadd, utilize [anexar o disco de vmss az](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="9797c-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="9797c-183">Olá exemplo seguinte adiciona um *50*instância de tooeach do disco Gb:</span><span class="sxs-lookup"><span data-stu-id="9797c-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="9797c-184">Desanexar os discos de dados</span><span class="sxs-lookup"><span data-stu-id="9797c-184">Detach data disks</span></span>
<span data-ttu-id="9797c-185">definir um tooinstances de disco de dados no seu dimensionamento de tooremove, utilize [desanexar o disco de vmss az](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="9797c-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="9797c-186">Olá exemplo a seguir remove o disco de dados de Olá em LUN *2* de cada instância:</span><span class="sxs-lookup"><span data-stu-id="9797c-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="9797c-187">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9797c-187">Next steps</span></span>
<span data-ttu-id="9797c-188">Neste tutorial, vai criar um conjunto de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9797c-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="9797c-189">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="9797c-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9797c-190">Utilizar a cloud init toocreate tooscale uma aplicação</span><span class="sxs-lookup"><span data-stu-id="9797c-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="9797c-191">Criar um conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9797c-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="9797c-192">Aumentar ou diminuir o número de Olá de instâncias de um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="9797c-193">Ver informações de ligação para as instâncias do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="9797c-194">Utilizar discos de dados num conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="9797c-194">Use data disks in a scale set</span></span>

<span data-ttu-id="9797c-195">Produzir toolearn tutorial seguinte de toohello mais informações sobre conceitos para máquinas virtuais de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="9797c-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9797c-196">Máquinas virtuais de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="9797c-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)