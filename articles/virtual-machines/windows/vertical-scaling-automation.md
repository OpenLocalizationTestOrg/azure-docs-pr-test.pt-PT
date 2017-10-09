---
title: "aaaUse da automatização do Azure toovertically dimensionar as máquinas virtuais do Windows | Microsoft Docs"
description: "Aumentar verticalmente Máquina Virtual do Windows nos alertas do toomonitoring resposta com a automatização do Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a>Aumentar verticalmente VMs do Windows com a automatização do Azure

Dimensionamento vertical é o processo de Olá de aumente ou diminua recursos Olá de uma máquina numa carga de trabalho de toohello de resposta. No Azure Isto pode ser efetuado ao alterar o tamanho de Olá de Olá Máquina Virtual. Isto pode ajudar nos seguintes cenários de Olá

* Se Olá Máquina Virtual não está a ser utilizada com frequência, pode redimensioná-lo para baixo tooa tooreduce de tamanho mais pequeno os custos mensais
* Se Olá Máquina Virtual está a ter um pico de carga, pode ser redimensionado tooa maior tamanho tooincrease a capacidade

Descrição de Olá para Olá passos tooaccomplish trata como abaixo

1. O programa de configuração da automatização do Azure tooaccess as máquinas virtuais
2. Importar Olá runbooks de escala Vertical de automatização do Azure para a sua subscrição
3. Adicionar um runbook de tooyour do webhook
4. Adicionar um alerta tooyour Máquina Virtual

> [!NOTE]
> Devido ao tamanho de Olá de Olá primeira Máquina Virtual, tamanhos de Olá pode ser ampliada, poderá ser limitado devido a disponibilidade de toohello de Olá outros tamanhos de cluster Olá atual Máquina Virtual está implementada no. No Olá publicar runbooks de automatização utilizados neste artigo, vamos asseguramos neste caso e dimensionar apenas dentro do Olá abaixo pares de tamanho VM. Isto significa que uma Máquina Virtual de Standard_D1v2 subitamente não irá ser escalado para cima tooStandard_G5 ou ampliada baixo tooBasic_A0.
> 
> | Dimensionamento par de tamanhos de VM |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | Standard_D1 |Standard_D4 |
> | Standard_D11 |Standard_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>O programa de configuração da automatização do Azure tooaccess as máquinas virtuais
Olá primeira coisa que precisa de toodo é criar uma conta de automatização do Azure que irá alojar Olá runbooks utilizados tooscale uma Máquina Virtual. Recentemente o serviço de automatização Olá introduzida Olá "Conta Run As" funcionalidade que permite configurar Olá Principal de serviço para executar automaticamente Olá runbooks em nome de utilizador Olá muito fácil. Pode ler mais sobre este artigo Olá abaixo:

* [Autenticar Runbooks com a conta Run As do Azure](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importar Olá runbooks de escala Vertical de automatização do Azure para a sua subscrição
Olá runbooks que são necessários para aumentar verticalmente a sua máquina Virtual já são publicados no Olá Galeria de Runbooks de automatização do Azure. Terá de tooimport-los na sua subscrição. Pode saber como tooimport runbooks. o lendo Olá seguinte artigo.

* [Galleries módulos e Runbooks de automatização do Azure](../../automation/automation-runbook-gallery.md)

Olá runbooks que necessitam de toobe importado são apresentados na imagem de Olá abaixo

![Importar runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Adicionar um runbook de tooyour do webhook
Assim que tiver de importar runbooks Olá terá tooadd webhook toohello runbook pelo que pode ser acionada por um alerta de uma Máquina Virtual. detalhes de Olá de criar um webhook de Runbook podem ser lidos aqui

* [Webhooks de automatização do Azure](../../automation/automation-webhooks.md)

Certifique-se que copiar Olá webhook antes de fechar a caixa de diálogo do Olá webhook como irá precisar na secção seguinte, Olá.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Adicionar um alerta tooyour Máquina Virtual
1. Selecione as definições da Máquina Virtual
2. Selecione "Regras de alerta"
3. Selecione "Adicionar alerta"
4. Selecione um alerta de Olá toofire métrica no
5. Selecione uma condição que quando cumprido irá causar Olá toofire de alerta
6. Selecione um limiar para a condição de Olá no passo 5. toobe cumprido
7. Selecionar um período de ativação pós-falha que Olá irá verificar o serviço de monitorização para a condição de Olá e limiar de passos 5 & 6
8. Cole no webhook Olá que copiou na secção anterior Olá.

![Adicionar o alerta tooVirtual máquina 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Adicionar o alerta tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

