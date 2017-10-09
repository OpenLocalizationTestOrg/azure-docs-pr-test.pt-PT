---
title: aaaMonitor e gerir tarefas do Stream Analytics com o PowerShell | Microsoft Docs
description: Saiba como toouse Azure PowerShell e cmdlets toomonitor e gerir tarefas do Stream Analytics.
keywords: o Azure powershell, o cmdlets do powershell do azure, o comando do powershell, scripts do powershell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Monitorizar e gerir tarefas do Stream Analytics com cmdlets do PowerShell do Azure
Saiba como toomonitor e gerir os recursos de Stream Analytics com cmdlets do Azure PowerShell e scripts do powershell que executar tarefas do Stream Analytics básicas.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Pré-requisitos para executar cmdlets do Azure PowerShell para o Stream Analytics
* Crie um grupo de recursos do Azure na sua subscrição. Olá segue-se um exemplo de script do PowerShell do Azure. Para obter informações do Azure PowerShell, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview);  

O Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

O Azure PowerShell 1.0:  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Tarefas do Stream Analytics criadas através de programação não dispõe de monitorização ativada por predefinição.  Pode ativar manualmente a monitorização em Olá Portal do Azure, aceda a página de Monitor da tarefa toohello e clicar no botão Ativar de Olá ou pode fazê-lo através de programação, seguindo os passos de Olá localizados em [Azure Stream Analytics - sequência de Monitor Análise de tarefas X509securitytokenparameters](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Cmdlets do PowerShell do Azure Stream Analytics
Olá, os seguintes cmdlets do Azure PowerShell pode ser utilizado toomonitor e gerir tarefas do Azure Stream Analytics. Tenha em atenção que o Azure PowerShell tem versões diferentes. 
**Nos exemplos de Olá é primeiro comando de Olá listados para o Azure PowerShell 0.9.8, o segundo comando de Olá é para o Azure PowerShell 1.0.** comandos de Olá Azure PowerShell 1.0 terão sempre no comando Olá "AzureRM".

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Apresenta uma lista de todas as tarefas do Stream Analytics definidas num Olá subscrição do Azure ou o grupo de recursos especificado ou obtém as informações da tarefa sobre uma tarefa específica dentro de um grupo de recursos.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob

Este comando PowerShell devolve informações sobre todas as tarefas do Stream Analytics Olá Olá subscrição do Azure.

**Exemplo 2**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Este comando PowerShell devolve informações sobre todas as tarefas do Stream Analytics Olá no grupo de recursos de Olá StreamAnalytics-predefinição-Central-US.

**Exemplo 3**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Este comando PowerShell devolve informações sobre a tarefa de Stream Analytics Olá StreamingJob no grupo de recursos de Olá StreamAnalytics-predefinição-Central-US.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Apresenta uma lista de todas as entradas de Olá que são definidas numa tarefa do Stream Analytics especificada ou obtém informações sobre uma entrada específica.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Este comando PowerShell devolve informações sobre todas as entradas de Olá definidos na tarefa de Olá StreamingJob.

**Exemplo 2**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Este comando PowerShell devolve informações sobre a entrada de Olá denominada EntryStream definido na tarefa de Olá StreamingJob.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Apresenta uma lista de todas as saídas de Olá que são definidas numa tarefa do Stream Analytics especificada ou obtém informações sobre uma saída específica.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Este comando PowerShell devolve informações sobre as saídas de Olá definidos na tarefa de Olá StreamingJob.

**Exemplo 2**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Este comando PowerShell devolve informações sobre a saída de Olá com o nome de saída definida na tarefa de Olá StreamingJob.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Obtém informações sobre a quota de Olá de transmissão em fluxo unidades numa região especificada.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Este comando PowerShell devolve informações sobre a quota de Olá e a utilização de unidades de transmissão em fluxo na região de EUA Central Olá.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Obtém informações sobre uma transformação específica definida numa tarefa de Stream Analytics.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

O Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Este comando PowerShell devolve informações sobre a transformação Olá chamada StreamingJob na tarefa de Olá StreamingJob.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>Novo AzureStreamAnalyticsInput | Novo AzureRMStreamAnalyticsInput
Cria uma nova entrada dentro de uma tarefa de Stream Analytics ou atualiza uma entrada existente especificada.

Olá nome da entrada de Olá pode ser especificado no ficheiro. JSON Olá ou na linha de comandos Olá. Se ambos forem especificadas, nome de Olá na linha de comandos Olá tem Olá igual Olá uma no ficheiro de Olá.

Se especificar uma entrada que já existe e se não especificar hello – parâmetro Force, Olá cmdlet irá perguntar se pretende ou não tooreplace Olá entrada existente.

Se especificar Olá – parâmetro Force e especifique existente introduzir o nome, será substituída Olá entrada sem confirmação.

Para obter informações detalhadas sobre a estrutura de ficheiros JSON Olá e o conteúdo, consulte toohello [entrada criar (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] secção Olá [API de REST de gestão do Stream Analytics Biblioteca de referência][stream.analytics.rest.api.reference].

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Este comando PowerShell cria uma nova entrada de ficheiro Olá Input. Se já está definida uma entrada existente com o nome de Olá especificado no ficheiro de definição de entrada de Olá, Olá cmdlet irá perguntar se pretende ou não tooreplace-lo.

**Exemplo 2**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Este comando PowerShell cria uma nova entrada na tarefa de Olá chamada EntryStream. Se uma entrada existente com este nome já está definida, o cmdlet Olá irá perguntar se pretende ou não tooreplace-lo.

**Exemplo 3**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Este comando PowerShell substitui a definição de Olá Olá existente de origens de entrada chamada EntryStream com a definição do ficheiro de Olá Olá.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>Novo AzureStreamAnalyticsJob | Novo AzureRMStreamAnalyticsJob
Cria uma nova tarefa de Stream Analytics no Microsoft Azure ou de atualizações de definição de Olá de uma tarefa especificada existente.

nome de Olá da tarefa de Olá pode ser especificado no ficheiro. JSON Olá ou na linha de comandos Olá. Se ambos forem especificadas, nome de Olá na linha de comandos Olá tem Olá igual Olá uma no ficheiro de Olá.

Se especificar um nome de tarefa já existe e se não especificar hello – parâmetro Force, Olá cmdlet irá perguntar se pretende ou não tooreplace Olá tarefa existente.

Se especificar Olá – parâmetro Force e especifique um nome de tarefa existente, definição de tarefa Olá será substituída sem confirmação.

Para obter informações detalhadas sobre a estrutura de ficheiros JSON Olá e o conteúdo, consulte toohello [criar tarefa do Stream Analytics] [ msdn-rest-api-create-stream-analytics-job] secção Olá [referência de API do REST de gestão do Stream Analytics Biblioteca][stream.analytics.rest.api.reference].

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Este comando PowerShell cria uma nova tarefa da definição de Olá no JobDefinition.json. Se uma tarefa existente com o nome de Olá especificado no ficheiro de definição de tarefa Olá já está definida, o cmdlet Olá irá perguntar se pretende ou não tooreplace-lo.

**Exemplo 2**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Este comando PowerShell substitui a definição de tarefa Olá para StreamingJob.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>Novo AzureStreamAnalyticsOutput | Novo AzureRMStreamAnalyticsOutput
Cria uma saída de novo dentro de uma tarefa de Stream Analytics ou atualiza uma saída existente.  

nome de Olá da saída de Olá pode ser especificado no ficheiro. JSON Olá ou na linha de comandos Olá. Se ambos forem especificadas, nome de Olá na linha de comandos Olá tem Olá igual Olá uma no ficheiro de Olá.

Se especificar um resultado que já existe e se não especificar hello – parâmetro Force, Olá cmdlet irá pedir-se ou não tooreplace Olá saída existente.

Se especificar Olá – parâmetro Force e especifique o nome de saída de um existente, saída Olá será substituída sem confirmação.

Para obter informações detalhadas sobre a estrutura de ficheiros JSON Olá e o conteúdo, consulte toohello [saída criar (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] secção Olá [API de REST de gestão do Stream Analytics Biblioteca de referência][stream.analytics.rest.api.reference].

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Este comando PowerShell cria uma nova saída chamada de "saída" na tarefa de Olá StreamingJob. Se uma saída existente com este nome já está definida, o cmdlet Olá irá perguntar se pretende ou não tooreplace-lo.

**Exemplo 2**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Este comando PowerShell substitui a definição de Olá de "saída" na tarefa de Olá StreamingJob.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>Novo AzureStreamAnalyticsTransformation | Novo AzureRMStreamAnalyticsTransformation
Cria uma transformação de novo dentro de uma tarefa de Stream Analytics ou atualiza a transformação existente Olá.

nome de Olá da transformação Olá pode ser especificado no ficheiro. JSON Olá ou na linha de comandos Olá. Se ambos forem especificadas, nome de Olá na linha de comandos Olá tem Olá igual Olá uma no ficheiro de Olá.

Se especificar uma transformação que já existe e se não especificar hello – parâmetro Force, Olá cmdlet irá pedir-se ou não tooreplace Olá transformação existente.

Se especificar Olá – parâmetro Force e especifique um nome de transformação existente será substituída transformação Olá sem confirmação.

Para obter informações detalhadas sobre a estrutura de ficheiros JSON Olá e o conteúdo, consulte toohello [criar transformação (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] secção Olá [Stream Analytics Management Biblioteca de referência de API de REST][stream.analytics.rest.api.reference].

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Este comando PowerShell cria uma nova transformação chamada StreamingJobTransform na tarefa de Olá StreamingJob. Se uma transformação existente já está definida com este nome, o cmdlet Olá irá perguntar se pretende ou não tooreplace-lo.

**Exemplo 2**

O Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

O Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 Este comando PowerShell substitui a definição de Olá de StreamingJobTransform na tarefa de Olá StreamingJob.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remover AzureStreamAnalyticsInput | Remover AzureRMStreamAnalyticsInput
No modo assíncrono elimina uma entrada específica de uma tarefa de Stream Analytics no Microsoft Azure.  
Se especificar hello – parâmetro Force, Olá entrada será eliminado sem confirmação.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

O Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Este comando PowerShell remove Olá EventStream entrada na tarefa de Olá StreamingJob.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remover AzureStreamAnalyticsJob | Remover AzureRMStreamAnalyticsJob
No modo assíncrono elimina uma tarefa de Stream Analytics específica no Microsoft Azure.  
Se especificar hello – parâmetro Force, Olá tarefa irá ser eliminado sem confirmação.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

O Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Este comando PowerShell remove tarefa Olá StreamingJob.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remover AzureStreamAnalyticsOutput | Remover AzureRMStreamAnalyticsOutput
No modo assíncrono elimina uma saída específica de uma tarefa de Stream Analytics no Microsoft Azure.  
Se especificar hello – parâmetro Force, Olá resultado será eliminado sem confirmação.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

O Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Este Olá de remove de comando do PowerShell de saída do resultado na tarefa de Olá StreamingJob.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Início AzureStreamAnalyticsJob | Início AzureRMStreamAnalyticsJob
No modo assíncrono implementa e inicia uma tarefa de Stream Analytics no Microsoft Azure.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

O Azure PowerShell 1.0:  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Este comando PowerShell inicia Olá tarefa StreamingJob com uma hora de início de saída personalizado Definir tooDecember 12, 2012, 12:12:12 UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
No modo assíncrono para uma tarefa de Stream Analytics sejam executadas no Microsoft Azure e anula a alocação recursos que foram que estavam a ser utilizados. Olá definição de tarefa e metadados permanecerá disponíveis na sua subscrição através de Olá portal do Azure e APIs, de gestão de forma a que hello tarefa pode ser editada e reiniciada. Não será cobrada para uma tarefa no estado de Olá parado.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

O Azure PowerShell 1.0:  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Este comando do PowerShell para a tarefa de Olá StreamingJob.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Teste AzureStreamAnalyticsInput | Teste AzureRMStreamAnalyticsInput
Capacidade de Olá testes do Stream Analytics tooconnect tooa especificada entrada.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

O Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Este estado de ligação de Olá de testes de comando do PowerShell da Olá EntryStream no StreamingJob de entrada.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Teste AzureStreamAnalyticsOutput | Teste AzureRMStreamAnalyticsOutput
Capacidade de Olá testes do Stream Analytics tooconnect tooa especificado saída.

**Exemplo 1**

O Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

O Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Este estado de ligação de Olá de testes de comando do PowerShell da Olá saída no StreamingJob de saída.  

## <a name="get-support"></a>Obter suporte
Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics). 

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

