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
# <a name="running-runbooks-on-a-hybrid-runbook-worker"></a><span data-ttu-id="0eea9-103">Runbooks em execução num Runbook Worker híbrido</span><span class="sxs-lookup"><span data-stu-id="0eea9-103">Running runbooks on a Hybrid Runbook Worker</span></span> 
<span data-ttu-id="0eea9-104">Não há qualquer diferença na estrutura de Olá de runbooks que são executados na automatização do Azure e os que executam o um Runbook Worker híbrido.</span><span class="sxs-lookup"><span data-stu-id="0eea9-104">There is no difference in hello structure of runbooks that run in Azure Automation and those that run on a Hybrid Runbook Worker.</span></span> <span data-ttu-id="0eea9-105">Os Runbooks que utiliza com cada provavelmente diferem significativamente entanto, uma vez que os runbooks direcionada para um Runbook Worker híbrido normalmente gerir recursos no computador local de Olá próprio ou relativamente aos recursos no ambiente local olá onde está implementada, enquanto os runbooks na automatização do Azure, normalmente, gerir recursos no Olá em nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="0eea9-105">Runbooks that you use with each most likely differ significantly though since runbooks targeting a Hybrid Runbook Worker typically manage resources on hello local computer itself or against resources in hello local environment where it is deployed, while runbooks in Azure Automation typically manage resources in hello Azure cloud.</span></span>

<span data-ttu-id="0eea9-106">Pode editar um runbook para o trabalho de Runbook híbrida na automatização do Azure, mas poderão ter dificuldades tente tootest Olá runbook no editor de Olá.</span><span class="sxs-lookup"><span data-stu-id="0eea9-106">You can edit a runbook for Hybrid Runbook Worker in Azure Automation, but you may have difficulties if you try tootest hello runbook in hello editor.</span></span>  <span data-ttu-id="0eea9-107">módulos do PowerShell Olá que acedem a recursos locais Olá poderão não estar instalados no seu ambiente de automatização do Azure sendo que nesse caso, o teste de Olá irão falhar.</span><span class="sxs-lookup"><span data-stu-id="0eea9-107">hello PowerShell modules that access hello local resources may not be installed in your Azure Automation environment in which case, hello test would fail.</span></span>  <span data-ttu-id="0eea9-108">Se instalar Olá necessário módulos, em seguida, Olá runbook será executado, mas não será capaz de tooaccess recursos locais para um teste completo.</span><span class="sxs-lookup"><span data-stu-id="0eea9-108">If you do install hello required modules, then hello runbook will run, but it will not be able tooaccess local resources for a complete test.</span></span>

## <a name="starting-a-runbook-on-hybrid-runbook-worker"></a><span data-ttu-id="0eea9-109">A iniciar um runbook no Runbook Worker híbrido</span><span class="sxs-lookup"><span data-stu-id="0eea9-109">Starting a runbook on Hybrid Runbook Worker</span></span>
<span data-ttu-id="0eea9-110">[Iniciar um Runbook na automatização do Azure](automation-starting-a-runbook.md) descreve diferentes métodos para iniciar um runbook.</span><span class="sxs-lookup"><span data-stu-id="0eea9-110">[Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) describes different methods for starting a runbook.</span></span>  <span data-ttu-id="0eea9-111">Runbook Worker híbrido adiciona um **RunOn** opção onde pode especificar o nome de Olá de um grupo de trabalho de Runbook híbrida.</span><span class="sxs-lookup"><span data-stu-id="0eea9-111">Hybrid Runbook Worker adds a **RunOn** option where you can specify hello name of a Hybrid Runbook Worker Group.</span></span>  <span data-ttu-id="0eea9-112">Se não for especificado um grupo, Olá runbook é obtida e execute dos trabalhadores Olá nesse grupo.</span><span class="sxs-lookup"><span data-stu-id="0eea9-112">If a group is specified, then hello runbook is retrieved and run by of hello workers in that group.</span></span>  <span data-ttu-id="0eea9-113">Se esta opção não for especificada, em seguida, é executado na automatização do Azure como habitualmente.</span><span class="sxs-lookup"><span data-stu-id="0eea9-113">If this option is not specified, then it is run in Azure Automation as normal.</span></span>

<span data-ttu-id="0eea9-114">Quando inicia um runbook no portal do Azure de Olá, é-lhe apresentado um **executar em** opção onde pode selecionar **Azure** ou **Worker híbrido**.</span><span class="sxs-lookup"><span data-stu-id="0eea9-114">When you start a runbook in hello Azure portal, you are presented with a **Run on** option where you can select **Azure** or **Hybrid Worker**.</span></span>  <span data-ttu-id="0eea9-115">Se selecionar **Worker híbrido**, em seguida, pode selecionar Olá grupo a partir de uma lista pendente.</span><span class="sxs-lookup"><span data-stu-id="0eea9-115">If you select **Hybrid Worker**, then you can select hello group from a dropdown.</span></span>

