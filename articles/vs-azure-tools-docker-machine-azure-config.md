---
title: "aaaCreate Docker aloja no Azure com o Docker máquina | Microsoft Docs"
description: "Descreve a utilização de anfitriões de docker toocreate Docker máquina no Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="e86a8-103">Criar Anfitriões do Docker no Azure com Máquina do Docker</span><span class="sxs-lookup"><span data-stu-id="e86a8-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="e86a8-104">Executar [Docker](https://www.docker.com/) contentores requer o daemon de docker de Olá em execução para um anfitrião VM.</span><span class="sxs-lookup"><span data-stu-id="e86a8-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="e86a8-105">Este tópico descreve como toouse Olá [docker máquina](https://docs.docker.com/machine/) comando toocreate novas VMs do Linux, configurados com Olá daemon de Docker, em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="e86a8-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="e86a8-106">**Nota:**</span><span class="sxs-lookup"><span data-stu-id="e86a8-106">**Note:**</span></span> 

* <span data-ttu-id="e86a8-107">*Este artigo depende 0.9.0-rc2 de versão da máquina de docker ou superior*</span><span class="sxs-lookup"><span data-stu-id="e86a8-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="e86a8-108">*Contentores do Windows serão suportados através do docker-máquina no Olá quase futuro*</span><span class="sxs-lookup"><span data-stu-id="e86a8-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="e86a8-109">Criar as VMs com a máquina do Docker</span><span class="sxs-lookup"><span data-stu-id="e86a8-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="e86a8-110">Criar docker anfitrião VMs no Azure com Olá `docker-machine create` comando utilizando Olá `azure` controlador.</span><span class="sxs-lookup"><span data-stu-id="e86a8-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="e86a8-111">Olá controlador do Azure requer o ID de subscrição.</span><span class="sxs-lookup"><span data-stu-id="e86a8-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="e86a8-112">Pode utilizar Olá [CLI do Azure](cli-install-nodejs.md) ou Olá [Portal do Azure](https://portal.azure.com) tooretrieve sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="e86a8-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="e86a8-113">**Utilizar Olá Portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="e86a8-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="e86a8-114">Selecione **subscrições** Olá navegação à esquerda página e copie Olá do id de subscrição.</span><span class="sxs-lookup"><span data-stu-id="e86a8-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="e86a8-115">**Utilizar Olá CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="e86a8-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="e86a8-116">Tipo ```azure account list``` e id de subscrição de Olá de cópia.</span><span class="sxs-lookup"><span data-stu-id="e86a8-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="e86a8-117">Tipo `docker-machine create --driver azure` toosee Olá opções e os respetivos valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="e86a8-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="e86a8-118">Também pode ver Olá [documentação do controlador de Azure do Docker](https://docs.docker.com/machine/drivers/azure/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e86a8-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="e86a8-119">Olá exemplo a seguir depende Olá [valores predefinidos](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), mas, opcionalmente, defina estes valores:</span><span class="sxs-lookup"><span data-stu-id="e86a8-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="e86a8-120">dns do Azure para o nome de Olá associado ao IP público Olá e certificados gerados.</span><span class="sxs-lookup"><span data-stu-id="e86a8-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="e86a8-121">Este é o nome DNS Olá da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e86a8-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="e86a8-122">Olá VM pode, em seguida, em segurança parar, Olá IP dinâmico de versão e fornecer Olá capacidade tooreconnect após a vm Olá novamente começa com um IP de novo.</span><span class="sxs-lookup"><span data-stu-id="e86a8-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="e86a8-123">prefixo de nome de Olá tem de ser exclusivo para essa região UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e86a8-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="e86a8-124">Abra a porta 80 no Olá VM para acesso de internet de saída</span><span class="sxs-lookup"><span data-stu-id="e86a8-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="e86a8-125">tamanho de Olá armazenamento mais rápido de premium do VM tooutilize</span><span class="sxs-lookup"><span data-stu-id="e86a8-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="e86a8-126">armazenamento Premium utilizado para o disco da vm Olá</span><span class="sxs-lookup"><span data-stu-id="e86a8-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="e86a8-127">Escolha um anfitrião de docker com máquina docker</span><span class="sxs-lookup"><span data-stu-id="e86a8-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="e86a8-128">Assim que tiver uma entrada na máquina de docker para o anfitrião, é possível definir o anfitrião predefinido de Olá ao executar comandos de docker.</span><span class="sxs-lookup"><span data-stu-id="e86a8-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="e86a8-129">Com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e86a8-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="e86a8-130">Utilizar Bash</span><span class="sxs-lookup"><span data-stu-id="e86a8-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="e86a8-131">Agora, pode executar comandos de docker contra anfitriões especificados Olá</span><span class="sxs-lookup"><span data-stu-id="e86a8-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="e86a8-132">Executar um contentor</span><span class="sxs-lookup"><span data-stu-id="e86a8-132">Run a container</span></span>
<span data-ttu-id="e86a8-133">Com um anfitrião configurado, pode agora executar um tootest de servidor web simples se o anfitrião foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="e86a8-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="e86a8-134">Aqui vamos utilizar uma imagem de padrão nginx, especifique se deve escutar na porta 80 e que, se o anfitrião de Olá VM reiniciar, contentor Olá irá reiniciar bem (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="e86a8-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="e86a8-135">saída de Olá deve ter um aspeto semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="e86a8-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="e86a8-136">Contentor de Olá de teste</span><span class="sxs-lookup"><span data-stu-id="e86a8-136">Test hello container</span></span>
<span data-ttu-id="e86a8-137">Examine os contentores em execução com `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="e86a8-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="e86a8-138">E, Olá toosee com o contentor, tipo `docker-machine ip <VM name>` toofind Olá IP endereço tooenter no browser Olá:</span><span class="sxs-lookup"><span data-stu-id="e86a8-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Contentor de ngnix em execução](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="e86a8-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="e86a8-140">Summary</span></span>
<span data-ttu-id="e86a8-141">Com o docker-máquina, pode aprovisionar facilmente os anfitriões de docker no Azure para as validações de anfitriões de docker individuais.</span><span class="sxs-lookup"><span data-stu-id="e86a8-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="e86a8-142">Para produção de alojamento de contentores, consulte o artigo Olá [serviço de contentor do Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="e86a8-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="e86a8-143">toodevelop .NET Core aplicações com o Visual Studio, consulte [Docker Tools para Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="e86a8-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

