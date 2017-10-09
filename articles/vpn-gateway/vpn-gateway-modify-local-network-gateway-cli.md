---
title: "Modificar os prefixos de endereços IP de gateway de rede local de Olá e endereço de IP do Gateway de VPN Olá | Azure | CLI | Microsoft Docs"
description: "Este artigo explica como alterar os prefixos de endereços IP para o gateway de rede local utilizando Olá CLI do Azure."
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
ms.openlocfilehash: 4b8bbf3e9d3d42ac2d12f87360fa0a4134c57a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a>Modificar as definições do gateway de rede local utilizando Olá CLI do Azure

Por vezes, alterar definições de Olá para o seu prefixo de endereço de gateway de rede local ou o endereço IP do Gateway. Este artigo mostra como toomodify as definições do gateway de rede local. Também pode modificar estas definições utilizando um método diferente ao selecionar uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [CLI do Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Antes de começar

Instale a versão mais recente do Olá dos comandos da CLI Olá (2.0 ou posteriores). Para obter informações sobre a instalação de comandos da CLI Olá, consulte [instalar o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="ipaddprefix"></a>Modificar os prefixos de endereço IP

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <a name="gwip"></a>Modificar o endereço IP do gateway Olá

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a>Passos seguintes

Pode verificar a ligação de gateway. Consulte [verificar uma ligação de gateway](vpn-gateway-verify-connection-resource-manager.md).

