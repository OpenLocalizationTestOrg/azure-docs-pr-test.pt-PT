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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Monitorizar os gateways de VPN com a resolução de problemas do observador de rede

Obter conhecimentos aprofundados sobre o desempenho de rede é crítico tooprovide serviços fiável toocustomers. É, por conseguinte, toodetect crítico condições de falha de rede rapidamente e tomar a condição de falha de Olá de toomitigate as medidas corretivas. A automatização do Azure permite-lhe tooimplement e executar uma tarefa de forma programática através de runbooks. Utilizar a automatização do Azure cria uma receitas perfeita para efetuar a monitorização de rede contínua e proativa e alertas.

## <a name="scenario"></a>Cenário

cenário de Olá no Olá seguinte imagem é uma aplicação de várias camadas, com conectividade no local estabelecida através de um Gateway de VPN e túnel. Garantir Olá que VPN Gateway está a funcionar e em execução são crítico toohello desempenho de aplicações.

É criado um runbook com um toocheck de script para o estado da ligação do túnel VPN de Olá, utilizando Olá toocheck de API de resolução de problemas de recursos para o estado de ligação do túnel. Se o estado de Olá não está em bom estado, um acionador de correio eletrónico é enviado tooadministrators.

![Exemplo de cenário][scenario]

Neste cenário irão:

- Criar Olá de chamar um runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot estado da ligação
- Ligar um runbook de toohello agenda

## <a name="before-you-begin"></a>Antes de começar

Antes de começar este cenário, tem de ter Olá os seguintes pré-requisitos:

- Uma conta de automatização do Azure no Azure. Certifique-se de que conta de automatização Olá tem módulos mais recentes Olá e também tem o módulo de AzureRM.Network Olá. Olá AzureRM.Network módulo está disponível na Galeria de módulo Olá se precisar de tooadd-tooyour conta de automatização.
- Tem de ter um conjunto de credenciais que configurar na automatização do Azure. Saiba mais em [segurança de automatização do Azure](../automation/automation-security-overview.md)
- Um servidor de SMTP válido (Office 365, o e-mail no local ou outra) e as credenciais definidas na automatização do Azure
- Um configurado Gateway de rede Virtual no Azure.
- Uma conta de armazenamento existente com uma toostore Olá existente do contentor nos registos.

> [!NOTE]
> infraestrutura de Olá representada no Olá anterior a imagem é para fins de ilustração e não são criados com passos de Olá contidos neste artigo.

### <a name="create-hello-runbook"></a>Criar Olá runbook

exemplo de Olá de tooconfiguring Olá primeiro passo é toocreate Olá runbook. Este exemplo utiliza uma conta executar como. toolearn sobre contas executar como, visite [autenticar Runbooks com a conta Run As do Azure](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>Passo 1

Navegue tooAzure automatização no Olá [portal do Azure](https://portal.azure.com) e clique em **Runbooks**

![Descrição geral da conta de automatização][1]

### <a name="step-2"></a>Passo 2

Clique em **adicionar um runbook** processo de criação de Olá toostart de Olá runbook.

![Painel de runbooks][2]

### <a name="step-3"></a>Passo 3

Em **criação rápida**, clique em **criar um novo runbook** toocreate Olá runbook.

![Adicionar um painel do runbook][3]

### <a name="step-4"></a>Passo 4

Neste passo, que lhe damos Olá runbook um nome, no exemplo de Olá é denominado **Get-VPNGatewayStatus**. É importante toogive Olá runbook um nome descritivo e recomendado, atribua um nome que se segue o padrão normas de nomenclatura do PowerShell. tipo de runbook Olá para este exemplo é **PowerShell**, hello outras opções são gráfico, fluxo de trabalho do PowerShell e fluxo de trabalho do PowerShell gráfica.

![painel do runbook][4]

### <a name="step-5"></a>Passo 5

Neste passo hello runbook for criado, Olá seguinte exemplo de código fornece que todos os Olá código necessário para o exemplo de Olá. Olá itens no código Olá que contêm \<valor\> necessário toobe substituído com valores de Olá da sua subscrição.

Seguinte de Olá de utilização código como clique **guardar**

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

### <a name="step-6"></a>Passo 6

Depois de Olá runbook é guardado, uma agenda tem de ser ligado tooit tooautomate Olá início Olá runbook. processo de Olá toostart, clique em **agenda**.

![Passo 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>Ligar um runbook de toohello agenda

Tem de ser criada uma nova agenda. Clique em **ligar um runbook de tooyour agenda**.

![Passo 7][7]

### <a name="step-1"></a>Passo 1

No Olá **agenda** painel, clique em **criar uma nova agenda**

![Passo 8][8]

### <a name="step-2"></a>Passo 2

No Olá **nova agenda** preenchimento painel informações de agenda Olá. os valores de Olá que podem ser definidos são no Olá lista a seguir:

- **Nome** -nome amigável do Olá da agenda de Olá.
- **Descrição** -uma descrição da agenda de Olá.
- **Inicia** -este valor é uma combinação de padrões de data, hora e fuso horário que compõem acionadores do Olá tempo Olá agenda.
- **Periodicidade** -este valor determina Olá agendas repetição.  Os valores válidos são **uma vez** ou **periódica**.
- **Repetir cada** -intervalo de periodicidade Olá da agenda de Olá em horas, dias, semanas ou meses.
- **Definir expiração** -valor Olá determina se a agenda de Olá deve expirar ou não. Pode ser definido demasiado**Sim** ou **não**. Uma data ou hora válida são toobe fornecido se Sim, é escolhido.

> [!NOTE]
> Se precisar de toohave um runbook execute mais frequentemente a cada hora, vários agendamentos simultâneos têm de ser criados com intervalos diferentes (ou seja, 15, 30, 45 minutos após a hora de Olá)

![Passo 9][9]

### <a name="step-3"></a>Passo 3

Clique em Guardar toosave Olá agenda toohello runbook.

![Passo 10][10]

## <a name="next-steps"></a>Passos seguintes

Agora que tem uma compreensão sobre como toointegrate observador de rede resolução de problemas com a automatização do Azure, saiba como capturas de pacotes de tootrigger alertas de VM, visitando [criar uma captura de pacotes accionadas alerta com o observador de rede de Azure](network-watcher-alert-triggered-packet-capture.md).

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
