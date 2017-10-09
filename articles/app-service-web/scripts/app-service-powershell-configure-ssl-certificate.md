---
title: "aaaAzure exemplo de Script do PowerShell - vincular uma certificado SSL personalizada aplicação de web de tooa | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - enlace uma aplicação de web do tooa de certificado SSL personalizada"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a>Vincular uma certificado SSL personalizada aplicação de web de tooa

Este script de exemplo cria uma aplicação web no App Service com os respetivos recursos relacionados, em seguida, vincula o certificado SSL Olá um tooit de nome de domínio personalizado. 

Se necessário, instale Olá, Azure PowerShell, utilizando a instrução de Olá encontrado no Olá [Guia do Azure PowerShell](/powershell/azure/overview). Além disso, certifique-se de que:

- Foi criada uma ligação com o Azure utilizando Olá `az login` comando.
- Tem de página de configuração de DNS de acesso tooyour domínio da entidade de registo.
- Tem um válido. Ficheiro PFX e a respetiva palavra-passe para Olá SSL de certificado pretende tooupload e vincular.

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

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
| [Novo AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Cria um plano de serviço de aplicações. |
| [Novo AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Cria uma aplicação web. |
| [Conjunto AzureRmAppServicePlan](/powershell/module/azurerm.websites/set-azurermappserviceplan) | Modifica uma toochange do plano de serviço de aplicações com o escalão de preço. |
| [Conjunto AzureRmWebApp](/powershell/module/azurerm.websites/set-azurermwebapp) | Modifica a configuração de uma aplicação web. |
| [Novo AzureRmWebAppSSLBinding](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | Cria um enlace de certificado SSL para uma aplicação web. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos do Azure Powershell adicionais para Web Apps do Azure App Service podem ser encontrados na Olá [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).
