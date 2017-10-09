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
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="08924-103">Aplicação .NET híbrida no local/cloud com o Reencaminhamento de WCF do Azure</span><span class="sxs-lookup"><span data-stu-id="08924-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="08924-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="08924-104">Introduction</span></span>

<span data-ttu-id="08924-105">Este artigo mostra como toobuild uma versão híbrida na nuvem a aplicação com o Microsoft Azure e o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08924-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="08924-106">Olá tutorial parte do princípio de que tem qualquer experiência na utilização do Azure.</span><span class="sxs-lookup"><span data-stu-id="08924-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="08924-107">Em menos de 30 minutos, terá uma aplicação que utiliza vários recursos do Azure e em execução na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="08924-108">Aprenderá:</span><span class="sxs-lookup"><span data-stu-id="08924-108">You will learn:</span></span>

* <span data-ttu-id="08924-109">Como toocreate ou adaptar um serviço web existente para consumo por uma solução web.</span><span class="sxs-lookup"><span data-stu-id="08924-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="08924-110">Como toouse Olá dados tooshare do serviço de reencaminhamento de WCF Azure entre uma aplicação do Azure e um serviço web alojado noutro local.</span><span class="sxs-lookup"><span data-stu-id="08924-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="08924-111">Como o Reencaminhamento do Azure ajuda com soluções híbridas</span><span class="sxs-lookup"><span data-stu-id="08924-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="08924-112">Soluções de negócio são normalmente compostas por uma combinação de código personalizado escrito tootackle novo e requisitos comerciais e funcionalidades existentes fornecidas por soluções e sistemas que já estão em vigor.</span><span class="sxs-lookup"><span data-stu-id="08924-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="08924-113">Arquitetos de soluções estão a começar nuvem de Olá toouse para processamento mais fácil de requisitos de escala e custos operacionais inferiores.</span><span class="sxs-lookup"><span data-stu-id="08924-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="08924-114">Ao fazê-lo, podem encontrar a que os elementos de serviço existente gostaria tooleverage como blocos modulares para as suas soluções no interior da firewall da empresa Olá e fora de fácil alcancem para acesso pela solução de nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="08924-115">Muitos serviços internos não são criados ou alojados de modo a que possam ser facilmente expostos na margem da rede empresarial de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="08924-116">[Reencaminhamento do Azure](https://azure.microsoft.com/services/service-bus/) foi concebido para Olá caso de utilização de serviços web do Windows Communication Foundation (WCF) existente e tornar os serviços acessíveis de forma segura toosolutions que residem fora do perímetro empresarial Olá sem necessidade de infraestrutura da rede empresarial toohello fazer alterações intrusivas na.</span><span class="sxs-lookup"><span data-stu-id="08924-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="08924-117">Os serviços de reencaminhamento continuam a ser alojados no seu ambiente existente, mas, delegam a escuta de entrada serviço de reencaminhamento alojado na nuvem de toohello de sessões e pedidos.</span><span class="sxs-lookup"><span data-stu-id="08924-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="08924-118">O Reencaminhamento do Azure também protege esses serviços de acesso não autorizado utilizando a autenticação por [Assinatura de Acesso Partilhado (SAS)](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="08924-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="08924-119">Cenário de solução</span><span class="sxs-lookup"><span data-stu-id="08924-119">Solution scenario</span></span>
<span data-ttu-id="08924-120">Neste tutorial, irá criar um Web site ASP.NET que permite toosee uma lista de produtos na página de inventário de produtos Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="08924-121">Olá tutorial parte do princípio de que tem informações do produto num sistema no local existente e utiliza o reencaminhamento do Azure tooreach para esse sistema.</span><span class="sxs-lookup"><span data-stu-id="08924-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="08924-122">Tal é simulado por um serviço Web executado numa aplicação de consola simples e está associado a um conjunto de produtos dentro da memória.</span><span class="sxs-lookup"><span data-stu-id="08924-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="08924-123">Irá ser capaz de toorun esta aplicação de consola no seu computador e implementa a função da web Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="08924-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="08924-124">Ao fazê-lo, verá como função da web Olá em execução no Olá datacenter do Azure chamará o computador, apesar do computador certamente protegido por, pelo menos, uma firewall e uma camada de tradução (NAT) de endereço de rede.</span><span class="sxs-lookup"><span data-stu-id="08924-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="08924-125">Configurar o ambiente de desenvolvimento de Olá</span><span class="sxs-lookup"><span data-stu-id="08924-125">Set up hello development environment</span></span>

