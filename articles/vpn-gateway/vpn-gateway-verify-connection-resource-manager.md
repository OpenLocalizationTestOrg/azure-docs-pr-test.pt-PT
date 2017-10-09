---
title: "aaaVerify uma ligação do VPN Gateway | Microsoft Docs"
description: "Este artigo mostra como tooverify a virtual rede de ligação do Gateway de VPN."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="d53ee-103">Certifique-se de uma ligação de Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="d53ee-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="d53ee-104">Este artigo mostra como tooverify uma ligação de gateway VPN para Olá clássico e modelos de implementação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d53ee-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="d53ee-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d53ee-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="d53ee-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d53ee-106">PowerShell</span></span>

<span data-ttu-id="d53ee-107">tooverify uma ligação de gateway VPN para Olá implementação do Resource Manager através do PowerShell de modelo, instale a versão mais recente do Olá do Olá [cmdlets do Azure Resource Manager PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d53ee-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="d53ee-108">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d53ee-108">Azure CLI</span></span>

<span data-ttu-id="d53ee-109">tooverify uma ligação de gateway VPN para Olá implementação do Resource Manager modelo a utilizar a CLI do Azure, instale a versão mais recente do Olá do Olá [comandos da CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="d53ee-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="d53ee-110">Portal do Azure (clássica)</span><span class="sxs-lookup"><span data-stu-id="d53ee-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="d53ee-111">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="d53ee-111">PowerShell (classic)</span></span>

<span data-ttu-id="d53ee-112">tooverify a ligação de gateway VPN para a implementação clássico Olá modelo com o PowerShell, instalar versões mais recentes do Olá das Olá cmdlets Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d53ee-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="d53ee-113">Ser se Olá toodownload e instalar [gestão de serviço](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) módulo.</span><span class="sxs-lookup"><span data-stu-id="d53ee-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="d53ee-114">Utilize o Add-AzureAccount toolog no modelo de implementação clássica toohello.</span><span class="sxs-lookup"><span data-stu-id="d53ee-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d53ee-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d53ee-115">Next steps</span></span>

* <span data-ttu-id="d53ee-116">Pode adicionar redes virtuais do tooyour máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d53ee-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="d53ee-117">Veja [Criar uma Máquina Virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter os passos.</span><span class="sxs-lookup"><span data-stu-id="d53ee-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
