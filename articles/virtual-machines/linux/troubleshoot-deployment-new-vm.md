---
title: "aaaTroubleshoot implementação-RM de VM com Linux | Microsoft Docs"
description: "Resolver problemas de implementação do Resource Manager, quando criar uma nova máquina virtual de Linux no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Resolver problemas de implementação do Resource Manager com a criação de uma nova máquina virtual de Linux no Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Problemas principais
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Para outros problemas de implementação da VM e perguntas, consulte [resolver problemas de máquina virtual Linux implementar no Azure](troubleshoot-deploy-vm.md).
## <a name="collect-activity-logs"></a>Regista a atividade de recolha
toostart de resolução de problemas, atividade Olá recolher os registos erro de Olá tooidentify associado ao problema Olá. Olá ligações seguintes contêm informações detalhadas sobre Olá toofollow de processo.

[Ver as operações de implementação](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Ver registos de atividade toomanage Azure recursos](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** se Olá SO é Linux generalizado e é carregado e/ou capturado com Olá generalizado definição, em seguida, haverá quaisquer erros. Da mesma forma, se Olá SO é especializada do Linux, e é carregado e/ou capturado com Olá especializada definição, em seguida, haverá quaisquer erros.

**Carregar erros:**

**N<sup>1</sup>:** se Olá SO Linux generalizado, e ser carregada como especializada, obterá um erro de tempo limite de aprovisionamento porque Olá VM é bloqueada no Olá fase de aprovisionamento.

**N<sup>2</sup>:** esteja Olá SO Linux especializada e ser carregada como generalizado, obterá um erro de falha de aprovisionamento porque hello nova VM está em execução com o nome do computador original Olá, nome de utilizador e palavra-passe.

**Resolução:**

tooresolve ambos estes erros, carregar Olá VHD original, disponível no local, com Olá, mesmo que a definição Olá SO (generalizado/especializado). tooupload como generalizado, lembre-se toorun-desaprovisionar primeiro.

**Captura de erros:**

**N<sup>3</sup>:** se Olá SO Linux generalizado, e é capturado como especializada, obterá um erro de tempo limite de aprovisionamento porque Olá original VM não é utilizável está marcado como generalizado.

**N<sup>4</sup>:** esteja Olá SO Linux especializada e é capturado como generalizado, obterá um erro de falha de aprovisionamento porque hello nova VM está em execução com o nome do computador original Olá, nome de utilizador e palavra-passe. Além disso, Olá original VM não é utilizável porque está marcado como especializado.

**Resolução:**

tooresolve ambos estes erros, eliminar imagem atual Olá do portal de Olá, e [recapturá-lo a partir de Olá VHDs atuais](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) com Olá, mesmo que a definição Olá SO (generalizado/especializado).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: Personalizada / Galeria / imagem do marketplace; Falha de alocação
Este erro for em situações quando novo pedido de VM Olá é afixado tooa de cluster que não suporta o tamanho da VM Olá que está a ser solicitado, ou não têm o pedido de Olá tooaccommodate de espaço livre disponível.

**Causa 1:** cluster Olá não pode suportar Olá solicitado o tamanho da VM.

**Resolução 1:**

* Repita o pedido de Olá utilizando um tamanho mais pequeno da VM.
* Se hello o tamanho do Olá pedido que não é possível alterar a VM:
  * Pare todas as VMs de Olá no conjunto de disponibilidade de Olá.
    Clique em **grupos de recursos** > *o grupo de recursos* > **recursos** > *o conjunto de disponibilidade* > **máquinas virtuais** > *a máquina virtual* > **parar**.
  * Depois de todos os hello parar de VMs, criar Olá nova VM na Olá pretendido tamanho.
  * Iniciar Olá nova VM primeiro e, em seguida, selecione cada Olá parado VMs e clique em **iniciar**.

**Causa 2:** Olá cluster não tem recursos gratuitos.

**Resolução de 2:**

* Repita o pedido de Olá numa altura posterior.
* Se hello nova VM pode ser faz parte de uma disponibilidade diferente conjunto
  * Criar uma nova VM num conjunto de disponibilidade diferente (no Olá mesma região).
  * Adicionar Olá nova VM toohello mesma rede virtual.

## <a name="next-steps"></a>Passos seguintes
Se ocorrerem problemas ao iniciar uma VM com Linux parada ou redimensionar uma VM com Linux existente no Azure, consulte o artigo [problemas de implementação do Gestor de recursos de resolução de problemas com reiniciar ou redimensionar uma Máquina Virtual de Linux existente no Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

