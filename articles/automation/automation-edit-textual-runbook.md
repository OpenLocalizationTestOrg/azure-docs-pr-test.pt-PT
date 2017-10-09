---
title: "aaaEditing runbooks textual na automatização do Azure"
description: "Este artigo fornece procedimentos diferentes para trabalhar com runbooks do PowerShell e o fluxo de trabalho do PowerShell na automatização do Azure utilizando o editor de texto Olá."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Editar textual runbooks na automatização do Azure
Olá editor de texto na automatização do Azure pode ser utilizado tooedit [runbooks do PowerShell](automation-runbook-types.md#powershell-runbooks) e [runbooks do fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Isto tem funcionalidades típico de Olá de outros editores de código como o intellisense e cor codificação com funcionalidades especiais adicionais tooassist, ao aceder ao toorunbooks comum de recursos.  Este artigo fornece os passos detalhados para executar diferentes funções deste editor.

editor de texto Olá inclui um código de tooinsert funcionalidade para atividades, recursos e runbooks subordinados num runbook. Em vez de digitar o código de Olá por si, pode selecionar numa lista de recursos disponíveis e código adequado Olá inserido no runbook Olá.

Cada runbook na automatização do Azure tem duas versões, rascunho e a publicada. Editar Olá versão de rascunho de runbook Olá e, em seguida, publica-pode ser executado. Não é possível editar a versão do Olá publicada. Consulte [publicar um runbook](automation-creating-importing-runbook.md#publishing-a-runbook) para obter mais informações.

toowork com [Runbooks gráficos](automation-runbook-types.md#graphical-runbooks), consulte [a criação de gráficos na automatização do Azure](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit um runbook com Olá portal do Azure
Utilize Olá seguir o procedimento tooopen um runbook para edição no editor de texto Olá.

1. No portal do Azure Olá, selecione a sua conta de automatização.
2. Clique em Olá **Runbooks** mosaico tooopen Olá lista de runbooks.
3. Clique no nome de Olá de runbook Olá pretende tooedit e, em seguida, clique em Olá **editar** botão.
4. Efetue Olá necessário editar.
5. Clique em **guardar** quando as edições que efectuou estiverem concluídas.
6. Clique em **publicar** se quiser Olá mais recente versão de rascunho Olá runbook toobe publicado.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert um cmdlet num runbook
1. Na tela do editor de texto Olá Olá, posicione o cursor olá onde pretende tooplace Olá cmdlet.
2. Expanda Olá **Cmdlets** nó Olá controlo da biblioteca.
3. Expanda o módulo Olá que contém o cmdlet de Olá pretende toouse.
4. Clique com o botão direito do rato em Olá cmdlet tooinsert e selecione **adicionar toocanvas**.  Se Olá cmdlet tem mais do que um parâmetro definido, será adicionado o conjunto predefinido de Olá.  Também pode expandir Olá cmdlet tooselect um parâmetro diferente definida.
5. o código de Olá Olá cmdlet é inserido com a lista completa de parâmetros.
6. Forneça um valor adequado em vez do tipo de dados de Olá rodeado por chavetas <> para os parâmetros necessários.  Remova quaisquer parâmetros, não precisa.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>código de tooinsert para um runbook subordinado num runbook
1. Na tela do editor de texto Olá Olá, posicione o cursor de olá onde pretende código de Olá tooplace para Olá [runbook subordinado](automation-child-runbooks.md).
2. Expanda Olá **Runbooks** nó Olá controlo da biblioteca.
3. Clique com o botão direito do rato em Olá runbook tooinsert e selecione **adicionar toocanvas**.
4. código de Olá para o runbook subordinado Olá é inserido com quaisquer marcadores de posição para quaisquer parâmetros do runbook.
5. Substitua os marcadores de posição de Olá valores adequados para cada parâmetro.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert um recurso num runbook
1. Na tela do editor de texto Olá Olá, posicione o cursor olá onde pretende código de Olá tooplace para o runbook subordinado Olá.
2. Expanda Olá **ativos** nó Olá controlo da biblioteca.
3. Expanda o nó de Olá para o tipo de Olá do recurso que pretende.
4. Clique com o botão direito do rato em Olá asset tooinsert e selecione **adicionar toocanvas**.  Para [recursos de variável](automation-variables.md), selecione **adicionar "Obter variável" toocanvas** ou **adicionar "Definir variável" toocanvas** dependendo se pretende tooget ou definir Olá variável.
5. código de Olá para o recurso de Olá é inserido no runbook Olá.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit um runbook com Olá portal do Azure
Utilize Olá seguir o procedimento tooopen um runbook para edição no editor de texto Olá.

1. No portal do Azure Olá, selecione **automatização** e, em seguida, em seguida, clique em nome de Olá de uma conta de automatização.
2. Selecione Olá **Runbooks** separador.
3. Clique no nome de Olá de runbook Olá pretende tooedit e, em seguida, selecione Olá **autor** separador.
4. Clique em Olá **editar** botão na Olá parte inferior do ecrã de Olá.
5. Efetue Olá necessário editar.
6. Clique em **guardar** quando as edições que efectuou estiverem concluídas.
7. Clique em **publicar** se quiser Olá mais recente versão de rascunho Olá runbook toobe publicado.

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert uma atividade num Runbook
1. Na tela do editor de texto Olá Olá, posicione o cursor olá onde pretende que a atividade de Olá tooplace.
2. Na Olá na parte inferior do ecrã de Olá, clique em **inserir** e, em seguida, **atividade**.
3. No Olá **módulo de integração** coluna, o módulo Olá select que contém a atividade de Olá.
4. No Olá **atividade** painel, selecione uma atividade.
5. No Olá **Descrição** coluna, tenha em atenção Olá descrição da atividade de Olá. Opcionalmente, pode clicar em ver detalhadas ajudar toolaunch ajuda para a atividade de Olá no browser Olá.
6. Clique em seta para a direita Olá.  Se a atividade de Olá tiver parâmetros, estes serão apresentados para sua informação.
7. Clique no botão de verificação Olá.  Código toorun Olá atividade será inserida no runbook Olá.
8. Se a atividade de Olá necessitar de parâmetros, forneça um valor adequado em vez do tipo de dados de Olá rodeado por chavetas <>.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>código de tooinsert para um runbook subordinado num runbook
1. Na tela do editor de texto Olá Olá, posicione o cursor de olá onde pretende tooplace Olá [runbook subordinado](automation-child-runbooks.md).
2. Na Olá na parte inferior do ecrã de Olá, clique em **inserir** e, em seguida, **Runbook**.
3. Selecione Olá runbook tooinsert da coluna de center Olá e clique em seta para a direita Olá.
4. Se Olá runbook tiver parâmetros, estes serão apresentados para sua informação.
5. Clique no botão de verificação Olá.  Código toorun Olá selecionado runbook será inserido no runbook atual Olá.
6. Se o runbook Olá necessitar de parâmetros, forneça um valor adequado em vez do tipo de dados de Olá rodeado por chavetas <>.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert um recurso num runbook
1. Na tela do editor de texto Olá Olá, posicione o cursor olá onde pretende que o recurso de Olá tooplace Olá atividade tooretrieve.
2. Na Olá na parte inferior do ecrã de Olá, clique em **inserir** e, em seguida, **definição**.
3. No Olá **ação da definição** coluna, acção de Olá selecione que pretende.
4. Selecione recursos disponíveis de Olá na coluna de center Olá.
5. Clique no botão de verificação Olá.  Code tooget ou conjunto Olá asset será inserido no runbook Olá.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit um runbook de automatização do Azure com o Windows PowerShell
tooedit um runbook com o Windows PowerShell, utilize Olá editor à sua escolha e guarde-o ficheiro. ps1 tooa. Pode utilizar Olá [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) cmdlet tooretrieve Olá conteúdo Olá runbook e, em seguida, [conjunto AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace Olá existente rascunho de runbook com Olá modificar um.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve Olá conteúdos de um Runbook através do Windows PowerShell
Olá comandos de exemplo a seguir mostra como tooretrieve Olá script para um runbook e guardá-lo tooa ficheiro de script. Neste exemplo, a versão de rascunho de Olá é obtido. Também é versão de publicada Olá tooretrieve possíveis de runbook Olá apesar de não pode ser alterada nesta versão.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange Olá conteúdos de um Runbook através do Windows PowerShell
Olá comandos de exemplo seguintes mostram como tooreplace Olá conteúdo existente de um runbook com conteúdos de Olá de um ficheiro de script. Tenha em atenção que isto é Olá mesmo procedimento como de exemplo [tooimport um runbook a partir de um ficheiro de script com o Windows PowerShell](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>Artigos relacionados
* [Criar ou importar um runbook na automatização do Azure](automation-creating-importing-runbook.md)
* [Fluxo de trabalho do PowerShell de aprendizagem](automation-powershell-workflow.md)
* [Gráfico de criação na automatização do Azure](automation-graphical-authoring-intro.md)
* [Certificados](automation-certificates.md)
* [Ligações](automation-connections.md)
* [Credenciais](automation-credentials.md)
* [Agendas](automation-schedules.md)
* [Variáveis](automation-variables.md)