<span data-ttu-id="08924-126">Antes de poder começar a desenvolver aplicações do Azure, descarregar as ferramentas de Olá e configurar o ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="08924-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="08924-127">Instale o Olá Azure SDK para .NET a partir de Olá SDK [página de transferências](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="08924-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="08924-128">No Olá **.NET** coluna, clique em versão Olá do [Visual Studio](http://www.visualstudio.com) estiver a utilizar.</span><span class="sxs-lookup"><span data-stu-id="08924-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="08924-129">Olá, os passos nesta utilização tutorial Visual Studio 2015, mas também funcionar com o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="08924-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="08924-130">Quando lhe for pedido toorun ou guardar o instalador Olá, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="08924-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="08924-131">No Olá **instalador de plataforma Web**, clique em **instalar** e continue com a instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="08924-132">Após a conclusão da instalação de Olá, terá tudo toostart necessário toodevelop Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="08924-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="08924-133">Olá SDK inclui ferramentas que permitem desenvolver facilmente aplicações do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08924-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="08924-134">Criar um espaço de nomes</span><span class="sxs-lookup"><span data-stu-id="08924-134">Create a namespace</span></span>

<span data-ttu-id="08924-135">utilizar toobegin Olá funcionalidades de reencaminhamento no Azure, primeiro tem de criar um espaço de nomes de serviço.</span><span class="sxs-lookup"><span data-stu-id="08924-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="08924-136">Um espaço de nomes fornece um contentor de âmbito para abordar os recursos do Azure na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="08924-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="08924-137">Siga Olá [instruções aqui](relay-create-namespace-portal.md) toocreate um espaço de nomes de reencaminhamento.</span><span class="sxs-lookup"><span data-stu-id="08924-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="08924-138">Criar um servidor no local</span><span class="sxs-lookup"><span data-stu-id="08924-138">Create an on-premises server</span></span>

<span data-ttu-id="08924-139">Em primeiro lugar, compilará um sistema de catálogo de produtos no local (mock).</span><span class="sxs-lookup"><span data-stu-id="08924-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="08924-140">Será bastante simple; Pode ver este como representando um sistema de catálogo de produtos no local real com uma superfície de serviço completo que estamos a tentar toointegrate.</span><span class="sxs-lookup"><span data-stu-id="08924-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="08924-141">Este projeto é uma aplicação de consola do Visual Studio e utiliza Olá [pacote NuGet do Service Bus do Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude Olá bibliotecas do Service Bus e definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="08924-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="08924-142">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="08924-142">Create hello project</span></span>

1. <span data-ttu-id="08924-143">Inicie o Microsoft Visual Studio com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="08924-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="08924-144">toodo por isso, clique no ícone de programa do Visual Studio Olá e, em seguida, clique em **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="08924-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="08924-145">No Visual Studio, no Olá **ficheiro** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="08924-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="08924-146">A partir de **Modelos Instalados**, no **Visual C#**, clique em **Aplicação de Consola (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="08924-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="08924-147">No Olá **nome** caixa, o nome do tipo Olá **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="08924-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="08924-148">Clique em **OK** toocreate Olá **ProductsServer** projeto.</span><span class="sxs-lookup"><span data-stu-id="08924-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="08924-149">Se já tiver instalado o Gestor de pacotes de NuGet Olá para Visual Studio, ignore o passo seguinte toohello.</span><span class="sxs-lookup"><span data-stu-id="08924-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="08924-150">Caso contrário, aceda a [NuGet][NuGet] e clique em [Instalar NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span><span class="sxs-lookup"><span data-stu-id="08924-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="08924-151">Siga o Gestor de pacotes de NuGet tooinstall Olá Olá pede e, em seguida, inicie novamente o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08924-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="08924-152">No Explorador de soluções, faça duplo clique Olá **ProductsServer** do projeto, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="08924-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="08924-153">Clique em Olá **procurar** separador, em seguida, procure `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="08924-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="08924-154">Selecione Olá **Windowsazure** pacote.</span><span class="sxs-lookup"><span data-stu-id="08924-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="08924-155">Clique em **instalar**e aceite os termos de Olá de utilização.</span><span class="sxs-lookup"><span data-stu-id="08924-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="08924-156">Tenha em atenção que Olá necessários conjuntos de cliente estão agora referenciados.</span><span class="sxs-lookup"><span data-stu-id="08924-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="08924-157">Adicione uma nova classe para o contrato de produto. </span><span class="sxs-lookup"><span data-stu-id="08924-157">Add a new class for your product contract.</span></span> <span data-ttu-id="08924-158">No Explorador de soluções, faça duplo clique Olá **ProductsServer** projeto e clique em **adicionar**e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="08924-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="08924-159">No Olá **nome** caixa, o nome do tipo Olá **Productscontract**.</span><span class="sxs-lookup"><span data-stu-id="08924-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="08924-160">Em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="08924-160">Then click **Add**.</span></span>
10. <span data-ttu-id="08924-161">No **Productscontract**, substitua a definição de espaço de nomes de Olá Olá seguinte código, que define o contrato de Olá para o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

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
11. <span data-ttu-id="08924-162">Em Program.cs, substitua a definição de espaço de nomes de Olá com Olá código, que adiciona o serviço de perfil de Olá e anfitrião Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="08924-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

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
12. <span data-ttu-id="08924-163">No Explorador de soluções, faça duplo clique Olá **App. config** ficheiro tooopen-lo no editor do Visual Studio Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="08924-164">Na parte inferior de Olá de Olá `<system.ServiceModel>` elemento (mas ainda dentro `<system.ServiceModel>`), adicione o seguinte código XML de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="08924-165">Ser tooreplace se *yourServiceNamespace* com o nome de Olá do espaço de nomes e *yourKey* com a chave SAS Olá que obteve anteriormente do portal de Olá:</span><span class="sxs-lookup"><span data-stu-id="08924-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

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
13. <span data-ttu-id="08924-166">Ainda em App. config, no Olá `<appSettings>` elemento, valor da cadeia de ligação de Olá de substituir com a cadeia de ligação de Olá previamente obtida no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="08924-167">Prima **Ctrl + Shift + B** ou a partir de Olá **criar** menu, clique em **compilar solução** toobuild Olá aplicação e verificar a precisão Olá do seu trabalho até ao momento.</span><span class="sxs-lookup"><span data-stu-id="08924-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="08924-168">Criar uma aplicação ASP.NET</span><span class="sxs-lookup"><span data-stu-id="08924-168">Create an ASP.NET application</span></span>

<span data-ttu-id="08924-169">Nesta secção, compilará uma aplicação ASP.NET simples que apresenta dados obtidos a partir do serviço de produtos.</span><span class="sxs-lookup"><span data-stu-id="08924-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="08924-170">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="08924-170">Create hello project</span></span>

1. <span data-ttu-id="08924-171">Certifique-se de que o Visual Studio está em execução com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="08924-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="08924-172">No Visual Studio, no Olá **ficheiro** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="08924-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="08924-173">A partir de **Modelos Instalados**, no **Visual C#**, clique em **Aplicação Web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="08924-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="08924-174">Projeto de Olá nome **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="08924-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="08924-175">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="08924-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="08924-176">De Olá **modelos ASP.NET** lista no Olá **nova aplicação Web do ASP.NET** caixa de diálogo, clique em **MVC**.</span><span class="sxs-lookup"><span data-stu-id="08924-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="08924-177">Clique em Olá **alterar autenticação** botão.</span><span class="sxs-lookup"><span data-stu-id="08924-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="08924-178">No Olá **alterar autenticação** diálogo caixa, certifique-se de que **sem autenticação** está selecionada e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="08924-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="08924-179">Para este tutorial, está a implementar uma aplicação que não precisa de um início de sessão do utilizador.</span><span class="sxs-lookup"><span data-stu-id="08924-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="08924-180">Novamente no Olá **nova aplicação Web do ASP.NET** caixa de diálogo, clique em **OK** toocreate Olá MVC aplicação.</span><span class="sxs-lookup"><span data-stu-id="08924-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="08924-181">Deve agora configurar recursos do Azure para uma nova aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="08924-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="08924-182">Siga os passos de Olá Olá [publicar tooAzure secção deste artigo](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="08924-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="08924-183">Em seguida, regresse toothis tutorial e continue toohello próximo passo.</span><span class="sxs-lookup"><span data-stu-id="08924-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="08924-184">No Explorador de Soluções, clique com o botão direito do rato em **Modelos** e, em seguida, em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="08924-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="08924-185">No Olá **nome** caixa, o nome do tipo Olá **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="08924-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="08924-186">Em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="08924-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="08924-187">Modificar a aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="08924-187">Modify hello web application</span></span>

1. <span data-ttu-id="08924-188">No ficheiro de Olá Product.cs no Visual Studio, substitua a definição de espaço de nomes existente de Olá pelo Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="08924-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

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
2. <span data-ttu-id="08924-189">No Explorador de soluções, expanda Olá **controladores** pasta, em seguida, faça duplo clique em Olá **Homecontroller** ficheiro tooopen-lo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08924-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="08924-190">No **Homecontroller**, substitua a definição de espaço de nomes existente Olá Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="08924-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

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
4. <span data-ttu-id="08924-191">No Explorador de soluções, expanda a pasta do Olá views\shared e, em seguida, faça duplo clique em **layout** tooopen-lo no editor do Visual Studio Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="08924-192">Alterar todas as ocorrências de **minha aplicação ASP.NET** demasiado**produtos da LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="08924-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="08924-193">Remover Olá **home page**, **sobre**, e **contacte** ligações.</span><span class="sxs-lookup"><span data-stu-id="08924-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="08924-194">No seguinte exemplo de Olá, elimine o código de Olá realçado.</span><span class="sxs-lookup"><span data-stu-id="08924-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="08924-195">No Explorador de soluções, expanda a pasta do Olá views\home e, em seguida, faça duplo clique em **Index. cshtml** tooopen-lo no editor do Visual Studio Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="08924-196">Substitua conteúdos integrais do Olá do ficheiro de Olá Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="08924-196">Replace hello entire contents of hello file with hello following code.</span></span>

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
8. <span data-ttu-id="08924-197">precisão de Olá tooverify do seu trabalho até ao momento, pode premir **Ctrl + Shift + B** projeto de Olá toobuild.</span><span class="sxs-lookup"><span data-stu-id="08924-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="08924-198">Executar localmente a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="08924-198">Run hello app locally</span></span>

<span data-ttu-id="08924-199">Execute Olá aplicação tooverify que funciona.</span><span class="sxs-lookup"><span data-stu-id="08924-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="08924-200">Certifique-se de que **ProductsPortal** for Olá projeto de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="08924-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="08924-201">Clique no nome do projeto Olá no Explorador de soluções e selecione **configurar como projeto de arranque**.</span><span class="sxs-lookup"><span data-stu-id="08924-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="08924-202">No Visual Studio, prima **F5**.</span><span class="sxs-lookup"><span data-stu-id="08924-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="08924-203">A aplicação deverá aparecer em execução num browser.</span><span class="sxs-lookup"><span data-stu-id="08924-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="08924-204">Juntar as peças de Olá</span><span class="sxs-lookup"><span data-stu-id="08924-204">Put hello pieces together</span></span>

<span data-ttu-id="08924-205">Olá passo seguinte consiste em toohook se o servidor de produtos no local Olá Olá aplicação ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="08924-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="08924-206">Se ainda não estiver aberto, no Visual Studio volte a abrir Olá **ProductsPortal** projeto que criou no Olá [criar uma aplicação ASP.NET](#create-an-aspnet-application) secção.</span><span class="sxs-lookup"><span data-stu-id="08924-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="08924-207">Semelhante toohello passo na secção de "Criar um servidor do On-Premises" Olá, adicione Olá NuGet pacote toohello referências do projeto.</span><span class="sxs-lookup"><span data-stu-id="08924-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="08924-208">No Explorador de soluções, faça duplo clique Olá **ProductsPortal** do projeto, em seguida, clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="08924-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="08924-209">Procurar "Service Bus" e selecione Olá **Windowsazure** item.</span><span class="sxs-lookup"><span data-stu-id="08924-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="08924-210">Em seguida, conclua a instalação Olá e fechar esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08924-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="08924-211">No Explorador de soluções, faça duplo clique Olá **ProductsPortal** do projeto, em seguida, clique em **adicionar**, em seguida, **Item existente**.</span><span class="sxs-lookup"><span data-stu-id="08924-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="08924-212">Navegue toohello **Productscontract** ficheiro a partir do Olá **ProductsServer** projeto de consola.</span><span class="sxs-lookup"><span data-stu-id="08924-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="08924-213">Clique em toohighlight Productscontract.</span><span class="sxs-lookup"><span data-stu-id="08924-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="08924-214">Clique Olá seta para baixo junto demasiado**adicionar**, em seguida, clique em **adicionar como hiperligação**.</span><span class="sxs-lookup"><span data-stu-id="08924-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="08924-215">Agora abra Olá **Homecontroller** ficheiro no editor do Visual Studio Olá e substitua a definição de espaço de nomes de Olá Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="08924-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="08924-216">Ser tooreplace se *yourServiceNamespace* com o nome de Olá do seu espaço de nomes do serviço e *yourKey* pela chave SAS.</span><span class="sxs-lookup"><span data-stu-id="08924-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="08924-217">Este procedimento activará Olá cliente toocall Olá serviço no local, devolvendo o resultado de Olá da chamada de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

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
7. <span data-ttu-id="08924-218">No Explorador de soluções, faça duplo clique Olá **ProductsPortal** solução (disponibilizar clique tooright se Olá solução, não projeto de Olá).</span><span class="sxs-lookup"><span data-stu-id="08924-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="08924-219">Clique em **Adicionar** e em **Projeto Existente**.</span><span class="sxs-lookup"><span data-stu-id="08924-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="08924-220">Navegue toohello **ProductsServer** do projeto, em seguida, faça duplo clique em Olá **ProductsServer.csproj** tooadd do ficheiro de solução-lo.</span><span class="sxs-lookup"><span data-stu-id="08924-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="08924-221">**ProductsServer** deve executar nos dados de Olá ordem toodisplay **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="08924-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="08924-222">No Explorador de soluções, faça duplo clique Olá **ProductsPortal** solução e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="08924-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="08924-223">Olá **páginas de propriedades** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08924-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="08924-224">Olá deixado lado, clique em **projeto de arranque**.</span><span class="sxs-lookup"><span data-stu-id="08924-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="08924-225">No lado direito de Olá, clique em **vários projetos de arranque**.</span><span class="sxs-lookup"><span data-stu-id="08924-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="08924-226">Certifique-se de que **ProductsServer** e **ProductsPortal** são apresentados, nessa ordem, com **iniciar** definido como ação Olá para ambos.</span><span class="sxs-lookup"><span data-stu-id="08924-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="08924-227">Ainda no Olá **propriedades** caixa de diálogo, clique em **dependências do projeto** no Olá à esquerda do lado do.</span><span class="sxs-lookup"><span data-stu-id="08924-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="08924-228">No Olá **projetos** lista, clique em **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="08924-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="08924-229">Certifique-se de que o **ProductsPortal** não está selecionado.</span><span class="sxs-lookup"><span data-stu-id="08924-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="08924-230">No Olá **projetos** lista, clique em **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="08924-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="08924-231">Certifique-se de que o **ProductsServer** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="08924-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="08924-232">Clique em **OK** no Olá **páginas de propriedades** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08924-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="08924-233">Executar o projeto de Olá localmente</span><span class="sxs-lookup"><span data-stu-id="08924-233">Run hello project locally</span></span>

<span data-ttu-id="08924-234">aplicação de Olá tootest localmente, no Visual Studio prima **F5**.</span><span class="sxs-lookup"><span data-stu-id="08924-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="08924-235">servidor no local de Olá (**ProductsServer**) deverá iniciar primeiro e Olá **ProductsPortal** aplicação deverá iniciar numa janela do browser.</span><span class="sxs-lookup"><span data-stu-id="08924-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="08924-236">Neste momento, verá que o inventário de produtos Olá lista os dados obtidos a partir do Olá produto serviço no sistema local.</span><span class="sxs-lookup"><span data-stu-id="08924-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="08924-237">Prima **atualizar** no Olá **ProductsPortal** página.</span><span class="sxs-lookup"><span data-stu-id="08924-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="08924-238">Sempre que atualizar a página Olá, verá a aplicação de servidor de Olá apresenta uma mensagem quando `GetProducts()` de **ProductsServer** é chamado.</span><span class="sxs-lookup"><span data-stu-id="08924-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="08924-239">Feche a ambas as aplicações antes de passo seguinte do toohello continuar.</span><span class="sxs-lookup"><span data-stu-id="08924-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="08924-240">Implementar a aplicação de web do Azure de tooan de projeto ProductsPortal Olá</span><span class="sxs-lookup"><span data-stu-id="08924-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="08924-241">Olá passo seguinte consiste em toorepublish Olá Azure Web app **ProductsPortal** front-end.</span><span class="sxs-lookup"><span data-stu-id="08924-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="08924-242">Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="08924-242">Do hello following:</span></span>

1. <span data-ttu-id="08924-243">No Explorador de soluções, faça duplo clique Olá **ProductsPortal** projeto e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="08924-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="08924-244">Em seguida, clique em **publicar** no Olá **publicar** página.</span><span class="sxs-lookup"><span data-stu-id="08924-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="08924-245">Poderá ver uma mensagem de erro na janela do browser Olá quando hello **ProductsPortal** projeto web é iniciado automaticamente após a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="08924-246">Isto é esperado e ocorre dado Olá **ProductsServer** aplicação não está em execução ainda.</span><span class="sxs-lookup"><span data-stu-id="08924-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="08924-247">Cópia Olá URL de Olá implementar a aplicação web, pois irá precisar do URL de Olá no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="08924-248">Também pode obter esse URL a partir da janela de atividade do App Service do Azure Olá no Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="08924-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="08924-249">Feche Olá toostop Olá browser janela execução da aplicação.</span><span class="sxs-lookup"><span data-stu-id="08924-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="08924-250">Configurar o ProductsPortal como uma aplicação Web</span><span class="sxs-lookup"><span data-stu-id="08924-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="08924-251">Antes de aplicação Olá em execução na nuvem de Olá, tem de garantir que **ProductsPortal** é iniciado a partir do Visual Studio como uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="08924-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="08924-252">No Visual Studio, clique com botão direito Olá **ProductsPortal** projeto e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="08924-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="08924-253">Na coluna esquerda do Olá, clique em **Web**.</span><span class="sxs-lookup"><span data-stu-id="08924-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="08924-254">No Olá **iniciar ação** secção, clique em Olá **URL de início** botão e, na caixa de texto Olá introduza Olá URL para a sua aplicação web anteriormente implementada; por exemplo, `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="08924-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="08924-255">De Olá **ficheiro** menu no Visual Studio, clique em **Guardar tudo**.</span><span class="sxs-lookup"><span data-stu-id="08924-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="08924-256">No menu de compilação de Olá no Visual Studio, clique em **reconstruir solução**.</span><span class="sxs-lookup"><span data-stu-id="08924-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="08924-257">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="08924-257">Run hello application</span></span>

1. <span data-ttu-id="08924-258">Prima F5 toobuild e executar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="08924-259">servidor no local de Olá (Olá **ProductsServer** aplicação de consola) deverá iniciar primeiro e Olá **ProductsPortal** aplicação deverá iniciar numa janela do browser, conforme mostrado no seguinte ecrã de Olá captura.</span><span class="sxs-lookup"><span data-stu-id="08924-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="08924-260">Tenha em atenção novamente que o inventário de produtos Olá lista os dados obtidos a partir do Olá produto serviço no sistema local e apresenta esses dados na aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="08924-261">Verifique Olá URL toomake se de que **ProductsPortal** está em execução na nuvem de Olá, como uma aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="08924-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="08924-262">Olá **ProductsServer** aplicação de consola tem de estar em execução e consegue tooserve Olá dados toohello **ProductsPortal** aplicação.</span><span class="sxs-lookup"><span data-stu-id="08924-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="08924-263">Se o browser de Olá apresenta um erro, aguarde mais alguns segundos para **ProductsServer** tooload e Olá de apresentação seguintes da mensagem.</span><span class="sxs-lookup"><span data-stu-id="08924-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="08924-264">Em seguida, prima **atualizar** no browser Olá.</span><span class="sxs-lookup"><span data-stu-id="08924-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="08924-265">No browser Olá, prima **atualizar** no Olá **ProductsPortal** página.</span><span class="sxs-lookup"><span data-stu-id="08924-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="08924-266">Sempre que atualizar a página Olá, verá a aplicação de servidor de Olá apresenta uma mensagem quando `GetProducts()` de **ProductsServer** é chamado.</span><span class="sxs-lookup"><span data-stu-id="08924-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="08924-267">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="08924-267">Next steps</span></span>

<span data-ttu-id="08924-268">toolearn mais informações sobre o reencaminhamento do Azure, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="08924-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="08924-269">O que é o Reencaminhamento do Azure?</span><span class="sxs-lookup"><span data-stu-id="08924-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="08924-270">Como toouse de reencaminhamento</span><span class="sxs-lookup"><span data-stu-id="08924-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
