---
title: "aaaAzure tipos de Runbook de automatização | Microsoft Docs"
description: "Descreve os diferentes tipos Olá de runbooks que pode utilizar na automatização do Azure e as considerações que deve ter em consideração quando determinar que toouse de tipo. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Tipos de runbook da automatização do Azure
A automatização do Azure suporta quatro tipos de runbooks que uma breve descrição Olá a tabela seguinte.  Olá seções abaixo fornecem informações adicionais sobre cada tipo de levando em consideração no quando toouse cada.

| Tipo | Descrição |
|:--- |:--- |
| [Gráficos](#graphical-runbooks) |Com base no Windows PowerShell e criado e editado completamente no editor gráfico no portal do Azure. |
| [Fluxo de trabalho do PowerShell gráfico](#graphical-runbooks) |Com base no fluxo de trabalho do Windows PowerShell e editor gráfico de criados e editados completamente no Olá no portal do Azure. |
| [PowerShell](#powershell-runbooks) |Runbook de texto com base no script do Windows PowerShell. |
| [Fluxo de Trabalho do PowerShell](#powershell-workflow-runbooks) |Runbook de texto com base no fluxo de trabalho do Windows PowerShell. |

## <a name="graphical-runbooks"></a>Runbooks gráficos
[Gráfico](automation-runbook-types.md#graphical-runbooks) e runbooks do fluxo de trabalho do PowerShell gráfico são criados e editados com o editor gráfico de Olá no Olá portal do Azure.  Pode exportá-las tooa ficheiro e, em seguida, importe-as para outra conta de automatização, mas não é possível criar ou editá-los com outra ferramenta.  Runbooks gráficos gerar código do PowerShell, mas não pode ver ou modificar Olá código diretamente. Runbooks gráficos não pode ser convertida tooone de Olá [formatos de texto](automation-runbook-types.md), nem pode ser de um runbook de texto convertida toographical formato. Runbooks gráficos pode ser convertida tooGraphical runbooks do fluxo de trabalho do PowerShell durante a importação e vice-versa.

### <a name="advantages"></a>Vantagens
* Visual insert-ligação-configurar o modelo criação  
* Focar-se na forma como os dados fluem através do processo de Olá  
* Visualmente representar processos de gestão  
* Incluir outros runbooks como subordinados runbooks toocreate elevado nível fluxos de trabalho  
* Encoraja programação modular  


### <a name="limitations"></a>Limitações
* Não é possível editar o runbook fora do portal do Azure.
* Pode necessitar de uma atividade de código que contém a lógica complexa do tooperform de código do PowerShell.
* Não é possível ver ou editar diretamente o código do PowerShell Olá que é criado pelo fluxo de trabalho gráfico Olá. Tenha em atenção que pode ver o código de Olá que criar quaisquer atividades de código.

## <a name="powershell-runbooks"></a>Runbooks do PowerShell
Os runbooks do PowerShell são baseados no Windows PowerShell.  Editar diretamente o código de Olá de runbook Olá utilizando o editor de texto Olá Olá portal do Azure.  Também pode utilizar qualquer editor de texto offline e [importar runbook Olá](http://msdn.microsoft.com/library/azure/dn643637.aspx) na automatização do Azure.

### <a name="advantages"></a>Vantagens
* Implementa toda a lógica complexa com o código do PowerShell sem complexidades adicionais do Olá de fluxo de trabalho do PowerShell. 
* Runbook inicia-se mais rapidamente do que os runbooks do fluxo de trabalho do PowerShell, uma vez que não necessita de toobe compilada antes de executar.

### <a name="limitations"></a>Limitações
* Tem de estar familiarizado com scripts do PowerShell.
* Não é possível utilizar [processamento paralelo](automation-powershell-workflow.md#parallel-processing) tooperform várias ações em paralelo.
* Não é possível utilizar [pontos de verificação](automation-powershell-workflow.md#checkpoints) tooresume runbook em caso de erro.
* Os runbooks do fluxo de trabalho do PowerShell e runbooks gráficos só pode ser incluídos como runbooks subordinados utilizando o cmdlet Olá AzureAutomationRunbook de início que cria uma nova tarefa.

### <a name="known-issues"></a>Problemas conhecidos
Seguem-se atuais problemas conhecidos com runbooks do PowerShell.

* Os runbooks do PowerShell não é possível não é possível obter um não encriptada [recurso de variável](automation-variables.md) com um valor nulo.
* Os runbooks do PowerShell não é possível obter um [recurso de variável](automation-variables.md) com  *~*  no nome de Olá.
* Get-Process num ciclo num PowerShell runbook pode falhar após cerca de 80 iterações. 
* Um runbook de PowerShell poderá falhar se tentar toowrite uma grande quantidade de fluxo de saída de toohello dados em simultâneo.   Normalmente, pode contornar este problema, exportar apenas informações de Olá que necessárias ao trabalhar com objetos grandes.  Por exemplo, em vez de exportar algo semelhante ao seguinte *Get-Process*, o utilizador pode apresentar apenas os campos de Olá necessário com *Get-Process | Selecione ProcessName, CPU*.

## <a name="powershell-workflow-runbooks"></a>Runbooks do fluxo de trabalho do PowerShell
Os runbooks do fluxo de trabalho do PowerShell são texto runbooks com base nos [o fluxo de trabalho do Windows PowerShell](automation-powershell-workflow.md).  Editar diretamente o código de Olá de runbook Olá utilizando o editor de texto Olá Olá portal do Azure.  Também pode utilizar qualquer editor de texto offline e [importar runbook Olá](http://msdn.microsoft.com/library/azure/dn643637.aspx) na automatização do Azure.

### <a name="advantages"></a>Vantagens
* Implementa toda a lógica complexa com o código de fluxo de trabalho do PowerShell.
* Utilize [pontos de verificação](automation-powershell-workflow.md#checkpoints) tooresume runbook em caso de erro.
* Utilize [processamento paralelo](automation-powershell-workflow.md#parallel-processing) tooperform várias ações em paralelo.
* Pode incluir outros runbooks gráficos e runbooks do fluxo de trabalho do PowerShell como subordinados runbooks toocreate elevado nível fluxos de trabalho.

### <a name="limitations"></a>Limitações
* Autor deve estar familiarizado com o fluxo de trabalho do PowerShell.
* Runbook tem de lidar com a complexidade adicional de Olá de fluxo de trabalho do PowerShell como [anular a serialização de objetos](automation-powershell-workflow.md#code-changes).
* Runbook demora toostart mais do que os runbooks do PowerShell, uma vez que é necessário toobe compilada antes de executar.
* Os runbooks do PowerShell só podem ser incluídos como runbooks subordinados utilizando o cmdlet Olá AzureAutomationRunbook de início que cria uma nova tarefa.

## <a name="considerations"></a>Considerações
Deve ter-se em Olá conta seguintes considerações adicionais ao determinar que toouse de tipo para um determinado runbook.

* Não é possível converter os runbooks do tipo de gráfico tootextual ou vice-versa.
* Existem limitações através de runbooks de diferentes tipos de como um runbook subordinado.  Consulte [runbooks subordinados na automatização do Azure](automation-child-runbooks.md) para obter mais informações.

## <a name="next-steps"></a>Passos seguintes
* toolearn mais informações sobre a criação de runbooks gráficos, consulte [a criação de gráficos na automatização do Azure](automation-graphical-authoring-intro.md)
* Olá toounderstand as diferenças entre o PowerShell e o PowerShell fluxos de trabalho para runbooks, consulte [aprendizagem do Windows PowerShell Workflow](automation-powershell-workflow.md)
* Para mais informações sobre como toocreate ou importar um Runbook, consulte [criar ou importar um Runbook](automation-creating-importing-runbook.md)

