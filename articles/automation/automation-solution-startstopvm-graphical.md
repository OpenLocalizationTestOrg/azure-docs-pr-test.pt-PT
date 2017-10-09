---
title: "aaaStarting e máquinas virtuais de paragem - Graph | Microsoft Docs"
description: "Versão de fluxo de trabalho do PowerShell do cenário de automatização do Azure, incluindo runbooks toostart e parar as máquinas virtuais clássicas."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Cenário de automatização do Azure – iniciar e parar máquinas virtuais
Neste cenário de automatização do Azure inclui runbooks toostart e parar as máquinas virtuais clássicas.  Pode utilizar este cenário para Olá seguinte:  

* Utilize runbooks Olá sem modificação no seu próprio ambiente.
* Modificar Olá runbooks tooperform personalizada de funcionalidade.  
* Chame Olá runbooks a partir de outro runbook como parte de uma solução global.
* Utilize runbooks Olá como tutoriais toolearn runbook conceitos de criação.

> [!div class="op_single_selector"]
> * [Gráficos](automation-solution-startstopvm-graphical.md)
> * [Fluxo de Trabalho do PowerShell](automation-solution-startstopvm-psworkflow.md)
>
>

Esta é a versão de um runbook gráfico Olá deste cenário. Está também disponível utilizando [runbooks do fluxo de trabalho do PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Ao obter cenário de Olá
Este cenário é composta por dois dois runbooks gráficos que pode transferir da Olá seguintes ligações.  Consulte Olá [versão de fluxo de trabalho do PowerShell](automation-solution-startstopvm-psworkflow.md) deste cenário para ligações toohello runbooks do fluxo de trabalho do PowerShell.

| Runbook | Ligação | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Iniciar o Runbook de gráfico de VMS clássicas do Azure](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Gráfico |Inicia todas as máquinas virtuais clássicas uma subscrição do Azure ou todas as máquinas virtuais com um nome de serviço específica. |
| StopAzureClassicVM |[Parar um Runbook gráfico VMS clássicas do Azure](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Gráfico |Interrompe a todas as máquinas virtuais de uma conta de automatização ou todas as máquinas virtuais com um nome de serviço específica. |

## <a name="installing-and-configuring-hello-scenario"></a>Instalar e configurar o cenário de Olá
### <a name="1-install-hello-runbooks"></a>1. Instalar Olá runbooks
Depois de transferir runbooks Olá, pode importá-los utilizando o procedimento Olá [procedimentos de runbook gráfico](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Requisitos e revisão Olá descrição
Olá runbooks incluem uma atividade chamada **Leia-Me** que inclui uma descrição e os recursos necessários.  Pode ver estas informações, selecionando Olá **Leia-Me** atividade e, em seguida, Olá **Script de fluxo de trabalho** parâmetro.  Também pode obter Olá mesmas informações do artigo.

### <a name="3-configure-assets"></a>3. Configurar recursos
Olá runbooks necessitam Olá os seguintes recursos de que tem de criar e preencher com os valores adequados.  os nomes de Olá são predefinido.  Pode utilizar recursos com nomes diferentes se especificar esses nomes de no Olá [parâmetros de entrada](#using-the-runbooks) quando iniciar o runbook Olá.

| Tipo de recurso | Nome predefinido | Descrição |
|:--- |:--- |:--- |:--- |
| [Credencial](automation-credentials.md) |AzureCredential |Contém as credenciais para uma conta que tem autoridade toostart e pare a máquinas virtuais no Olá subscrição do Azure. |
| [Variável](automation-variables.md) |AzureSubscriptionId |Contém o ID de subscrição de Olá da sua subscrição do Azure. |

## <a name="using-hello-scenario"></a>Utilizando o cenário de Olá
### <a name="parameters"></a>Parâmetros
Olá runbooks cada ter Olá seguinte [parâmetros de entrada](automation-starting-a-runbook.md#runbook-parameters).  Tem de fornecer valores para todos os parâmetros obrigatórios e opcionalmente, pode fornecer valores para os outros parâmetros dependendo dos seus requisitos.

| Parâmetro | Tipo | Obrigatório | Descrição |
|:--- |:--- |:--- |:--- |
| ServiceName |Cadeia |Não |Se não for fornecido um valor, todas as máquinas virtuais com esse nome de serviço são iniciadas ou paradas.  Se não for fornecido nenhum valor, todas as máquinas virtuais clássicas Olá subscrição do Azure são iniciadas ou paradas. |
| AzureSubscriptionIdAssetName |Cadeia |Não |Contém o nome de Olá de Olá [recurso de variável](#installing-and-configuring-the-scenario) que contém o ID de subscrição de Olá da sua subscrição do Azure.  Se não especificar um valor, *AzureSubscriptionId* é utilizado. |
| AzureCredentialAssetName |Cadeia |Não |Contém o nome de Olá de Olá [recurso de credencial](#installing-and-configuring-the-scenario) que contém as credenciais Olá Olá toouse de runbook.  Se não especificar um valor, *AzureCredential* é utilizado. |

### <a name="starting-hello-runbooks"></a>Iniciar runbooks Olá
Pode utilizar qualquer um dos métodos de Olá no [iniciar um runbook na automatização do Azure](automation-starting-a-runbook.md) toostart qualquer um dos runbooks Olá neste artigo.

os seguintes comandos de exemplo de Olá utiliza o Windows PowerShell toorun **StartAzureClassicVM** toostart todas as máquinas virtuais com o nome do serviço Olá *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Saída
Olá runbooks serão [uma mensagem de saída](automation-runbook-output-and-messages.md) para cada máquina virtual que indica se pretende ou não Olá início ou paragem instrução foi submetida com êxito.  Pode procurar uma cadeia específica no resultado de Olá Olá saída toodetermine para cada runbook.  cadeias de saída possíveis Olá estão listadas na Olá a tabela seguinte.

| Runbook | Condição | Mensagem |
|:--- |:--- |:--- |
| StartAzureClassicVM |Máquina virtual já está em execução |MyVM já está em execução |
| StartAzureClassicVM |Pedido de início para a máquina virtual foi submetido com êxito |MyVM foi iniciado |
| StartAzureClassicVM |Falha no pedido de início para a máquina virtual |Toostart MyVM falhou |
| StopAzureClassicVM |Máquina virtual já está em execução |MyVM já está parado |
| StopAzureClassicVM |Pedido de início para a máquina virtual foi submetido com êxito |MyVM foi iniciado |
| StopAzureClassicVM |Falha no pedido de início para a máquina virtual |Toostart MyVM falhou |

Segue-se uma imagem da utilização de Olá **StartAzureClassicVM** como um [runbook subordinado](automation-child-runbooks.md) de um runbook de gráfico de exemplo.  Esta opção utiliza ligações condicionais Olá no Olá a tabela seguinte.

| Ligação | Critérios |
|:--- |:--- |
| Ligação de êxito |$ActivityOutput ['StartAzureClassicVM']-como "\* foi iniciado" |
| Ligação de erro |$ActivityOutput ['StartAzureClassicVM']-notlike "\* foi iniciado" |

![Exemplo de runbook subordinado](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Divisão de detalhado
Segue-se uma divisão de detalhado de runbooks Olá neste cenário.  Pode utilizar estas informações tooeither personalizar Olá runbooks ou toolearn apenas dos mesmos para os seus próprios cenários de automatização de criação.

### <a name="authentication"></a>Autenticação
![Autenticação](media/automation-solution-startstopvm/graphical-authentication.png)

runbook Olá começa com Olá tooset de atividades [credenciais](automation-credentials.md) e subscrição do Azure que será utilizada para o resto Olá Olá runbook.

Olá primeiro duas atividades, **obter Id de subscrição** e **obter credenciais do Azure**, obter Olá [ativos](#installing-the-runbook) que são utilizadas pelo Olá junto duas atividades.  Essas atividades diretamente especificar ativos Olá, mas têm nomes de elemento Olá.  Uma vez que vamos são permitidos Olá utilizador toospecify esses nomes na Olá [parâmetros de entrada](#using-the-runbooks), precisamos de ativos de Olá estas atividades tooretrieve com um nome especificado por um parâmetro de entrada.

**Adicionar-AzureAccount** conjuntos Olá credenciais que serão utilizadas para o resto Olá Olá runbook.  recurso de credencial de Olá que obtém a partir do **obter credenciais do Azure** tem de ter acesso toostart e pare a máquinas virtuais no Olá subscrição do Azure.  Olá subscrição que é utilizada está selecionada por **Select-AzureSubscription** que utiliza o Id de subscrição de Olá de **obter Id de subscrição**.

### <a name="get-virtual-machines"></a>Obter máquinas virtuais
![Obter VMs](media/automation-solution-startstopvm/graphical-getvms.png)

runbook Olá precisa toodetermine que máquinas virtuais que irá funcionar com e se estão já foi iniciados ou parados (consoante o runbook Olá).   Uma das duas atividades irá obter Olá VMs.  **Obter VMs no serviço** será executado se hello *ServiceName* parâmetro de entrada do runbook Olá contém um valor.  **Obter todas as VMs** será executado se hello *ServiceName* parâmetro de entrada do runbook Olá não contém um valor.  Esta lógica é efetuada por ligações condicionais Olá anterior a cada atividade.

Ambas as atividades utilizam Olá **Get-AzureVM** cmdlet.  **Obter todas as VMs** utiliza Olá **ListAllVMs** tooreturn de conjunto de parâmetros, todas as máquinas virtuais.  **Obter VMs no serviço** utiliza Olá **GetVMByServiceAndVMName** parâmetro definido e fornece Olá **ServiceName** parâmetro de entrada para Olá **ServiceName**parâmetro.  

### <a name="merge-vms"></a>VMs de intercalação
![VMs de intercalação](media/automation-solution-startstopvm/graphical-mergevms.png)

Olá **intercalar VMs** atividade é necessário tooprovide entrada demasiado**Start-AzureVM** que precisa de nome de Olá e nome do serviço de Olá toostart de VM.  Que entrada provir de um **obter todas as VMs** ou **obter VMs no serviço**, mas **Start-AzureVM** só é possível especificar uma atividade de entrada.   

cenário de Olá é toocreate **intercalar VMs** que é executada Olá **Write-Output** cmdlet.  Olá **InputObject** parâmetro para este cmdlet é uma expressão do PowerShell que combina entrada Olá das atividades de Olá dois anterior.  Apenas uma dessas atividades serão executados, apenas um conjunto de saída é esperado.  **Start-AzureVM** pode utilizar essa saída dos respetivos parâmetros de entrada.

### <a name="startstop-virtual-machines"></a>Iniciar/Parar máquinas virtuais
![VMs de início](media/automation-solution-startstopvm/graphical-startvm.png) ![Parar de VMs](media/automation-solution-startstopvm/graphical-stopvm.png)

Dependendo do runbook Olá, atividades seguintes Olá tentativa toostart ou deixar de utilizar de runbook Olá **Start-AzureVM** ou **Stop-AzureVM**.  Uma vez que a atividade de Olá é precedida por uma ligação de pipeline, irá executar uma vez para cada objeto devolvido do **intercalar VMs**.  Olá ligação é condicional para que a atividade de Olá só será executado se hello *RunningState* Olá máquina virtual é *parado* para **Start-AzureVM** e  *Iniciado* para **Stop-AzureVM**. Se esta condição não for cumprida, em seguida, **notificar já foi iniciado** ou **já notificar parado** é executar toosend uma mensagem utilizando **Write-Output**.

### <a name="send-output"></a>Enviar o resultado
![Notificar VMs de início](media/automation-solution-startstopvm/graphical-notifystart.png) ![Notificar VMs de paragem](media/automation-solution-startstopvm/graphical-notifystop.png)

Olá passo final Olá runbook é toosend saída Olá se início ou pedido de paragem para cada máquina virtual foi submetido com êxito. Há um separado **Write-Output** atividade para cada um, e é determinar que um toorun com ligações condicionais.  **Notificar VM Started** ou **notificar VM parada** será executado se *OperationStatus* é *com êxito*.  Se *OperationStatus* é qualquer outro valor, em seguida, **notificar falha tooStart** ou **notificar falha tooStop** é executado.

## <a name="next-steps"></a>Passos seguintes
* [Gráfico de criação na automatização do Azure](automation-graphical-authoring-intro.md)
* [Runbooks subordinados na automatização do Azure](automation-child-runbooks.md)
* [Resultados de Runbook e mensagens na automatização do Azure](automation-runbook-output-and-messages.md)
