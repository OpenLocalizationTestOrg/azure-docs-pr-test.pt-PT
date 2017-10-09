---
title: "aaaCreate vários modelos de uma experimentação | Microsoft Docs"
description: "Utilize o PowerShell toocreate vários modelos de Machine Learning e web pontos finais de serviço com Olá mesmo algoritmo mas formação diferentes conjuntos de dados."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>Utilizar o PowerShell para criar muitos modelos do Machine Learning e pontos finais do serviço Web a partir de uma experimentação
Segue-se um problema de aprendizagem máquina comum: pretende toocreate muitos modelos que tenham Olá mesmo fluxo de trabalho de formação e utilize Olá mesmo algoritmo, mas tem conjuntos de dados de formação diferente como entrada. Este artigo mostra como toodo isto à escala no Azure Machine Learning Studio utilizando apenas uma única experimentação.

Por exemplo, vamos supor que é proprietário de uma bicicleta global rental franchise empresa. Pretende toobuild uma regressão modelo toopredict Olá rental a pedido com base nos dados históricos. Tiver 1.000 rental localizações em Olá mundo e ter recolhido um conjunto de dados para cada localização que inclui funcionalidades importantes, como data, hora, meteorologia e o tráfego que são específicas tooeach localização.

Foi possível preparar o seu modelo uma vez com uma versão intercalada de todos os conjuntos de dados de Olá em todas as localizações. Mas porque cada um dos seus localizações tem um ambiente exclusivo, uma abordagem de melhor seria possível tootrain o modelo de regressão Olá conjunto de dados a utilizar em separado para cada localização. Dessa forma, pode demorar cada modelo treinado para tamanhos de arquivo diferente conta Olá, volume, geografia, população, ambiente de tráfego de bicicleta amigável, *etc.*.

Que podem ser abordagem das melhores Olá, mas que não pretende experimentações de formação toocreate 1.000 no Azure Machine Learning com cada um, que representa uma localização única. Para além de ser uma tarefa muito confuso, também é parece pretty ineficaz, uma vez que cada experimentação teria todas Olá componentes mesmos, exceto para o conjunto de dados de formação de Olá.

Felizmente, iremos pode conseguir isto utilizando Olá [reparametrização API do Azure Machine Learning](machine-learning-retrain-models-programmatically.md) e automatizar tarefas de Olá com [PowerShell do Azure Machine Learning](machine-learning-powershell-module.md).

