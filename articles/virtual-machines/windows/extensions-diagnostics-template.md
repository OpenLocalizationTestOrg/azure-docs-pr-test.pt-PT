---
title: "aaaAdd monitorização & diagnóstico tooan máquina virtual do Azure | Microsoft Docs"
description: "Utilize um toocreate de modelo de Gestor de recursos do Azure nova máquina virtual do Windows com a extensão de diagnóstico do Azure."
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Utilizar a monitorização e diagnóstico com modelos de VM do Windows e o Azure Resource Manager
Olá extensão de diagnóstico do Azure fornece a monitorização de Olá e as capacidades de diagnóstico do Windows baseado em máquina virtual do Azure. Pode ativar estas capacidades na máquina virtual de Olá, incluindo a extensão de Olá como parte do modelo do Olá do azure resource manager. Consulte [criação de modelos de Gestor de recursos do Azure com extensões de VM](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) para obter mais informações sobre incluindo qualquer extensão como parte de um modelo de máquina virtual. Este artigo descreve como adicionar o modelo de máquina virtual de windows extensão tooa Olá diagnósticos do Azure.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Adicionar definição de recurso VM extensão toohello Olá diagnósticos do Azure
extensão de diagnóstico de Olá tooenable na máquina Virtual do Windows tem de extensão de Olá tooadd como um recurso VM no Olá modelo do Resource manager.

Para um Gestor de recursos simples baseada em Máquina Virtual adicionar Olá extensão configuração toohello *recursos* matriz para Olá Máquina Virtual: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Outra convenção comum é adicionar configuração de extensão de Olá Olá nó raiz da recursos do modelo de Olá em vez de define sob o nó de recursos da máquina virtual Olá. Com esta abordagem tem tooexplicitly especifique uma relação hierárquica entre a extensão de Olá e a máquina virtual de Olá com Olá *nome* e *tipo* valores. Por exemplo: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

extensão Olá sempre está associado a máquina virtual de Olá, pode ser diretamente defini-lo diretamente no nó de recursos da máquina virtual Olá ou defini-lo ao nível da base de Olá e utilizar tooassociate de convenção de nomenclatura hierárquica de Olá com Olá virtual máquina.

Extensões de Olá de conjuntos de dimensionamento de Máquina Virtual de configuração é especificada no Olá *extensionProfile* propriedade Olá *VirtualMachineProfile*.

Olá *publicador* propriedade com o valor Olá **Microsoft.Azure.Diagnostics** e Olá *tipo* propriedade com o valor Olá **IaaSDiagnostics** identificar exclusivamente a extensão de diagnóstico do Azure Olá.

Olá, valor de Olá *nome* propriedade pode ser utilizado toorefer toohello extensão no grupo de recursos de Olá. Defini-la especificamente demasiado**Microsoft.Insights.VMDiagnosticsSettings** irá ativá-lo toobe facilmente identificado por Olá garantir portal do Azure que Olá monitorização gráficos são apresentados corretamente Olá portal do Azure.

Olá *typeHandlerVersion* Especifica Olá versão da extensão de Olá que gostaria de toouse. Definição *autoUpgradeMinorVersion* secundária versão demasiado**verdadeiro** garante que irá obter versão secundária mais recente Olá da extensão de Olá que está disponível. É altamente recomendável que defina sempre *autoUpgradeMinorVersion* tooalways ser **verdadeiro** para que recebem sempre toouse Olá mais recente disponível diagnostics a extensão com todas as novas funcionalidades de Olá e erros correções. 

