---
title: "aaaDeploy uma aplicação .NET no tooAzure contentor Service Fabric | Microsoft Docs"
description: "Informa-o como toopackage uma aplicação .NET no Visual Studio num contentor de Docker. Esta nova aplicação de \"container\", em seguida, for implementada tooa cluster do Service Fabric."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="1d54c-104">Implementar uma aplicação .NET num tooAzure de contentor do Windows Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1d54c-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="1d54c-105">Este tutorial mostra como toodeploy uma aplicação ASP.NET existente num contentor do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="1d54c-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="1d54c-106">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="1d54c-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1d54c-107">Criar um projeto de Docker no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d54c-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="1d54c-108">Containerize uma aplicação existente</span><span class="sxs-lookup"><span data-stu-id="1d54c-108">Containerize an existing application</span></span>
> * <span data-ttu-id="1d54c-109">Configurar a integração contínua com o Visual Studio e VSTS</span><span class="sxs-lookup"><span data-stu-id="1d54c-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d54c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1d54c-110">Prerequisites</span></span>

1. <span data-ttu-id="1d54c-111">Instalar [Docker CE para Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) para que possam executar contentores no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1d54c-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="1d54c-112">Familiarize-se com Olá [início rápido do Windows 10 contentores][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="1d54c-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="1d54c-113">Transferir Olá [Fabrikam fibra CallCenter] [ link-fabrikam-github] aplicação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1d54c-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="1d54c-114">Instalar [o Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="1d54c-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="1d54c-115">Instalar Olá [extensão de ferramentas de entrega contínua para Visual Studio 2017][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="1d54c-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="1d54c-116">Criar um [subscrição do Azure] [ link-azure-subscription] e um [conta Visual Studio Team Services][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="1d54c-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="1d54c-117">Criar um cluster no Azure</span><span class="sxs-lookup"><span data-stu-id="1d54c-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="1d54c-118">Containerize aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="1d54c-118">Containerize hello application</span></span>

<span data-ttu-id="1d54c-119">Agora que tem um [cluster do Service Fabric está em execução no Azure](service-fabric-tutorial-create-cluster-azure-ps.md) são toocreate pronto e implementar uma aplicação de.</span><span class="sxs-lookup"><span data-stu-id="1d54c-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="1d54c-120">toostart com a nossa aplicação num contentor, precisamos tooadd **Docker suporte** toohello projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d54c-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="1d54c-121">Quando adiciona **suporte Docker** aplicação toohello, duas coisas acontecer.</span><span class="sxs-lookup"><span data-stu-id="1d54c-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="1d54c-122">Primeiro, um _Dockerfile_ é adicionada toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="1d54c-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="1d54c-123">Este novo ficheiro descreve como a imagem do contentor de Olá é toobe incorporada.</span><span class="sxs-lookup"><span data-stu-id="1d54c-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="1d54c-124">Em seguida, segundo, um novo _compor o docker_ projeto é adicionado toohello solução.</span><span class="sxs-lookup"><span data-stu-id="1d54c-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="1d54c-125">Olá novo projeto contém alguns ficheiros de compose docker.</span><span class="sxs-lookup"><span data-stu-id="1d54c-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="1d54c-126">Ficheiros de compose de docker podem ser utilizado toodescribe como contentor Olá é executado.</span><span class="sxs-lookup"><span data-stu-id="1d54c-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="1d54c-127">Obter mais informações sobre como trabalhar com [ferramentas de contentor do Visual Studio][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="1d54c-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="1d54c-128">Se for Olá pela primeira vez que as imagens de contentor do Windows estiver a executar no seu computador, tem obter Docker CE imagens base do Olá para os contentores.</span><span class="sxs-lookup"><span data-stu-id="1d54c-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="1d54c-129">imagens de Olá utilizadas neste tutorial são 14 GB.</span><span class="sxs-lookup"><span data-stu-id="1d54c-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="1d54c-130">Avançar e execute Olá imagens base do comando terminal toopull Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1d54c-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="1d54c-131">Adicionar suporte de Docker</span><span class="sxs-lookup"><span data-stu-id="1d54c-131">Add Docker support</span></span>

<span data-ttu-id="1d54c-132">Abra Olá [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] ficheiro no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1d54c-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="1d54c-133">Contexto Olá **FabrikamFiber.Web** projeto > **adicionar** > **Docker suporte**.</span><span class="sxs-lookup"><span data-stu-id="1d54c-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="1d54c-134">Adicionar suporte para o SQL Server</span><span class="sxs-lookup"><span data-stu-id="1d54c-134">Add support for SQL</span></span>

<span data-ttu-id="1d54c-135">Esta aplicação utiliza o SQL Server como fornecedor de dados de Olá, para que um SQL server é necessário toorun Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="1d54c-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="1d54c-136">Referência a uma imagem de contentor do SQL Server no nosso ficheiro docker compose.override.yml.</span><span class="sxs-lookup"><span data-stu-id="1d54c-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="1d54c-137">No Visual Studio, abra **Explorador de soluções**, localizar **compor o docker**e o ficheiro aberto Olá **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="1d54c-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="1d54c-138">Navegue toohello `services:` nó, adicionar um nó com o nome `db:` que define a entrada do SQL Server Olá para o contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="1d54c-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
><span data-ttu-id="1d54c-139">Pode utilizar qualquer servidor de SQL que preferir para depuração local, desde que seja acessível a partir do seu anfitrião.</span><span class="sxs-lookup"><span data-stu-id="1d54c-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="1d54c-140">No entanto, **localdb** não suporta `container -> host` comunicação.</span><span class="sxs-lookup"><span data-stu-id="1d54c-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="1d54c-141">Executar o SQL Server num contentor não suporta dados persistentes.</span><span class="sxs-lookup"><span data-stu-id="1d54c-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="1d54c-142">Paragem do contentor de Olá, é apagar os dados.</span><span class="sxs-lookup"><span data-stu-id="1d54c-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="1d54c-143">Utilize esta configuração para produção.</span><span class="sxs-lookup"><span data-stu-id="1d54c-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="1d54c-144">Navegue toohello `fabrikamfiber.web:` nós e adicionar um nó subordinado com o nome `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="1d54c-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="1d54c-145">Isto garante que Olá `db` início do serviço (contentor de SQL Server Olá) antes da nossa aplicação web (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="1d54c-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="1d54c-146">Atualizar a configuração de web de Olá</span><span class="sxs-lookup"><span data-stu-id="1d54c-146">Update hello web config</span></span>

<span data-ttu-id="1d54c-147">Novamente no Olá **FabrikamFiber.Web** projeto, cadeia de ligação Olá atualização Olá **Web. config** toopoint toohello do SQL Server no contentor de Olá, de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="1d54c-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="1d54c-148">Se quiser toouse um SQL Server diferente durante a criação de uma versão de compilação da aplicação web, adicione outra cadeia tooyour web.release.config o ficheiro de ligação.</span><span class="sxs-lookup"><span data-stu-id="1d54c-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="1d54c-149">O contentor de teste</span><span class="sxs-lookup"><span data-stu-id="1d54c-149">Test your container</span></span>

<span data-ttu-id="1d54c-150">Prima **F5** toorun e depuração aplicação Olá no seu contentor.</span><span class="sxs-lookup"><span data-stu-id="1d54c-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="1d54c-151">Limite abre uma página de início definido da sua aplicação utilizando o endereço IP de Olá do contentor de Olá no Olá NAT internos (normalmente 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="1d54c-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="1d54c-152">toolearn mais informações sobre a depuração de aplicações nos contentores utilizando o Visual Studio 2017, consulte [neste artigo][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="1d54c-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![exemplo de fabrikam num contentor][image-web-preview]

<span data-ttu-id="1d54c-154">contentor de Olá está agora pronto toobe incorporada e empacotada numa aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1d54c-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="1d54c-155">Assim que tiver a imagem de contentor Olá incorporada no seu computador, pode enviá-lo tooany registo de contentor e obtenha-tooany toorun de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="1d54c-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="1d54c-156">Preparar para a nuvem de Olá aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="1d54c-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="1d54c-157">aplicação de Olá tooget pronta para ser executado no Service Fabric no Azure, é preciso toocomplete dois passos:</span><span class="sxs-lookup"><span data-stu-id="1d54c-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="1d54c-158">Expor as portas de olá onde queremos tooreach capaz de toobe nossa aplicação web no cluster do Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="1d54c-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="1d54c-159">Forneça um produção pronto base de dados SQL para a nossa aplicação.</span><span class="sxs-lookup"><span data-stu-id="1d54c-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="1d54c-160">Expor as portas de Olá da aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="1d54c-160">Expose hello port for hello app</span></span>
<span data-ttu-id="1d54c-161">tem de ter configurámos, de cluster do Service Fabric Olá porta *80* aberta por predefinição no Olá Balanceador de carga do Azure, que equilibra e o cluster de toohello receber tráfego.</span><span class="sxs-lookup"><span data-stu-id="1d54c-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="1d54c-162">Pode expomos nosso contentor esta porta através do nosso ficheiro docker-Compose.yml.</span><span class="sxs-lookup"><span data-stu-id="1d54c-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="1d54c-163">No Visual Studio, abra **Explorador de soluções**, localizar **compor o docker**e o ficheiro aberto Olá **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="1d54c-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="1d54c-164">Modificar Olá `fabrikamfiber.web:` nó, adicionar um nó subordinado com o nome `ports:`.</span><span class="sxs-lookup"><span data-stu-id="1d54c-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="1d54c-165">Adicionar uma entrada de cadeia `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="1d54c-165">Add a string entry `- "80:80"`.</span></span>

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a><span data-ttu-id="1d54c-166">Utilizar uma base de dados do SQL Server de produção</span><span class="sxs-lookup"><span data-stu-id="1d54c-166">Use a production SQL database</span></span>
<span data-ttu-id="1d54c-167">Quando em execução na produção, precisamos que os nossos dados persistentes na nossa base de dados.</span><span class="sxs-lookup"><span data-stu-id="1d54c-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="1d54c-168">Atualmente não existem dados persistentes do tooguarantee de forma num contentor, existe, por conseguinte, não é possível armazenar dados de produção no SQL Server num contentor.</span><span class="sxs-lookup"><span data-stu-id="1d54c-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="1d54c-169">É recomendável que utilizar uma base de dados do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d54c-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="1d54c-170">tooset cópias de segurança e executar um servidor gerido do SQL Server no Azure, visite Olá [inícios rápidos de base de dados do SQL do Azure] [ link-azure-sql] artigo.</span><span class="sxs-lookup"><span data-stu-id="1d54c-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="1d54c-171">Lembre-se toochange Olá ligação cadeias toohello do SQL Server no Olá **web.release.config** ficheiro Olá **FabrikamFiber.Web** projeto.</span><span class="sxs-lookup"><span data-stu-id="1d54c-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="1d54c-172">Esta aplicação não consegue transições se nenhuma base de dados do SQL Server está acessível.</span><span class="sxs-lookup"><span data-stu-id="1d54c-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="1d54c-173">Pode escolher toogo avançar e implementar a aplicação Olá não SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1d54c-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="1d54c-174">Implementar com o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="1d54c-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="1d54c-175">tooset com a implementação com o Visual Studio Team Services, terá de tooinstall Olá [extensão de ferramentas de entrega contínua para Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="1d54c-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="1d54c-176">Esta extensão torna mais fácil toodeploy tooAzure configurando o Visual Studio Team Services e obtenha o seu cluster do Service Fabric tooyour aplicação implementada.</span><span class="sxs-lookup"><span data-stu-id="1d54c-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="1d54c-177">tooget iniciado, o código tem de estar alojado no controlo de origem.</span><span class="sxs-lookup"><span data-stu-id="1d54c-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="1d54c-178">parte do princípio de rest de Olá desta secção **git** está a ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="1d54c-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="1d54c-179">Configurar um repositório VSTS</span><span class="sxs-lookup"><span data-stu-id="1d54c-179">Set up a VSTS repo</span></span>
<span data-ttu-id="1d54c-180">No canto inferior direito de Olá do Visual Studio, clique em **adicionar tooSource controlo** > **Git** (ou qualquer opção que preferir).</span><span class="sxs-lookup"><span data-stu-id="1d54c-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Prima o botão de controlo de origem Olá][image-source-control]

<span data-ttu-id="1d54c-182">No Olá _equipa Explorer_ painel, prima **publicar repositório de Git**.</span><span class="sxs-lookup"><span data-stu-id="1d54c-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="1d54c-183">Selecione o nome do repositório VSTS e prima **repositório**.</span><span class="sxs-lookup"><span data-stu-id="1d54c-183">Select your VSTS repository name and press **Repository**.</span></span>

![publicar tooVSTS repositório][image-publish-repo]

<span data-ttu-id="1d54c-185">Agora que o seu código está sincronizado com um repositório de origem VSTS, pode configurar a integração contínua e entrega contínua.</span><span class="sxs-lookup"><span data-stu-id="1d54c-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="1d54c-186">Configurar a entrega contínua</span><span class="sxs-lookup"><span data-stu-id="1d54c-186">Setup continuous delivery</span></span>

<span data-ttu-id="1d54c-187">No _Explorador de soluções_, contexto Olá **solução** > **configurar contínua entrega**.</span><span class="sxs-lookup"><span data-stu-id="1d54c-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="1d54c-188">Selecione Olá subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d54c-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="1d54c-189">Definir **tipo de anfitrião** demasiado**Cluster do Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="1d54c-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="1d54c-190">Definir **anfitrião de destino** que criou na secção anterior Olá de cluster do toohello service fabric.</span><span class="sxs-lookup"><span data-stu-id="1d54c-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="1d54c-191">Escolha um **contentor registo** toopublish o contentor para.</span><span class="sxs-lookup"><span data-stu-id="1d54c-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="1d54c-192">Olá utilize **editar** toocreate de botão de registo do contentor.</span><span class="sxs-lookup"><span data-stu-id="1d54c-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="1d54c-193">Prima **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d54c-193">Press **OK**.</span></span>

![integração contínua de recursos de infraestrutura do serviço de configuração][image-setup-ci]
   
   <span data-ttu-id="1d54c-195">Depois de concluída a configuração de Olá, o contentor é implementado tooService recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="1d54c-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="1d54c-196">Sempre que push repositório toohello de atualizações é executada uma nova compilação e a versão.</span><span class="sxs-lookup"><span data-stu-id="1d54c-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1d54c-197">As imagens de contentor do edifício Olá demorar cerca de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="1d54c-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="1d54c-198">Olá primeira implementação toohello cluster do Service Fabric faz com que Olá base Windows Server Core contentor imagens toobe transferido.</span><span class="sxs-lookup"><span data-stu-id="1d54c-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="1d54c-199">transferência de Olá demora toocomplete adicionais 5-10 minutos.</span><span class="sxs-lookup"><span data-stu-id="1d54c-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="1d54c-200">Procure a aplicação do Centro de atendimento telefónico de Fabrikam toohello utilizando Olá url do cluster: por exemplo, *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="1d54c-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="1d54c-201">Agora que tem de e implementar a solução de centro de atendimento telefónico de Fabrikam Olá, pode abrir Olá [portal do Azure] [ link-azure-portal] e ver aplicação Olá em execução no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1d54c-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="1d54c-202">aplicação de Olá tootry, abra um browser e aceda toohello URL do seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1d54c-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d54c-203">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1d54c-203">Next steps</span></span>

<span data-ttu-id="1d54c-204">Neste tutorial, ficou a saber como:</span><span class="sxs-lookup"><span data-stu-id="1d54c-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1d54c-205">Criar um projeto de Docker no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d54c-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="1d54c-206">Containerize uma aplicação existente</span><span class="sxs-lookup"><span data-stu-id="1d54c-206">Containerize an existing application</span></span>
> * <span data-ttu-id="1d54c-207">Configurar a integração contínua com o Visual Studio e VSTS</span><span class="sxs-lookup"><span data-stu-id="1d54c-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