> [!NOTE]
> toomake nosso exemplo são executadas mais rápido, iremos irá reduzir Olá número de localizações de too10 1000. Mas hello mesmo princípios e procedimentos aplicam too1, 000 localizações. Step-by-Olá única diferença é que se quiser tootrain de conjuntos de 1.000 dados provavelmente pretende toothink da execução Olá seguintes scripts do PowerShell em paralelo. Como toodo ultrapassa o âmbito de Olá neste artigo, mas pode encontrar exemplos do PowerShell vários segmentos no Olá Internet.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Configurar a experimentação de preparação de Olá
Vamos toouse um exemplo [experimentação de preparação](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) que criámos já no Olá [galeria da Cortana Intelligence](http://gallery.cortanaintelligence.com). Abrir este experimentação na sua [Azure Machine Learning Studio](https://studio.azureml.net) área de trabalho.

> [!NOTE]
> Na ordem toofollow juntamente com este exemplo, poderá ser útil toouse uma área de trabalho padrão em vez de uma área de trabalho gratuita. Estamos irá criar um ponto final de cada cliente - para um total de pontos 10 finais - e que irão solicitar uma área de trabalho padrão, uma vez que a área de trabalho gratuita pontos finais de too3 limitado. Se tiver apenas uma área de trabalho gratuita, basta modificar scripts Olá abaixo tooallow apenas 3 localizações.
> 
> 

Olá experimentação utiliza um **importar dados** o conjunto de dados do módulo tooimport Olá formação *customer001.csv* de uma conta de armazenamento do Azure. Vamos assumir que tem recolhidas conjuntos de dados de formação de todas as localizações de rental bicicleta e armazenou numa Olá mesma localização de armazenamento de Blobs com nomes de ficheiro de *rentalloc001.csv* demasiado*rentalloc10.csv* .

![Imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Tenha em atenção que um **saída de serviço Web** módulo foi adicionado toohello **preparar modelo** módulo.
Quando esta fase experimental é implementado como um serviço web, o ponto final de Olá associada com essa saída irá devolver modelo treinado Olá no formato de Olá de um ficheiro de .ilearner.

Tenha também em atenção que configuramos um parâmetro de serviço web para o URL de Olá esse Olá **importar dados** módulo utiliza. Isto permite-nos toouse Olá parâmetro toospecify formação individuais conjuntos de dados tootrain Olá modelo para cada localização.
Existem outras formas que pode ter efetuado esta ação, por exemplo, utilizando uma consulta SQL com um web service parâmetro tooget de dados de uma base de dados do SQL Azure, ou simplesmente um **entrada de serviço Web** serviço web do módulo toopass no toohello conjunto de dados.

![Imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

Agora, vamos executar este experimentação de preparação utilizando um valor predefinido de Olá *rental001.csv* como Olá conjunto de dados de formação. Se visualizar resultado Olá Olá **Evaluate** módulo (clique saída Olá e selecione **visualizar**), pode ver obtemos um desempenho decent de *AUC* = 0.91. Neste momento, estamos pronto toodeploy um serviço web fora deste experimentação de preparação.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Implementar serviços web de classificação de cenários e estimativas de Olá
Olá toodeploy preparação do serviço web, clique em Olá **segurança serviço Web** no botão abaixo tela de experimentação Olá e selecione **implementar serviço Web**. Chamar este serviço web "" bicicleta Rental formação".

Agora que temos o serviço de web do toodeploy Olá classificação.
toodo isto, iremos pode clicar em **segurança serviço Web** abaixo Olá tela e selecione **preditiva serviço Web**. Esta ação cria uma experimentação de classificação.
Precisamos toomake alguns ajustes secundárias toomake, que funciona como um serviço web, tal como remover a coluna de etiqueta de Olá "cnt" da Olá dados de entrada e limitar o id de instância do Olá saída tooonly Olá e Olá correspondente prever valor.

toosave-se de que funcionam, pode simplesmente abrir Olá [experimentação preditiva](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) no Olá galeria que já foi preparada.

serviço web de Olá toodeploy, execute a experimentação preditiva Olá, em seguida, clique em Olá **implementar serviço Web** no botão abaixo tela Olá. Olá nome da classificação de serviço web "Bicicleta Rental classificação" ".

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>Criar 10 pontos finais do serviço web idênticos com o PowerShell
Este serviço web é fornecido com um ponto final predefinido. Mas não estamos como interessados no ponto final predefinido de Olá, uma vez que não pode ser atualizada. É necessário toodo é toocreate 10 os pontos finais adicionais, um para cada localização. Iremos irá efetuar este procedimento com o PowerShell.

Em primeiro lugar, iremos configurar nosso ambiente de PowerShell:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

Em seguida, execute o seguinte comando do PowerShell de Olá:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Agora, criámos 10 pontos finais e contêm Olá mesmo modelo treinado preparado no *customer001.csv*. Pode visualizá-los no Olá Portal de gestão do Azure.

![Imagem](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>Atualizar Olá pontos finais toouse formação separado conjuntos de dados com o PowerShell
Olá passo seguinte consiste em pontos finais de Olá tooupdate com os modelos que preparado exclusivamente nos dados individuais de cada cliente. Mas, primeiro é preciso tooproduce estes modelos de Olá **bicicleta Rental formação** serviço web. Passemos back toohello **bicicleta Rental formação** serviço web. É necessário toocall seu ponto final de BES 10 vezes com 10 formação diferentes conjuntos de dados na ordem tooproduce 10 diferentes criação de modelos. Utilizaremos Olá **InovkeAmlWebServiceBESEndpoint** toodo de cmdlet do PowerShell isto.

Também terá de tooprovide credenciais para a sua conta de armazenamento de BLOBs para `$configContent`, nomeadamente, em campos de Olá `AccountName`, `AccountKey` e `RelativeLocation`. Olá `AccountName` pode ser um dos seus nomes de conta, visto na Olá **Portal de gestão clássico do Azure** (*armazenamento* separador). Assim que clicar na conta de armazenamento, o `AccountKey` pode encontrar, premindo Olá **gerir chaves de acesso** botão na parte inferior de Olá e copiar Olá *chave de acesso primária*. Olá `RelativeLocation` é o armazenamento de tooyour relativo de caminho olá onde um novo modelo será armazenado. Por exemplo, caminho de Olá `hai/retrain/bike_rental/` no script de Olá abaixo pontos tooa contentor com o nome `hai`, e `/retrain/bike_rental/` estão subpastas. Atualmente, não é possível criar subpastas através da IU do portal de Olá, mas existem [várias exploradores de armazenamento do Azure](../storage/common/storage-explorers.md) que permitem-lhe toodo por isso. Recomenda-se que crie um novo contentor no seu Olá de toostore armazenamento novos modelos de formação (ficheiros .ilearner) da seguinte forma: a página de armazenamento, clique em Olá **adicionar** botão na parte inferior de Olá e dê-lhe nome `retrain`. Em resumo, o script de toohello das alterações necessárias Olá abaixo pertençam demasiado`AccountName`, `AccountKey` e `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> Olá BES endpoint é Olá modo apenas suportado para esta operação. RRS não pode ser utilizada para produzir os modelos de formação.
> 
> 

Como pode ver acima, em vez de construir 10 diferentes BES tarefa json ficheiros de configuração, vamos criar uma cadeia de configuração de Olá em vez disso e dinamicamente feed-toohello *jobConfigString* parâmetro de Olá  **InvokeAmlWebServceBESEndpoint** cmdlet, porque não existe realmente não tookeep necessidade de uma cópia no disco.

Se tudo correr bem, ao fim de algum deve vir de 10 .ilearner os ficheiros, de *model001.ilearner* demasiado*model010.ilearner*, na sua conta do storage do Azure. Agora está tudo pronto tooupdate nosso 10 classificação web service pontos finais com estes modelos utilizando Olá **Patch AmlWebServiceEndpoint** cmdlet do PowerShell. Lembre-se novamente, apenas pode corrigir pontos finais não predefinidas de Olá que programaticamente criámos anteriormente.

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

Isto deve ser executada razoavelmente depressa. Quando termina a execução de Olá, iremos irá criada com êxito 10 web preditiva pontos finais de serviço, cada um possuindo um modelo preparado exclusivamente preparado no Olá conjunto de dados específico tooa rental localização, tudo a partir de uma experimentação de preparação único. tooverify, pode tentar chamar estes pontos finais utilizando Olá **InvokeAmlWebServiceRRSEndpoint** cmdlet, fornecendo-las com Olá mesmo dados de entrada e deve esperar toosee resultados de predição diferentes, desde que os modelos do Olá preparado com conjuntos de formação diferentes.

## <a name="full-powershell-script"></a>Total de script do PowerShell
Eis listagem Olá do código de origem completo Olá:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
