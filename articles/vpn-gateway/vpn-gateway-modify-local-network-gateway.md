---
title: "Modificar os prefixos de endereços IP de gateway de rede local de Olá e endereço de IP do Gateway de VPN Olá | Azure | PowerShell | Microsoft Docs"
description: "Este artigo explica como alterar os prefixos de endereços IP para o gateway de rede local com o PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="c7b9f-103">Modificar as definições do gateway de rede local com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7b9f-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="c7b9f-104">Por vezes, Olá as definições para o gateway de rede local AddressPrefix ou GatewayIPAddress alterar.</span><span class="sxs-lookup"><span data-stu-id="c7b9f-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="c7b9f-105">Este artigo mostra como toomodify as definições do gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="c7b9f-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="c7b9f-106">Também pode modificar estas definições utilizando um método diferente ao selecionar uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7b9f-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7b9f-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7b9f-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="c7b9f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7b9f-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="c7b9f-109">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c7b9f-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="c7b9f-110"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c7b9f-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="c7b9f-111">Instale a versão mais recente do Olá do Olá cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c7b9f-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c7b9f-112">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para obter mais informações sobre a instalação de cmdlets do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="c7b9f-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="c7b9f-113"><a name="ipaddprefix"></a>Modificar os prefixos de endereço IP</span><span class="sxs-lookup"><span data-stu-id="c7b9f-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="c7b9f-114"><a name="gwip"></a>Modificar o endereço IP do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="c7b9f-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c7b9f-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c7b9f-115">Next steps</span></span>

<span data-ttu-id="c7b9f-116">Pode verificar a ligação de gateway.</span><span class="sxs-lookup"><span data-stu-id="c7b9f-116">You can verify your gateway connection.</span></span> <span data-ttu-id="c7b9f-117">Consulte [verificar uma ligação de gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c7b9f-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>