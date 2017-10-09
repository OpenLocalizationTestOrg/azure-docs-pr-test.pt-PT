---
title: "aaaNode.js guia de introdução | Microsoft Docs"
description: "Saiba como toocreate Node.js uma simples aplicação web e implementá-la tooan serviço em nuvem Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="964f2-103">Criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="964f2-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="964f2-104">Este tutorial mostra como toocreate Node.js uma simples aplicação em execução num serviço em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="964f2-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="964f2-105">Serviços cloud são os blocos modulares de Olá das aplicações em nuvem dimensionáveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="964f2-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="964f2-106">Permitem a separação de Olá e gestão independente e escalável de componentes front-end e back-end da aplicação.</span><span class="sxs-lookup"><span data-stu-id="964f2-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="964f2-107">Os Cloud Services fornecem uma máquina virtual dedicada robusta para alojar cada função de forma fiável.</span><span class="sxs-lookup"><span data-stu-id="964f2-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="964f2-108">Para obter mais informações sobre serviços em nuvem e como comparar tooAzure Web sites e as máquinas virtuais, consulte [comparação de Web sites do Azure, os serviços de nuvem e máquinas virtuais].</span><span class="sxs-lookup"><span data-stu-id="964f2-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="964f2-109">Está à procura toobuild um site simples?</span><span class="sxs-lookup"><span data-stu-id="964f2-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="964f2-110">Se o seu cenário envolver apenas um front-end de site simples, considere a [utilização de uma aplicação Web simples].</span><span class="sxs-lookup"><span data-stu-id="964f2-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="964f2-111">Pode facilmente atualizar tooa serviço em nuvem à medida que aumenta a sua aplicação web e os seus requisitos se alteram.</span><span class="sxs-lookup"><span data-stu-id="964f2-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="964f2-112">Este tutorial descreve como compilar uma aplicação Web simples alojada numa função da Web.</span><span class="sxs-lookup"><span data-stu-id="964f2-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="964f2-113">Irá utilizar tootest de emulador de computação Olá a aplicação localmente, e em seguida, implementá-la utilizando as ferramentas de linha de comandos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="964f2-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="964f2-114">aplicação Olá é uma aplicação "Olá, mundo" simples:</span><span class="sxs-lookup"><span data-stu-id="964f2-114">hello application is a simple "hello world" application:</span></span>

