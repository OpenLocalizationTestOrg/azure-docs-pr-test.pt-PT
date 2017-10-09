---
title: "aaaCreate uma aplicação .NET para o Service Fabric | Microsoft Docs"
description: "Saiba como toocreate uma aplicação com um front-end do ASP.NET Core e uma fiável com monitorização de estado de back-end de serviço e implementar Olá aplicação tooa cluster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="490b9-103">Criar e implementar uma aplicação com um serviço de front-end de API Web do ASP.NET Core e o serviço de back-end com monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="490b9-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="490b9-104">Este tutorial faz parte de um de uma série.</span><span class="sxs-lookup"><span data-stu-id="490b9-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="490b9-105">Ficará a saber como toocreate uma aplicação de Service Fabric do Azure com um início de API Web do ASP.NET Core de fim e um serviço de back-end com monitorização de estado toostore os dados.</span><span class="sxs-lookup"><span data-stu-id="490b9-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="490b9-106">Quando tiver terminado, terá uma aplicação de voto com um front-end que guarda os resultados de votos num serviço de back-end com monitorização de estado no cluster de Olá de web de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="490b9-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="490b9-107">Se não quiser toomanually criar Olá votar na aplicação, pode [transferir o código de origem Olá](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) para Olá concluir a aplicação e avançar diretamente demasiado[guiá votar na aplicação de exemplo de Olá](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="490b9-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Diagrama de aplicação](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="490b9-109">Na parte de uma série de Olá, saiba como:</span><span class="sxs-lookup"><span data-stu-id="490b9-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="490b9-110">Criar um serviço de API Web do ASP.NET Core como um serviço fiável com monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="490b9-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="490b9-111">Criar um serviço de aplicação Web do ASP.NET Core como um serviço web sem monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="490b9-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="490b9-112">Utilizar Olá proxy inverso toocommunicate com o serviço com estado Olá</span><span class="sxs-lookup"><span data-stu-id="490b9-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="490b9-113">Este tutorial série, a saber como:</span><span class="sxs-lookup"><span data-stu-id="490b9-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="490b9-114">Criar uma aplicação .NET Service Fabric</span><span class="sxs-lookup"><span data-stu-id="490b9-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="490b9-115">Implementar Olá aplicação tooa remoto cluster</span><span class="sxs-lookup"><span data-stu-id="490b9-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="490b9-116">Configurar CI/CD utilizando o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="490b9-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="490b9-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="490b9-117">Prerequisites</span></span>
<span data-ttu-id="490b9-118">Antes de começar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="490b9-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="490b9-119">Se não tiver uma subscrição do Azure, crie um [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="490b9-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="490b9-120">[Instalar Visual Studio 2017](https://www.visualstudio.com/) e instalar Olá **programação do Azure** e **desenvolvimento ASP.NET e web** cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="490b9-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="490b9-121">Instalar Olá SDK de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="490b9-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="490b9-122">Criar um serviço de API Web do ASP.NET como um serviço fiável</span><span class="sxs-lookup"><span data-stu-id="490b9-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="490b9-123">Em primeiro lugar, crie web Olá front-end de Olá votar na aplicação com o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="490b9-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="490b9-124">ASP.NET Core é uma estrutura de desenvolvimento simples, de plataforma web que pode utilizar a IU da web moderna toocreate e web APIs.</span><span class="sxs-lookup"><span data-stu-id="490b9-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="490b9-125">tooget uma compreensão concluída de forma ASP.NET Core é se integra com o Service Fabric, recomendamos vivamente que ler através de Olá [ASP.NET Core no Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="490b9-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="490b9-126">Por agora, pode seguir este tutorial tooget a trabalhar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="490b9-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="490b9-127">toolearn mais informações sobre o ASP.NET Core, consulte Olá [ASP.NET Core documentação](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="490b9-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="490b9-128">Este tutorial baseia-se no Olá [ASP.NET Core tools para Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="490b9-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="490b9-129">ferramentas do .NET Core Olá para Visual Studio 2015 já não estão a ser atualizadas.</span><span class="sxs-lookup"><span data-stu-id="490b9-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="490b9-130">Inicie o Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="490b9-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="490b9-131">Criar um projeto com **ficheiro**->**novo**->**projeto**</span><span class="sxs-lookup"><span data-stu-id="490b9-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="490b9-132">No Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicação de Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="490b9-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="490b9-133">Nome da aplicação Olá **voto** e prima **OK**.</span><span class="sxs-lookup"><span data-stu-id="490b9-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Caixa de diálogo de novo projeto no Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="490b9-135">No Olá **novo serviço de recursos de infraestrutura de serviço** página, escolha **sem monitorização de estado ASP.NET Core**e o nome do seu serviço **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="490b9-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Escolher o serviço web ASP.NET na caixa de diálogo Olá novo serviço](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="490b9-137">página seguinte Olá fornece um conjunto de ASP.NET Core modelos de projeto.</span><span class="sxs-lookup"><span data-stu-id="490b9-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="490b9-138">Para este tutorial, escolha **aplicação Web**.</span><span class="sxs-lookup"><span data-stu-id="490b9-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Escolha o tipo de projeto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="490b9-140">Visual Studio cria uma aplicação e um projeto de serviço e apresenta-os no Explorador de soluções.</span><span class="sxs-lookup"><span data-stu-id="490b9-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Explorador de soluções a seguir a criação da aplicação com o serviço de Web API do ASP.NET core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="490b9-142">Adicionar AngularJS toohello VotingWeb serviço</span><span class="sxs-lookup"><span data-stu-id="490b9-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="490b9-143">Adicionar [AngularJS](http://angularjs.org/) serviço tooyour utilizando incorporado Olá [Bower suporte](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="490b9-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="490b9-144">Abra *bower.json* e adicionar entradas para angular para e de arranque de angular para, em seguida, guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="490b9-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
<span data-ttu-id="490b9-145">Após guardar Olá *bower.json* ficheiro, Angular está instalado no seu projeto *wwwroot/lib* pasta.</span><span class="sxs-lookup"><span data-stu-id="490b9-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="490b9-146">Além disso, este está listado no Olá *dependências/Bower* pasta.</span><span class="sxs-lookup"><span data-stu-id="490b9-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="490b9-147">Atualizar Olá site.js ficheiro</span><span class="sxs-lookup"><span data-stu-id="490b9-147">Update hello site.js file</span></span>
<span data-ttu-id="490b9-148">Abra Olá *wwwroot/js/site.js* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="490b9-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="490b9-149">Substitua os respetivos conteúdos Olá JavaScript utilizado pelas vistas de Home Olá:</span><span class="sxs-lookup"><span data-stu-id="490b9-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="490b9-150">Ficheiro de atualização de Olá Index. cshtml</span><span class="sxs-lookup"><span data-stu-id="490b9-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="490b9-151">Abra Olá *Views/Home/Index.cshtml* ficheiro, Olá vista toohello Home um controlador específico.</span><span class="sxs-lookup"><span data-stu-id="490b9-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="490b9-152">Substitua o conteúdo seguinte Olá, em seguida, guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="490b9-152">Replace its contents with hello following, then save your changes.</span></span>

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click toovote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="490b9-153">Atualizar Olá layout ficheiro</span><span class="sxs-lookup"><span data-stu-id="490b9-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="490b9-154">Abra Olá *Views/Shared/_Layout.cshtml* ficheiro, o esquema predefinido de Olá para a aplicação ASP.NET Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="490b9-155">Substitua o conteúdo seguinte Olá, em seguida, guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="490b9-155">Replace its contents with hello following, then save your changes.</span></span>

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="490b9-156">Atualizar Olá VotingWeb.cs ficheiro</span><span class="sxs-lookup"><span data-stu-id="490b9-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="490b9-157">Abra Olá *VotingWeb.cs* ficheiro, que cria Olá ASP.NET Core WebHost dentro de serviço sem estado Olá utilizar Olá WebListener web server.</span><span class="sxs-lookup"><span data-stu-id="490b9-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="490b9-158">Adicionar Olá `using System.Net.Http;` toohello directiva superior do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="490b9-159">Substitua Olá `CreateServiceInstanceListeners()` funcionar com o seguinte Olá, em seguida, guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="490b9-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="490b9-160">Adicione Olá VotesController.cs ficheiro</span><span class="sxs-lookup"><span data-stu-id="490b9-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="490b9-161">Adicione um controlador que define as ações de votos.</span><span class="sxs-lookup"><span data-stu-id="490b9-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="490b9-162">Clique com o botão direito no Olá **controladores** pasta, em seguida, selecione **adicionar -> novo item -> classe**.</span><span class="sxs-lookup"><span data-stu-id="490b9-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="490b9-163">Nome do ficheiro de Olá "VotesController.cs" e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="490b9-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="490b9-164">Substitua o conteúdo do ficheiro Olá seguinte Olá, em seguida, guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="490b9-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="490b9-165">Mais adiante, [ficheiro de atualização de Olá VotesController.cs](#updatevotecontroller_anchor), este ficheiro será modificado tooread e escrever dados de votos do serviço de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="490b9-166">Por agora, o controlador de Olá devolve vista de toohello de dados de cadeia estática.</span><span class="sxs-lookup"><span data-stu-id="490b9-166">For now, hello controller returns static string data toohello view.</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="490b9-167">Implementar e executar a aplicação Olá localmente</span><span class="sxs-lookup"><span data-stu-id="490b9-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="490b9-168">Agora, pode avançar e executar a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="490b9-169">No Visual Studio, prima `F5` aplicação de Olá toodeploy de depuração.</span><span class="sxs-lookup"><span data-stu-id="490b9-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="490b9-170">`F5`falha se anteriormente não abra o Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="490b9-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="490b9-171">Olá pela primeira vez, executar e implementar a aplicação de Olá localmente, Visual Studio cria um cluster local para a depuração.</span><span class="sxs-lookup"><span data-stu-id="490b9-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="490b9-172">Criação do cluster pode demorar algum tempo.</span><span class="sxs-lookup"><span data-stu-id="490b9-172">Cluster creation may take some time.</span></span> <span data-ttu-id="490b9-173">o estado de criação do cluster Olá é apresentado na janela de saída do Visual Studio Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="490b9-174">Neste momento, a aplicação web deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="490b9-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core front-end](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="490b9-176">toostop depuração aplicação Olá, volte atrás tooVisual Studio e prima **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="490b9-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="490b9-177">Adicionar uma aplicação de tooyour do serviço de back-end com monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="490b9-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="490b9-178">Agora que temos um serviço de API Web do ASP.NET em execução na nossa aplicação, vamos avançar e adicionar um serviço fiável com estado toostore alguns dados na nossa aplicação.</span><span class="sxs-lookup"><span data-stu-id="490b9-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="490b9-179">Recursos de infraestrutura de serviço permite-lhe tooconsistently e fiável armazenar os seus diretamente dados dentro do seu serviço através de coleções fiáveis.</span><span class="sxs-lookup"><span data-stu-id="490b9-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="490b9-180">Coleções fiáveis são um conjunto de classes de elevada disponibilidade e fiável coleção que estão familiarizado tooanyone que tenha utilizado c# coleções.</span><span class="sxs-lookup"><span data-stu-id="490b9-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="490b9-181">Neste tutorial, vai criar um serviço que armazena um valor de contador numa coleção fiável.</span><span class="sxs-lookup"><span data-stu-id="490b9-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="490b9-182">No Explorador de soluções, faça duplo clique **serviços** dentro Olá projeto de aplicação e escolha **adicionar > novo serviço de recursos de infraestrutura de serviço**.</span><span class="sxs-lookup"><span data-stu-id="490b9-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Adicionar uma nova aplicação de tooan do serviço existente](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="490b9-184">No Olá **novo serviço de recursos de infraestrutura de serviço** caixa de diálogo, escolha **com monitorização de estado ASP.NET Core**e o serviço de nomes de Olá **VotingData** e prima **OK**.</span><span class="sxs-lookup"><span data-stu-id="490b9-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Caixa de diálogo novo serviço no Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="490b9-186">Depois do projeto de serviço é criado, tem dois serviços na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="490b9-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="490b9-187">Como continuar toobuild a aplicação, pode adicionar mais serviços em Olá mesma forma.</span><span class="sxs-lookup"><span data-stu-id="490b9-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="490b9-188">Cada pode ser independente com versão e atualizado.</span><span class="sxs-lookup"><span data-stu-id="490b9-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="490b9-189">página seguinte Olá fornece um conjunto de ASP.NET Core modelos de projeto.</span><span class="sxs-lookup"><span data-stu-id="490b9-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="490b9-190">Para este tutorial, escolha **Web API**.</span><span class="sxs-lookup"><span data-stu-id="490b9-190">For this tutorial, choose **Web API**.</span></span>

    ![Escolha o tipo de projeto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="490b9-192">Visual Studio cria um projeto de serviço e apresenta-os no Explorador de soluções.</span><span class="sxs-lookup"><span data-stu-id="490b9-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Explorador de Soluções](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="490b9-194">Adicione Olá VoteDataController.cs ficheiro</span><span class="sxs-lookup"><span data-stu-id="490b9-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="490b9-195">No Olá **VotingData** contexto do projeto no Olá **controladores** pasta, em seguida, selecione **adicionar -> novo item -> classe**.</span><span class="sxs-lookup"><span data-stu-id="490b9-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="490b9-196">Nome do ficheiro de Olá "VoteDataController.cs" e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="490b9-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="490b9-197">Substitua o conteúdo do ficheiro Olá seguinte Olá, em seguida, guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="490b9-197">Replace hello file contents with hello following, then save your changes.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-hello-services"></a><span data-ttu-id="490b9-198">Ligar a serviços Olá</span><span class="sxs-lookup"><span data-stu-id="490b9-198">Connect hello services</span></span>
<span data-ttu-id="490b9-199">Neste passo seguinte, iremos ligar Olá dois serviços e tornar Olá Web front-end de aplicação get e set votar informações a partir do serviço de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="490b9-200">O Service Fabric fornece flexibilidade concluída na como comunicar com serviços fiáveis.</span><span class="sxs-lookup"><span data-stu-id="490b9-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="490b9-201">Dentro de uma única aplicação, poderá ter serviços que estão acessíveis através de TCP.</span><span class="sxs-lookup"><span data-stu-id="490b9-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="490b9-202">Outros serviços que podem estar acessíveis através de uma API de REST de HTTP e ainda outros serviços poderia ficar acessíveis através de web sockets.</span><span class="sxs-lookup"><span data-stu-id="490b9-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="490b9-203">Para em segundo plano nas opções de Olá disponíveis e fala Olá envolvidas, consulte [comunicar com serviços](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="490b9-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="490b9-204">Neste tutorial, estamos a utilizar [Web API do ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="490b9-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="490b9-205">Atualizar Olá VotesController.cs ficheiro</span><span class="sxs-lookup"><span data-stu-id="490b9-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="490b9-206">No Olá **VotingWeb** projeto, abra Olá *Controllers/VotesController.cs* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="490b9-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="490b9-207">Substitua Olá `VotesController` classe conteúdo de definição com a seguinte Olá, em seguida, guarde as alterações.</span><span class="sxs-lookup"><span data-stu-id="490b9-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="490b9-208">Percorrer Olá votar na aplicação de exemplo</span><span class="sxs-lookup"><span data-stu-id="490b9-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="490b9-209">Olá voto a aplicação é composta por dois serviços:</span><span class="sxs-lookup"><span data-stu-id="490b9-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="490b9-210">Serviço de front-end (VotingWeb) Web - web de ASP.NET Core um serviço front-end, o que funciona a página web de Olá e expõe web toocommunicate APIs com o serviço de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="490b9-211">O serviço de back-end (VotingData)-o serviço de web de uma ASP.NET Core, que expõe um voto de Olá toostore API resulta num dictionary fiável persistentes no disco.</span><span class="sxs-lookup"><span data-stu-id="490b9-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagrama de aplicação](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="490b9-213">Quando votar em Olá de aplicação Olá os seguintes eventos ocorrem:</span><span class="sxs-lookup"><span data-stu-id="490b9-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="490b9-214">Um JavaScript envia Olá voto pedido toohello API web no serviço de front-end Olá web como um pedido HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="490b9-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="490b9-215">serviço de front-end Olá web utiliza um toolocate de proxy e reencaminhar o serviço de back-end um toohello de pedido HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="490b9-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="490b9-216">serviço de back-end Olá demora pedido recebido Olá e arquivos Olá atualizado resultado um dicionário fiável, que obtém toomultiple replicadas nós num cluster de Olá e persistentes no disco.</span><span class="sxs-lookup"><span data-stu-id="490b9-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="490b9-217">Dados de todas as aplicações de Olá são armazenados no cluster de Olá, pelo que não é necessária nenhuma base de dados.</span><span class="sxs-lookup"><span data-stu-id="490b9-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="490b9-218">Depuração no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="490b9-218">Debug in Visual Studio</span></span>
<span data-ttu-id="490b9-219">Quando a depuração de aplicações no Visual Studio, está a utilizar um cluster de desenvolvimento do Service Fabric local.</span><span class="sxs-lookup"><span data-stu-id="490b9-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="490b9-220">Ter Olá opção tooadjust seu cenário de tooyour de experiência de depuração.</span><span class="sxs-lookup"><span data-stu-id="490b9-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="490b9-221">Nesta aplicação, podemos armazenar dados no nosso serviço de back-end, utilizando um dicionário fiável.</span><span class="sxs-lookup"><span data-stu-id="490b9-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="490b9-222">Visual Studio remove aplicação Olá por predefinição, quando parar o depurador Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="490b9-223">Remover aplicação Olá faz com que dados Olá no back-end de Olá serviço tooalso removidos.</span><span class="sxs-lookup"><span data-stu-id="490b9-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="490b9-224">dados de Olá toopersist entre sessões de depuração, pode alterar Olá **modo de depuração da aplicação** como uma propriedade no Olá **voto** projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="490b9-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="490b9-225">toolook, o que acontece no código Olá, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="490b9-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="490b9-226">Abra Olá **VotesController.cs** de ficheiros e defina um ponto de interrupção no Olá API web do **colocar** método (linha 47) - pode procurar ficheiro Olá Olá Explorador de soluções no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="490b9-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="490b9-227">Abra Olá **VoteDataController.cs** de ficheiros e defina um ponto de interrupção da API web **colocar** método (50 de linha).</span><span class="sxs-lookup"><span data-stu-id="490b9-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="490b9-228">Voltar atrás toohello browser e clique numa opção de voto ou adicionar uma nova opção de voto.</span><span class="sxs-lookup"><span data-stu-id="490b9-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="490b9-229">Atingiu o Olá primeiro ponto de interrupção do controlador da api do Olá frente-end da web.</span><span class="sxs-lookup"><span data-stu-id="490b9-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="490b9-230">Este é onde Olá JavaScript no browser Olá envia um controlador de API do pedido toohello web no serviço de front-end Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Adicionar serviço de front-end de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="490b9-232">Primeiro vamos construir Olá URL toohello ReverseProxy para o nosso serviço de back-end **(1)**.</span><span class="sxs-lookup"><span data-stu-id="490b9-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="490b9-233">Em seguida, iremos enviar Olá HTTP PUT pedido toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="490b9-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="490b9-234">Por fim Olá, Devolvemos resposta Olá do cliente de toohello do serviço de back-end Olá **(3)**.</span><span class="sxs-lookup"><span data-stu-id="490b9-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="490b9-235">Prima **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="490b9-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="490b9-236">Está agora no ponto de interrupção de Olá no serviço de back-end Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Adicionar serviço de Back-End de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="490b9-238">Na linha de primeiro Olá no método Olá **(1)** estamos a utilizar Olá `StateManager` tooget ou adicionar um dicionário fiável chamado `counts`.</span><span class="sxs-lookup"><span data-stu-id="490b9-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="490b9-239">Todas as interações com valores num dictionary fiável necessitam de uma transação, esta utilizando instrução **(2)** cria esse transação.</span><span class="sxs-lookup"><span data-stu-id="490b9-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="490b9-240">Transação Olá, vamos, em seguida, atualizar valor Olá chave relevantes do Olá para Olá votar na opção e consolidações Olá operação **(3)**.</span><span class="sxs-lookup"><span data-stu-id="490b9-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="490b9-241">Após a consolidação de Olá método devolve, Olá dados são atualizados no dicionário de Olá e replicados tooother nós num cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="490b9-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="490b9-242">dados de Olá estão agora armazenados em segurança num cluster de Olá e serviço de back-end Olá pode efetuar a ativação pós-falha tooother nós, continua a ter dados Olá disponíveis.</span><span class="sxs-lookup"><span data-stu-id="490b9-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="490b9-243">Prima **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="490b9-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="490b9-244">Olá toostop sessão, prima de depuração **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="490b9-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="490b9-245">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="490b9-245">Next steps</span></span>
<span data-ttu-id="490b9-246">Nesta parte do tutorial Olá, aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="490b9-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="490b9-247">Criar um serviço de API Web do ASP.NET Core como um serviço fiável com monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="490b9-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="490b9-248">Criar um serviço de aplicação Web do ASP.NET Core como um serviço web sem monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="490b9-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="490b9-249">Utilizar Olá proxy inverso toocommunicate com o serviço com estado Olá</span><span class="sxs-lookup"><span data-stu-id="490b9-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="490b9-250">Avançadas toohello próximo tutorial:</span><span class="sxs-lookup"><span data-stu-id="490b9-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="490b9-251">Implementar Olá tooAzure de aplicação</span><span class="sxs-lookup"><span data-stu-id="490b9-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
