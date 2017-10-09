---
title: "aaaCreating ou importar um runbook na automatização do Azure"
description: "Este artigo descreve como toocreate um novo runbook na automatização do Azure ou importar um de um ficheiro."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Criar ou importar um runbook na automatização do Azure
Pode adicionar um tooAzure de runbook da automatização, [criar uma nova](#creating-a-new-runbook) ou ao importar um runbook existente a partir de um ficheiro ou de Olá [Galeria de Runbooks](automation-runbook-gallery.md). Este artigo fornece informações sobre como criar e importar runbooks a partir de um ficheiro.  Pode obter todos os detalhes de Olá em aceder a Comunidade runbooks e módulos no [galleries módulos e Runbooks de automatização do Azure](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Criar um novo runbook
Pode criar um novo runbook na automatização do Azure utilizando um dos Olá Azure portais ou o Windows PowerShell. Quando tiver sido criada Olá runbook, pode editá-la utilizando as informações no [Learning fluxo de trabalho do PowerShell](automation-powershell-workflow.md) e [a criação de gráficos na automatização do Azure](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate um novo runbook de automatização do Azure com o portal clássico do Azure Olá
Apenas pode trabalhar com [runbooks do fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) no Olá portal do Azure.

1. No portal clássico do Azure Olá, clique em, **novo**, **serviços aplicacionais**, **automatização**, **Runbook**, **criaçãorápida**.
2. Introduza as informações de Olá necessário e, em seguida, clique em **criar**. nome do runbook Olá tem de começar com uma letra e pode ter letras, números, carateres de sublinhado e travessões.
3. Se pretender que tooedit Olá runbook agora, em seguida, clique em **editar Runbook**. Caso contrário, clique em **OK**.
4. O seu runbook novo aparecerá no Olá **Runbooks** separador.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate um novo runbook de automatização do Azure com Olá portal do Azure
1. No portal do Azure Olá, abra a sua conta de automatização.
2. A partir da Olá Hub, selecione **Runbooks** lista de Olá tooopen de runbooks.
3. Clique em Olá **adicionar um runbook** botão e, em seguida, **criar um novo runbook**.
4. Escreva um **nome** para Olá runbook e selecione o [tipo](automation-runbook-types.md). nome do runbook Olá tem de começar com uma letra e pode ter letras, números, carateres de sublinhado e travessões.
5. Clique em **criar** toocreate Olá runbook e editor Olá aberta.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate um novo runbook de automatização do Azure com o Windows PowerShell
Pode utilizar Olá [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate vazio [runbook de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Pode especificar Olá **nome** parâmetro toocreate um runbook vazio, que pode editar mais tarde ou pode especificar Olá **caminho** parâmetro tooimport um ficheiro de runbook. Olá **tipo** parâmetro também deve ser incluída toospecify um dos tipos de runbook Olá quatro.

seguinte Olá mostrar os comandos de exemplo como toocreate um novo runbook vazio.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Importar um runbook a partir de um ficheiro para a automatização do Azure
Pode criar um novo runbook na automatização do Azure através da importação de um script do PowerShell ou o fluxo de trabalho do PowerShell (extensão. ps1) ou um runbook gráfico exportado (. graphrunbook).  Tem de especificar Olá [tipo de runbook](automation-runbook-types.md) que será criada a partir de importação de Olá tendo em Olá conta seguintes considerações.

* Um ficheiro. graphrunbook só pode ser importado para um novo [runbook gráfico](automation-runbook-types.md#graphical-runbooks), e runbooks gráficos só podem ser criados a partir de um ficheiro. graphrunbook.
* Um ficheiro. ps1, que contém um fluxo de trabalho do PowerShell só pode ser importado para um [runbook de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Se o ficheiro de Olá contém vários fluxos de trabalho do PowerShell, em seguida, Olá importação falhará. Tem de guardar cada ficheiro próprio do fluxo de trabalho tooits e importar cada separadamente.
* Um ficheiro. ps1, que não contenha um fluxo de trabalho pode ser importado para o um [runbook do PowerShell](automation-runbook-types.md#powershell-runbooks) ou um [runbook de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Se for importado para um runbook de fluxo de trabalho do PowerShell, em seguida, será convertida tooa fluxo de trabalho e os comentários serão incluídos no runbook Olá especificando as alterações de Olá efetuadas.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport um runbook a partir de um ficheiro com o portal clássico do Azure Olá
Pode utilizar Olá seguir o procedimento tooimport um ficheiro de script para a automatização do Azure.  Tenha em atenção que só pode importar um ficheiro. ps1 para um runbook de fluxo de trabalho do PowerShell com este portal.  Tem de utilizar Olá portal do Azure para outros tipos.

1. No portal de gestão do Azure Olá, selecione **automatização** e, em seguida, selecione uma conta de automatização.
2. Clique em **importar**.
3. Clique em **Procurar ficheiro** e localize tooimport de ficheiro de script de Olá.
4. Se pretender que tooedit Olá runbook agora, em seguida, clique em **editar Runbook**. Caso contrário, clique em OK.
5. Olá novo runbook serão apresentados na Olá **Runbooks** separador para Olá conta de automatização.
6. Tem [publicar o runbook Olá](#publishing-a-runbook) antes de pode executá-lo.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport um runbook a partir de um ficheiro com Olá portal do Azure
Pode utilizar Olá seguir o procedimento tooimport um ficheiro de script para a automatização do Azure.  

> [!NOTE]
> Tenha em atenção que só pode importar um ficheiro. ps1 para um runbook de fluxo de trabalho do PowerShell através do portal Olá.
> 
> 

1. No portal do Azure Olá, abra a sua conta de automatização.
2. A partir da Olá Hub, selecione **Runbooks** lista de Olá tooopen de runbooks.
3. Clique em Olá **adicionar um runbook** botão e, em seguida, **importação**.
4. Clique em **Runbook ficheiro** tooselect Olá ficheiro tooimport
5. Se hello **nome** campo está ativado, então tem Olá opção toochange-lo.  nome do runbook Olá tem de começar com uma letra e pode ter letras, números, carateres de sublinhado e travessões.
6. Olá [tipo de runbook](automation-runbook-types.md) será selecionada automaticamente, mas pode alterar o tipo de Olá após obter restrições de aplicável Olá na conta. 
7. Olá novo runbook irá aparecer na lista de Olá de runbooks para Olá conta de automatização.
8. Tem [publicar o runbook Olá](#publishing-a-runbook) antes de pode executá-lo.

> [!NOTE]
> Depois de importar um runbook gráfico ou um runbook gráfico de fluxo de trabalho do PowerShell, tem Olá opção tooconvert toohello outro tipo se pretendesse. Não é possível converter tootextual.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport um runbook a partir de um ficheiro de script com o Windows PowerShell
Pode utilizar Olá [importação AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport um ficheiro de script como um rascunho do runbook de fluxo de trabalho do PowerShell. Se já existe um runbook de Olá, importação Olá falhará a menos que utilize Olá *-Force* parâmetro. 

Olá comandos de exemplo a seguir mostra como tooimport um script de ficheiros num runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Publicar um runbook
Quando criar ou importar um runbook novo, tem de o publicar antes de pode executá-lo.  Cada runbook na automatização possui um rascunho e uma versão publicada. Apenas a versão publicada Olá é toobe disponível executar e versão de rascunho de Olá só pode ser editada. versão do Olá publicada não é afetada por qualquer versão de rascunho de toohello de alterações. Quando deve ser disponibilizada versão de rascunho de Olá, em seguida, publica-o que substitui a versão publicada de Olá com a versão de rascunho de Olá.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish um runbook através do portal clássico do Azure Olá
1. Abra o runbook de Olá no portal clássico do Azure Olá.
2. Olá parte superior do ecrã de Olá, clique em **autor**.
3. Na Olá na parte inferior do ecrã de Olá, clique em **publicar** e, em seguida, **Sim** toohello mensagem de verificação.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish um runbook com Olá portal do Azure
1. Abra o runbook Olá Olá portal do Azure.
2. Clique em Olá **editar** botão.
3. Clique em Olá **publicar** botão e, em seguida, **Sim** toohello mensagem de verificação.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>toopublish um runbook com o Windows PowerShell
Pode utilizar Olá [publicar AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish um runbook com o Windows PowerShell. seguinte Olá mostrar os comandos de exemplo como toopublish um runbook de exemplo.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Passos Seguintes
* toolearn sobre como pode beneficiar Olá Runbook e Galeria de módulo do PowerShell, consulte [galleries módulos e Runbooks de automatização do Azure](automation-runbook-gallery.md)
* toolearn mais sobre a edição de runbooks do PowerShell e o fluxo de trabalho do PowerShell com um editor de texto, consulte [editar textual runbooks na automatização do Azure](automation-edit-textual-runbook.md)
* toolearn mais informações sobre a criação de runbooks gráficos, consulte [a criação de gráficos na automatização do Azure](automation-graphical-authoring-intro.md)

