---
title: "aaaFeature engenharia e seleção no Azure Machine Learning | Microsoft Docs"
description: "Explica fins Olá de seleção de funcionalidade e engenharia da funcionalidade e fornece exemplos da sua função no processo de dados-melhoramento Olá de aprendizagem."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>“Feature engineering” e seleção no Azure Machine Learning
Este tópico explica a fins de Olá de engenharia da funcionalidade e a seleção de funcionalidades no processo de dados-melhoramento Olá de aprendizagem. Ilustra o que estes processos envolvem utilizando exemplos fornecidos pelo Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

dados de formação Olá utilizados na machine learning, muitas vezes, podem ser melhorados através da seleção de Olá ou extração das funcionalidades de dados não processados Olá recolhidos. Um exemplo de uma funcionalidade engineered no contexto de Olá da learning como imagens de Olá tooclassify carateres handwritten é um mapa de bits densidade construídas a partir de dados de distribuição de bits não processados de Olá. Este mapa pode ajudar a localizar de forma mais eficiente de distribuição não processados Olá contornos Olá de carateres de Olá.

Funcionalidades selecionadas foi desenvolvidas e aumentam a eficiência de Olá do processo de preparação de Olá, que tenta tooextract Olá chave as informações contidas nos dados de Olá. Eles também melhorar o power Olá estes modelos tooclassify Olá de dados de entrada com precisão e resultados de toopredict do seu interesse mais robustly. Engenharia da funcionalidade e a seleção também podem combinar learning de Olá toomake mais viáveis tractable. Isto é feito através da Otimização e, em seguida, reduzir o número de Olá das funcionalidades necessárias toocalibrate ou preparar um modelo. Matematicamente utilizando um modelo de Olá Olá funcionalidades tootrain selecionados são um conjunto mínimo de variáveis independentes que explicam padrões Olá nos dados de Olá e, em seguida, prever resultados com êxito.

engenharia Olá e seleção de funcionalidades é uma parte de um processo maior, que normalmente consiste em quatro passos:

* Recolha de dados
* Melhoramento de dados
* Construção de modelo
* Pós-processamento

Engenharia e seleção de constituem Olá dados melhoramento passo aprendizagem. Podem ser distinguidos três aspetos deste processo para o nosso fins:

* **O pré-processamento de dados**: Este processo tenta tooensure que os dados recolhidos de Olá está limpa e consistente. Inclui tarefas como integrar vários conjuntos de dados, processamento de dados em falta, processamento de dados inconsistentes e conversão de tipos de dados.
* **Engenharia da funcionalidade**: Este processo tenta toocreate relevantes as funcionalidades adicionais do Olá em bruto as funcionalidades existentes no Olá dados e tooincrease energia preditiva toohello algoritmo de aprendizagem.
* **Seleção de funcionalidade**: Este processo seleciona subconjunto chave Olá original dados funcionalidades tooreduce Olá dimensionalidade do problema de formação Olá.

