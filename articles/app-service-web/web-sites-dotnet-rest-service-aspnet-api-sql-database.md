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
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Criar um serviço REST utilizando a API Web do ASP.NET e a SQL Database no App Service do Azure
Este tutorial mostra como toodeploy um ASP.NET web app tooan [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) utilizando o Assistente para publicar Web Olá no Visual Studio 2013 ou Visual Studio 2013 Community Edition. 

Pode criar uma conta do Azure gratuitamente e, se ainda não tiver o Visual Studio 2013, Olá SDK instala automaticamente o Visual Studio 2013 Express Web. Por isso, pode começar a desenvolver para o Azure inteiramente para gratuita.

Este tutorial parte do princípio de que tem qualquer experiência na utilização do Azure. Concluir neste tutorial, terá uma aplicação web simples cópias de segurança e em execução na nuvem de Olá.

Irá aprender:

* Como tooenable Olá, o computador para a programação do Azure instalando o Azure SDK.
* Como toocreate um Visual Studio ASP.NET MVC 5 do projeto e publicá-lo tooan aplicações do Azure.
* Como toouse Olá API Web do ASP.NET tooenable chama a Restful API.
* Como toouse SQL da base de dados de toostore no Azure.
* Como aplicação toopublish atualizações tooAzure.

Irá criar uma aplicação de web de lista de contactos simples que está incorporada no ASP.NET MVC 5 e utiliza hello do ADO.NET Entity Framework para acesso de base de dados. Olá seguinte ilustração mostra Olá concluída aplicação:

