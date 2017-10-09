---
title: aaaUse Docker Compose numa VM com Linux no Azure | Microsoft Docs
description: "Como toouse Docker e Compose em máquinas virtuais Linux Olá CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="f2563-103">Obter iniciado com o Docker e Compose toodefine e executar uma aplicação de contentor multi no Azure</span><span class="sxs-lookup"><span data-stu-id="f2563-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="f2563-104">Com [Compose](http://github.com/docker/compose), que utiliza um toodefine do ficheiro de texto simples, uma aplicação consiste de vários contentores de Docker.</span><span class="sxs-lookup"><span data-stu-id="f2563-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="f2563-105">Em seguida, de rotação cópias de segurança da aplicação num único comando que tudo toodeploy ambiente definido.</span><span class="sxs-lookup"><span data-stu-id="f2563-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="f2563-106">Por exemplo, este artigo mostra como tooquickly configurar um blogue do WordPress com um back-end da base de dados MariaDB SQL numa VM com Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f2563-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="f2563-107">Também pode utilizar Compose tooset das aplicações mais complexas.</span><span class="sxs-lookup"><span data-stu-id="f2563-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="f2563-108">Configurar uma VM com Linux como um anfitrião do Docker</span><span class="sxs-lookup"><span data-stu-id="f2563-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="f2563-109">Pode utilizar vários procedimentos do Azure e imagens disponíveis ou modelos do Resource Manager no Azure Marketplace de Olá toocreate uma VM com Linux e configurá-lo como um anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="f2563-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="f2563-110">Por exemplo, consulte [utilizando Olá extensão da VM Docker toodeploy ambiente](dockerextension.md) tooquickly criar uma VM com Ubuntu com Olá extensão da VM do Azure Docker com um [modelo de início rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="f2563-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="f2563-111">Quando utiliza a extensão da VM de Docker Olá, a VM é automaticamente configurada como um anfitrião do Docker e Compose já está instalado.</span><span class="sxs-lookup"><span data-stu-id="f2563-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="f2563-112">Criar anfitrião Docker com o Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f2563-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="f2563-113">Olá de instalação mais recente [Azure CLI 2.0](/cli/azure/install-az-cli2) e inicie sessão com a conta do Azure tooan [início de sessão az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f2563-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f2563-114">Em primeiro lugar, crie um grupo de recursos para o seu ambiente de Docker com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f2563-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f2563-115">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroup* no Olá *westus* localização:</span><span class="sxs-lookup"><span data-stu-id="f2563-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="f2563-116">Em seguida, implementar uma VM com [criar a implementação do grupo az](/cli/azure/group/deployment#create) que inclui a extensão de VM do Azure Docker Olá de [este modelo Azure Resource Manager no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="f2563-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="f2563-117">Fornecer os seus próprios valores para *newStorageAccountName*, *adminUsername*, *adminPassword*, e *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="f2563-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="f2563-118">Demora alguns minutos para Olá toofinish de implementação.</span><span class="sxs-lookup"><span data-stu-id="f2563-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="f2563-119">Após a conclusão da implementação de Olá, [mover toonext passo](#verify-that-compose-is-installed) tooSSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="f2563-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="f2563-120">Opcionalmente, a linha de comandos do tooinstead controlo retorno toohello e implementação de Olá permitem continuam em segundo plano de Olá, adicione Olá `--no-wait` sinalizador toohello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="f2563-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="f2563-121">Este processo permite-lhe tooperform outras tarefas no Olá CLI enquanto continua a implementação de Olá alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f2563-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="f2563-122">Em seguida, pode ver detalhes sobre o estado de anfitriões de Docker Olá com [mostrar de vm az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="f2563-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="f2563-123">Olá exemplo seguinte verifica o estado de Olá da VM com o nome de Olá *myDockerVM* (Olá nome predefinido do modelo de Olá - não altere este nome) no grupo de recursos de Olá designado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="f2563-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="f2563-124">Quando este comando devolve *com êxito*, concluiu a implementação de Olá e pode SSH toohello VM na Olá passo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f2563-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="f2563-125">Certifique-se de que o Compose está instalado</span><span class="sxs-lookup"><span data-stu-id="f2563-125">Verify that Compose is installed</span></span>
<span data-ttu-id="f2563-126">Após a conclusão da implementação de Olá, SSH tooyour novo Docker anfitrião com o nome DNS Olá fornecido durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="f2563-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="f2563-127">Pode utilizar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview detalhes da sua VM, incluindo o nome DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="f2563-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="f2563-128">toocheck que compõem está instalado no Olá VM, execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f2563-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="f2563-129">Poderá ver um resultado semelhante demasiado*1.6.2 de compose docker, crie 4d 72027*.</span><span class="sxs-lookup"><span data-stu-id="f2563-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="f2563-130">Se utilizou o outro método toocreate um anfitrião do Docker e precisa de tooinstall compor a si, consulte Olá [compor documentação](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="f2563-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="f2563-131">Criar um ficheiro de configuração docker-Compose.yml</span><span class="sxs-lookup"><span data-stu-id="f2563-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="f2563-132">Em seguida, crie um `docker-compose.yml` ficheiro, que é apenas um ficheiro de configuração de texto, toodefine Olá Docker contentores toorun no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f2563-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="f2563-133">ficheiro de Olá Especifica Olá toorun de imagem em cada contentor (ou pode ser uma compilação de um Dockerfile), as variáveis de ambiente necessários e as dependências, portas e ligações de Olá entre contentores.</span><span class="sxs-lookup"><span data-stu-id="f2563-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="f2563-134">Para obter detalhes sobre a sintaxe de ficheiro yml, consulte [compor a referência de ficheiro](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="f2563-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="f2563-135">Criar Olá *docker-Compose.yml* ficheiro da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f2563-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="f2563-136">Utilize o tooadd do editor de texto favorito alguns ficheiros de toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="f2563-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="f2563-137">Olá exemplo seguinte utiliza Olá *vi* editor:</span><span class="sxs-lookup"><span data-stu-id="f2563-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="f2563-138">Colar Olá seguinte o exemplo para o ficheiro de texto.</span><span class="sxs-lookup"><span data-stu-id="f2563-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="f2563-139">Esta configuração utilize imagens a partir do Olá [DockerHub registo](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Olá open source para blogging e o conteúdo de sistema de gestão) e um back-end ligado MariaDB SQL da base de dados.</span><span class="sxs-lookup"><span data-stu-id="f2563-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="f2563-140">Introduza os seus próprios *MYSQL_ROOT_PASSWORD* da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f2563-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="f2563-141">Iniciar contentores Olá com Compose</span><span class="sxs-lookup"><span data-stu-id="f2563-141">Start hello containers with Compose</span></span>
<span data-ttu-id="f2563-142">No Olá mesmo diretório como o *docker-Compose.yml* ficheiro, execute Olá seguinte comando (dependendo do seu ambiente, poderá ser necessário toorun `docker-compose` utilizando `sudo`):</span><span class="sxs-lookup"><span data-stu-id="f2563-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="f2563-143">Este comando inicia contentores de Docker Olá especificados no *docker-Compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="f2563-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="f2563-144">Demorará um minuto ou dois para toocomplete este passo.</span><span class="sxs-lookup"><span data-stu-id="f2563-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="f2563-145">Consulte toohello semelhante de saída seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="f2563-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="f2563-146">Ser se toouse Olá **-d** opção no arranque, para que os contentores de Olá executam em segundo plano de Olá continuamente.</span><span class="sxs-lookup"><span data-stu-id="f2563-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="f2563-147">tooverify que são contentores Olá, tipo `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="f2563-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="f2563-148">Deverá ver algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f2563-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="f2563-149">Pode agora ligar tooWordPress diretamente no Olá VM na porta 80.</span><span class="sxs-lookup"><span data-stu-id="f2563-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="f2563-150">Abra um browser e introduza o nome DNS Olá da sua VM (tais como `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="f2563-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="f2563-151">Deverá ver agora Olá que wordpress iniciar o ecrã, onde pode concluir a instalação de Olá e começar a utilizar com a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f2563-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![Ecrã de início do WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="f2563-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f2563-153">Next steps</span></span>
* <span data-ttu-id="f2563-154">Aceda toohello [Guia do utilizador de extensão de VM de Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obter mais opções tooconfigure Docker e Compose na sua VM de Docker.</span><span class="sxs-lookup"><span data-stu-id="f2563-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="f2563-155">Por exemplo, uma opção é tooput Olá Compose yml ficheiro (tooJSON convertida) diretamente na configuração de Olá da Olá extensão da VM de Docker.</span><span class="sxs-lookup"><span data-stu-id="f2563-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="f2563-156">Veja Olá [compor a referência da linha de comandos](http://docs.docker.com/compose/reference/) e [Guia do utilizador](http://docs.docker.com/compose/) para obter mais exemplos de criar e implementar aplicações de várias contentor.</span><span class="sxs-lookup"><span data-stu-id="f2563-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="f2563-157">Está a utilizar um modelo Azure Resource Manager, o próprio ou um contribuíram de Olá [Comunidade](https://azure.microsoft.com/documentation/templates/), toodeploy uma VM do Azure com o Docker e uma aplicação configurar com Compose.</span><span class="sxs-lookup"><span data-stu-id="f2563-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="f2563-158">Por exemplo, Olá [implementar um blogue do WordPress com Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) modelo utiliza Docker e Compose tooquickly implementar WordPress com um back-end de MySQL numa VM com Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f2563-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="f2563-159">Tente integrar o Docker Compose com um cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="f2563-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="f2563-160">Consulte [utilizando compor com Swarm](https://docs.docker.com/compose/swarm/) para cenários.</span><span class="sxs-lookup"><span data-stu-id="f2563-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
