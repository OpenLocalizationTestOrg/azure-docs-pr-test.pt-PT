---
title: "aaaCreate sua primeira baseado em ator Azure microsserviço em Java | Microsoft Docs"
description: "Este tutorial orienta-o pelos passos de Olá da criação, depurar e implementar um serviço baseado em ator simple utilizando o serviço de recursos de infraestrutura Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a>Introdução a Reliable Actors
> [!div class="op_single_selector"]
> * [C# no Windows](service-fabric-reliable-actors-get-started.md)
> * [Java em Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

Este artigo explica Olá Noções básicas do Azure Service Fabric Reliable Actors e explica-lhe como criar e implementar uma aplicação simples de Ator fiável em Java.

## <a name="installation-and-setup"></a>Instalação e configuração
Antes de começar, certifique-se de que tem o ambiente de desenvolvimento do Service Fabric Olá que configurar no seu computador.
Se precisar de tooset-lo, aceda demasiado[introdução no Mac](service-fabric-get-started-mac.md) ou [introdução no Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Conceitos básicos
tooget começar Reliable Actors, apenas é necessário toounderstand alguns conceitos básicos:

* **Serviço de atores**. Reliable Actors são reunidas em Reliable Services que podem ser implementados numa infraestrutura de Service Fabric Olá. Instâncias de ator são ativadas numa instância de serviço com nome.
* **Registo de ator**. Como com Reliable Services, um serviço de Atores fiável tem toobe registado com o tempo de execução do Olá Service Fabric. Além disso, o tipo de ator Olá deve toobe registado com o tempo de execução do Olá Ator.
* **Interface de ator**. interface de ator Olá é utilizado toodefine uma interface pública com tipo seguro de um ator. Na terminologia de modelo de Ator fiável Olá, a interface de ator Olá define Olá tipos de mensagens hello ator podem compreender e processar. interface de ator Olá é utilizado por outros atores e aplicações cliente demasiado "de envio" (no modo assíncrono) ator toohello de mensagens. Reliable Actors podem implementar várias interfaces.
* **Classe de ActorProxy**. Olá ActorProxy classe é utilizada pelo cliente aplicações tooinvoke Olá métodos expostos através da interface de ator Olá. Olá ActorProxy classe fornece duas funcionalidades importantes:
  
  * Resolução de nomes: é capaz de toolocate actor de Olá num cluster de Olá (localizar Olá nó de cluster olá onde está alojado).
  * Processamento de falhas: pode repetir invocações de método e novamente resolver a localização de atores de Olá depois, por exemplo, uma falha de que necessita de Olá ator toobe relocalizada tooanother de nó no cluster de Olá.

Olá seguintes regras que dizem respeito tooactor interfaces é mencionar:

* Métodos de interface de ator não podem estar sobrecarregados.
* Interface de ator métodos não pode ter out, ref ou parâmetros opcionais.
* Interfaces genéricas não são suportadas.

## <a name="create-an-actor-service"></a>Criar um serviço de atores
Comece por criar uma nova aplicação de Service Fabric. Olá para Linux SDK de Service Fabric inclui um Yeoman andaime de Olá tooprovide gerador para uma aplicação de Service Fabric com um serviço sem estado. Comece por executar Olá Yeoman os seguintes comandos:

```bash
$ yo azuresfjava
```

Siga Olá instruções toocreate um **fiável serviço de Atores**. Para este tutorial, nome Olá aplicação "HelloWorldActorApplication" e Olá ator "HelloWorldActor." será criado Olá andaime os seguintes:

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a>Fiáveis blocos modulares básicos Actors
conceitos básicos Olá descritos anteriormente implica Olá blocos modulares básicos de um serviço de Atores fiável.

### <a name="actor-interface"></a>Interface de ator
Esta contém uma definição de interface de Olá para ator Olá. Esta interface define o contrato de ator Olá que é partilhado por clientes de Olá chamar ator Olá, pelo que, normalmente, faz sentido toodefine-lo num local que está separada da implementação de ator Olá e podem ser partilhados por vários outros e de implementação de ator Olá os serviços ou aplicações de cliente.

`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a>Serviço de atores
Contém a implementação de ator e o código de registo de atores. a classe de ator Olá implementa a interface de ator Olá. Isto tem onde o seu ator não respetivo trabalho.

`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a>Registo de ator
serviço de atores Olá tem de ser registado com um tipo de serviço no tempo de execução do Olá Service Fabric. Na ordem de Olá toorun do serviço de Atores as instâncias de ator, o tipo de ator também tem de ser registado com Olá serviço de Atores. Olá `ActorRuntime` método de registo efetua este trabalho de atores.

`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a>Cliente de teste
Esta é uma aplicação de cliente de teste simples pode executar separadamente a partir tootest de aplicação de Service Fabric Olá o serviço de atores. Este é um exemplo de onde Olá ActorProxy pode ser utilizado tooactivate e comunicar com instâncias de atores. É implementado com o serviço.

### <a name="hello-application"></a>aplicação Olá
Por fim, os pacotes de aplicações de Olá Olá serviço de atores e quaisquer outros serviços, que poderá adicionar no Olá futura em conjunto para implementação. Contém Olá *ApplicationManifest.xml* e proprietários de local para o pacote de serviço de atores Olá.

## <a name="run-hello-application"></a>Executar a aplicação Olá

Olá Yeoman andaime inclui um gradle script toobuild Olá bash de aplicações e scripts toodeploy e remover a aplicação. aplicação de Olá toodeploy, primeira aplicação de Olá de compilação com o gradle:

```bash
$ gradle
```

Isto produzirá um pacote de aplicação de Service Fabric que pode ser implementado através de ferramentas da CLI de recursos de infraestrutura de serviço.

### <a name="deploy-service-fabric-cli"></a>Implementar o Service Fabric CLI

script de install.sh Olá contém Olá necessário CLI de recursos de infraestrutura de serviço (sfctl) comandos toodeploy Olá pacote de aplicação.
Execute Olá install.sh script toodeploy Olá aplicação.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Passos seguintes

* [Introdução à CLI do Service Fabric](service-fabric-cli.md)
