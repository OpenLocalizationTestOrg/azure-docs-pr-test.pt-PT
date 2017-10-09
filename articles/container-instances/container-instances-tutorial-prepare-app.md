---
title: "aaaAzure tutorial de instâncias de contentor – preparar a sua aplicação | Documentos do Azure"
description: "Preparar uma aplicação para implementação tooAzure instâncias de contentor"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="954ae-103">Criar contentor para implementação tooAzure instâncias de contentor</span><span class="sxs-lookup"><span data-stu-id="954ae-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="954ae-104">As Instâncias do Azure Container permitem implementar contentores do Docker na infraestrutura do Azure sem que seja necessário aprovisionar máquinas virtuais ou adotar serviços de nível superior.</span><span class="sxs-lookup"><span data-stu-id="954ae-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="954ae-105">Neste tutorial, vai criar uma aplicação Web simples em Node.js e empacotá-lo num contentor que pode ser executado com Instâncias do Azure Container.</span><span class="sxs-lookup"><span data-stu-id="954ae-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="954ae-106">Vamos abordar:</span><span class="sxs-lookup"><span data-stu-id="954ae-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="954ae-107">A clonagem de origens das aplicações a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="954ae-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="954ae-108">A criação de imagens de contentores a partir das origens das aplicações</span><span class="sxs-lookup"><span data-stu-id="954ae-108">Creating container images from application source</span></span>
> * <span data-ttu-id="954ae-109">Testar imagens de Olá num ambiente de Docker local</span><span class="sxs-lookup"><span data-stu-id="954ae-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="954ae-110">Nos tutoriais subsequentes, irá carregar a imagem tooan registo de contentor do Azure e, em seguida, implementá-las tooAzure instâncias de contentor.</span><span class="sxs-lookup"><span data-stu-id="954ae-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="954ae-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="954ae-111">Before you begin</span></span>

<span data-ttu-id="954ae-112">Este tutorial pressupõe conhecimentos básicos dos principais conceitos do Docker, como contentores, imagens de contentores e comandos simples do Docker.</span><span class="sxs-lookup"><span data-stu-id="954ae-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="954ae-113">Se for necessário, veja [Get started with Docker]( https://docs.docker.com/get-started/) (Introdução ao Docker) para obter um manual sobre as noções básicas dos contentores.</span><span class="sxs-lookup"><span data-stu-id="954ae-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="954ae-114">toocomplete neste tutorial, precisa de um ambiente de desenvolvimento do Docker.</span><span class="sxs-lookup"><span data-stu-id="954ae-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="954ae-115">O Docker disponibiliza pacotes que o configuram facilmente em qualquer sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="954ae-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="954ae-116">Obter o código da aplicação</span><span class="sxs-lookup"><span data-stu-id="954ae-116">Get application code</span></span>

<span data-ttu-id="954ae-117">exemplo de Olá neste tutorial inclui uma aplicação web simples incorporada [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="954ae-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="954ae-118">aplicação Olá serve uma página HTML estática e este aspeto:</span><span class="sxs-lookup"><span data-stu-id="954ae-118">hello app serves a static HTML page and looks like this:</span></span>

![Tutorial de aplicação mostrada no browser][aci-tutorial-app]

<span data-ttu-id="954ae-120">Utilize o exemplo de Olá toodownload de git:</span><span class="sxs-lookup"><span data-stu-id="954ae-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="954ae-121">Compilar a imagem de contentor do Olá</span><span class="sxs-lookup"><span data-stu-id="954ae-121">Build hello container image</span></span>

<span data-ttu-id="954ae-122">Olá Dockerfile fornecida no repositório de exemplo de Olá mostra como o contentor de Olá é criada.</span><span class="sxs-lookup"><span data-stu-id="954ae-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="954ae-123">Inicia a partir de um [oficial Node.js imagem] [ dockerhub-nodeimage] com base no [Linux Extreme](https://alpinelinux.org/), uma distribuição pequena que é toouse adequado com contentores.</span><span class="sxs-lookup"><span data-stu-id="954ae-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="954ae-124">Em seguida, copia os ficheiros da aplicação Olá num contentor de Olá, instalar dependências utilizando Olá Gestor de pacotes do nó e, finalmente inicia a aplicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="954ae-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="954ae-125">Olá utilize `docker build` toocreate Olá contentor imagem do comando, marcação como *aci-tutorial-aplicação*:</span><span class="sxs-lookup"><span data-stu-id="954ae-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="954ae-126">Olá utilize `docker images` toosee imagem de Olá incorporada:</span><span class="sxs-lookup"><span data-stu-id="954ae-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="954ae-127">Saída:</span><span class="sxs-lookup"><span data-stu-id="954ae-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="954ae-128">Executar localmente o contentor de Olá</span><span class="sxs-lookup"><span data-stu-id="954ae-128">Run hello container locally</span></span>

<span data-ttu-id="954ae-129">Antes de tentar implementar Olá contentor tooAzure instâncias de contentor, executá-la localmente tooconfirm funciona.</span><span class="sxs-lookup"><span data-stu-id="954ae-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="954ae-130">Olá `-d` comutador permite contentor Olá executadas em segundo plano de Olá, enquanto `-p` permite-lhe toomap uma porta no seu tooport computação 80 no contentor de Olá arbitrária.</span><span class="sxs-lookup"><span data-stu-id="954ae-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="954ae-131">Abra Olá browser toohttp://localhost:8080 tooconfirm que Olá contentor está em execução.</span><span class="sxs-lookup"><span data-stu-id="954ae-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Aplicação Olá em execução localmente no browser Olá][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="954ae-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="954ae-133">Next steps</span></span>

<span data-ttu-id="954ae-134">Neste tutorial, vai criar uma imagem de contentor que pode ser implementado tooAzure instâncias de contentor.</span><span class="sxs-lookup"><span data-stu-id="954ae-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="954ae-135">foram efetuado Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="954ae-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="954ae-136">Origem da aplicação Olá clonagem a partir do GitHub</span><span class="sxs-lookup"><span data-stu-id="954ae-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="954ae-137">A criação de imagens de contentores a partir das origens das aplicações</span><span class="sxs-lookup"><span data-stu-id="954ae-137">Creating container images from application source</span></span>
> * <span data-ttu-id="954ae-138">Testar o contentor de Olá localmente</span><span class="sxs-lookup"><span data-stu-id="954ae-138">Testing hello container locally</span></span>

<span data-ttu-id="954ae-139">Produzir toohello seguinte toolearn tutorial sobre o armazenamento de imagens do contentor num registo de contentor do Azure.</span><span class="sxs-lookup"><span data-stu-id="954ae-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="954ae-140">Push imagens tooAzure registo de contentor</span><span class="sxs-lookup"><span data-stu-id="954ae-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png