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
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Criar contentor para implementação tooAzure instâncias de contentor

As Instâncias do Azure Container permitem implementar contentores do Docker na infraestrutura do Azure sem que seja necessário aprovisionar máquinas virtuais ou adotar serviços de nível superior. Neste tutorial, vai criar uma aplicação Web simples em Node.js e empacotá-lo num contentor que pode ser executado com Instâncias do Azure Container. Vamos abordar:

> [!div class="checklist"]
> * A clonagem de origens das aplicações a partir do GitHub  
> * A criação de imagens de contentores a partir das origens das aplicações
> * Testar imagens de Olá num ambiente de Docker local

Nos tutoriais subsequentes, irá carregar a imagem tooan registo de contentor do Azure e, em seguida, implementá-las tooAzure instâncias de contentor.

## <a name="before-you-begin"></a>Antes de começar

Este tutorial pressupõe conhecimentos básicos dos principais conceitos do Docker, como contentores, imagens de contentores e comandos simples do Docker. Se for necessário, veja [Get started with Docker]( https://docs.docker.com/get-started/) (Introdução ao Docker) para obter um manual sobre as noções básicas dos contentores. 

toocomplete neste tutorial, precisa de um ambiente de desenvolvimento do Docker. O Docker disponibiliza pacotes que o configuram facilmente em qualquer sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Obter o código da aplicação

exemplo de Olá neste tutorial inclui uma aplicação web simples incorporada [Node.js](http://nodejs.org). aplicação Olá serve uma página HTML estática e este aspeto:

![Tutorial de aplicação mostrada no browser][aci-tutorial-app]

Utilize o exemplo de Olá toodownload de git:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Compilar a imagem de contentor do Olá

Olá Dockerfile fornecida no repositório de exemplo de Olá mostra como o contentor de Olá é criada. Inicia a partir de um [oficial Node.js imagem] [ dockerhub-nodeimage] com base no [Linux Extreme](https://alpinelinux.org/), uma distribuição pequena que é toouse adequado com contentores. Em seguida, copia os ficheiros da aplicação Olá num contentor de Olá, instalar dependências utilizando Olá Gestor de pacotes do nó e, finalmente inicia a aplicação de Olá.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Olá utilize `docker build` toocreate Olá contentor imagem do comando, marcação como *aci-tutorial-aplicação*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Olá utilize `docker images` toosee imagem de Olá incorporada:

```bash
docker images
```

Saída:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Executar localmente o contentor de Olá

Antes de tentar implementar Olá contentor tooAzure instâncias de contentor, executá-la localmente tooconfirm funciona. Olá `-d` comutador permite contentor Olá executadas em segundo plano de Olá, enquanto `-p` permite-lhe toomap uma porta no seu tooport computação 80 no contentor de Olá arbitrária.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Abra Olá browser toohttp://localhost:8080 tooconfirm que Olá contentor está em execução.

![Aplicação Olá em execução localmente no browser Olá][aci-tutorial-app-local]

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, vai criar uma imagem de contentor que pode ser implementado tooAzure instâncias de contentor. foram efetuado Olá os seguintes passos:

> [!div class="checklist"]
> * Origem da aplicação Olá clonagem a partir do GitHub  
> * A criação de imagens de contentores a partir das origens das aplicações
> * Testar o contentor de Olá localmente

Produzir toohello seguinte toolearn tutorial sobre o armazenamento de imagens do contentor num registo de contentor do Azure.

> [!div class="nextstepaction"]
> [Push imagens tooAzure registo de contentor](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png