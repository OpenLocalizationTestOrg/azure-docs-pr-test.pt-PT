---
title: aaaDesign Azure sua primeira base de dados da base de dados MySQL - CLI do Azure | Microsoft Docs
description: "Este tutorial explica como toocreate e gerir a base de dados do Azure para o servidor de MySQL e da base de dados a utilizar o Azure CLI 2.0 Olá linha de comandos."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="337db-103">Conceber a sua primeira base de dados do Azure para a base de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="337db-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="337db-104">Base de dados do Azure para MySQL é um serviço de base de dados relacional no Olá nuvem da Microsoft com base no motor de base de dados MySQL Comunidade edição.</span><span class="sxs-lookup"><span data-stu-id="337db-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="337db-105">Neste tutorial, utilizar a CLI do Azure (interface de linha de comandos) e outro toolearn utilitários como para:</span><span class="sxs-lookup"><span data-stu-id="337db-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="337db-106">Criar uma base de dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="337db-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="337db-107">Configurar a firewall do servidor Olá</span><span class="sxs-lookup"><span data-stu-id="337db-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="337db-108">Utilize [ferramenta de linha de comandos mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate uma base de dados</span><span class="sxs-lookup"><span data-stu-id="337db-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="337db-109">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="337db-109">Load sample data</span></span>
> * <span data-ttu-id="337db-110">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="337db-110">Query data</span></span>
> * <span data-ttu-id="337db-111">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="337db-111">Update data</span></span>
> * <span data-ttu-id="337db-112">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="337db-112">Restore data</span></span>

