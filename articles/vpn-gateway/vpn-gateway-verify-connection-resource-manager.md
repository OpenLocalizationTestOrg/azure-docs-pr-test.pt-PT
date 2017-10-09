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
# <a name="verify-a-vpn-gateway-connection"></a>Certifique-se de uma ligação de Gateway de VPN

Este artigo mostra como tooverify uma ligação de gateway VPN para Olá clássico e modelos de implementação do Resource Manager.

## <a name="azure-portal"></a>Portal do Azure

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a>PowerShell

tooverify uma ligação de gateway VPN para Olá implementação do Resource Manager através do PowerShell de modelo, instale a versão mais recente do Olá do Olá [cmdlets do Azure Resource Manager PowerShell](/powershell/azure/overview).

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a>CLI do Azure

tooverify uma ligação de gateway VPN para Olá implementação do Resource Manager modelo a utilizar a CLI do Azure, instale a versão mais recente do Olá do Olá [comandos da CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 ou posterior).

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a>Portal do Azure (clássica)

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a>PowerShell (clássico)

tooverify a ligação de gateway VPN para a implementação clássico Olá modelo com o PowerShell, instalar versões mais recentes do Olá das Olá cmdlets Azure PowerShell. Ser se Olá toodownload e instalar [gestão de serviço](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) módulo. Utilize o Add-AzureAccount toolog no modelo de implementação clássica toohello.

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a>Passos seguintes

* Pode adicionar redes virtuais do tooyour máquinas virtuais. Veja [Criar uma Máquina Virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter os passos.
