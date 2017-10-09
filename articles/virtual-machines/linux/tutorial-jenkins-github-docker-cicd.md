---
title: aaaCreate um pipeline de desenvolvimento no Azure com Jenkins | Microsoft Docs
description: "Saiba como toocreate um Jenkins virtual máquina no Azure que obtém a partir do GitHub em cada código consolidar e cria um novo Docker toorun de contentor, a aplicação"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="02548-103">Como toocreate uma infraestrutura de desenvolvimento de uma VM com Linux no Azure com Jenkins, GitHub e Docker</span><span class="sxs-lookup"><span data-stu-id="02548-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="02548-104">tooautomate Olá compilação e testar a fase de desenvolvimento de aplicações, pode utilizar uma integração contínua e o pipeline de implementação (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="02548-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="02548-105">Neste tutorial, vai criar um pipeline de CI/CD numa VM do Azure incluindo como:</span><span class="sxs-lookup"><span data-stu-id="02548-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="02548-106">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="02548-107">Instalar e configurar Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="02548-108">Criar o webhook integração entre o GitHub e Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="02548-109">Criar e consolida acionador que jenkins criar tarefas a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="02548-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="02548-110">Criar uma imagem de Docker para a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="02548-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="02548-111">Certifique-se de consolidações de GitHub criem nova imagem do Docker e executar a aplicação de atualizações</span><span class="sxs-lookup"><span data-stu-id="02548-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="02548-112">Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="02548-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="02548-113">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="02548-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="02548-114">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="02548-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="02548-115">Criar uma instância de Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-115">Create Jenkins instance</span></span>
<span data-ttu-id="02548-116">Um tutorial anterior em [como toocustomize uma máquina virtual do Linux no primeiro arranque](tutorial-automate-vm-deployment.md), que aprendeu como tooautomate personalização de VM com init de nuvem.</span><span class="sxs-lookup"><span data-stu-id="02548-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="02548-117">Este tutorial utiliza um ficheiro de nuvem init tooinstall Jenkins e Docker numa VM.</span><span class="sxs-lookup"><span data-stu-id="02548-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="02548-118">Na sua shell atual, crie um ficheiro denominado *nuvem init.txt* e colar Olá seguindo a configuração.</span><span class="sxs-lookup"><span data-stu-id="02548-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="02548-119">Por exemplo, crie o ficheiro de Olá no Olá Shell na nuvem não no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="02548-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="02548-120">Introduza `sensible-editor cloud-init-jenkins.txt` toocreate Olá ficheiro e ver uma lista de editores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="02548-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="02548-121">Certifique-se de que o ficheiro init de nuvem todo Olá foi corretamente copiado, Olá especialmente a primeira linha:</span><span class="sxs-lookup"><span data-stu-id="02548-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

