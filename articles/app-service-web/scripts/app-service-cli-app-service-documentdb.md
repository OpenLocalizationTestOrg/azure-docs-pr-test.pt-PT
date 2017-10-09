---
title: "aaaAzure CLI Script de exemplo - ligar um tooCosmos de aplicação web DB | Microsoft Docs"
description: "Script CLI do Azure de exemplo - ligar um tooCosmos de aplicação web DB"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a>Ligar um tooCosmos de aplicação web DB

Neste cenário ficará a saber como toocreate uma conta de base de dados do Azure Cosmos e um Azure aplicação web. Em seguida, vai ligar a aplicação web Olá Cosmos DB toohello utilizando as definições de aplicação.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, aplicação web, base de dados do Cosmos e relacionados todos os recursos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar plano de serviço aplicacional AZ](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Cria um plano de serviço de aplicações. Trata-se como um farm de servidores para a sua aplicação web do Azure. |
| [Criar AZ webapp](https://docs.microsoft.com/cli/azure/webapp#create) | Cria uma aplicação web do Azure. |
| [Criar AZ cosmosdb](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | Cria uma conta de base de dados do Cosmos. Este é onde os dados de Olá serão armazenados. |
| [AZ cosmosdb lista de chaves](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | Apresenta uma lista de chaves de acesso de Olá para Olá especificar conta de base de dados do Cosmos. |
| [AZ webapp configuração appsettings conjunto](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Cria ou atualiza uma definição de aplicação para uma aplicação web do Azure. As definições de aplicação são expostas como variáveis de ambiente para a sua aplicação. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).
