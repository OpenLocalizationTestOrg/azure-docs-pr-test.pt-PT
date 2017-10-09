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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Criar e implementar uma aplicação com um serviço de front-end de API Web do ASP.NET Core e o serviço de back-end com monitorização de estado
Este tutorial faz parte de um de uma série.  Ficará a saber como toocreate uma aplicação de Service Fabric do Azure com um início de API Web do ASP.NET Core de fim e um serviço de back-end com monitorização de estado toostore os dados. Quando tiver terminado, terá uma aplicação de voto com um front-end que guarda os resultados de votos num serviço de back-end com monitorização de estado no cluster de Olá de web de ASP.NET Core. Se não quiser toomanually criar Olá votar na aplicação, pode [transferir o código de origem Olá](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) para Olá concluir a aplicação e avançar diretamente demasiado[guiá votar na aplicação de exemplo de Olá](#walkthrough_anchor).

![Diagrama de aplicação](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Na parte de uma série de Olá, saiba como:

> [!div class="checklist"]
> * Criar um serviço de API Web do ASP.NET Core como um serviço fiável com monitorização de estado
> * Criar um serviço de aplicação Web do ASP.NET Core como um serviço web sem monitorização de estado
> * Utilizar Olá proxy inverso toocommunicate com o serviço com estado Olá

Este tutorial série, a saber como:
> [!div class="checklist"]
> * Criar uma aplicação .NET Service Fabric
> * [Implementar Olá aplicação tooa remoto cluster](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Configurar CI/CD utilizando o Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial:
- Se não tiver uma subscrição do Azure, crie um [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Instalar Visual Studio 2017](https://www.visualstudio.com/) e instalar Olá **programação do Azure** e **desenvolvimento ASP.NET e web** cargas de trabalho.
- [Instalar Olá SDK de Service Fabric](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Criar um serviço de API Web do ASP.NET como um serviço fiável
Em primeiro lugar, crie web Olá front-end de Olá votar na aplicação com o ASP.NET Core. ASP.NET Core é uma estrutura de desenvolvimento simples, de plataforma web que pode utilizar a IU da web moderna toocreate e web APIs. tooget uma compreensão concluída de forma ASP.NET Core é se integra com o Service Fabric, recomendamos vivamente que ler através de Olá [ASP.NET Core no Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) artigo. Por agora, pode seguir este tutorial tooget a trabalhar rapidamente. toolearn mais informações sobre o ASP.NET Core, consulte Olá [ASP.NET Core documentação](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> Este tutorial baseia-se no Olá [ASP.NET Core tools para Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). ferramentas do .NET Core Olá para Visual Studio 2015 já não estão a ser atualizadas.

1. Inicie o Visual Studio como **administrador**.

2. Criar um projeto com **ficheiro**->**novo**->**projeto**

3. No Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicação de Service Fabric**.

4. Nome da aplicação Olá **voto** e prima **OK**.

   ![Caixa de diálogo de novo projeto no Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. No Olá **novo serviço de recursos de infraestrutura de serviço** página, escolha **sem monitorização de estado ASP.NET Core**e o nome do seu serviço **VotingWeb**.
   
   ![Escolher o serviço web ASP.NET na caixa de diálogo Olá novo serviço](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. página seguinte Olá fornece um conjunto de ASP.NET Core modelos de projeto. Para este tutorial, escolha **aplicação Web**. 
   
   ![Escolha o tipo de projeto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio cria uma aplicação e um projeto de serviço e apresenta-os no Explorador de soluções.

   ![Explorador de soluções a seguir a criação da aplicação com o serviço de Web API do ASP.NET core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>Adicionar AngularJS toohello VotingWeb serviço
Adicionar [AngularJS](http://angularjs.org/) serviço tooyour utilizando incorporado Olá [Bower suporte](/aspnet/core/client-side/bower). Abra *bower.json* e adicionar entradas para angular para e de arranque de angular para, em seguida, guarde as alterações.

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
Após guardar Olá *bower.json* ficheiro, Angular está instalado no seu projeto *wwwroot/lib* pasta. Além disso, este está listado no Olá *dependências/Bower* pasta.

### <a name="update-hello-sitejs-file"></a>Atualizar Olá site.js ficheiro
Abra Olá *wwwroot/js/site.js* ficheiro.  Substitua os respetivos conteúdos Olá JavaScript utilizado pelas vistas de Home Olá:

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

### <a name="update-hello-indexcshtml-file"></a>Ficheiro de atualização de Olá Index. cshtml
Abra Olá *Views/Home/Index.cshtml* ficheiro, Olá vista toohello Home um controlador específico.  Substitua o conteúdo seguinte Olá, em seguida, guarde as alterações.

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

### <a name="update-hello-layoutcshtml-file"></a>Atualizar Olá layout ficheiro
Abra Olá *Views/Shared/_Layout.cshtml* ficheiro, o esquema predefinido de Olá para a aplicação ASP.NET Olá.  Substitua o conteúdo seguinte Olá, em seguida, guarde as alterações.

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

### <a name="update-hello-votingwebcs-file"></a>Atualizar Olá VotingWeb.cs ficheiro
Abra Olá *VotingWeb.cs* ficheiro, que cria Olá ASP.NET Core WebHost dentro de serviço sem estado Olá utilizar Olá WebListener web server.  Adicionar Olá `using System.Net.Http;` toohello directiva superior do ficheiro de Olá.  Substitua Olá `CreateServiceInstanceListeners()` funcionar com o seguinte Olá, em seguida, guarde as alterações.

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

### <a name="add-hello-votescontrollercs-file"></a>Adicione Olá VotesController.cs ficheiro
Adicione um controlador que define as ações de votos. Clique com o botão direito no Olá **controladores** pasta, em seguida, selecione **adicionar -> novo item -> classe**.  Nome do ficheiro de Olá "VotesController.cs" e clique em **adicionar**.  Substitua o conteúdo do ficheiro Olá seguinte Olá, em seguida, guarde as alterações.  Mais adiante, [ficheiro de atualização de Olá VotesController.cs](#updatevotecontroller_anchor), este ficheiro será modificado tooread e escrever dados de votos do serviço de back-end Olá.  Por agora, o controlador de Olá devolve vista de toohello de dados de cadeia estática.

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



### <a name="deploy-and-run-hello-application-locally"></a>Implementar e executar a aplicação Olá localmente
Agora, pode avançar e executar a aplicação Olá. No Visual Studio, prima `F5` aplicação de Olá toodeploy de depuração. `F5`falha se anteriormente não abra o Visual Studio como **administrador**.

> [!NOTE]
> Olá pela primeira vez, executar e implementar a aplicação de Olá localmente, Visual Studio cria um cluster local para a depuração.  Criação do cluster pode demorar algum tempo. o estado de criação do cluster Olá é apresentado na janela de saída do Visual Studio Olá.

Neste momento, a aplicação web deve ter o seguinte aspeto:

![ASP.NET Core front-end](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

toostop depuração aplicação Olá, volte atrás tooVisual Studio e prima **Shift + F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Adicionar uma aplicação de tooyour do serviço de back-end com monitorização de estado
Agora que temos um serviço de API Web do ASP.NET em execução na nossa aplicação, vamos avançar e adicionar um serviço fiável com estado toostore alguns dados na nossa aplicação.

Recursos de infraestrutura de serviço permite-lhe tooconsistently e fiável armazenar os seus diretamente dados dentro do seu serviço através de coleções fiáveis. Coleções fiáveis são um conjunto de classes de elevada disponibilidade e fiável coleção que estão familiarizado tooanyone que tenha utilizado c# coleções.

Neste tutorial, vai criar um serviço que armazena um valor de contador numa coleção fiável.

1. No Explorador de soluções, faça duplo clique **serviços** dentro Olá projeto de aplicação e escolha **adicionar > novo serviço de recursos de infraestrutura de serviço**.
   
    ![Adicionar uma nova aplicação de tooan do serviço existente](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. No Olá **novo serviço de recursos de infraestrutura de serviço** caixa de diálogo, escolha **com monitorização de estado ASP.NET Core**e o serviço de nomes de Olá **VotingData** e prima **OK**.

    ![Caixa de diálogo novo serviço no Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Depois do projeto de serviço é criado, tem dois serviços na sua aplicação. Como continuar toobuild a aplicação, pode adicionar mais serviços em Olá mesma forma. Cada pode ser independente com versão e atualizado.

3. página seguinte Olá fornece um conjunto de ASP.NET Core modelos de projeto. Para este tutorial, escolha **Web API**.

    ![Escolha o tipo de projeto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio cria um projeto de serviço e apresenta-os no Explorador de soluções.

    ![Explorador de Soluções](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Adicione Olá VoteDataController.cs ficheiro

No Olá **VotingData** contexto do projeto no Olá **controladores** pasta, em seguida, selecione **adicionar -> novo item -> classe**. Nome do ficheiro de Olá "VoteDataController.cs" e clique em **adicionar**. Substitua o conteúdo do ficheiro Olá seguinte Olá, em seguida, guarde as alterações.

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


## <a name="connect-hello-services"></a>Ligar a serviços Olá
Neste passo seguinte, iremos ligar Olá dois serviços e tornar Olá Web front-end de aplicação get e set votar informações a partir do serviço de back-end Olá.

O Service Fabric fornece flexibilidade concluída na como comunicar com serviços fiáveis. Dentro de uma única aplicação, poderá ter serviços que estão acessíveis através de TCP. Outros serviços que podem estar acessíveis através de uma API de REST de HTTP e ainda outros serviços poderia ficar acessíveis através de web sockets. Para em segundo plano nas opções de Olá disponíveis e fala Olá envolvidas, consulte [comunicar com serviços](service-fabric-connect-and-communicate-with-services.md).

Neste tutorial, estamos a utilizar [Web API do ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Atualizar Olá VotesController.cs ficheiro
No Olá **VotingWeb** projeto, abra Olá *Controllers/VotesController.cs* ficheiro.  Substitua Olá `VotesController` classe conteúdo de definição com a seguinte Olá, em seguida, guarde as alterações.

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

## <a name="walk-through-hello-voting-sample-application"></a>Percorrer Olá votar na aplicação de exemplo
Olá voto a aplicação é composta por dois serviços:
- Serviço de front-end (VotingWeb) Web - web de ASP.NET Core um serviço front-end, o que funciona a página web de Olá e expõe web toocommunicate APIs com o serviço de back-end Olá.
- O serviço de back-end (VotingData)-o serviço de web de uma ASP.NET Core, que expõe um voto de Olá toostore API resulta num dictionary fiável persistentes no disco.

![Diagrama de aplicação](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Quando votar em Olá de aplicação Olá os seguintes eventos ocorrem:
1. Um JavaScript envia Olá voto pedido toohello API web no serviço de front-end Olá web como um pedido HTTP PUT.

2. serviço de front-end Olá web utiliza um toolocate de proxy e reencaminhar o serviço de back-end um toohello de pedido HTTP PUT.

3. serviço de back-end Olá demora pedido recebido Olá e arquivos Olá atualizado resultado um dicionário fiável, que obtém toomultiple replicadas nós num cluster de Olá e persistentes no disco. Dados de todas as aplicações de Olá são armazenados no cluster de Olá, pelo que não é necessária nenhuma base de dados.

## <a name="debug-in-visual-studio"></a>Depuração no Visual Studio
Quando a depuração de aplicações no Visual Studio, está a utilizar um cluster de desenvolvimento do Service Fabric local. Ter Olá opção tooadjust seu cenário de tooyour de experiência de depuração. Nesta aplicação, podemos armazenar dados no nosso serviço de back-end, utilizando um dicionário fiável. Visual Studio remove aplicação Olá por predefinição, quando parar o depurador Olá. Remover aplicação Olá faz com que dados Olá no back-end de Olá serviço tooalso removidos. dados de Olá toopersist entre sessões de depuração, pode alterar Olá **modo de depuração da aplicação** como uma propriedade no Olá **voto** projeto no Visual Studio.

toolook, o que acontece no código Olá, Olá concluir os seguintes passos:
1. Abra Olá **VotesController.cs** de ficheiros e defina um ponto de interrupção no Olá API web do **colocar** método (linha 47) - pode procurar ficheiro Olá Olá Explorador de soluções no Visual Studio.

2. Abra Olá **VoteDataController.cs** de ficheiros e defina um ponto de interrupção da API web **colocar** método (50 de linha).

3. Voltar atrás toohello browser e clique numa opção de voto ou adicionar uma nova opção de voto. Atingiu o Olá primeiro ponto de interrupção do controlador da api do Olá frente-end da web.
    
    1. Este é onde Olá JavaScript no browser Olá envia um controlador de API do pedido toohello web no serviço de front-end Olá.
    
    ![Adicionar serviço de front-end de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Primeiro vamos construir Olá URL toohello ReverseProxy para o nosso serviço de back-end **(1)**.
    3. Em seguida, iremos enviar Olá HTTP PUT pedido toohello ReverseProxy **(2)**.
    4. Por fim Olá, Devolvemos resposta Olá do cliente de toohello do serviço de back-end Olá **(3)**.

4. Prima **F5** toocontinue
    1. Está agora no ponto de interrupção de Olá no serviço de back-end Olá.
    
    ![Adicionar serviço de Back-End de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. Na linha de primeiro Olá no método Olá **(1)** estamos a utilizar Olá `StateManager` tooget ou adicionar um dicionário fiável chamado `counts`.
    3. Todas as interações com valores num dictionary fiável necessitam de uma transação, esta utilizando instrução **(2)** cria esse transação.
    4. Transação Olá, vamos, em seguida, atualizar valor Olá chave relevantes do Olá para Olá votar na opção e consolidações Olá operação **(3)**. Após a consolidação de Olá método devolve, Olá dados são atualizados no dicionário de Olá e replicados tooother nós num cluster de Olá. dados de Olá estão agora armazenados em segurança num cluster de Olá e serviço de back-end Olá pode efetuar a ativação pós-falha tooother nós, continua a ter dados Olá disponíveis.
5. Prima **F5** toocontinue

Olá toostop sessão, prima de depuração **Shift + F5**.


## <a name="next-steps"></a>Passos seguintes
Nesta parte do tutorial Olá, aprendeu como:

> [!div class="checklist"]
> * Criar um serviço de API Web do ASP.NET Core como um serviço fiável com monitorização de estado
> * Criar um serviço de aplicação Web do ASP.NET Core como um serviço web sem monitorização de estado
> * Utilizar Olá proxy inverso toocommunicate com o serviço com estado Olá

Avançadas toohello próximo tutorial:
> [!div class="nextstepaction"]
> [Implementar Olá tooAzure de aplicação](service-fabric-tutorial-deploy-app-to-party-cluster.md)