<span data-ttu-id="02548-122">Antes de poder criar uma VM, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="02548-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="02548-123">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupJenkins* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="02548-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="02548-124">Agora criar uma VM com [az vm criar](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="02548-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="02548-125">Olá utilize `--custom-data` toopass de parâmetro no seu ficheiro de configuração de nuvem init.</span><span class="sxs-lookup"><span data-stu-id="02548-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="02548-126">Forneça o caminho completo do Olá demasiado*nuvem-init-jenkins.txt* se tiver guardado o ficheiro de Olá fora do diretório de trabalho presente.</span><span class="sxs-lookup"><span data-stu-id="02548-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="02548-127">Demora alguns minutos para Olá VM toobe criada e configurada.</span><span class="sxs-lookup"><span data-stu-id="02548-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="02548-128">tooallow web tráfego tooreach a VM, utilize [az vm open-porta](/cli/azure/vm#open-port) tooopen porta *8080* Jenkins para tráfego de e porta *1337* para aplicação Node.js Olá que é utilizado toorun uma aplicação de exemplo:</span><span class="sxs-lookup"><span data-stu-id="02548-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="02548-129">Configurar Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-129">Configure Jenkins</span></span>
<span data-ttu-id="02548-130">tooaccess sua Jenkins instância, obtenha o endereço IP público Olá da sua VM:</span><span class="sxs-lookup"><span data-stu-id="02548-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="02548-131">Por motivos de segurança, terá de tooenter Olá administrador inicial palavra-passe que é armazenado num ficheiro de texto no seu Olá de toostart VM que jenkins instalar.</span><span class="sxs-lookup"><span data-stu-id="02548-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="02548-132">Utilize o endereço IP público Olá obtido no Olá anterior passo tooSSH tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="02548-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="02548-133">Olá vista `initialAdminPassword` para sua Jenkins instalar e copie-o:</span><span class="sxs-lookup"><span data-stu-id="02548-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="02548-134">Se o ficheiro de Olá ainda não está disponível, aguarde alguns minutos para a nuvem init toocomplete Olá Jenkins e instalação de Docker.</span><span class="sxs-lookup"><span data-stu-id="02548-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="02548-135">Agora abra um browser e aceda demasiado`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="02548-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="02548-136">Conclua a configuração Jenkins Olá inicial da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="02548-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="02548-137">Introduza Olá *initialAdminPassword* obtida Olá VM no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="02548-138">Clique em **selecione tooinstall de plug-ins**</span><span class="sxs-lookup"><span data-stu-id="02548-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="02548-139">Procurar *GitHub* na caixa de texto de Olá na parte superior do Olá, selecione Olá *Plug-in do GitHub*, em seguida, clique em **instalar**</span><span class="sxs-lookup"><span data-stu-id="02548-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="02548-140">toocreate uma conta de utilizador Jenkins, preencha o formulário de Olá conforme pretendido.</span><span class="sxs-lookup"><span data-stu-id="02548-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="02548-141">Numa perspetiva de segurança, deve criar este primeiro utilizador Jenkins em vez de os continuar como conta de administrador predefinida Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="02548-142">Quando terminar, clique em **começar a utilizar Jenkins**</span><span class="sxs-lookup"><span data-stu-id="02548-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="02548-143">Criar o GitHub webhook</span><span class="sxs-lookup"><span data-stu-id="02548-143">Create GitHub webhook</span></span>
<span data-ttu-id="02548-144">integração de Olá tooconfigure com o GitHub, abra Olá [aplicação de exemplo de Olá, mundo Node.js](https://github.com/Azure-Samples/nodejs-docs-hello-world) do repositório do Olá exemplos do Azure.</span><span class="sxs-lookup"><span data-stu-id="02548-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="02548-145">toofork Olá repositório tooyour ser proprietário da conta do GitHub, clique em Olá **bifurcação** botão no canto superior direito Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="02548-146">Crie um webhook no interior de bifurcação de Olá que criou:</span><span class="sxs-lookup"><span data-stu-id="02548-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="02548-147">Clique em **definições**, em seguida, selecione **integrações & serviços** no lado esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="02548-148">Clique em **Adicionar serviço**, em seguida, introduza *Jenkins* na caixa Filtro.</span><span class="sxs-lookup"><span data-stu-id="02548-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="02548-149">Selecione *Jenkins (GitHub Plug-in)*</span><span class="sxs-lookup"><span data-stu-id="02548-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="02548-150">Para Olá **Jenkins ligue URL**, introduza `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="02548-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="02548-151">Certifique-se de que incluem Olá à direita /</span><span class="sxs-lookup"><span data-stu-id="02548-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="02548-152">Clique em **Adicionar serviço**</span><span class="sxs-lookup"><span data-stu-id="02548-152">Click **Add service**</span></span>

![Adicione o repositório do GitHub webhook tooyour escolhido](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="02548-154">Criar tarefa de Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-154">Create Jenkins job</span></span>
<span data-ttu-id="02548-155">toohave Jenkins respondeu tooan eventos no GitHub, tais como consolidar o código, criar uma tarefa de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="02548-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="02548-156">No seu Web site Jenkins, clique em **criar novas tarefas** da home page do Olá:</span><span class="sxs-lookup"><span data-stu-id="02548-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="02548-157">Introduza *Olámundo* como o nome da tarefa.</span><span class="sxs-lookup"><span data-stu-id="02548-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="02548-158">Escolha **projeto Freestyle**, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="02548-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="02548-159">Em Olá **geral** secção, selecione **GitHub** projeto e introduza o URL do repositório escolhido, tais como *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="02548-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="02548-160">Em Olá **gestão de código de origem** secção, selecione **Git**, introduza o seu repositório forked *.git* URL, tais como *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="02548-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="02548-161">Em Olá **criar Acionadores** secção, selecione **acionador de rotina do GitHub para consulta GITscm**.</span><span class="sxs-lookup"><span data-stu-id="02548-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="02548-162">Em Olá **criar** secção, escolha **Adicionar passo de compilação**.</span><span class="sxs-lookup"><span data-stu-id="02548-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="02548-163">Selecione **executar shell**, em seguida, introduza `echo "Testing"` na janela toocommand.</span><span class="sxs-lookup"><span data-stu-id="02548-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="02548-164">Clique em **guardar** em Olá parte inferior da janela de tarefas Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="02548-165">Integração do GitHub de teste</span><span class="sxs-lookup"><span data-stu-id="02548-165">Test GitHub integration</span></span>
<span data-ttu-id="02548-166">Olá tootest integração do GitHub com Jenkins, consolidar uma alteração na sua bifurcação.</span><span class="sxs-lookup"><span data-stu-id="02548-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="02548-167">No GitHub da IU da web, selecione o seu repositório forked e, em seguida, clique em Olá **index.js** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="02548-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="02548-168">Clique em tooedit de ícone de lápis Olá este ficheiro para a linha 6 lê:</span><span class="sxs-lookup"><span data-stu-id="02548-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="02548-169">toocommit as suas alterações, clique em Olá **consolidar alterações** botão na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="02548-170">No Jenkins, uma nova compilação é iniciado em Olá **criar histórico** secção do canto de esquerdo Olá inferior da sua página de tarefa.</span><span class="sxs-lookup"><span data-stu-id="02548-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="02548-171">Clique em ligação de número de compilação de Olá e selecione **consola saída** no tamanho da esquerda Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="02548-172">Pode ver os passos de Olá Jenkins demora como o seu código é retirado da GitHub e Olá mensagem de saudação do saídas ação de compilação `Testing` toohello consola.</span><span class="sxs-lookup"><span data-stu-id="02548-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="02548-173">Sempre que uma consolidação é efetuada no GitHub webhook Olá acede tooJenkins e acionar uma nova compilação desta forma.</span><span class="sxs-lookup"><span data-stu-id="02548-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="02548-174">Definir imagem de compilação do Docker</span><span class="sxs-lookup"><span data-stu-id="02548-174">Define Docker build image</span></span>
<span data-ttu-id="02548-175">toosee Olá Node.js aplicação em execução com base no seu consolidações do GitHub, permite criar um Docker imagem toorun Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="02548-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="02548-176">imagem de Olá é criada a partir de um Dockerfile que define a forma como tooconfigure Olá contentor que executa a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="02548-177">Olá SSH ligação tooyour VM, altere o diretório de área de trabalho de Jenkins de toohello chamado após a tarefa de Olá que criou no passo anterior.</span><span class="sxs-lookup"><span data-stu-id="02548-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="02548-178">No nosso exemplo, que foi atribuído o nome *Olámundo*.</span><span class="sxs-lookup"><span data-stu-id="02548-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="02548-179">Criar um ficheiro com neste diretório de área de trabalho com `sudo sensible-editor Dockerfile` e colar Olá seguir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="02548-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="02548-180">Certifique-se de que Olá que dockerfile todo é copiados corretamente, especialmente Olá primeira linha:</span><span class="sxs-lookup"><span data-stu-id="02548-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="02548-181">Este Dockerfile utiliza Olá imagem base do Node.js com Linux Extreme, porta expõe 1337 Olá mundo Olá aplicação é executado em, em seguida, copia os ficheiros de aplicação Olá e inicializa-lo.</span><span class="sxs-lookup"><span data-stu-id="02548-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="02548-182">Criar regras de compilação Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-182">Create Jenkins build rules</span></span>
<span data-ttu-id="02548-183">No passo anterior, criou uma regra de compilação Jenkins básica que uma consola de toohello de mensagem de saída.</span><span class="sxs-lookup"><span data-stu-id="02548-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="02548-184">Permite criar Olá compilação passo toouse nosso Dockerfile e executar a aplicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="02548-185">Novamente na instância Jenkins, selecione a tarefa de Olá que criou no passo anterior.</span><span class="sxs-lookup"><span data-stu-id="02548-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="02548-186">Clique em **configurar** no lado esquerdo Olá e desloque para baixo toohello **criar** secção:</span><span class="sxs-lookup"><span data-stu-id="02548-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="02548-187">Remover existentes `echo "Test"` passo de compilação.</span><span class="sxs-lookup"><span data-stu-id="02548-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="02548-188">Clique em Olá vermelho cruzada na Olá canto superior direito da caixa de passo de compilação Olá existente.</span><span class="sxs-lookup"><span data-stu-id="02548-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="02548-189">Clique em **Adicionar passo de compilação**, em seguida, selecione **executar shell**</span><span class="sxs-lookup"><span data-stu-id="02548-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="02548-190">No Olá **comando** caixa, introduza Olá os seguintes comandos do Docker, em seguida, selecione **guardar**:</span><span class="sxs-lookup"><span data-stu-id="02548-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="02548-191">passos de compilação do Docker Olá criar uma imagem e a etiqueta com Olá Jenkins número de compilação para pode manter um histórico de imagens.</span><span class="sxs-lookup"><span data-stu-id="02548-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="02548-192">Quaisquer contentores existentes a executar a aplicação Olá são parados e, em seguida, são removidas.</span><span class="sxs-lookup"><span data-stu-id="02548-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="02548-193">Um novo contentor é iniciado utilizando a imagem de Olá e executa a aplicação Node.js com base no consolidações mais recentes do Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="02548-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="02548-194">Testar o pipeline</span><span class="sxs-lookup"><span data-stu-id="02548-194">Test your pipeline</span></span>
<span data-ttu-id="02548-195">pipeline de todo Olá toosee em ação, editar Olá *index.js* ficheiros no seu repositório do GitHub forked novamente e clique em **Confirmar alteração**.</span><span class="sxs-lookup"><span data-stu-id="02548-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="02548-196">Inicia uma nova tarefa em Jenkins com base nos Olá webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="02548-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="02548-197">Este demora alguns segundos a imagem de Docker toocreate Olá e iniciar a sua aplicação num contentor de novo.</span><span class="sxs-lookup"><span data-stu-id="02548-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="02548-198">Se for necessário, obter novamente o endereço IP público Olá da sua VM:</span><span class="sxs-lookup"><span data-stu-id="02548-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="02548-199">Abra um browser e introduza `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="02548-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="02548-200">A aplicação Node.js é apresentada e reflete consolidações mais recentes do Olá no seu bifurcação de GitHub da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="02548-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Aplicação Node.js em execução](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="02548-202">Agora a efetuar outra edição toohello *index.js* ficheiro no GitHub e Confirmar alteração Olá.</span><span class="sxs-lookup"><span data-stu-id="02548-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="02548-203">Aguarde alguns segundos para Olá tarefa toocomplete no Jenkins, em seguida, atualize a sua versão do web browser toosee Olá atualizada da sua aplicação em execução num novo contentor da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="02548-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Aplicação Node.js em execução depois de outra consolidação do GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="02548-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="02548-205">Next steps</span></span>
<span data-ttu-id="02548-206">Neste tutorial, configurou GitHub toorun uma tarefa de compilação Jenkins em cada consolidação de código e, em seguida, implementar a aplicação de um tootest de contentor do Docker.</span><span class="sxs-lookup"><span data-stu-id="02548-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="02548-207">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="02548-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="02548-208">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="02548-209">Instalar e configurar Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="02548-210">Criar o webhook integração entre o GitHub e Jenkins</span><span class="sxs-lookup"><span data-stu-id="02548-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="02548-211">Criar e consolida acionador que jenkins criar tarefas a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="02548-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="02548-212">Criar uma imagem de Docker para a sua aplicação</span><span class="sxs-lookup"><span data-stu-id="02548-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="02548-213">Certifique-se de consolidações de GitHub criem nova imagem do Docker e executar a aplicação de atualizações</span><span class="sxs-lookup"><span data-stu-id="02548-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="02548-214">Avançar toolearn tutorial seguinte de toohello mais informações sobre como toointegrate Jenkins com o Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="02548-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="02548-215">Implementar aplicações com Jenkins e serviços da equipa</span><span class="sxs-lookup"><span data-stu-id="02548-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)