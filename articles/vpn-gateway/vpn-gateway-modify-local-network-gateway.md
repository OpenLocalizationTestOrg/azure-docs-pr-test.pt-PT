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
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Modificar as definições do gateway de rede local com o PowerShell

Por vezes, Olá as definições para o gateway de rede local AddressPrefix ou GatewayIPAddress alterar. Este artigo mostra como toomodify as definições do gateway de rede local. Também pode modificar estas definições utilizando um método diferente ao selecionar uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [CLI do Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Antes de começar

Instale a versão mais recente do Olá do Olá cmdlets do PowerShell do Azure Resource Manager. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para obter mais informações sobre a instalação de cmdlets do PowerShell Olá.

## <a name="ipaddprefix"></a>Modificar os prefixos de endereço IP

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Modificar o endereço IP do gateway Olá

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Passos seguintes

Pode verificar a ligação de gateway. Consulte [verificar uma ligação de gateway](vpn-gateway-verify-connection-resource-manager.md).