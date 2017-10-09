---
title: aaaCreate uma API de REST no Azure com o ASP.NET e a base de dados SQL | Microsoft Docs
description: "Um tutorial que informa-como toodeploy uma aplicação que utiliza Olá API Web do ASP.NET tooan aplicação web do Azure utilizando o Visual Studio."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="87f50-103">Criar um serviço REST utilizando a API Web do ASP.NET e a SQL Database no App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="87f50-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="87f50-104">Este tutorial mostra como toodeploy um ASP.NET web app tooan [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) utilizando o Assistente para publicar Web Olá no Visual Studio 2013 ou Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="87f50-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="87f50-105">Pode criar uma conta do Azure gratuitamente e, se ainda não tiver o Visual Studio 2013, Olá SDK instala automaticamente o Visual Studio 2013 Express Web.</span><span class="sxs-lookup"><span data-stu-id="87f50-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="87f50-106">Por isso, pode começar a desenvolver para o Azure inteiramente para gratuita.</span><span class="sxs-lookup"><span data-stu-id="87f50-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="87f50-107">Este tutorial parte do princípio de que tem qualquer experiência na utilização do Azure.</span><span class="sxs-lookup"><span data-stu-id="87f50-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="87f50-108">Concluir neste tutorial, terá uma aplicação web simples cópias de segurança e em execução na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="87f50-109">Irá aprender:</span><span class="sxs-lookup"><span data-stu-id="87f50-109">You'll learn:</span></span>

* <span data-ttu-id="87f50-110">Como tooenable Olá, o computador para a programação do Azure instalando o Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="87f50-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="87f50-111">Como toocreate um Visual Studio ASP.NET MVC 5 do projeto e publicá-lo tooan aplicações do Azure.</span><span class="sxs-lookup"><span data-stu-id="87f50-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="87f50-112">Como toouse Olá API Web do ASP.NET tooenable chama a Restful API.</span><span class="sxs-lookup"><span data-stu-id="87f50-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="87f50-113">Como toouse SQL da base de dados de toostore no Azure.</span><span class="sxs-lookup"><span data-stu-id="87f50-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="87f50-114">Como aplicação toopublish atualizações tooAzure.</span><span class="sxs-lookup"><span data-stu-id="87f50-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="87f50-115">Irá criar uma aplicação de web de lista de contactos simples que está incorporada no ASP.NET MVC 5 e utiliza hello do ADO.NET Entity Framework para acesso de base de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="87f50-116">Olá seguinte ilustração mostra Olá concluída aplicação:</span><span class="sxs-lookup"><span data-stu-id="87f50-116">hello following illustration shows hello completed application:</span></span>

