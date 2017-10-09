---
title: aaaALM no Azure Machine Learning | Microsoft Docs
description: "Aplique as melhores práticas de gestão de ciclo de vida de aplicação no Azure Machine Learning Studio"
keywords: "Controlo de versão do Azure ML, gestão de ciclo de vida de aplicações, ALM, AML,"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Gestão de ciclo de vida de aplicação no Azure Machine Learning Studio
Azure Machine Learning Studio é uma ferramenta para o desenvolvimento de experimentações de machine learning que são operacionalizadas na plataforma de nuvem do Azure Olá. É como Olá IDE do Visual Studio e o serviço de nuvem dimensionáveis intercalados numa plataforma única. Pode incorporar padrão práticas de gestão de ciclo de vida de aplicação (ALM), do controlo de versões vários e implementação, da execução de tooautomated de recursos do Azure Machine Learning Studio. Este artigo descreve algumas das opções de Olá e abordagens.

## <a name="versioning-experiment"></a>Experimentação de controlo de versões
Existem duas formas recomendada tooversion das suas experimentações. Pode confiar no histórico de execução incorporado, ou exportar Olá experimentação no formato de JavaScript Object Notation (JSON) e geri-lo externamente. Cada abordagem é fornecido com o respetivo os profissionais de TI e contras.

### <a name="experiment-snapshots-using-run-history"></a>Utilizar o histórico de execuções de instantâneos de experimentação
No modelo de execução de Olá de Olá experimentação de aprendizagem do Azure Machine Learning Studio, sempre que clica Olá **executar** botão num editor de experimentação Olá, um instantâneo da experimentação Olá imutável é submetido toohello Programador de tarefas. Pode ver esta lista de instantâneos clicando Olá **histórico de execuções** botão na barra de comando Olá na vista de editor Olá experimentação.

![Botão de histórico de execução](media/machine-learning-version-control/runhistory.png)

O utilizador pode, em seguida, instantâneo Olá aberto no modo de está bloqueado, clicando em nome de Olá da experimentação Olá na experimentação de Olá Olá tempo foi submetido toorun e Olá instantâneo foi tirado. Tenha em atenção que apenas Olá primeiro item na lista de Olá, que representa a experimentação atual Olá, está num estado editável. Também tenha em atenção que cada instantâneo pode estar em estado de vários Estados bem, incluindo concluído (parcial executar) falhou, com falhas (parcial executar), ou de rascunho.

![Lista de histórico de execução](media/machine-learning-version-control/runhistorylist.png)

Depois de ter aberta, pode guardar Olá instantâneo experimentação como uma nova experimentação e depois modificá-lo. Se o instantâneo de experimentação contém recursos, tais como um modelo preparado, transformação ou conjunto de dados que tenham atualizado de versões, o instantâneo de Olá mantém versão original do Olá referências toohello quando Olá instantâneo foi tirado. Se guardar Olá bloqueado instantâneo como uma nova experimentação, Azure Machine Learning Studio detetar a existência de Olá de uma versão mais recente estes recursos e atualiza automaticamente na nova experiência de Olá.

Se eliminar experimentação Olá, são eliminados todos os instantâneos dessa experiência.

