---
title: aaaConnect tooa VM do Windows Server | Microsoft Docs
description: "Saiba como tooconnect e iniciar sessão utilizando o tooa VM do Windows hello do Azure modelo de implementação de Gestor de recursos de portal e Olá."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="bd454-103">Como o registo no tooan virtual do Azure e tooconnect máquina com o Windows</span><span class="sxs-lookup"><span data-stu-id="bd454-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="bd454-104">Irá utilizar Olá **Connect** botão no Olá toostart portal do Azure, uma sessão de ambiente de trabalho remoto (RDP) a partir de um ambiente de trabalho do Windows.</span><span class="sxs-lookup"><span data-stu-id="bd454-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="bd454-105">Ligue primeiro toohello máquina e, em seguida, iniciar sessão.</span><span class="sxs-lookup"><span data-stu-id="bd454-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="bd454-106">Se estiver a tentar tooconnect tooa VM do Windows de um Mac, terá de tooinstall como um cliente RDP para Mac [ambiente de trabalho remoto](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="bd454-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="bd454-107">Ligar a máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="bd454-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="bd454-108">Se ainda não o fez, inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bd454-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bd454-109">No menu do Hub de Olá, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="bd454-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="bd454-110">Selecione a máquina virtual de Olá na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="bd454-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="bd454-111">No painel de Olá para a máquina virtual de Olá, clique em **Connect**.</span><span class="sxs-lookup"><span data-stu-id="bd454-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Captura de ecrã do Olá Mostrar portal do Azure como tooconnect tooyour VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="bd454-113">Se hello **Connect** botão no portal de Olá estiver a cinzento e não são tooAzure ligado através de um [Express Route](../../expressroute/expressroute-introduction.md) ou [VPN Site a Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) ligação, terá de toocreate e Atribua à VM um endereço IP público antes de poder utilizar o RDP.</span><span class="sxs-lookup"><span data-stu-id="bd454-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="bd454-114">Pode ler mais sobre [endereços IP públicos no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bd454-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="bd454-115">Inicie sessão na máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="bd454-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="bd454-116">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bd454-116">Next steps</span></span>
<span data-ttu-id="bd454-117">Caso se depare com problemas quando tenta tooconnect, consulte [ligações de resolução de problemas de ambiente de trabalho remoto](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd454-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="bd454-118">Este artigo orienta-o ao longo do diagnóstico e da resolução de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="bd454-118">This article walks you through diagnosing and resolving common problems.</span></span>

