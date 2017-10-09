---
title: registos do servidor de acesso e aaaConfigure para PostgreSQL utilizando a CLI do Azure | Microsoft Docs
description: "Este artigo descreve como tooconfigure e acesso Olá os registos do servidor na base de dados do Azure para PostgreSQL utilizando a linha de comandos da CLI do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Configurar e os registos do servidor de acesso utilizando a CLI do Azure
Pode transferir Olá PostgreSQL erro registos do servidor utilizando Olá Interface de linha de comandos (CLI do Azure). No entanto, os registos de tootransaction de acesso não é suportada. 

## <a name="prerequisites"></a>Pré-requisitos
toostep através deste tooguide como, tem de:
- Um [base de dados do Azure para o servidor de PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Instalar [Azure CLI 2.0](/cli/azure/install-azure-cli) da linha de comandos utilitário ou utilize Olá Shell de nuvem do Azure no browser Olá.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Configurar o registo da base de dados do Azure para PostgreSQL
Pode configurar Olá servidor tooaccess consulta registos e registos de erros. Os registos de erros podem conter informações vacuum automática, a ligação e a pontos de verificação.
1. Ativar o registo
2. Registo de atualização\_declaração e de registo\_min\_duração\_registo de consultas de tooenable de declaração
3. Período de retenção de atualização

Para obter mais informações, consulte [personalizar parâmetros de configuração do servidor](howto-configure-server-parameters-using-cli.md).

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Registos de lista da base de dados do Azure para o servidor de PostgreSQL
os ficheiros de registo disponível do toolist hello do servidor, execute Olá [lista de registos do servidor de postgres az](/cli/azure/postgres/server-logs#list) comando.

Pode listar os ficheiros de registo de Olá para servidor **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup**e direcionar o mesmo texto tooa ficheiro chamado **registo\_ficheiros\_list.txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Transferir localmente os registos do servidor de Olá
Olá [az postgres-registos do servidor transferir](/cli/azure/postgres/server-logs#download) comando permite-lhe ficheiros de registo individuais toodownload para o servidor. 

Neste exemplo Olá, transferências de ficheiros de registo específico para o servidor de Olá **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup** tooyour de ambiente local.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Passos seguintes
- toolearn mais informações sobre os registos do servidor, consulte [registos do servidor na base de dados do Azure para PostgreSQL](concepts-server-logs.md)
- Para obter mais informações sobre os parâmetros de servidor, consulte [personalizar parâmetros de configuração de servidor utilizando a CLI do Azure](howto-configure-server-parameters-using-cli.md)
