---
title: amostras de aaaAzure CLI tooscale uma base de dados do Azure para o servidor de MySQL | Microsoft Docs
description: "Este script de exemplo do CLI dimensiona de base de dados do Azure para o nível de desempenho diferentes MySQL servidor tooa depois de consultar as métricas de Olá."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 721ef9db35a5f3be7a38438c1abb724187b18b75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a>Monitorizar e dimensionar uma base de dados do Azure para o servidor de MySQL utilizando a CLI do Azure
Este script de exemplo do CLI dimensiona uma única base de dados do Azure para o nível de desempenho diferentes MySQL servidor tooa depois de consultar as métricas de Olá.

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo
Este script de exemplo, altere Olá realçado linhas toocustomize Olá admin nome de utilizador e palavra-passe. Substitua o id de subscrição de Olá utilizado nos comandos de monitor de az Olá com o seu id de subscrição.[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]

## <a name="clean-up-deployment"></a>Limpar a implementação
Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.
[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete hello resource group.")]

## <a name="script-explanation"></a>Explicação de script
Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| **Comando** | **Notas** |
|---|---|
| [Criar grupo AZ](/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar servidor do AZ mysql](/cli/azure/mysql/server#create) | Cria um servidor de MySQL aloja Olá bases de dados. |
| [lista de métricas de monitor AZ](/cli/azure/monitor/metrics#list) | Olá métrico valor da lista de recursos de Olá. |
| [eliminação do grupo de AZ](/cli/azure/group#delete) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes
- Leia mais informações sobre Olá CLI do Azure: [documentação da CLI do Azure](/cli/azure/overview).
- Tente scripts adicionais: [amostras da CLI do Azure para a base de dados do Azure para MySQL](../sample-scripts-azure-cli.md)
- Para obter mais informações sobre como aumentar, consulte [escalões de serviço](../concepts-service-tiers.md) e [unidades de armazenamento e computação unidades](../concepts-compute-unit-and-storage.md).
