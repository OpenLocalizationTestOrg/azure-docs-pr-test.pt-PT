---
title: aaaDifferent formas toocreate uma VM do Windows no Azure | Microsoft Docs
description: "Apresenta uma lista de formas diferentes de Olá toocreate uma máquina virtual do Windows com o Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Diferentes formas toocreate máquina virtual do Windows

O Azure oferece diferentes formas toocreate uma máquina virtual porque as máquinas virtuais são adequadas para diferentes utilizadores e efeitos. Isto significa que terá de toomake algumas opções sobre a máquina virtual de Olá e como toocreate-lo. Este artigo dá-lhe um resumo destas opções e liga tooinstructions.

## <a name="azure-portal"></a>Portal do Azure
A utilização de Olá portal do Azure é um tootry de forma simples de saída de uma máquina virtual, especialmente se é inexperiente com o Azure. 

[Criar uma máquina virtual com o Windows através do portal Olá](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Modelo
Máquinas virtuais requerem uma combinação de recursos (por exemplo, uma disponibilidade conjuntos e as contas de armazenamento). Em vez de implementar e gerir separadamente cada recurso, pode criar um modelo Azure Resource Manager que implementa e aprovisiona todos os recursos de Olá numa operação única e coordenada.

* [Criar uma máquina virtual do Windows com um modelo do Resource Manager](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Se preferir trabalhar numa shell de comandos, pode utilizar o Azure PowerShell.

* [Criar uma VM do Windows com o PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Utilizar o Visual Studio toobuild, gerir, implementar VMs com ferramentas do Azure Olá para Visual Studio e Olá Azure SDK.

[Ferramentas do Azure para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

