---
title: "aaaUser ação iniciada pelo Azure Automation Runbook no Log Analytics | Microsoft Docs"
description: "Este artigo descreve como toorun um runbook de automatização a partir de uma análise de registos procurar resultado a pedido."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Ação com um Runbook de automatização a partir de um resultado de pesquisa de registos de análise de registos

A partir de um resultado de pesquisa de registo no Log Analytics do Azure, agora, pode selecionar **ação** toorun um runbook de automatização.  Olá runbook pode ser utilizado tooremediate Olá problema ação algumas outras, tais como recolher informações de resolução de problemas, envie um e-mail ou criar um pedido de serviço. 

## <a name="components-and-features-used"></a>Componentes e funcionalidades utilizados
* [Conta de automatização do Azure](../automation/automation-offering-get-started.md)
* [Área de trabalho de análise de registo](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>tooinitiate runbook a partir de pesquisa de registo

ação de tootake de um evento e iniciar um runbook a partir dos resultados da pesquisa de registo, comece por criar uma pesquisa de registo e a partir dos resultados de Olá pode invocar uma runbook a pedido.  Isto pode ser conseguido de funcionalidade de pesquisa de registo Olá no Olá, Azure ou [portal do OMS](../log-analytics/log-analytics-log-searches.md).  Neste exemplo, vamos efetuar uma pesquisa de registo de Olá portal do Azure com uma demonstração básico desta funcionalidade.

1. No portal do Azure Olá, no menu do Hub de Olá clique **mais serviços** e selecione **Log Analytics**.  
2. No painel de análise de registos de Olá, selecione a sua área de trabalho de análise de registos e no painel da área de trabalho de Olá selecione **pesquisa registo**.  
3. No painel de pesquisa de registo de Olá, efetue uma pesquisa de registo.  
4. Dos resultados de pesquisa de registo de Olá, clique em esquerda de toohello elipse Olá de um dos campos de Olá e Olá pop-up, selecione **executar ações em**.<br><br> ![Selecione a ação demorar do resultado de pesquisa](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. No painel de ação de tomar Olá, selecione **executar um runbook**e em Olá **executar um runbook** painel, pode selecionar um toorun de runbook.  Pode selecionar qualquer runbook na Olá conta de automatização que é a área de trabalho de análise de registos de toohello ligado.  Tenha em atenção o seguinte Olá:

    * Os Runbooks estão organizados por etiquetas
    * Os valores de parâmetro de entrada do Runbook podem ser selecionados diretamente a partir de campos de Olá do resultado da pesquisa Olá.  Na lista pendente aparecerá a apresentar todos os campos disponíveis Olá de Olá resultado tooselect do.  
    * Pode escolher toorun Olá runbook num [runbook worker híbrido](../automation/automation-hybrid-runbook-worker.md) que tem instalado na máquina de Olá que possui um problema de Olá, se tiver um grupo de trabalho de Runbook híbrida correspondente que contém apenas esta máquina como membro.  Se o nome de Olá do grupo de trabalho híbrida Olá corresponde ao nome de Olá do computador Olá que está a ser resultado de pesquisa de registo Olá, grupo de Olá é selecionado automaticamente.    

6. Depois de clicar em **executar**, painel de tarefas de runbook Olá abrirá tooallow tooreview Olá estado da tarefa de Olá.   

Se selecionar um runbook que foi configurado toobe [chamado a partir de um alerta de análise de registos](../automation/automation-invoke-runbook-from-omsla-alert.md), tem um parâmetro de entrada chamado **WebhookData** que **objeto** tipo.  Se o parâmetro de entrada Olá é obrigatório, terá de toopass Olá pesquisa resultados toohello runbook pelo que pode converter a cadeia de formatada em JSON Olá para um tipo de objeto, permitindo-lhe toofilter nos itens específicos que irá referenciar em atividades do runbook.  Fazê-lo ao selecionar **procurar resultado (objeto)** de Olá na lista pendente.<br><br> ![Selecione o objeto de dados de Webhook para o parâmetro de runbook](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Passos seguintes

* Olá revisão [referência de pesquisa de registo de análise de registos](log-analytics-search-reference.md) tooview todas Olá procurar campos e facetas disponíveis na análise de registos.
* toolearn como tooinvoke um runbook da automatização automaticamente, reveja [chamar um runbook de automatização do Azure a partir de um alerta de análise de registos do OMS](../automation/automation-invoke-runbook-from-omsla-alert.md).  
