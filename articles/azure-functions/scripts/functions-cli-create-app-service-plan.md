---
title: "aaaAzure CLI Script de exemplo - criar uma aplicação de função num plano do serviço de aplicações | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma aplicação de função num plano do serviço de aplicações"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a>Criar uma aplicação de função num plano do serviço de aplicações

Este script de exemplo cria uma aplicação de função do Azure, que é um contentor para as suas funções. Olá aplicação de função é criada utilizando um plano de serviço aplicacional dedicado, o que significa que os recursos do servidor estão sempre ativos.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

Este script cria uma aplicação de função do Azure utilizando um dedicado [plano do App Service](../functions-scale.md#app-service-plan).

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação de script

Cada comando na tabela de Olá contém ligações a documentação específica toocommand. Este script utiliza Olá os seguintes comandos:

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [criar conta de armazenamento AZ](https://docs.microsoft.com/cli/azure/storage/account#create) | Cria uma conta de armazenamento do Azure. |
| [Criar plano de serviço aplicacional AZ](https://docs.microsoft.com/cli/azure/appserviceplan#create) | Cria um plano de serviço de aplicações. |
| [Criar AZ functionapp](https://docs.microsoft.com/cli/azure/functionapp#delete) | Cria uma aplicação de função do Azure. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de funções do Azure adicionais podem ser encontrados na Olá [documentação de funções do Azure](../functions-cli-samples.md).