![captura de ecrã do web site][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="87f50-118">Criar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="87f50-118">Create hello project</span></span>
1. <span data-ttu-id="87f50-119">Inicie o Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="87f50-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="87f50-120">De Olá **ficheiro** menu clique **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="87f50-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="87f50-121">No Olá **novo projeto** diálogo caixa, expanda **Visual c#** e selecione **Web** e, em seguida, selecione **aplicação Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="87f50-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="87f50-122">Nome da aplicação Olá **ContactManager** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="87f50-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Caixa de diálogo Novo Projeto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="87f50-124">No Olá **novo projeto ASP.NET** caixa de diálogo, selecione de Olá **MVC** modelo, verificação **Web API** e, em seguida, clique em **alterar autenticação**.</span><span class="sxs-lookup"><span data-stu-id="87f50-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="87f50-125">No Olá **alterar autenticação** caixa de diálogo, clique em **sem autenticação**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="87f50-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Sem Autenticação](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="87f50-127">aplicação de exemplo de Olá que está a criar não terá de funcionalidades que requerem toolog de utilizadores no.</span><span class="sxs-lookup"><span data-stu-id="87f50-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="87f50-128">Para obter informações sobre como tooimplement funcionalidades de autenticação e autorização, consulte Olá [passos](#nextsteps) secção no final deste tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="87f50-129">No Olá **novo projeto ASP.NET** caixa de diálogo, Olá se disponibilizar **anfitrião na nuvem de Olá** está selecionada e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="87f50-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="87f50-130">Se não tiver no tooAzure, será pedido toosign no.</span><span class="sxs-lookup"><span data-stu-id="87f50-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="87f50-131">Assistente de configuração de Olá será sugerir um nome exclusivo com base no *ContactManager* (ver a imagem de Olá abaixo).</span><span class="sxs-lookup"><span data-stu-id="87f50-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="87f50-132">Selecione uma região perto de si.</span><span class="sxs-lookup"><span data-stu-id="87f50-132">Select a region near you.</span></span> <span data-ttu-id="87f50-133">Pode utilizar [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind Olá menor latência de centro de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="87f50-134">Se ainda não criou um servidor de base de dados antes, selecione **criar novo servidor**, introduza um nome de utilizador de base de dados e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="87f50-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configurar Web site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="87f50-136">Se tiver um servidor de base de dados, utilize essa toocreate uma nova base de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="87f50-137">Servidores de base de dados são um recurso precioso e geralmente pretender toocreate várias bases de dados no Olá mesmo servidor de teste e desenvolvimento em vez de criar um servidor de base de dados por base de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="87f50-138">Certifique-se o web site e a base de dados Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="87f50-138">Make sure your web site and database are in hello same region.</span></span>

![Configurar Web site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="87f50-140">Definir Olá cabeçalho e rodapé</span><span class="sxs-lookup"><span data-stu-id="87f50-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="87f50-141">No **Explorador de soluções**, expanda Olá *Views\Shared* pasta e abra Olá *layout* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="87f50-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![Layout no Explorador de soluções][newapp004]
2. <span data-ttu-id="87f50-143">Substituir conteúdo Olá Olá *Views\Shared_Layout.cshtml* ficheiro com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="87f50-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="87f50-144">marcação Olá acima nome da aplicação Olá alterações da "Aplicação ASP.NET My" demasiado "Contacte Manager" e remove ligações Olá demasiado**home page**, **sobre** e **contacte**.</span><span class="sxs-lookup"><span data-stu-id="87f50-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="87f50-145">Executar a aplicação Olá localmente</span><span class="sxs-lookup"><span data-stu-id="87f50-145">Run hello application locally</span></span>
1. <span data-ttu-id="87f50-146">Prima a aplicação de Olá toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="87f50-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="87f50-147">home page da aplicação Olá é apresentada no browser predefinido de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="87f50-148">![home page da lista tooDo](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="87f50-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="87f50-149">Isto é tudo o que precisa toodo para aplicação de Olá agora toocreate que vai implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="87f50-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="87f50-150">Mais tarde, irá adicionar a funcionalidade de base de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="87f50-151">Implementar Olá tooAzure de aplicação</span><span class="sxs-lookup"><span data-stu-id="87f50-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="87f50-152">No Visual Studio, clique no projeto Olá no **Explorador de soluções** e selecione **publicar** no menu de contexto de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![Publicar no menu de contexto do projeto][PublishVSSolution]
   
    <span data-ttu-id="87f50-154">Olá **publicar Web** é aberto o assistente.</span><span class="sxs-lookup"><span data-stu-id="87f50-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="87f50-155">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-155">Click **Publish**.</span></span>

![Separador Definições](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="87f50-157">Visual Studio inicia o processo de Olá de copiar ficheiros de Olá toohello servidor do Azure.</span><span class="sxs-lookup"><span data-stu-id="87f50-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="87f50-158">Olá **saída** janela mostra que ações de implementação foram executadas e reporta a conclusão com êxito da implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="87f50-159">browser predefinido de Olá abre automaticamente toohello URL do site de Olá implementado.</span><span class="sxs-lookup"><span data-stu-id="87f50-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="87f50-160">aplicação Olá que criou está agora em execução na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-160">hello application you created is now running in hello cloud.</span></span>
   
   ![tooDo lista home page em execução no Azure][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="87f50-162">Adicionar uma aplicação de toohello de base de dados</span><span class="sxs-lookup"><span data-stu-id="87f50-162">Add a database toohello application</span></span>
<span data-ttu-id="87f50-163">Em seguida, irá atualizar Olá MVC aplicação tooadd Olá capacidade toodisplay e atualizar os contactos e armazenar dados de Olá numa base de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="87f50-164">aplicação Olá irá utilizar a base de dados do Olá do Entity Framework toocreate Olá e tooread e atualizar os dados na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="87f50-165">Adicionar classes de modelo de dados dos contactos de Olá</span><span class="sxs-lookup"><span data-stu-id="87f50-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="87f50-166">Comece por criar um modelo de dados simples no código.</span><span class="sxs-lookup"><span data-stu-id="87f50-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="87f50-167">No **Explorador de soluções**, faça duplo clique Olá modelos pasta, clique em **adicionar**e, em seguida, **classe**.</span><span class="sxs-lookup"><span data-stu-id="87f50-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Adicionar classe no menu de contexto de pasta de modelos][adddb001]
2. <span data-ttu-id="87f50-169">No Olá **Adicionar Novo Item** caixa de diálogo, nome Olá novo classe ficheiro *Contact.cs*e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Adicionar Novo Item caixa de diálogo][adddb002]
3. <span data-ttu-id="87f50-171">Substitua Olá conteúdo de Olá Contacts.cs ficheiro Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="87f50-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="87f50-172">Olá **contacte** classe define dados Olá que irá armazenar para cada contacte plus uma chave primária, ContactID, que é necessário para a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="87f50-173">Pode obter mais informações sobre modelos de dados no Olá [passos](#nextsteps) secção no final deste tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="87f50-174">Criar páginas web que ativar a aplicação aos utilizadores toowork com contactos Olá</span><span class="sxs-lookup"><span data-stu-id="87f50-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="87f50-175">Olá funcionalidade do ASP.NET MVC Olá andaime pode gerar automaticamente o código que executa a criar, ler, atualizar e eliminar ações (CRUD).</span><span class="sxs-lookup"><span data-stu-id="87f50-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="87f50-176">Adicionar um controlador e uma vista de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="87f50-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="87f50-177">No **Explorador de soluções**, expanda a pasta de controladores Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="87f50-178">Compilar o projeto de Olá **(Ctrl + Shift + B)**.</span><span class="sxs-lookup"><span data-stu-id="87f50-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="87f50-179">(Tem de criar o projeto de Olá antes de utilizar o mecanismo de andaime.)</span><span class="sxs-lookup"><span data-stu-id="87f50-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="87f50-180">Faça duplo clique Olá controladores pasta e clique em **adicionar**e, em seguida, clique em **controlador**.</span><span class="sxs-lookup"><span data-stu-id="87f50-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Adicionar controlador no menu de contexto de pasta de controladores][addcode001]
4. <span data-ttu-id="87f50-182">No Olá **adicionar andaime** caixa de diálogo, selecione **controlador MVC com vistas, utilizando o Entity Framework** e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Adicionar o controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="87f50-184">Definir o nome do controlador de Olá demasiado**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="87f50-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="87f50-185">Selecione **contacte** como a classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="87f50-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="87f50-186">Clique em Olá **contexto de dados nova** botão e aceite a predefinição de Olá "ContactManager.Models.ContactManagerContext" para Olá **novo tipo de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="87f50-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="87f50-187">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-187">Click **Add**.</span></span>

    <span data-ttu-id="87f50-188">Uma caixa de diálogo irá solicitar-lhe: "um ficheiro com nome Olá HomeController já existe.</span><span class="sxs-lookup"><span data-stu-id="87f50-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="87f50-189">Pretende tooreplace-? ".</span><span class="sxs-lookup"><span data-stu-id="87f50-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="87f50-190">Clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="87f50-190">Click **Yes**.</span></span> <span data-ttu-id="87f50-191">Estamos a substituição Olá home page controlador que foi criada com o novo projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="87f50-192">Utilizaremos Olá novo home page controlador para a nossa lista de contactos.</span><span class="sxs-lookup"><span data-stu-id="87f50-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="87f50-193">Métodos de controlador e vistas para operações CRUD de base de dados para o Visual Studio cria **contacte** objetos.</span><span class="sxs-lookup"><span data-stu-id="87f50-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="87f50-194">Ativar migrações, crie a base de dados de Olá, adicionar dados de exemplo e um inicializador de dados</span><span class="sxs-lookup"><span data-stu-id="87f50-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="87f50-195">a tarefa seguinte Olá está tooenable Olá [migrações primeiro código](http://curah.microsoft.com/55220) funcionalidade na ordem toocreate Olá da base de dados baseada no modelo de dados de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="87f50-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="87f50-196">No Olá **ferramentas** menu, selecione **Gestor de pacotes de biblioteca** e, em seguida, **consola do Gestor de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="87f50-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Consola do Gestor de pacotes no menu Ferramentas][addcode008]
2. <span data-ttu-id="87f50-198">No Olá **consola do Gestor de pacotes** janela, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="87f50-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="87f50-199">Olá **ativar migrações** comando cria um *migrações* pasta e coloca nessa pasta um *Configuration.cs* ficheiros que pode editar tooconfigure migrações.</span><span class="sxs-lookup"><span data-stu-id="87f50-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="87f50-200">No Olá **consola do Gestor de pacotes** janela, introduza Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="87f50-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="87f50-201">Olá **inicial da migração adicionar** comandos gera uma classe com o nome  **&lt;date_stamp&gt;inicial** que cria a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="87f50-202">Olá primeiro parâmetro ( *inicial* ) é arbitrário e utilizada toocreate Olá nome do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="87f50-203">Pode ver Olá nova classe ficheiros **Explorador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="87f50-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="87f50-204">No Olá **inicial** classe, hello **segurança** método cria a tabela de contactos de Olá e Olá **baixo** método (utilizado quando pretender que o estado anterior do tooreturn toohello) ignora-lo.</span><span class="sxs-lookup"><span data-stu-id="87f50-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="87f50-205">Abra Olá *Migrations\Configuration.cs* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="87f50-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="87f50-206">Adicione Olá seguintes espaços de nomes.</span><span class="sxs-lookup"><span data-stu-id="87f50-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="87f50-207">Substitua Olá *Seed* método com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="87f50-207">Replace hello *Seed* method with hello following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="87f50-208">Este código acima inicializará a base de dados de Olá com as informações de contacto Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="87f50-209">Para obter mais informações sobre a propagação de base de dados de Olá, consulte [bds de depuração do Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="87f50-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="87f50-210">No Olá **consola do Gestor de pacotes** introduza Olá comando:</span><span class="sxs-lookup"><span data-stu-id="87f50-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Comandos de consola do Gestor de pacotes][addcode009]
   
    <span data-ttu-id="87f50-212">Olá **base de dados de atualização** executa Olá migração primeiro que cria Olá base de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="87f50-213">Por predefinição, a base de dados de Olá será criado como uma base de dados do SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="87f50-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="87f50-214">Prima a aplicação de Olá toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="87f50-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="87f50-215">aplicação Olá mostra os dados de seed Olá e fornece edição, detalhes e ligações de eliminação.</span><span class="sxs-lookup"><span data-stu-id="87f50-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![Vista MVC de dados][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="87f50-217">Editar Olá vista</span><span class="sxs-lookup"><span data-stu-id="87f50-217">Edit hello View</span></span>
1. <span data-ttu-id="87f50-218">Abra Olá *Views\Home\Index.cshtml* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="87f50-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="87f50-219">No próximo passo Olá, iremos irá substituir o markup Olá gerado com o código que utiliza [jQuery](http://jquery.com/) e [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="87f50-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="87f50-220">Este novo código obtém a lista de contactos de Olá de utilizar a web API e JSON e, em seguida, vincula Olá contacte dados toohello IU knockout.js a utilizar.</span><span class="sxs-lookup"><span data-stu-id="87f50-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="87f50-221">Para obter mais informações, consulte Olá [passos](#nextsteps) secção no final deste tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="87f50-222">Substitua conteúdo de Olá do ficheiro de Olá Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="87f50-222">Replace hello contents of hello file with hello following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="87f50-223">Pasta de conteúdo de Olá com o botão direito e clique em **adicionar**e, em seguida, clique em **Novo Item...** .</span><span class="sxs-lookup"><span data-stu-id="87f50-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Adicionar a folha de estilos no menu de contexto da pasta de conteúdo][addcode005]
4. <span data-ttu-id="87f50-225">No Olá **Adicionar Novo Item** caixa de diálogo, introduza **estilo** no Olá caixa de pesquisa direito superior e, em seguida, selecione **folha de estilos**.</span><span class="sxs-lookup"><span data-stu-id="87f50-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="87f50-226">![Adicionar Novo Item caixa de diálogo][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="87f50-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="87f50-227">Ficheiro de Olá nome *Contacts.css* e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="87f50-228">Substitua conteúdo de Olá do ficheiro de Olá Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="87f50-228">Replace hello contents of hello file with hello following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="87f50-229">Utilizaremos esta folha de estilo de esquema de Olá, cores e estilos utilizados na aplicação do Gestor de contacto Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="87f50-230">Abra Olá *App_Start\BundleConfig.cs* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="87f50-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="87f50-231">Adicionar Olá seguir Olá do código tooregister [Knockout](http://knockoutjs.com/index.html "KO") Plug-in.</span><span class="sxs-lookup"><span data-stu-id="87f50-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="87f50-232">Este exemplo com knockout toosimplify dinâmico código JavaScript que processa os modelos de ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="87f50-233">Modificar Olá do Olá conteúdo/css entrada tooregister *contacts.css* folha de estilos.</span><span class="sxs-lookup"><span data-stu-id="87f50-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="87f50-234">Alterar Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="87f50-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="87f50-235">Para:</span><span class="sxs-lookup"><span data-stu-id="87f50-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="87f50-236">Na consola do Gestor de pacotes Olá, execute Olá os seguintes comandos tooinstall Knockout.</span><span class="sxs-lookup"><span data-stu-id="87f50-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="87f50-237">Adicionar um controlador para a interface Web API Restful Olá</span><span class="sxs-lookup"><span data-stu-id="87f50-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="87f50-238">No **Explorador de soluções**, faça duplo clique controladores e clique em **adicionar** e, em seguida, **controlador...**</span><span class="sxs-lookup"><span data-stu-id="87f50-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="87f50-239">No Olá **adicionar andaime** caixa de diálogo, introduza **Web API 2 controlador com ações, utilizando o Entity Framework** e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Adicionar controlador da API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="87f50-241">No Olá **Adicionar controlador** caixa de diálogo, introduza "ContactsController" que o seu nome de controlador.</span><span class="sxs-lookup"><span data-stu-id="87f50-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="87f50-242">Selecione "Contacte (ContactManager.Models)" para Olá **classe de modelo**.</span><span class="sxs-lookup"><span data-stu-id="87f50-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="87f50-243">Manter o valor predefinido Olá Olá **classe de contexto de dados**.</span><span class="sxs-lookup"><span data-stu-id="87f50-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="87f50-244">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="87f50-245">Executar a aplicação Olá localmente</span><span class="sxs-lookup"><span data-stu-id="87f50-245">Run hello application locally</span></span>
1. <span data-ttu-id="87f50-246">Prima a aplicação de Olá toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="87f50-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![Página Índice][intro001]
2. <span data-ttu-id="87f50-248">Introduza um contacto e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="87f50-249">aplicação Olá devolve home page do toohello e apresenta contacte Olá que introduziu.</span><span class="sxs-lookup"><span data-stu-id="87f50-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Página de índice com itens de lista de tarefas][addwebapi004]
3. <span data-ttu-id="87f50-251">No browser Olá, acrescentar **/api/contactos** toohello URL.</span><span class="sxs-lookup"><span data-stu-id="87f50-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="87f50-252">URL de resultante Olá irá assemelhar-se http://localhost:1234/api/contactos.</span><span class="sxs-lookup"><span data-stu-id="87f50-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="87f50-253">Olá a API web RESTful adicionou devolve contactos Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="87f50-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="87f50-254">Firefox e o Chrome irão apresentar dados de Olá no formato XML.</span><span class="sxs-lookup"><span data-stu-id="87f50-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Página de índice com itens de lista de tarefas][rxFFchrome]

    <span data-ttu-id="87f50-256">I/e irá solicitar-lhe tooopen ou guardar Olá contactos.</span><span class="sxs-lookup"><span data-stu-id="87f50-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Caixa de diálogo de guardar API Web][addwebapi006]


    <span data-ttu-id="87f50-258">Pode abrir Olá devolvido contactos no bloco de notas ou um browser.</span><span class="sxs-lookup"><span data-stu-id="87f50-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="87f50-259">Este resultado pode ser utilizado por outra aplicação, tais como a aplicação ou página web móvel.</span><span class="sxs-lookup"><span data-stu-id="87f50-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Caixa de diálogo de guardar API Web][addwebapi007]

    <span data-ttu-id="87f50-261">**Aviso de segurança**: nesta fase, a aplicação é ataque tooCSRF inseguras e vulnerável.</span><span class="sxs-lookup"><span data-stu-id="87f50-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="87f50-262">Mais tarde no tutorial Olá vamos remover esta vulnerabilidade.</span><span class="sxs-lookup"><span data-stu-id="87f50-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="87f50-263">Para obter mais informações consulte [impedir entre sites pedido falsificação (CSRF) ataques][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="87f50-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="87f50-264">Adicionar proteção XSRF</span><span class="sxs-lookup"><span data-stu-id="87f50-264">Add XSRF Protection</span></span>
<span data-ttu-id="87f50-265">Falsificação de pedidos entre sites (também conhecido como XSRF ou CSRF) é um ataque contra aplicações web alojadas na qual um Web site malicioso pode influenciar a interação de Olá entre um browser do cliente e um site fidedigno para esse browser.</span><span class="sxs-lookup"><span data-stu-id="87f50-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="87f50-266">Estes ataques são efetuados possíveis porque web browsers envia os tokens de autenticação automaticamente com cada Web site tooa de pedido.</span><span class="sxs-lookup"><span data-stu-id="87f50-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="87f50-267">exemplo de canónico Olá é um cookie de autenticação, como ASP. Permissão de autenticação de formulários do NET.</span><span class="sxs-lookup"><span data-stu-id="87f50-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="87f50-268">No entanto, os Web sites que utilizam qualquer mecanismo de autenticação persistente (por exemplo, a autenticação do Windows, Basic e assim sucessivamente) podem ser segmentados por estes ataques.</span><span class="sxs-lookup"><span data-stu-id="87f50-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="87f50-269">Um ataque XSRF é diferente de um ataque de phishing.</span><span class="sxs-lookup"><span data-stu-id="87f50-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="87f50-270">Ataques de phishing requerem interação do vítima Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="87f50-271">Ataques de phishing, um Web site malicioso irão imitar o Web site de destino Olá e vítima Olá é fooled para fornecer o atacante toohello de informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="87f50-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="87f50-272">Num ataque XSRF, há muitas vezes, sem interação necessárias da vítima Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="87f50-273">Em vez disso, o atacante Olá é a entidade confiadora no browser Olá enviar automaticamente o site de destino de toohello do todos os cookies relevantes.</span><span class="sxs-lookup"><span data-stu-id="87f50-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="87f50-274">Para obter mais informações, consulte Olá [abrir projeto de segurança de aplicações Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="87f50-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="87f50-275">No **Explorador de soluções**, direita **ContactManager** projeto e clique em **adicionar** e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="87f50-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="87f50-276">Ficheiro de Olá nome *ValidateHttpAntiForgeryTokenAttribute.cs* e adicione Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="87f50-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="87f50-277">Adicione Olá seguinte *utilizando* instrução toohello contrai controlador, pelo que tem acesso toohello **[ValidateHttpAntiForgeryToken]** atributo.</span><span class="sxs-lookup"><span data-stu-id="87f50-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="87f50-278">Adicionar Olá **[ValidateHttpAntiForgeryToken]** atributo toohello métodos Post Olá **ContactsController** tooprotect-lo contra ameaças XSRF.</span><span class="sxs-lookup"><span data-stu-id="87f50-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="87f50-279">Irá adicioná-la toohello "PutContact", "PostContact" e **DeleteContact** métodos de ação.</span><span class="sxs-lookup"><span data-stu-id="87f50-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="87f50-280">Olá atualização *Scripts* secção Olá *Views\Home\Index.cshtml* tooinclude código tooget Olá XSRF os tokens de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="87f50-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="87f50-281">Publicar tooAzure de atualização de aplicação Olá e base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="87f50-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="87f50-282">aplicação de Olá toopublish, que repete procedimento Olá que seguiu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="87f50-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="87f50-283">No **Explorador de soluções**, clique com o botão direito do rato em projeto Olá e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Publicar][rxP]
2. <span data-ttu-id="87f50-285">Clique em Olá **definições** separador.</span><span class="sxs-lookup"><span data-stu-id="87f50-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="87f50-286">Em **ContactsManagerContext(ContactsManagerContext)**, clique em Olá **v** ícone toochange *cadeia de ligação remota* toohello a cadeia de ligação para contacte Olá base de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="87f50-287">Clique em **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="87f50-287">Click **ContactDB**.</span></span>
   
    ![Definições](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="87f50-289">Verifique a caixa de Olá **executar código primeiro migrações (em execução no início da aplicação)**.</span><span class="sxs-lookup"><span data-stu-id="87f50-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="87f50-290">Clique em **seguinte** e, em seguida, clique em **pré-visualização**.</span><span class="sxs-lookup"><span data-stu-id="87f50-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="87f50-291">Visual Studio mostra uma lista de ficheiros de Olá que irá ser adicionadas ou atualizadas.</span><span class="sxs-lookup"><span data-stu-id="87f50-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="87f50-292">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="87f50-292">Click **Publish**.</span></span>
   <span data-ttu-id="87f50-293">Depois de concluída a implementação de Olá, o browser Olá abre toohello home page da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Página de índice com nenhuma contactos][intro001]
   
    <span data-ttu-id="87f50-295">Olá Visual Studio publicar a cadeia de ligação de Olá processo configurado automaticamente no Olá implementado *Web. config* base de dados do ficheiro toopoint toohello SQL.</span><span class="sxs-lookup"><span data-stu-id="87f50-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="87f50-296">Este também configurado migrações primeiro código tooautomatically Olá atualização da base de dados toohello versão mais recente Olá primeira hora Olá aplicação acede a base de dados de Olá após a implementação.</span><span class="sxs-lookup"><span data-stu-id="87f50-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="87f50-297">Como resultado desta configuração Code First criou Olá base de dados ao executar código Olá na Olá **inicial** classe que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="87f50-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="87f50-298">Era esta Olá primeiro tempo Olá aplicação tentou tooaccess Olá base de dados após a implementação.</span><span class="sxs-lookup"><span data-stu-id="87f50-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="87f50-299">Introduza um contacto tal como fez quando executou localmente, aplicação Olá tooverify implementação de base de dados concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="87f50-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="87f50-300">Quando vir que introduziu o item Olá é guardado e é apresentado na página de contacto manager Olá, sabe que tenham sido armazenado na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="87f50-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Página de índice com contactos][addwebapi004]

