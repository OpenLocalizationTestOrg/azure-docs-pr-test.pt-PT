---
title: "aaaBuild uma aplicação ASP.NET no Azure com a base de dados SQL | Microsoft Docs"
description: "Saiba como tooget um ASP.NET aplicação a funcionar no Azure, com tooa de ligação da base de dados do SQL Server."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Criar uma aplicação ASP.NET no Azure com a base de dados SQL

[As Aplicações Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática. Este tutorial mostra como toodeploy um ASP.NET condicionada por dados web de aplicação no Azure e ligá-lo demasiado[SQL Database do Azure](../sql-database/sql-database-technical-overview.md). Quando tiver terminado, tem uma aplicação ASP.NET em execução no [App Service do Azure](../app-service/app-service-value-prop-what-is.md) e ligado tooSQL da base de dados.

![Aplicação de ASP.NET publicada na aplicação web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Criar uma base de dados do SQL Server no Azure
> * Ligar um tooSQL de aplicação do ASP.NET da base de dados
> * Implementar Olá tooAzure de aplicação
> * Atualizar o modelo de dados de Olá e volte a implementar a aplicação de Olá
> * Transmitir os registos do Azure tooyour terminal
> * Gerir a aplicação Olá no Olá portal do Azure

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial:

* Instalar [Visual Studio 2017](https://www.visualstudio.com/downloads/) com Olá seguintes cargas de trabalho:
  - **Desenvolvimento do ASP.NET e Web**
  - **Desenvolvimento do Azure**

  ![Desenvolvimento do ASP.NET e Web e desenvolvimento do Azure (na Web e na nuvem)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Transferir o exemplo de Olá

[Transferir o projeto de exemplo de Olá](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Extrair (deszipe) Olá *dotnet-sqldb-tutorial-master.zip* ficheiro.

projeto de exemplo de Olá contém num nível básico [ASP.NET MVC](https://www.asp.net/mvc) CRUD (criar-leitura-atualizar-eliminar) utilizando a aplicação [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Executar a aplicação Olá

Abra Olá *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* ficheiro no Visual Studio. 

Tipo `Ctrl+F5` toorun Olá aplicação sem a depuração. aplicação Olá é apresentada no seu browser predefinido. Selecione Olá **criar novo** ligar e criar alguns *tarefas* itens. 

![Caixa de diálogo Novo Projeto ASP.NET](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Olá teste **editar**, **detalhes**, e **eliminar** ligações.

aplicação Olá utiliza um tooconnect de contexto de base de dados com base de dados de Olá. Neste exemplo, o contexto de base de dados de Olá utiliza uma cadeia de ligação com o nome `MyDbConnection`. a cadeia de ligação Olá está definida no Olá *Web. config* de ficheiros e Olá referenciada na *Models/MyDatabaseContext.cs* ficheiro. nome de cadeia de ligação de Olá é utilizado mais tarde na Olá tutorial tooconnect Olá web do Azure aplicação tooan SQL Database do Azure. 

## <a name="publish-tooazure-with-sql-database"></a>Publicar tooAzure com base de dados SQL

No Olá **Explorador de soluções**, clique com botão direito do **DotNetAppSqlDb** projeto e selecione **publicar**.

![Publicar a partir do Explorador de Soluções](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

Certifique-se de que o **Serviço de Aplicações do Microsoft Azure** está selecionado e clique em **Publicar**.

![Publicar a partir da página de descrição geral do projeto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Publicação abre Olá **criar App Service** caixa de diálogo, Olá, que ajuda a criar todos os recursos do Azure, terá de toorun a aplicação web do ASP.NET no Azure.

### <a name="sign-in-tooazure"></a>Inicie sessão no tooAzure

No Olá **criar App Service** caixa de diálogo, clique em **adicionar uma conta**e, em seguida, inicie sessão tooyour subscrição do Azure. Se já tiver sessão iniciada numa conta Microsoft, confirme que esta inclui a sua subscrição do Azure. Se Olá com sessão iniciada conta Microsoft não tem a sua subscrição do Azure, clique no mesmo tooadd Olá correta da conta.
   
![Inicie sessão no tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

Depois de iniciar sessão, está pronto toocreate que Olá todos os recursos que necessários para a sua aplicação web do Azure nesta caixa de diálogo.

### <a name="configure-hello-web-app-name"></a>Configurar o nome da aplicação Olá web

Pode manter o nome da aplicação web Olá gerado ou alterá-la tooanother exclusivo (carateres válidos são `a-z`, `0-9`, e `-`). nome da aplicação Olá web é utilizado como parte do URL do Olá predefinido para a sua aplicação (`<app_name>.azurewebsites.net`, onde `<app_name>` é o nome da aplicação web). nome da aplicação web Olá tem toobe exclusivo em todas as aplicações no Azure. 

![Criar caixa de diálogo do app service](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Seguinte demasiado**grupo de recursos**, clique em **novo**.

![TooResource seguinte grupo, clique em novo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Grupo de recursos do nome Olá **myResourceGroup**.

> [!NOTE]
> Não clique em **criar**. Terá primeiro de tooset segurança uma base de dados do SQL Server num passo posterior.

### <a name="create-an-app-service-plan"></a>Crie um plano do Serviço de Aplicações

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Seguinte demasiado**plano do App Service**, clique em **novo**. 

No Olá **configurar plano do App Service** caixa de diálogo, configurar o plano de serviço aplicacional novo Olá com Olá seguintes definições:

![Criar plano do App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Definição  | Valor sugerido | Para obter mais informações |
| ----------------- | ------------ | ----|
|**Plano do App Service**| myAppServicePlan | [Planos do Serviço de Aplicações](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Localização**| Europa Ocidental | [Regiões do Azure](https://azure.microsoft.com/regions/) |
|**Tamanho**| Gratuito | [Escalões de preço](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>Criar uma instância do SQL Server

Antes de criar uma base de dados, é necessário um [servidor lógico da SQL Database do Azure](../sql-database/sql-database-features.md). Um servidor lógico contém um grupo de bases de dados geridas como um grupo.

Selecione **explorar serviços Azure adicionais**.

![Configurar o nome da aplicação Web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

No Olá **serviços** separador, clique em Olá  **+**  ícone seguinte demasiado**base de dados SQL**. 

![No separador de serviços de Olá, clique em Olá + ícone tooSQL seguinte base de dados.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

No Olá **configurar a base de dados do SQL** caixa de diálogo, clique em **novo** seguinte demasiado**do SQL Server**. 

É gerado um nome de servidor único. Este nome é utilizado como parte do URL do Olá predefinido para o servidor lógico, `<server_name>.database.windows.net`. Tem de ser exclusivo em todas as instâncias de servidor lógico no Azure. Pode alterar o nome do servidor Olá, mas para este tutorial, mantenha o valor de Olá gerado.

Adicionar um nome de utilizador administrador e a palavra-passe e, em seguida, selecione **OK**. Para requisitos de complexidade de palavra-passe, consulte [política de palavra-passe](/sql/relational-databases/security/password-policy).

Lembre-se de que este nome de utilizador e palavra-passe. Tem servidor lógico de Olá toomanage instância mais tarde.

![Criar a instância do SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>Criar uma Base de Dados SQL

No Olá **configurar a base de dados do SQL** diálogo: 

* Manter as predefinições de Olá gerada **nome de base de dados**.
* No **nome da cadeia de ligação**, tipo *MyDbConnection*. Este nome tem de corresponder à cadeia de ligação de Olá é referenciada em *Models/MyDatabaseContext.cs*.
* Selecione **OK**.

![Configurar a base de dados SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Olá **criar App Service** recursos Olá de mostra a caixa de diálogo que criou. Clique em **Criar**. 

![recursos de Olá criou](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Depois do Assistente de Olá acaba de criar Olá recursos do Azure, publica a tooAzure de aplicação do ASP.NET. O browser predefinido é iniciado com Olá URL toohello implementado aplicação. 

Adicione alguns itens de tarefas.

![Aplicação de ASP.NET publicada na aplicação web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Parabéns! A aplicação de ASP.NET condicionada por dados está em execução no App Service do Azure.

## <a name="access-hello-sql-database-locally"></a>Acesso Olá base de dados SQL localmente

Visual Studio permite-lhe explorar e gerir a sua nova base de dados do SQL Server facilmente no Olá **SQL Server Object Explorer**.

### <a name="create-a-database-connection"></a>Criar uma ligação de base de dados

De Olá **vista** menu, selecione **SQL Server Object Explorer**.

Na parte superior de Olá de **SQL Server Object Explorer**, clique em Olá **adicionar SQL Server** botão.

### <a name="configure-hello-database-connection"></a>Configurar a ligação de base de dados de Olá

No Olá **Connect** caixa de diálogo, expanda Olá **Azure** nós. Todas as instâncias de base de dados SQL no Azure estão listadas aqui.

Selecione Olá `DotNetAppSqlDb` base de dados SQL. ligação de Olá que criou anteriormente é preenchida automaticamente na parte inferior de Olá.

Escreva a palavra-passe Olá da base de dados administrador que criou anteriormente e clique em **Connect**.

![Configure a ligação de base de dados do Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>Permitir a ligação de cliente do computador

Olá **criar uma nova regra de firewall** abrir a caixa de diálogo. Por predefinição, a instância de base de dados SQL só permite ligações a partir de serviços do Azure, tais como a sua aplicação web do Azure. tooconnect tooyour da base de dados, crie uma regra de firewall na instância de base de dados SQL Olá. regra de firewall de Olá permite que o endereço IP público Olá do computador local.

caixa de diálogo Olá já é preenchida com endereço IP público do seu computador.

Certifique-se de que **Adicionar IP do cliente** está selecionada e clique em **OK**. 

![Configurar a firewall para a instância de base de dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Depois do Visual Studio acaba de criar a definição da firewall Olá para a instância de base de dados do SQL Server, a ligação que aparecem no **SQL Server Object Explorer**.

Aqui, pode realizar Olá mais comuns da base de dados operações, tais como executadas consultas, criar vistas e procedimentos armazenados e muito mais. 

Clique com o botão direito no Olá `Todoes` tabela e selecione **ver dados**. 

![Explorar os objetos de base de dados SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Atualizar a aplicação com código de migrações primeiro

Pode utilizar ferramentas familiares do Olá no Visual Studio tooupdate a base de dados e a aplicação web no Azure. Neste passo, utilize migrações primeiro código do Entity Framework toomake um esquema de base de dados de tooyour de alteração e publicá-lo tooAzure.

Para obter mais informações sobre como utilizar o Entity Framework Code primeiro migrações, consulte [introdução Entity Framework 6 Code First utilizando MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="update-your-data-model"></a>Atualizar o modelo de dados

Abra _Models\Todo.cs_ num editor de código Olá. Adicionar Olá seguinte propriedade toohello `ToDo` classe:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Execute migrações primeiro código localmente

Execute alguns comandos toomake atualizações tooyour local da base de dados. 

De Olá **ferramentas** menu, clique em **Gestor de pacotes NuGet** > **consola do Gestor de pacotes**.

Na janela consola do Gestor de pacote Olá, ative migrações primeiro código:

```PowerShell
Enable-Migrations
```

Adicione uma migração:

```PowerShell
Add-Migration AddProperty
```

Atualize a base de dados local Olá:

```PowerShell
Update-Database
```

Tipo `Ctrl+F5` toorun Olá aplicação. Olá teste editar detalhes e criar ligações.

Se a aplicação Olá carrega sem erros, em seguida, migrações primeiro código foi bem sucedida. No entanto, a procura de ainda página Olá mesmo porque a lógica de aplicação não está a utilizar esta propriedade novo com ainda. 

### <a name="use-hello-new-property"></a>Utilize a nova propriedade de Olá

Faça algumas alterações no seu Olá de toouse código `Done` propriedade. De simplicidade neste tutorial, que só vai toochange Olá `Index` e `Create` vistas propriedade de Olá toosee em ação.

Abra _Controllers\TodosController.cs_.

Determinar Olá `Create()` método e adicione `Done` toohello lista de propriedades no Olá `Bind` atributo. Quando tiver terminado, a `Create()` assinatura do método aspeto Olá seguinte código:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Abra _Views\Todos\Create.cshtml_.

No código Razor Olá, deverá ver uma `<div class="form-group">` elemento que utiliza `model.Description`e, em seguida, outra `<div class="form-group">` elemento que utiliza `model.CreatedDate`. Imediatamente a seguir estes dois elementos, adicione outro `<div class="form-group">` elemento que utiliza `model.Done`:

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Abra _Views\Todos\Index.cshtml_.

Procure Olá vazio `<th></th>` elemento. Apenas acima este elemento, adicione Olá código Razor os seguintes:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Determinar Olá `<td>` elemento que contenha Olá `Html.ActionLink()` métodos de programa auxiliar. Apenas acima este elemento, adicione Olá código Razor os seguintes:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

É tudo o que precisa toosee alterações Olá Olá `Index` e `Create` vistas. 

Tipo `Ctrl+F5` toorun Olá aplicação.

Agora pode adicionar um item de tarefas e verifique **feito**. Em seguida, deve agora mostrar cópias de segurança na sua home page como um item concluído. Lembre-se de que Olá `Edit` vista não mostra Olá `Done` campo, porque não foi alterado Olá `Edit` vista.

### <a name="enable-code-first-migrations-in-azure"></a>Ativar migrações primeiro do código no Azure

Agora que o seu código alterar funciona, incluindo a migração de base de dados, publicá-lo tooyour aplicação de web do Azure e atualizar a base de dados do SQL Server com o código de migrações primeiro demasiado.

Tal como anteriormente, clique no seu projeto e selecione **publicar**.

Clique em **definições** tooopen Olá publicar assistente.

![Definições de publicação aberta](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

No Assistente de Olá, clique em **seguinte**.

Certifique-se essa cadeia de ligação Olá para a base de dados SQL é preenchida no **MyDatabaseContext (MyDbConnection)**. Poderá ser necessário tooselect Olá **myToDoAppDb** base de dados da lista pendente de Olá. 

Selecione **executar código primeiro migrações (em execução no início da aplicação)**, em seguida, clique em **guardar**.

![Ativar migrações primeiro código na aplicação web do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Publicar as suas alterações

Agora que ativou migrações primeiro código na sua aplicação web do Azure, publique as suas alterações de código.

No Olá publicar página, clique em **publicar**.

Tente novamente adicionar itens de tarefas e selecione **feito**, e estes deverão aparecer na sua home page como um item concluído.

![Aplicação web do Azure após a migração primeiro código](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Todos os seus itens de tarefas existentes ainda são apresentados. Quando voltar a publicar a aplicação ASP.NET, os dados existentes na sua base de dados do SQL Server não são perdidos. Além disso, migrações primeiro código apenas alterações de esquema de dados de Olá e mantém os dados existentes intactas.


## <a name="stream-application-logs"></a>Registos de aplicações de fluxo

Pode transmitir mensagens de rastreio diretamente a partir do seu tooVisual de aplicação web do Azure Studio.

Abra _Controllers\TodosController.cs_.

Cada ação começa com um `Trace.WriteLine()` método. Este código é adicionado tooshow, como o rastreio tooadd mensagens tooyour aplicação de web do Azure.

### <a name="open-server-explorer"></a>Explorador de servidores aberta

De Olá **vista** menu, selecione **Explorador de servidores**. Pode configurar o registo para a sua aplicação web do Azure no **Explorador de servidores**. 

### <a name="enable-log-streaming"></a>Ativar o registo de transmissão em fluxo

No **Explorador de servidores**, expanda **Azure** > **do serviço de aplicações**.

Expanda Olá **myResourceGroup** grupo de recursos que criou quando criou Olá aplicação de web do Azure.

A aplicação web do Azure com o botão direito e selecione **ver registos de transmissão em fluxo**.

![Ativar o registo de transmissão em fluxo](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Olá registos são agora transmissão em fluxo em Olá **saída** janela. 

![Registo de transmissão em fluxo numa janela de saída](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

No entanto, não vir qualquer uma das mensagens hello do rastreio ainda. Da porque quando primeiro selecione **ver registos de transmissão em fluxo**, a aplicação web do Azure define o nível de rastreio de Olá demasiado`Error`, que apenas os registos de eventos de erro (com Olá `Trace.TraceError()` método).

### <a name="change-trace-levels"></a>Níveis de rastreio de alterações

rastreio de Olá toochange níveis toooutput outras mensagens de rastreio, acedas novamente demasiado**Explorador de servidores**.

Faça duplo clique novamente a aplicação web do Azure e selecione **definições**.

No Olá **registo na aplicação (sistema de ficheiros)** lista pendente, selecione **verboso**. Clique em **Guardar**.

![Alterar tooVerbose de nível de rastreio](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> Pode experimentar a toosee de níveis de rastreio de diferentes tipos de mensagens são apresentados para cada nível. Por exemplo, Olá **informações** nível inclui todos os registos criados pela `Trace.TraceInformation()`, `Trace.TraceWarning()`, e `Trace.TraceError()`, mas não os registos criados pela `Trace.WriteLine()`.
>
>

No seu browser, tente clicar em torno da aplicação de lista de tarefas Olá no Azure. mensagens Hello do rastreio estão agora transmissão em fluxo toohello **saída** janela no Visual Studio.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Parar o registo de transmissão em fluxo

toostop Olá o serviço de registo para transmissão em fluxo, clique em Olá **parar a monitorização** botão no Olá **saída** janela.

![Parar o registo de transmissão em fluxo](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Gerir a sua aplicação web do Azure

Aceda toohello [portal do Azure](https://portal.azure.com) toosee Olá web aplicação que criou. 



No menu à esquerda Olá, clique em **do serviço de aplicações**, em seguida, clique no nome de Olá da sua aplicação web do Azure.

![Aplicação de web de tooAzure de navegação do portal](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

Atingiu na página da aplicação web. 

Por predefinição, o portal de Olá mostra Olá **descrição geral** página. Esta página proporciona-lhe uma vista do desempenho da aplicação. Aqui, também pode realizar tarefas de gestão básicas, como navegar, parar, iniciar, reiniciar e eliminar. separadores Olá no lado esquerdo do Olá da página Olá mostram páginas de configuração diferente Olá que pode abrir. 

![Página Serviço de Aplicações no portal do Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Criar uma base de dados do SQL Server no Azure
> * Ligar um tooSQL de aplicação do ASP.NET da base de dados
> * Implementar Olá tooAzure de aplicação
> * Atualizar o modelo de dados de Olá e volte a implementar a aplicação de Olá
> * Transmitir os registos do Azure tooyour terminal
> * Gerir a aplicação Olá no Olá portal do Azure

Avançar toohello toolearn de tutorial seguinte como toomap um DNS personalizado nome toohello web app.

> [!div class="nextstepaction"]
> [Mapear um existente personalizado DNS nome tooAzure aplicações Web](app-service-web-tutorial-custom-domain.md)
