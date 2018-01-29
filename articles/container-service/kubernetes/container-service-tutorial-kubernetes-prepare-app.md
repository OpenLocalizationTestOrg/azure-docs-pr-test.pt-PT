---
title: "Tutorial de serviço de contentor do Azure – preparar aplicações"
description: "Tutorial de serviço de contentor do Azure – preparar aplicações"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3dcfc0d454926d6040692b0e8a9d44b13e7603c5
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/06/2017
---
# <a name="create-container-images-to-be-used-with-azure-container-service"></a>Criar contentor de imagens para ser utilizado com o serviço de contentor do Azure

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

Neste tutorial, a parte de um dos sete, uma aplicação de contentor multi está preparada para utilização em Kubernetes. Passos concluídos incluem:  

> [!div class="checklist"]
> * A clonagem de origens das aplicações a partir do GitHub  
> * Criar uma imagem de contentor da origem de aplicação
> * Testar a aplicação num ambiente de Docker local

Depois de concluída, a aplicação seguinte está acessível no seu ambiente de desenvolvimento local.

![Imagem do cluster do Kubernetes no Azure no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

Nos tutoriais subsequentes, a imagem do contentor é carregada para um registo de contentor do Azure e, em seguida, executar num Azure alojada Kubernetes cluster.

## <a name="before-you-begin"></a>Antes de começar

Este tutorial pressupõe conhecimentos básicos dos principais conceitos do Docker, como contentores, imagens de contentores e comandos simples do Docker. Se for necessário, veja [Get started with Docker]( https://docs.docker.com/get-started/) (Introdução ao Docker) para obter um manual sobre as noções básicas dos contentores. 

Para concluir este tutorial, precisa de um ambiente de desenvolvimento do Docker. O Docker disponibiliza pacotes que o configuram facilmente em qualquer sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

Shell de nuvem do Azure não inclui os componentes de Docker necessários para concluir cada passo neste tutorial. Por conseguinte, recomendamos a utilização de um ambiente de desenvolvimento do Docker completo.

## <a name="get-application-code"></a>Obter o código da aplicação

A aplicação de exemplo utilizada neste tutorial, é uma aplicação de voto básica. A aplicação é composta por um componente de front-end web e uma instância de Redis do back-end. O componente de web é empacotado para uma imagem personalizada do contentor. A instância de Redis utiliza uma imagem inalterada do Hub de Docker.  

Utilize o git para transferir uma cópia da aplicação para o ambiente de desenvolvimento.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Altere os diretórios para que estiver a trabalhar a partir do diretório clonado.

```
cd azure-voting-app-redis
```

Dentro do diretório é o código fonte da aplicação, um pré-criadas Docker compose ficheiro e um ficheiro de manifesto Kubernetes. Estes ficheiros são utilizados em todo o conjunto de tutorial. 

## <a name="create-container-images"></a>Criar imagens de contentor

[Docker Compose](https://docs.docker.com/compose/) pode ser utilizada para automatizar a compilação fora das imagens de contentor e a implementação de aplicações de várias contentor.

Execute o `docker-compose.yml` ficheiros para criar a imagem do contentor, transferir a imagem de Redis e iniciar a aplicação.

```bash
docker-compose up -d
```

Quando tiver terminado, utilize o [imagens docker](https://docs.docker.com/engine/reference/commandline/images/) comando para ver as imagens criadas.

```bash
docker images
```

Tenha em atenção que foram transferidas ou criadas três imagens. O `azure-vote-front` imagem contém a aplicação e utiliza o `nginx-flask` imagem como base. O `redis` imagem é utilizada para iniciar uma instância de Redis.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Execute o [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) comando para ver os contentores em execução.

```bash
docker ps
```

Saída:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Testar a aplicação localmente

Procure http://localhost:8080 para ver a aplicação em execução.

![Imagem do cluster do Kubernetes no Azure no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Limpar recursos

Agora que a funcionalidade da aplicação foi validada, os contentores em execução podem ser parados e removidos. Não elimine as imagens de contentor. O `azure-vote-front` imagem é carregada para uma instância de registo de contentor do Azure no tutorial seguinte.

Execute o seguinte para parar os contentores em execução.

```bash
docker-compose stop
```

Elimine os contentores parados e os recursos com o seguinte comando.

```bash
docker-compose down
```

Após a conclusão, ter uma imagem de contentor que contém a aplicação de voto do Azure.

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, uma aplicação foi testada e imagens de contentor criado para a aplicação. Foram efetuados os seguintes passos:

> [!div class="checklist"]
> * Clonagem da origem da aplicação a partir do GitHub  
> * Criar uma imagem de contentor da origem da aplicação
> * Testar a aplicação num ambiente de Docker local

Avance para o próximo tutorial para saber mais sobre o armazenamento das imagens de contentores em registos do Azure Container Registry.

> [!div class="nextstepaction"]
> [Push images to Azure Container Registry](./container-service-tutorial-kubernetes-prepare-acr.md) (Enviar imagens para o Azure Container Registry)
