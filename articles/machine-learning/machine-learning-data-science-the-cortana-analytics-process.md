---
title: "aaaWhat é o processo de ciência de dados de equipa?  | Microsoft Docs"
description: "Olá o processo de ciência de dados de equipa é um método systematic para compilar inteligentes aplicações que tiram partido da análise avançada."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>O que é Olá processo de ciência de dados de equipa (TDSP)?
Olá [processo de ciência de dados de equipa (TDSP)](data-science-process-overview.md) fornece uma abordagem systematic toobuilding aplicações inteligente que permite equipas de toocollaborate de cientistas de dados de forma eficaz ao longo do ciclo de vida completo do Olá de atividades necessário tooturn estas aplicações para os produtos. Olá TDSP descreve uma sequência de passos que fornecem **orientações** na forma como o problema de Olá toodefine, configurar Olá ferramentas e ambiente necessários, analisar dados relevantes, criar modelos preditivos de avaliar e, em seguida, implementar esses modelos na aplicações da empresa. 

Seguem-se passos Olá **o processo de ciência de dados de equipa**:  

![Fluxo de trabalho extremidade](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

processo de Olá é **iterativo**: Olá compreensão das novas e existentes ou refinamentos no modelo de Olá medida que evolui e requer reworking passos concluídos anteriormente na sequência de Olá. Desenvolvimento organizacional existente e processos de planeamento de projetos são **facilmente adaptada** toowork com Olá definido pelo TDSP sequência de passos. 

Olá passos no processo de Olá são diagrammed e ligados Olá [percurso de aprendizagem TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e descrito abaixo.  

## <a name="preparation-steps"></a>Passos de preparação
## <a name="p1-plan-hello-analytics-project"></a>P1. Planear o projeto de análise Olá
Inicie um projeto de análise, definindo os seus objetivos de negócio e problemas. Forem especificadas em termos de **requisitos comerciais**. Um central objetivo deste passo é tooidentify Olá empresarial fundamentais variáveis (vendas previsão ou Olá probabilidade de uma ordem a ser fraudulenta, por exemplo) Olá analysis necessidades toopredict toosatisfy estes requisitos. Planeamento adicional, em seguida, é essencial normalmente toodevelop uma compreensão dos Olá **origens de dados** necessário tooaddress Olá objetivos do projeto de Olá de uma perspetiva analítico. Não é invulgar, por exemplo, toofind que sistemas existentes têm toocollect e de registo adicionais tipos de dados tooaddress Olá o problema e alcançar os objetivos de projeto Olá. Para obter orientações, consulte [planear o ambiente para Olá o processo de ciência de dados de equipa](machine-learning-data-science-plan-your-environment.md) e [cenários para análise avançada no Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Configurar o ambiente da análise
Um ambiente de análise para Olá o processo de ciência de dados de equipa envolve vários componentes: 

* **áreas de trabalho de dados** onde os dados de Olá preparados para análise e modelação, 
* um **infraestrutura de processamento** para processar previamente, explorar e modelação dados Olá
* um **infraestrutura de runtime** toooperationalize Olá modelos analíticos e executar aplicações de cliente inteligente Olá que consumam modelos Olá.  

infraestrutura de análise de Olá que necessita de configuração de toobe é frequentemente parte de um ambiente que é separado dos sistemas operacionais core. Mas, utiliza normalmente dados a partir de vários sistemas na empresa Olá, bem como da empresa de toohello externo origens. infraestrutura de análise Olá pode ser puramente baseado na nuvem ou um programa de configuração no local ou uma versão híbrida do Olá dois. Para opções, consulte [configurar ambientes de ciência de dados para utilização num Olá o processo de ciência de dados de equipa](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Passos de análise:
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Ingerir dados no ambiente analíticos Olá
Step-by-Olá primeiro passo é toobring dados relevantes do Olá de várias origens, a partir do dentro ou do enterprise exteriores Olá, para uma análise ambientes onde os dados de Olá podem ser processados. Olá **formato** de Olá dados na origem podem ser diferentes de formato Olá exigido pelo destino Olá. Por isso, algumas transformação de dados pode também ter toobe feito por ferramentas de ingestão Olá. Para opções, consulte [carregar dados para ambientes de armazenamento para a análise](machine-learning-data-science-ingest-data.md)

Adição toohello inicial a ingestão de dados, muitas aplicações inteligentes são necessárias toorefresh Olá dados regularmente como parte de um processo de aprendizagem em curso. Isto pode ser feito ao configurar um **pipeline de dados** ou fluxo de trabalho. Isto faz parte da Olá iterativo parte processo Olá que inclui reconstruir e voltar a avaliar modelos analíticos Olá utilizados pela aplicação inteligente Olá implementar a solução de Olá. Vê, por exemplo, [mover dados de um tooSQL de servidor do SQL Server no local do Azure com o Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Explorar e pré-processar dados
Olá passo seguinte consiste em tooobtain uma compreensão mais aprofundada dos dados de Olá por investigar o **estatística de resumo** , relações e utilizando técnicas, tais **visualização**. Este é também onde problemas de **qualidade dos dados** e integridade, tais como os valores em falta, correspondência de tipo de dados e relações de dados inconsistentes, são processadas. Transformações previamente processamento são utilizado tooclean dos dados não processados do Olá antes de análise adicional e modelação pode ocorrer. Para obter uma descrição, consulte [tarefas tooprepare dados para o avançada de machine learning](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Desenvolver funcionalidades
Cientistas de dados em colaboração com especialistas de domínio, tem de identificar as funcionalidades de Olá que captura Olá salientes propriedades do conjunto de dados de Olá e que melhor podem ser utilizados toopredict as variáveis da empresarial fundamentais de Olá identificadas durante o planeamento da. Estas novas funcionalidades podem derivar de dados existentes ou podem necessitar de toobe dados adicionais recolhida. Este processo é conhecido como **engenharia da funcionalidade** e é uma das Olá passos chaves na criação de um sistema de Análise Preditiva Efetivo. Este passo necessita de uma combinação das informações de conhecimentos e Olá do domínio obtido a partir do passo de exploração de dados de Olá criativos. Para obter orientações, consulte [engenharia no Olá o processo de ciência de dados de equipa da funcionalidade](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Criar modelos preditivos
Cientistas de dados criar modelos analíticos toopredict Olá chave as variáveis identificadas pelos requisitos de negócio Olá definidos no Olá planeamento passo utilizando os dados que foi limpa e featurized. Sistemas do Machine learning suportam vários **modelação algoritmos** que são aplicáveis tooa ampla variedade de cenários. Para obter orientações, consulte [como algoritmos toochoose para a equipa do Azure Machine Learning](machine-learning-algorithm-choice.md).

Cientistas de dados tem de escolher modelo mais adequado do Olá para as respetivas tarefas de predição e não é invulgar que resultados a partir de vários modelos tem toobe combinado tooobtain Olá obter os melhores resultados. Olá dados de entrada para a modelação é normalmente divididos aleatoriamente em três partes:

* um conjunto de dados de formação 
* um conjunto de dados de validação 
* um conjunto de dados de teste 

modelos de Olá criados com Olá **conjunto de dados de formação**. Olá ideal combinação dos modelos (com parâmetros otimizados) está selecionada por com modelos de Olá e medir erros de predição de Olá para Olá **conjunto de dados de validação**. Por fim Olá **conjunto de dados de teste** é utilizado tooevaluate Olá desempenho do modelo de Olá escolhido nos dados independentes que não foi utilizado tootrain ou validar modelo Olá.  Para obter os procedimentos, consulte [como tooevaluate modelo desempenho no Azure Machine Learning](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Implementar e consumir modelos
Assim que tivermos um conjunto de modelos que efetuar bem, podem ser **operacionalizado** para tooconsume outras aplicações. Dependendo dos requisitos de negócio Olá, predições efetuadas no **em tempo real** ou num **batch** base. toobe operacionalizado, tem de modelos de Olá toobe exposto com um **abrir a interface de API** que é consumido facilmente de várias aplicações esse site online, folhas de cálculo, dashboards ou aplicações de empresas e o back-end de linha de. Consulte [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Resumo e os passos seguintes
Olá [o processo de ciência de dados de equipa](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) é modelada como uma sequência de passos iterated que **fornecem orientações** nas tarefas Olá toouse necessário avançadas análise toobuild um aplicações inteligente. Cada passo também fornece detalhes sobre como toouse descrito várias tarefas de Olá do toocomplete tecnologias Microsoft. 

Enquanto TDSP não recomende uma tipos específicos de **documentação** artefactos, é uma melhor prática toodocument Olá os resultados de exploração de dados de Olá, modelação e avaliação e toosave Olá pertinentes código, para que Olá Analysis Services Pode iterated quando necessário. Isto também permite a reutilização de Olá análise funciona quando trabalhar em outras aplicações que envolvem dados semelhantes e tarefas de predição.

Total de instruções ponto-a-ponto que demonstram todos os passos de Olá no processo de Olá para **cenários específicos** também são fornecidos. Consulte o artigo, por exemplo:

* [Olá o processo de ciência de dados de equipa em ação: utilizar o SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [Olá o processo de ciência de dados de equipa em ação: com clusters do HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).
* [Utilização do Spark no Azure HD.mdnsight de ciência de dados](machine-learning-data-science-spark-overview.md)
* [Dimensionável ciência de dados no Azure Data Lake: uma instruções ponto a ponto](machine-learning-data-science-process-data-lake-walkthrough.md)

