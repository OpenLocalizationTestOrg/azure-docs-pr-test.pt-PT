---
title: "aaaAzure extensão da máquina virtual de agente do observador de rede para Linux | Microsoft Docs"
description: "Implemente Olá agente do observador de rede na máquina de virtual com Linux utilizando uma extensão da máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Extensão da máquina virtual de agente do observador de rede para Linux

## <a name="overview"></a>Descrição geral

[Observador de rede do Azure](https://review.docs.microsoft.com/en-us/azure/network-watcher/) é um serviço de monitorização, diagnóstico e análise de desempenho de rede que permite a monitorização de redes do Azure. Olá extensão da máquina virtual de agente do observador de rede é um requisito para algumas das funcionalidades de observador de rede Olá em máquinas virtuais do Azure. Isto inclui capturar o tráfego de rede a pedido e outras funcionalidades avançadas.

Olá de detalhes deste documento suportado plataformas e opções de implementação para Olá extensão da máquina virtual de agente do observador de rede para Linux.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema operativo

Olá extensão de agente do observador de rede pode ser executada relativamente a estes distribuições do Linux:

| Distribuição | Versão |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS e 12.04 LTS |
| Debian | 7 e 8 |
| RedHat | 6 e 7. x |
| Oracle Linux | 7 x |
| SUSE | 11 e 12 |
| OpenSuse | 7.0 |
| CentOS | 7.0 |

Tenha em atenção que CoreOS não é suportado neste momento.

### <a name="internet-connectivity"></a>Conectividade Internet

Algumas das funcionalidades do agente do observador de rede de Olá requer uma máquina virtual de destino que Olá toohello ligado à Internet. Sem ligações de saída Olá capacidade tooestablish algumas das funcionalidades do agente do observador de rede de Olá podem avaria ou ficar indisponíveis. Para obter mais detalhes, consulte Olá [documentação de observador de rede](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

## <a name="extension-schema"></a>Esquema de extensão

Olá seguinte JSON mostra esquema Olá para Olá extensão de agente do observador de rede. extensão de Olá nem requer nem suporta as definições fornecido pelo utilizador neste momento e baseia-se na sua configuração predefinida.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Valores de propriedade

| Nome | Valor / exemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Fabricante | Microsoft.Azure.NetworkWatcher |
| tipo | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Implementação de modelos

Extensões VM do Azure podem ser implementadas com modelos Azure Resource Manager. esquema JSON Olá descrita na secção anterior Olá pode ser utilizada numa Olá de toorun de modelo Azure Resource Manager extensão de agente do observador de rede durante uma implementação de modelo Azure Resource Manager.

## <a name="azure-cli-deployment"></a>Implementação da CLI do Azure

Olá CLI do Azure pode ser utilizado toodeploy Olá VM de agente do observador de rede extensão tooan máquina virtual existente.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Resolução de problemas e suporte

### <a name="troubleshooting"></a>Resolução de problemas

Dados sobre o estado de Olá das implementações de extensão de podem ser obtidos a partir da Olá portal do Azure e utilizando Olá CLI do Azure. Estado de implementação de Olá toosee das extensões para uma determinada VM, execute Olá utilizando o comando a seguir Olá CLI do Azure.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Execução de extensão de saída é iniciada toofiles encontrado no Olá seguinte diretório:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Suporte

Se precisar de mais ajuda, a qualquer altura neste artigo, pode consulte a documentação do toohello observador de rede ou contactar Olá Azure peritos em Olá [fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/en-us/support/forums/). Em alternativa, pode ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione o suporte de Get. Para obter informações sobre como utilizar o suporte do Azure, leia o artigo Olá [suporte do Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