Este tópico aborda apenas Olá funcionalidade engenharia e a funcionalidade de seleção aspetos do processo de melhoramento do Olá dados. Para obter mais informações sobre o passo de pré-processamento de dados de Olá, consulte [processar previamente os dados no Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Funcionalidades de criação dos seus dados – engenharia da funcionalidade
dados de formação Olá é composta por uma matriz composta exemplos (registos ou as observações armazenadas nas linhas), cada um dos quais tem um conjunto de funcionalidades (os campos armazenados nas colunas ou variáveis). funcionalidades de Olá especificadas na estrutura experimental Olá são toocharacterize esperado Olá padrões nos dados de Olá. Embora muitos dos dados não processados Olá campos podem ser incluídos diretamente no hello funcionalidade selecionada conjunto utilizado tootrain um modelo, funcionalidades adicionais foi desenvolvidas muitas vezes necessitam toobe construída a partir das funcionalidades de Olá no Olá dados não processados toogenerate um conjunto de dados de formação avançada.

Que tipo de funcionalidades deverá ser criado um conjunto de dados de Olá tooenhance quando se prepara um modelo? Funcionalidades foi desenvolvidas que melhoram a formação Olá fornecem informações que melhor diferencia à padrões Olá nos dados de Olá. Esperar Olá novas funcionalidades tooprovide informações adicionais que não é claramente capturada ou facilmente aparente em Olá original ou definir a funcionalidade existente, mas este processo é algo um art. Decisões de som e produtivas frequentemente requerem alguns conhecimentos de domínio.

Ao iniciar com o Azure Machine Learning, é mais fácil toograsp este processo concretely utilizando exemplos fornecido no Machine Learning Studio. Dois exemplos são apresentados aqui:

* Um exemplo de regressão ([previsão do número de Olá de alugueres de bicicleta](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) numa experimentação supervisionada onde os valores de destino Olá são conhecidos
* Uma classificação de extração de texto exemplo com [funcionalidade hash][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Exemplo 1: Adicionar funcionalidades temporais para um modelo de regressão
toodemonstrate como tooengineer funcionalidades para uma tarefa de regressão, vamos utilizar Olá experimentação "a pedido previsão de bikes" no Azure Machine Learning Studio. objetivo do Olá desta fase experimental é toopredict procura Olá bikes hello, ou seja, Olá diversas alugueres de bicicleta dentro de um mês, dia ou hora específico. conjunto de dados de Olá **conjunto de dados de bicicleta Rental UCI** é utilizado como dados de entrada não processados Olá.

Este conjunto de dados é baseado nos dados reais anónimos da Olá da empresa de Capital Bikeshare que mantém uma bicicleta rental rede Washington D.C. no Olá dos Estados Unidos. conjunto de dados de Olá representa número de Olá de alugueres de bicicleta dentro de uma hora específica de um dia, 2011 too2012 e contém 17379 linhas e colunas de 17. conjunto de funcionalidades em bruto de Olá contém as condições de Meteorologia (temperatura humidade, a velocidade do vento) e o tipo de Olá do dia de Olá (feriado ou dia da semana). Olá campo toopredict é **cnt**, um número que representa alugueres de bicicleta Olá dentro de uma hora específica e que intervalos de 1 too977.

tooconstruct funcionalidades efeito nos dados de formação Olá, quatro modelos de regressão são criados utilizando Olá mesmo algoritmo, but com dados de formação diferentes quatro define. Olá quatro conjuntos de dados representam Olá mesmos dados de entrada não processados, mas com um número crescente de funcionalidades definida. Estas funcionalidades estão agrupadas em quatro categorias:

1. A fim de semana funcionalidades para o dia previstas Olá + de = Meteorologia + feriado + dia da semana
2. B = diversas bikes foram rented em cada um dos Olá anteriores 12 horas
3. C = diversas bikes foram rented em cada um dos Olá últimos 12 dias em Olá mesma hora
4. D = diversas bikes foram rented em cada um dos Olá anteriores 12 semanas em Olá mesma hora e Olá mesmo dia

Para além de um conjunto de funcionalidade, que já existe nos dados não processados original de Olá, hello outros três conjuntos de funcionalidades são criados através da funcionalidade de Olá processos de engenharia. Funcionalidade definida B capturas Olá recente a pedido para bikes Olá. Funcionalidade definido C capturas Olá a pedido para bikes uma hora específica. Funcionalidade definido a pedido de captura de D para bikes determinada hora e dia específico da semana de Olá. Cada um dos conjuntos de dados de formação Olá quatro inclui conjuntos de funcionalidades A, D + B, D + B + C e D + B + C + D, respetivamente.

No Olá experimentação do Azure Machine Learning, estes quatro conjuntos de dados de formação são formados através de quatro ramos conjunto de dados de entrada pré-processados de Olá. Exceto ramo mais â esquerda de Olá, cada um destes ramos contém um [executar Script do R] [ execute-r-script] módulo no qual um conjunto de derivada funcionalidades (funcionalidade define B, C e D), respetivamente é construído e acrescentado toohello importar o conjunto de dados. Olá figura a seguir demonstra o script de Olá R utilizado o conjunto de funcionalidades de toocreate B no ramo do Olá segundo esquerdo.

![Criar um conjunto de funcionalidades](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

Olá tabela seguinte resume a comparação de Olá dos resultados de desempenho de Olá dos modelos de quatro Olá. Olá obter os melhores resultados, são apresentados as funcionalidades de D + B + C. Tenha em atenção que taxa de erros de Olá diminui quando conjuntos de funcionalidades adicionais são incluídos nos dados de formação Olá. Isto verifica o nosso presumption que Olá B e C fornecem informações adicionais de relevantes para a tarefa de regressão Olá de conjuntos de funcionalidades. Adicionar o conjunto de funcionalidades de Olá D aparenta não tooprovide qualquer redução adicional da taxa de erros de Olá.

![Comparar os resultados de desempenho](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a>Exemplo 2: Criar funcionalidades na extração de texto
Engenharia da funcionalidade é amplamente aplicada no tootext relacionados com tarefas de extração, tais como a análise de classificação e dados de sentimento do documento. Por exemplo, quando pretender tooclassify documentos em várias categorias, um pressuposto típico é que palavras Olá ou frases reconhecíveis incluídos na categoria de um documento são menos provável toooccur noutra categoria do documento. Por outras palavras, a frequência de Olá da distribuição de Olá palavra ou expressão é capaz de toocharacterize categorias de documento diferente. Em aplicações de extração de texto, a funcionalidade de Olá processos de engenharia é necessário toocreate Olá funcionalidades que envolvam frequências palavra ou expressão porque partes individuais de conteúdos de texto, normalmente, servem como Olá dados de entrada.

tooachieve esta tarefa, uma técnica chamada *funcionalidade hash* é aplicado tooefficiently ativar funcionalidades de texto arbitrários para índices. Em vez de associação de cada funcionalidade (palavras ou frases reconhecíveis) tooa específico índice de texto, este funções de método aplicando um funcionalidades de toohello de função de hash e utilizando os valores de hash como índices diretamente.

No Azure Machine Learning, há um [funcionalidade hash] [ feature-hashing] módulo que cria estas funcionalidades palavra ou expressão. Olá figura seguinte mostra um exemplo de como utilizar este módulo. conjunto de dados de entrada Olá contém duas colunas: classificação de livro Olá vão de 1 too5 e Olá real revisão conteúdo. este objetivo Olá [funcionalidade hash] [ feature-hashing] módulo é tooretrieve novas funcionalidades que mostram a frequência de ocorrência de Olá de palavras correspondente Olá ou frases reconhecíveis dentro de revisão de livro específico Olá. toouse este módulo, terá de Olá toocomplete os seguintes passos:

1. Coluna de Olá SELECT que contém o texto de entrada Olá (**Col2** neste exemplo).
2. Definir *hash bitsize* too8, o que significa a 2 ^ 8 = 256 funcionalidades são criadas. Olá palavra ou frase no texto Olá é, em seguida, too256 índices de hash. Olá parâmetro *hash bitsize* intervalos de 1 too31. Se o parâmetro de Olá estiver definido palavras de Olá de números, maior de tooa ou expressões são menos prováveis toobe codificadas no Olá mesmo índice.
3. Defina o parâmetro Olá *N-grams* too2. Este obtém o Olá ocorrência frequência unigrams (uma funcionalidade para cada uma única palavra) e bigrams (uma funcionalidade para cada par de palavras adjacentes) a partir do texto de entrada Olá. Olá parâmetro *N-grams* intervalos de too10 0, o que indica o número máximo de Olá de toobe palavras sequenciais incluído numa funcionalidade.  

![Módulo de hash de funcionalidade](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Olá figura seguinte mostra que aspeto estas novas funcionalidades.

![Exemplo de hash de funcionalidade](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Filtragem de funcionalidades dos seus dados - seleção de funcionalidades
*Seleção de funcionalidade* é um processo que é normalmente aplicada toohello construção de conjuntos de dados de formação para tarefas de modelação preditiva como tarefas de classificação ou regressão. o objetivo de Olá é tooselect um subconjunto das funcionalidades de Olá Olá original conjunto de dados que reduz o respetivas dimensões utilizando um conjunto mínimo de período máximo do funcionalidades toorepresent Olá de variância nos dados de Olá. Este subconjunto das funcionalidades contém Olá apenas funcionalidades toobe incluído tootrain Olá modelo. A seleção de funcionalidades serve duas finalidades principais:

* A seleção de funcionalidades, muitas vezes, aumenta a precisão da classificação através da eliminação irrelevantes, redundante ou altamente correlacionadas funcionalidades.
* Funcionalidade seleção diminuições Olá várias funcionalidades, que torna o processo de preparação do modelo de Olá mais eficiente. Isto é particularmente importante para learners são dispendiosas tootrain como máquinas de vetor de suporte.

Embora a seleção de funcionalidades procura tooreduce Olá diversas funcionalidades Olá o conjunto de dados utilizado tootrain Olá modelo, não é geralmente referido termo de Olá tooby *redução dimensionalidade.* Métodos de seleção de funcionalidade extrair um subconjunto das funcionalidades originais nos dados de Olá sem alterá-los.  Métodos de redução dimensionalidade utilizam funcionalidades foi desenvolvidas que podem transformar funcionalidades original Olá e, por conseguinte, modificá-las. Exemplos de métodos de redução dimensionalidade incluem analysis componente principal, análise de correlação canónico e decomposição de valor único.

Categoria amplamente aplicada um dos métodos de seleção de funcionalidade num contexto supervisionado é a seleção de funcionalidades baseado no filtro. Através da avaliação de correlação de Olá entre cada atributo de destino funcionalidade e Olá, estes métodos, aplicam-se um tooassign medidas análises uma funcionalidade de tooeach de pontuação. Olá funcionalidades estão, em seguida, ordenadas pelo modelo de pontuação Olá, que pode utilizar o limiar de Olá tooset para manter os ou eliminando uma funcionalidade específica. Exemplos de medidas de análises de Olá utilizado nestes métodos incluem Pearson correlação, informações mútua e teste qui quadrado Olá.

Azure Machine Learning Studio fornece módulos para a seleção de funcionalidades. Conforme mostrado na figura a seguir de Olá, estes módulos incluem [filtro com base na seleção de funcionalidades] [ filter-based-feature-selection] e [Fisher Linear Discriminant Analysis] [ fisher-linear-discriminant-analysis].

![Exemplo de seleção de funcionalidade](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Por exemplo, utilizar Olá [filtro com base na seleção de funcionalidades] [ filter-based-feature-selection] módulo com o exemplo de extração de texto de Olá descrito anteriormente. Partem do princípio de que pretende que toobuild um modelo de regressão depois de um conjunto de 256 funcionalidades é criado através da Olá [funcionalidade hash] [ feature-hashing] módulo e essa variável de resposta de Olá é **Col1**e representa uma livro rever classificação vão de 1 too5. Definir **funcionalidade método de classificação** demasiado**Pearson correlação**, **coluna de destino** demasiado**Col1**, e **diversas pretendida funcionalidades** demasiado**50**. módulo Olá [filtro com base na seleção de funcionalidades] [ filter-based-feature-selection] , em seguida, produz um conjunto de dados que contém 50 funcionalidades juntamente com o atributo de destino Olá **Col1**. Olá apresentado a seguir figura mostra Olá fluxo desta fase experimental e Olá parâmetros de entrada.

![Exemplo de seleção de funcionalidade](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Olá figura seguinte mostra Olá resultante conjuntos de dados. Cada funcionalidade é classificada com base no Olá Pearson correlação entre si próprio e Olá atributo target **Col1**. funcionalidades de Olá com pontuações superiores são mantidas.

![Conjuntos de dados de seleção de funcionalidade com base em filtro](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

Olá mostra a figura a seguir Olá correspondentes pontuações das funcionalidades de Olá selecionado.

![Pontuações de funcionalidade selecionada](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Ao aplicar este [filtro com base na seleção de funcionalidades] [ filter-based-feature-selection] módulo, 50 fora de 256 funcionalidades estão selecionadas porque têm Olá maioria das funcionalidades correlacionadas com a variável de destino Olá **Col1** com base no método de classificação de Olá **Pearson correlação**.

## <a name="conclusion"></a>Conclusão
Engenharia da funcionalidade e a seleção de funcionalidades são dois passos efetuar frequentemente dados de formação tooprepare Olá quando criar um modelo de machine learning. Normalmente, engenharia da funcionalidade é aplicado primeiro toogenerate as funcionalidades adicionais e, em seguida, o passo de seleção de funcionalidade Olá é efetuada tooeliminate irrelevantes, redundante ou funcionalidades de elevada disponibilidade correlacionadas.

Não é sempre necessariamente tooperform de seleção de engenharia ou funcionalidade de funcionalidade. Indica se é necessária depende dados Olá tiver ou recolher algoritmo Olá que escolher, e Olá objetivo da experimentação Olá.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
