---
title: "aaaBuild uma aplicação web PHP e o MySQL no Azure | Microsoft Docs"
description: "Saiba como tooget uma aplicação PHP a funcionar no Azure, com ligação tooa MySQL da base de dados no Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Criar uma aplicação web PHP e o MySQL no Azure

[As Aplicações Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática. Este tutorial mostra como toocreate um PHP web de aplicação no Azure e ligá-lo tooa base de dados MySQL. Quando tiver terminado, terá um [Laravel](https://laravel.com/) aplicação em execução no Web Apps do Azure App Service.

![Aplicação PHP em execução no App Service do Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Criar uma base de dados MySQL no Azure
> * Ligar um tooMySQL de aplicações do PHP
> * Implementar Olá tooAzure de aplicação
> * Atualizar o modelo de dados de Olá e volte a implementar a aplicação de Olá
> * Registos de diagnóstico de fluxo a partir do Azure
> * Gerir a aplicação Olá no Olá portal do Azure

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial:

* [Instale o Git](https://git-scm.com/).
* [Instalar o PHP 5.6.4 ou superior](http://php.net/downloads.php)
* [Instalar compositor](https://getcomposer.org/doc/00-intro.md)
* Ativar Olá seguintes extensões PHP Laravel necessidades: OpenSSL PDO MySQL, Mbstring, atomizador, XML
* [Instalar e iniciar o MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Preparar o local MySQL

Neste passo, vai criar uma base de dados no seu servidor MySQL local para a utilização deste tutorial.

### <a name="connect-toolocal-mysql-server"></a>Ligar toolocal MySQL servidor

Numa janela de terminal, ligar tooyour local MySQL servidor. Pode utilizar esta janela de terminal toorun todos os comandos de Olá neste tutorial.

```bash
mysql -u root -p
```

Se lhe for pedida uma palavra-passe, introduza a palavra-passe de Olá para Olá `root` conta. Se não se lembra da sua palavra-passe da conta de raiz, consulte o artigo [MySQL: como tooReset Olá palavra-passe raiz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Se o comando for executado com êxito, em seguida, o servidor de MySQL está em execução. Se não, certifique-se de que o servidor de MySQL local é iniciado por Olá seguinte [passos de pós-instalação MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Criar uma base de dados localmente

Em Olá `mysql` solicitar, crie uma base de dados.

```sql 
CREATE DATABASE sampledb;
```

Sair da sua ligação ao servidor introduzindo `quit`.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Criar uma aplicação PHP localmente
Neste passo, obter um exemplo de aplicação Laravel, configurar a ligação de base de dados e executá-la localmente. 

### <a name="clone-hello-sample"></a>Exemplo de Olá clone

Na janela de terminal Olá, `cd` tooa diretório de trabalho.

Execute Olá repositório do comando tooclone Olá exemplo a seguir.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`diretório de tooyour clonado.
Instale pacotes de Olá necessário.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>Configurar a ligação de MySQL

Na raiz do repositório de Olá, crie um ficheiro denominado *.env*. Olá cópia seguintes variáveis em Olá *.env* ficheiro. Substitua Olá  _&lt;root_password >_ marcador de posição pela palavra-passe do utilizador de Olá, MySQL raiz.

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

Para obter informações sobre como Laravel utiliza Olá _.env_ de ficheiros, consulte [Laravel ambiente configuração](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Executar o exemplo de Olá localmente

Executar [migrações de base de dados de Laravel](https://laravel.com/docs/5.4/migrations) toocreate Olá tabelas Olá necessidades de aplicação. toosee que são criadas tabelas em migrações Olá, procure no Olá _da base de dados/migrações_ diretório no repositório de Git Olá.

```bash
php artisan migrate
```

Gere uma nova chave de aplicação de Laravel.

```bash
php artisan key:generate
```

Execute a aplicação Olá.

```bash
php artisan serve
```

Navegue demasiado`http://localhost:8000` num browser. Adicione algumas tarefas na página Olá.

![PHP liga-se com êxito tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

toostop PHP, escreva `Ctrl + C` no Olá terminal.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>Criar o MySQL no Azure

Neste passo, vai criar uma base de dados MySQL no [MySQL (pré-visualização) na base de dados Azure](/azure/mysql). Posteriormente, configurar Olá PHP aplicação tooconnect toothis da base de dados.

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>Criar um servidor de MySQL

Criar um servidor na base de dados do Azure para MySQL (pré-visualização) com Olá [az mysql servidor criar](/cli/azure/mysql/server#create) comando.

No Olá seguinte comando, substitua o nome do servidor MySQL onde vir Olá  _&lt;mysql_server_name >_ marcador de posição (carateres válidos são `a-z`, `0-9`, e `-`). Este nome é parte do nome de anfitrião do servidor de MySQL Olá (`<mysql_server_name>.database.windows.net`), tem de toobe globalmente exclusivo.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Quando é criado o servidor de MySQL Olá, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a>Configurar a firewall do servidor

Criar uma regra de firewall para o cliente do MySQL servidor tooallow ligações utilizando Olá [az mysql servidor-regra de firewall criar](/cli/azure/mysql/server/firewall-rule#create) comando.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Base de dados do Azure para MySQL (pré-visualização) atualmente não limita os serviços de tooAzure apenas de ligações. Como dinamicamente forem atribuídos a endereços IP no Azure, é melhor tooenable todos os endereços IP. serviço de Olá está em pré-visualização. Melhor métodos para proteger a sua base de dados estão a ser planeados.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Ligar tooproduction MySQL servidor localmente

Na janela de terminal Olá, ligar toohello MySQL server no Azure. Utilizar valor Olá especificado anteriormente para  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

Quando lhe for pedido para uma palavra-passe, utilize _$tr0ngPa$ w0rd!_, que especificou quando criou a base de dados de Olá.

### <a name="create-a-production-database"></a>Criar uma base de dados de produção

Em Olá `mysql` solicitar, crie uma base de dados.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>Criar um utilizador com permissões

Criar um utilizador de base de dados chamado _phpappuser_ e conceda-lhe todos os privilégios no Olá `sampledb` base de dados.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Sair da ligação ao servidor Olá escrevendo `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Ligar a aplicação tooAzure MySQL

Neste passo, ligar Olá PHP aplicação toohello base de dados MySQL que criou na base de dados do Azure para MySQL (pré-visualização).

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Configurar a ligação de base de dados de Olá

Na raiz do repositório de Olá, crie um _. env.production_ Olá ficheiro e copie os seguintes variáveis para a mesma. Substitua o marcador de posição de Olá  _&lt;mysql_server_name >_.

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

Guarde as alterações de Olá.

> [!TIP]
> toosecure as informações de ligação do MySQL, este ficheiro já foi excluídas do repositório de Git Olá (consulte _. gitignore_ na raiz do repositório de Olá). Mais tarde, saiba como variáveis de ambiente de tooconfigure do serviço de aplicações tooconnect tooyour da base de dados na base de dados do Azure para MySQL (pré-visualização). Com variáveis de ambiente, não precisa de Olá *.env* ficheiro no App Service.
>

### <a name="configure-ssl-certificate"></a>Configurar um certificado SSL

Por predefinição, a base de dados do Azure para MySQL impõe ligações de SSL de clientes. tooconnect tooyour base de dados MySQL no Azure, tem de utilizar um _. pem_ certificado SSL.

Abra _config/database.php_ e adicione Olá _sslmode_ e _opções_ parâmetros demasiado`connections.mysql`, conforme apresentado na Olá seguinte código.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn como toogenerate isto _certificate.pem_, consulte [conectividade de configurar o SSL na sua toosecurely de aplicação de ligação tooAzure da base de dados MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> caminho de Olá _/ssl/certificate.pem_ pontos tooan existente _certificate.pem_ ficheiro no repositório de Git Olá. Este ficheiro é fornecido para sua comodidade, neste tutorial. Para melhor prática, não deve consolidar o _. pem_ certificados para o controlo de origem. 
>

### <a name="test-hello-application-locally"></a>Testar a aplicação Olá localmente

Execute migrações de base de dados de Laravel com _. env.production_ como hello ambiente ficheiro toocreate Olá as tabelas na base de dados MySQL na base de dados do Azure para MySQL (pré-visualização). Lembre-se de que _. env.production_ tem Olá ligação informações tooyour base de dados MySQL no Azure.

```bash
php artisan migrate --env=production --force
```

_. env.production_ ainda não tem uma chave de aplicação válida. Gere um novo para o mesmo no Olá terminal.

```bash
php artisan key:generate --env=production --force
```

Executar a aplicação de exemplo de Olá com _. env.production_ como ficheiro de ambiente de Olá.

```bash
php artisan serve --env=production
```

Navegue demasiado`http://localhost:8000`. Se a página Olá carrega sem erros, Olá aplicação PHP está a ligar toohello de dados MySQL no Azure.

Adicione algumas tarefas na página Olá.

![PHP estabelece ligação com êxito tooAzure da base de dados para o MySQL (pré-visualização)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

toostop PHP, escreva `Ctrl + C` no Olá terminal.

### <a name="commit-your-changes"></a>Consolidar as alterações

Execute as suas alterações de Olá seguir toocommit de comandos de Git:

```bash
git add .
git commit -m "database.php updates"
```

A aplicação está pronta toobe implementado.

## <a name="deploy-tooazure"></a>Implementar tooAzure

Neste passo, pode implementar Olá ligados MySQL PHP aplicação tooAzure do serviço de aplicações.

### <a name="create-an-app-service-plan"></a>Crie um plano do Serviço de Aplicações

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Criar uma aplicação Web

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Versão do conjunto Olá PHP

Versão do PHP de Olá conjunto que Olá aplicação requer utilizando Olá [az webapp configuração conjunto](/cli/azure/webapp/config#set) comando.

Olá comando seguinte define Olá PHP versão too_7.0_.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Configurar definições de base de dados

Como indicada anteriormente, pode ligar a base de dados do Azure MySQL tooyour utilizando variáveis de ambiente no App Service.

No App Service, definir variáveis de ambiente como _as definições de aplicação_ utilizando Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.

Olá seguinte comando configura as definições de aplicação Olá `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, e `DB_PASSWORD`. Substitua os marcadores de posição de Olá  _&lt;appname >_ e  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

Pode utilizar Olá PHP [getenv](http://www.php.net/manual/function.getenv.php) método tooaccess Olá definições. Olá Laravel código utiliza um [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper através de Olá PHP `getenv`. Por exemplo, Olá MySQL configuração _config/database.php_ aspeto Olá seguinte código:

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a>Configurar variáveis de ambiente de Laravel

Laravel tem uma chave de aplicação no App Service. Pode configurá-lo com as definições de aplicação.

Utilize `php artisan` toogenerate uma nova chave de aplicação sem a guardar too_.env_.

```bash
php artisan key:generate --show
```

Definir a chave da aplicação Olá no Olá do serviço de aplicações aplicação web com Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando. Substitua os marcadores de posição de Olá  _&lt;appname >_ e  _&lt;outputofphpartisankey: gerar >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`Indica a Laravel tooreturn informações de depuração quando Olá implementado a aplicação web detetar erros. Quando executar uma aplicação de produção, defina-o demasiado`false`, que é mais segura.

### <a name="set-hello-virtual-application-path"></a>Caminho de aplicação virtual Olá de conjunto

Definir o caminho da aplicação virtual Olá da aplicação web de Olá. Este passo é necessário porque Olá [ciclo de vida de aplicação de Laravel](https://laravel.com/docs/5.4/lifecycle) começa no Olá _pública_ diretório em vez de diretório de raiz da aplicação Olá. Outras estruturas PHP cujo ciclo de vida iniciar no diretório de raiz de Olá podem trabalhar sem configuração manual do caminho de aplicação virtual Olá.

Caminho de aplicação virtual do conjunto Olá utilizando Olá [atualização de recurso az](/cli/azure/resource#update) comando. Substitua Olá  _&lt;appname >_ marcador de posição.

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

Por predefinição, o App Service do Azure pontos caminho de aplicação virtual de raiz de Olá (_/_) toohello o diretório de raiz de Olá implementado ficheiros da aplicação (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Configurar um utilizador de implementação

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Configurar a implementação do Git local

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>Push tooAzure do Git

Adicione um repositório de Git local tooyour remoto do Azure.

```bash
git remote add azure <paste_copied_url_here>
```

Aplicação de PHP toohello toodeploy remoto do Azure Olá de emissão. Lhe for pedido para palavra-passe de Olá fornecidas anteriormente como parte da criação de Olá de utilizador de implementação de Olá.

```bash
git push azure master
```

Durante a implementação, o App Service do Azure comunica o progresso da mesma com o Git.

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> Poderá reparar que o processo de implementação de Olá instala [compositor](https://getcomposer.org/) pacotes em fim Olá. Serviço de aplicações não executa estas automatizações durante a implementação predefinida, pelo que este repositório de exemplo tem três adicionais ficheiros no respetivo tooenable de diretório de raiz que:
>
> - `.deployment`-Este ficheiro indica ao serviço de aplicações toorun `bash deploy.sh` como script de implementação personalizada Olá.
> - `deploy.sh`-Olá script de implementação personalizada. Se analisar ficheiro Olá, verá que é executada `php composer.phar install` depois `npm install`.
> - `composer.phar`-o Gestor de pacotes do compositor Olá.
>
> Pode utilizar esta abordagem tooadd tooApp de implementação baseada no Git tooyour qualquer passo serviço. Para obter mais informações, consulte [Script de implementação personalizada](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).
>

### <a name="browse-toohello-azure-web-app"></a>Procure a aplicação de web do Azure toohello

Procurar demasiado`http://<app_name>.azurewebsites.net` e adicione alguns lista de toohello de tarefas.

![Aplicação PHP em execução no App Service do Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

Parabéns, que está a executar uma aplicação PHP condicionada por dados no App Service do Azure.

## <a name="update-model-locally-and-redeploy"></a>Atualizar o modelo localmente e volte a implementar

Neste passo, efetuar uma alteração simples toohello `task` modelo de dados e Olá webapp e, em seguida, publicar Olá tooAzure de atualização.

Para o cenário de tarefas Olá, modificar aplicação Olá, de modo a que pode marcar uma tarefa como concluídos.

### <a name="add-a-column"></a>Adicionar uma coluna

No Olá terminal, navegue até toohello raiz do repositório de Git Olá.

Gerar uma nova migração de base de dados para Olá `tasks` tabela:

```bash
php artisan make:migration add_complete_column --table=tasks
```

Este mostra comandos Olá o nome do ficheiro de migração de Olá que é gerado. Localizar este ficheiro na _da base de dados/migrações_ e abri-lo.

Substitua Olá `up` método com Olá seguinte código:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Olá anterior código adiciona uma coluna booleana no Olá `tasks` tabela denominada `complete`.

Substitua Olá `down` método com Olá seguinte código para a ação de reversão Olá:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

Olá terminal, execute Laravel da base de dados migrações toomake Olá de alterações na base de dados local Olá.

```bash
php artisan migrate
```

Com base no Olá [Convenção de nomenclatura Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modelo de Olá `Task` (consulte _app/Task.php_) mapeia toohello `tasks` tabela por predefinição.

### <a name="update-application-logic"></a>Lógica da aplicação de atualização

Abra Olá *routes/web.php* ficheiro. Olá aplicação define a respetiva rotas e lógica de negócio aqui.

No fim de Olá do ficheiro de Olá, adicione uma rota com Olá seguinte código:

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

Olá código anterior torna um modelo de dados de toohello atualização simples ao ativando ou desativando valor Olá `complete`.

### <a name="update-hello-view"></a>Vista de atualização de Olá

Abra Olá *resources/views/tasks.blade.php* ficheiro. Determinar Olá `<tr>` tag de início e substitua-o com:

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Olá anterior a cor de linha do código alterações Olá, dependendo se a tarefa de Olá estar concluída.

Na linha seguinte Olá, terá de Olá seguinte código:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Substitua toda a linha Olá Olá seguinte código:

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

Olá anterior código adiciona botão para submeter Olá que faça referência a rota de Olá definido anteriormente.

### <a name="test-hello-changes-locally"></a>Testar Olá alterações localmente

A partir do diretório de raiz de Olá do repositório de Git Olá, execute o servidor de desenvolvimento de Olá.

```bash
php artisan serve
```

Olá toosee alteração de estado de tarefas, navegue demasiado`http://localhost:8000` e Olá selecione caixa de verificação.

![Caixa de verificação adicionado tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

toostop PHP, escreva `Ctrl + C` no Olá terminal.

### <a name="publish-changes-tooazure"></a>Publicar alterações tooAzure

Olá terminal, execute Laravel migrações de base de dados com Olá produção ligação cadeia toomake Olá alteração Olá da base de dados do Azure.

```bash
php artisan migrate --env=production --force
```

Consolide todas as alterações de Olá no Git e, em seguida, emita tooAzure de alterações de código Olá.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Uma vez Olá `git push` é concluída, navegue até toohello web do Azure aplicação e teste Olá novas funcionalidades.

![As alterações de modelo e a base de dados publicados tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Se tiver adicionado quaisquer tarefas, estes são retidos na base de dados de Olá. Esquema de dados de toohello atualizações deixar os dados existentes intactas.

## <a name="stream-diagnostic-logs"></a>Registos de diagnóstico de fluxo

Enquanto executa Olá aplicação PHP no App Service do Azure, pode obter Olá consola registos direcionado tooyour terminal. Dessa forma, pode obter Olá mesmas mensagens de diagnóstico toohelp depurar erros de aplicações.

registo de toostart de transmissão em fluxo, utilize Olá [seguimento de registo de webapp az](/cli/azure/webapp/log#tail) comando.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

Assim que o registo de transmissão em fluxo foi iniciado, atualize Olá aplicação de web do Azure no Olá browser tooget algum tráfego web. Agora, pode ver o terminal de direcionado toohello de registos de consola. Se não vir registos console imediatamente, verifique novamente dentro de 30 segundos.

registo de toostop de transmissão em fluxo em qualquer altura, tipo `Ctrl` + `C`.

> [!TIP]
> Uma aplicação PHP pode utilizar o padrão de Olá [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello consola. aplicação de exemplo de Olá utiliza esta abordagem em _app/Http/routes.php_.
>
> Como uma arquitetura de web [Laravel utiliza Monolog](https://laravel.com/docs/5.4/errors) como fornecedor de registo Olá. toosee como tooget Monolog toooutput mensagens toohello consola, consulte [PHP: como toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Gerir a aplicação web do Azure de Olá

Aceda toohello [portal do Azure](https://portal.azure.com) toomanage Olá web aplicação que criou.

No menu à esquerda Olá, clique em **serviços aplicacionais**e, em seguida, clique em nome de Olá da sua aplicação web do Azure.

![Aplicação de web de tooAzure de navegação do portal](./media/app-service-web-tutorial-php-mysql/access-portal.png)

É apresentada a página de descrição geral da sua aplicação Web. Aqui, pode efetuar tarefas de gestão básicas, como parar, iniciar, reiniciar, procurar e eliminar.

menu à esquerda Olá fornece páginas para configurar a sua aplicação.

![Página Serviço de Aplicações no portal do Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Criar uma base de dados MySQL no Azure
> * Ligar um tooMySQL de aplicações do PHP
> * Implementar Olá tooAzure de aplicação
> * Atualizar o modelo de dados de Olá e volte a implementar a aplicação de Olá
> * Registos de diagnóstico de fluxo a partir do Azure
> * Gerir a aplicação Olá no Olá portal do Azure

Avançar toohello toolearn de tutorial seguinte como toomap um DNS personalizado nome tooa web app.

> [!div class="nextstepaction"]
> [Mapear um existente personalizado DNS nome tooAzure aplicações Web](app-service-web-tutorial-custom-domain.md)
