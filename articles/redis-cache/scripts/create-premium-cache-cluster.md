---
title: aaaAzure CLI Script de exemplo - criar uma Cache de Redis do Azure Premium com clustering | Microsoft Docs
description: "Script CLI do Azure de exemplo - criação de um escalão Premium a Cache de Redis do Azure com o clustering"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a>Criar uma Cache de Redis do Azure Premium com clustering

Neste cenário, saiba como toocreate ativado um escalão Premium da 6 GB a Cache de Redis do Azure com o clustering e duas partições horizontais.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos e uma cache de redis do escalão Premium com clustering de ativação. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar AZ redis](https://docs.microsoft.com/cli/azure/redis#create) | Crie uma instância da Cache de Redis. |


## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de Cache de Redis do Azure adicionais podem ser encontrados na Olá [documentação de Cache de Redis do Azure](../cli-samples.md).
