---
title: "aaaAzure exemplo de Script do PowerShell - dimensionar uma aplicação web em todo o mundo com uma arquitetura de elevada disponibilidade | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - escala uma aplicação web em todo o mundo com uma arquitetura de elevada disponibilidade"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a>Dimensionar uma aplicação web em todo o mundo com uma arquitetura de elevada disponibilidade

Neste cenário, irá criar um grupo de recursos, dois planos de serviço de aplicações, duas aplicações web, um perfil do Gestor de tráfego e dois pontos finais Gestor de tráfego. Após a conclusão do exercício de Olá terá um elevado disponível arquitetura que permite que fornece disponibilidade global da sua aplicação web com base na latência de rede mais baixa Olá.

Se necessário, instale Olá, Azure PowerShell, utilizando a instrução de Olá encontrado no Olá [Guia do Azure PowerShell](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma ligação com o Azure.

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Depois de executar o script de exemplo Olá, Olá os seguintes comandos pode ser utilizados tooremove grupo de recursos de Olá, web aplicação e todos os recursos relacionados.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Novo-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Novo AzureRMTrafficManagerProfile](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | Cria um perfil do Traffic Manager. |
| [Novo AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Cria um plano de serviço de aplicações. |
| [Novo AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Cria uma aplicação web. |
| [Novo AzureRMTrafficManagerEndpoint](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | Cria um ponto final num perfil do Traffic Manager. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos do Azure Powershell adicionais para Web Apps do Azure App Service podem ser encontrados na Olá [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).
