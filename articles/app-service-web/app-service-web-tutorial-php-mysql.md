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
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="6aa4a-103">Criar uma aplicação web PHP e o MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="6aa4a-104">[As Aplicações Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="6aa4a-105">Este tutorial mostra como toocreate um PHP web de aplicação no Azure e ligá-lo tooa base de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="6aa4a-106">Quando tiver terminado, terá um [Laravel](https://laravel.com/) aplicação em execução no Web Apps do Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![Aplicação PHP em execução no App Service do Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="6aa4a-108">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6aa4a-109">Criar uma base de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="6aa4a-110">Ligar um tooMySQL de aplicações do PHP</span><span class="sxs-lookup"><span data-stu-id="6aa4a-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="6aa4a-111">Implementar Olá tooAzure de aplicação</span><span class="sxs-lookup"><span data-stu-id="6aa4a-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="6aa4a-112">Atualizar o modelo de dados de Olá e volte a implementar a aplicação de Olá</span><span class="sxs-lookup"><span data-stu-id="6aa4a-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="6aa4a-113">Registos de diagnóstico de fluxo a partir do Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="6aa4a-114">Gerir a aplicação Olá no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6aa4a-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6aa4a-115">Prerequisites</span></span>

<span data-ttu-id="6aa4a-116">toocomplete neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="6aa4a-117">[Instale o Git](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-117">[Install Git](https://git-scm.com/)</span></span>
* [<span data-ttu-id="6aa4a-118">Instalar o PHP 5.6.4 ou superior</span><span class="sxs-lookup"><span data-stu-id="6aa4a-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="6aa4a-119">Instalar compositor</span><span class="sxs-lookup"><span data-stu-id="6aa4a-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="6aa4a-120">Ativar Olá seguintes extensões PHP Laravel necessidades: OpenSSL PDO MySQL, Mbstring, atomizador, XML</span><span class="sxs-lookup"><span data-stu-id="6aa4a-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="6aa4a-121">Instalar e iniciar o MySQL</span><span class="sxs-lookup"><span data-stu-id="6aa4a-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="6aa4a-122">Preparar o local MySQL</span><span class="sxs-lookup"><span data-stu-id="6aa4a-122">Prepare local MySQL</span></span>

<span data-ttu-id="6aa4a-123">Neste passo, vai criar uma base de dados no seu servidor MySQL local para a utilização deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="6aa4a-124">Ligar toolocal MySQL servidor</span><span class="sxs-lookup"><span data-stu-id="6aa4a-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="6aa4a-125">Numa janela de terminal, ligar tooyour local MySQL servidor.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="6aa4a-126">Pode utilizar esta janela de terminal toorun todos os comandos de Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="6aa4a-127">Se lhe for pedida uma palavra-passe, introduza a palavra-passe de Olá para Olá `root` conta.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="6aa4a-128">Se não se lembra da sua palavra-passe da conta de raiz, consulte o artigo [MySQL: como tooReset Olá palavra-passe raiz](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="6aa4a-129">Se o comando for executado com êxito, em seguida, o servidor de MySQL está em execução.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="6aa4a-130">Se não, certifique-se de que o servidor de MySQL local é iniciado por Olá seguinte [passos de pós-instalação MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="6aa4a-131">Criar uma base de dados localmente</span><span class="sxs-lookup"><span data-stu-id="6aa4a-131">Create a database locally</span></span>

<span data-ttu-id="6aa4a-132">Em Olá `mysql` solicitar, crie uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="6aa4a-133">Sair da sua ligação ao servidor introduzindo `quit`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="6aa4a-134">Criar uma aplicação PHP localmente</span><span class="sxs-lookup"><span data-stu-id="6aa4a-134">Create a PHP app locally</span></span>
<span data-ttu-id="6aa4a-135">Neste passo, obter um exemplo de aplicação Laravel, configurar a ligação de base de dados e executá-la localmente.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="6aa4a-136">Exemplo de Olá clone</span><span class="sxs-lookup"><span data-stu-id="6aa4a-136">Clone hello sample</span></span>

<span data-ttu-id="6aa4a-137">Na janela de terminal Olá, `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="6aa4a-138">Execute Olá repositório do comando tooclone Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="6aa4a-139">`cd`diretório de tooyour clonado.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="6aa4a-140">Instale pacotes de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="6aa4a-141">Configurar a ligação de MySQL</span><span class="sxs-lookup"><span data-stu-id="6aa4a-141">Configure MySQL connection</span></span>

<span data-ttu-id="6aa4a-142">Na raiz do repositório de Olá, crie um ficheiro denominado *.env*.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="6aa4a-143">Olá cópia seguintes variáveis em Olá *.env* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="6aa4a-144">Substitua Olá  _&lt;root_password >_ marcador de posição pela palavra-passe do utilizador de Olá, MySQL raiz.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

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

<span data-ttu-id="6aa4a-145">Para obter informações sobre como Laravel utiliza Olá _.env_ de ficheiros, consulte [Laravel ambiente configuração](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="6aa4a-146">Executar o exemplo de Olá localmente</span><span class="sxs-lookup"><span data-stu-id="6aa4a-146">Run hello sample locally</span></span>

<span data-ttu-id="6aa4a-147">Executar [migrações de base de dados de Laravel](https://laravel.com/docs/5.4/migrations) toocreate Olá tabelas Olá necessidades de aplicação.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="6aa4a-148">toosee que são criadas tabelas em migrações Olá, procure no Olá _da base de dados/migrações_ diretório no repositório de Git Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="6aa4a-149">Gere uma nova chave de aplicação de Laravel.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="6aa4a-150">Execute a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="6aa4a-151">Navegue demasiado`http://localhost:8000` num browser.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="6aa4a-152">Adicione algumas tarefas na página Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-152">Add a few tasks in hello page.</span></span>

![PHP liga-se com êxito tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="6aa4a-154">toostop PHP, escreva `Ctrl + C` no Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="6aa4a-155">Criar o MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-155">Create MySQL in Azure</span></span>

<span data-ttu-id="6aa4a-156">Neste passo, vai criar uma base de dados MySQL no [MySQL (pré-visualização) na base de dados Azure](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="6aa4a-157">Posteriormente, configurar Olá PHP aplicação tooconnect toothis da base de dados.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="6aa4a-158">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6aa4a-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="6aa4a-159">Criar um servidor de MySQL</span><span class="sxs-lookup"><span data-stu-id="6aa4a-159">Create a MySQL server</span></span>

<span data-ttu-id="6aa4a-160">Criar um servidor na base de dados do Azure para MySQL (pré-visualização) com Olá [az mysql servidor criar](/cli/azure/mysql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="6aa4a-161">No Olá seguinte comando, substitua o nome do servidor MySQL onde vir Olá  _&lt;mysql_server_name >_ marcador de posição (carateres válidos são `a-z`, `0-9`, e `-`).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="6aa4a-162">Este nome é parte do nome de anfitrião do servidor de MySQL Olá (`<mysql_server_name>.database.windows.net`), tem de toobe globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="6aa4a-163">Quando é criado o servidor de MySQL Olá, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="6aa4a-164">Configurar a firewall do servidor</span><span class="sxs-lookup"><span data-stu-id="6aa4a-164">Configure server firewall</span></span>

<span data-ttu-id="6aa4a-165">Criar uma regra de firewall para o cliente do MySQL servidor tooallow ligações utilizando Olá [az mysql servidor-regra de firewall criar](/cli/azure/mysql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="6aa4a-166">Base de dados do Azure para MySQL (pré-visualização) atualmente não limita os serviços de tooAzure apenas de ligações.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="6aa4a-167">Como dinamicamente forem atribuídos a endereços IP no Azure, é melhor tooenable todos os endereços IP.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="6aa4a-168">serviço de Olá está em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-168">hello service is in preview.</span></span> <span data-ttu-id="6aa4a-169">Melhor métodos para proteger a sua base de dados estão a ser planeados.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="6aa4a-170">Ligar tooproduction MySQL servidor localmente</span><span class="sxs-lookup"><span data-stu-id="6aa4a-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="6aa4a-171">Na janela de terminal Olá, ligar toohello MySQL server no Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="6aa4a-172">Utilizar valor Olá especificado anteriormente para  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="6aa4a-173">Quando lhe for pedido para uma palavra-passe, utilize _$tr0ngPa$ w0rd!_, que especificou quando criou a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="6aa4a-174">Criar uma base de dados de produção</span><span class="sxs-lookup"><span data-stu-id="6aa4a-174">Create a production database</span></span>

<span data-ttu-id="6aa4a-175">Em Olá `mysql` solicitar, crie uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="6aa4a-176">Criar um utilizador com permissões</span><span class="sxs-lookup"><span data-stu-id="6aa4a-176">Create a user with permissions</span></span>

<span data-ttu-id="6aa4a-177">Criar um utilizador de base de dados chamado _phpappuser_ e conceda-lhe todos os privilégios no Olá `sampledb` base de dados.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="6aa4a-178">Sair da ligação ao servidor Olá escrevendo `quit`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="6aa4a-179">Ligar a aplicação tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="6aa4a-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="6aa4a-180">Neste passo, ligar Olá PHP aplicação toohello base de dados MySQL que criou na base de dados do Azure para MySQL (pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="6aa4a-181">Configurar a ligação de base de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="6aa4a-181">Configure hello database connection</span></span>

<span data-ttu-id="6aa4a-182">Na raiz do repositório de Olá, crie um _. env.production_ Olá ficheiro e copie os seguintes variáveis para a mesma.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="6aa4a-183">Substitua o marcador de posição de Olá  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="6aa4a-184">Guarde as alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="6aa4a-185">toosecure as informações de ligação do MySQL, este ficheiro já foi excluídas do repositório de Git Olá (consulte _. gitignore_ na raiz do repositório de Olá).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="6aa4a-186">Mais tarde, saiba como variáveis de ambiente de tooconfigure do serviço de aplicações tooconnect tooyour da base de dados na base de dados do Azure para MySQL (pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="6aa4a-187">Com variáveis de ambiente, não precisa de Olá *.env* ficheiro no App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="6aa4a-188">Configurar um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="6aa4a-188">Configure SSL certificate</span></span>

<span data-ttu-id="6aa4a-189">Por predefinição, a base de dados do Azure para MySQL impõe ligações de SSL de clientes.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="6aa4a-190">tooconnect tooyour base de dados MySQL no Azure, tem de utilizar um _. pem_ certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="6aa4a-191">Abra _config/database.php_ e adicione Olá _sslmode_ e _opções_ parâmetros demasiado`connections.mysql`, conforme apresentado na Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="6aa4a-192">toolearn como toogenerate isto _certificate.pem_, consulte [conectividade de configurar o SSL na sua toosecurely de aplicação de ligação tooAzure da base de dados MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="6aa4a-193">caminho de Olá _/ssl/certificate.pem_ pontos tooan existente _certificate.pem_ ficheiro no repositório de Git Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="6aa4a-194">Este ficheiro é fornecido para sua comodidade, neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="6aa4a-195">Para melhor prática, não deve consolidar o _. pem_ certificados para o controlo de origem.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="6aa4a-196">Testar a aplicação Olá localmente</span><span class="sxs-lookup"><span data-stu-id="6aa4a-196">Test hello application locally</span></span>

<span data-ttu-id="6aa4a-197">Execute migrações de base de dados de Laravel com _. env.production_ como hello ambiente ficheiro toocreate Olá as tabelas na base de dados MySQL na base de dados do Azure para MySQL (pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="6aa4a-198">Lembre-se de que _. env.production_ tem Olá ligação informações tooyour base de dados MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="6aa4a-199">_. env.production_ ainda não tem uma chave de aplicação válida.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="6aa4a-200">Gere um novo para o mesmo no Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="6aa4a-201">Executar a aplicação de exemplo de Olá com _. env.production_ como ficheiro de ambiente de Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="6aa4a-202">Navegue demasiado`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="6aa4a-203">Se a página Olá carrega sem erros, Olá aplicação PHP está a ligar toohello de dados MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="6aa4a-204">Adicione algumas tarefas na página Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-204">Add a few tasks in hello page.</span></span>

![PHP estabelece ligação com êxito tooAzure da base de dados para o MySQL (pré-visualização)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="6aa4a-206">toostop PHP, escreva `Ctrl + C` no Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="6aa4a-207">Consolidar as alterações</span><span class="sxs-lookup"><span data-stu-id="6aa4a-207">Commit your changes</span></span>

<span data-ttu-id="6aa4a-208">Execute as suas alterações de Olá seguir toocommit de comandos de Git:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="6aa4a-209">A aplicação está pronta toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="6aa4a-210">Implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-210">Deploy tooAzure</span></span>

<span data-ttu-id="6aa4a-211">Neste passo, pode implementar Olá ligados MySQL PHP aplicação tooAzure do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="6aa4a-212">Crie um plano do Serviço de Aplicações</span><span class="sxs-lookup"><span data-stu-id="6aa4a-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="6aa4a-213">Criar uma aplicação Web</span><span class="sxs-lookup"><span data-stu-id="6aa4a-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="6aa4a-214">Versão do conjunto Olá PHP</span><span class="sxs-lookup"><span data-stu-id="6aa4a-214">Set hello PHP version</span></span>

<span data-ttu-id="6aa4a-215">Versão do PHP de Olá conjunto que Olá aplicação requer utilizando Olá [az webapp configuração conjunto](/cli/azure/webapp/config#set) comando.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="6aa4a-216">Olá comando seguinte define Olá PHP versão too_7.0_.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="6aa4a-217">Configurar definições de base de dados</span><span class="sxs-lookup"><span data-stu-id="6aa4a-217">Configure database settings</span></span>

<span data-ttu-id="6aa4a-218">Como indicada anteriormente, pode ligar a base de dados do Azure MySQL tooyour utilizando variáveis de ambiente no App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="6aa4a-219">No App Service, definir variáveis de ambiente como _as definições de aplicação_ utilizando Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="6aa4a-220">Olá seguinte comando configura as definições de aplicação Olá `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, e `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="6aa4a-221">Substitua os marcadores de posição de Olá  _&lt;appname >_ e  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="6aa4a-222">Pode utilizar Olá PHP [getenv](http://www.php.net/manual/function.getenv.php) método tooaccess Olá definições.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="6aa4a-223">Olá Laravel código utiliza um [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper através de Olá PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="6aa4a-224">Por exemplo, Olá MySQL configuração _config/database.php_ aspeto Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="6aa4a-225">Configurar variáveis de ambiente de Laravel</span><span class="sxs-lookup"><span data-stu-id="6aa4a-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="6aa4a-226">Laravel tem uma chave de aplicação no App Service.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="6aa4a-227">Pode configurá-lo com as definições de aplicação.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-227">You can configure it with app settings.</span></span>

<span data-ttu-id="6aa4a-228">Utilize `php artisan` toogenerate uma nova chave de aplicação sem a guardar too_.env_.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="6aa4a-229">Definir a chave da aplicação Olá no Olá do serviço de aplicações aplicação web com Olá [az webapp configuração appsettings conjunto](/cli/azure/webapp/config/appsettings#set) comando.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="6aa4a-230">Substitua os marcadores de posição de Olá  _&lt;appname >_ e  _&lt;outputofphpartisankey: gerar >_.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="6aa4a-231">`APP_DEBUG="true"`Indica a Laravel tooreturn informações de depuração quando Olá implementado a aplicação web detetar erros.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="6aa4a-232">Quando executar uma aplicação de produção, defina-o demasiado`false`, que é mais segura.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="6aa4a-233">Caminho de aplicação virtual Olá de conjunto</span><span class="sxs-lookup"><span data-stu-id="6aa4a-233">Set hello virtual application path</span></span>

<span data-ttu-id="6aa4a-234">Definir o caminho da aplicação virtual Olá da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="6aa4a-235">Este passo é necessário porque Olá [ciclo de vida de aplicação de Laravel](https://laravel.com/docs/5.4/lifecycle) começa no Olá _pública_ diretório em vez de diretório de raiz da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="6aa4a-236">Outras estruturas PHP cujo ciclo de vida iniciar no diretório de raiz de Olá podem trabalhar sem configuração manual do caminho de aplicação virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="6aa4a-237">Caminho de aplicação virtual do conjunto Olá utilizando Olá [atualização de recurso az](/cli/azure/resource#update) comando.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="6aa4a-238">Substitua Olá  _&lt;appname >_ marcador de posição.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-238">Replace hello _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="6aa4a-239">Por predefinição, o App Service do Azure pontos caminho de aplicação virtual de raiz de Olá (_/_) toohello o diretório de raiz de Olá implementado ficheiros da aplicação (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="6aa4a-240">Configurar um utilizador de implementação</span><span class="sxs-lookup"><span data-stu-id="6aa4a-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="6aa4a-241">Configurar a implementação do Git local</span><span class="sxs-lookup"><span data-stu-id="6aa4a-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="6aa4a-242">Push tooAzure do Git</span><span class="sxs-lookup"><span data-stu-id="6aa4a-242">Push tooAzure from Git</span></span>

<span data-ttu-id="6aa4a-243">Adicione um repositório de Git local tooyour remoto do Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="6aa4a-244">Aplicação de PHP toohello toodeploy remoto do Azure Olá de emissão.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="6aa4a-245">Lhe for pedido para palavra-passe de Olá fornecidas anteriormente como parte da criação de Olá de utilizador de implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="6aa4a-246">Durante a implementação, o App Service do Azure comunica o progresso da mesma com o Git.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

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
> <span data-ttu-id="6aa4a-247">Poderá reparar que o processo de implementação de Olá instala [compositor](https://getcomposer.org/) pacotes em fim Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="6aa4a-248">Serviço de aplicações não executa estas automatizações durante a implementação predefinida, pelo que este repositório de exemplo tem três adicionais ficheiros no respetivo tooenable de diretório de raiz que:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="6aa4a-249">`.deployment`-Este ficheiro indica ao serviço de aplicações toorun `bash deploy.sh` como script de implementação personalizada Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="6aa4a-250">`deploy.sh`-Olá script de implementação personalizada.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="6aa4a-251">Se analisar ficheiro Olá, verá que é executada `php composer.phar install` depois `npm install`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="6aa4a-252">`composer.phar`-o Gestor de pacotes do compositor Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="6aa4a-253">Pode utilizar esta abordagem tooadd tooApp de implementação baseada no Git tooyour qualquer passo serviço.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="6aa4a-254">Para obter mais informações, consulte [Script de implementação personalizada](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="6aa4a-255">Procure a aplicação de web do Azure toohello</span><span class="sxs-lookup"><span data-stu-id="6aa4a-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="6aa4a-256">Procurar demasiado`http://<app_name>.azurewebsites.net` e adicione alguns lista de toohello de tarefas.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![Aplicação PHP em execução no App Service do Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="6aa4a-258">Parabéns, que está a executar uma aplicação PHP condicionada por dados no App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="6aa4a-259">Atualizar o modelo localmente e volte a implementar</span><span class="sxs-lookup"><span data-stu-id="6aa4a-259">Update model locally and redeploy</span></span>

<span data-ttu-id="6aa4a-260">Neste passo, efetuar uma alteração simples toohello `task` modelo de dados e Olá webapp e, em seguida, publicar Olá tooAzure de atualização.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="6aa4a-261">Para o cenário de tarefas Olá, modificar aplicação Olá, de modo a que pode marcar uma tarefa como concluídos.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="6aa4a-262">Adicionar uma coluna</span><span class="sxs-lookup"><span data-stu-id="6aa4a-262">Add a column</span></span>

<span data-ttu-id="6aa4a-263">No Olá terminal, navegue até toohello raiz do repositório de Git Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="6aa4a-264">Gerar uma nova migração de base de dados para Olá `tasks` tabela:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="6aa4a-265">Este mostra comandos Olá o nome do ficheiro de migração de Olá que é gerado.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="6aa4a-266">Localizar este ficheiro na _da base de dados/migrações_ e abri-lo.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="6aa4a-267">Substitua Olá `up` método com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="6aa4a-268">Olá anterior código adiciona uma coluna booleana no Olá `tasks` tabela denominada `complete`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="6aa4a-269">Substitua Olá `down` método com Olá seguinte código para a ação de reversão Olá:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="6aa4a-270">Olá terminal, execute Laravel da base de dados migrações toomake Olá de alterações na base de dados local Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="6aa4a-271">Com base no Olá [Convenção de nomenclatura Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modelo de Olá `Task` (consulte _app/Task.php_) mapeia toohello `tasks` tabela por predefinição.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="6aa4a-272">Lógica da aplicação de atualização</span><span class="sxs-lookup"><span data-stu-id="6aa4a-272">Update application logic</span></span>

<span data-ttu-id="6aa4a-273">Abra Olá *routes/web.php* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="6aa4a-274">Olá aplicação define a respetiva rotas e lógica de negócio aqui.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="6aa4a-275">No fim de Olá do ficheiro de Olá, adicione uma rota com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-275">At hello end of hello file, add a route with hello following code:</span></span>

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

<span data-ttu-id="6aa4a-276">Olá código anterior torna um modelo de dados de toohello atualização simples ao ativando ou desativando valor Olá `complete`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="6aa4a-277">Vista de atualização de Olá</span><span class="sxs-lookup"><span data-stu-id="6aa4a-277">Update hello view</span></span>

<span data-ttu-id="6aa4a-278">Abra Olá *resources/views/tasks.blade.php* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="6aa4a-279">Determinar Olá `<tr>` tag de início e substitua-o com:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="6aa4a-280">Olá anterior a cor de linha do código alterações Olá, dependendo se a tarefa de Olá estar concluída.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="6aa4a-281">Na linha seguinte Olá, terá de Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="6aa4a-282">Substitua toda a linha Olá Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-282">Replace hello entire line with hello following code:</span></span>

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

<span data-ttu-id="6aa4a-283">Olá anterior código adiciona botão para submeter Olá que faça referência a rota de Olá definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="6aa4a-284">Testar Olá alterações localmente</span><span class="sxs-lookup"><span data-stu-id="6aa4a-284">Test hello changes locally</span></span>

<span data-ttu-id="6aa4a-285">A partir do diretório de raiz de Olá do repositório de Git Olá, execute o servidor de desenvolvimento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="6aa4a-286">Olá toosee alteração de estado de tarefas, navegue demasiado`http://localhost:8000` e Olá selecione caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Caixa de verificação adicionado tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="6aa4a-288">toostop PHP, escreva `Ctrl + C` no Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="6aa4a-289">Publicar alterações tooAzure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-289">Publish changes tooAzure</span></span>

<span data-ttu-id="6aa4a-290">Olá terminal, execute Laravel migrações de base de dados com Olá produção ligação cadeia toomake Olá alteração Olá da base de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="6aa4a-291">Consolide todas as alterações de Olá no Git e, em seguida, emita tooAzure de alterações de código Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="6aa4a-292">Uma vez Olá `git push` é concluída, navegue até toohello web do Azure aplicação e teste Olá novas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![As alterações de modelo e a base de dados publicados tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="6aa4a-294">Se tiver adicionado quaisquer tarefas, estes são retidos na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="6aa4a-295">Esquema de dados de toohello atualizações deixar os dados existentes intactas.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="6aa4a-296">Registos de diagnóstico de fluxo</span><span class="sxs-lookup"><span data-stu-id="6aa4a-296">Stream diagnostic logs</span></span>

<span data-ttu-id="6aa4a-297">Enquanto executa Olá aplicação PHP no App Service do Azure, pode obter Olá consola registos direcionado tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="6aa4a-298">Dessa forma, pode obter Olá mesmas mensagens de diagnóstico toohelp depurar erros de aplicações.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="6aa4a-299">registo de toostart de transmissão em fluxo, utilize Olá [seguimento de registo de webapp az](/cli/azure/webapp/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="6aa4a-300">Assim que o registo de transmissão em fluxo foi iniciado, atualize Olá aplicação de web do Azure no Olá browser tooget algum tráfego web.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="6aa4a-301">Agora, pode ver o terminal de direcionado toohello de registos de consola.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="6aa4a-302">Se não vir registos console imediatamente, verifique novamente dentro de 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="6aa4a-303">registo de toostop de transmissão em fluxo em qualquer altura, tipo `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="6aa4a-304">Uma aplicação PHP pode utilizar o padrão de Olá [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello consola.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="6aa4a-305">aplicação de exemplo de Olá utiliza esta abordagem em _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="6aa4a-306">Como uma arquitetura de web [Laravel utiliza Monolog](https://laravel.com/docs/5.4/errors) como fornecedor de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="6aa4a-307">toosee como tooget Monolog toooutput mensagens toohello consola, consulte [PHP: como toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="6aa4a-308">Gerir a aplicação web do Azure de Olá</span><span class="sxs-lookup"><span data-stu-id="6aa4a-308">Manage hello Azure web app</span></span>

<span data-ttu-id="6aa4a-309">Aceda toohello [portal do Azure](https://portal.azure.com) toomanage Olá web aplicação que criou.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="6aa4a-310">No menu à esquerda Olá, clique em **serviços aplicacionais**e, em seguida, clique em nome de Olá da sua aplicação web do Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Aplicação de web de tooAzure de navegação do portal](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="6aa4a-312">É apresentada a página de descrição geral da sua aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-312">You see your web app's Overview page.</span></span> <span data-ttu-id="6aa4a-313">Aqui, pode efetuar tarefas de gestão básicas, como parar, iniciar, reiniciar, procurar e eliminar.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="6aa4a-314">menu à esquerda Olá fornece páginas para configurar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-314">hello left menu provides pages for configuring your app.</span></span>

![Página Serviço de Aplicações no portal do Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="6aa4a-316">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6aa4a-316">Next steps</span></span>

<span data-ttu-id="6aa4a-317">Neste tutorial, ficou a saber como:</span><span class="sxs-lookup"><span data-stu-id="6aa4a-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6aa4a-318">Criar uma base de dados MySQL no Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="6aa4a-319">Ligar um tooMySQL de aplicações do PHP</span><span class="sxs-lookup"><span data-stu-id="6aa4a-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="6aa4a-320">Implementar Olá tooAzure de aplicação</span><span class="sxs-lookup"><span data-stu-id="6aa4a-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="6aa4a-321">Atualizar o modelo de dados de Olá e volte a implementar a aplicação de Olá</span><span class="sxs-lookup"><span data-stu-id="6aa4a-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="6aa4a-322">Registos de diagnóstico de fluxo a partir do Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="6aa4a-323">Gerir a aplicação Olá no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="6aa4a-324">Avançar toohello toolearn de tutorial seguinte como toomap um DNS personalizado nome tooa web app.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6aa4a-325">Mapear um existente personalizado DNS nome tooAzure aplicações Web</span><span class="sxs-lookup"><span data-stu-id="6aa4a-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
