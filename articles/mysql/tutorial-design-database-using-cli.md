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
# <a name="design-your-first-azure-database-for-mysql-database"></a>Conceber a sua primeira base de dados do Azure para a base de dados MySQL

Base de dados do Azure para MySQL é um serviço de base de dados relacional no Olá nuvem da Microsoft com base no motor de base de dados MySQL Comunidade edição. Neste tutorial, utilizar a CLI do Azure (interface de linha de comandos) e outro toolearn utilitários como para:

> [!div class="checklist"]
> * Criar uma base de dados do Azure para MySQL
> * Configurar a firewall do servidor Olá
> * Utilize [ferramenta de linha de comandos mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate uma base de dados
> * Carregar dados de exemplo
> * Consultar dados
> * Atualizar dados
> * Restaurar dados

Pode utilizar Olá Shell de nuvem do Azure no hello browser, ou [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli) nos seus blocos de código do computador toorun Olá neste tutorial.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Se tiver várias subscrições, escolha subscrição adequada de Olá em que o recurso de Olá existe ou é faturado por. Selecione um ID de subscrição específica na sua conta com o comando [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Criar um [grupo de recursos do Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) com [criar grupo az](https://docs.microsoft.com/cli/azure/group#create) comando. Um grupo de recursos é um contentor lógico no qual os recursos do Azure são implementados e geridos como um grupo.

Olá exemplo seguinte cria um grupo de recursos denominado `mycliresource` no Olá `westus` localização.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Criar uma Base de Dados do Azure para o servidor MySQL
Crie uma base de dados do Azure para o servidor de MySQL com o servidor de mysql Olá az criar comando. Cada servidor pode gerir múltiplas bases de dados. Geralmente, é utilizada uma base de dados em separado para cada projeto ou para cada utilizador.

Olá exemplo seguinte cria uma base de dados do Azure para o servidor de MySQL localizado em `westus` no grupo de recursos de Olá `mycliresource` com nome `mycliserver`. servidor de Olá tem um registo de administrador no nome `myadmin` e palavra-passe `Password01!`. servidor de Olá é criado com **básico** camada de desempenho e **50** unidades partilhadas entre todos os Olá bases de dados no servidor de Olá de computação. Pode dimensionar a computação e armazenamento ou reduza verticalmente consoante as necessidades de aplicação Olá.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurar a regra de firewall
Crie uma base de dados do Azure para comandos de criação de regra de firewall ao nível do servidor de MySQL com Olá az mysql servidor-regra de firewall. Uma regra de firewall ao nível do servidor permite que uma aplicação externa, tais como **mysql** ferramenta da linha de comandos ou o servidor de tooyour do MySQL Workbench tooconnect através da firewall do serviço de Azure MySQL de Olá. 

Olá exemplo seguinte cria uma regra de firewall para um intervalo de endereços predefinidas. Este exemplo mostra Olá todo possíveis intervalo de endereços IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Obter informações de ligação de Olá

servidor de tooyour tooconnect, terá de tooprovide de credenciais de acesso e informação de anfitrião.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

resultado de Olá está no formato JSON. Tome nota do Olá **fullyQualifiedDomainName** e **administratorLogin**.
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

## <a name="connect-toohello-server-using-mysql"></a>Ligar o servidor de toohello utilizando mysql
Utilize [ferramenta de linha de comandos mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour uma ligação da base de dados do Azure para o servidor de MySQL. Neste exemplo, o comando de Olá é:
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Criar uma base de dados vazia
Quando estiver ligado toohello server, crie uma base de dados em branco.
```sql
mysql> CREATE DATABASE mysampledb;
```

Na linha de comandos Olá, execute Olá os seguintes comandos tooswitch Olá ligação toothis recém-criado da base de dados:
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Criar tabelas na base de dados de Olá
Agora que já sabe como tooconnect toohello base de dados do Azure para a base de dados MySQL, pode abordar como toocomplete algumas tarefas básicas.

Em primeiro lugar, iremos criar uma tabela e carregue-a com alguns dados. Vamos criar uma tabela que armazena informações de inventário.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Carregar dados para tabelas de Olá
Agora que temos uma tabela, iremos pode inserir alguns dados para a mesma. Janela de linha de comandos aberta Olá, execute Olá tooinsert de consulta a seguir algumas linhas de dados.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Tem agora duas linhas de dados de exemplo na tabela de Olá que criou anteriormente.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Consultar e atualizar os dados de Olá nas tabelas de Olá
Execute Olá seguintes tooretrieve informações da consulta de tabela de base de dados de Olá.
```sql
SELECT * FROM inventory;
```

Também pode atualizar os dados de Olá nas tabelas de Olá.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

linha Olá obtém atualizada em conformidade ao obter dados.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurar um ponto anterior de tooa de base de dados no tempo
Imagine que tenha eliminado acidentalmente nesta tabela. Este é algo que facilmente não consegue recuperar. Base de dados do Azure para MySQL permite-lhe toogo back tooany ponto no tempo no Olá última cópia de segurança too35 dias e restaurar nesta fase do novo servidor tooa de tempo. Pode utilizar esta nova toorecover de servidor os dados eliminados. Olá os seguintes passos Olá exemplo servidor tooa ponto de restauro do antes de tabela Olá foi adicionada.

Para Olá restauro terá Olá seguintes informações:

- Ponto de restauro: selecione um ponto no tempo que ocorre antes do servidor de Olá foi alterado. Tem de ser maior que ou igual ao valor de cópia de segurança mais antigo toohello origem da base de dados.
- Servidor de destino: forneça um novo nome de servidor que pretende toorestore para
- Servidor de origem: forneça Olá nome do servidor de Olá pretende toorestore do
- Localização: Não é possível selecionar a região de Olá, por predefinição é igual ao servidor de origem Olá

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

servidor de Olá toorestore e [restaurar tooa no momento](./howto-restore-server-portal.md) antes de tabela Olá foi eliminada. Restaurar um servidor tooa diferentes ponto no tempo cria um novo servidor duplicado como servidor original Olá de Olá ponto no tempo Especifica, desde que está dentro do período de retenção de Olá para sua [camada de serviço](./concepts-service-tiers.md).

## <a name="next-steps"></a>Passos Seguintes
Neste tutorial, que aprendeu a:
> [!div class="checklist"]
> * Criar uma base de dados do Azure para MySQL
> * Configurar a firewall do servidor Olá
> * Utilize [ferramenta de linha de comandos mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate uma base de dados
> * Carregar dados de exemplo
> * Consultar dados
> * Atualizar dados
> * Restaurar dados

> [!div class="nextstepaction"]
> [Base de dados do Azure para MySQL - amostras da CLI do Azure](./sample-scripts-azure-cli.md)