### <a name="exportimport-experiment-in-json-format"></a>Experimentação de exportação/importação no formato JSON
instantâneos do histórico de Olá executar mantenha uma versão imutável do Olá experimentação no Azure Machine Learning Studio sempre que é submetido toorun. Pode também guardar uma cópia local da experimentação Olá e registá-lo no sistema de controlo de origem favorito de tooyour, tais como o Team Foundation Server e mais tarde voltar a criar uma experimentação de que o ficheiro local. Pode utilizar Olá [PowerShell do Azure Machine Learning](http://aka.ms/amlps) mini-comandos [ *exportação AmlExperimentGraph* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) e [  *Importar AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish que.

ficheiro JSON Olá é uma representação textual de Olá experimentação gráfico, que pode incluir uma referência tooassets na área de trabalho Olá, tais como um conjunto de dados ou um modelo preparado. Não contém uma versão de ativo Olá serializada. Se tentar documento JSON tooimport Olá novamente para a área de trabalho Olá, ativos Olá referenciada já devem existir com Olá mesmo recurso IDs que são referenciados na experimentação de Olá. Caso contrário, não será capaz de tooaccess Olá importado experimentação.

## <a name="versioning-trained-model"></a>Modelo treinado do controlo de versões
Um modelo preparado no Azure Machine Learning está a ser serializado para um formato ao conhecido como um ficheiro de .iLearner e for armazenado na conta de armazenamento de Blobs do Azure Olá associada à área de trabalho Olá. Uma forma tooget uma cópia do ficheiro de .iLearner Olá é efetuada através de Olá reparametrização API. [Este artigo](machine-learning-retrain-models-programmatically.md) explica como funciona o Olá reparametrização API. passos de alto nível Olá:

1. Configure a sua experimentação de preparação.
2. Adicione uma saída porta toohello preparar modelo módulo do serviço web ou o módulo Olá que produz o modelo treinado Olá, tais como otimizar Hyperparameter do modelo ou criar modelo de R.
3. Execute a experimentação de preparação e, em seguida, implementá-lo como um serviço de web de formação do modelo.
4. Chamar Olá BES ponto final do serviço de web de formação Olá e especifique o nome de ficheiro Olá .iLearner pretendido e localização da conta de armazenamento de BLOBs onde será armazenado.
5. Recolher Olá produzido .iLearner ficheiro depois de chamar Olá BES é concluída.

Outra forma tooretrieve Olá .iLearner o ficheiro de está através de Olá PowerShell commandlet [ *transferência AmlExperimentNodeOutput*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput). Esta situação pode ser mais fácil se pretender apenas tooget uma cópia do Olá .iLearner ficheiro sem modelo de Olá Olá necessidade tooretrain através de programação.

Depois de ter Olá .iLearner ficheiro que contém o modelo treinado Olá, em seguida, pode utilizar a seus próprios estratégia de controlo de versões. estratégia de Olá pode ser tão simple como aplicar um pre sufixo como uma convenção de nomenclatura e deixando apenas o ficheiro de .iLearner Olá no armazenamento de BLOBs ou copiar/importá-lo no seu sistema de controlo de versão.

ficheiro de .iLearner guardado Olá, em seguida, pode ser utilizado para classificação através dos serviços web implementado.

## <a name="versioning-web-service"></a>Serviço web de controlo de versões
Pode implementar dois tipos de serviços web de uma experimentação do Azure Machine Learning. serviço web clássico de Olá é fortemente conjugado com experimentação Olá, bem como a área de trabalho Olá. novo serviço de web Olá utiliza arquitetura de Gestor de recursos do Azure Olá e já não está a ser integrado com experimentação original Olá ou a área de trabalho Olá.

### <a name="classic-web-service"></a>Serviço web clássico
tooversion um serviço web clássico, pode tirar partido de construção de ponto final de serviço do Olá web. Eis um fluxo típico de:

1. Da sua experimentação preditiva, implemente um novo serviço web clássico, que contém um ponto final predefinido.
2. Criar um novo ponto final com o nome ep2, que expõe a versão atual do Olá do modelo de experimentação/preparado Olá.
3. Pode voltar atrás e atualizar a sua experimentação preditiva e o modelo treinado.
4. Reimplementar experimentação preditiva Olá, que, em seguida, irá atualizar o ponto final do Olá predefinido. Mas isto não irá alterar ep2.
5. Criar um ponto de final adicional com o nome ep3, que expõe a nova versão de Olá da experimentação Olá e o modelo treinado.
6. Volte atrás toostep 3, se necessário.

Ao longo do tempo, pode ter vários pontos finais criados no Olá mesmo serviço web. Cada ponto final representa uma cópia de ponto no tempo da experimentação Olá que contém a versão de pontos no tempo de Olá do modelo treinado Olá. Em seguida, pode utilizar toodetermine lógica externa que toocall de ponto final, que efetivamente significa selecionar uma versão de Olá preparado modelo para a execução da classificação de Olá.

Pode também criar vários pontos finais do serviço web idênticos e, em seguida, aplicar o patch versões diferentes do Olá .iLearner ficheiro toohello endpoint tooachieve semelhantes em vigor. [Este artigo](machine-learning-create-models-and-endpoints-with-powershell.md) explica em detalhe mais como tooaccomplish que.

### <a name="new-web-service"></a>Novo serviço web
Se criar um novo serviço web baseado no Azure Resource Manager, construção de ponto final de Olá já não está disponível. Em vez disso, pode gerar ficheiros de definição (WSD) do serviço web, no formato JSON, da sua experimentação preditiva utilizando Olá [exportação AmlWebServiceDefinitionFromExperiment](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) commandlet do PowerShell, ou utilizando Olá [ *Exportação AzureRmMlWebservice* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) commandlet PowerShell a partir de um serviço web implementado baseado no Resource Manager.

Depois de ter Olá exportado WSD ficheiro e a versão controlá-lo, também pode implementar Olá WSD como um novo serviço web um plano de serviço web diferente na região do Azure diferente. Basta certificar-se de que fornecer a conta de armazenamento adequada de Olá configuração, bem como Olá web novo ID de plano de serviço. toopatch nos ficheiros de .iLearner diferente, pode modificar o ficheiro WSD Olá e referência de localização de Olá de atualização de Olá preparado modelo e implementá-lo como um novo serviço web.

## <a name="automate-experiment-execution-and-deployment"></a>Automatizar a implementação e execução da experimentação
Um aspeto importante de ALM é a execução de Olá tooautomate capaz de toobe e processo de implementação da aplicação Olá. No Azure Machine Learning, pode conseguir isto, utilizando Olá [módulo do PowerShell](http://aka.ms/amlps). Eis um exemplo de passos de ponto-a-ponto que são relevantes tooa padrão ALM automatizada implementação/execução processo através da utilização de Olá [módulo do PowerShell do Azure Machine Learning Studio](http://aka.ms/amlps). Cada passo é tooone ligado ou mais PowerShell mini-comandos que pode utilizar tooaccomplish que passo.

1. [Carregar um conjunto de dados](https://github.com/hning86/azuremlps#upload-amldataset).
2. Copiar uma experimentação de preparação para a área de trabalho Olá de um [área de trabalho](https://github.com/hning86/azuremlps#copy-amlexperiment) ou a partir de [galeria](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), ou [importar](https://github.com/hning86/azuremlps#import-amlexperimentgraph) um [exportado](https://github.com/hning86/azuremlps#export-amlexperimentgraph) experimentação de disco local.
3. [Atualizar o conjunto de dados de Olá](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) na experimentação de preparação de Olá.
4. [Execute a experimentação de preparação de Olá](https://github.com/hning86/azuremlps#start-amlexperiment).
5. [Promover modelo treinado Olá](https://github.com/hning86/azuremlps#promote-amltrainedmodel).
6. [Copiar uma experimentação preditiva](https://github.com/hning86/azuremlps#copy-amlexperiment) na área de trabalho Olá.
7. [Modelo treinado do atualização Olá](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) na experimentação preditiva Olá.
8. [Execute experimentação preditiva Olá](https://github.com/hning86/azuremlps#start-amlexperiment).
9. [Implementar um serviço web](https://github.com/hning86/azuremlps#new-amlwebservice) da experimentação preditiva Olá.
10. Testar o serviço web de Olá [RRS](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) ou [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) ponto final.

## <a name="next-steps"></a>Passos seguintes
* Transferir Olá [Azure Machine Learning Studio PowerShell](http://aka.ms/amlps) tooautomate módulo e iniciar as suas tarefas ALM.
* Saiba como demasiado[criar e gerir grande número de modelos de ML utilizando apenas uma única experimentação](machine-learning-create-models-and-endpoints-with-powershell.md) através do PowerShell e reparametrização API.
* Saiba mais sobre [implementar serviços web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
