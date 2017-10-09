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
# <a name="modify-local-network-gateway-settings-using-hello-azure-cli"></a><span data-ttu-id="8cde6-103">Modificar as definições do gateway de rede local utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8cde6-103">Modify local network gateway settings using hello Azure CLI</span></span>

<span data-ttu-id="8cde6-104">Por vezes, alterar definições de Olá para o seu prefixo de endereço de gateway de rede local ou o endereço IP do Gateway.</span><span class="sxs-lookup"><span data-stu-id="8cde6-104">Sometimes hello settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="8cde6-105">Este artigo mostra como toomodify as definições do gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="8cde6-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="8cde6-106">Também pode modificar estas definições utilizando um método diferente ao selecionar uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="8cde6-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8cde6-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8cde6-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="8cde6-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cde6-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="8cde6-109">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8cde6-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="8cde6-110"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8cde6-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="8cde6-111">Instale a versão mais recente do Olá dos comandos da CLI Olá (2.0 ou posteriores).</span><span class="sxs-lookup"><span data-stu-id="8cde6-111">Install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="8cde6-112">Para obter informações sobre a instalação de comandos da CLI Olá, consulte [instalar o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8cde6-112">For information about installing hello CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="8cde6-113"><a name="ipaddprefix"></a>Modificar os prefixos de endereço IP</span><span class="sxs-lookup"><span data-stu-id="8cde6-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="8cde6-114"><a name="gwip"></a>Modificar o endereço IP do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="8cde6-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="8cde6-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8cde6-115">Next steps</span></span>

<span data-ttu-id="8cde6-116">Pode verificar a ligação de gateway.</span><span class="sxs-lookup"><span data-stu-id="8cde6-116">You can verify your gateway connection.</span></span> <span data-ttu-id="8cde6-117">Consulte [verificar uma ligação de gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="8cde6-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

