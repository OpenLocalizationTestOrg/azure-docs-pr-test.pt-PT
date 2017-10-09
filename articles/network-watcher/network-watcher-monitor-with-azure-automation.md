---
title: "gateways de VPN aaaMonitor na resolução de problemas do observador de rede do Azure | Microsoft Docs"
description: "Este artigo descreve como diagnosticar conectividade no local com a automatização do Azure e o observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="89616-103">Monitorizar os gateways de VPN com a resolução de problemas do observador de rede</span><span class="sxs-lookup"><span data-stu-id="89616-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="89616-104">Obter conhecimentos aprofundados sobre o desempenho de rede é crítico tooprovide serviços fiável toocustomers.</span><span class="sxs-lookup"><span data-stu-id="89616-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="89616-105">É, por conseguinte, toodetect crítico condições de falha de rede rapidamente e tomar a condição de falha de Olá de toomitigate as medidas corretivas.</span><span class="sxs-lookup"><span data-stu-id="89616-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="89616-106">A automatização do Azure permite-lhe tooimplement e executar uma tarefa de forma programática através de runbooks.</span><span class="sxs-lookup"><span data-stu-id="89616-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="89616-107">Utilizar a automatização do Azure cria uma receitas perfeita para efetuar a monitorização de rede contínua e proativa e alertas.</span><span class="sxs-lookup"><span data-stu-id="89616-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="89616-108">Cenário</span><span class="sxs-lookup"><span data-stu-id="89616-108">Scenario</span></span>

<span data-ttu-id="89616-109">cenário de Olá no Olá seguinte imagem é uma aplicação de várias camadas, com conectividade no local estabelecida através de um Gateway de VPN e túnel.</span><span class="sxs-lookup"><span data-stu-id="89616-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="89616-110">Garantir Olá que VPN Gateway está a funcionar e em execução são crítico toohello desempenho de aplicações.</span><span class="sxs-lookup"><span data-stu-id="89616-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="89616-111">É criado um runbook com um toocheck de script para o estado da ligação do túnel VPN de Olá, utilizando Olá toocheck de API de resolução de problemas de recursos para o estado de ligação do túnel.</span><span class="sxs-lookup"><span data-stu-id="89616-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="89616-112">Se o estado de Olá não está em bom estado, um acionador de correio eletrónico é enviado tooadministrators.</span><span class="sxs-lookup"><span data-stu-id="89616-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Exemplo de cenário][scenario]

<span data-ttu-id="89616-114">Neste cenário irão:</span><span class="sxs-lookup"><span data-stu-id="89616-114">This scenario will:</span></span>

- <span data-ttu-id="89616-115">Criar Olá de chamar um runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot estado da ligação</span><span class="sxs-lookup"><span data-stu-id="89616-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="89616-116">Ligar um runbook de toohello agenda</span><span class="sxs-lookup"><span data-stu-id="89616-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="89616-117">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="89616-117">Before you begin</span></span>

<span data-ttu-id="89616-118">Antes de começar este cenário, tem de ter Olá os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="89616-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="89616-119">Uma conta de automatização do Azure no Azure.</span><span class="sxs-lookup"><span data-stu-id="89616-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="89616-120">Certifique-se de que conta de automatização Olá tem módulos mais recentes Olá e também tem o módulo de AzureRM.Network Olá.</span><span class="sxs-lookup"><span data-stu-id="89616-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="89616-121">Olá AzureRM.Network módulo está disponível na Galeria de módulo Olá se precisar de tooadd-tooyour conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="89616-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="89616-122">Tem de ter um conjunto de credenciais que configurar na automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="89616-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="89616-123">Saiba mais em [segurança de automatização do Azure](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="89616-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="89616-124">Um servidor de SMTP válido (Office 365, o e-mail no local ou outra) e as credenciais definidas na automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="89616-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="89616-125">Um configurado Gateway de rede Virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="89616-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="89616-126">Uma conta de armazenamento existente com uma toostore Olá existente do contentor nos registos.</span><span class="sxs-lookup"><span data-stu-id="89616-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="89616-127">infraestrutura de Olá representada no Olá anterior a imagem é para fins de ilustração e não são criados com passos de Olá contidos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="89616-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="89616-128">Criar Olá runbook</span><span class="sxs-lookup"><span data-stu-id="89616-128">Create hello runbook</span></span>

