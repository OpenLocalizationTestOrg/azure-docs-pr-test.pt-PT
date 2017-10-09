---
title: "falhas de extensão de VM do Windows aaaTroubleshooting | Microsoft Docs"
description: "Saiba mais sobre a resolução de falhas de extensão de VM do Windows Azure"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Resolução de falhas de extensão de VM do Windows Azure
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Visualizar o estado de extensão
Modelos Azure Resource Manager podem ser executados a partir do Azure PowerShell. Assim que o modelo de Olá é executado, pode ser visualizado estado da extensão Olá Explorador de recursos do Azure ou Olá ferramentas de linha de comandos.

Segue-se um exemplo:

O Azure PowerShell:

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

O resultado de exemplo de Olá é:

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extension-failures"></a>Resolução de problemas de falhas de extensão
### <a name="re-running-hello-extension-on-hello-vm"></a>Executar novamente a extensão de Olá no Olá VM
Se estiver a executar scripts num Olá VM utilizando a extensão de Script personalizado, por vezes, é possível executar um erro em que a VM foi criada com êxito mas Olá script falhou. Nestes conditons Olá recomendado toorecover de forma do erro tooremove Olá extensão e novamente o modelo de Olá.
Nota: No futuro, esta funcionalidade seria tooremove avançada Olá necessidade para desinstalar a extensão de Olá.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Remover extensão de Olá do Azure PowerShell
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Assim que tiver sido removido extensão Olá, o modelo de Olá pode ser novamente executado toorun Olá scripts no Olá VM.

