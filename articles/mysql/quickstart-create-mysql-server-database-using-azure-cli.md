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
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Criar uma Base de Dados do Azure para o servidor MySQL com a CLI do Azure
Este guia de introdução descreve como toouse Olá CLI do Azure toocreate uma base de dados do Azure para o servidor de MySQL num grupo de recursos do Azure em cerca de cinco minutos. Olá CLI do Azure é utilizado toocreate e gerir recursos do Azure Olá linha de comandos ou em scripts.

Se não tiver uma subscrição do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Se tiver várias subscrições, escolha subscrição adequada de Olá em que o recurso de Olá existe ou é faturado por. Selecione um ID de subscrição específica na sua conta com o comando [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Criar um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) utilizando Olá [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. Um grupo de recursos é um contentor lógico no qual os recursos do Azure são implementados e geridos como um grupo.

Olá exemplo seguinte cria um grupo de recursos denominado `myresourcegroup` no Olá `westus` localização.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Criar uma Base de Dados do Azure para o servidor MySQL
Criar uma base de dados do Azure para o servidor de MySQL com Olá **az mysql servidor criar** comando. Cada servidor pode gerir múltiplas bases de dados. Geralmente, é utilizada uma base de dados em separado para cada projeto ou para cada utilizador.

Olá exemplo seguinte cria uma base de dados do Azure para o servidor de MySQL localizado em `westus` no grupo de recursos de Olá `myresourcegroup` com nome `myserver4demo`. servidor de Olá tem um registo de administrador no nome `myadmin` e palavra-passe `Password01!`. servidor de Olá é criado com **básico** camada de desempenho e **50** unidades partilhadas entre todos os Olá bases de dados no servidor de Olá de computação. Pode dimensionar a computação e armazenamento ou reduza verticalmente consoante as necessidades de aplicação Olá.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurar a regra de firewall
Criar uma base de dados do Azure para a regra de firewall ao nível do servidor de MySQL utilizando Olá **az mysql servidor-regra de firewall criar** comando. Uma regra de firewall ao nível do servidor permite que uma aplicação externa, tais como Olá **mysql.exe** ferramenta da linha de comandos ou o servidor de tooyour do MySQL Workbench tooconnect através da firewall do serviço de Azure MySQL de Olá. 

Olá exemplo seguinte cria uma regra de firewall para um intervalo de endereços predefinidos, que, neste exemplo, é Olá todo possíveis intervalo de endereços IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Configurar as definições de SSL
Por predefinição, são aplicadas ligações SSL entre o servidor e as aplicações cliente.  Isto garante que a segurança de "em movimento" Olá, dados ao encriptar o fluxo de dados de Olá através de internet.  toomake este de início rápido mais fácil, desativamos a ligações de SSL para o servidor.  A desativação não é recomendada para servidores de produção.  Para obter mais informações, consulte [conectividade de configurar o SSL na sua toosecurely de aplicação de ligação tooAzure da base de dados MySQL](./howto-configure-ssl.md).

Olá exemplo a seguir desativa a imposição de SSL no seu servidor MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Obter informações de ligação de Olá

servidor de tooyour tooconnect, terá de tooprovide de credenciais de acesso e informação de anfitrião.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

resultado de Olá está no formato JSON. Tome nota do Olá **fullyQualifiedDomainName** e **administratorLogin**.
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Ligar o servidor toohello utilizando a ferramenta de linha de comandos do Olá mysql.exe
Ligar o servidor de tooyour utilizando Olá **mysql.exe** ferramenta da linha de comandos. Pode transferir o MySQL [aqui](https://dev.mysql.com/downloads/) e instalá-lo no seu computador. Em vez disso, pode também clicar em Olá **tente-** botão amostras de código ou Olá `>_` botão de Olá superior direita barra de ferramentas no Olá portal do Azure e iniciação Olá **Shell de nuvem do Azure**.

Escreva os comandos seguintes Olá: 

1. Ligar através de servidor toohello **mysql** ferramenta da linha de comandos:
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Ver o estado do servidor:
```sql
 mysql> status
```
Se tudo correr bem, ferramenta da linha de comandos Olá deve saída Olá seguinte texto:

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
> Para obter comandos adicionais, veja [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) (Manual de Referência do MySQL 5.7 - Capítulo 4.5.1).

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Ligar o servidor toohello utilizando a ferramenta de MySQL Workbench GUI Olá
1.  Inicie Olá aplicação MySQL Workbench no computador cliente. Pode transferir e instalar o MySQL Workbench [aqui](https://dev.mysql.com/downloads/workbench/).

2.  No Olá **configuração nova ligação** caixa de diálogo, introduza Olá seguindo as informações do **parâmetros** separador:

   ![configurar ligação nova](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Definição** | **Valor Sugerido** | **Descrição** |
|---|---|---|
|   Nome da Ligação | A Minha Ligação | Especifique uma etiqueta para esta ligação (pode ser qualquer nome) |
| Método de Ligação | escolha Standard (TCP/IP) | Utilizar o TCP/IP protocolo tooconnect tooAzure da base de dados para MySQL > |
| Nome de anfitrião | myserver4demo.mysql.database.azure.com | O nome de servidor que apontou anteriormente. |
| Porta | 3306 | é utilizada a porta predefinida de Olá para MySQL. |
| Nome de utilizador | myadmin@myserver4demo | Olá admin início de sessão do que anotou anteriormente. |
| Palavra-passe | **** | Utilize a palavra-passe Olá admin conta configurados anteriormente. |

Clique em **Testar ligação** tootest se todos os parâmetros estão corretamente configurados.
Agora, pode clicar em ligação Olá toosuccessfully ligar toohello servidor.

## <a name="clean-up-resources"></a>Limpar recursos
Se não tiver estes recursos para outro/tutorial de início rápido, podem eliminá-los efetuando Olá os seguintes comandos: 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Passos seguintes

> [!div class="nextstepaction"]
> [Design a MySQL Database with Azure CLI](./tutorial-design-database-using-cli.md) (Conceber uma Base de Dados MySQL com a CLI do Azure)
