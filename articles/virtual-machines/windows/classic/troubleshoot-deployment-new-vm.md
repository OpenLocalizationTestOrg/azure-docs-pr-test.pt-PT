---
title: "aaaTroubleshoot implementação de Windows VM-clássico | Microsoft Docs"
description: "Resolver problemas de implementação clássica, quando criar uma nova máquina virtual do Windows no Azure"
services: virtual-machines-windows
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f01d237-ba39-4c32-b72d-18f5f505d43a
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cjiang
ms.openlocfilehash: aa12cb013a18e0572fbef8b7ea69106dd47c1fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-windows-virtual-machine-in-azure"></a>Resolver problemas de implementação clássica com a criação de nova máquina virtual do Windows no Azure
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Para a versão do Gestor de recursos de Olá deste artigo, consulte [aqui](../../virtual-machines-windows-troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Os registos de auditoria de recolha
toostart de resolução de problemas, auditoria Olá recolher os registos erro de Olá tooidentify associado ao problema Olá.

No portal do Azure Olá, clique em **procurar** > **máquinas virtuais** > *a máquina virtual do Windows*  >   **Definições** > **registos de auditoria**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** se Olá SO é o Windows generalizado e é carregado e/ou capturado com Olá generalizado definição, em seguida, haverá quaisquer erros. Da mesma forma, se Olá SO é especializada do Windows e de é carregado e/ou capturado com Olá especializada definição, em seguida, haverá quaisquer erros.

**Carregar erros:**

**N<sup>1</sup>:** se Olá SO Windows generalizado, e ser carregada como especializada, obterá um erro de tempo limite de aprovisionamento com Olá VM bloqueada no ecrã OOBE Olá.

**N<sup>2</sup>:** esteja Olá SO Windows especializada e ser carregada como generalizado, obterá um erro de falha de aprovisionamento com Olá VM bloqueada no ecrã OOBE Olá porque hello nova VM está em execução com o computador original Olá o nome, nome de utilizador e palavra-passe.

**Resolução:**

tooresolve ambos estes erros, carregar Olá VHD original, disponível no local, com Olá, mesmo que a definição Olá SO (generalizado/especializado). tooupload como generalizado, lembre-se toorun sysprep primeiro. Consulte [criar e carregar um VHD do Windows Server tooAzure](createupload-vhd.md) para obter mais informações.

**Captura de erros:**

**N<sup>3</sup>:** se Olá SO Windows generalizado, e é capturado como especializada, obterá um erro de tempo limite de aprovisionamento porque Olá original VM não é utilizável está marcado como generalizado.

**N<sup>4</sup>:** esteja Olá SO Windows especializada e é capturado como generalizado, obterá um erro de falha de aprovisionamento porque hello nova VM está em execução com o nome do computador original Olá, nome de utilizador e palavra-passe. Além disso, Olá original VM não é utilizável porque está marcado como especializado.

**Resolução:**

tooresolve ambos estes erros, eliminar imagem atual Olá do portal de Olá, e [recapturá-lo a partir de Olá VHDs atuais](capture-image.md) com Olá, mesmo que a definição Olá SO (generalizado/especializado).

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Problema: Personalizada / Galeria / imagem do marketplace; Falha de alocação
Este erro for em situações quando novo pedido de VM Olá é enviado tooa cluster que não ter pedido de Olá tooaccommodate de espaço livre disponível, ou não suporta o tamanho da VM Olá que está a ser solicitado. Não é possível toomix série de diferentes de VMs no Olá mesmo serviço em nuvem. Por isso, se quiser toocreate uma nova VM de um tamanho diferente que o seu serviço em nuvem pode suportar, Olá computação pedido irá falhar.

Consoante as restrições de Olá do serviço de nuvem Olá utilizar toocreate Olá nova VM, podem ocorrer um erro foi causado por uma das duas situações.

**Causa 1:** o serviço em nuvem Olá é afixado tooa cluster específicos, ou é o grupo de afinidade tooan ligado e, por conseguinte, afixado tooa cluster específicos por predefinição. Para que os pedidos de novos recursos de computação nesse grupo de afinidade são experimentadas em Olá mesmo cluster onde estão alojados recursos existentes Olá. No entanto, hello mesmo cluster poderá não é suporte Olá solicitadas tamanho da VM ou ter espaço disponível suficiente, resultando no erro de alocação. Isto acontece se os recursos novos Olá são criados através de um novo serviço em nuvem ou através de um serviço em nuvem existente.

**Resolução 1:**

* Criar um novo serviço de nuvem e associá-la a uma região ou uma rede virtual com base na região.
* Crie uma nova VM no novo serviço de nuvem Olá.
  Se obtiver um erro quando tenta toocreate um novo serviço em nuvem, tente novamente mais tarde ou alterar a região de Olá para o serviço em nuvem Olá.

> [!IMPORTANT]
> Se foram tentar toocreate uma nova VM num serviço em nuvem existente, mas não foi possível e tinha toocreate um novo serviço em nuvem para a nova VM, pode optar por tooconsolidate todas as suas VMs no Olá mesmo serviço em nuvem. toodo por isso, eliminar as VMs de Olá num serviço em nuvem existente do Olá e recapturá-los a partir os respetivos discos no novo serviço de nuvem Olá. No entanto, é importante tooremember que novo serviço de nuvem Olá terá um novo nome e VIP, pelo que terá tooupdate estes para todas as dependências de Olá que a utilizam atualmente estas informações para o serviço em nuvem existente Olá.
> 
> 

**Causa 2:** o serviço em nuvem Olá está associado uma rede virtual que é o grupo de afinidade tooan ligado, pelo que é afixado tooa cluster específicos por predefinição. Todos os pedidos de recursos computação novo nesse grupo de afinidade, por isso, são experimentados em Olá mesmo cluster onde estão alojados recursos existentes Olá. No entanto, hello mesmo cluster poderá não é suporte Olá solicitadas tamanho da VM ou ter espaço disponível suficiente, resultando no erro de alocação. Isto acontece se os recursos novos Olá são criados através de um novo serviço em nuvem ou através de um serviço em nuvem existente.

**Resolução de 2:**

* Crie uma nova rede virtual regional.
* Criar Olá nova VM na rede virtual de novo Olá.
* [Ligar à rede virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello nova rede virtual. Ver mais informações sobre [redes virtuais regionais](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Em alternativa, pode [migrar baseado em grupo de afinidade de rede virtual tooa regional rede virtual](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)e, em seguida, criar Olá nova VM.

## <a name="next-steps"></a>Passos seguintes
Se ocorrerem problemas ao iniciar uma VM do Windows parada ou redimensionar uma VM existente do Windows no Azure, consulte o artigo [resolver problemas de implementação clássica com reiniciar ou redimensionar uma Máquina Virtual existente do Windows no Azure](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md).

