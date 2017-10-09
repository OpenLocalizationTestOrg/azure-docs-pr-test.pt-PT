---
title: "aaaAzure aplicação do reencaminhamento de WCF híbrida no local/nuvem (.NET) | Microsoft Docs"
description: "Saiba como aplicação híbrida de toocreate um .NET no local/nuvem utilizando o reencaminhamento de WCF do Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Aplicação .NET híbrida no local/cloud com o Reencaminhamento de WCF do Azure
## <a name="introduction"></a>Introdução

Este artigo mostra como toobuild uma versão híbrida na nuvem a aplicação com o Microsoft Azure e o Visual Studio. Olá tutorial parte do princípio de que tem qualquer experiência na utilização do Azure. Em menos de 30 minutos, terá uma aplicação que utiliza vários recursos do Azure e em execução na nuvem de Olá.

Aprenderá:

* Como toocreate ou adaptar um serviço web existente para consumo por uma solução web.
* Como toouse Olá dados tooshare do serviço de reencaminhamento de WCF Azure entre uma aplicação do Azure e um serviço web alojado noutro local.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Como o Reencaminhamento do Azure ajuda com soluções híbridas

Soluções de negócio são normalmente compostas por uma combinação de código personalizado escrito tootackle novo e requisitos comerciais e funcionalidades existentes fornecidas por soluções e sistemas que já estão em vigor.

Arquitetos de soluções estão a começar nuvem de Olá toouse para processamento mais fácil de requisitos de escala e custos operacionais inferiores. Ao fazê-lo, podem encontrar a que os elementos de serviço existente gostaria tooleverage como blocos modulares para as suas soluções no interior da firewall da empresa Olá e fora de fácil alcancem para acesso pela solução de nuvem Olá. Muitos serviços internos não são criados ou alojados de modo a que possam ser facilmente expostos na margem da rede empresarial de Olá.

