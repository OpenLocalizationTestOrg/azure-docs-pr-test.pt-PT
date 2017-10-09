---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação web do ASP.NET Core num contentor Docker | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma aplicação web do ASP.NET Core num contentor Docker"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 23106345bfbbf1f68757d99010db98e7c9a7da49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a>Criar uma aplicação web do ASP.NET Core num contentor Docker

Neste cenário, ficará a saber como toocreate um grupo de recursos, a aplicação do Linux plano e a aplicação web service e implementar uma aplicação ASP.NET Core utilizar um contentor de Docker.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, web aplicação e todos os recursos relacionados. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar plano de serviço aplicacional AZ](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Cria um plano de serviço de aplicações. Trata-se como um farm de servidores para a sua aplicação web do Azure. |
| [Criar AZ webapp](https://docs.microsoft.com/cli/azure/webapp#create) | Cria uma aplicação web do Azure. |
| [conjunto de contentor de configuração do AZ webapp](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | Define o contentor de Docker Olá para aplicação de web do Azure Olá. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).