<span data-ttu-id="337db-113">Pode utilizar Olá Shell de nuvem do Azure no hello browser, ou [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli) nos seus blocos de código do computador toorun Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="337db-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="337db-114">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="337db-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="337db-115">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="337db-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="337db-116">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="337db-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="337db-117">Se tiver várias subscrições, escolha subscrição adequada de Olá em que o recurso de Olá existe ou é faturado por.</span><span class="sxs-lookup"><span data-stu-id="337db-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="337db-118">Selecione um ID de subscrição específica na sua conta com o comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="337db-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="337db-119">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="337db-119">Create a resource group</span></span>
<span data-ttu-id="337db-120">Criar um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) com [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="337db-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="337db-121">Um grupo de recursos é um contentor lógico no qual os recursos do Azure são implementados e geridos como um grupo.</span><span class="sxs-lookup"><span data-stu-id="337db-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="337db-122">Olá exemplo seguinte cria um grupo de recursos denominado `mycliresource` no Olá `westus` localização.</span><span class="sxs-lookup"><span data-stu-id="337db-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="337db-123">Criar uma Base de Dados do Azure para o servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="337db-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="337db-124">Crie uma base de dados do Azure para o servidor de MySQL com o servidor de mysql Olá az criar comando.</span><span class="sxs-lookup"><span data-stu-id="337db-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="337db-125">Cada servidor pode gerir múltiplas bases de dados.</span><span class="sxs-lookup"><span data-stu-id="337db-125">A server can manage multiple databases.</span></span> <span data-ttu-id="337db-126">Geralmente, é utilizada uma base de dados em separado para cada projeto ou para cada utilizador.</span><span class="sxs-lookup"><span data-stu-id="337db-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="337db-127">Olá exemplo seguinte cria uma base de dados do Azure para o servidor de MySQL localizado em `westus` no grupo de recursos de Olá `mycliresource` com nome `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="337db-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="337db-128">servidor de Olá tem um registo de administrador no nome `myadmin` e palavra-passe `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="337db-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="337db-129">servidor de Olá é criado com **básico** camada de desempenho e **50** unidades partilhadas entre todos os Olá bases de dados no servidor de Olá de computação.</span><span class="sxs-lookup"><span data-stu-id="337db-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="337db-130">Pode dimensionar a computação e armazenamento ou reduza verticalmente consoante as necessidades de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="337db-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="337db-131">Configurar a regra de firewall</span><span class="sxs-lookup"><span data-stu-id="337db-131">Configure firewall rule</span></span>
<span data-ttu-id="337db-132">Crie uma base de dados do Azure para comandos de criação de regra de firewall ao nível do servidor de MySQL com Olá az mysql servidor-regra de firewall.</span><span class="sxs-lookup"><span data-stu-id="337db-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="337db-133">Uma regra de firewall ao nível do servidor permite que uma aplicação externa, tais como **mysql** ferramenta da linha de comandos ou o servidor de tooyour do MySQL Workbench tooconnect através da firewall do serviço de Azure MySQL de Olá.</span><span class="sxs-lookup"><span data-stu-id="337db-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="337db-134">Olá exemplo seguinte cria uma regra de firewall para um intervalo de endereços predefinidas.</span><span class="sxs-lookup"><span data-stu-id="337db-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="337db-135">Este exemplo mostra Olá todo possíveis intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="337db-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="337db-136">Obter informações de ligação de Olá</span><span class="sxs-lookup"><span data-stu-id="337db-136">Get hello connection information</span></span>

<span data-ttu-id="337db-137">servidor de tooyour tooconnect, terá de tooprovide de credenciais de acesso e informação de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="337db-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="337db-138">resultado de Olá está no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="337db-138">hello result is in JSON format.</span></span> <span data-ttu-id="337db-139">Tome nota do Olá **fullyQualifiedDomainName** e **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="337db-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="337db-140">Ligar o servidor de toohello utilizando mysql</span><span class="sxs-lookup"><span data-stu-id="337db-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="337db-141">Utilize [ferramenta de linha de comandos mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour uma ligação da base de dados do Azure para o servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="337db-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="337db-142">Neste exemplo, o comando de Olá é:</span><span class="sxs-lookup"><span data-stu-id="337db-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="337db-143">Criar uma base de dados vazia</span><span class="sxs-lookup"><span data-stu-id="337db-143">Create a blank database</span></span>
<span data-ttu-id="337db-144">Quando estiver ligado toohello server, crie uma base de dados em branco.</span><span class="sxs-lookup"><span data-stu-id="337db-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="337db-145">Na linha de comandos Olá, execute Olá os seguintes comandos tooswitch Olá ligação toothis recém-criado da base de dados:</span><span class="sxs-lookup"><span data-stu-id="337db-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="337db-146">Criar tabelas na base de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="337db-146">Create tables in hello database</span></span>
<span data-ttu-id="337db-147">Agora que já sabe como tooconnect toohello base de dados do Azure para a base de dados MySQL, pode abordar como toocomplete algumas tarefas básicas.</span><span class="sxs-lookup"><span data-stu-id="337db-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="337db-148">Em primeiro lugar, iremos criar uma tabela e carregue-a com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="337db-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="337db-149">Vamos criar uma tabela que armazena informações de inventário.</span><span class="sxs-lookup"><span data-stu-id="337db-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="337db-150">Carregar dados para tabelas de Olá</span><span class="sxs-lookup"><span data-stu-id="337db-150">Load data into hello tables</span></span>
<span data-ttu-id="337db-151">Agora que temos uma tabela, iremos pode inserir alguns dados para a mesma.</span><span class="sxs-lookup"><span data-stu-id="337db-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="337db-152">Janela de linha de comandos aberta Olá, execute Olá tooinsert de consulta a seguir algumas linhas de dados.</span><span class="sxs-lookup"><span data-stu-id="337db-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="337db-153">Tem agora duas linhas de dados de exemplo na tabela de Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="337db-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="337db-154">Consultar e atualizar os dados de Olá nas tabelas de Olá</span><span class="sxs-lookup"><span data-stu-id="337db-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="337db-155">Execute Olá seguintes tooretrieve informações da consulta de tabela de base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="337db-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="337db-156">Também pode atualizar os dados de Olá nas tabelas de Olá.</span><span class="sxs-lookup"><span data-stu-id="337db-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="337db-157">linha Olá obtém atualizada em conformidade ao obter dados.</span><span class="sxs-lookup"><span data-stu-id="337db-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="337db-158">Restaurar um ponto anterior de tooa de base de dados no tempo</span><span class="sxs-lookup"><span data-stu-id="337db-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="337db-159">Imagine que tenha eliminado acidentalmente nesta tabela.</span><span class="sxs-lookup"><span data-stu-id="337db-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="337db-160">Este é algo que facilmente não consegue recuperar.</span><span class="sxs-lookup"><span data-stu-id="337db-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="337db-161">Base de dados do Azure para MySQL permite-lhe toogo back tooany ponto no tempo no Olá última cópia de segurança too35 dias e restaurar nesta fase do novo servidor tooa de tempo.</span><span class="sxs-lookup"><span data-stu-id="337db-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="337db-162">Pode utilizar esta nova toorecover de servidor os dados eliminados.</span><span class="sxs-lookup"><span data-stu-id="337db-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="337db-163">Olá os seguintes passos Olá exemplo servidor tooa ponto de restauro do antes de tabela Olá foi adicionada.</span><span class="sxs-lookup"><span data-stu-id="337db-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="337db-164">Para Olá restauro terá Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="337db-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="337db-165">Ponto de restauro: selecione um ponto no tempo que ocorre antes do servidor de Olá foi alterado.</span><span class="sxs-lookup"><span data-stu-id="337db-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="337db-166">Tem de ser maior que ou igual ao valor de cópia de segurança mais antigo toohello origem da base de dados.</span><span class="sxs-lookup"><span data-stu-id="337db-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="337db-167">Servidor de destino: forneça um novo nome de servidor que pretende toorestore para</span><span class="sxs-lookup"><span data-stu-id="337db-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="337db-168">Servidor de origem: forneça Olá nome do servidor de Olá pretende toorestore do</span><span class="sxs-lookup"><span data-stu-id="337db-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="337db-169">Localização: Não é possível selecionar a região de Olá, por predefinição é igual ao servidor de origem Olá</span><span class="sxs-lookup"><span data-stu-id="337db-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="337db-170">servidor de Olá toorestore e [restaurar tooa no momento](./howto-restore-server-portal.md) antes de tabela Olá foi eliminada.</span><span class="sxs-lookup"><span data-stu-id="337db-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="337db-171">Restaurar um servidor tooa diferentes ponto no tempo cria um novo servidor duplicado como servidor original Olá de Olá ponto no tempo Especifica, desde que está dentro do período de retenção de Olá para sua [camada de serviço](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="337db-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="337db-172">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="337db-172">Next Steps</span></span>
<span data-ttu-id="337db-173">Neste tutorial, que aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="337db-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="337db-174">Criar uma base de dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="337db-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="337db-175">Configurar a firewall do servidor Olá</span><span class="sxs-lookup"><span data-stu-id="337db-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="337db-176">Utilize [ferramenta de linha de comandos mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate uma base de dados</span><span class="sxs-lookup"><span data-stu-id="337db-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="337db-177">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="337db-177">Load sample data</span></span>
> * <span data-ttu-id="337db-178">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="337db-178">Query data</span></span>
> * <span data-ttu-id="337db-179">Atualizar dados</span><span class="sxs-lookup"><span data-stu-id="337db-179">Update data</span></span>
> * <span data-ttu-id="337db-180">Restaurar dados</span><span class="sxs-lookup"><span data-stu-id="337db-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="337db-181">Base de dados do Azure para MySQL - amostras da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="337db-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
