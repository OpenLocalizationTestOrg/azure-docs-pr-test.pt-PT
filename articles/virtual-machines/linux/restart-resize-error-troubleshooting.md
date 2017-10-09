---
title: aaaVM reiniciar ou redimensionar problemas no Azure | Microsoft Docs
description: "Resolver problemas de implementação do Resource Manager com reiniciar ou redimensionar uma Máquina Virtual de Linux existente no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>Resolver problemas de implementação com reiniciar ou redimensionar uma VM com Linux existente no Azure
Quando tentar toostart uma Máquina Virtual do Azure (VM) parada ou redimensionar uma VM do Azure existente, o erro comum de Olá que ocorrerem é uma falha de alocação. Este erro resulta quando cluster Olá ou a região não ter recursos disponíveis ou não é suporte Olá pedir o tamanho da VM.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Regista a atividade de recolha
toostart de resolução de problemas, atividade Olá recolher os registos erro de Olá tooidentify associado ao problema Olá. Olá seguintes ligações contém informações detalhadas sobre o processo de Olá:

[Ver as operações de implementação](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Ver registos de atividade toomanage Azure recursos](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Problema: Erro ao iniciar uma VM parada
Tente toostart uma VM parada mas obtêm uma falha de alocação.

### <a name="cause"></a>Causa
pedido de Olá toostart Olá parado VM tem toobe tentada no cluster original Olá que aloja o serviço em nuvem Olá. No entanto, o cluster de Olá não tem o pedido de Olá toofulfill disponíveis de espaço livre.

### <a name="resolution"></a>Resolução
* Pare Olá todas as VMs na disponibilidade de Olá definido e, em seguida, reiniciar cada VM.
  
  1. Clique em **grupos de recursos** > *o grupo de recursos* > **recursos** > *o conjunto de disponibilidade* > **máquinas virtuais** > *a máquina virtual* > **parar**.
  2. Após todos os Olá parar de VMs, selecione cada uma das VMs Olá parado e clique em Iniciar.
* Repetir o pedido de reinício de Olá numa altura posterior.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Problema: Ocorreu um erro ao redimensionar uma VM existente
Tente tooresize uma VM existente mas obtêm uma falha de alocação.

### <a name="cause"></a>Causa
pedido de Olá tooresize Olá VM tem toobe tentativa no cluster original Olá referido serviço em nuvem Olá anfitriões. No entanto, o cluster de Olá não suporta Olá solicitado o tamanho da VM.

### <a name="resolution"></a>Resolução
* Repita o pedido de Olá utilizando um tamanho mais pequeno da VM.
* Se hello o tamanho do Olá pedido que não é possível alterar a VM:
  
  1. Pare todas as VMs de Olá no conjunto de disponibilidade de Olá.
     
     * Clique em **grupos de recursos** > *o grupo de recursos* > **recursos** > *o conjunto de disponibilidade* > **máquinas virtuais** > *a máquina virtual* > **parar**.
  2. Após todos os hello VMs parar, redimensionar Olá pretendido tooa VM tamanho maior.
  3. Selecione Olá redimensionado VM e clique em **iniciar**, e, em seguida, inicie cada Olá parado VMs.

## <a name="next-steps"></a>Passos seguintes
Se ocorrerem problemas ao criar uma nova VM com Linux no Azure, consulte o artigo [resolver problemas de implementação com a criação de uma nova máquina virtual de Linux no Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

