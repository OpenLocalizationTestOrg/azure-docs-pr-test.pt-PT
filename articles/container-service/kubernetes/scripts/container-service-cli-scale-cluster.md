---
title: um Cluster de ACS de escala aaaAzure CLI Script de exemplo - | Microsoft Docs
description: Exemplo de Script do CLI do Azure - escala um Cluster de ACS
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contentores, Microsserviços, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: nepeters
ms.openlocfilehash: 1e07518fc2ca67476d9ef64bb22d75f848a37e43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-an-azure-container-service-cluster"></a>Dimensionar um Cluster do serviço de contentor do Azure

Este exemplo escalas e o serviço de contentor do Azure. 

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

```azurecli
az acs scale --resource-group myResourceGroup --name myK8SCluster --new-agent-count 5
```

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá após a implementação de Olá toocreate de comandos. Cada item na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [escala de acs AZ](/cli/azure/acs#scale) | Dimensione um cluster de ACS. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de serviço de contentor do Azure adicionais podem ser encontrados na Olá [documentação do serviço de contentor Azure](../cli-samples.md).

