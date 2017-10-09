---
title: "aaaSource integração do controlo na automatização do Azure | Microsoft Docs"
description: "Este artigo descreve a integração de controlo de origem com o GitHub na automatização do Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Integração de controlo de código fonte da Automatização do Azure
Integração de controlo de origem permite-lhe tooassociate runbooks no seu repositório de controlo de origem do automatização conta tooa GitHub. Controlo de código fonte permite-lhe tooeasily colaborar com a sua equipa, controlar as alterações e reverter tooearlier versões dos seus runbooks. Por exemplo, controlo de código fonte permite-lhe toosync diferentes ramos no controlo de código fonte tooyour desenvolvimento, teste ou de produção as contas de automatização, tornando-o código de fácil toopromote que foi testado na produção de tooyour de ambiente de desenvolvimento automatização conta.

Controlo de código fonte permite-lhe o código de toopush do controlo de toosource de automatização do Azure ou os runbooks do controlo de origem tooAzure automatização de extração. Este artigo descreve como controlar o tooset segurança origem no seu ambiente de automatização do Azure. Iremos começar por configurar a automatização do Azure tooaccess repositório do GitHub e guiá operações diferentes que podem ser feitas através da integração do controlo de origem. 

> [!NOTE]
> Controlo de origem suporta extrair e enviar [runbooks do fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) , bem como [runbooks do PowerShell](automation-runbook-types.md#powershell-runbooks). [Runbooks gráficos](automation-runbook-types.md#graphical-runbooks) ainda não são suportadas.<br><br>
> 
> 

Existem dois passos simples tooconfigure necessário controlo de código fonte da sua conta de automatização e apenas um se já tiver uma conta GitHub. São:

## <a name="step-1--create-a-github-repository"></a>Passo 1 – criar um repositório do GitHub
Se já tiver uma conta GitHub e um repositório de que pretende toolink tooAzure automatização, em seguida, existente tooyour de início de sessão da conta e iniciar a partir do passo 2 abaixo. Caso contrário, navegue até demasiado[GitHub](https://github.com/), inscreva-se numa nova conta e [criar um novo repositório de](https://help.github.com/articles/create-a-repo/).

## <a name="step-2--set-up-source-control-in-azure-automation"></a>Passo 2 – configurar o controlo de origem na automatização do Azure
1. No painel de conta de automatização de Olá no Olá portal do Azure, clique em **segurança controlo de origem.** 
   
    ![Configurar o controlo de origem](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. Olá **controlo de código fonte** abre o painel, onde pode configurar os detalhes da sua conta GitHub. Segue-se uma lista de Olá de tooconfigure parâmetros:  
   
   | **Parâmetro** | **Descrição** |
   |:--- |:--- |
   | Escolher origem |Selecione a origem de Olá. Atualmente, apenas **GitHub** é suportada. |
   | Autorização |Clique em Olá **autorizar** repositório GitHub de tooyour acesso botão toogrant da automatização do Azure. Se tiver sessão iniciada no tooyour conta GitHub numa janela diferente, hello são utilizadas credenciais dessa conta. Depois de autorização é efetuada com êxito, o painel Olá irá mostrar o nome de utilizador do GitHub em **autorização propriedade**. |
   | Escolha o repositório |Selecione um repositório GitHub da lista de Olá dos repositórios disponíveis. |
   | Selecione o ramo |Selecione um ramo de lista de Olá de ramos disponíveis. Apenas Olá **mestre** ramo é apresentado se ainda não criou quaisquer ramos. |
   | Caminho de pasta do Runbook |caminho de pasta do runbook Olá Especifica o caminho de Olá no repositório do GitHub Olá partir do qual pretende toopush ou extraia o seu código. Têm de ser introduzido no formato de Olá **/nomedapasta/nomedasubpasta**. Apenas os runbooks existentes no caminho de pasta do runbook Olá será sincronizado tooyour conta de automatização. Os Runbooks em subpastas Olá do caminho de pasta do runbook Olá será **não** ser sincronizada com êxito. Utilize  **/**  toosync Olá todos os runbooks no repositório de Olá. |
3. Por exemplo, se tiver um repositório denominado **PowerShellScripts** que contém uma pasta denominada **RootFolder**, que contém uma pasta denominada **subpasta**. Pode utilizar Olá seguintes cadeias toosync cada nível de pasta:
   
   1. toosync runbooks **repositório**, é o caminho de pasta do runbook*/*
   2. toosync runbooks **RootFolder**, caminho de pasta do runbook é */RootFolder*
   3. toosync runbooks **subpasta**, caminho de pasta do runbook é *RootFolder/subpasta*.
4. Depois de configurar parâmetros de Olá, são apresentadas no Olá **painel de segurança de controlo de origem.**  
   
    ![Configurar o painel](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. Assim que clicar em OK, a integração do controlo de origem está agora configurada para a sua conta de automatização e deve ser atualizada com as informações do GitHub. Agora pode clicar em tooview esta parte todas o controlo de origem histórico da tarefa de sincronização.  
   
    ![Valores do repositório](media/automation-source-control-integration/automation_03_RepoValues.png)
6. Depois de configurar o controlo de origem, hello seguintes recursos de automatização serão criados na sua conta de automatização:  
   Dois [recursos de variável](automation-variables.md) são criados.  
   
   * variável de Olá **Microsoft.Azure.Automation.SourceControl.Connection** contém valores de Olá Olá da cadeia de ligação, conforme mostrado abaixo.  
     
     | **Parâmetro** | **Valor** |
     |:--- |:--- |
     | Nome |Microsoft.Azure.Automation.SourceControl.Connection |
     | Tipo |Cadeia |
     | Valor |{"Ramo":\<*o nome da sua sucursal*>, "RunbookFolderPath":\<*caminho de pasta do Runbook*>, "ProviderType":\<*tem um valor de 1 para GitHub*>, "Repositório":\<*nome do seu repositório*>, "Nomedeutilizador":\<*nome de utilizador do GitHub*>} |

    * variável de Olá **Microsoft.Azure.Automation.SourceControl.OAuthToken**, contém o valor encriptados segura do seu OAuthToken Olá.  

    |**Parâmetro**            |**Valor** |
    |:---|:---|
    | Nome  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | Tipo | UNKNOWN(Encrypted) |
    | Valor | <*OAuthToken encriptado*> |  

    ![Variáveis](media/automation-source-control-integration/automation_04_Variables.png)  

    * **Controlo de origem de automatização** é adicionado como um tooyour aplicação autorizados conta GitHub. aplicação de Olá tooview: sua home page do GitHub, navegue tooyour **perfil** > **definições** > **aplicações**. Esta aplicação permite toosync de automatização do Azure a tooan de repositório do GitHub conta de automatização.  

    ![Aplicação de Git](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>Utilizar o controlo de origem na automatização
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>Verificação num runbook do controlo de toosource de automatização do Azure
Dar entrada no Runbook permite-lhe alterações de Olá toopush efetuadas tooa runbook na automatização do Azure para o repositório de controlo de origem. Seguem-se Olá passos toocheck um runbook:

1. Da sua conta de automatização, [criar um novo runbook textual](automation-first-runbook-textual.md), ou [editar um runbook existente, textual](automation-edit-textual-runbook.md). Este runbook pode ser um fluxo de trabalho do PowerShell ou um runbook do script do PowerShell.  
2. Depois de editar o runbook, guarde-o e clique em **dar entrada no** de Olá **editar** painel.  
   
    ![Botão de Checkin](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Dar entrada da automatização do Azure irá substituir o código de Olá que atualmente existe no controlo de origem. Olá instrução de linha de comandos equivalentes do Git toocheck-in é **git adicionar + consolidação de git + git push**  

1. Ao clicar em **dar entrada no**, será apresentada uma mensagem de confirmação, clique em Sim toocontinue.  
   
    ![Mensagem de Checkin](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. Inicio de inicia Olá runbook de controlo de origem: **sincronização MicrosoftAzureAutomationAccountToGitHubV1**. Este runbook liga tooGitHub e pushes alterações a partir do repositório de tooyour de automatização do Azure. tooview Olá dar entrada no histórico da tarefa, volte atrás toohello **integração de controlo de origem** separador e clique em Painel de sincronização do repositório de Olá tooopen. Este painel mostra todas as tarefas de controlo de origem.  Selecione a tarefa de Olá pretende tooview e clique em tooview Olá detalhes.  
   
    ![Checkin Runbook](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > Os runbooks do controlo de origem são especiais runbooks de automatização que não é possível ver ou editar. Enquanto que não irão aparecer na sua lista de runbook, verá as tarefas de sincronização na sua lista de tarefas.
   > 
   > 
3. nome de Olá de runbook Olá modificado é enviado como um parâmetro de entrada toohello dar entrada no runbook. Pode [ver detalhes da tarefa Olá](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) expandindo o runbook no **repositório sincronização** painel.  
   
    ![Entrada de Checkin](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Atualize o seu repositório do GitHub após a conclusão do trabalho Olá alterações de Olá tooview.  Deverá haver uma consolidação no seu repositório com uma mensagem de consolidação: **atualizados *nome do Runbook* na automatização do Azure.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>Runbooks de sincronização do controlo de origem tooAzure automatização
botão de sincronizar Olá no painel de sincronização do repositório de Olá permite-lhe toopull Olá todos os runbooks no caminho de pasta do runbook Olá da sua conta de automatização de tooyour do repositório. Olá mesmo repositório pode ser sincronizado toomore que uma conta de automatização. Seguem-se Olá passos toosync um runbook:

1. A partir do Olá conta de automatização onde configurou o controlo de origem, abra Olá **painel de sincronização de integração/repositório de controlo de origem** e clique em **sincronização** , em seguida, será solicitado com uma confirmação mensagem, clique em **Sim** toocontinue.  
   
    ![Botão de sincronização](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Olá runbook inicia a sincronização: **sincronização MicrosoftAzureAutomationAccountFromGitHubV1**. Este runbook liga tooGitHub e obtém Olá alterações relativamente ao seu repositório de tooAzure automatização. Deverá ver uma tarefa de novo no Olá **repositório sincronização** painel para esta ação. tooview detalhes sobre a tarefa de sincronização de Olá, clique em Painel de detalhes de tarefa de Olá tooopen.  
   
    ![Runbook de sincronização](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > Uma sincronização do controlo de origem substitui a versão de rascunho de Olá de runbooks Olá que atualmente existe na sua conta de automatização para **todos os** runbooks que estão atualmente nos controlo de origem. Olá Git toosync de instrução de linha de comandos equivalentes é **solicitação de git**


## <a name="troubleshooting-source-control-problems"></a>Resolução de problemas de controlo de origem
Se existirem quaisquer erros com uma tarefa de verificação ou no sincronização, estado de tarefa de Olá deve ser suspenso e pode ver mais detalhes sobre o erro de Olá no painel de tarefas Olá.  Olá **todos os registos** parte irá mostrar-lhe Olá todos os fluxos de PowerShell associados a essa tarefa. Isto irá proporcionar-lhe detalhes Olá necessário toohelp corrigir quaisquer problemas com a entrada ou uma sincronização. Também irá mostrar-lhe Olá sequência de ações que ocorreu durante a sincronização ou a verificar. num runbook.  

![Imagem de AllLogs](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>Desligar o controlo de código fonte
toodisconnect da sua conta do GitHub, abra o painel de sincronização do repositório de Olá e clique em **desligar**. Depois de desligar o controlo de origem, os runbooks que foram sincronizados anteriormente ainda irá permanecer na sua conta de automatização, mas não será possível ativar o painel de sincronização do repositório de Olá.  

  ![Botão de desligar](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre a integração de controlo de origem, consulte Olá os seguintes recursos:  

* [Da automatização do Azure: Integração do controlo de origem na automatização do Azure](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [Votos para o seu sistema de controlo de origem favorito](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Da automatização do Azure: Controlo de origem de Runbook utilizando o Visual Studio Team Services a integração](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

