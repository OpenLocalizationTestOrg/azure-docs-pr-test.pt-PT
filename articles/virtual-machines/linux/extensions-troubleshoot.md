---
title: "aaaTroubleshooting VM com Linux falhas de extensão | Microsoft Docs"
description: "Saiba mais sobre a resolução de falhas de extensão de VM do Linux do Azure"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Resolução de falhas de extensão de VM do Linux do Azure
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Visualizar o estado de extensão
Modelos Azure Resource Manager podem ser executados a partir Olá CLI do Azure. Assim que o modelo de Olá é executado, pode ser visualizado estado da extensão Olá Explorador de recursos do Azure ou Olá ferramentas de linha de comandos.

Segue-se um exemplo:

CLI do Azure:

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>Resolução de falhas de Extenson:
### <a name="re-running-hello-extension-on-hello-vm"></a>Executar novamente a extensão de Olá no Olá VM
Se estiver a executar scripts num Olá VM utilizando a extensão de Script personalizado, por vezes, é possível executar um erro em que a VM foi criada com êxito mas Olá script falhou. Nestes conditons Olá recomendado toorecover de forma do erro tooremove Olá extensão e novamente o modelo de Olá.
Nota: No futuro, esta funcionalidade seria tooremove avançada Olá necessidade para desinstalar a extensão de Olá.

#### <a name="remove-hello-extension-from-azure-cli"></a>Remover extensão de Olá da CLI do Azure
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Onde "publsher-name" corresponde ao tipo de extensão de toohello da saída de Olá de "get-instância-vista da vm do azure" e o nome é Olá nome do recurso de extensão de Olá a partir do modelo de Olá

Assim que tiver sido removido extensão Olá, o modelo de Olá pode ser novamente executado toorun Olá scripts no Olá VM.