![captura de ecrã do web site][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Criar projeto Olá
1. Inicie o Visual Studio 2013.
2. De Olá **ficheiro** menu clique **novo projeto**.
3. No Olá **novo projeto** diálogo caixa, expanda **Visual c#** e selecione **Web** e, em seguida, selecione **aplicação Web ASP.NET**. Nome da aplicação Olá **ContactManager** e clique em **OK**.
   
    ![Caixa de diálogo Novo Projeto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. No Olá **novo projeto ASP.NET** caixa de diálogo, selecione de Olá **MVC** modelo, verificação **Web API** e, em seguida, clique em **alterar autenticação**.
5. No Olá **alterar autenticação** caixa de diálogo, clique em **sem autenticação**e, em seguida, clique em **OK**.
   
    ![Sem Autenticação](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    aplicação de exemplo de Olá que está a criar não terá de funcionalidades que requerem toolog de utilizadores no. Para obter informações sobre como tooimplement funcionalidades de autenticação e autorização, consulte Olá [passos](#nextsteps) secção no final deste tutorial Olá. 
6. No Olá **novo projeto ASP.NET** caixa de diálogo, Olá se disponibilizar **anfitrião na nuvem de Olá** está selecionada e clique em **OK**.

Se não tiver no tooAzure, será pedido toosign no.

1. Assistente de configuração de Olá será sugerir um nome exclusivo com base no *ContactManager* (ver a imagem de Olá abaixo). Selecione uma região perto de si. Pode utilizar [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind Olá menor latência de centro de dados. 
2. Se ainda não criou um servidor de base de dados antes, selecione **criar novo servidor**, introduza um nome de utilizador de base de dados e a palavra-passe.
   
    ![Configurar Web site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Se tiver um servidor de base de dados, utilize essa toocreate uma nova base de dados. Servidores de base de dados são um recurso precioso e geralmente pretender toocreate várias bases de dados no Olá mesmo servidor de teste e desenvolvimento em vez de criar um servidor de base de dados por base de dados. Certifique-se o web site e a base de dados Olá mesma região.

![Configurar Web site do Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Definir Olá cabeçalho e rodapé
1. No **Explorador de soluções**, expanda Olá *Views\Shared* pasta e abra Olá *layout* ficheiro.
   
    ![Layout no Explorador de soluções][newapp004]
2. Substituir conteúdo Olá Olá *Views\Shared_Layout.cshtml* ficheiro com Olá seguinte código:

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

marcação Olá acima nome da aplicação Olá alterações da "Aplicação ASP.NET My" demasiado "Contacte Manager" e remove ligações Olá demasiado**home page**, **sobre** e **contacte**.

### <a name="run-hello-application-locally"></a>Executar a aplicação Olá localmente
1. Prima a aplicação de Olá toorun CTRL + F5.
   home page da aplicação Olá é apresentada no browser predefinido de Olá.
    ![home page da lista tooDo](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Isto é tudo o que precisa toodo para aplicação de Olá agora toocreate que vai implementar tooAzure. Mais tarde, irá adicionar a funcionalidade de base de dados.

## <a name="deploy-hello-application-tooazure"></a>Implementar Olá tooAzure de aplicação
1. No Visual Studio, clique no projeto Olá no **Explorador de soluções** e selecione **publicar** no menu de contexto de Olá.
   
    ![Publicar no menu de contexto do projeto][PublishVSSolution]
   
    Olá **publicar Web** é aberto o assistente.
2. Clique em **Publicar**.

![Separador Definições](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio inicia o processo de Olá de copiar ficheiros de Olá toohello servidor do Azure. Olá **saída** janela mostra que ações de implementação foram executadas e reporta a conclusão com êxito da implementação de Olá.

1. browser predefinido de Olá abre automaticamente toohello URL do site de Olá implementado.
   
   aplicação Olá que criou está agora em execução na nuvem de Olá.
   
   ![tooDo lista home page em execução no Azure][rxz2]

## <a name="add-a-database-toohello-application"></a>Adicionar uma aplicação de toohello de base de dados
Em seguida, irá atualizar Olá MVC aplicação tooadd Olá capacidade toodisplay e atualizar os contactos e armazenar dados de Olá numa base de dados. aplicação Olá irá utilizar a base de dados do Olá do Entity Framework toocreate Olá e tooread e atualizar os dados na base de dados de Olá.

### <a name="add-data-model-classes-for-hello-contacts"></a>Adicionar classes de modelo de dados dos contactos de Olá
Comece por criar um modelo de dados simples no código.

1. No **Explorador de soluções**, faça duplo clique Olá modelos pasta, clique em **adicionar**e, em seguida, **classe**.
   
    ![Adicionar classe no menu de contexto de pasta de modelos][adddb001]
2. No Olá **Adicionar Novo Item** caixa de diálogo, nome Olá novo classe ficheiro *Contact.cs*e, em seguida, clique em **adicionar**.
   
    ![Adicionar Novo Item caixa de diálogo][adddb002]
3. Substitua Olá conteúdo de Olá Contacts.cs ficheiro Olá seguinte código.
   
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

Olá **contacte** classe define dados Olá que irá armazenar para cada contacte plus uma chave primária, ContactID, que é necessário para a base de dados de Olá. Pode obter mais informações sobre modelos de dados no Olá [passos](#nextsteps) secção no final deste tutorial Olá.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Criar páginas web que ativar a aplicação aos utilizadores toowork com contactos Olá
Olá funcionalidade do ASP.NET MVC Olá andaime pode gerar automaticamente o código que executa a criar, ler, atualizar e eliminar ações (CRUD).

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Adicionar um controlador e uma vista de dados de Olá
1. No **Explorador de soluções**, expanda a pasta de controladores Olá.
2. Compilar o projeto de Olá **(Ctrl + Shift + B)**. (Tem de criar o projeto de Olá antes de utilizar o mecanismo de andaime.) 
3. Faça duplo clique Olá controladores pasta e clique em **adicionar**e, em seguida, clique em **controlador**.
   
    ![Adicionar controlador no menu de contexto de pasta de controladores][addcode001]
4. No Olá **adicionar andaime** caixa de diálogo, selecione **controlador MVC com vistas, utilizando o Entity Framework** e clique em **adicionar**.
   
   ![Adicionar o controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Definir o nome do controlador de Olá demasiado**HomeController**. Selecione **contacte** como a classe de modelo. Clique em Olá **contexto de dados nova** botão e aceite a predefinição de Olá "ContactManager.Models.ContactManagerContext" para Olá **novo tipo de contexto de dados**. Clique em **Adicionar**.

    Uma caixa de diálogo irá solicitar-lhe: "um ficheiro com nome Olá HomeController já existe. Pretende tooreplace-? ". Clique em **Sim**. Estamos a substituição Olá home page controlador que foi criada com o novo projeto de Olá. Utilizaremos Olá novo home page controlador para a nossa lista de contactos.

    Métodos de controlador e vistas para operações CRUD de base de dados para o Visual Studio cria **contacte** objetos.

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Ativar migrações, crie a base de dados de Olá, adicionar dados de exemplo e um inicializador de dados
a tarefa seguinte Olá está tooenable Olá [migrações primeiro código](http://curah.microsoft.com/55220) funcionalidade na ordem toocreate Olá da base de dados baseada no modelo de dados de Olá que criou.

1. No Olá **ferramentas** menu, selecione **Gestor de pacotes de biblioteca** e, em seguida, **consola do Gestor de pacotes**.
   
    ![Consola do Gestor de pacotes no menu Ferramentas][addcode008]
2. No Olá **consola do Gestor de pacotes** janela, introduza Olá os seguintes comandos:
   
        enable-migrations 
   
    Olá **ativar migrações** comando cria um *migrações* pasta e coloca nessa pasta um *Configuration.cs* ficheiros que pode editar tooconfigure migrações. 
3. No Olá **consola do Gestor de pacotes** janela, introduza Olá os seguintes comandos:
   
        add-migration Initial
   
    Olá **inicial da migração adicionar** comandos gera uma classe com o nome  **&lt;date_stamp&gt;inicial** que cria a base de dados de Olá. Olá primeiro parâmetro ( *inicial* ) é arbitrário e utilizada toocreate Olá nome do ficheiro de Olá. Pode ver Olá nova classe ficheiros **Explorador de soluções**.
   
    No Olá **inicial** classe, hello **segurança** método cria a tabela de contactos de Olá e Olá **baixo** método (utilizado quando pretender que o estado anterior do tooreturn toohello) ignora-lo.
4. Abra Olá *Migrations\Configuration.cs* ficheiro. 
5. Adicione Olá seguintes espaços de nomes. 
   
         using ContactManager.Models;
6. Substitua Olá *Seed* método com Olá seguinte código:
   
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
   
    Este código acima inicializará a base de dados de Olá com as informações de contacto Olá. Para obter mais informações sobre a propagação de base de dados de Olá, consulte [bds de depuração do Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. No Olá **consola do Gestor de pacotes** introduza Olá comando:
   
        update-database
   
    ![Comandos de consola do Gestor de pacotes][addcode009]
   
    Olá **base de dados de atualização** executa Olá migração primeiro que cria Olá base de dados. Por predefinição, a base de dados de Olá será criado como uma base de dados do SQL Server Express LocalDB.
8. Prima a aplicação de Olá toorun CTRL + F5. 

aplicação Olá mostra os dados de seed Olá e fornece edição, detalhes e ligações de eliminação.

![Vista MVC de dados][rxz3]

## <a name="edit-hello-view"></a>Editar Olá vista
1. Abra Olá *Views\Home\Index.cshtml* ficheiro. No próximo passo Olá, iremos irá substituir o markup Olá gerado com o código que utiliza [jQuery](http://jquery.com/) e [Knockout.js](http://knockoutjs.com/). Este novo código obtém a lista de contactos de Olá de utilizar a web API e JSON e, em seguida, vincula Olá contacte dados toohello IU knockout.js a utilizar. Para obter mais informações, consulte Olá [passos](#nextsteps) secção no final deste tutorial Olá. 
2. Substitua conteúdo de Olá do ficheiro de Olá Olá seguinte código.
   
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
3. Pasta de conteúdo de Olá com o botão direito e clique em **adicionar**e, em seguida, clique em **Novo Item...** .
   
    ![Adicionar a folha de estilos no menu de contexto da pasta de conteúdo][addcode005]
4. No Olá **Adicionar Novo Item** caixa de diálogo, introduza **estilo** no Olá caixa de pesquisa direito superior e, em seguida, selecione **folha de estilos**.
    ![Adicionar Novo Item caixa de diálogo][rxStyle]
5. Ficheiro de Olá nome *Contacts.css* e clique em **adicionar**. Substitua conteúdo de Olá do ficheiro de Olá Olá seguinte código.
   
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
   
    Utilizaremos esta folha de estilo de esquema de Olá, cores e estilos utilizados na aplicação do Gestor de contacto Olá.
6. Abra Olá *App_Start\BundleConfig.cs* ficheiro.
7. Adicionar Olá seguir Olá do código tooregister [Knockout](http://knockoutjs.com/index.html "KO") Plug-in.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Este exemplo com knockout toosimplify dinâmico código JavaScript que processa os modelos de ecrã de Olá.
8. Modificar Olá do Olá conteúdo/css entrada tooregister *contacts.css* folha de estilos. Alterar Olá seguinte linha:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Para:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Na consola do Gestor de pacotes Olá, execute Olá os seguintes comandos tooinstall Knockout.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Adicionar um controlador para a interface Web API Restful Olá
1. No **Explorador de soluções**, faça duplo clique controladores e clique em **adicionar** e, em seguida, **controlador...** 
2. No Olá **adicionar andaime** caixa de diálogo, introduza **Web API 2 controlador com ações, utilizando o Entity Framework** e, em seguida, clique em **adicionar**.
   
    ![Adicionar controlador da API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. No Olá **Adicionar controlador** caixa de diálogo, introduza "ContactsController" que o seu nome de controlador. Selecione "Contacte (ContactManager.Models)" para Olá **classe de modelo**.  Manter o valor predefinido Olá Olá **classe de contexto de dados**. 
4. Clique em **Adicionar**.

### <a name="run-hello-application-locally"></a>Executar a aplicação Olá localmente
1. Prima a aplicação de Olá toorun CTRL + F5.
   
    ![Página Índice][intro001]
2. Introduza um contacto e clique em **adicionar**. aplicação Olá devolve home page do toohello e apresenta contacte Olá que introduziu.
   
    ![Página de índice com itens de lista de tarefas][addwebapi004]
3. No browser Olá, acrescentar **/api/contactos** toohello URL.
   
    URL de resultante Olá irá assemelhar-se http://localhost:1234/api/contactos. Olá a API web RESTful adicionou devolve contactos Olá armazenado. Firefox e o Chrome irão apresentar dados de Olá no formato XML.
   
    ![Página de índice com itens de lista de tarefas][rxFFchrome]

    I/e irá solicitar-lhe tooopen ou guardar Olá contactos.

    ![Caixa de diálogo de guardar API Web][addwebapi006]


    Pode abrir Olá devolvido contactos no bloco de notas ou um browser.

    Este resultado pode ser utilizado por outra aplicação, tais como a aplicação ou página web móvel.

    ![Caixa de diálogo de guardar API Web][addwebapi007]

    **Aviso de segurança**: nesta fase, a aplicação é ataque tooCSRF inseguras e vulnerável. Mais tarde no tutorial Olá vamos remover esta vulnerabilidade. Para obter mais informações consulte [impedir entre sites pedido falsificação (CSRF) ataques][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>Adicionar proteção XSRF
Falsificação de pedidos entre sites (também conhecido como XSRF ou CSRF) é um ataque contra aplicações web alojadas na qual um Web site malicioso pode influenciar a interação de Olá entre um browser do cliente e um site fidedigno para esse browser. Estes ataques são efetuados possíveis porque web browsers envia os tokens de autenticação automaticamente com cada Web site tooa de pedido. exemplo de canónico Olá é um cookie de autenticação, como ASP. Permissão de autenticação de formulários do NET. No entanto, os Web sites que utilizam qualquer mecanismo de autenticação persistente (por exemplo, a autenticação do Windows, Basic e assim sucessivamente) podem ser segmentados por estes ataques.

Um ataque XSRF é diferente de um ataque de phishing. Ataques de phishing requerem interação do vítima Olá. Ataques de phishing, um Web site malicioso irão imitar o Web site de destino Olá e vítima Olá é fooled para fornecer o atacante toohello de informações confidenciais. Num ataque XSRF, há muitas vezes, sem interação necessárias da vítima Olá. Em vez disso, o atacante Olá é a entidade confiadora no browser Olá enviar automaticamente o site de destino de toohello do todos os cookies relevantes.

Para obter mais informações, consulte Olá [abrir projeto de segurança de aplicações Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. No **Explorador de soluções**, direita **ContactManager** projeto e clique em **adicionar** e, em seguida, clique em **classe**.
2. Ficheiro de Olá nome *ValidateHttpAntiForgeryTokenAttribute.cs* e adicione Olá seguinte código:
   
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
3. Adicione Olá seguinte *utilizando* instrução toohello contrai controlador, pelo que tem acesso toohello **[ValidateHttpAntiForgeryToken]** atributo.
   
        using ContactManager.Filters;
4. Adicionar Olá **[ValidateHttpAntiForgeryToken]** atributo toohello métodos Post Olá **ContactsController** tooprotect-lo contra ameaças XSRF. Irá adicioná-la toohello "PutContact", "PostContact" e **DeleteContact** métodos de ação.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Olá atualização *Scripts* secção Olá *Views\Home\Index.cshtml* tooinclude código tooget Olá XSRF os tokens de ficheiros.
   
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

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Publicar tooAzure de atualização de aplicação Olá e base de dados SQL
aplicação de Olá toopublish, que repete procedimento Olá que seguiu anteriormente.

1. No **Explorador de soluções**, clique com o botão direito do rato em projeto Olá e selecione **publicar**.
   
    ![Publicar][rxP]
2. Clique em Olá **definições** separador.
3. Em **ContactsManagerContext(ContactsManagerContext)**, clique em Olá **v** ícone toochange *cadeia de ligação remota* toohello a cadeia de ligação para contacte Olá base de dados. Clique em **ContactDB**.
   
    ![Definições](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Verifique a caixa de Olá **executar código primeiro migrações (em execução no início da aplicação)**.
5. Clique em **seguinte** e, em seguida, clique em **pré-visualização**. Visual Studio mostra uma lista de ficheiros de Olá que irá ser adicionadas ou atualizadas.
6. Clique em **Publicar**.
   Depois de concluída a implementação de Olá, o browser Olá abre toohello home page da aplicação Olá.
   
    ![Página de índice com nenhuma contactos][intro001]
   
    Olá Visual Studio publicar a cadeia de ligação de Olá processo configurado automaticamente no Olá implementado *Web. config* base de dados do ficheiro toopoint toohello SQL. Este também configurado migrações primeiro código tooautomatically Olá atualização da base de dados toohello versão mais recente Olá primeira hora Olá aplicação acede a base de dados de Olá após a implementação.
   
    Como resultado desta configuração Code First criou Olá base de dados ao executar código Olá na Olá **inicial** classe que criou anteriormente. Era esta Olá primeiro tempo Olá aplicação tentou tooaccess Olá base de dados após a implementação.
7. Introduza um contacto tal como fez quando executou localmente, aplicação Olá tooverify implementação de base de dados concluída com êxito.

Quando vir que introduziu o item Olá é guardado e é apresentado na página de contacto manager Olá, sabe que tenham sido armazenado na base de dados de Olá.

![Página de índice com contactos][addwebapi004]

aplicação Olá está agora em execução na nuvem de Olá, utilizando a base de dados SQL toostore respetivos dados. Depois de concluir a testar a aplicação de Olá no Azure, elimine-o. aplicação Olá é pública e não tem acesso de toolimit um mecanismo.

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="next-steps"></a>Passos Seguintes
Outra forma os dados toostore numa aplicação do Azure são toouse storage do Azure, que fornecem armazenamento de dados não relacionais no formulário de Olá de blobs e tabelas. Olá seguintes ligações fornece mais informações sobre Web API, ASP.NET MVC e Azure de janela.

* [Introdução Entity Framework utilizando MVC][EFCodeFirstMVCTutorial]
* [Introdução tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Primeiro ASP.NET API Web](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Depuração WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Este tutorial e Olá exemplo de aplicação foi escrito pelo [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) com a assistência de Dykstra personalizada e Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Deixe comentários no que gostou ou o que gostaria de toosee melhorada, não apenas sobre tutorial Olá próprio, mas também sobre os produtos de Olá que demonstra. Os seus comentários irão ajudá-lo-na priorizar melhoramentos. Estamos especialmente interessados em localizar quanto interesse existe é na automatização mais para o processo de Olá de configurar e implementar Olá associação da base de dados. 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

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

