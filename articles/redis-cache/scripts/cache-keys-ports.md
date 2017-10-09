---
title: "aaaAzure CLI Script de exemplo - Olá hostname Get, portas e as chaves para a Cache de Redis do Azure | Microsoft Docs"
description: "Azure CLI Script de exemplo - o nome de anfitrião do Get Olá, portas e as chaves de uma instância da Cache de Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 761eb24e-2ba7-418d-8fc3-431153e69a90
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: e6e794558087d6568438c439e2bf99fc46eeb8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-hostname-ports-and-keys-for-azure-redis-cache"></a>Obter nome de anfitrião Olá, portas e as chaves para a Cache de Redis do Azure

Neste cenário, saiba como o nome de anfitrião do tooretrieve Olá, portas e as chaves utilizadas instância do tooconnect tooan a Cache de Redis do Azure.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/redis-cache/cache-keys-ports/cache-keys-ports.sh "Azure Redis Cache")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos tooretrieve Olá hostname, chaves e as portas de uma instância da Cache de Redis do Azure. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Mostrar de redis AZ](https://docs.microsoft.com/cli/azure/redis#show) | Obter os detalhes de uma instância da Cache de Redis do Azure. |
| [AZ lista-as chaves de redis](https://docs.microsoft.com/cli/azure/redis#list-keys) | Obter chaves de acesso para uma instância da Cache de Redis do Azure. |


## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de Cache de Redis do Azure adicionais podem ser encontrados na Olá [documentação de Cache de Redis do Azure](../cli-samples.md).
