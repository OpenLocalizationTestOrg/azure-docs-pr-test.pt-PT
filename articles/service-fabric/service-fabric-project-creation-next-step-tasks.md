---
title: "passos de criação de projeto dos recursos de infraestrutura do aaaService seguintes | Microsoft Docs"
description: "Este artigo contém ligações tooa conjunto de tarefas de desenvolvimento de núcleos de Service Fabric"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>A aplicação de Service Fabric e os passos seguintes
Foi criada a sua aplicação de Service Fabric do Azure. Este artigo descreve makeup Olá do seu projeto e alguns passos potenciais.

## <a name="your-application"></a>A aplicação
Cada nova aplicação inclui um projeto de aplicação. Pode haver um ou dois projetos adicionais, dependendo do tipo de Olá de serviço escolhido.

### <a name="hello-application-project"></a>projeto de aplicação Olá
projeto de aplicação Olá consiste em:

* Um conjunto de serviços de toohello referências que compõem a sua aplicação.
* Publicar três perfis (1-nó Local, 5-nó Local e nuvem) que pode utilizar as preferências de toomaintain para trabalhar com ambientes diferentes – como o ponto final de cluster do preferências tooa relacionados e se tooperform atualizar implementações por predefinição.
* Três ficheiros parâmetro da aplicação (igual ao acima) que pode utilizar configurações de aplicação específico do ambiente de toomaintain, como número de Olá de partições toocreate para um serviço.
* Um script de implementação que é possível utilizar toodeploy a aplicação a partir da linha de comandos Olá ou como parte de um pipeline de integração e a implementação contínuo automatizado.
* Olá manifesto da aplicação, que descreve a aplicação Olá. Pode encontrar o manifesto de Olá na pasta de ApplicationPackageRoot Olá.

### <a name="stateless-service"></a>Sem estado
Quando adiciona um novo serviço sem monitorização de estado, o Visual Studio adiciona uma solução de tooyour do projeto de serviço que inclui um tipo descended de `StatelessService`. serviço de Olá incrementa uma variável local um contador.

### <a name="stateful-service"></a>Serviço com estado
Quando adiciona um novo serviço de monitorização de estado, o Visual Studio adiciona uma solução de tooyour do projeto de serviço que inclui um tipo descended de `StatefulService`. Olá serviço incrementos de um contador no respetivo `RunAsync` método e arquivos Olá resultado um `ReliableDictionary`.

### <a name="actor-service"></a>Serviço de atores
Quando adiciona um novo ator fiável, Visual Studio adiciona a solução de tooyour dois projetos: um projeto de ator e um projeto de interface.

projeto de ator Olá fornece métodos para definição e ao obter valor Olá de um contador que é fiável continuado no estado do ator Olá. Olá interface projeto fornece uma interface que outros serviços pode utilizar o actor de Olá tooinvoke.

### <a name="stateless-web-api"></a>API de Web sem monitorização de estado
projeto Web API sem monitorização de estado do Olá fornece num nível básico que é possível utilizar tooopen os clientes de tooexternal de aplicação de serviço web. Para obter mais informações sobre como o projeto de Olá estruturados, consulte [serviços de API Web do Service Fabric com OWIN automática de alojamento](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>Núcleo ASP.NET
Olá SDK de Service Fabric fornece Olá mesmo conjunto de modelos de núcleo de ASP.NET que estão disponíveis para autónomo ASP.NET Core projetos: vazio, [Web API][aspnet-webapi], e [aplicação Web][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Contentores executáveis e de convidado de convidado

Um recurso de infraestrutura do serviço 'Convidado' é um serviço que não está incorporado com modelos de programação da plataforma Olá. Pode compactar binários Olá para um convidado está [diretamente no pacote de aplicação Olá](service-fabric-deploy-existing-app.md) ou [através de uma imagem de contentor](service-fabric-deploy-container.md). Em ambos os casos, o Visual Studio cria Olá artefactos necessários em Olá **ApplicationPackageRoot** na pasta do projeto de aplicação Olá. Visual Studio não irá criar um novo projeto de serviço porque o código de Olá já existe noutro local. Se quiser toomanage o convidado projetos em conjunto com o projeto de aplicação de Service Fabric Olá, pode adicioná-los toohello mesma solução Visual Studio.

## <a name="next-steps"></a>Passos seguintes
### <a name="create-an-azure-cluster"></a>Criar um cluster do Azure
Olá SDK de Service Fabric fornece um cluster local para desenvolvimento e testes. toocreate um cluster no Azure, consulte [configurar um cluster do Service Fabric do portal do Azure de Olá][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Publicar a aplicação tooAzure
Pode publicar a aplicação diretamente a partir do Visual Studio tooan cluster do Azure. como, consulte toolearn [publicar a aplicação tooAzure][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Utilizar o cluster de Service Fabric Explorer toovisualize
Service Fabric Explorer proporciona uma forma fácil toovisualize o cluster, incluindo aplicações implementadas e o esquema físico. toolearn mais, consulte [visualizar o cluster utilizando o Service Fabric Explorer][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Versão e atualizar os serviços
Service Fabric permite o controlo de versões independente e atualização dos serviços independentes de uma aplicação. toolearn mais, consulte [controlo de versões e atualizar os serviços][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Configurar a integração contínua com o Visual Studio Team Services
toolearn como pode configurar um processo de integração contínua para a sua aplicação de Service Fabric, consulte [configurar a integração contínua com o Visual Studio Team Services][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