<span data-ttu-id="89616-129">exemplo de Olá de tooconfiguring Olá primeiro passo é toocreate Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="89616-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="89616-130">Este exemplo utiliza uma conta executar como.</span><span class="sxs-lookup"><span data-stu-id="89616-130">This example uses a run-as account.</span></span> <span data-ttu-id="89616-131">toolearn sobre contas executar como, visite [autenticar Runbooks com a conta Run As do Azure](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="89616-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="89616-132">Passo 1</span><span class="sxs-lookup"><span data-stu-id="89616-132">Step 1</span></span>

<span data-ttu-id="89616-133">Navegue tooAzure automatização no Olá [portal do Azure](https://portal.azure.com) e clique em **Runbooks**</span><span class="sxs-lookup"><span data-stu-id="89616-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Descrição geral da conta de automatização][1]

### <a name="step-2"></a><span data-ttu-id="89616-135">Passo 2</span><span class="sxs-lookup"><span data-stu-id="89616-135">Step 2</span></span>

<span data-ttu-id="89616-136">Clique em **adicionar um runbook** processo de criação de Olá toostart de Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="89616-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![Painel de runbooks][2]

### <a name="step-3"></a><span data-ttu-id="89616-138">Passo 3</span><span class="sxs-lookup"><span data-stu-id="89616-138">Step 3</span></span>

<span data-ttu-id="89616-139">Em **criação rápida**, clique em **criar um novo runbook** toocreate Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="89616-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![Adicionar um painel do runbook][3]

### <a name="step-4"></a><span data-ttu-id="89616-141">Passo 4</span><span class="sxs-lookup"><span data-stu-id="89616-141">Step 4</span></span>

<span data-ttu-id="89616-142">Neste passo, que lhe damos Olá runbook um nome, no exemplo de Olá é denominado **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="89616-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="89616-143">É importante toogive Olá runbook um nome descritivo e recomendado, atribua um nome que se segue o padrão normas de nomenclatura do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89616-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="89616-144">tipo de runbook Olá para este exemplo é **PowerShell**, hello outras opções são gráfico, fluxo de trabalho do PowerShell e fluxo de trabalho do PowerShell gráfica.</span><span class="sxs-lookup"><span data-stu-id="89616-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![painel do runbook][4]

### <a name="step-5"></a><span data-ttu-id="89616-146">Passo 5</span><span class="sxs-lookup"><span data-stu-id="89616-146">Step 5</span></span>

<span data-ttu-id="89616-147">Neste passo hello runbook for criado, Olá seguinte exemplo de código fornece que todos os Olá código necessário para o exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="89616-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="89616-148">Olá itens no código Olá que contêm \<valor\> necessário toobe substituído com valores de Olá da sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="89616-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="89616-149">Seguinte de Olá de utilização código como clique **guardar**</span><span class="sxs-lookup"><span data-stu-id="89616-149">Use hello following code as click **Save**</span></span>

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a><span data-ttu-id="89616-150">Passo 6</span><span class="sxs-lookup"><span data-stu-id="89616-150">Step 6</span></span>

<span data-ttu-id="89616-151">Depois de Olá runbook é guardado, uma agenda tem de ser ligado tooit tooautomate Olá início Olá runbook.</span><span class="sxs-lookup"><span data-stu-id="89616-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="89616-152">processo de Olá toostart, clique em **agenda**.</span><span class="sxs-lookup"><span data-stu-id="89616-152">toostart hello process, click **Schedule**.</span></span>

![Passo 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="89616-154">Ligar um runbook de toohello agenda</span><span class="sxs-lookup"><span data-stu-id="89616-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="89616-155">Tem de ser criada uma nova agenda.</span><span class="sxs-lookup"><span data-stu-id="89616-155">A new schedule must be created.</span></span> <span data-ttu-id="89616-156">Clique em **ligar um runbook de tooyour agenda**.</span><span class="sxs-lookup"><span data-stu-id="89616-156">Click **Link a schedule tooyour runbook**.</span></span>

![Passo 7][7]

### <a name="step-1"></a><span data-ttu-id="89616-158">Passo 1</span><span class="sxs-lookup"><span data-stu-id="89616-158">Step 1</span></span>

<span data-ttu-id="89616-159">No Olá **agenda** painel, clique em **criar uma nova agenda**</span><span class="sxs-lookup"><span data-stu-id="89616-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![Passo 8][8]

### <a name="step-2"></a><span data-ttu-id="89616-161">Passo 2</span><span class="sxs-lookup"><span data-stu-id="89616-161">Step 2</span></span>

<span data-ttu-id="89616-162">No Olá **nova agenda** preenchimento painel informações de agenda Olá.</span><span class="sxs-lookup"><span data-stu-id="89616-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="89616-163">os valores de Olá que podem ser definidos são no Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="89616-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="89616-164">**Nome** -nome amigável do Olá da agenda de Olá.</span><span class="sxs-lookup"><span data-stu-id="89616-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="89616-165">**Descrição** -uma descrição da agenda de Olá.</span><span class="sxs-lookup"><span data-stu-id="89616-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="89616-166">**Inicia** -este valor é uma combinação de padrões de data, hora e fuso horário que compõem acionadores do Olá tempo Olá agenda.</span><span class="sxs-lookup"><span data-stu-id="89616-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="89616-167">**Periodicidade** -este valor determina Olá agendas repetição.</span><span class="sxs-lookup"><span data-stu-id="89616-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="89616-168">Os valores válidos são **uma vez** ou **periódica**.</span><span class="sxs-lookup"><span data-stu-id="89616-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="89616-169">**Repetir cada** -intervalo de periodicidade Olá da agenda de Olá em horas, dias, semanas ou meses.</span><span class="sxs-lookup"><span data-stu-id="89616-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="89616-170">**Definir expiração** -valor Olá determina se a agenda de Olá deve expirar ou não.</span><span class="sxs-lookup"><span data-stu-id="89616-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="89616-171">Pode ser definido demasiado**Sim** ou **não**.</span><span class="sxs-lookup"><span data-stu-id="89616-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="89616-172">Uma data ou hora válida são toobe fornecido se Sim, é escolhido.</span><span class="sxs-lookup"><span data-stu-id="89616-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="89616-173">Se precisar de toohave um runbook execute mais frequentemente a cada hora, vários agendamentos simultâneos têm de ser criados com intervalos diferentes (ou seja, 15, 30, 45 minutos após a hora de Olá)</span><span class="sxs-lookup"><span data-stu-id="89616-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![Passo 9][9]

### <a name="step-3"></a><span data-ttu-id="89616-175">Passo 3</span><span class="sxs-lookup"><span data-stu-id="89616-175">Step 3</span></span>

<span data-ttu-id="89616-176">Clique em Guardar toosave Olá agenda toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="89616-176">Click Save toosave hello schedule toohello runbook.</span></span>

![Passo 10][10]

## <a name="next-steps"></a><span data-ttu-id="89616-178">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="89616-178">Next steps</span></span>

<span data-ttu-id="89616-179">Agora que tem uma compreensão sobre como toointegrate observador de rede resolução de problemas com a automatização do Azure, saiba como capturas de pacotes de tootrigger alertas de VM, visitando [criar uma captura de pacotes accionadas alerta com o observador de rede de Azure](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="89616-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
