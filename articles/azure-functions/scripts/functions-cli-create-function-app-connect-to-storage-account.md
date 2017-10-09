---
title: "aaaCreate uma função do Azure que liga tooan Storage do Azure | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar uma função do Azure que liga tooan Storage do Azure"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a>Integrar a aplicação de função na conta do Storage do Azure

Este script de exemplo cria uma aplicação de função e a conta de armazenamento.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de exemplo

Este exemplo cria uma aplicação de função do Azure e adiciona a definição de aplicação de tooan ligação cadeia Olá armazenamento.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a>Limpar a implementação

Depois de executar o script de exemplo Olá, Olá seguinte comando pode ser utilizado tooremove grupo de recursos de Olá, do serviço de aplicações aplicação e todos os recursos relacionados:

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [início de sessão AZ](https://docs.microsoft.com/cli/azure/#login) | TooAzure de início de sessão. |
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Criar um grupo de recursos com a localização |
| [criar conta de armazenamento AZ](https://docs.microsoft.com/cli/azure/storage/account) | Criar uma conta de armazenamento |
| [Criar AZ functionapp](https://docs.microsoft.com/cli/azure/functionapp#create) | Criar uma nova aplicação de função |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/group#delete) | Limpeza |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de funções do Azure adicionais podem ser encontrados na Olá [documentação de funções do Azure](../functions-cli-samples.md).
