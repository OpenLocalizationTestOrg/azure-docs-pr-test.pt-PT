---
title: aaaSet configurar o ambiente de desenvolvimento no Linux | Microsoft Docs
description: "Instalar o runtime Olá e SDK e criar um cluster de desenvolvimento local no Linux. Depois de concluir esta configuração, estará pronto toobuild aplicações."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="ddb00-104">Preparar o ambiente de desenvolvimento no Linux</span><span class="sxs-lookup"><span data-stu-id="ddb00-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ddb00-105">Windows</span><span class="sxs-lookup"><span data-stu-id="ddb00-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="ddb00-106">Linux</span><span class="sxs-lookup"><span data-stu-id="ddb00-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="ddb00-107">OSX</span><span class="sxs-lookup"><span data-stu-id="ddb00-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="ddb00-108">toodeploy e execute [aplicações do Azure Service Fabric](service-fabric-application-model.md) no seu computador de desenvolvimento do Linux, instalar o runtime de Olá e SDK comuns.</span><span class="sxs-lookup"><span data-stu-id="ddb00-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="ddb00-109">Também pode instalar SDKs opcionais para Java e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ddb00-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddb00-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ddb00-110">Prerequisites</span></span>

<span data-ttu-id="ddb00-111">Olá seguintes versões do sistema operativo é suportada para desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="ddb00-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="ddb00-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="ddb00-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="ddb00-113">Atualizar as origens do APT</span><span class="sxs-lookup"><span data-stu-id="ddb00-113">Update your APT sources</span></span>
<span data-ttu-id="ddb00-114">tooinstall Olá SDK e Olá runtime associados pacote através da ferramenta de linha de comandos Olá apt get, tem primeiro de atualizar as origens de ferramenta de empacotamento avançadas (APT).</span><span class="sxs-lookup"><span data-stu-id="ddb00-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="ddb00-115">Abra um terminal.</span><span class="sxs-lookup"><span data-stu-id="ddb00-115">Open a terminal.</span></span>
2. <span data-ttu-id="ddb00-116">Adicione a lista de origens do Olá Service Fabric repositório tooyour.</span><span class="sxs-lookup"><span data-stu-id="ddb00-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="ddb00-117">Adicionar Olá `dotnet` lista de origens de tooyour do repositório.</span><span class="sxs-lookup"><span data-stu-id="ddb00-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="ddb00-118">Adicionar Olá tooyour APT porta-chaves da chave nova proteção de privacidade Gnu (o GnuPG ou GPG).</span><span class="sxs-lookup"><span data-stu-id="ddb00-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="ddb00-119">Adicione Olá oficial Docker GPG tooyour chave APT porta-chaves.</span><span class="sxs-lookup"><span data-stu-id="ddb00-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="ddb00-120">Configure o repositório de Docker Olá.</span><span class="sxs-lookup"><span data-stu-id="ddb00-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="ddb00-121">Atualizar o pacote listas com base no Olá recentemente adicionado repositórios.</span><span class="sxs-lookup"><span data-stu-id="ddb00-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="ddb00-122">Instalar e configurar Olá SDK para a configuração de local cluster</span><span class="sxs-lookup"><span data-stu-id="ddb00-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="ddb00-123">Depois de atualizar as origens, pode instalar Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="ddb00-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="ddb00-124">Instalar pacote do SDK de Service Fabric de Olá, confirmar instalação Olá e aceitar o contrato de licença toohello.</span><span class="sxs-lookup"><span data-stu-id="ddb00-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="ddb00-125">Olá seguintes comandos automatizar aceitar Olá licença para pacotes de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="ddb00-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="ddb00-126">Configurar um cluster local</span><span class="sxs-lookup"><span data-stu-id="ddb00-126">Set up a local cluster</span></span>
  <span data-ttu-id="ddb00-127">Se a instalação de Olá for bem-sucedida, deve ser capaz de toostart um cluster local.</span><span class="sxs-lookup"><span data-stu-id="ddb00-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="ddb00-128">Execute script de configuração de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="ddb00-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="ddb00-129">Abra um browser e aceda demasiado[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="ddb00-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="ddb00-130">Se tiver iniciado o cluster Olá, deverá ver o dashboard de Service Fabric Explorer Olá.</span><span class="sxs-lookup"><span data-stu-id="ddb00-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer no Linux][sfx-linux]

  <span data-ttu-id="ddb00-132">Nesta fase, pode implementar pacotes de aplicações do Service Fabric pré-configurados ou novos com base em contentores convidados ou em executáveis convidados.</span><span class="sxs-lookup"><span data-stu-id="ddb00-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="ddb00-133">toobuild novos serviços utilizando Java Olá ou .NET Core SDKs, siga os passos de configuração opcional Olá que são fornecidos nas secções subsequentes.</span><span class="sxs-lookup"><span data-stu-id="ddb00-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="ddb00-134">O Linux não suporta clusters autónomos.</span><span class="sxs-lookup"><span data-stu-id="ddb00-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="ddb00-135">Olá preview suporta apenas uma caixa e clusters de múltiplos computadores Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb00-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="ddb00-136">Configurar Olá CLI de recursos de infraestrutura de serviço</span><span class="sxs-lookup"><span data-stu-id="ddb00-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="ddb00-137">Olá [CLI de recursos de infraestrutura de serviço](service-fabric-cli.md) tem comandos para interagir com entidades do Service Fabric, incluindo clusters e aplicações.</span><span class="sxs-lookup"><span data-stu-id="ddb00-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="ddb00-138">Se baseia no python, por isso tenha se toohave python e pip instalado antes de continuar com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ddb00-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="ddb00-139">Instalar e configurar generators Olá para contentores e executáveis de convidado</span><span class="sxs-lookup"><span data-stu-id="ddb00-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="ddb00-140">O Service Fabric fornece ferramentas estruturais que irão ajudá-lo a criar aplicações do Service Fabric a partir do terminal, através do gerador de modelos Yeoman.</span><span class="sxs-lookup"><span data-stu-id="ddb00-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="ddb00-141">Siga os passos de Olá abaixo tooensure que tiver o gerador de modelo yeoman Olá Service Fabric para trabalhar no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ddb00-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="ddb00-142">Instalar nodejs e NPM no seu computador</span><span class="sxs-lookup"><span data-stu-id="ddb00-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="ddb00-143">Instalar o gerador de modelos [Yeoman](http://yeoman.io/) no seu computador a partir do NPM</span><span class="sxs-lookup"><span data-stu-id="ddb00-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="ddb00-144">Instalar o gerador de contentor do serviço Fabric Yeo Olá e gerador de execuatble de convidado de NPM</span><span class="sxs-lookup"><span data-stu-id="ddb00-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="ddb00-145">Depois de ter instalado Olá acima generators, deve ser capaz de toocreate aplicações com serviços de convidados executável ou contentor executando `yo azuresfguest` ou `yo azuresfcontainer` respetivamente.</span><span class="sxs-lookup"><span data-stu-id="ddb00-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="ddb00-146">Instalar Olá necessários Java artefactos (opcionais, se quiser toouse Olá Java modelos de programação)</span><span class="sxs-lookup"><span data-stu-id="ddb00-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="ddb00-147">serviços do Service Fabric toobuild utilizando Java, certifique-se de que tem 1.8 JDK instalados juntamente com o Gradle que é utilizada para executar tarefas de compilação.</span><span class="sxs-lookup"><span data-stu-id="ddb00-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="ddb00-148">Olá seguinte fragmento instala abra JDK 1.8 juntamente com o Gradle.</span><span class="sxs-lookup"><span data-stu-id="ddb00-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="ddb00-149">bibliotecas de Service Fabric Java Olá são solicitadas do Maven.</span><span class="sxs-lookup"><span data-stu-id="ddb00-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="ddb00-150">Instalar Olá Eclipse Neon Plug-in (opcional)</span><span class="sxs-lookup"><span data-stu-id="ddb00-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="ddb00-151">Pode instalar Olá Plug-in do Eclipse para o Service Fabric do dentro Olá **IDE Eclipse para programadores de Java**.</span><span class="sxs-lookup"><span data-stu-id="ddb00-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="ddb00-152">Pode utilizar aplicações executável do Eclipse toocreate do Service Fabric convidado e aplicações de contentor em aplicações de Java de recursos de infraestrutura de tooService de adição.</span><span class="sxs-lookup"><span data-stu-id="ddb00-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="ddb00-153">No Eclipse, certifique-se de que dispõe de mais recente Eclipse Neon e Olá a versão mais recente do Buildship (1.0.17 ou posterior) instalado.</span><span class="sxs-lookup"><span data-stu-id="ddb00-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="ddb00-154">Pode verificar as versões de Olá componentes instalados selecionando **ajudar** > **detalhes da instalação**.</span><span class="sxs-lookup"><span data-stu-id="ddb00-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="ddb00-155">Pode atualizar Buildship utilizando instruções Olá em [Eclipse Buildship: Eclipse Plug-ins para Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="ddb00-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="ddb00-156">tooinstall Olá, selecione de plug-in do Service Fabric **ajudar** > **instalar novo Software**.</span><span class="sxs-lookup"><span data-stu-id="ddb00-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="ddb00-157">No Olá **trabalhar com** caixa, escreva **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="ddb00-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="ddb00-158">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ddb00-158">Click **Add**.</span></span>

    ![página de Software disponíveis Olá][sf-eclipse-plugin]

5. <span data-ttu-id="ddb00-160">Selecione Olá **ServiceFabric** Plug-in e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="ddb00-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="ddb00-161">Conclua os passos de instalação de Olá e, em seguida, aceite o contrato de licença de utilizador final de Olá.</span><span class="sxs-lookup"><span data-stu-id="ddb00-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="ddb00-162">Se já tiver Olá Service Fabric Eclipse Plug-in instalado, certifique-se de que tem a versão mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="ddb00-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="ddb00-163">Pode verificar selecionando **ajudar** > **detalhes da instalação** e, em seguida, procura na lista de Olá de Service Fabric instalado plug-ins. Se estiver disponível uma versão mais recente, selecione **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="ddb00-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="ddb00-164">Para obter mais informações, veja [Plug-in do Service Fabric para desenvolvimento de aplicações Java de Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="ddb00-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="ddb00-165">Instalar Olá .NET Core SDK (opcional, se pretender que os modelos de programação do .NET Core toouse Olá)</span><span class="sxs-lookup"><span data-stu-id="ddb00-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="ddb00-166">Olá .NET Core SDK fornece bibliotecas Olá e modelos que são necessárias toobuild aos serviços do Service Fabric com .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ddb00-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="ddb00-167">Instalar o pacote de SDK do .NET Core Olá seguindo em execução Olá-</span><span class="sxs-lookup"><span data-stu-id="ddb00-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="ddb00-168">Olá atualização SDK e tempo de execução</span><span class="sxs-lookup"><span data-stu-id="ddb00-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="ddb00-169">tooupdate toohello versão mais recente de Olá SDK e tempo de execução, execute os seguintes comandos de Olá (desselecione Olá SDKs que não pretende):</span><span class="sxs-lookup"><span data-stu-id="ddb00-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="ddb00-170">binários de Java SDK do Olá tooupdate do Maven, terá de tooupdate Olá versão detalhes binário correspondente do Olá no Olá ``build.gradle`` versão mais recente do ficheiro toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="ddb00-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="ddb00-171">tooknow exatamente onde necessita de versão de Olá tooupdate, pode consultar tooany ``build.gradle`` ficheiro nos exemplos de introdução do Service Fabric [aqui](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ddb00-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="ddb00-172">Atualizar pacotes de Olá poderá causar a toostop de cluster de desenvolvimento local em execução.</span><span class="sxs-lookup"><span data-stu-id="ddb00-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="ddb00-173">Reinicie o seu cluster local após uma atualização ao seguir as instruções de Olá nesta página.</span><span class="sxs-lookup"><span data-stu-id="ddb00-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddb00-174">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ddb00-174">Next steps</span></span>

* [<span data-ttu-id="ddb00-175">Criar e implementar a sua primeira aplicação Java do Service Fabric no Linux com o Yeoman</span><span class="sxs-lookup"><span data-stu-id="ddb00-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="ddb00-176">Criar e implementar a sua primeira aplicação Java do Service Fabric no Linux com o Plug-in do Service Fabric para Eclipse</span><span class="sxs-lookup"><span data-stu-id="ddb00-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="ddb00-177">Create your first CSharp application on Linux (Criar a sua primeira aplicação CSharp no Linux)</span><span class="sxs-lookup"><span data-stu-id="ddb00-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="ddb00-178">Prepare your development environment on OSX (Preparar o ambiente de desenvolvimento no OSX)</span><span class="sxs-lookup"><span data-stu-id="ddb00-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="ddb00-179">Utilizar Olá CLI de recursos de infraestrutura de serviço toomanage as suas aplicações</span><span class="sxs-lookup"><span data-stu-id="ddb00-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="ddb00-180">Diferenças do Service Fabric no Windows/Linux</span><span class="sxs-lookup"><span data-stu-id="ddb00-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="ddb00-181">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ddb00-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