<span data-ttu-id="0eea9-116">Olá utilize **RunOn** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0eea9-116">Use hello **RunOn** parameter.</span></span>  <span data-ttu-id="0eea9-117">Pode utilizar os seguintes comandos toostart um runbook denominado Test-Runbook num grupo de trabalho de Runbook híbrida MyHybridGroup através do Windows PowerShell com o nome de Olá.</span><span class="sxs-lookup"><span data-stu-id="0eea9-117">You can use hello following command toostart a runbook named Test-Runbook on a Hybrid Runbook Worker Group named MyHybridGroup using Windows PowerShell.</span></span>

    Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -RunOn "MyHybridGroup"

> [!NOTE]
> <span data-ttu-id="0eea9-118">Olá **RunOn** parâmetro foi adicionado toohello **início AzureAutomationRunbook** cmdlet na versão 0.9.1 do Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eea9-118">hello **RunOn** parameter was added toohello **Start-AzureAutomationRunbook** cmdlet in version 0.9.1 of Microsoft Azure PowerShell.</span></span>  <span data-ttu-id="0eea9-119">Deve [transferir a versão mais recente Olá](https://azure.microsoft.com/downloads/) se tiver um anteriormente instalado.</span><span class="sxs-lookup"><span data-stu-id="0eea9-119">You should [download hello latest version](https://azure.microsoft.com/downloads/) if you have an earlier one installed.</span></span>  <span data-ttu-id="0eea9-120">Basta tooinstall esta versão numa estação de trabalho em que estiver a iniciar o runbook Olá a partir do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eea9-120">You only need tooinstall this version on a workstation where you are starting hello runbook from Windows PowerShell.</span></span>  <span data-ttu-id="0eea9-121">Não é necessário tooinstall-lo no computador de trabalho de Olá, exceto se tenciona toostart runbooks desse computador.</span><span class="sxs-lookup"><span data-stu-id="0eea9-121">You do not need tooinstall it on hello worker computer unless you intend toostart runbooks from that computer.</span></span>  <span data-ttu-id="0eea9-122">Atualmente não é possível iniciar um runbook num Runbook Worker híbrido partir de outro runbook, uma vez que isto iria requer a versão mais recente do Olá do toobe Azure Powershell instalada na sua conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="0eea9-122">You cannot currently start a runbook on a Hybrid Runbook Worker from another runbook since this would require hello latest version of Azure Powershell toobe installed in your Automation account.</span></span>  <span data-ttu-id="0eea9-123">versão mais recente Olá é atualizada automaticamente na automatização do Azure e instalada automaticamente pendente toohello workers em breve.</span><span class="sxs-lookup"><span data-stu-id="0eea9-123">hello latest version is automatically updated in Azure Automation and automatically pushed down toohello workers soon.</span></span>
>
>

## <a name="runbook-permissions"></a><span data-ttu-id="0eea9-124">Permissões de Runbook</span><span class="sxs-lookup"><span data-stu-id="0eea9-124">Runbook permissions</span></span>
<span data-ttu-id="0eea9-125">Os Runbooks em execução num Runbook Worker híbrido não é possível utilizar Olá mesmo método que é normalmente utilizado para autenticar tooAzure recursos, uma vez que estão a aceder a recursos fora do Azure de runbooks.</span><span class="sxs-lookup"><span data-stu-id="0eea9-125">Runbooks running on a Hybrid Runbook Worker cannot use hello same method that is typically used for runbooks authenticating tooAzure resources, since they are accessing resources outside of Azure.</span></span>  <span data-ttu-id="0eea9-126">Olá runbook pode fornecer a suas próprias autenticação toolocal recursos ou pode especificar um tooprovide de conta RunAs um contexto de utilizador para todos os runbooks.</span><span class="sxs-lookup"><span data-stu-id="0eea9-126">hello runbook can either provide its own authentication toolocal resources, or you can specify a RunAs account tooprovide a user context for all runbooks.</span></span>

### <a name="runbook-authentication"></a><span data-ttu-id="0eea9-127">Autenticação de Runbook</span><span class="sxs-lookup"><span data-stu-id="0eea9-127">Runbook authentication</span></span>
<span data-ttu-id="0eea9-128">Por predefinição, os runbooks será executado no contexto de Olá de Olá conta do sistema local no Olá num computador local, pelo que têm de fornecer as suas próprias tooresources de autenticação que acedem.</span><span class="sxs-lookup"><span data-stu-id="0eea9-128">By default, runbooks will run in hello context of hello local System account on hello on-premises computer, so they must provide their own authentication tooresources that they will access.</span></span>  