Olá *definições* elemento contém as propriedades de configurações para a extensão de Olá que podem ser definidas e ler novamente a partir do extensão Olá (configuração pública, por vezes, referidos tooas). Olá *xmlcfg* propriedade contém com base em xml configuração para os registos de diagnóstico de Olá, etc., que serão recolhidas pelo agente de diagnóstico de Olá os contadores de desempenho. Consulte [esquema de configuração de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) para obter mais informações sobre o esquema de xml Olá próprio. Uma prática comum é a configuração de xml real toostore Olá como uma variável no modelo do Azure Resource Manager Olá e, em seguida, concatenate e base64 codificá-los do valor de Olá tooset para *xmlcfg*. Consulte a secção de Olá no [variáveis de configuração de diagnósticos](#diagnostics-configuration-variables) toounderstand mais informações sobre como toostore Olá xml em variáveis. Olá *storageAccount* propriedade especifica o nome de Olá Olá conta toowhich diagnósticos de dados de armazenamento será transferido. 

Olá propriedades no *protectedSettings* (por vezes, referidos tooas privada configuração) pode ser definida, mas não é possível ler novamente após a ser definida. Olá só de escrita natureza *protectedSettings* torna útil para armazenar segredos como Olá chave de conta do storage onde os dados de diagnóstico de Olá serão escritos.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Especificar a conta de armazenamento de diagnóstico como parâmetros
Olá diagnóstico extensão fragmento json acima assume que dois parâmetros *existingdiagnosticsStorageAccountName* e *existingdiagnosticsStorageResourceGroup* diagnósticos de Olá toospecify conta de armazenamento onde serão armazenados os dados de diagnóstico. Especificar a conta de armazenamento de diagnóstico de Olá como um parâmetro faz com que conta de armazenamento de diagnóstico de Olá toochange fácil entre ambientes diferentes por exemplo, poderá ser útil toouse uma conta de armazenamento do diagnostics diferentes para testar e outra para o implementação de produção.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

É melhor prática toospecify uma conta de armazenamento de diagnóstico num grupo de recursos diferente ao grupo de recursos de Olá para a máquina virtual de Olá. Um grupo de recursos pode ser considerado toobe uma unidade de implementação com a respetiva duração, uma máquina virtual pode ser implementada e implementar como novas atualizações de configurações são efetuadas-tooit mas poderá pretender toocontinue armazenar dados de diagnóstico de Olá no Olá mesma conta de armazenamento entre as implementações de máquina virtual. A presença de conta de armazenamento Olá num recurso diferentes permite Olá armazenamento conta tooaccept de dados de várias implementações de máquinas virtuais, tornando mais fácil tootroubleshoot problemas em Olá várias versões.

> [!NOTE]
> Se criar um modelo de máquina virtual do windows a partir do Visual Studio, pode ser definida a conta do storage predefinida Olá toouse Olá a mesma conta do storage onde o VHD da máquina Olá virtual é carregado. Esta é configuração inicial do toosimplify do Olá VM. Deverá pesar novamente Olá modelo toouse uma conta de armazenamento diferente que pode ser transmitida como um parâmetro. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>Variáveis de configuração de diagnóstico
Olá diagnóstico extensão fragmento json acima define um *accountid* toosimplify variável obter a chave de conta do storage Olá para armazenamento de diagnóstico de Olá:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Olá *xmlcfg* propriedade de extensão de diagnóstico de Olá está definida com várias variáveis que são concatenadas em conjunto. valores Olá destas variáveis são em xml, pelo que precisam de toobe escape corretamente ao definir variáveis de json Olá.

seguinte Olá descreve xml de configuração de diagnósticos Olá que recolhe os contadores de desempenho ao nível do sistema padrão, juntamente com alguns registos de eventos do windows e registos de infraestrutura de diagnóstico. Foi caráter de escape correto e formatado corretamente para que hello configuração pode diretamente ser colada na secção de variáveis de Olá do seu modelo. Consulte Olá [esquema de configuração de diagnósticos](https://msdn.microsoft.com/library/azure/dn782207.aspx) para obter um exemplo mais humano legível de Olá xml de configuração.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

nó xml de definição de métrica do Olá no Olá acima configuração é um elemento de configuração importantes como define como os contadores de desempenho de Olá definido anteriormente no xml de Olá no *PerformanceCounter* será agregado nó e armazenados. 

> [!IMPORTANT]
> Estas métricas unidade Olá monitorização gráficos e alertas no Olá portal do Azure.  Olá **métricas** nós com Olá *resourceID* e **MetricAggregation** tem de ser incluído na configuração de diagnósticos de Olá para a VM se quiser toosee Olá VM dados de monitorização no Olá portal do Azure. 
> 
> 

Olá segue-se um exemplo de Olá xml de definições de métrica: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Olá *resourceID* atributo identifica exclusivamente a máquina virtual de Olá na sua subscrição. Certifique-se de que subscription() de Olá toouse e resourceGroup() funciona para que hello modelo atualiza automaticamente esses valores com base no grupo de recursos e subscrição do Olá que estiver a implementar.

Se estiver a criar várias máquinas virtuais num ciclo, em seguida, terá de toopopulate Olá *resourceID* cada VM individuais de distinguir o valor com um toocorrectly de função copyindex (). Olá *xmlCfg* valor pode ser atualizada toosupport isto da seguinte forma:  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Olá MetricAggregation valor *PT1H* e *PT1M* significam uma agregação ao longo de um minuto e uma agregação mais de uma hora.

## <a name="wadmetrics-tables-in-storage"></a>Tabelas de WADMetrics no armazenamento
configuração de métricas de Olá acima irá gerar tabelas na sua conta de armazenamento de diagnóstico com Olá seguintes convenções de nomenclatura:

* **WADMetrics** : prefixo padrão para todas as tabelas de WADMetrics
* **PT1H** ou **PT1M** : significa nessa tabela Olá contém dados agregados mais de 1 hora ou de 1 minuto
* **P10D** : significa tabela Olá irá conter os dados de 10 dias do quando tabela Olá iniciou a recolha de dados
* **V2S** : constante de cadeia
* **AAAAMMDD** : data de Olá no qual Olá tabela iniciou a recolha de dados

Exemplo: *WADMetricsPT1HP10DV2S20151108* irá conter os dados de métricas agregados mais de uma hora para 10 dias, começando no 11-Novembro de 2015    

Cada tabela WADMetrics irá conter Olá seguintes colunas:

* **PartitionKey**: Olá partitionkey é criada com base no Olá *resourceID* valor toouniquely identificar o recurso VM de Olá. para por ex.: 002Fsubscriptions:<subscriptionID>: 002FresourceGroups:002F<ResourceGroupName>: 002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : formato de Olá de forma <Descending time tick>:<Performance Counter Name>. Olá descendente cálculo de marcas de escala de tempo é ticks de tempo máximo menos tempo Olá de início de Olá do período de agregação de Olá. Por exemplo, Se o período de exemplo de Olá iniciado em 10-Novembro de 2015 e 00:00Hrs UTC, em seguida, Olá cálculo seria: ticks - (DateTime(2015,11,10,0,0,0,DateTimeKind.Utc) novo. Batimentos). Para a chave de linha ao hello do contador de desempenho Olá memória bytes disponíveis procurará como: 2519551871999999999__:005CMemory:005CAvailable:0020 Bytes
* **CounterName** : É Olá nome de contador de desempenho de Olá. Isto corresponde à Olá *counterSpecifier* definidos na configuração do xml de Olá.
* **Máximo** : Olá valor máximo de contador de desempenho de Olá período de agregação de Olá.
* **Mínimo** : Olá valor mínimo de contador de desempenho de Olá período de agregação de Olá.
* **Total** : soma Olá de todos os valores de contador de desempenho de Olá comunicadas período de agregação de Olá.
* **Contagem** : número total de Olá dos valores comunicados Olá contador de desempenho.
* **Médio** : Olá valor média (contagem/total) de contador de desempenho de Olá período de agregação de Olá.

## <a name="next-steps"></a>Passos Seguintes
* Para um modelo de exemplo completo da máquina virtual do Windows com a extensão de diagnóstico consulte [201-vm-monitorização--extensão de diagnóstico](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Implementar através do modelo Olá resource manager [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [linha de comandos do Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Saiba mais sobre [criação de modelos Azure Resource Manager](../../resource-group-authoring-templates.md)

