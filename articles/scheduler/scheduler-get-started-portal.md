---
title: aaaGet ao agendador do Azure no portal do Azure | Microsoft Docs
description: "Introdução ao Agendador do Azure no portal do Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Introdução ao Agendador do Azure no portal do Azure
É fácil toocreate agendada tarefas do agendador do Azure. Neste tutorial, irá aprender como toocreate uma tarefa. Também irá aprender capacidades de monitorização e gestão do Agendador.

## <a name="create-a-job"></a>Criar uma tarefa
1. A iniciar sessão demasiado[portal do Azure](https://portal.azure.com/).  
2. Clique em **+ novo** > tipo *programador* na caixa de pesquisa de Olá > selecione **programador** nos resultados > clique **criar**.
   
    ![][marketplace-create]
3. Vamos criar uma tarefa que simplesmente chegue a http://www.microsoft.com/ com um pedido GET. No Olá **tarefa do agendador** ecrã, introduza Olá seguintes informações:
   
   1. **Nome:** `getmicrosoft`  
   2. **Subscrição:** a sua subscrição do Azure   
   3. **Coleção de Tarefas:** selecione uma coleção de tarefas existente ou clique em **Criar novo** > introduza um nome.
4. Em seguida, no **definições de ação**, definir Olá os seguintes valores:
   
   1. **Tipo de Ação:** ` HTTP`  
   2. **Método:** `GET`  
   3. **URL:** ` http://www.microsoft.com`  
      
      ![][action-settings]
5. Por fim, vamos definir uma agenda. tarefa de Olá pode ser definido como uma única tarefa, mas vamos escolher uma agenda de periodicidade:
   
   1. **Periodicidade**: `Recurring`
   2. **Iniciar**: data de hoje
   3. **Recorrer a cada**: `12 Hours`
   4. **Terminar a**: dois dias a partir da data de hoje  
      
      ![][recurrence-schedule]
6. Clique em **Criar**.

## <a name="manage-and-monitor-jobs"></a>Gerir e monitorizar tarefas
Quando é criada uma tarefa, aparecerá no dashboard do Olá principal do Azure. Clique em tarefa Olá e uma nova janela abre-se com Olá seguintes separadores:

1. Propriedades  
2. Definições de Ação  
3. Agenda  
4. Histórico
5. Utilizadores
   
   ![][job-overview]

### <a name="properties"></a>Propriedades
Estas propriedades só de leitura descrevem Olá gestão metadados de tarefa do agendador de Olá.

   ![][job-properties]

### <a name="action-settings"></a>Definições de ação
Clicar numa tarefa no Olá **tarefas** ecrã permite-lhe tooconfigure da tarefa. Isto permite-lhe configurar as definições avançadas, se não as tenha feito no Olá criação rápida assistente.

Para todos os tipos de ação, pode alterar a política de repetição Olá e ação de erro Olá.

Para os tipos de ação de tarefa HTTP e HTTPS, pode alterar Olá método tooany permitido verbo HTTP. Também pode adicionar, eliminar ou alterar cabeçalhos Olá e informações de autenticação básica.

Para tipos de ação de fila de armazenamento, pode alterar a conta de armazenamento Olá, nome da fila, SAS token e corpo.

Para os tipos de ação de barramento de serviço, pode alterar Olá espaço de nomes, caminho do tópico/fila, definições de autenticação, tipo de transporte, propriedades da mensagem e corpo da mensagem.

   ![][job-action-settings]

### <a name="schedule"></a>Agenda
Isto permite-lhe reconfigurar a agenda de Olá, se pretender que o agendamento de Olá toochange que criou no Olá criação rápida assistente.

Esta é uma oportunidade toobuild [agendas complexas e periodicidade avançada na sua tarefa](scheduler-advanced-complexity.md)

Pode alterar a data de início Olá e tempo, a agenda de periodicidade e Olá terminar a data e hora (se a tarefa de Olá seja recorrente).

   ![][job-schedule]

### <a name="history"></a>Histórico
Olá **histórico** separador mostra as métricas selecionadas para cada execução da tarefa no sistema de Olá para a tarefa selecionada Olá. Estas métricas fornecem valores em tempo real sobre o estado de funcionamento de Olá do seu agendador:

1. Estado  
2. Detalhes  
3. Tentativas de repetição
4. Ocorrência: 1ª, 2ª, 3ª, etc.
5. Hora de início de execução  
6. Hora de fim de execução
   
   ![][job-history]

Pode clicar numa execução tooview respetivo **detalhes de histórico**, incluindo a resposta completa do Olá para cada execução. Esta caixa de diálogo também lhe permite área de transferência do toocopy Olá resposta toohello.

   ![][job-history-details]

### <a name="users"></a>Utilizadores
O Controlo de Acesso Baseado em Funções (RBAC) do Azure permite uma gestão pormenorizada de acesso ao Agendador do Azure. toolearn como toouse Olá separador de utilizadores, consulte demasiado[controlo de acesso em funções do Azure](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>Consultar também
 [O que é o Scheduler?](scheduler-intro.md)

 [Conceitos, terminologia e hierarquia de entidades do Scheduler](scheduler-concepts-terms.md)

 [Planos e faturação no Azure Scheduler](scheduler-plans-billing.md)

 [Como as agendas de toobuild complexas e periodicidade avançada com o agendador do Azure](scheduler-advanced-complexity.md)

 [Referência da API REST do Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Referência de cmdlets do PowerShell do Scheduler](scheduler-powershell-reference.md)

 [Elevada disponibilidade e fiabilidade do Scheduler](scheduler-high-availability-reliability.md)

 [Limites, predefinições e códigos de erro do Scheduler](scheduler-limits-defaults-errors.md)

 [Autenticação de saída do Scheduler](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
