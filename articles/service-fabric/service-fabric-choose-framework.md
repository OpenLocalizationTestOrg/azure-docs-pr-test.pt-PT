---
title: "aaaService recursos de infraestrutura programação descrição geral do modelo | Microsoft Docs"
description: "Recursos de infraestrutura de serviço oferece dois estruturas para a criação de serviços: Olá framework ator e a arquitetura de serviços de Olá. Oferecem distintos compromissos na simplicidade e controlo."
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Descrição geral do modelo programação Service Fabric
Recursos de infraestrutura de serviço oferece várias formas toowrite e gerir os seus serviços. Serviços podem escolher toouse Olá APIs de recursos de infraestrutura de serviço tootake tirem o máximo partido das funcionalidades e estruturas de aplicações da plataforma Olá. Os serviços também podem ser qualquer programa do executável compilado escrito em qualquer idioma ou código em execução num contentor simplesmente alojado num cluster do Service Fabric.

## <a name="guest-executables"></a>Executáveis de convidado
A [executável convidado](service-fabric-deploy-existing-app.md) é um existente, o executável arbitrário (escritos em qualquer idioma) que pode ser executado como um serviço na sua aplicação. Executáveis convidado não chamam diretamente Olá APIs do SDK do serviço de recursos de infraestrutura. No entanto, ainda beneficiam da plataforma de Olá funcionalidades oferece, tais como a capacidade de deteção do serviço, o estado de funcionamento personalizado e carga relatórios ao chamar as APIs REST exposta pelo Service Fabric. Também têm o suporte de ciclo de vida de aplicação completa.

Introdução ao executáveis convidado ao implementar o primeiro [aplicação executável convidado](service-fabric-deploy-existing-app.md).

## <a name="containers"></a>Contentores
Por predefinição, o Service Fabric implementa e ativa serviços como processos. Serviço de recursos de infraestrutura também pode implementar serviços no [contentores](service-fabric-containers-overview.md). Serviço de recursos de infraestrutura suporta a implementação do Linux contentores e contentores do Windows no Windows Server 2016. As imagens de contentor podem ser solicitadas a partir de qualquer repositório de contentor e implementado toohello máquina. Pode implementar as aplicações existentes como convidado exectuables, Service Fabric sem monitorização de estado ou com monitorização de estado Reliable services ou Reliable Actors em contentores e podem combinar os serviços de processos e serviços nos contentores no Olá mesma aplicação.

[Saiba mais sobre containerizing os serviços no Windows ou Linux](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
Reliable Services é uma arquitetura de ponderação leve de escrita de serviços que integram com a plataforma de Service Fabric Olá e beneficiam do conjunto completo de Olá das funcionalidades de plataforma. Reliable Services fornecem um conjunto mínimo de APIs que permitem Olá Service Fabric runtime toomanage Olá ciclo de vida dos seus serviços e que permitem que o seu toointeract de serviços com Olá tempo de execução. estrutura da aplicação Olá mínima, que lhe confere completa controlo sobre as opções de design e implementação e pode ser utilizado toohost quaisquer outra estrutura da aplicação, por exemplo, o ASP.NET Core.

Reliable Services podem ser plataformas de serviço toomost sem monitorização de estado, semelhante, tais como servidores web, em que é criada igual a cada instância do serviço de Olá e estado é persistente numa solução externa, como a base de dados do Azure ou o Table Storage do Azure.

Reliable Services também podem ser com monitorização de estado, exclusivo tooService recursos de infraestrutura, onde o estado é persistente diretamente no serviço de Olá próprio através de coleções fiável. O estado é efetuado elevada através da replicação e distribuído através da criação de partições, todos os geridos automaticamente pelo Service Fabric.

[Saiba mais sobre Reliable Services](service-fabric-reliable-services-introduction.md) ou começar por [ao escrever no primeiro serviço fiável](service-fabric-reliable-services-quick-start.md).

## <a name="reliable-actors"></a>Reliable Actors
Desenvolvida Reliable Services, o framework de Ator fiável Olá é uma arquitetura de aplicações que implementa o padrão de Ator Virtual Olá, com base num padrão de conceção de ator Olá. arquitetura de Ator fiável Olá utiliza independentes unidades de estado e de computação com single-threaded execução chamada atores. arquitetura de Ator fiável Olá fornece comunicação incorporada para atores e configurações de persistência e escalável de estado predefinido.

Como Reliable Actors em si é uma arquitetura de aplicações incorporada no Reliable Services, estão totalmente integrado com a plataforma de Service Fabric Olá e os benefícios do conjunto completo de Olá das funcionalidades oferecidas pelas plataforma Olá.

[Saiba mais sobre Reliable Actors](service-fabric-reliable-actors-introduction.md) ou começar por [ao escrever o seu primeiro serviço de Atores fiável](service-fabric-reliable-actors-get-started.md)

## <a name="aspnet-core"></a>Núcleo de ASP.NET
Integra de Service Fabric [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) para criação de serviços Web e API que pode ser incluído como parte da sua aplicação. 

[Criar um serviço de front-end com o ASP.NET Core](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>Passos seguintes
[Descrição geral do Service Fabric e os contentores](service-fabric-containers-overview.md)

[Descrição geral de serviços fiável](service-fabric-reliable-services-introduction.md)

[Descrição geral de serviços fiável](service-fabric-reliable-actors-introduction.md)

[Recursos de infraestrutura de serviço e o ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)




