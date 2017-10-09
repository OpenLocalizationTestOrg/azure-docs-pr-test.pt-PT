---
title: "aaaCertificate ativos na automatização do Azure | Microsoft Docs"
description: "Certificados podem ser armazenados em segurança na automatização do Azure para que possam ser acedidos por runbooks ou configurações de DSC tooauthenticate contra do Azure e recursos de terceiros.  Este artigo explica os detalhes de Olá de certificados e como toowork com os mesmos no texto e gráficos de criação."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Ativos de certificado na automatização do Azure

Certificados podem ser armazenados em segurança na automatização do Azure para que possam ser acedidos por runbooks ou configurações de DSC utilizando Olá **Get-AzureRmAutomationRmCertificate** atividade para recursos do Azure Resource Manager. Isto permite-lhe toocreate runbooks e configurações de DSC que utilizam certificados para autenticação ou adiciona-os recursos tooAzure ou de terceiros.

> [!NOTE] 
> Proteger recursos na automatização do Azure incluem as credenciais, certificados, ligações e as variáveis encriptadas. Estes elementos são encriptados e armazenados em Olá da automatização do Azure com uma chave exclusiva que é gerada para cada conta de automatização. Esta chave é encriptada por um certificado principal e armazenada na automatização do Azure. Antes de o armazenamento de um recurso seguro, chave de Olá da conta de automatização de Olá é desencriptada utilizando o certificado principal Olá e, em seguida, utilizado asset de Olá tooencrypt.
> 

## <a name="windows-powershell-cmdlets"></a>Cmdlets do Windows PowerShell

cmdlets de Olá no Olá a tabela seguinte são utilizado toocreate e gerir recursos de certificado de automatização com o Windows PowerShell. Estes são enviados como parte da Olá [módulo Azure PowerShell](../powershell-install-configure.md) que está disponível para utilização nos runbooks de automatização e configurações de DSC.

|Cmdlets|Descrição|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Obtém informações sobre toouse um certificado de um runbook ou a configuração de DSC. Apenas pode obter o certificado de Olá propriamente dito da atividade de Get-AutomationCertificate.|
|[Novo AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Cria um novo certificado para a automatização do Azure.|
[Remover AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Remove um certificado da automatização do Azure.|Cria um novo certificado para a automatização do Azure.
|[Conjunto AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Define as propriedades de Olá para um certificado existente, incluindo carregar o ficheiro de certificado Olá e a palavra-passe Olá de definição para um ficheiro. pfx.|
|[AzureCertificate adicionar](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Carrega um serviço de certificado para Olá especificado serviço em nuvem.|


## <a name="creating-a-new-certificate"></a>Criar um novo certificado

Quando cria um novo certificado, carregue uma tooAzure de ficheiro. cer ou. pfx automatização. Se marcar o certificado de Olá como exportável, pode transferi-la fora do arquivo de certificados do Olá da automatização do Azure. Se não é exportável, em seguida, pode apenas ser utilizado para a assinatura no runbook Olá ou a configuração de DSC.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate um novo certificado com Olá portal do Azure

1. Da sua conta de automatização, clique em Olá **ativos** mosaico tooopen Olá **ativos** painel.
1. Clique em Olá **certificados** mosaico tooopen Olá **certificados** painel.
1. Clique em **adicionar um certificado** , Olá parte superior do painel de Olá.
2. Escreva um nome para o certificado de Olá Olá **nome** caixa.
2. Clique em **selecione um ficheiro** em **carregar um ficheiro de certificado** toobrowse para um ficheiro. cer ou. pfx.  Se selecionar um ficheiro. pfx, especifique uma palavra-passe e se deve ter permissão toobe exportado.
1. Clique em **criar** toosave Olá novo certificado elemento.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate um novo certificado com o Windows PowerShell

Olá exemplo seguinte demonstra como toocreate uma automatização novo certificado e marcá-la exportável. Esta ação importa um ficheiro. pfx existente.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Utilizar um certificado

Tem de utilizar Olá **Get-AutomationCertificate** atividade toouse um certificado. Não é possível utilizar Olá [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet, uma vez que devolve informações sobre o recurso de certificado Olá, mas não o certificado de Olá propriamente dito.

### <a name="textual-runbook-sample"></a>Exemplo de textual runbook

Olá, código de exemplo a seguir mostra como serviço num runbook em nuvem tooadd tooa um certificado. Neste exemplo, palavra-passe de Olá é obtido a partir de uma variável de automatização encriptados.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Exemplo de um runbook gráfico

Adicionar um **Get-AutomationCertificate** tooa runbook gráfico clicando no certificado de Olá no painel de biblioteca de Olá do editor gráfico Olá e selecionando **adicionar toocanvas**.

![Adicionar tela toohello de certificado](media/automation-certificates/automation-certificate-add-to-canvas.png)

Olá imagem seguinte mostra um exemplo de utilização de um certificado de um runbook gráfico.  Este é Olá mesmo exemplo mostrado acima para adicionar um serviço de nuvem de tooa de certificado a partir de um runbook textual.

![Criação de gráficos de exemplo ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Passos seguintes

- toolearn mais informações sobre como trabalhar com fluxo lógico de ligações toocontrol Olá de atividades do runbook é concebido tooperform, consulte [nas hiperligações na criação de gráficos](automation-graphical-authoring-intro.md#links-and-workflow). 
