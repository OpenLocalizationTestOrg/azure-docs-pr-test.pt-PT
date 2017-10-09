---
title: "comunicação remota de aaaService no Service Fabric do Azure | Microsoft Docs"
description: "Comunicação remota do Service Fabric permite que os clientes e serviços toocommunicate com serviços através de uma chamada de procedimento remoto."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a>Comunicação remota do serviço com Reliable Services
> [!div class="op_single_selector"]
> * [C# no Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java em Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

arquitetura de Reliable Services de Olá fornece um tooquickly de mecanismo de comunicação remota e configurar facilmente a chamada de procedimento remoto para os serviços.

## <a name="set-up-remoting-on-a-service"></a>Configurar a gestão remota num serviço
Configurar a gestão remota para um serviço é efetuada em dois passos simples:

1. Crie uma interface para sua tooimplement de serviço. Esta interface define os métodos de Olá que estão disponíveis para uma chamada de procedimento remoto do seu serviço. tem de ser métodos Olá tarefas métodos assíncronos. tem de implementar a interface de Olá `microsoft.serviceFabric.services.remoting.Service` toosignal Olá serviço tem uma interface de gestão remota.
2. Utilize um serviço de escuta de comunicação remota no seu serviço. Este é um `CommunicationListener` implementação que oferece funções de sistema de interação remota. `FabricTransportServiceRemotingListener`pode ser utilizado toocreate um serviço de escuta da gestão remota utilizando o protocolo de transporte de comunicação remota do Olá predefinido.

Por exemplo, hello seguinte serviço sem estado expõe um único método tooget "Olá mundo" através de uma chamada de procedimento remoto.

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> argumentos Olá e Olá devolvem tipos na interface de serviço Olá podem ser qualquer tipos personalizados, simples ou complexos, mas tem de ser serializáveis.
>
>

## <a name="call-remote-service-methods"></a>Chamar os métodos de serviço remoto
Chamar os métodos num serviço utilizando a pilha de comunicação remota de Olá é feito utilizando um serviço de toohello local proxy através de Olá `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe. Olá `ServiceProxyBase` método cria um proxy local utilizando Olá a mesma interface Olá service implementa. Com esse proxy, pode chamar simplesmente métodos na interface de Olá remotamente.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

arquitetura de sistema de interação remota Olá propaga exceções acionadas no cliente do serviço do Olá toohello. Lógica de processamento de exceções, por isso, cliente Olá utilizando `ServiceProxyBase` diretamente pode processar exceções Olá gera de serviço.

## <a name="service-proxy-lifetime"></a>Duração do Proxy de serviço
Criação de ServiceProxy é uma operação simples, para que o utilizador pode criar tantas como precisarem. Proxy de serviço pode ser reutilizado desde que o utilizador precisar dele. Utilizador pode utilizar novamente Olá proxy mesmo em caso de exceção. Cada ServiceProxy contém comunicação cliente utilizado toosend mensagens através de transmissão de Olá. Ao invocar a API, temos toosee verificação interno se o cliente de comunicação utilizada é válido. Com base no que resultam, vamos voltar crie Olá comunicação do cliente. Por conseguinte, o utilizador não é necessário toorecreate serviceproxy em caso de exceção.

### <a name="serviceproxyfactory-lifetime"></a>Duração de ServiceProxyFactory
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) é uma fábrica de que cria o proxy para interfaces de comunicação remota diferente. Se utilizar a API `ServiceProxyBase.create` para criar o proxy, em seguida, framework cria um `FabricServiceProxyFactory`.
É útil toocreate um manualmente quando precisar de toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) propriedades.
Fábrica é uma operação dispendiosa. `FabricServiceProxyFactory`mantém a cache de clientes de comunicação.
Melhor prática é toocache `FabricServiceProxyFactory` há tempo quanto possível.

## <a name="remoting-exception-handling"></a>Processamento de exceções de comunicação remota
Todos os Olá remoto Ocorreu uma excepção ao serviço API, são enviadas como RuntimeException ou FabricException toohello back-cliente.

ServiceProxy processar todas as exceções de ativação pós-falha para a partição de serviço Olá é criado para. Resolve novamente pontos finais de Olá se houver Exceptions(Non-Transient Exceptions) ativação pós-falha e repete chamada Olá com o ponto final do Olá correto. Número de tentativas de ativação pós-falha exceção é indefinido.
Em caso de TransientExceptions, apenas de voltar a chamada de Olá.

Os parâmetros predefinidos de repetição são fornecidos por [OperationRetrySettings]. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Utilizador pode configurar estes valores através da transmissão de construtor de tooServiceProxyFactory OperationRetrySettings objeto.

## <a name="next-steps"></a>Passos seguintes
* [Proteger a comunicação para Reliable Services](service-fabric-reliable-services-secure-communication.md)
