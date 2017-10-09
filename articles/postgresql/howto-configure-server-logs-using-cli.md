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
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="5e523-103">Configurar e os registos do servidor de acesso utilizando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5e523-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="5e523-104">Pode transferir Olá PostgreSQL erro registos do servidor utilizando Olá Interface de linha de comandos (CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="5e523-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="5e523-105">No entanto, os registos de tootransaction de acesso não é suportada.</span><span class="sxs-lookup"><span data-stu-id="5e523-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5e523-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5e523-106">Prerequisites</span></span>
<span data-ttu-id="5e523-107">toostep através deste tooguide como, tem de:</span><span class="sxs-lookup"><span data-stu-id="5e523-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="5e523-108">Um [base de dados do Azure para o servidor de PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="5e523-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="5e523-109">Instalar [Azure CLI 2.0](/cli/azure/install-azure-cli) da linha de comandos utilitário ou utilize Olá Shell de nuvem do Azure no browser Olá.</span><span class="sxs-lookup"><span data-stu-id="5e523-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="5e523-110">Configurar o registo da base de dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="5e523-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="5e523-111">Pode configurar Olá servidor tooaccess consulta registos e registos de erros.</span><span class="sxs-lookup"><span data-stu-id="5e523-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="5e523-112">Os registos de erros podem conter informações vacuum automática, a ligação e a pontos de verificação.</span><span class="sxs-lookup"><span data-stu-id="5e523-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="5e523-113">Ativar o registo</span><span class="sxs-lookup"><span data-stu-id="5e523-113">Turn on logging</span></span>
2. <span data-ttu-id="5e523-114">Registo de atualização\_declaração e de registo\_min\_duração\_registo de consultas de tooenable de declaração</span><span class="sxs-lookup"><span data-stu-id="5e523-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="5e523-115">Período de retenção de atualização</span><span class="sxs-lookup"><span data-stu-id="5e523-115">Update retention period</span></span>

<span data-ttu-id="5e523-116">Para obter mais informações, consulte [personalizar parâmetros de configuração do servidor](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5e523-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="5e523-117">Registos de lista da base de dados do Azure para o servidor de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="5e523-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="5e523-118">os ficheiros de registo disponível do toolist hello do servidor, execute Olá [lista de registos do servidor de postgres az](/cli/azure/postgres/server-logs#list) comando.</span><span class="sxs-lookup"><span data-stu-id="5e523-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="5e523-119">Pode listar os ficheiros de registo de Olá para servidor **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup**e direcionar o mesmo texto tooa ficheiro chamado **registo\_ficheiros\_list.txt.**</span><span class="sxs-lookup"><span data-stu-id="5e523-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="5e523-120">Transferir localmente os registos do servidor de Olá</span><span class="sxs-lookup"><span data-stu-id="5e523-120">Download logs locally from hello server</span></span>
<span data-ttu-id="5e523-121">Olá [az postgres-registos do servidor transferir](/cli/azure/postgres/server-logs#download) comando permite-lhe ficheiros de registo individuais toodownload para o servidor.</span><span class="sxs-lookup"><span data-stu-id="5e523-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="5e523-122">Neste exemplo Olá, transferências de ficheiros de registo específico para o servidor de Olá **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup** tooyour de ambiente local.</span><span class="sxs-lookup"><span data-stu-id="5e523-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="5e523-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5e523-123">Next steps</span></span>
- <span data-ttu-id="5e523-124">toolearn mais informações sobre os registos do servidor, consulte [registos do servidor na base de dados do Azure para PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="5e523-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="5e523-125">Para obter mais informações sobre os parâmetros de servidor, consulte [personalizar parâmetros de configuração de servidor utilizando a CLI do Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="5e523-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
