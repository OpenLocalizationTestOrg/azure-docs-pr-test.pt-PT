---
title: "aaaHelp comunicação segura para serviços no Azure Service Fabric | Microsoft Docs"
description: "Descrição geral de como toohelp proteger a comunicação para fiáveis serviços que estão em execução num cluster do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Ajudar a comunicação segura para serviços no Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# no Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java em Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

A segurança é um dos aspetos mais importantes de Olá de comunicação. estrutura da aplicação Olá Reliable Services fornece algumas ferramentas que pode utilizar segurança tooimprove e pilhas de comunicação prebuilt. Este artigo aborda como tooimprove segurança quando estiver a utilizar o serviço Gestão remota e Olá pilha de comunicações do Windows Communication Foundation (WCF).

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Ajudar a proteger um serviço quando estiver a utilizar a comunicação remota do serviço
Estamos a utilizar um existente [exemplo](service-fabric-reliable-services-communication-remoting.md) que explica como tooset segurança remotamente serviços fiáveis. toohelp proteger um serviço quando estiver a utilizar a comunicação remota do serviço, siga estes passos:

1. Criar uma interface, `IHelloWorldStateful`, que define os métodos de Olá que estarão disponíveis para uma chamada de procedimento remoto do seu serviço. O serviço irá utilizar `FabricTransportServiceRemotingListener`, que está declarada na Olá `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` espaço de nomes. Este é um `ICommunicationListener` implementação que oferece funções de sistema de interação remota.

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. Adicione as definições de escuta e credenciais de segurança.

    Certifique-se esse certificado Olá que pretende que o toohelp de toouse proteger que a comunicação de serviço está instalada em todos os nós de Olá num cluster de Olá. Existem duas formas que pode fornecer as definições de escuta e credenciais de segurança:

   1. Fornecê-los diretamente no código do serviço Olá:

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. Fornecê-los utilizando um [o pacote de configuração](service-fabric-application-model.md):

       Adicionar um `TransportSettings` secção no ficheiro de settings.xml Olá.

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       Neste caso, Olá `CreateServiceReplicaListeners` método terá este aspeto:

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        Se adicionar um `TransportSettings` secção no ficheiro de settings.xml Olá, `FabricTransportRemotingListenerSettings ` carregará todas as definições de Olá desta secção por predefinição.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        Neste caso, Olá `CreateServiceReplicaListeners` método terá este aspeto:

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. Quando chamar métodos num serviço protegido através da utilização de pilha do sistema de interação remota Olá, em vez de utilizar Olá `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe toocreate um proxy de serviço, utilize `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Transmita `FabricTransportRemotingSettings`, que contém `SecurityCredentials`.

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Se o código de cliente Olá está em execução como parte de um serviço, pode carregar `FabricTransportRemotingSettings` do ficheiro de settings.xml Olá. Crie uma secção de HelloWorldClientTransportSettings é toohello serviço um código semelhante, conforme mostrado anteriormente. Certifique-Olá seguinte código de cliente de toohello alterações:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Se o cliente de Olá não está em execução como parte de um serviço, pode criar um ficheiro de client_name.settings.xml no Olá mesma localização onde é Olá client_name.exe. Em seguida, crie uma secção TransportSettings nesse ficheiro.

    Serviço de toohello semelhante, se adicionar um `TransportSettings` secção cliente settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` carrega todas as definições de Olá desta secção por predefinição.

    Nesse caso, hello código anterior é ainda mais simplificado:  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>Ajudar a proteger um serviço quando estiver a utilizar uma pilha de comunicação baseada em WCF
Estamos a utilizar um existente [exemplo](service-fabric-reliable-services-communication-wcf.md) que explica como tooset segurança uma comunicação baseada em WCF pilha para serviços fiáveis. toohelp proteger um serviço quando estiver a utilizar uma pilha de comunicação baseada em WCF, siga estes passos:

1. Para o serviço de Olá, terá do serviço de escuta do toohelp Olá segura WCF comunicação (`WcfCommunicationListener`) que criar. toodo, modificar Olá `CreateServiceReplicaListeners` método.

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in hello ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. No cliente Olá, Olá `WcfCommunicationClient` classe que foi criado no Olá anterior [exemplo](service-fabric-reliable-services-communication-wcf.md) permanece inalterado. Precisa de toooverride Olá `CreateClientAsync` método `WcfCommunicationClientFactory`:

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    Utilize `SecureWcfCommunicationClientFactory` toocreate um cliente de comunicação de WCF (`WcfCommunicationClient`). Utilize os métodos do serviço Olá cliente tooinvoke.

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a>Passos seguintes
* [Web API com OWIN nos serviços de fiáveis](service-fabric-reliable-services-communication-webapi.md)
