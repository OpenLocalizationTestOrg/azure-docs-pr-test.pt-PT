---
title: "máquinas virtuais do Windows aaaRedeploy no Azure | Microsoft Docs"
description: "Como problemas de máquinas virtuais do Windows tooredeploy na ligação de RDP toomitigate do Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Reimplementar toonew de máquina virtual do Windows Azure nó
Se ter sido enfrentam dificuldades resolução de problemas de ambiente de trabalho remoto (RDP) ligação ou a aplicação o acesso baseado em tooWindows máquina virtual do Azure (VM), reimplementação Olá pode ajudar a VM. Quando voltar a implementar uma VM, este move Olá VM tooa novo nó dentro Olá infraestrutura do Azure e, em seguida, for ligado-la novamente, manter todas as suas opções de configuração e os recursos associados. Este artigo mostra como tooredeploy uma VM com o Azure PowerShell ou Olá portal do Azure.

> [!NOTE]
> Depois de voltar a implementar uma VM, disco temporário Olá perde-se e endereços IP dinâmicos associados à interface de rede virtual foram atualizados. 


## <a name="using-azure-powershell"></a>Utilizar o Azure PowerShell
Certifique-se de ter hello mais recente do Azure PowerShell 1. x instalado no seu computador. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

Olá exemplo seguinte implementa Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Passos seguintes
Se estiver a ter problemas em ligar tooyour VM, pode encontrar ajuda específica no [resolução de problemas nas ligações RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [RDP passos de resolução de problemas de detalhado](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Se não conseguir aceder uma aplicação em execução na sua VM, pode ainda ler [aplicação resolução de problemas](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

