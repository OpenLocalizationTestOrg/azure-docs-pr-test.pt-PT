---
title: problemas de Azure Data Factory aaaTroubleshoot
description: "Saiba como tootroubleshoot problemas com a utilização do Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a>Resolver Problemas do Data Factory
Este artigo fornece sugestões de resolução de problemas para problemas ao utilizar o Azure Data Factory. Este artigo não listar todos os problemas de possíveis Olá ao utilizar o serviço de Olá, mas abrange alguns problemas e sugestões de resolução de problemas gerais.   

## <a name="troubleshooting-tips"></a>Sugestões de resolução de problemas
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Erro: a subscrição de Olá não está registado toouse espaço de nomes 'Microsoft. DataFactory'
Se receber este erro, o fornecedor de recursos do Azure Data Factory Olá não foi registado no seu computador. Olá seguintes:

1. Inicie o Azure PowerShell.
2. Inicie sessão no tooyour conta do Azure utilizando Olá os seguintes comandos.

    ```powershell
    Login-AzureRmAccount
    ```
3. Execute Olá seguir o fornecedor do comando tooregister Olá do Azure Data Factory.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Problema: Não autorizado Ocorreu um erro ao executar um cmdlet de fábrica de dados
Provavelmente não estiver a utilizar o direito de Olá conta do Azure ou de subscrição com Olá Azure PowerShell. Utilize Olá os seguintes cmdlets tooselect Olá direito toouse de conta e subscrição do Azure com Olá Azure PowerShell.

1. Login-AzureRmAccount - ID de utilizador correto de Olá de utilização e a palavra-passe
2. Get-AzureRmSubscription - vista Olá todas as subscrições da conta de Olá.
3. SELECT-AzureRmSubscription &lt;nome da subscrição&gt; -selecionar a subscrição correta Olá. Utilize Olá mesmo utilizar toocreate uma fábrica de dados no Olá portal do Azure.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Problema: Falha toolaunch Express programa de configuração do Gateway do gestão de dados a partir do portal do Azure
a configuração de Express de Olá para Olá Data Management Gateway requer o Internet Explorer ou um Microsoft ClickOnce browser compatível com. Se Olá configuração Express falhar toostart, efetue um dos seguintes Olá:

* Utilize o Internet Explorer ou um ClickOnce da Microsoft compatível browser.

    Se estiver a utilizar o Chrome, aceda toohello [arquivo da web de Chrome](https://chrome.google.com/webstore/), pesquise com palavra-chave de "ClickOnce", escolha uma das extensões de ClickOnce Olá e instalá-lo.

    Olá, mesmo para Firefox (instalação suplemento). Clique no botão de abrir Menu na barra de ferramentas Olá (nas três linhas horizontais no canto superior direito de Olá), clique em suplementos, procurar com palavra-chave de "ClickOnce", escolha uma das extensões de ClickOnce Olá e instalá-lo.
* Olá utilize **configuração Manual** ligação apresentada na Olá mesmo painel no portal de Olá. Pode utiliza este ficheiro de instalação de toodownload abordagem e executá-la manualmente. Após a instalação de Olá for bem sucedida, verá a caixa de diálogo de configuração do Gateway de gestão de dados de Olá. Olá cópia **chave** no ecrã de portal de Olá e utilize-a no Olá configuration manager toomanually registar o gateway de Olá com o serviço de Olá.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Problema: Falha tooconnect tooon local do SQL Server
Iniciar **Gestor de configuração do Data Management Gateway** no Olá computador gateway e utilize Olá **resolução de problemas** separador tootest Olá ligação tooSQL servidor da máquina do gateway de Olá. Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para dicas sobre/gateway de ligação de resolução de problemas relacionados com problemas.   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Problema: Setores de entrada estão a aguardar estado por alguma vez
setores Olá dever-se no **a aguardar** Estado devido a razões toovarious. É uma das razões comuns Olá esse Olá **externo** propriedade não está definida demasiado**verdadeiro**. Qualquer conjunto de dados que é o âmbito de produzidos Olá fora do Azure Data Factory deve ser marcado com **externo** propriedade. Esta propriedade indica que os dados de Olá são externos e não é efetuada por qualquer pipelines dentro da fábrica de dados de Olá. setores de dados de Olá estão marcados como **pronto** depois Olá os dados estão disponíveis no arquivo respetivos Olá.

Consulte Olá seguinte o exemplo de utilização de Olá de Olá **externo** propriedade. Pode especificar opcionalmente **externalData*** quando configurar tootrue externo.

Consulte [conjuntos de dados](data-factory-create-datasets.md) artigo para obter mais detalhes sobre esta propriedade.

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

tooresolve Olá erro, adicione Olá **externo** propriedade e Olá opcional **externalData** secção toohello definição de JSON da tabela de entrada Olá e recrie a tabela de Olá.

### <a name="problem-hybrid-copy-operation-fails"></a>Problema: Falha de operação de cópia híbrida
Consulte [resolver problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para passos tootroubleshoot problemas com a cópia de um dados no local/arquivo utiliza Olá Data Management Gateway.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Problema: HDInsight a pedido falha de aprovisionamento
Quando utilizar um serviço ligado do tipo HDInsightOnDemand, terá de toospecify um linkedServiceName que aponta tooan Blob Storage do Azure. Serviço de fábrica de dados utiliza este armazenamento toostore registos e ficheiros de suporte para o cluster de HDInsight a pedido.  Por vezes, o aprovisionamento de um cluster do HDInsight a pedido falha com Olá seguinte erro:

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Este erro normalmente indica que a localização de Olá Olá da conta de armazenamento especificada na Olá linkedServiceName não está a ser Olá localização onde Olá HDInsight aprovisionamento está a acontecer do Centro de dados do mesmos. Exemplo: se a fábrica de dados está nos EUA oeste e Olá storage do Azure está nos EUA leste, Olá a pedido falha aprovisionamento nos EUA oeste.

Além disso, existe um segundo additionalLinkedServiceNames de propriedade JSON onde é possível especificar contas de armazenamento adicionais no HDInsight a pedido. Essas contas de armazenamento ligado adicional devem estar no Olá falha a mesma localização que o cluster do HDInsight hello, ou com Olá mesmo erro.

### <a name="problem-custom-net-activity-fails"></a>Problema: Personalizado não for possível atividade de .NET
Consulte [depurar um pipeline com atividade personalizada](data-factory-use-custom-activities.md#troubleshoot-failures) para obter passos detalhados.

## <a name="use-azure-portal-tootroubleshoot"></a>Utilizar tootroubleshoot portal do Azure
### <a name="using-portal-blades"></a>Com os painéis do portais
Consulte [monitorizar o pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) para obter os passos.

### <a name="using-monitor-and-manage-app"></a>Com a Aplicação Monitorizar e Gerir
Consulte [monitorizar e gerir pipelines de fábrica de dados com a monitorizar e gerir aplicações](data-factory-monitor-manage-app.md) para obter mais detalhes.

## <a name="use-azure-powershell-tootroubleshoot"></a>Utilizar o Azure PowerShell tootroubleshoot
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Utilizar o Azure PowerShell tootroubleshoot um erro
Consulte [Monitor Data Factory pipelines com o Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) para obter mais detalhes.

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
