---
title: "Modificar os prefixos de endereços IP de gateway de rede local de Olá e endereço de IP do Gateway de VPN Olá | Azure | Portal | Microsoft Docs"
description: "Este artigo explica como alterar os prefixos de endereços IP para o gateway de rede local utilizando Olá portal do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="bc85c-103">Modificar as definições do gateway de rede local utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc85c-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="bc85c-104">Por vezes, Olá as definições para o gateway de rede local AddressPrefix ou GatewayIPAddress alterar.</span><span class="sxs-lookup"><span data-stu-id="bc85c-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="bc85c-105">Este artigo mostra como toomodify as definições do gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="bc85c-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="bc85c-106">Também pode modificar estas definições utilizando um método diferente ao selecionar uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc85c-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc85c-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc85c-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="bc85c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc85c-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="bc85c-109">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bc85c-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="bc85c-110"><a name="ipaddprefix"></a>Modificar os prefixos de endereço IP</span><span class="sxs-lookup"><span data-stu-id="bc85c-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="bc85c-111">Ao modificar os prefixos de endereços IP, os passos de Olá que seguir dependem se o gateway de rede local tem uma ligação.</span><span class="sxs-lookup"><span data-stu-id="bc85c-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="bc85c-112"><a name="gwip"></a>Modificar o endereço IP do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="bc85c-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="bc85c-113">Se o dispositivo VPN de Olá que pretende que o tooconnect toohas alterar o respetivo endereço IP público, tem de toomodify Olá rede local gateway tooreflect que alteram.</span><span class="sxs-lookup"><span data-stu-id="bc85c-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="bc85c-114">Quando alterar o endereço IP público Olá, os passos de Olá que seguir dependem se o gateway de rede local tem uma ligação.</span><span class="sxs-lookup"><span data-stu-id="bc85c-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="bc85c-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bc85c-115">Next steps</span></span>

<span data-ttu-id="bc85c-116">Pode verificar a ligação de gateway.</span><span class="sxs-lookup"><span data-stu-id="bc85c-116">You can verify your gateway connection.</span></span> <span data-ttu-id="bc85c-117">Consulte [verificar uma ligação de gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bc85c-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>