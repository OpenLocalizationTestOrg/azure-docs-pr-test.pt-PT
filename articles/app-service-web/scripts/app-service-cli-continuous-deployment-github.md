---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação web com a implementação contínua do GitHub | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma aplicação web com a implementação contínua do GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a>Criar uma aplicação web com a implementação contínua do GitHub

Este script de exemplo cria uma aplicação web no App Service com respetivos recursos relacionados e, em seguida, configura a implementação contínua provém de um repositório do GitHub. Para a implementação do GitHub sem a implementação contínua, consulte [criar uma aplicação web e implementar código a partir do GitHub](app-service-cli-deploy-github.md). Neste exemplo, necessitará de:

* Um repositório do GitHub com código da aplicação, que tem permissões administrativas.
* A [pessoais acesso Token (TERESA)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) para a sua conta do GitHub.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar plano de serviço aplicacional AZ](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Cria um plano de serviço de aplicações. |
| [Criar AZ webapp](https://docs.microsoft.com/cli/azure/webapp#create) | Cria uma aplicação web do Azure. |
| [AZ webapp configuração da origem de implementação](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | Associa um repositório de Git ou Mercurial uma aplicação web do Azure. |
| [Procurar de webapp AZ](https://docs.microsoft.com/cli/azure/webapp#browse) | Abra uma aplicação web do Azure num browser. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).
