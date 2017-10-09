---
title: "aaaNode.js web app através da Olá serviço de tabela do Azure"
description: "Este tutorial informa como toouse Olá tabelas do Azure service toostore dados a partir de uma aplicação Node.js que está alojado nas Web Apps do Azure App Service."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Aplicação de web do node.js utilizando Olá serviço de tabela do Azure
## <a name="overview"></a>Descrição geral
Este tutorial mostra como serviço de tabela toouse forneceu dados de toostore e acesso de gestão de dados do Azure de um [nó] aplicação alojada em [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps. Este tutorial parte do princípio de que tem alguma experiência anterior com o nó e [Git].

Aprenderá:

* Como toouse npm (Gestor de pacotes do nó) tooinstall Olá módulos de nó
* Como toowork com Olá serviço tabela do Azure
* Como toouse Olá toocreate CLI do Azure numa aplicação web.

Ao seguir este tutorial, irá criar uma simples baseada na web aplicação de "lista de tarefas", que permite criar, obter e concluir tarefas. tarefas de Olá são armazenadas no Olá serviço tabela.

Segue-se a aplicação Olá concluída:

![Uma página web que apresenta um tasklist vazio][node-table-finished]

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Antes de seguir as instruções de Olá neste artigo, certifique-se de que tem o seguinte Olá instalado:

* [nó] versão 0.10.24 ou superior
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
Crie uma conta do Storage do Azure. aplicação Olá irá utilizar itens de tarefas nesta conta toostore Olá.

1. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com/).
2. Clique em Olá **novo** ícone na parte inferior de Olá esquerda do portal de Olá, em seguida, clique em **dados + armazenamento** > **armazenamento**. Dê um nome exclusivo de conta de armazenamento Olá e crie um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para o mesmo.
   
      ![Botão novo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Quando tiver sido criada a conta de armazenamento Olá, Olá **notificações** botão será flash um verde **êxito** e painel de conta de armazenamento a Olá está aberta tooshow que pertence toohello novo recurso do grupo criar.
3. No painel de conta de armazenamento a Olá, clique em **definições** > **chaves**. Área de transferência da chave toohello de acesso primária do Olá de cópia.
   
    ![Chave de acesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Instalar módulos e gerar andaime
Nesta secção irá criar uma nova aplicação de nó e utilizar pacotes de módulo de tooadd npm. Para esta aplicação utilizará Olá [Express] e [Azure] módulos. módulo de Express de Olá fornece uma arquitetura de controlador de vista de modelo para o nó, ao hello módulos do Azure fornece o serviço de tabela de toohello de conectividade.

### <a name="install-express-and-generate-scaffolding"></a>Instalação rápida e gerar andaime
1. A partir da linha de comandos Olá, criar um novo diretório designado **tasklist** e comutador toothat diretório.  
2. Introduza Olá seguir o módulo do comando tooinstall Olá rápida.
   
        npm install express-generator@4.2.0 -g
   
    Consoante o sistema de operativo Olá, poderá ser necessário tooput 'sudo' antes de comando de Olá:
   
        sudo npm install express-generator@4.2.0 -g
   
    saída de Olá aparece toohello semelhante seguinte exemplo:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Olá "-g' parâmetro instala o módulo Olá global. Dessa forma, podemos utilizar **rápida** toogenerate andaime de aplicação web sem ter tootype nas informações de caminho adicionais.
   > 
   > 
3. andaime de Olá toocreate para aplicação Olá, introduza Olá **rápida** comando:
   
        express
   
    é apresentado toohello semelhante seguinte o exemplo de resultado de Olá deste comando:
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    Agora, tem várias novos diretórios e ficheiros no Olá **tasklist** diretório.

### <a name="install-additional-modules"></a>Instalar módulos adicionais
Um dos Olá ficheiros que **rápida** cria é **Package. JSON**. Este ficheiro contém uma lista de dependências de módulo. Mais tarde, quando implementar Olá aplicação tooApp serviço Web Apps, este determina quais os módulos que precisam de toobe instalado no Azure.

No Olá da linha de comandos, introduza Olá seguintes módulos de Olá comando tooinstall descritos Olá **Package. JSON** ficheiro. Poderá ser necessário toouse 'sudo'.

    npm install

é apresentado toohello semelhante seguinte o exemplo de resultado de Olá deste comando:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Em seguida, introduza Olá Olá tooinstall de comando a seguir [azure], [uuid de nó], [nconf] e [async] módulos:

    npm install azure-storage node-uuid async nconf --save

Olá **– guardar** sinalizador Adiciona entradas para estes módulos toohello **Package. JSON** ficheiro.

é apresentado toohello semelhante seguinte o exemplo de resultado de Olá deste comando:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Criar aplicação Olá
Agora, estamos a aplicação de Olá toobuild pronto.

### <a name="create-a-model"></a>Criar um modelo
A *modelo* é um objeto que representa dados Olá na sua aplicação. Para a aplicação Olá, Olá apenas é um objeto de tarefa, que representa um item na lista de tarefas Olá. Tarefas terão Olá seguintes campos:

* PartitionKey
* RowKey
* nome (cadeia)
* categoria (cadeia)
* foi concluído (valor boleano)

**PartitionKey** e **RowKey** são utilizados pelo Olá serviço tabela como chaves de tabela. Para obter mais informações, consulte [modelo de dados de serviço tabela de Olá compreender](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. No Olá **tasklist** directory, criar um novo diretório designado **modelos**.
2. No Olá **modelos** directory, crie um novo ficheiro designado **task.js**. Este ficheiro irá conter o modelo de Olá para tarefas de Olá criado pela sua aplicação.
3. Início de Olá do Olá **task.js** ficheiro, adicione Olá bibliotecas do código tooreference necessário os seguintes:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Adicione o seguinte Olá code toodefine e exportar o objeto de tarefa Olá. Este objeto é responsável por ligar toohello tabela.
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. Adicione Olá seguindo métodos adicionais do código toodefine do objeto de tarefa Olá, que permite interações com os dados armazenados na tabela de Olá:
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. Guarde e feche Olá **task.js** ficheiro.

### <a name="create-a-controller"></a>Criar um controlador
A *controlador* processa os pedidos HTTP e apresenta-resposta Olá HTML.

1. No Olá **tasklist/rotas** directory, crie um novo ficheiro designado **tasklist.js** e abri-lo no editor de texto.
2. Adicionar Olá seguinte código demasiado**tasklist.js**. Esta ação carregue Olá do azure e async módulos, que são utilizados pelo **tasklist.js**. Isto também define Olá **TaskList** função, o que é transmitida uma instância de Olá **tarefas** objeto definido anteriormente:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Definir um **TaskList** objeto.
   
        function TaskList(task) {
          this.task = task;
        }
4. Adicionar Olá demasiado os seguintes métodos**TaskList**:
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a>Modificar app.js
1. De Olá **tasklist** Olá diretório, abra **app.js** ficheiro. Este ficheiro foi criado anteriormente executando Olá **rápida** comando.
2. Início de Olá do ficheiro de Olá, adicione Olá tooload Olá azure módulo, o nome de tabela do conjunto Olá, chave de partição e as credenciais de armazenamento do conjunto Olá utilizadas por este exemplo a seguir:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf irá carregar os valores de configuração de Olá de variáveis de ambiente ou Olá **config** ficheiro, que iremos criar mais tarde.
   > 
   > 
3. No ficheiro de app.js Olá, desloque para baixo toowhere vir Olá seguinte linha:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Substitua Olá acima linhas com o código de Olá mostrado abaixo. Isto irá inicializar uma instância de <strong>tarefas</strong> com uma conta de armazenamento de tooyour de ligação. Isto é transmitido toohello <strong>TaskList</strong>, que irá utilizar toocommunicate com Olá serviço tabela:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Guardar Olá **app.js** ficheiro.

### <a name="modify-hello-index-view"></a>Modificar a vista de índice de Olá
1. Abra Olá **tasklist/views/index.jade** ficheiro num editor de texto.
2. Substitua conteúdos integrais do Olá do ficheiro de Olá Olá seguinte código. Isto define uma vista que apresenta tarefas existentes e inclui um formulário para adicionar novas tarefas e marcar existentes como concluído.
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. Guarde e feche **Index. jade** ficheiro.

### <a name="modify-hello-global-layout"></a>Modificar esquema global Olá
Olá **jade** ficheiro Olá **vistas** diretório é um modelo global para outros **. jade** ficheiros. Neste passo, irá modificá-la toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), que é um toolkit que torna mais fácil toodesign uma aplicação de web looking nice.

Transferir e extrair os ficheiros de Olá para [Twitter Bootstrap](http://getbootstrap.com/). Olá cópia **bootstrap.min.css** ficheiros do arranque de Olá **css** pasta para Olá **público/tramas** diretório da sua aplicação.

De Olá **vistas** pasta, abra **jade** e substitua os conteúdos integrais Olá pelo seguinte Olá:

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a>Criar um ficheiro de configuração
localmente toorun Olá aplicação, vamos pôr em prática as credenciais do armazenamento do Azure para um ficheiro de configuração. Crie um ficheiro denominado **config* * com Olá JSON a seguir:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Substitua **nome da conta de armazenamento** com o nome de Olá de armazenamento de Olá conta que criou anteriormente e substitua **chave de acesso de armazenamento** com a chave de acesso primária de Olá para a sua conta de armazenamento. Por exemplo:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Guarde este ficheiro *nível superior de um diretório* que Olá **tasklist** diretório, como esta:

    parent/
      |-- config.json
      |-- tasklist/

motivo de Olá para efetuar este procedimento é tooavoid a verificar o ficheiro de configuração de Olá para controlo de origem, onde poderá ficar público. Iremos implementar tooAzure de aplicação Olá, utilizaremos as variáveis de ambiente em vez de um ficheiro de configuração.

## <a name="run-hello-application-locally"></a>Executar a aplicação Olá localmente
aplicação de Olá tootest no seu computador local, execute Olá os seguintes passos:

1. De Olá da linha de comandos, altere os diretórios toohello **tasklist** diretório.
2. Utilize Olá aplicação localmente do comando toolaunch Olá os seguintes:
   
        npm start
3. Abra um browser e navegue toohttp://127.0.0.1:3000.
   
    É apresentada uma página web de toohello semelhante seguinte exemplo.
   
    ![Uma página Web que apresenta um tasklist vazio][node-table-finished]
4. toocreate um novo item de tarefas, introduza um nome e a categoria e clique em **Adicionar Item**. 
5. toomark uma tarefa como concluída, verifique **concluída** e clique em **tarefas de actualização**.
   
    ![Uma imagem de Olá novo item na lista de Olá de tarefas][node-table-list-items]

Apesar de aplicação Olá é executada localmente, este é armazenar dados de Olá no Olá serviço de Azure Table.

## <a name="deploy-your-application-tooazure"></a>Implementar a aplicação tooAzure
Olá passos nesta secção utilizam ferramentas de linha de comandos do Azure de Olá toocreate uma nova aplicação web no App Service e, em seguida, utilizarem a aplicação de toodeploy de Git. tooperform estes passos têm de ter uma subscrição do Azure.

> [!NOTE]
> Estes passos podem também ser executados utilizando Olá [Portal do Azure](https://portal.azure.com/). Consulte [criar e implementar uma aplicação de web de Node.js no App Service do Azure].
> 
> Se este for Olá primeira aplicação web que criou, tem de utilizar Olá Portal do Azure toodeploy esta aplicação.
> 
> 

tooget iniciado, instalar Olá [CLI do Azure] introduzindo Olá os seguintes comandos Olá linha de comandos:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Importar definições de publicação
Neste passo, irá transferir um ficheiro que contém informações sobre a sua subscrição.

1. Introduza Olá os seguintes comandos:
   
        azure login
   
    Este comando inicia um browser e navega toohello página de transferência. Se lhe for solicitado, inicie sessão com a conta Olá com a sua subscrição do Azure.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    transferência de ficheiros de Olá começa automaticamente; Se não existir, pode clicar em ligação Olá início Olá de Olá toomanually transferência Olá do ficheiro de paginação. Guarde Olá de ficheiros e nota Olá caminho do ficheiro.
2. Introduza Olá definições do comando tooimport Olá os seguintes:
   
        azure account import <path-to-file>
   
    Especifique o nome de ficheiro e caminho de Olá do Olá a publicação do ficheiro de definições que transferiu no passo anterior Olá.
3. Depois das definições de Olá são importadas, eliminar Olá publicar o ficheiro de definições. Já não é necessária e contém informações confidenciais relativas à sua subscrição do Azure.

### <a name="create-an-app-service-web-app"></a>Criar um aplicação web do app Service
1. De Olá da linha de comandos, altere os diretórios toohello **tasklist** diretório.
2. Utilize Olá os seguintes comandos toocreate uma nova aplicação web.
   
        azure site create --git
   
    Será solicitado para o nome da aplicação web Olá e localização. Forneça um nome exclusivo e selecione Olá mesma localização geográfica da sua conta do Storage do Azure.
   
    Olá `--git` parâmetro cria um repositório de Git no Azure para esta aplicação web. Também inicializa um repositório de Git no diretório atual Olá se nenhum existir e adiciona uma [Git remoto] com o nome "azure", que é utilizado toopublish Olá aplicação tooAzure. Por fim, cria um **Web. config** ficheiro que contém as definições utilizadas por aplicações de nó toohost do Azure. Se omitir Olá `--git` parâmetro mas Olá diretório contém um repositório de Git, o comando de Olá ainda criará remoto Olá "azure".
   
    Assim que este comando foi concluída, verá a seguinte de toohello semelhante de saída. Tenha em atenção que Olá linha a partir **Web site criado em** contém Olá URL da aplicação web de Olá.
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > Se este for Olá primeira aplicação web do app Service para a sua subscrição, será aplicação web de Olá toocreate instruiu toouse Olá Portal do Azure. Para obter mais informações, consulte [criar e implementar uma aplicação de web de Node.js no App Service do Azure].
   > 
   > 

### <a name="set-environment-variables"></a>Variáveis de ambiente de conjunto
Neste passo, irá adicionar configuração de aplicação de web de tooyour de variáveis de ambiente no Azure.
Olá linha de comandos, introduza o seguinte Olá:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Substitua  **<storage account name>**  com o nome de Olá de armazenamento de Olá conta que criou anteriormente e substitua  **<storage access key>**  com a chave de acesso primária de Olá para a sua conta de armazenamento. (Utilizar o mesmo valores de Olá como ficheiro de config Olá que criou anteriormente.)

Em alternativa, pode definir variáveis de ambiente no Olá [Portal do Azure](https://portal.azure.com/):

1. Abra o painel da aplicação web Olá clicando **procurar** > **Web Apps** > nome da aplicação web.
2. No painel da sua aplicação web, clique em **todas as definições** > **definições da aplicação**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Desloque para baixo toohello **as definições de aplicação** secção e adicionar os pares chave/valor de Olá.
   
     ![Definições de aplicação](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Clique em **GUARDAR**.

### <a name="publish-hello-application"></a>Publicar a aplicação Olá
aplicação do toopublish Olá, consolide Olá código ficheiros tooGit e, em seguida, emita tooazure/principal.

1. Defina as suas credenciais de implementação.
   
        azure site deployment user set <name> <password>
2. Adicionar e consolidar os ficheiros da aplicação.
   
        git add .
        git commit -m "adding files"
3. Push Olá consolidação toohello aplicação web do app Service:
   
        git push azure master
   
    Utilize **mestre** como ramo de destino Olá. No final de Olá da implementação de Olá, verá um toohello semelhante de instrução seguinte exemplo:
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Depois de concluída a operação de push Olá, procure o URL da aplicação web toohello devolvido anteriormente por Olá `azure create site` comando tooview a aplicação.

## <a name="next-steps"></a>Passos seguintes
Enquanto os passos descritos neste artigo Olá descrevem a utilizar as informações de toostore do serviço tabela Olá, também pode utilizar [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Recursos adicionais
[CLI do Azure]

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- URLs -->

[criar e implementar uma aplicação de web de Node.js no App Service do Azure]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[nó]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remoto]: http://git-scm.com/docs/git-remote

[CLI do Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[uuid de nó]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
