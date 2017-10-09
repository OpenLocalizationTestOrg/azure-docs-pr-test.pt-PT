---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação web e implementar o código do repositório de Git local | Microsoft Docs"
description: "Exemplo de Script do CLI do Azure - criar uma aplicação web e implementar o código do repositório de Git local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a>Criar uma aplicação web e implementar o código do repositório de Git local

Este script de exemplo cria uma aplicação web no App Service com os respetivos recursos relacionados e, em seguida, implementa o código de aplicação web num repositório de Git local.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar plano de serviço aplicacional AZ](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Cria um plano de serviço de aplicações. |
| [Criar AZ webapp](https://docs.microsoft.com/cli/azure/webapp#create) | Cria uma aplicação web do Azure. |
| [utilizador AZ webapp implementação definido](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | Define as credenciais de implementação de nível de conta de Olá para serviço de aplicações. |
| [origem de implementação webapp com AZ-config-local-git](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | Cria uma configuração de controlo de origem para um repositório de Git local. |
| [Procurar de webapp AZ](https://docs.microsoft.com/cli/azure/webapp#browse) | Abra uma aplicação web do Azure num browser. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [documentação do App Service do Azure](../app-service-cli-samples.md).
