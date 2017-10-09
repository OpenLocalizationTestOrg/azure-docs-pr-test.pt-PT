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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="1ece5-103">Reimplementar toonew de máquina virtual do Windows Azure nó</span><span class="sxs-lookup"><span data-stu-id="1ece5-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="1ece5-104">Se ter sido enfrentam dificuldades resolução de problemas de ambiente de trabalho remoto (RDP) ligação ou a aplicação o acesso baseado em tooWindows máquina virtual do Azure (VM), reimplementação Olá pode ajudar a VM.</span><span class="sxs-lookup"><span data-stu-id="1ece5-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="1ece5-105">Quando voltar a implementar uma VM, este move Olá VM tooa novo nó dentro Olá infraestrutura do Azure e, em seguida, for ligado-la novamente, manter todas as suas opções de configuração e os recursos associados.</span><span class="sxs-lookup"><span data-stu-id="1ece5-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="1ece5-106">Este artigo mostra como tooredeploy uma VM com o Azure PowerShell ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ece5-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="1ece5-107">Depois de voltar a implementar uma VM, disco temporário Olá perde-se e endereços IP dinâmicos associados à interface de rede virtual foram atualizados.</span><span class="sxs-lookup"><span data-stu-id="1ece5-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="1ece5-108">Utilizar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ece5-108">Using Azure PowerShell</span></span>
<span data-ttu-id="1ece5-109">Certifique-se de ter hello mais recente do Azure PowerShell 1. x instalado no seu computador.</span><span class="sxs-lookup"><span data-stu-id="1ece5-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="1ece5-110">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1ece5-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="1ece5-111">Olá exemplo seguinte implementa Olá VM com o nome `myVM` no grupo de recursos de Olá designado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="1ece5-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="1ece5-112">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1ece5-112">Next steps</span></span>
<span data-ttu-id="1ece5-113">Se estiver a ter problemas em ligar tooyour VM, pode encontrar ajuda específica no [resolução de problemas nas ligações RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [RDP passos de resolução de problemas de detalhado](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ece5-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1ece5-114">Se não conseguir aceder uma aplicação em execução na sua VM, pode ainda ler [aplicação resolução de problemas](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ece5-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

