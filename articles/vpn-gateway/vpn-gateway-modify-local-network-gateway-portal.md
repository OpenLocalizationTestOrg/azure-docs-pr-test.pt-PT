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
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>Modificar as definições do gateway de rede local utilizando Olá portal do Azure

Por vezes, Olá as definições para o gateway de rede local AddressPrefix ou GatewayIPAddress alterar. Este artigo mostra como toomodify as definições do gateway de rede local. Também pode modificar estas definições utilizando um método diferente ao selecionar uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [CLI do Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>Modificar os prefixos de endereço IP

Ao modificar os prefixos de endereços IP, os passos de Olá que seguir dependem se o gateway de rede local tem uma ligação.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>Modificar o endereço IP do gateway Olá

Se o dispositivo VPN de Olá que pretende que o tooconnect toohas alterar o respetivo endereço IP público, tem de toomodify Olá rede local gateway tooreflect que alteram. Quando alterar o endereço IP público Olá, os passos de Olá que seguir dependem se o gateway de rede local tem uma ligação.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>Passos seguintes

Pode verificar a ligação de gateway. Consulte [verificar uma ligação de gateway](vpn-gateway-verify-connection-resource-manager.md).