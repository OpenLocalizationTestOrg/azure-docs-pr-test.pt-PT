---
title: "aaaTesting um runbook na automatização do Azure | Microsoft Docs"
description: "Antes de publicar um runbook na automatização do Azure, pode testá-lo tooensure funciona conforme esperado.  Este artigo descreve como tootest um runbook e ver o resultado."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Testar um runbook na automatização do Azure
Quando testa um runbook, Olá [versão de rascunho](automation-creating-importing-runbook.md#publishing-a-runbook) é executado e todas as ações que executar são concluídas. Nenhum histórico da tarefa é criado, mas Olá [saída](automation-runbook-output-and-messages.md#output-stream) e [avisos e erros](automation-runbook-output-and-messages.md#message-streams) fluxos são apresentados no Olá de teste de saída do painel. Mensagens toohello [fluxo verboso](automation-runbook-output-and-messages.md#message-streams) apenas são apresentadas no painel de resultados de Olá se hello [$VerbosePreference variável](automation-runbook-output-and-messages.md#preference-variables) está definido tooContinue.

Apesar de versão de rascunho de Olá está a ser executado, runbook Olá ainda executa o fluxo de trabalho Olá normalmente e efetua quaisquer ações relativamente aos recursos no ambiente de Olá. Por este motivo, deverá testar apenas runbooks em recursos de não produção.

Olá procedimento tootest [tipo de runbook](automation-runbook-types.md) é Olá mesmo e não existe nenhuma diferença nos testes entre o editor de texto Olá e editor gráfico de Olá no Olá portal do Azure.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest um runbook no Olá portal do Azure
Pode trabalhar com qualquer [tipo de runbook](automation-runbook-types.md) no Olá portal do Azure.

1. Versão de rascunho de Olá aberta de runbook Olá em qualquer um dos Olá [editor de texto](automation-edit-textual-runbook.md) ou [editor gráfico](automation-graphical-authoring-intro.md).
2. Clique em Olá **teste** painel de teste do botão tooopen Olá.
3. Se Olá runbook tiver parâmetros, estes serão apresentados no painel esquerdo olá onde pode fornecer toobe de valores utilizado para teste Olá.
4. Se pretender o teste de Olá toorun num [Runbook Worker híbrido](automation-hybrid-runbook-worker.md), em seguida, altere **executar definições** demasiado**Worker híbrido** e selecione Olá nome do grupo de destino Olá.  Caso contrário, mantenha a predefinição de Olá **Azure** toorun Olá teste na nuvem de Olá.
5. Clique em Olá **iniciar** teste do botão toostart Olá.
6. Se for Olá runbook [fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) ou [gráfico](automation-runbook-types.md#graphical-runbooks), em seguida, pode parar ou suspender-enquanto está a ser testado com botões Olá por baixo do painel de resultados de Olá. Quando suspende o runbook Olá, conclui atividade atual Olá antes de ser suspenso. Depois de Olá runbook está suspenso, pode pará-la ou reiniciá-lo.
7. Inspecione o resultado Olá Olá runbook no painel de resultados de Olá.

## <a name="next-steps"></a>Passos Seguintes
* toolearn como toocreate ou importar um runbook, consulte [criar ou importar um runbook na automatização do Azure](automation-creating-importing-runbook.md)
* toolearn mais informações sobre a criação de gráficos, consulte [a criação de gráficos na automatização do Azure](automation-graphical-authoring-intro.md)
* tooget iniciado com runbooks do fluxo de trabalho do PowerShell, consulte [o meu primeiro runbook do fluxo de trabalho do PowerShell](automation-first-runbook-textual.md)
* toolearn mais sobre como configurar as mensagens de estado de tooreturn runboks e erros, incluindo práticas recomendadas, consulte [Runbook resultados e mensagens na automatização do Azure](automation-runbook-output-and-messages.md)

