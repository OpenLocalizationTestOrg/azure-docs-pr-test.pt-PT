---
title: "aaaAuthoring modelos com extensões de VM do Windows | Microsoft Docs"
description: "Saiba mais sobre a criação de modelos Azure Resource Manager com as extensões para VMs do Windows"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Criação de modelos Azure Resource Manager com extensões de VM do Windows
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

A partir do Azure PowerShell, execute Olá seguinte cmdlet do PowerShell do Azure:

      Get-AzureVMAvailableExtension


Este cmdlet devolve o nome do publicador Olá, nome de extensão e versão da seguinte forma:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Estas três propriedades mapeiam demasiado "publisher", "type" e "typeHandlerVersion" respetivamente no Olá acima fragmento de modelo.

> [!NOTE]
> É sempre toouse recomendada Olá mais recente extensão versão tooget Olá atualizada mais funcionalidade.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Identificação Olá esquema para os parâmetros de configuração de extensão Olá
passo seguinte do Olá com criação de um modelo de extensão é o formato de Olá tooidentify para fornecer parâmetros de configuração. Cada extensão suporta o próprio conjunto de parâmetros.

toolook em configurações de exemplo para extensões do Windows, consulte [exemplos de extensões do Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Consulte toohello seguir tooget um modelo totalmente concluído com extensões VM.

[Extensão de Script personalizado na VM do Windows](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Após a criação do modelo de Olá, a poder implementar com o Azure PowerShell.

