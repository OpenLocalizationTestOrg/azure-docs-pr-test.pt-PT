---
title: aaaVM reiniciar ou redimensionar problemas | Microsoft Docs
description: "Resolver problemas de implementação clássica com reiniciar ou redimensionar uma Máquina Virtual existente do Windows no Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a>Resolver problemas de implementação clássica com reiniciar ou redimensionar uma Máquina Virtual existente do Windows no Azure
> [!div class="op_single_selector"]
> * [Clássico](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [Resource Manager](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

Quando tentar toostart uma Máquina Virtual do Azure (VM) parada ou redimensionar uma VM do Azure existente, o erro comum de Olá que ocorrerem é uma falha de alocação. Este erro resulta quando cluster Olá ou a região não ter recursos disponíveis ou não é suporte Olá pedir o tamanho da VM.

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Os registos de auditoria de recolha
toostart de resolução de problemas, auditoria Olá recolher os registos erro de Olá tooidentify associado ao problema Olá.

No portal do Azure Olá, clique em **procurar** > **máquinas virtuais** > *a máquina virtual do Windows*  >   **Definições** > **registos de auditoria**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: Erro ao iniciar uma VM parada
Tente toostart uma VM parada mas obtêm uma falha de alocação.

### <a name="cause"></a>Causa
pedido de Olá toostart Olá parado VM tem toobe tentada no cluster original Olá que aloja o serviço em nuvem Olá. No entanto, o cluster de Olá não tem o pedido de Olá toofulfill disponíveis de espaço livre.

### <a name="resolution"></a>Resolução
* Criar um novo serviço de nuvem e associá-la a uma região ou uma rede virtual com base na região, mas não é um grupo de afinidade.
* Eliminar Olá parado VM.
* Recrie Olá VM no novo serviço de nuvem Olá utilizando discos de Olá.
* Iniciar Olá recriada VM.

Se obtiver um erro quando tenta toocreate um novo serviço em nuvem, tente novamente mais tarde ou alterar a região de Olá para o serviço em nuvem Olá.

> [!IMPORTANT]
> novo serviço de nuvem Olá terá um novo nome e VIP, pelo que terá toochange essas informações para todas as dependências de Olá utilizam essas informações para o serviço em nuvem existente Olá.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: Ocorreu um erro ao redimensionar uma VM existente
Tente tooresize uma VM existente mas obtêm uma falha de alocação.

### <a name="cause"></a>Causa
pedido de Olá tooresize Olá VM tem toobe tentativa no cluster original Olá referido serviço em nuvem Olá anfitriões. No entanto, o cluster de Olá não suporta Olá solicitado o tamanho da VM.

### <a name="resolution"></a>Resolução
Reduzir Olá solicitado o tamanho da VM e repita Olá redimensionar pedido.

* Clique em **Procurar tudo** > **máquinas virtuais (clássicas)** > *a máquina virtual* > **definições** > **tamanho**. Para obter passos detalhados, consulte [redimensionar a máquina virtual de Olá](https://msdn.microsoft.com/library/dn168976.aspx).

Se não for possível tooreduce Olá tamanho da VM, siga estes passos:

* Crie um novo serviço de nuvem, assegurar que não se trata de grupo de afinidade tooan ligado e não associados a uma rede virtual que é o grupo de afinidade tooan ligado.
* Crie uma VM nova, maior dimensão no mesmo.

Pode consolidar todas as suas VMs no Olá mesmo serviço em nuvem. Se o serviço em nuvem existente está associado uma rede virtual com base na região, pode ligar Olá novo nuvem serviço toohello rede virtual existente.

Se o serviço em nuvem existente Olá não estiver associado uma rede virtual com base na região, em seguida, pode ter toodelete Olá VMs num serviço em nuvem existente do Olá e recriá-los no Olá novo serviço em nuvem dos respetivos discos. No entanto, é importante tooremember que novo serviço de nuvem Olá terá um novo nome e VIP, pelo que terá tooupdate estes para todas as dependências de Olá que a utilizam atualmente estas informações para o serviço em nuvem existente Olá.

## <a name="next-steps"></a>Passos seguintes
Se ocorrerem problemas ao criar uma VM do Windows no Azure, consulte o artigo [resolver problemas de implementação com a criação de uma máquina virtual do Windows Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