![Um browser a apresentar a página de web de Olá mundo Olá][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="964f2-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="964f2-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="964f2-117">Este tutorial utiliza o Azure PowerShell, que requer o Windows.</span><span class="sxs-lookup"><span data-stu-id="964f2-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="964f2-118">Instale e configure o [Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="964f2-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="964f2-119">Transfira e instale Olá [Azure SDK para .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="964f2-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="964f2-120">No Olá instalar o programa de configuração, selecione:</span><span class="sxs-lookup"><span data-stu-id="964f2-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="964f2-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="964f2-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="964f2-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="964f2-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="964f2-123">Criar um projeto do Serviço em Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="964f2-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="964f2-124">Execute Olá tarefas toocreate um novo projeto do serviço de nuvem do Azure, juntamente com andaime Node.js básico a seguir:</span><span class="sxs-lookup"><span data-stu-id="964f2-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="964f2-125">Executar **do Windows PowerShell** como administrador; a partir de Olá **Menu Iniciar** ou **ecrã Iniciar**, procure **do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="964f2-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="964f2-126">[Ligue o PowerShell] tooyour subscrição.</span><span class="sxs-lookup"><span data-stu-id="964f2-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="964f2-127">Introduza Olá projeto do PowerShell cmdlet toocreate toocreate Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="964f2-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![resultado de Olá do comando do Olá New-AzureService helloworld][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="964f2-129">Olá **New-AzureServiceProject** cmdlet gera uma estrutura básica para publicar um tooa de aplicação Node.js serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="964f2-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="964f2-130">Contém os ficheiros de configuração necessários para publicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="964f2-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="964f2-131">Olá cmdlet também altera o diretório de toohello do diretório de trabalho para o serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="964f2-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="964f2-132">Olá cmdlet cria Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="964f2-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="964f2-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** e **ServiceDefinition.csdef**: ficheiros específicos do Azure necessários para publicar a aplicação.</span><span class="sxs-lookup"><span data-stu-id="964f2-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="964f2-134">Para obter mais informações, consulte [Descrição Geral da Criação de um Serviço Alojado do Azure].</span><span class="sxs-lookup"><span data-stu-id="964f2-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="964f2-135">**Deploymentsettings**: armazena as definições locais que são utilizadas pelo Olá cmdlets de implementação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="964f2-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="964f2-136">Introduza Olá os seguintes comandos tooadd uma nova função da web:</span><span class="sxs-lookup"><span data-stu-id="964f2-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![resultado Olá Olá comando Add-AzureNodeWebRole][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="964f2-138">Olá **Add-AzureNodeWebRole** cmdlet cria uma aplicação Node.js básica.</span><span class="sxs-lookup"><span data-stu-id="964f2-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="964f2-139">Também modifica Olá **. csfg** e **. csdef** ficheiros tooadd entradas de configuração para a nova função de Olá.</span><span class="sxs-lookup"><span data-stu-id="964f2-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="964f2-140">Se não especificar um nome de função, será utilizado um nome predefinido.</span><span class="sxs-lookup"><span data-stu-id="964f2-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="964f2-141">Pode fornecer um nome como primeiro parâmetro de cmdlet Olá:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="964f2-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="964f2-142">aplicação de Node.js Olá está definida no ficheiro de Olá **server.js**, localizado no diretório de Olá de função da web Olá (**WebRole1** por predefinição).</span><span class="sxs-lookup"><span data-stu-id="964f2-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="964f2-143">Eis o código de Olá:</span><span class="sxs-lookup"><span data-stu-id="964f2-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="964f2-144">Este código é, essencialmente, igual ao hello "Olá mundo" no Olá de exemplo de Olá [nodejs.org] Web site, exceto que utiliza o número de porta de Olá atribuído pelo ambiente de nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="964f2-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="964f2-145">Implementar Olá tooAzure de aplicação</span><span class="sxs-lookup"><span data-stu-id="964f2-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="964f2-146">toocomplete neste tutorial, precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="964f2-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="964f2-147">Pode [ativar os benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ou [inscrever-se numa conta gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="964f2-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="964f2-148">Transferir Olá Azure as definições de publicação</span><span class="sxs-lookup"><span data-stu-id="964f2-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="964f2-149">toodeploy tooAzure sua aplicação, primeiro tem de transferir Olá publicação definições para a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="964f2-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="964f2-150">Execute Olá seguinte cmdlet do PowerShell do Azure:</span><span class="sxs-lookup"><span data-stu-id="964f2-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="964f2-151">Este procedimento irá utilizar o seu browser toonavigate toohello publicar a página de transferências de definições.</span><span class="sxs-lookup"><span data-stu-id="964f2-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="964f2-152">Poderá ser pedido toolog com uma Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="964f2-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="964f2-153">Se assim for, utilize conta Olá associada à subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="964f2-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="964f2-154">Guarde Olá transferido perfil tooa localização do ficheiro facilmente acessível.</span><span class="sxs-lookup"><span data-stu-id="964f2-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="964f2-155">Execute o seguinte cmdlet tooimport Olá que transferiu do perfil de publicação:</span><span class="sxs-lookup"><span data-stu-id="964f2-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="964f2-156">Depois de importar Olá definições de publicação, considere eliminar Olá transferido o ficheiro. publishsettings, porque contém informações que podem permitir a alguém tooaccess sua conta.</span><span class="sxs-lookup"><span data-stu-id="964f2-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="964f2-157">Publicar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="964f2-157">Publish hello application</span></span>
<span data-ttu-id="964f2-158">toopublish executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="964f2-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="964f2-159">**-ServiceName** Especifica Olá nome para a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="964f2-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="964f2-160">Tem de ser um nome exclusivo, caso contrário Olá publicar processo irá falhar.</span><span class="sxs-lookup"><span data-stu-id="964f2-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="964f2-161">Olá **Get-Data** comando adiciona uma cadeia de data/hora que deve certificar-nome Olá exclusivo.</span><span class="sxs-lookup"><span data-stu-id="964f2-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="964f2-162">**-Location** Especifica Olá datacenter que Olá aplicação será alojada no.</span><span class="sxs-lookup"><span data-stu-id="964f2-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="964f2-163">toosee uma lista de datacenters disponíveis, utilize Olá **Get-AzureLocation** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="964f2-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="964f2-164">**-Launch** abre uma janela do browser e navega serviço toohello alojado após conclusão da implementação.</span><span class="sxs-lookup"><span data-stu-id="964f2-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="964f2-165">Publicação for bem sucedida, verá um resposta semelhante toohello seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="964f2-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![resultado Olá Olá comando Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="964f2-167">Isto pode demorar alguns minutos até Olá aplicação toodeploy e fique disponível quando publicada pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="964f2-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="964f2-168">Depois de concluída a implementação de Olá, uma janela do browser irá abrir e navegue toohello o serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="964f2-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Uma janela do browser a apresentar Olá página Olá, mundo; URL de Olá indica a página Olá está alojada no Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="964f2-170">A aplicação está agora em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="964f2-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="964f2-171">Olá **Publish-AzureServiceProject** cmdlet efetua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="964f2-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="964f2-172">Cria um toodeploy de pacote.</span><span class="sxs-lookup"><span data-stu-id="964f2-172">Creates a package toodeploy.</span></span> <span data-ttu-id="964f2-173">pacote de Olá contém todos os ficheiros de Olá na pasta de aplicação.</span><span class="sxs-lookup"><span data-stu-id="964f2-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="964f2-174">Cria uma nova **Conta do Storage**, se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="964f2-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="964f2-175">Olá conta do storage do Azure é o pacote de aplicação Olá toostore utilizado durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="964f2-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="964f2-176">Pode eliminar em segurança a conta de armazenamento Olá após a conclusão da implementação.</span><span class="sxs-lookup"><span data-stu-id="964f2-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="964f2-177">Cria um novo **serviço em nuvem**, se ainda não existir um.</span><span class="sxs-lookup"><span data-stu-id="964f2-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="964f2-178">A **serviço em nuvem** é contentor Olá na qual a aplicação será alojada quando for tooAzure implementado.</span><span class="sxs-lookup"><span data-stu-id="964f2-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="964f2-179">Para obter mais informações, consulte [Descrição Geral da Criação de um Serviço Alojado do Azure].</span><span class="sxs-lookup"><span data-stu-id="964f2-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="964f2-180">Publica tooAzure de pacote de implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="964f2-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="964f2-181">Parar e eliminar a aplicação</span><span class="sxs-lookup"><span data-stu-id="964f2-181">Stopping and deleting your application</span></span>
<span data-ttu-id="964f2-182">Depois de implementar a aplicação, poderá ser útil toodisable-lo, para evitar custos adicionais.</span><span class="sxs-lookup"><span data-stu-id="964f2-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="964f2-183">O Azure cobra as instâncias de função da Web por hora de tempo do servidor consumido.</span><span class="sxs-lookup"><span data-stu-id="964f2-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="964f2-184">Hora do servidor é consumida logo que a aplicação é implementada, mesmo se instâncias Olá não estão em execução e estão em estado de Olá parado.</span><span class="sxs-lookup"><span data-stu-id="964f2-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="964f2-185">Na janela do Windows PowerShell Olá, pare a implementação do serviço de Olá criada na secção anterior Olá com Olá seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="964f2-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="964f2-186">A parar serviço Olá poderá demorar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="964f2-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="964f2-187">Quando Olá serviço for parado, receberá uma mensagem a indicar que foi parado.</span><span class="sxs-lookup"><span data-stu-id="964f2-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![Estado de Olá do comando de Olá Stop-AzureService][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="964f2-189">serviço de Olá toodelete, Olá chamada seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="964f2-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="964f2-190">Quando lhe for pedido, introduza **Y** serviço de Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="964f2-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="964f2-191">A eliminar o serviço de Olá poderá demorar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="964f2-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="964f2-192">Depois de Olá tiver sido eliminado, receberá uma mensagem a indicar que o serviço de Olá foi eliminado.</span><span class="sxs-lookup"><span data-stu-id="964f2-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![Estado de Olá do comando de Olá Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="964f2-194">A eliminar o serviço de Olá não elimina a conta de armazenamento de Olá que foi criada quando o serviço de Olá foi inicialmente publicado e irá continuar toobe faturado por armazenamento utilizado.</span><span class="sxs-lookup"><span data-stu-id="964f2-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="964f2-195">Se mais nada estiver a utilizar armazenamento Olá, poderá ser útil toodelete-lo.</span><span class="sxs-lookup"><span data-stu-id="964f2-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="964f2-196">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="964f2-196">Next steps</span></span>
<span data-ttu-id="964f2-197">Para obter mais informações, consulte Olá [Centro para programadores do Node.js].</span><span class="sxs-lookup"><span data-stu-id="964f2-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[comparação de Web sites do Azure, os serviços de nuvem e máquinas virtuais]: ../app-service-web/choose-web-site-cloud-service-vm.md
[utilização de uma aplicação Web simples]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK para .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Ligue o PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Descrição Geral da Criação de um Serviço Alojado do Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centro para programadores do Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
