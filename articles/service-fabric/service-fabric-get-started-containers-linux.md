---
title: "aaaCreate uma aplicação de contentor do Azure Service Fabric no Linux | Microsoft Docs"
description: "Crie a sua primeira aplicação de contentor do Linux no Azure Service Fabric.  Construir uma imagem do Docker com a sua aplicação, push o registo de contentor do Olá imagem tooa, criar e implementar uma aplicação de contentor do Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="50743-104">Criar a sua primeira aplicação de contentor do Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="50743-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50743-105">Windows</span><span class="sxs-lookup"><span data-stu-id="50743-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="50743-106">Linux</span><span class="sxs-lookup"><span data-stu-id="50743-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="50743-107">Executar uma aplicação existente num contentor Linux num cluster de Service Fabric não necessita de qualquer aplicação tooyour de alterações.</span><span class="sxs-lookup"><span data-stu-id="50743-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="50743-108">Este artigo explica como criar uma imagem de Docker que contém um Python [Flask](http://flask.pocoo.org/) web de aplicação e implementar a política tooa cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="50743-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="50743-109">Também vai partilhar a sua aplicação contentorizada através do [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="50743-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="50743-110">Este artigo pressupõe uma compreensão básica do Docker.</span><span class="sxs-lookup"><span data-stu-id="50743-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="50743-111">Pode saber mais sobre o Docker por ler Olá [descrição geral do Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="50743-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50743-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="50743-112">Prerequisites</span></span>
* <span data-ttu-id="50743-113">Um computador de programação com:</span><span class="sxs-lookup"><span data-stu-id="50743-113">A development computer running:</span></span>
  * <span data-ttu-id="50743-114">[SDK e ferramentas do Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="50743-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="50743-115">[Docker CE para Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="50743-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="50743-116">CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="50743-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="50743-117">Um registo no Azure Container Registry - [Criar um registo de contentor](../container-registry/container-registry-get-started-portal.md) na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="50743-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="50743-118">Definir o contentor de Docker Olá</span><span class="sxs-lookup"><span data-stu-id="50743-118">Define hello Docker container</span></span>
<span data-ttu-id="50743-119">Criar uma imagem com base no Olá [imagem Python](https://hub.docker.com/_/python/) localizado no Hub de Docker.</span><span class="sxs-lookup"><span data-stu-id="50743-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="50743-120">Defina o contentor do Docker num Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="50743-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="50743-121">Olá Dockerfile contém instruções para configurar o ambiente de Olá no interior do contentor, carregar a aplicação Olá pretende toorun e mapeamento de portas.</span><span class="sxs-lookup"><span data-stu-id="50743-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="50743-122">Olá Dockerfile é toohello entrada Olá `docker build` comando, que cria Olá imagem.</span><span class="sxs-lookup"><span data-stu-id="50743-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="50743-123">Criar um diretório vazio e criar o ficheiro de Olá *Dockerfile* (com nenhuma extensão de ficheiro).</span><span class="sxs-lookup"><span data-stu-id="50743-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="50743-124">Adicionar Olá seguir demasiado*Dockerfile* e guarde as alterações:</span><span class="sxs-lookup"><span data-stu-id="50743-124">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="50743-125">Olá leitura [Dockerfile referência](https://docs.docker.com/engine/reference/builder/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="50743-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="50743-126">Criar uma aplicação Web simples</span><span class="sxs-lookup"><span data-stu-id="50743-126">Create a simple web application</span></span>
<span data-ttu-id="50743-127">Crie uma aplicação web Flask que escute na porta 80 e que devolva "Hello World!".</span><span class="sxs-lookup"><span data-stu-id="50743-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="50743-128">No mesmo diretório de Olá, criar ficheiro de Olá *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="50743-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="50743-129">Adicione o seguinte Olá e guardar as alterações:</span><span class="sxs-lookup"><span data-stu-id="50743-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="50743-130">Também criar Olá *app.py* de ficheiros e adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="50743-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="50743-131">Compilar Olá imagem</span><span class="sxs-lookup"><span data-stu-id="50743-131">Build hello image</span></span>
<span data-ttu-id="50743-132">Executar Olá `docker build` comando toocreate Olá imagem, que executa a aplicação web.</span><span class="sxs-lookup"><span data-stu-id="50743-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="50743-133">Abra uma janela do PowerShell e navegue demasiado*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="50743-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="50743-134">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="50743-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="50743-135">Este comando compilações Olá nova imagem utilizando instruções Olá no seu Dockerfile nomenclatura (-t etiquetagem) imagem Olá "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="50743-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="50743-136">Criar uma imagem obtém a imagem base Olá para baixo do Docker Hub e cria uma nova imagem que adiciona a sua aplicação em cima da imagem base Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="50743-137">Após a conclusão do comando de compilação de Olá, execute Olá `docker images` toosee sobre a nova imagem de Olá de comando:</span><span class="sxs-lookup"><span data-stu-id="50743-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="50743-138">Executar a aplicação Olá localmente</span><span class="sxs-lookup"><span data-stu-id="50743-138">Run hello application locally</span></span>
<span data-ttu-id="50743-139">Certifique-se de que a sua aplicação de é executada localmente antes de enviar-registo de contentor Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="50743-140">Executar a aplicação Olá, mapeamento do contentor do seu computador, porta 4000 toohello expostos a porta 80:</span><span class="sxs-lookup"><span data-stu-id="50743-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="50743-141">*nome* fornece toohello um nome com o contentor (em vez do ID de contentor Olá).</span><span class="sxs-lookup"><span data-stu-id="50743-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="50743-142">Ligar toohello com o contentor.</span><span class="sxs-lookup"><span data-stu-id="50743-142">Connect toohello running container.</span></span>  <span data-ttu-id="50743-143">Abra um browser apontar toohello endereço IP devolvido na porta 4000, por exemplo "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="50743-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="50743-144">Deverá ver Olá cabeçalho "Olá mundo!"</span><span class="sxs-lookup"><span data-stu-id="50743-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="50743-145">apresentar num browser de Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-145">display in hello browser.</span></span>

![Hello World!][hello-world]

<span data-ttu-id="50743-147">toostop o contentor, execute:</span><span class="sxs-lookup"><span data-stu-id="50743-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="50743-148">Elimine o contentor de Olá a partir do seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="50743-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="50743-149">Registo de contentor do push Olá imagem toohello</span><span class="sxs-lookup"><span data-stu-id="50743-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="50743-150">Depois de verificar que a aplicação Olá é executada no Docker, emitir o registo de tooyour Olá imagem no registo de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="50743-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="50743-151">Executar `docker login` toolog no registo de contentor tooyour com seu [credenciais do registo](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="50743-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="50743-152">Olá seguinte exemplo, passa Olá ID e palavra-passe de um Azure Active Directory [principal de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="50743-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="50743-153">Por exemplo, poderá ter atribuído um registo de principal tooyour de serviço para um cenário de automatização.</span><span class="sxs-lookup"><span data-stu-id="50743-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="50743-154">Em alternativa, pode iniciar sessão com o nome de utilizador e a palavra-passe do registo.</span><span class="sxs-lookup"><span data-stu-id="50743-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="50743-155">Olá comando seguinte cria uma etiqueta, ou alias, da imagem de Olá, com um registo de tooyour caminho completamente qualificado.</span><span class="sxs-lookup"><span data-stu-id="50743-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="50743-156">Neste exemplo locais Olá imagem no Olá `samples` espaço de nomes tooavoid clutter na raiz de Olá do registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="50743-157">Registo de contentor do push Olá imagem tooyour:</span><span class="sxs-lookup"><span data-stu-id="50743-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="50743-158">O pacote de imagem de Docker Olá com Yeoman</span><span class="sxs-lookup"><span data-stu-id="50743-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="50743-159">Olá para Linux SDK de Service Fabric inclui um [Yeoman](http://yeoman.io/) gerador que torna mais fácil toocreate a aplicação e adicionar uma imagem de contentor.</span><span class="sxs-lookup"><span data-stu-id="50743-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="50743-160">Vamos utilizar Yeoman toocreate chamada de uma aplicação com um único contentor de Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="50743-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="50743-161">toocreate uma aplicação de contentor do Service Fabric, abra uma janela de terminal e execute `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="50743-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="50743-162">Dê um nome à aplicação (por exemplo, “mycontainer”).</span><span class="sxs-lookup"><span data-stu-id="50743-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="50743-163">Fornecer Olá URL para a imagem de contentor Olá no registo de contentor (por exemplo, "").</span><span class="sxs-lookup"><span data-stu-id="50743-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="50743-164">Esta imagem tem uma carga de trabalho ponto de entrada definido, por isso, tem de tooexplicitly especifique comandos de entrada (executados no interior do contentor de Olá, que irá manter o contentor de Olá executar após o arranque de comandos).</span><span class="sxs-lookup"><span data-stu-id="50743-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="50743-165">Especifique uma contagem de instâncias de "1".</span><span class="sxs-lookup"><span data-stu-id="50743-165">Specify an instance count of "1".</span></span>

![Gerador Yeoman do Service Fabric para contentores][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="50743-167">Configurar o mapeamento de portas e a autenticação do repositório de contentores</span><span class="sxs-lookup"><span data-stu-id="50743-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="50743-168">O seu serviço contentorizado precisa de um ponto final para comunicação.</span><span class="sxs-lookup"><span data-stu-id="50743-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="50743-169">Agora adicione Olá protocolo, porta e tipo tooan `Endpoint` no ficheiro de ServiceManifest.xml Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="50743-170">Para este artigo, o serviço de Olá de escuta na porta 4000:</span><span class="sxs-lookup"><span data-stu-id="50743-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="50743-171">Fornecer Olá `UriScheme` automaticamente regista Olá ponto final de contentor com Olá Service Fabric Naming service para deteção.</span><span class="sxs-lookup"><span data-stu-id="50743-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="50743-172">Um ficheiro de exemplo ServiceManifest.xml completo é fornecido no fim de Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="50743-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="50743-173">Configurar o mapeamento de porta de anfitrião de porta do contentor de Olá, especificando um `PortBinding` política no `ContainerHostPolicies` do ficheiro de ApplicationManifest.xml Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="50743-174">Para este artigo, `ContainerPort` é 80 (contentor de Olá expõe a porta 80, como especificado no Olá Dockerfile) e `EndpointRef` é "myserviceTypeEndpoint" (Olá ponto final definido no manifesto do serviço de Olá).</span><span class="sxs-lookup"><span data-stu-id="50743-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="50743-175">Os pedidos recebidos toohello serviço na porta 4000 estão mapeados tooport 80 no contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="50743-176">Se o contentor tem tooauthenticate com um repositório privado, em seguida, adicione `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="50743-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="50743-177">Para este artigo, adicione nome Olá da conta e palavra-passe para Olá myregistry.azurecr.io contentor de registo.</span><span class="sxs-lookup"><span data-stu-id="50743-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="50743-178">Compilação e pacote de aplicação de Service Fabric Olá</span><span class="sxs-lookup"><span data-stu-id="50743-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="50743-179">modelos de serviço Fabric Yeoman Olá incluem um script de compilação para [Gradle](https://gradle.org/), que pode utilizar a aplicação Olá toobuild Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="50743-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="50743-180">toobuild e pacote Olá aplicação, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="50743-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="50743-181">Implementar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="50743-181">Deploy hello application</span></span>
<span data-ttu-id="50743-182">Uma vez que é criada a aplicação Olá, pode implementá-la toohello cluster local com Olá CLI de recursos de infraestrutura de serviço.</span><span class="sxs-lookup"><span data-stu-id="50743-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="50743-183">Ligue o cluster do Service Fabric local toohello.</span><span class="sxs-lookup"><span data-stu-id="50743-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="50743-184">Olá utilize instalar o script fornecido no Olá modelo toocopy aplicação Olá arquivo de imagens do cluster toohello do pacote, registar o tipo de aplicação Olá e criar uma instância da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="50743-185">Abra um browser e navegue tooService Explorador de recursos de infraestrutura em http://localhost:19080/Explorer (substituir localhost com Olá IP privado de Olá VM se utilizar Vagrant no Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="50743-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="50743-186">Expanda o nó de aplicações de Olá e observe que não existe agora uma entrada para o tipo de aplicação e outro para Olá primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="50743-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="50743-187">Ligar toohello com o contentor.</span><span class="sxs-lookup"><span data-stu-id="50743-187">Connect toohello running container.</span></span>  <span data-ttu-id="50743-188">Abra um browser apontar toohello endereço IP devolvido na porta 4000, por exemplo "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="50743-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="50743-189">Deverá ver Olá cabeçalho "Olá mundo!"</span><span class="sxs-lookup"><span data-stu-id="50743-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="50743-190">apresentar num browser de Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-190">display in hello browser.</span></span>

![Hello World!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="50743-192">Limpeza</span><span class="sxs-lookup"><span data-stu-id="50743-192">Clean up</span></span>
<span data-ttu-id="50743-193">Utilizar script de desinstalação de Olá fornecido na instância da aplicação de Olá modelo toodelete Olá do cluster de desenvolvimento local Olá e anular o registo do tipo de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="50743-194">Depois de push o registo de contentor do Olá imagem toohello pode eliminar imagem local Olá do seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="50743-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="50743-195">Exemplo completo da aplicação do Service Fabric e dos manifestos do serviço</span><span class="sxs-lookup"><span data-stu-id="50743-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="50743-196">Seguem-se o serviço concluído Olá e os manifestos da aplicação utilizados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="50743-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="50743-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="50743-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="50743-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="50743-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="50743-199">Adicionar mais serviços tooan aplicação existente</span><span class="sxs-lookup"><span data-stu-id="50743-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="50743-200">executar a aplicação de tooan de serviço de contentor outro já criada utilizando yeoman, tooadd Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="50743-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="50743-201">Alterar a raiz de toohello do diretório da aplicação existente Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="50743-202">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é aplicação Olá criada pelo Yeoman.</span><span class="sxs-lookup"><span data-stu-id="50743-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="50743-203">Execute `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="50743-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="50743-204">Configurar o intervalo de tempo antes do contentor ser forçado a terminar</span><span class="sxs-lookup"><span data-stu-id="50743-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="50743-205">Pode configurar um intervalo de tempo para Olá runtime toowait antes do contentor de Olá é removida após hello eliminação do serviço (ou um nó de tooanother mover) foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="50743-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="50743-206">Intervalo de tempo de Olá configurar envia Olá `docker stop <time in seconds>` contentor toohello de comando.</span><span class="sxs-lookup"><span data-stu-id="50743-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="50743-207">Para obter mais detalhes, veja [paragem do docker](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="50743-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="50743-208">toowait de intervalo de tempo de Olá especificado nas Olá `Hosting` secção.</span><span class="sxs-lookup"><span data-stu-id="50743-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="50743-209">Olá fragmento de manifesto do cluster a seguir mostra como tooset Olá Aguarde intervalo:</span><span class="sxs-lookup"><span data-stu-id="50743-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
<span data-ttu-id="50743-210">Olá intervalo de tempo predefinido estiver definido too10 segundos.</span><span class="sxs-lookup"><span data-stu-id="50743-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="50743-211">Uma vez que esta configuração for dinâmica, uma configuração atualizar-se apenas no tempo limite do Olá cluster atualizações Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="50743-212">Configurar Olá runtime tooremove imagens do contentor não utilizadas</span><span class="sxs-lookup"><span data-stu-id="50743-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="50743-213">Pode configurar tooremove de cluster do Service Fabric Olá imagens do contentor não utilizado a partir do nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="50743-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="50743-214">Esta configuração permite toobe de espaço em disco recaptured se estiverem presentes no nó de Olá demasiados de contentor de imagens.</span><span class="sxs-lookup"><span data-stu-id="50743-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="50743-215">tooenable desta funcionalidade, a atualização Olá `Hosting` secção manifesto do cluster Olá conforme mostrado no Olá seguinte fragmento:</span><span class="sxs-lookup"><span data-stu-id="50743-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

<span data-ttu-id="50743-216">Para imagens que não devem ser eliminadas, pode especificá-las em Olá `ContainerImagesToSkip` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="50743-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="50743-217">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="50743-217">Next steps</span></span>
* <span data-ttu-id="50743-218">Saiba mais sobre como executar [contentores no Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50743-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="50743-219">Olá leitura [implementar uma aplicação .NET num contentor](service-fabric-host-app-in-a-container.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="50743-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="50743-220">Saiba mais sobre Olá Service Fabric [ciclo de vida de aplicação](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="50743-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="50743-221">Olá finalizar [exemplos de código do contentor de Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="50743-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
