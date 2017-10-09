---
title: aaaHow toocreate as imagens de VM do Linux do Azure com Packer | Microsoft Docs
description: Saiba como imagens de toocreate Packer toouse de computadores virtuais Linux no Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="753d9-103">Como imagens de máquina virtual do toouse Packer toocreate Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="753d9-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="753d9-104">Cada máquina virtual (VM) no Azure é criada a partir de uma imagem que define Olá distribuição de Linux e versão do SO.</span><span class="sxs-lookup"><span data-stu-id="753d9-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="753d9-105">Imagens podem incluir aplicações pré-instaladas e configurações.</span><span class="sxs-lookup"><span data-stu-id="753d9-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="753d9-106">Olá, Azure Marketplace disponibiliza várias imagens primeira e de terceiros para distribuições mais comuns e ambientes de aplicação, ou pode criar as suas próprias necessidades de tooyour imagens personalizadas e adaptadas.</span><span class="sxs-lookup"><span data-stu-id="753d9-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="753d9-107">Este artigo fornece detalhes sobre como toouse Olá abrir a ferramenta de origem [Packer](https://www.packer.io/) toodefine e compilação imagens personalizadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="753d9-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="753d9-108">Criar grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="753d9-108">Create Azure resource group</span></span>
<span data-ttu-id="753d9-109">Durante o processo de compilação de Olá, Packer cria temporários recursos do Azure como compilações Olá de VM de origem.</span><span class="sxs-lookup"><span data-stu-id="753d9-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="753d9-110">toocapture VM de origem para utilização como uma imagem, tem de definir um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="753d9-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="753d9-111">Olá saída do processo de compilação do Olá Packer é armazenada neste grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="753d9-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="753d9-112">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="753d9-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="753d9-113">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="753d9-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="753d9-114">Criar as credenciais do Azure</span><span class="sxs-lookup"><span data-stu-id="753d9-114">Create Azure credentials</span></span>
<span data-ttu-id="753d9-115">Packer autentica com o Azure utilizando um principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="753d9-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="753d9-116">Um principal de serviço do Azure é uma identidade de segurança que pode utilizar com aplicações, serviços e ferramentas de automatização como Packer.</span><span class="sxs-lookup"><span data-stu-id="753d9-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="753d9-117">Controlar e definir permissões de Olá como principal de serviço do toowhat operações Olá pode efetuar no Azure.</span><span class="sxs-lookup"><span data-stu-id="753d9-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="753d9-118">Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de Olá de saída que Packer necessita:</span><span class="sxs-lookup"><span data-stu-id="753d9-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="753d9-119">Segue-se um exemplo de saída de Olá do Olá precedente comandos:</span><span class="sxs-lookup"><span data-stu-id="753d9-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="753d9-120">tooauthenticate tooAzure, terá também tooobtain a sua subscrição do Azure com o ID [mostrar de conta az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="753d9-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="753d9-121">Utilize o resultado Olá estes dois comandos no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="753d9-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="753d9-122">Definir Packer modelo</span><span class="sxs-lookup"><span data-stu-id="753d9-122">Define Packer template</span></span>
<span data-ttu-id="753d9-123">imagens de toobuild, crie um modelo como um ficheiro JSON.</span><span class="sxs-lookup"><span data-stu-id="753d9-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="753d9-124">No modelo de Olá, definir construtores e processo de compilação provisioners realizar Olá real.</span><span class="sxs-lookup"><span data-stu-id="753d9-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="753d9-125">Packer tem um [provisioner para o Azure](https://www.packer.io/docs/builders/azure.html) que lhe permite toodefine Azure recursos, tais como credenciais de principal de serviço de Olá criados no Olá precedente passo.</span><span class="sxs-lookup"><span data-stu-id="753d9-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="753d9-126">Crie um ficheiro denominado *ubuntu.json* e colar Olá seguir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="753d9-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="753d9-127">Introduza os seus próprios valores para seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="753d9-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="753d9-128">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="753d9-128">Parameter</span></span>                           | <span data-ttu-id="753d9-129">Onde tooobtain</span><span class="sxs-lookup"><span data-stu-id="753d9-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="753d9-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="753d9-130">*client_id*</span></span>                         | <span data-ttu-id="753d9-131">Primeira linha do resultado de `az ad sp` criar comando - *appId*</span><span class="sxs-lookup"><span data-stu-id="753d9-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="753d9-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="753d9-132">*client_secret*</span></span>                     | <span data-ttu-id="753d9-133">Segunda linha de saída de `az ad sp` criar comando - *palavra-passe*</span><span class="sxs-lookup"><span data-stu-id="753d9-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="753d9-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="753d9-134">*tenant_id*</span></span>                         | <span data-ttu-id="753d9-135">Terceira linha de saída de `az ad sp` criar comando - *inquilino*</span><span class="sxs-lookup"><span data-stu-id="753d9-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="753d9-136">*SUBSCRIPTION_ID*</span><span class="sxs-lookup"><span data-stu-id="753d9-136">*subscription_id*</span></span>                   | <span data-ttu-id="753d9-137">O resultado da `az account show` comando</span><span class="sxs-lookup"><span data-stu-id="753d9-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="753d9-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="753d9-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="753d9-139">Nome do grupo de recursos que criou no passo primeiro Olá</span><span class="sxs-lookup"><span data-stu-id="753d9-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="753d9-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="753d9-140">*managed_image_name*</span></span>                | <span data-ttu-id="753d9-141">Nome para a imagem de disco gerido Olá que é criada</span><span class="sxs-lookup"><span data-stu-id="753d9-141">Name for hello managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="753d9-142">Este modelo cria uma imagem de Ubuntu 16.04 LTS, instala NGINX e deprovisions Olá VM.</span><span class="sxs-lookup"><span data-stu-id="753d9-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="753d9-143">Se expandir nas credenciais de utilizador de tooprovision modelo, ajuste o comando de provisioner Olá que deprovisions Olá tooread de agente do Azure `-deprovision` vez `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="753d9-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="753d9-144">Olá `+user` sinalizador remove todas as contas de utilizador Olá de VM de origem.</span><span class="sxs-lookup"><span data-stu-id="753d9-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="753d9-145">Compilar Packer imagem</span><span class="sxs-lookup"><span data-stu-id="753d9-145">Build Packer image</span></span>
<span data-ttu-id="753d9-146">Se ainda não tiver Packer instalado no seu computador local, [siga as instruções de instalação do Olá Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="753d9-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="753d9-147">Crie imagem Olá, especificando o Packer ficheiro do modelo da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="753d9-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="753d9-148">Segue-se um exemplo de saída de Olá do Olá precedente comandos:</span><span class="sxs-lookup"><span data-stu-id="753d9-148">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="753d9-149">Criar a VM da imagem do Azure</span><span class="sxs-lookup"><span data-stu-id="753d9-149">Create VM from Azure Image</span></span>
<span data-ttu-id="753d9-150">Agora pode criar uma VM a partir da imagem com [az vm criar](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="753d9-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="753d9-151">Especifique Olá imagem que criou com Olá `--image` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="753d9-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="753d9-152">Olá exemplo seguinte cria uma VM chamada *myVM* de *myPackerImage* e gera chaves SSH, caso ainda não existam:</span><span class="sxs-lookup"><span data-stu-id="753d9-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="753d9-153">Demora alguns minutos de Olá de toocreate VM.</span><span class="sxs-lookup"><span data-stu-id="753d9-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="753d9-154">Quando tiver sido criada Olá VM, tome nota do Olá `publicIpAddress` apresentado pela Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="753d9-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="753d9-155">Este endereço é o site NGINX de Olá de tooaccess utilizadas através de um browser web.</span><span class="sxs-lookup"><span data-stu-id="753d9-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="753d9-156">tooallow web tráfego tooreach a VM, abrir porta 80 do Olá Internet com [az vm open-porta](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="753d9-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="753d9-157">Testar a VM e NGINX</span><span class="sxs-lookup"><span data-stu-id="753d9-157">Test VM and NGINX</span></span>
<span data-ttu-id="753d9-158">Agora pode abrir um browser e introduza `http://publicIpAddress` na barra de endereço Olá.</span><span class="sxs-lookup"><span data-stu-id="753d9-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="753d9-159">Forneça o suas próprias público endereços IP a partir Olá VM criar o processo.</span><span class="sxs-lookup"><span data-stu-id="753d9-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="753d9-160">página NGINX Olá predefinida é apresentada como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="753d9-160">hello default NGINX page is displayed as in hello following example:</span></span>

![Site predefinido do NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="753d9-162">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="753d9-162">Next steps</span></span>
<span data-ttu-id="753d9-163">Neste exemplo, utilizou Packer toocreate uma imagem de VM com NGINX já instalado.</span><span class="sxs-lookup"><span data-stu-id="753d9-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="753d9-164">Pode utilizar esta imagem de VM em conjunto com a implementação fluxos de trabalho existentes, tais como toodeploy tooVMs sua aplicação criada a partir de Olá imagem com Ansible, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="753d9-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="753d9-165">Para modelos de Packer de exemplo adicionais para outros distros Linux, consulte [este repositório do GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="753d9-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>