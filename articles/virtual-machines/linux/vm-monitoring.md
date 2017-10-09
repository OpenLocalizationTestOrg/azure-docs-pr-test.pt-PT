---
title: "aaaEnable ou desativar a monitorização de VM do Azure"
description: "Descreve como tooEnable ou desativar a monitorização de VM do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Ativar ou desativar a monitorização de VM do Azure

Esta secção descreve como tooenable ou desativar a monitorização em Virtual máquinas em execução no Azure. Pode ativar ou desativar a monitorização utilizando o portal de Olá ou Interface de linha de comandos do Azure para Mac, Linux e Windows (Olá CLI do Azure).

> [!IMPORTANT]
> Este documento descreve a versão 2.3 de Olá extensão diagnóstico de Linux, o que foi preterido. Versão 2.3 será suportada até 30 de Junho de 2018.
>
> Versão 3.0 do Olá que extensão de diagnóstico do Linux em vez disso, pode ser ativada. Para obter mais informações, consulte [Olá documentação](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Ativar / desativar a monitorização Olá através do portal do Azure

Pode ativar a monitorização da sua VM do Azure, que fornecem dados sobre a instância em períodos de 1 minuto. (aplicam alterações de armazenamento). Dados de diagnóstico detalhadas, em seguida, estão disponíveis para Olá VM em gráficos de portal Olá ou através de Olá API. Por predefinição, o portal do Azure permite a monitorização baseadas em anfitrião de um conjunto limitado de métricas. Pode ativar a monitorização de métricas de dentro de uma VM ao hello que VM está em execução ou em estado de paragem.

* Abra Olá Azure portal em [https://portal.azure.com](https://portal.azure.com).
* No Olá deixado de navegação, clique em máquinas virtuais.
* Em Olá máquinas de virtuais de lista, selecione uma instância em execução ou parada. é aberto o painel do Olá "Máquina Virtual".
* Clique em todas as definições.
* Clique em diagnóstico.
* Alterar Estado tooOn ou terminar a sessão. Também pode escolher neste nível de Olá do painel de detalhes que gostaria de tooenable para a máquina virtual de monitorização.

![Ativar / desativar a monitorização através de Olá portal do Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Ativar / desativar a monitorização com a CLI do Azure

tooenable monitorização para uma VM do Azure.

* Crie um ficheiro (com o nome como PrivateConfig.json):

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Ative a extensão de Olá através da CLI do Azure.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Para obter mais informações, consulte [utilizando a extensão de diagnóstico do Linux tooMonitor Linux VM dados de desempenho e diagnóstico](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
