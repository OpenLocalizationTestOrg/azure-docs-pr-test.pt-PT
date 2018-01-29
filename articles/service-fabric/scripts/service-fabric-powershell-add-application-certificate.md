---
title: "Script do PowerShell do Azure de exemplo - adicionar o certificado de aplicação para um cluster | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - adicionar um certificado de aplicação para um cluster do Service Fabric."
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
ms.topic: sample
ms.date: 01/18/2018
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: c9cf6485c2621f839b93da162e5f4d82a8d287a4
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/19/2018
---
# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a>Adicionar um certificado de aplicação para um cluster do Service Fabric

Este script de exemplo cria um certificado autoassinado no Cofre de chave do Azure especificado e instala-o a todos os nós do cluster Service Fabric. O certificado também transferências para uma pasta local. O nome do certificado transferido é igual ao nome do certificado no Cofre de chaves. Personalize os parâmetros conforme necessário.

Se necessário, instale o Azure PowerShell com a instrução foi encontrada no [Guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma ligação com o Azure. 

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate to a cluster")]

## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos: cada comando nas ligações de tabela para a documentação específica do comando.

| Comando | Notas |
|---|---|
| [Add-AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Adicione um novo certificado de aplicação para o conjunto de dimensionamento de máquina virtual que compõem o cluster.  |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre o módulo Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Amostras de Azure Powershell adicionais para o Azure Service Fabric podem ser encontradas no [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).
