---
title: "Criar a sua primeira função a partir da CLI do Azure | Microsoft Docs"
description: "Saiba como criar a sua primeira Função do Azure para execução sem servidor através da CLI do Azure."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 11/08/2017
ms.topic: quickstart
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: cfowler
ms.openlocfilehash: 4356d00b2694224f52a9359cd4a57d3a70a34d18
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/15/2017
---
# <a name="create-your-first-function-using-the-azure-cli"></a>Criar a sua primeira função com a CLI do Azure

Este tópico do guia de introdução mostra-lhe como utilizar as Funções do Azure para criar a sua primeira função. Vai utilizar a CLI do Azure para criar uma aplicação de funções, que é a infraestrutura [sem servidor](https://azure.microsoft.com/overview/serverless-computing/) que aloja a sua função. O código da função propriamente dito é implementado a partir de um repositório de exemplos do GitHub.    

Pode seguir os passos abaixo num computador Mac, Windows ou Linux. 

## <a name="prerequisites"></a>Pré-requisitos 

Antes de executar este exemplo, tem de ter o seguinte:

+ Uma conta do [GitHub](https://github.com) ativa. 
+ Uma subscrição ativa do Azure.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se optar por instalar e usar a CLI localmente, este tópico requer a execução da versão 2.0 ou posterior da CLI do Azure. Execute `az --version` para localizar a versão atual. Se precisar de instalar ou atualizar, veja [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 


[!INCLUDE [functions-create-resource-group](../../includes/functions-create-resource-group.md)]

[!INCLUDE [functions-create-storage-account](../../includes/functions-create-storage-account.md)]

## <a name="create-a-function-app"></a>Criar uma aplicação de função

Precisa de uma aplicação Function App para alojar a execução das suas funções. A aplicação Function App proporciona um ambiente para a execução sem servidor do código da sua função. Permite-lhe agrupar funções como unidades lógicas para uma gestão, implementação e partilha de recursos mais fácil. Utilize o comando [az functionapp create](/cli/azure/functionapp#create) para criar uma aplicação Function App. 

No comando seguinte, substitua o nome da sua aplicação de funções exclusivo onde vir o marcador de posição `<app_name>` e o nome da conta de armazenamento para `<storage_name>`. O `<app_name>` vai ser utilizado como o domínio DNS predefinido para a aplicação Function App, daí que o nome tenha de ser exclusivo em todas as aplicações no Azure. O parâmetro _deployment-source-url_ é um repositório de exemplo no GitHub que contém uma função acionada por HTTP "Hello World".

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope --deployment-source-url https://github.com/Azure-Samples/functions-quickstart
```
Definir o parâmetro _consumption-plan-location_ significa que a aplicação de funções é alojada num plano de alojamento de Consumo. Neste plano, os recursos são adicionados dinamicamente conforme exigido pelas suas funções e paga apenas quando as funções estão em execução. Para obter mais informações, veja [Choose the correct hosting plan](functions-scale.md) (Escolher o plano de alojamento certo). 

Depois de a aplicação Function App ter sido criada, a CLI do Azure mostra informações semelhantes às do exemplo seguinte:

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

[!INCLUDE [functions-test-function-code](../../includes/functions-test-function-code.md)]

[!INCLUDE [functions-cleanup-resources](../../includes/functions-cleanup-resources.md)]

[!INCLUDE [functions-quickstart-next-steps-cli](../../includes/functions-quickstart-next-steps-cli.md)]