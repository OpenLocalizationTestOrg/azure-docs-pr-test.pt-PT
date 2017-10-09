---
title: "aaaRun runbooks num trabalho de Runbook híbrida de automatização do Azure | Microsoft Docs"
description: "Este artigo fornece informações sobre a execução de runbooks em computadores no seu local datacenter ou o fornecedor de nuvem com a função de trabalho de Runbook híbrida Olá."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/22/2017
ms.author: magoedte
ms.openlocfilehash: 51961e02603e5690edd11e577594ad2ddea489a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a>Runbooks em execução num Runbook Worker híbrido 
Não há qualquer diferença na estrutura de Olá de runbooks que são executados na automatização do Azure e os que executam o um Runbook Worker híbrido. Os Runbooks que utiliza com cada provavelmente diferem significativamente entanto, uma vez que os runbooks direcionada para um Runbook Worker híbrido normalmente gerir recursos no computador local de Olá próprio ou relativamente aos recursos no ambiente local olá onde está implementada, enquanto os runbooks na automatização do Azure, normalmente, gerir recursos no Olá em nuvem do Azure.

Pode editar um runbook para o trabalho de Runbook híbrida na automatização do Azure, mas poderão ter dificuldades tente tootest Olá runbook no editor de Olá.  módulos do PowerShell Olá que acedem a recursos locais Olá poderão não estar instalados no seu ambiente de automatização do Azure sendo que nesse caso, o teste de Olá irão falhar.  Se instalar Olá necessário módulos, em seguida, Olá runbook será executado, mas não será capaz de tooaccess recursos locais para um teste completo.

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a>A iniciar um runbook no Runbook Worker híbrido
[Iniciar um Runbook na automatização do Azure](automation-starting-a-runbook.md) descreve diferentes métodos para iniciar um runbook.  Runbook Worker híbrido adiciona um **RunOn** opção onde pode especificar o nome de Olá de um grupo de trabalho de Runbook híbrida.  Se não for especificado um grupo, Olá runbook é obtida e execute dos trabalhadores Olá nesse grupo.  Se esta opção não for especificada, em seguida, é executado na automatização do Azure como habitualmente.

Quando inicia um runbook no portal do Azure de Olá, é-lhe apresentado um **executar em** opção onde pode selecionar **Azure** ou **Worker híbrido**.  Se selecionar **Worker híbrido**, em seguida, pode selecionar Olá grupo a partir de uma lista pendente.

