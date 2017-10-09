---
title: "Guia de introdução: criar uma Base de Dados do Azure para o servidor MySQL - CLI do Azure | Microsoft Docs"
description: "Este guia de introdução descreve como toouse Olá CLI do Azure toocreate uma base de dados do Azure para o servidor de MySQL num grupo de recursos do Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="629db-103">Criar uma Base de Dados do Azure para o servidor MySQL com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="629db-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="629db-104">Este guia de introdução descreve como toouse Olá CLI do Azure toocreate uma base de dados do Azure para o servidor de MySQL num grupo de recursos do Azure em cerca de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="629db-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="629db-105">Olá CLI do Azure é utilizado toocreate e gerir recursos do Azure Olá linha de comandos ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="629db-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="629db-106">Se não tiver uma subscrição do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="629db-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="629db-107">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="629db-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="629db-108">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="629db-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="629db-109">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="629db-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="629db-110">Se tiver várias subscrições, escolha subscrição adequada de Olá em que o recurso de Olá existe ou é faturado por.</span><span class="sxs-lookup"><span data-stu-id="629db-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="629db-111">Selecione um ID de subscrição específica na sua conta com o comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="629db-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="629db-112">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="629db-112">Create a resource group</span></span>
<span data-ttu-id="629db-113">Criar um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) utilizando Olá [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="629db-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="629db-114">Um grupo de recursos é um contentor lógico no qual os recursos do Azure são implementados e geridos como um grupo.</span><span class="sxs-lookup"><span data-stu-id="629db-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="629db-115">Olá exemplo seguinte cria um grupo de recursos denominado `myresourcegroup` no Olá `westus` localização.</span><span class="sxs-lookup"><span data-stu-id="629db-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="629db-116">Criar uma Base de Dados do Azure para o servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="629db-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="629db-117">Criar uma base de dados do Azure para o servidor de MySQL com Olá **az mysql servidor criar** comando.</span><span class="sxs-lookup"><span data-stu-id="629db-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="629db-118">Cada servidor pode gerir múltiplas bases de dados.</span><span class="sxs-lookup"><span data-stu-id="629db-118">A server can manage multiple databases.</span></span> <span data-ttu-id="629db-119">Geralmente, é utilizada uma base de dados em separado para cada projeto ou para cada utilizador.</span><span class="sxs-lookup"><span data-stu-id="629db-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="629db-120">Olá exemplo seguinte cria uma base de dados do Azure para o servidor de MySQL localizado em `westus` no grupo de recursos de Olá `myresourcegroup` com nome `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="629db-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="629db-121">servidor de Olá tem um registo de administrador no nome `myadmin` e palavra-passe `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="629db-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="629db-122">servidor de Olá é criado com **básico** camada de desempenho e **50** unidades partilhadas entre todos os Olá bases de dados no servidor de Olá de computação.</span><span class="sxs-lookup"><span data-stu-id="629db-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="629db-123">Pode dimensionar a computação e armazenamento ou reduza verticalmente consoante as necessidades de aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="629db-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="629db-124">Configurar a regra de firewall</span><span class="sxs-lookup"><span data-stu-id="629db-124">Configure firewall rule</span></span>
<span data-ttu-id="629db-125">Criar uma base de dados do Azure para a regra de firewall ao nível do servidor de MySQL utilizando Olá **az mysql servidor-regra de firewall criar** comando.</span><span class="sxs-lookup"><span data-stu-id="629db-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="629db-126">Uma regra de firewall ao nível do servidor permite que uma aplicação externa, tais como Olá **mysql.exe** ferramenta da linha de comandos ou o servidor de tooyour do MySQL Workbench tooconnect através da firewall do serviço de Azure MySQL de Olá.</span><span class="sxs-lookup"><span data-stu-id="629db-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="629db-127">Olá exemplo seguinte cria uma regra de firewall para um intervalo de endereços predefinidos, que, neste exemplo, é Olá todo possíveis intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="629db-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="629db-128">Configurar as definições de SSL</span><span class="sxs-lookup"><span data-stu-id="629db-128">Configure SSL settings</span></span>
<span data-ttu-id="629db-129">Por predefinição, são aplicadas ligações SSL entre o servidor e as aplicações cliente.</span><span class="sxs-lookup"><span data-stu-id="629db-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="629db-130">Isto garante que a segurança de "em movimento" Olá, dados ao encriptar o fluxo de dados de Olá através de internet.</span><span class="sxs-lookup"><span data-stu-id="629db-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="629db-131">toomake este de início rápido mais fácil, desativamos a ligações de SSL para o servidor.</span><span class="sxs-lookup"><span data-stu-id="629db-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="629db-132">A desativação não é recomendada para servidores de produção.</span><span class="sxs-lookup"><span data-stu-id="629db-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="629db-133">Para obter mais informações, consulte [conectividade de configurar o SSL na sua toosecurely de aplicação de ligação tooAzure da base de dados MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="629db-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="629db-134">Olá exemplo a seguir desativa a imposição de SSL no seu servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="629db-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="629db-135">Obter informações de ligação de Olá</span><span class="sxs-lookup"><span data-stu-id="629db-135">Get hello connection information</span></span>

<span data-ttu-id="629db-136">servidor de tooyour tooconnect, terá de tooprovide de credenciais de acesso e informação de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="629db-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="629db-137">resultado de Olá está no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="629db-137">hello result is in JSON format.</span></span> <span data-ttu-id="629db-138">Tome nota do Olá **fullyQualifiedDomainName** e **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="629db-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="629db-139">Ligar o servidor toohello utilizando a ferramenta de linha de comandos do Olá mysql.exe</span><span class="sxs-lookup"><span data-stu-id="629db-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="629db-140">Ligar o servidor de tooyour utilizando Olá **mysql.exe** ferramenta da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="629db-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="629db-141">Pode transferir o MySQL [aqui](https://dev.mysql.com/downloads/) e instalá-lo no seu computador.</span><span class="sxs-lookup"><span data-stu-id="629db-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="629db-142">Em vez disso, pode também clicar em Olá **tente-** botão amostras de código ou Olá `>_` botão de Olá superior direita barra de ferramentas no Olá portal do Azure e iniciação Olá **Shell de nuvem do Azure**.</span><span class="sxs-lookup"><span data-stu-id="629db-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="629db-143">Escreva os comandos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="629db-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="629db-144">Ligar através de servidor toohello **mysql** ferramenta da linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="629db-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="629db-145">Ver o estado do servidor:</span><span class="sxs-lookup"><span data-stu-id="629db-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="629db-146">Se tudo correr bem, ferramenta da linha de comandos Olá deve saída Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="629db-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="629db-147">Para obter comandos adicionais, veja [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) (Manual de Referência do MySQL 5.7 - Capítulo 4.5.1).</span><span class="sxs-lookup"><span data-stu-id="629db-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="629db-148">Ligar o servidor toohello utilizando a ferramenta de MySQL Workbench GUI Olá</span><span class="sxs-lookup"><span data-stu-id="629db-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="629db-149">Inicie Olá aplicação MySQL Workbench no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="629db-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="629db-150">Pode transferir e instalar o MySQL Workbench [aqui](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="629db-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="629db-151">No Olá **configuração nova ligação** caixa de diálogo, introduza Olá seguindo as informações do **parâmetros** separador:</span><span class="sxs-lookup"><span data-stu-id="629db-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![configurar ligação nova](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="629db-153">**Definição**</span><span class="sxs-lookup"><span data-stu-id="629db-153">**Setting**</span></span> | <span data-ttu-id="629db-154">**Valor Sugerido**</span><span class="sxs-lookup"><span data-stu-id="629db-154">**Suggested Value**</span></span> | <span data-ttu-id="629db-155">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="629db-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="629db-156">Nome da Ligação</span><span class="sxs-lookup"><span data-stu-id="629db-156">Connection Name</span></span> | <span data-ttu-id="629db-157">A Minha Ligação</span><span class="sxs-lookup"><span data-stu-id="629db-157">My Connection</span></span> | <span data-ttu-id="629db-158">Especifique uma etiqueta para esta ligação (pode ser qualquer nome)</span><span class="sxs-lookup"><span data-stu-id="629db-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="629db-159">Método de Ligação</span><span class="sxs-lookup"><span data-stu-id="629db-159">Connection Method</span></span> | <span data-ttu-id="629db-160">escolha Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="629db-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="629db-161">Utilizar o TCP/IP protocolo tooconnect tooAzure da base de dados para MySQL ></span><span class="sxs-lookup"><span data-stu-id="629db-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="629db-162">Nome de anfitrião</span><span class="sxs-lookup"><span data-stu-id="629db-162">Hostname</span></span> | <span data-ttu-id="629db-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="629db-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="629db-164">O nome de servidor que apontou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="629db-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="629db-165">Porta</span><span class="sxs-lookup"><span data-stu-id="629db-165">Port</span></span> | <span data-ttu-id="629db-166">3306</span><span class="sxs-lookup"><span data-stu-id="629db-166">3306</span></span> | <span data-ttu-id="629db-167">é utilizada a porta predefinida de Olá para MySQL.</span><span class="sxs-lookup"><span data-stu-id="629db-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="629db-168">Nome de utilizador</span><span class="sxs-lookup"><span data-stu-id="629db-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="629db-169">Olá admin início de sessão do que anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="629db-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="629db-170">Palavra-passe</span><span class="sxs-lookup"><span data-stu-id="629db-170">Password</span></span> | **** | <span data-ttu-id="629db-171">Utilize a palavra-passe Olá admin conta configurados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="629db-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="629db-172">Clique em **Testar ligação** tootest se todos os parâmetros estão corretamente configurados.</span><span class="sxs-lookup"><span data-stu-id="629db-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="629db-173">Agora, pode clicar em ligação Olá toosuccessfully ligar toohello servidor.</span><span class="sxs-lookup"><span data-stu-id="629db-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="629db-174">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="629db-174">Clean up resources</span></span>
<span data-ttu-id="629db-175">Se não tiver estes recursos para outro/tutorial de início rápido, podem eliminá-los efetuando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="629db-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="629db-176">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="629db-176">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="629db-177">[Design a MySQL Database with Azure CLI](./tutorial-design-database-using-cli.md) (Conceber uma Base de Dados MySQL com a CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="629db-177">[Design a MySQL Database with Azure CLI](./tutorial-design-database-using-cli.md)</span></span>
