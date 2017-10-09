---
title: "aaaAzure CLI Script de exemplo - encaminhar o tráfego para elevada disponibilidade de aplicações | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - encaminhar o tráfego para elevada disponibilidade de aplicações"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Encaminhar o tráfego para elevada disponibilidade de aplicações

Este script cria um grupo de recursos, dois planos de serviço de aplicações, duas aplicações web, um perfil do Gestor de tráfego e dois pontos finais Gestor de tráfego. Gestor de tráfego direciona o tráfego toohello aplicação uma região como região primária Olá e região secundária toohello quando a aplicação Olá na região primária Olá não está disponível. Antes de executar o script de Olá, tem de alterar Olá MyWebApp, MyWebAppL1 e MyWebAppL2 valores toounique valores em todo o Azure. Depois de executar o script de Olá, pode aceder à aplicação Olá na região primária de Olá com Olá URL mywebapp.trafficmanager.net.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a>Limpar a implementação 

Depois de executar o script de exemplo Olá, Olá siga pode ser utilizado tooremove grupo de recursos de Olá, do serviço de aplicações aplicação e todos os recursos relacionados.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, de aplicação web, de perfil do Gestor de tráfego e todos os recursos relacionados. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar plano de serviço aplicacional AZ](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Cria um plano de serviço de aplicações. Trata-se como um farm de servidores para a sua aplicação web do Azure. |
| [criar web de serviço aplicacional AZ](https://docs.microsoft.com/cli/azure/appservice/web#create) | Cria uma aplicação web do Azure dentro Olá plano do App Service. |
| [Criar perfil de Gestor de tráfego de rede AZ](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Cria um perfil do Traffic Manager do Azure. |
| [criar o ponto final do Gestor de tráfego de rede AZ](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Adiciona um ponto final tooan perfil do Traffic Manager do Azure. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script de aplicação serviço CLI adicionais podem ser encontrados na Olá [redes do Azure documentação](../cli-samples.md).