<span data-ttu-id="0eea9-129">Pode utilizar [credencial](http://msdn.microsoft.com/library/dn940015.aspx) e [certificado](http://msdn.microsoft.com/library/dn940013.aspx) ativos no runbook com os cmdlets que lhe permitem toospecify credenciais pelo que pode autenticar toodifferent recursos.</span><span class="sxs-lookup"><span data-stu-id="0eea9-129">You can use [Credential](http://msdn.microsoft.com/library/dn940015.aspx) and [Certificate](http://msdn.microsoft.com/library/dn940013.aspx) assets in your runbook with cmdlets that allow you toospecify credentials so you can authenticate toodifferent resources.</span></span>  <span data-ttu-id="0eea9-130">Olá exemplo seguinte mostra uma parte de um runbook que reinicia um computador.</span><span class="sxs-lookup"><span data-stu-id="0eea9-130">hello following example shows a portion of a runbook that restarts a computer.</span></span>  <span data-ttu-id="0eea9-131">Este obtém as credenciais a partir de um nome de recurso e Olá de credenciais de computador Olá de um recurso de variável e, em seguida, utiliza estes valores com o cmdlet Olá reiniciar o computador.</span><span class="sxs-lookup"><span data-stu-id="0eea9-131">It retrieves credentials from a credential asset and hello name of hello computer from a variable asset and then uses these values with hello Restart-Computer cmdlet.</span></span>

    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -Name "MyCredential"
    $Computer = Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" -Name  "ComputerName"

    Restart-Computer -ComputerName $Computer -Credential $Cred

<span data-ttu-id="0eea9-132">Também pode tirar partido [InlineScript](automation-powershell-workflow.md#inlinescript), que lhe permite toorun blocos de código noutro computador com as credenciais especificadas pelo Olá [parâmetro comum de PSCredential](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="0eea9-132">You can also leverage [InlineScript](automation-powershell-workflow.md#inlinescript), which  allows you toorun blocks of code on another computer with credentials specified by hello [PSCredential common parameter](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="runas-account"></a><span data-ttu-id="0eea9-133">Conta RunAs</span><span class="sxs-lookup"><span data-stu-id="0eea9-133">RunAs account</span></span>
<span data-ttu-id="0eea9-134">Em vez de ter runbooks fornecer as seus próprios autenticação toolocal recursos, pode especificar um **RunAs** conta para um grupo de trabalho híbrida.</span><span class="sxs-lookup"><span data-stu-id="0eea9-134">Instead of having runbooks provide their own authentication toolocal resources, you can specify a **RunAs** account for a Hybrid worker group.</span></span>  <span data-ttu-id="0eea9-135">Especificar um [recurso de credencial](automation-credentials.md) que tenha acesso toolocal recursos e todos os runbooks executados estas credenciais quando em execução num Runbook Worker híbrido no grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0eea9-135">You specify a [credential asset](automation-credentials.md) that has access toolocal resources, and all runbooks run under these credentials when running on a Hybrid Runbook Worker in hello group.</span></span>  

<span data-ttu-id="0eea9-136">nome de utilizador de Olá credencial Olá tem de ser dos seguintes formatos de Olá:</span><span class="sxs-lookup"><span data-stu-id="0eea9-136">hello user name for hello credential must be in one of hello following formats:</span></span>

* <span data-ttu-id="0eea9-137">domínio ome de utilizador</span><span class="sxs-lookup"><span data-stu-id="0eea9-137">domain\username</span></span>
* username@domain
* <span data-ttu-id="0eea9-138">nome de utilizador (para contas locais toohello num computador local)</span><span class="sxs-lookup"><span data-stu-id="0eea9-138">username (for accounts local toohello on-premises computer)</span></span>

<span data-ttu-id="0eea9-139">Utilize Olá seguir o procedimento toospecify uma conta RunAs para um grupo de trabalho híbridas:</span><span class="sxs-lookup"><span data-stu-id="0eea9-139">Use hello following procedure toospecify a RunAs account for a Hybrid worker group:</span></span>

1. <span data-ttu-id="0eea9-140">Criar um [recurso de credencial](automation-credentials.md) com toolocal aceder a recursos.</span><span class="sxs-lookup"><span data-stu-id="0eea9-140">Create a [credential asset](automation-credentials.md) with access toolocal resources.</span></span>
2. <span data-ttu-id="0eea9-141">Abra a conta de automatização de Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0eea9-141">Open hello Automation account in hello Azure portal.</span></span>
3. <span data-ttu-id="0eea9-142">Selecione Olá **grupos de trabalho híbrida** mosaico e, em seguida, selecione o grupo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0eea9-142">Select hello **Hybrid Worker Groups** tile, and then select hello group.</span></span>
4. <span data-ttu-id="0eea9-143">Selecione **todas as definições** e, em seguida, **definições do grupo de trabalho híbrida**.</span><span class="sxs-lookup"><span data-stu-id="0eea9-143">Select **All settings** and then **Hybrid worker group settings**.</span></span>
5. <span data-ttu-id="0eea9-144">Alteração **Run** de **predefinido** demasiado**personalizada**.</span><span class="sxs-lookup"><span data-stu-id="0eea9-144">Change **Run As** from **Default** too**Custom**.</span></span>
6. <span data-ttu-id="0eea9-145">Selecione credenciais Olá e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0eea9-145">Select hello credential and click **Save**.</span></span>

### <a name="automation-run-as-account"></a><span data-ttu-id="0eea9-146">Conta Run As de automatização</span><span class="sxs-lookup"><span data-stu-id="0eea9-146">Automation Run As account</span></span>
<span data-ttu-id="0eea9-147">Como parte do processo de compilação automatizada para a implementação de recursos no Azure, poderá ser necessário acesso tooon local sistemas toosupport uma tarefa ou o conjunto de passos na sua sequência de implementação.</span><span class="sxs-lookup"><span data-stu-id="0eea9-147">As part of your automated build process for deploying resources in Azure, you may require access tooon-premise systems toosupport a task or set of steps in your deployment sequence.</span></span>  <span data-ttu-id="0eea9-148">autenticação de toosupport no Azure utilizando a conta Run As de Olá, terá de tooinstall Olá Run certificado da conta.</span><span class="sxs-lookup"><span data-stu-id="0eea9-148">toosupport authentication against Azure using hello Run As account, you need tooinstall hello Run As account certificate.</span></span>  

<span data-ttu-id="0eea9-149">Olá runbook do PowerShell, os seguintes *exportação RunAsCertificateToHybridWorker*, exporta Olá Run certificado da sua conta de automatização do Azure e transfere e importa-os para arquivo de certificados do computador local Olá num Função de trabalho híbrida ligado toohello mesma conta.</span><span class="sxs-lookup"><span data-stu-id="0eea9-149">hello following PowerShell runbook, *Export-RunAsCertificateToHybridWorker*, exports hello Run As certificate from your Azure Automation account and downloads and imports it into hello local machine certificate store on a Hybrid worker connected toohello same account.</span></span>  <span data-ttu-id="0eea9-150">Depois de concluído este passo, verifica trabalho Olá pode autenticar com êxito tooAzure com Olá a conta Run As.</span><span class="sxs-lookup"><span data-stu-id="0eea9-150">Once that step is completed, it verifies hello worker can successfully authenticate tooAzure using hello Run As account.</span></span>

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

<span data-ttu-id="0eea9-151">Guardar Olá *exportação RunAsCertificateToHybridWorker* runbook tooyour computador com um `.ps1` extensão.</span><span class="sxs-lookup"><span data-stu-id="0eea9-151">Save hello *Export-RunAsCertificateToHybridWorker* runbook tooyour computer with a `.ps1` extension.</span></span>  <span data-ttu-id="0eea9-152">Importe-o para a sua conta de automatização e editar runbook Olá, alterar Olá valor da variável de Olá `$Password` com a sua própria palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="0eea9-152">Import it into your Automation account and edit hello runbook, changing hello value of hello variable `$Password` with your own password.</span></span>  <span data-ttu-id="0eea9-153">Publicar e, em seguida, executar o runbook de Olá direcionada para o grupo de trabalho híbrida Olá que são executados e autenticar runbooks com Olá a conta Run As.</span><span class="sxs-lookup"><span data-stu-id="0eea9-153">Publish and then run hello runbook targeting hello Hybrid Worker group that run and authenticate runbooks using hello Run As account.</span></span>  <span data-ttu-id="0eea9-154">Olá tarefa fluxo relatórios Olá tentativa tooimport Olá certificado no arquivo do computador local Olá e forma com várias linhas, dependendo de quantos contas de automatização são definidas na sua subscrição e se a autenticação é efetuada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0eea9-154">hello job stream reports hello attempt tooimport hello certificate into hello local machine store, and follows with multiple lines depending on how many Automation accounts are defined in your subscription and if authentication is successful.</span></span>  

## <a name="troubleshooting-runbooks-on-hybrid-runbook-worker"></a><span data-ttu-id="0eea9-155">Resolução de problemas de runbooks num Runbook Worker híbrido</span><span class="sxs-lookup"><span data-stu-id="0eea9-155">Troubleshooting runbooks on Hybrid Runbook Worker</span></span>
<span data-ttu-id="0eea9-156">Os registos são armazenados localmente em cada função de trabalho híbrida no C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span><span class="sxs-lookup"><span data-stu-id="0eea9-156">Logs are stored locally on each hybrid worker at C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes.</span></span>  <span data-ttu-id="0eea9-157">Função de trabalho híbrida também regista eventos e erros no registo de eventos do Windows hello em **aplicações e serviços Logs\Microsoft-SMA\Operational**.</span><span class="sxs-lookup"><span data-stu-id="0eea9-157">Hybrid worker also records errors and events in hello Windows event log under **Application and Services Logs\Microsoft-SMA\Operational**.</span></span>  <span data-ttu-id="0eea9-158">Eventos relacionados com toorunbooks executadas no trabalho Olá são escritas demasiado**aplicações e serviços Logs\Microsoft-Automation\Operational**.</span><span class="sxs-lookup"><span data-stu-id="0eea9-158">Events related toorunbooks executed on hello worker are written too**Application and Services Logs\Microsoft-Automation\Operational**.</span></span>  <span data-ttu-id="0eea9-159">Olá **Microsoft SMA** registo inclui muitas mais eventos relacionados toohello runbook tarefa toohello premido worker e Olá processamento de Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="0eea9-159">hello **Microsoft-SMA** log includes many more events related toohello runbook job pushed toohello worker and hello processing of hello runbook.</span></span>  <span data-ttu-id="0eea9-160">Ao hello **automatização do Microsoft** registo de eventos tem muitos eventos com detalhes a prestar assistência na resolução de problemas de Olá de execução do runbook, pelo menos encontrará Olá os resultados da tarefa de runbook Olá.</span><span class="sxs-lookup"><span data-stu-id="0eea9-160">While hello **Microsoft-Automation** event log does not have many events with details assisting with hello troubleshooting of runbook execution, you will at least find hello results of hello runbook job.</span></span>  

<span data-ttu-id="0eea9-161">[Runbook de saída e mensagens](automation-runbook-output-and-messages.md) são enviados tooAzure Automation a partir de híbridos apenas como tarefas de runbook executadas na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="0eea9-161">[Runbook output and messages](automation-runbook-output-and-messages.md) are sent tooAzure Automation from hybrid workers just like runbook jobs run in hello cloud.</span></span>  <span data-ttu-id="0eea9-162">Também pode ativar Olá verboso e fluxos de progresso Olá mesma forma que faria para outros runbooks.</span><span class="sxs-lookup"><span data-stu-id="0eea9-162">You can also enable hello Verbose and Progress streams hello same way you would for other runbooks.</span></span>  

<span data-ttu-id="0eea9-163">Se os runbooks não são concluir com êxito e a tarefa de Olá resumo mostra um Estado de **suspenso**, reveja o artigo de resolução de problemas de Olá [Runbook Worker híbrido: uma tarefa de runbook termina com o Estado Suspenso](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span><span class="sxs-lookup"><span data-stu-id="0eea9-163">If your runbooks are not completing successfully and hello job summary shows a status of **Suspended**, please review hello troubleshooting article [Hybrid Runbook Worker: A runbook job terminates with a status of Suspended](automation-troubleshooting-hybrid-runbook-worker.md#a-runbook-job-terminates-with-a-status-of-suspended).</span></span>   

## <a name="next-steps"></a><span data-ttu-id="0eea9-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0eea9-164">Next steps</span></span>
* <span data-ttu-id="0eea9-165">toolearn mais informações sobre os diferentes métodos de Olá que podem ser utilizado toostart um runbook, consulte [iniciar um Runbook na automatização do Azure](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="0eea9-165">toolearn more about hello different methods that can be used toostart a runbook, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>  
* <span data-ttu-id="0eea9-166">toounderstand Olá diferentes os procedimentos para trabalhar com runbooks do PowerShell e o fluxo de trabalho do PowerShell na automatização do Azure utilizando o editor de texto Olá, consulte [editar um Runbook na automatização do Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0eea9-166">toounderstand hello different procedures for working with PowerShell and PowerShell Workflow runbooks in Azure Automation using hello textual editor, see [Editing a Runbook in Azure Automation](automation-edit-textual-runbook.md)</span></span>
