---
title: "aaaCreate o primeiro e fiável microsserviço do Azure em Java | Microsoft Docs"
description: "Introdução toocreating uma aplicação do Microsoft Azure Service Fabric com serviços sem monitorização de estado e com monitorização de estado."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Introdução ao Reliable Services
> [!div class="op_single_selector"]
> * [C# no Windows](service-fabric-reliable-services-quick-start.md)
> * [Java em Linux](service-fabric-reliable-services-quick-start-java.md)
>
>

Este artigo explica Olá Noções básicas do Azure Service Fabric Reliable Services e explica-lhe como criar e implementar uma aplicação de serviço fiável simple escrita em Java. Este vídeo Microsoft Virtual Academy mostra também como toocreate um serviço fiável sem monitorização de estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a>Instalação e configuração
Antes de começar, certifique-se de que tem o ambiente de desenvolvimento do Service Fabric Olá que configurar no seu computador.
Se precisar de tooset-lo, aceda demasiado[introdução no Mac](service-fabric-get-started-mac.md) ou [introdução no Linux](service-fabric-get-started-linux.md).

## <a name="basic-concepts"></a>Conceitos básicos
tooget começar Reliable Services, apenas é necessário toounderstand alguns conceitos básicos:

* **Tipo de serviço**: Esta é a implementação de serviço. Está definido por classe de Olá escreve que expande `StatelessService` e quaisquer outras código ou dependências utilizadas nas mesmas, juntamente com um nome e um número de versão.
* **Com o nome de instância de serviço**: toorun seu serviço, criar instâncias nomeadas do seu tipo de serviço, muito como criar instâncias do objecto de um tipo de classe. Instâncias de serviço são de facto instâncias de objeto da sua classe de serviço escreve.
* **Anfitrião do serviço**: Olá instâncias de serviço criar necessidade toorun dentro de um anfitrião com o nome. anfitrião do serviço Olá é apenas um processo em que podem executar instâncias do seu serviço.
* **Serviço de registo**: registo reúne tudo. Olá o tipo de serviço tem de ser registado com Olá Service Fabric runtime num serviço alojem tooallow Service Fabric toocreate instâncias do mesmo toorun.  

## <a name="create-a-stateless-service"></a>Criar um serviço sem monitorização de estado
Comece por criar uma aplicação de Service Fabric. Olá para Linux SDK de Service Fabric inclui um Yeoman andaime de Olá tooprovide gerador para uma aplicação de Service Fabric com um serviço sem estado. Comece por executar Olá Yeoman os seguintes comandos:

```bash
$ yo azuresfjava
```

Siga Olá instruções toocreate um **sem monitorização de estado de serviço fiável**. Para este tutorial, a aplicação de Olá nome "HelloWorldApplication" e a Olá do serviço "Olámundo". resultado de Olá inclui diretórios para Olá `HelloWorldApplication` e `HelloWorld`.

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a>Implementar o serviço de Olá
Abra **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**. Esta classe define o tipo de serviço Olá e pode executar qualquer código. API do serviço Olá fornece dois pontos de entrada para o seu código:

* Um método de ponto de entrada open-ended, denominado `runAsync()`, onde pode começar a executar quaisquer cargas de trabalho, incluindo as cargas de trabalho de computação de execução longa.

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* Um ponto de entrada de comunicação em que pode plug-in a pilha de comunicação de eleição. Este é onde pode começar a receber pedidos de utilizadores e outros serviços.

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

Neste tutorial, iremos focar-se no Olá `runAsync()` o método de ponto de entrada. Este é onde imediatamente pode começar a executar o seu código.

### <a name="runasync"></a>Runasync com
plataforma de Olá chama este método quando uma instância de um serviço é tooexecute pronto e colocá-la. Para um serviço sem monitorização de estado, basta que significa quando a instância de serviço Olá é aberta. Um token de cancelamento é fornecido toocoordinate quando a instância de serviço tem toobe fechado. No Service Fabric, este ciclo de abertura/fecho de uma instância de serviço pode ocorrer demasiadas vezes ao longo da duração Olá de serviço Olá como um todo. Esta situação pode ocorrer por vários motivos, incluindo:

* sistema de Olá move as instâncias de serviço para balanceamento de recurso.
* Falhas ocorrerem no seu código.
* aplicação Olá ou do sistema está atualizado.
* hardware subjacente Olá sofre uma falha.

Esta orquestração é gerida pelo Service Fabric tookeep seu serviço altamente disponível e corretamente equilibrado.

`runAsync()`não deverá bloquear forma síncrona. A implementação de runasync com deverá devolver um CompletableFuture tooallow Olá runtime toocontinue. Se a carga de trabalho tem uma tarefa de execução longa que deve ser efetuada dentro de tooimplement Olá CompletableFuture.

#### <a name="cancellation"></a>Cancelamento
O cancelamento da sua carga de trabalho é um esforço cooperative orquestrado por Olá fornecido o token de cancelamento. sistema de Olá aguarda tooend sua tarefa (por conclusão com êxito, cancelamento ou falhas) antes de se move. É importante toohonor Olá cancelamento token, concluir qualquer trabalho e sair `runAsync()` mais rapidamente possível ao sistema de Olá pedidos de cancelamento. Olá exemplo seguinte demonstra como toohandle um evento de cancelamento:

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a>Registo do serviço
Tipos de serviço tem de ser registados com o tempo de execução do Olá Service Fabric. tipo de serviço de Olá está definido no Olá `ServiceManifest.xml` e a classe de serviço que implementa `StatelessService`. Registo do serviço é executado no ponto de entrada principal do processo de Olá. Neste exemplo, Olá o processo de ponto de entrada principal é `HelloWorldServiceHost.java`:

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a>Executar a aplicação Olá

Olá Yeoman andaime inclui um gradle script toobuild Olá bash de aplicações e scripts toodeploy e remover a aplicação. aplicação de Olá toorun, primeira aplicação de Olá de compilação com o gradle:

```bash
$ gradle
```

Isto produz um pacote de aplicação de Service Fabric pode ser implementado utilizando a CLI de recursos de infraestrutura de serviço.

### <a name="deploy-with-service-fabric-cli"></a>Implementar com a CLI do Service Fabric

script de install.sh Olá contém Olá necessário CLI de recursos de infraestrutura de serviço comandos toodeploy Olá pacote de aplicação. Execute a aplicação de Olá install.sh script toodeploy.

```bash
$ ./install.sh
```

## <a name="next-steps"></a>Passos seguintes

* [Introdução à CLI do Service Fabric](service-fabric-cli.md)
