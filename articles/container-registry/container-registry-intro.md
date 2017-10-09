---
title: os registos do contentor de Docker aaaPrivate no Azure | Microsoft Docs
description: "Introdução toohello serviço de registo de contentor do Azure, fornecendo baseados na nuvem geridos, os registos do Docker privados."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Registos do contentor de Docker de tooprivate do introdução


Registo de contentor do Azure é um gerido [registo Docker](https://docs.docker.com/registry/) serviço com base na Olá open source Docker registo 2.0. Criar e manter toostore de registos do contentor do Azure e gerir a sua privada [contentor de Docker](https://www.docker.com/what-docker) imagens. Utilize os registos do contentor no Azure com pipelines de implementação e desenvolvimento de contentor existente e desenhar no corpo de Olá de conhecimentos de Comunidade do Docker.

Para obter informações sobre o Docker e os contentores, veja:

* [Docker user guide (Guia de utilizador do Docker)](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Casos de utilização
Solicitar imagens a partir de um contentor do Azure destinos de implementação do registo toovarious:

* **Sistemas de orquestração dimensionáveis** que gerem aplicações contentorizadas em clusters de anfitriões, incluindo [CD/SO](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) e [Kubernetes](http://kubernetes.io/docs/).
* **Serviços do Azure** que suportam a criação e a execução de aplicações em escala, incluindo o [Container Service](../container-service/index.yml), o [Serviço de Aplicações](/app-service/index.md), o [Batch](../batch/index.md), o [Service Fabric](/azure/service-fabric/) e outros.

Os programadores também podem emitir tooa registo de contentor como parte de um fluxo de trabalho de desenvolvimento do contentor. Por exemplo, podem segmentar um registo de contentores de uma ferramenta de integração contínua e programação, como o [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) ou o [Jenkins](https://jenkins.io/).





## <a name="key-concepts"></a>Conceitos-chave
* **Registo** - crie um ou mais registos de contentores na sua subscrição do Azure. Cada registo é copiado por um Azure padrão [conta de armazenamento](../storage/common/storage-introduction.md) no Olá mesma localização. Tire partido do armazenamento local e fecho de rede das suas imagens de contentor, criando um registo na Olá mesma localização do Azure que as implementações. Um nome completamente qualificado de registo tem o formato de Olá `myregistry.azurecr.io`.

  [Controlar o acesso](container-registry-authentication.md) registo de contentor de tooa utilizando uma cópia do Azure Active Directory [principal de serviço](../active-directory/active-directory-application-objects.md) ou uma conta de administrador fornecido. Execute Olá padrão `docker login` tooauthenticate de comando com um registo.

* **Registo Gerido** - uma camada que oferece capacidades adicionais para os registos em três SKUs - Básico, Standard e Premium. imagens de Olá nestes SKUs são armazenadas em contas de armazenamento gerido pelo Olá serviço de registos de contentor do Azure, o que melhora a fiabilidade e permite funcionalidades de novo. As novas capacidades incluem a integração de webhooks, autenticação do repositório no Azure Active Directory e suporte para a funcionalidade de eliminação. Os utilizadores têm Olá opção toochoose entre registos geridos ou toocreate um registo de segurança efetuado pelas suas próprias contas de armazenamento durante a criação de registos.

* **Repositório** - um registo contém um ou mais repositórios, que são grupos de imagens do contentor. O Registo de Contentores do Azure suporta espaços de nomes de repositórios com múltiplos níveis. Esta funcionalidade permite-lhe toogroup coleções de aplicação específica do imagens relacionadas tooa ou uma coleção de aplicações toospecific programação ou para equipas operacionais. Por exemplo:

  * `myregistry.azurecr.io/aspnetcore:1.0.1` representa uma imagem transversal a toda a empresa
  * `myregistry.azurecr.io/warrantydept/dotnet-build`representa uma imagem de aplicações de .NET toobuild, partilhadas em departamento de garantia Olá utilizado
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`representa uma imagem de web, agrupada numa aplicação submissões cliente Olá, pertencente ao departamento de garantia Olá

* **Imagem** - armazenadas num repositório, as imagens são um instantâneo só de leitura de contentores do Docker. O registo de contentores do Azure pode incluir imagens do Windows e do Linux. O utilizador controla os nomes de todas as implementações de contentores. Padrão de utilização [comandos Docker](https://docs.docker.com/engine/reference/commandline/) toopush imagens para um repositório, ou uma imagem a partir de um repositório de extração.

* **Contentor** - um contentor define uma aplicação de software e as respetivas dependências, envoltas num sistema de ficheiros completo, que inclui código, tempo de execução, ferramentas do sistema e bibliotecas. Execute os contentores do Docker com base nas imagens do Windows ou do Linux que extrai de um registo de contentores. Contentores em execução num único computador partilham kernel do sistema operativo de Olá. Os contentores de docker são tooall portabilidade total principais distros de Linux, Mac e Windows.




## <a name="next-steps"></a>Passos seguintes
* [Criar um registo de contentor utilizando Olá portal do Azure](container-registry-get-started-portal.md)
* [Criar um registo de contentor utilizando Olá CLI do Azure](container-registry-get-started-azure-cli.md)
* [Push imagem primeiro utilizar Olá CLI do Docker](container-registry-get-started-docker-cli.md)
* toobuild uma integração contínua e fluxo de trabalho de implementação utilizando o Visual Studio Team Services, o serviço de contentor do Azure e o registo de contentor do Azure, consulte [neste tutorial](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Se quiser tooset segurança o seus próprios registo privado Docker no Azure (sem um ponto de final público), consulte [implementar o seu próprio privada Docker registo no Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