Olá utilize **RunOn** parâmetro.  Pode utilizar os seguintes comandos toostart um runbook denominado Test-Runbook num grupo de trabalho de Runbook híbrida MyHybridGroup através do Windows PowerShell com o nome de Olá.

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> Olá **RunOn** parâmetro foi adicionado toohello **início AzureAutomationRunbook** cmdlet na versão 0.9.1 do Microsoft Azure PowerShell.  Deve [transferir a versão mais recente Olá](https://azure.microsoft.com/downloads/) se tiver um anteriormente instalado.  Basta tooinstall esta versão numa estação de trabalho em que estiver a iniciar o runbook Olá a partir do Windows PowerShell.  Não é necessário tooinstall-lo no computador de trabalho de Olá, exceto se tenciona toostart runbooks desse computador.  Atualmente não é possível iniciar um runbook num Runbook Worker híbrido partir de outro runbook, uma vez que isto iria requer a versão mais recente do Olá do toobe Azure Powershell instalada na sua conta de automatização.  versão mais recente Olá é atualizada automaticamente na automatização do Azure e instalada automaticamente pendente toohello workers em breve.
>
>

## <a name="runbook-permissions"></a>Permissões de Runbook
Os Runbooks em execução num Runbook Worker híbrido não é possível utilizar Olá mesmo método que é normalmente utilizado para autenticar tooAzure recursos, uma vez que estão a aceder a recursos fora do Azure de runbooks.  Olá runbook pode fornecer a suas próprias autenticação toolocal recursos ou pode especificar um tooprovide de conta RunAs um contexto de utilizador para todos os runbooks.

### <a name="runbook-authentication"></a>Autenticação de Runbook
Por predefinição, os runbooks será executado no contexto de Olá de Olá conta do sistema local no Olá num computador local, pelo que têm de fornecer as suas próprias tooresources de autenticação que acedem.  

Pode utilizar [credencial](http://msdn.microsoft.com/library/dn940015.aspx) e [certificado](http://msdn.microsoft.com/library/dn940013.aspx) ativos no runbook com os cmdlets que lhe permitem toospecify credenciais pelo que pode autenticar toodifferent recursos.  Olá exemplo seguinte mostra uma parte de um runbook que reinicia um computador.  Este obtém as credenciais a partir de um nome de recurso e Olá de credenciais de computador Olá de um recurso de variável e, em seguida, utiliza estes valores com o cmdlet Olá reiniciar o computador.

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

Também pode tirar partido [InlineScript](automation-powershell-workflow.md#inlinescript), que lhe permite toorun blocos de código noutro computador com as credenciais especificadas pelo Olá [parâmetro comum de PSCredential](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="runas-account"></a>Conta RunAs
Em vez de ter runbooks fornecer as seus próprios autenticação toolocal recursos, pode especificar um **RunAs** conta para um grupo de trabalho híbrida.  Especificar um [recurso de credencial](automation-credentials.md) que tenha acesso toolocal recursos e todos os runbooks executados estas credenciais quando em execução num Runbook Worker híbrido no grupo de Olá.  

nome de utilizador de Olá credencial Olá tem de ser dos seguintes formatos de Olá:

* domínio ome de utilizador
* username@domain
* nome de utilizador (para contas locais toohello num computador local)

Utilize Olá seguir o procedimento toospecify uma conta RunAs para um grupo de trabalho híbridas:

1. Criar um [recurso de credencial](automation-credentials.md) com toolocal aceder a recursos.
2. Abra a conta de automatização de Olá no Olá portal do Azure.
3. Selecione Olá **grupos de trabalho híbrida** mosaico e, em seguida, selecione o grupo de Olá.
4. Selecione **todas as definições** e, em seguida, **definições do grupo de trabalho híbrida**.
5. Alteração **Run** de **predefinido** demasiado**personalizada**.
6. Selecione credenciais Olá e clique em **guardar**.

### <a name="automation-run-as-account"></a>Conta Run As de automatização
Como parte do processo de compilação automatizada para a implementação de recursos no Azure, poderá ser necessário acesso tooon local sistemas toosupport uma tarefa ou o conjunto de passos na sua sequência de implementação.  autenticação de toosupport no Azure utilizando a conta Run As de Olá, terá de tooinstall Olá Run certificado da conta.  

Olá runbook do PowerShell, os seguintes *exportação RunAsCertificateToHybridWorker*, exporta Olá Run certificado da sua conta de automatização do Azure e transfere e importa-os para arquivo de certificados do computador local Olá num Função de trabalho híbrida ligado toohello mesma conta.  Depois de concluído este passo, verifica trabalho Olá pode autenticar com êxito tooAzure com Olá a conta Run As.

    <#PSScriptInfo
    .VERSION 1.0
    .GUID 3a796b9a-623d-499d-86c8-c249f10a6986
    .AUTHOR Azure Automation Team
    .COMPANYNAME Microsoft
    .COPYRIGHT 
    .TAGS Azure Automation 
    .LICENSEURI 
    .PROJECTURI 
    .ICONURI 
    .EXTERNALMODULEDEPENDENCIES 
    .REQUIREDSCRIPTS 
    .EXTERNALSCRIPTDEPENDENCIES 
    .RELEASENOTES
    #>

    <#  
    .SYNOPSIS  
    Exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account. 
  
    .DESCRIPTION  
    This runbook exports hello Run As certificate from an Azure Automation account tooa hybrid worker in that account.
    Run this runbook in hello hybrid worker where you want hello certificate installed.
    This allows hello use of hello AzureRunAsConnection tooauthenticate tooAzure and manage Azure resources from runbooks running in hello hybrid worker.

    .EXAMPLE
    .\Export-RunAsCertificateToHybridWorker

    .NOTES
    AUTHOR: Azure Automation Team 
    LASTEDIT: 2016.10.13
    #>

    [OutputType([string])] 

    # Set hello password used for this certificate
    $Password = "YourStrongPasswordForTheCert"

    # Stop on errors
    $ErrorActionPreference = 'stop'

    # Get hello management certificate that will be used toomake calls into Azure Service Management resources
    $RunAsCert = Get-AutomationCertificate -Name "AzureRunAsCertificate"
       
    # location toostore temporary certificate in hello Automation service host
    $CertPath = Join-Path $env:temp  "AzureRunAsCertificate.pfx"
   
    # Save hello certificate
    $Cert = $RunAsCert.Export("pfx",$Password)
    Set-Content -Value $Cert -Path $CertPath -Force -Encoding Byte | Write-Verbose 

    Write-Output ("Importing certificate into $env:computername local machine root store from " + $CertPath)
    $SecurePassword = ConvertTo-SecureString $Password -AsPlainText -Force
    Import-PfxCertificate -FilePath $CertPath -CertStoreLocation Cert:\LocalMachine\My -Password $SecurePassword -Exportable | Write-Verbose

    # Test that authentication tooAzure Resource Manager is working
    $RunAsConnection = Get-AutomationConnection -Name "AzureRunAsConnection" 
    
    Add-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $RunAsConnection.TenantId `
      -ApplicationId $RunAsConnection.ApplicationId `
      -CertificateThumbprint $RunAsConnection.CertificateThumbprint | Write-Verbose

    Set-AzureRmContext -SubscriptionId $RunAsConnection.SubscriptionID | Write-Verbose

    # List automation accounts tooconfirm Azure Resource Manager calls are working
    Get-AzureRmAutomationAccount | Select AutomationAccountName

Guardar Olá *exportação RunAsCertificateToHybridWorker* runbook tooyour computador com um `.ps1` extensão.  Importe-o para a sua conta de automatização e editar runbook Olá, alterar Olá valor da variável de Olá `$Password` com a sua própria palavra-passe.  Publicar e, em seguida, executar o runbook de Olá direcionada para o grupo de trabalho híbrida Olá que são executados e autenticar runbooks com Olá a conta Run As.  Olá tarefa fluxo relatórios Olá tentativa tooimport Olá certificado no arquivo do computador local Olá e forma com várias linhas, dependendo de quantos contas de automatização são definidas na sua subscrição e se a autenticação é efetuada com êxito.  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a>Resolução de problemas de runbooks num Runbook Worker híbrido
Os registos são armazenados localmente em cada função de trabalho híbrida no C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.  Função de trabalho híbrida também regista eventos e erros no registo de eventos do Windows hello em **aplicações e serviços Logs\Microsoft-SMA\Operational**.  Eventos relacionados com toorunbooks executadas no trabalho Olá são escritas demasiado**aplicações e serviços Logs\Microsoft-Automation\Operational**.  Olá **Microsoft SMA** registo inclui muitas mais eventos relacionados toohello runbook tarefa toohello premido worker e Olá processamento de Olá runbook.  Ao hello **automatização do Microsoft** registo de eventos tem muitos eventos com detalhes a prestar assistência na resolução de problemas de Olá de execução do runbook, pelo menos encontrará Olá os resultados da tarefa de runbook Olá.  

[Runbook de saída e mensagens](automation-runbook-output-and-messages.md) são enviados tooAzure Automation a partir de híbridos apenas como tarefas de runbook executadas na nuvem de Olá.  Também pode ativar Olá verboso e fluxos de progresso Olá mesma forma que faria para outros runbooks.  

Se os runbooks não são concluir com êxito e a tarefa de Olá resumo mostra um Estado de **suspenso**, reveja o artigo de resolução de problemas de Olá [Runbook Worker híbrido: uma tarefa de runbook termina com o Estado Suspenso](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).   

## <a name="next-steps"></a>Passos seguintes
* toolearn mais informações sobre os diferentes métodos de Olá que podem ser utilizado toostart um runbook, consulte [iniciar um Runbook na automatização do Azure](automation-starting-a-runbook.md).  
* toounderstand Olá diferentes os procedimentos para trabalhar com runbooks do PowerShell e o fluxo de trabalho do PowerShell na automatização do Azure utilizando o editor de texto Olá, consulte [editar um Runbook na automatização do Azure](automation-edit-textual-runbook.md)
