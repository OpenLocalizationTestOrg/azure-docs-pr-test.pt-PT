---
title: "aaaAzure exemplo de Script do PowerShell - Adicionar aplicação cert tooa cluster | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - adicionar o cluster do Service Fabric certificado tooa uma aplicação."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Adicionar o cluster do Service Fabric certificado tooa uma aplicação

Este script de exemplo cria um certificado autoassinado no Cofre de chaves do Azure especificado Olá e instala-tooall nós de cluster do Service Fabric Olá. certificado de Olá também transfere tooa de pasta local. nome de Olá do certificado de Olá transferido é Olá igual ao nome de Olá Olá do certificado de no Cofre de chaves Olá. Personalize parâmetros Olá conforme necessário.

Se necessário, instale Olá, Azure PowerShell, utilizando a instrução de Olá encontrado no Olá [Guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` toocreate uma ligação com o Azure. 

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos: cada comando na tabela de Olá ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [AzureRmServiceFabricApplicationCertificate adicionar](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Adicione que um nova aplicação certificado toohello dimensionamento da máquina virtual definir que constituem cluster Olá.  |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Amostras de Azure Powershell adicionais para o Azure Service Fabric podem ser encontradas na Olá [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).