[Reencaminhamento do Azure](https://azure.microsoft.com/services/service-bus/) foi concebido para Olá caso de utilização de serviços web do Windows Communication Foundation (WCF) existente e tornar os serviços acessíveis de forma segura toosolutions que residem fora do perímetro empresarial Olá sem necessidade de infraestrutura da rede empresarial toohello fazer alterações intrusivas na. Os serviços de reencaminhamento continuam a ser alojados no seu ambiente existente, mas, delegam a escuta de entrada serviço de reencaminhamento alojado na nuvem de toohello de sessões e pedidos. O Reencaminhamento do Azure também protege esses serviços de acesso não autorizado utilizando a autenticação por [Assinatura de Acesso Partilhado (SAS)](../service-bus-messaging/service-bus-sas.md).

## <a name="solution-scenario"></a>Cenário de solução
Neste tutorial, irá criar um Web site ASP.NET que permite toosee uma lista de produtos na página de inventário de produtos Olá.

![][0]

Olá tutorial parte do princípio de que tem informações do produto num sistema no local existente e utiliza o reencaminhamento do Azure tooreach para esse sistema. Tal é simulado por um serviço Web executado numa aplicação de consola simples e está associado a um conjunto de produtos dentro da memória. Irá ser capaz de toorun esta aplicação de consola no seu computador e implementa a função da web Olá no Azure. Ao fazê-lo, verá como função da web Olá em execução no Olá datacenter do Azure chamará o computador, apesar do computador certamente protegido por, pelo menos, uma firewall e uma camada de tradução (NAT) de endereço de rede.

## <a name="set-up-hello-development-environment"></a>Configurar o ambiente de desenvolvimento de Olá

Antes de poder começar a desenvolver aplicações do Azure, descarregar as ferramentas de Olá e configurar o ambiente de desenvolvimento:

1. Instale o Olá Azure SDK para .NET a partir de Olá SDK [página de transferências](https://azure.microsoft.com/downloads/).
2. No Olá **.NET** coluna, clique em versão Olá do [Visual Studio](http://www.visualstudio.com) estiver a utilizar. Olá, os passos nesta utilização tutorial Visual Studio 2015, mas também funcionar com o Visual Studio 2017.
3. Quando lhe for pedido toorun ou guardar o instalador Olá, clique em **executar**.
4. No Olá **instalador de plataforma Web**, clique em **instalar** e continue com a instalação de Olá.
5. Após a conclusão da instalação de Olá, terá tudo toostart necessário toodevelop Olá aplicação. Olá SDK inclui ferramentas que permitem desenvolver facilmente aplicações do Azure no Visual Studio.

## <a name="create-a-namespace"></a>Criar um espaço de nomes

utilizar toobegin Olá funcionalidades de reencaminhamento no Azure, primeiro tem de criar um espaço de nomes de serviço. Um espaço de nomes fornece um contentor de âmbito para abordar os recursos do Azure na sua aplicação. Siga Olá [instruções aqui](relay-create-namespace-portal.md) toocreate um espaço de nomes de reencaminhamento.

## <a name="create-an-on-premises-server"></a>Criar um servidor no local

Em primeiro lugar, compilará um sistema de catálogo de produtos no local (mock). Será bastante simple; Pode ver este como representando um sistema de catálogo de produtos no local real com uma superfície de serviço completo que estamos a tentar toointegrate.

Este projeto é uma aplicação de consola do Visual Studio e utiliza Olá [pacote NuGet do Service Bus do Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude Olá bibliotecas do Service Bus e definições de configuração.

### <a name="create-hello-project"></a>Criar projeto Olá

1. Inicie o Microsoft Visual Studio com privilégios de administrador. toodo por isso, clique no ícone de programa do Visual Studio Olá e, em seguida, clique em **executar como administrador**.
2. No Visual Studio, no Olá **ficheiro** menu, clique em **novo**e, em seguida, clique em **projeto**.
3. A partir de **Modelos Instalados**, no **Visual C#**, clique em **Aplicação de Consola (.NET Framework)**. No Olá **nome** caixa, o nome do tipo Olá **ProductsServer**:

   ![][11]
4. Clique em **OK** toocreate Olá **ProductsServer** projeto.
5. Se já tiver instalado o Gestor de pacotes de NuGet Olá para Visual Studio, ignore o passo seguinte toohello. Caso contrário, aceda a [NuGet][NuGet] e clique em [Instalar NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c). Siga o Gestor de pacotes de NuGet tooinstall Olá Olá pede e, em seguida, inicie novamente o Visual Studio.
6. No Explorador de soluções, faça duplo clique Olá **ProductsServer** do projeto, em seguida, clique em **gerir pacotes NuGet**.
7. Clique em Olá **procurar** separador, em seguida, procure `Microsoft Azure Service Bus`. Selecione Olá **Windowsazure** pacote.
8. Clique em **instalar**e aceite os termos de Olá de utilização.

   ![][13]

   Tenha em atenção que Olá necessários conjuntos de cliente estão agora referenciados.
8. Adicione uma nova classe para o contrato de produto.  No Explorador de soluções, faça duplo clique Olá **ProductsServer** projeto e clique em **adicionar**e, em seguida, clique em **classe**.
9. No Olá **nome** caixa, o nome do tipo Olá **Productscontract**. Em seguida, clique em **Adicionar**.
10. No **Productscontract**, substitua a definição de espaço de nomes de Olá Olá seguinte código, que define o contrato de Olá para o serviço de Olá.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. Em Program.cs, substitua a definição de espaço de nomes de Olá com Olá código, que adiciona o serviço de perfil de Olá e anfitrião Olá a seguir.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. No Explorador de soluções, faça duplo clique Olá **App. config** ficheiro tooopen-lo no editor do Visual Studio Olá. Na parte inferior de Olá de Olá `<system.ServiceModel>` elemento (mas ainda dentro `<system.ServiceModel>`), adicione o seguinte código XML de Olá. Ser tooreplace se *yourServiceNamespace* com o nome de Olá do espaço de nomes e *yourKey* com a chave SAS Olá que obteve anteriormente do portal de Olá:

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. Ainda em App. config, no Olá `<appSettings>` elemento, valor da cadeia de ligação de Olá de substituir com a cadeia de ligação de Olá previamente obtida no portal de Olá.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Prima **Ctrl + Shift + B** ou a partir de Olá **criar** menu, clique em **compilar solução** toobuild Olá aplicação e verificar a precisão Olá do seu trabalho até ao momento.

## <a name="create-an-aspnet-application"></a>Criar uma aplicação ASP.NET

Nesta secção, compilará uma aplicação ASP.NET simples que apresenta dados obtidos a partir do serviço de produtos.

### <a name="create-hello-project"></a>Criar projeto Olá

1. Certifique-se de que o Visual Studio está em execução com privilégios de administrador.
2. No Visual Studio, no Olá **ficheiro** menu, clique em **novo**e, em seguida, clique em **projeto**.
3. A partir de **Modelos Instalados**, no **Visual C#**, clique em **Aplicação Web ASP.NET (.NET Framework)**. Projeto de Olá nome **ProductsPortal**. Em seguida, clique em **OK**.

   ![][15]

4. De Olá **modelos ASP.NET** lista no Olá **nova aplicação Web do ASP.NET** caixa de diálogo, clique em **MVC**.

   ![][16]

6. Clique em Olá **alterar autenticação** botão. No Olá **alterar autenticação** diálogo caixa, certifique-se de que **sem autenticação** está selecionada e, em seguida, clique em **OK**. Para este tutorial, está a implementar uma aplicação que não precisa de um início de sessão do utilizador.

    ![][18]

7. Novamente no Olá **nova aplicação Web do ASP.NET** caixa de diálogo, clique em **OK** toocreate Olá MVC aplicação.
8. Deve agora configurar recursos do Azure para uma nova aplicação Web. Siga os passos de Olá Olá [publicar tooAzure secção deste artigo](../app-service-web/app-service-web-get-started-dotnet.md). Em seguida, regresse toothis tutorial e continue toohello próximo passo.
10. No Explorador de Soluções, clique com o botão direito do rato em **Modelos** e, em seguida, em **Adicionar** e em **Classe**. No Olá **nome** caixa, o nome do tipo Olá **Product.cs**. Em seguida, clique em **Adicionar**.

    ![][17]

### <a name="modify-hello-web-application"></a>Modificar a aplicação web de Olá

1. No ficheiro de Olá Product.cs no Visual Studio, substitua a definição de espaço de nomes existente de Olá pelo Olá seguinte código.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. No Explorador de soluções, expanda Olá **controladores** pasta, em seguida, faça duplo clique em Olá **Homecontroller** ficheiro tooopen-lo no Visual Studio.
3. No **Homecontroller**, substitua a definição de espaço de nomes existente Olá Olá seguinte código.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. No Explorador de soluções, expanda a pasta do Olá views\shared e, em seguida, faça duplo clique em **layout** tooopen-lo no editor do Visual Studio Olá.
5. Alterar todas as ocorrências de **minha aplicação ASP.NET** demasiado**produtos da LITWARE**.
6. Remover Olá **home page**, **sobre**, e **contacte** ligações. No seguinte exemplo de Olá, elimine o código de Olá realçado.

    ![][41]

7. No Explorador de soluções, expanda a pasta do Olá views\home e, em seguida, faça duplo clique em **Index. cshtml** tooopen-lo no editor do Visual Studio Olá. Substitua conteúdos integrais do Olá do ficheiro de Olá Olá seguinte código.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. precisão de Olá tooverify do seu trabalho até ao momento, pode premir **Ctrl + Shift + B** projeto de Olá toobuild.

### <a name="run-hello-app-locally"></a>Executar localmente a aplicação Olá

Execute Olá aplicação tooverify que funciona.

1. Certifique-se de que **ProductsPortal** for Olá projeto de Active Directory. Clique no nome do projeto Olá no Explorador de soluções e selecione **configurar como projeto de arranque**.
2. No Visual Studio, prima **F5**.
3. A aplicação deverá aparecer em execução num browser.

   ![][21]

## <a name="put-hello-pieces-together"></a>Juntar as peças de Olá

Olá passo seguinte consiste em toohook se o servidor de produtos no local Olá Olá aplicação ASP.NET.

1. Se ainda não estiver aberto, no Visual Studio volte a abrir Olá **ProductsPortal** projeto que criou no Olá [criar uma aplicação ASP.NET](#create-an-aspnet-application) secção.
2. Semelhante toohello passo na secção de "Criar um servidor do On-Premises" Olá, adicione Olá NuGet pacote toohello referências do projeto. No Explorador de soluções, faça duplo clique Olá **ProductsPortal** do projeto, em seguida, clique em **gerir pacotes NuGet**.
3. Procurar "Service Bus" e selecione Olá **Windowsazure** item. Em seguida, conclua a instalação Olá e fechar esta caixa de diálogo.
4. No Explorador de soluções, faça duplo clique Olá **ProductsPortal** do projeto, em seguida, clique em **adicionar**, em seguida, **Item existente**.
5. Navegue toohello **Productscontract** ficheiro a partir do Olá **ProductsServer** projeto de consola. Clique em toohighlight Productscontract. Clique Olá seta para baixo junto demasiado**adicionar**, em seguida, clique em **adicionar como hiperligação**.

   ![][24]

6. Agora abra Olá **Homecontroller** ficheiro no editor do Visual Studio Olá e substitua a definição de espaço de nomes de Olá Olá seguinte código. Ser tooreplace se *yourServiceNamespace* com o nome de Olá do seu espaço de nomes do serviço e *yourKey* pela chave SAS. Este procedimento activará Olá cliente toocall Olá serviço no local, devolvendo o resultado de Olá da chamada de Olá.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. No Explorador de soluções, faça duplo clique Olá **ProductsPortal** solução (disponibilizar clique tooright se Olá solução, não projeto de Olá). Clique em **Adicionar** e em **Projeto Existente**.
8. Navegue toohello **ProductsServer** do projeto, em seguida, faça duplo clique em Olá **ProductsServer.csproj** tooadd do ficheiro de solução-lo.
9. **ProductsServer** deve executar nos dados de Olá ordem toodisplay **ProductsPortal**. No Explorador de soluções, faça duplo clique Olá **ProductsPortal** solução e clique em **propriedades**. Olá **páginas de propriedades** é apresentada a caixa de diálogo.
10. Olá deixado lado, clique em **projeto de arranque**. No lado direito de Olá, clique em **vários projetos de arranque**. Certifique-se de que **ProductsServer** e **ProductsPortal** são apresentados, nessa ordem, com **iniciar** definido como ação Olá para ambos.

      ![][25]

11. Ainda no Olá **propriedades** caixa de diálogo, clique em **dependências do projeto** no Olá à esquerda do lado do.
12. No Olá **projetos** lista, clique em **ProductsServer**. Certifique-se de que o **ProductsPortal** não está selecionado.
13. No Olá **projetos** lista, clique em **ProductsPortal**. Certifique-se de que o **ProductsServer** está selecionado.

    ![][26]

14. Clique em **OK** no Olá **páginas de propriedades** caixa de diálogo.

## <a name="run-hello-project-locally"></a>Executar o projeto de Olá localmente

aplicação de Olá tootest localmente, no Visual Studio prima **F5**. servidor no local de Olá (**ProductsServer**) deverá iniciar primeiro e Olá **ProductsPortal** aplicação deverá iniciar numa janela do browser. Neste momento, verá que o inventário de produtos Olá lista os dados obtidos a partir do Olá produto serviço no sistema local.

![][10]

Prima **atualizar** no Olá **ProductsPortal** página. Sempre que atualizar a página Olá, verá a aplicação de servidor de Olá apresenta uma mensagem quando `GetProducts()` de **ProductsServer** é chamado.

Feche a ambas as aplicações antes de passo seguinte do toohello continuar.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Implementar a aplicação de web do Azure de tooan de projeto ProductsPortal Olá

Olá passo seguinte consiste em toorepublish Olá Azure Web app **ProductsPortal** front-end. Olá seguintes:

1. No Explorador de soluções, faça duplo clique Olá **ProductsPortal** projeto e clique em **publicar**. Em seguida, clique em **publicar** no Olá **publicar** página.

  > [!NOTE]
  > Poderá ver uma mensagem de erro na janela do browser Olá quando hello **ProductsPortal** projeto web é iniciado automaticamente após a implementação de Olá. Isto é esperado e ocorre dado Olá **ProductsServer** aplicação não está em execução ainda.
>
>

2. Cópia Olá URL de Olá implementar a aplicação web, pois irá precisar do URL de Olá no passo seguinte Olá. Também pode obter esse URL a partir da janela de atividade do App Service do Azure Olá no Visual Studio:

  ![][9]

3. Feche Olá toostop Olá browser janela execução da aplicação.

### <a name="set-productsportal-as-web-app"></a>Configurar o ProductsPortal como uma aplicação Web

Antes de aplicação Olá em execução na nuvem de Olá, tem de garantir que **ProductsPortal** é iniciado a partir do Visual Studio como uma aplicação web.

1. No Visual Studio, clique com botão direito Olá **ProductsPortal** projeto e, em seguida, clique em **propriedades**.
2. Na coluna esquerda do Olá, clique em **Web**.
3. No Olá **iniciar ação** secção, clique em Olá **URL de início** botão e, na caixa de texto Olá introduza Olá URL para a sua aplicação web anteriormente implementada; por exemplo, `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. De Olá **ficheiro** menu no Visual Studio, clique em **Guardar tudo**.
5. No menu de compilação de Olá no Visual Studio, clique em **reconstruir solução**.

## <a name="run-hello-application"></a>Executar a aplicação Olá

1. Prima F5 toobuild e executar a aplicação Olá. servidor no local de Olá (Olá **ProductsServer** aplicação de consola) deverá iniciar primeiro e Olá **ProductsPortal** aplicação deverá iniciar numa janela do browser, conforme mostrado no seguinte ecrã de Olá captura. Tenha em atenção novamente que o inventário de produtos Olá lista os dados obtidos a partir do Olá produto serviço no sistema local e apresenta esses dados na aplicação web de Olá. Verifique Olá URL toomake se de que **ProductsPortal** está em execução na nuvem de Olá, como uma aplicação web do Azure.

   ![][1]

   > [!IMPORTANT]
   > Olá **ProductsServer** aplicação de consola tem de estar em execução e consegue tooserve Olá dados toohello **ProductsPortal** aplicação. Se o browser de Olá apresenta um erro, aguarde mais alguns segundos para **ProductsServer** tooload e Olá de apresentação seguintes da mensagem. Em seguida, prima **atualizar** no browser Olá.
   >
   >

   ![][37]
2. No browser Olá, prima **atualizar** no Olá **ProductsPortal** página. Sempre que atualizar a página Olá, verá a aplicação de servidor de Olá apresenta uma mensagem quando `GetProducts()` de **ProductsServer** é chamado.

    ![][38]

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre o reencaminhamento do Azure, consulte Olá os seguintes recursos:  

* [O que é o Reencaminhamento do Azure?](relay-what-is-it.md)  
* [Como toouse de reencaminhamento](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