<span data-ttu-id="87f50-302">aplicação Olá está agora em execução na nuvem de Olá, utilizando a base de dados SQL toostore respetivos dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="87f50-303">Depois de concluir a testar a aplicação de Olá no Azure, elimine-o.</span><span class="sxs-lookup"><span data-stu-id="87f50-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="87f50-304">aplicação Olá é pública e não tem acesso de toolimit um mecanismo.</span><span class="sxs-lookup"><span data-stu-id="87f50-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="87f50-305">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="87f50-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="87f50-306">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="87f50-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="87f50-307">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="87f50-307">Next Steps</span></span>
<span data-ttu-id="87f50-308">Outra forma os dados toostore numa aplicação do Azure são toouse storage do Azure, que fornecem armazenamento de dados não relacionais no formulário de Olá de blobs e tabelas.</span><span class="sxs-lookup"><span data-stu-id="87f50-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="87f50-309">Olá seguintes ligações fornece mais informações sobre Web API, ASP.NET MVC e Azure de janela.</span><span class="sxs-lookup"><span data-stu-id="87f50-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="87f50-310">[Introdução Entity Framework utilizando MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="87f50-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="87f50-311">Introdução tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="87f50-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="87f50-312">Primeiro ASP.NET API Web</span><span class="sxs-lookup"><span data-stu-id="87f50-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="87f50-313">Depuração WAWS</span><span class="sxs-lookup"><span data-stu-id="87f50-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="87f50-314">Este tutorial e Olá exemplo de aplicação foi escrito pelo [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) com a assistência de Dykstra personalizada e Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="87f50-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="87f50-315">Deixe comentários no que gostou ou o que gostaria de toosee melhorada, não apenas sobre tutorial Olá próprio, mas também sobre os produtos de Olá que demonstra.</span><span class="sxs-lookup"><span data-stu-id="87f50-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="87f50-316">Os seus comentários irão ajudá-lo-na priorizar melhoramentos.</span><span class="sxs-lookup"><span data-stu-id="87f50-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="87f50-317">Estamos especialmente interessados em localizar quanto interesse existe é na automatização mais para o processo de Olá de configurar e implementar Olá associação da base de dados.</span><span class="sxs-lookup"><span data-stu-id="87f50-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="87f50-318">O que mudou</span><span class="sxs-lookup"><span data-stu-id="87f50-318">What's changed</span></span>
* <span data-ttu-id="87f50-319">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="87f50-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

