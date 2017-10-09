---
title: dados de aaaImport no Machine Learning Studio | Microsoft Docs
description: "Como tooimport os dados no Azure Machine Learning Studio de várias origens de dados. Saiba que tipos de dados e formatos de dados são suportados."
keywords: "Importar dados, o formato de dados, os tipos de dados, as origens de dados, dados de formação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Importar os seus dados de preparação para o Azure Machine Learning Studio a partir de várias origens de dados
toouse os seus próprios dados no Machine Learning Studio toodevelop e formação uma solução de Análise Preditiva, pode: 

* carregar dados a partir de um **ficheiro local** ahead de tempo da sua toocreate de disco rígido, um módulo de conjunto de dados na sua área de trabalho
* aceder a dados a partir de um dos vários **origens de dados online** enquanto está a executar a experimentação utilizando Olá [importar dados] [ import-data] módulo 
* utilizar dados a partir de outro Azure Machine learning **experimentação** guardada como um conjunto de dados
* utilizar dados a partir de um local **base de dados do SQL Server**

Cada uma destas opções é descrita dos tópicos de Olá no menu de Olá abaixo. Estes tópicos mostram-lhe como tooimport dados a partir destes dados de várias origens toouse no Machine Learning Studio. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Um número de conjuntos de dados de exemplo estão disponíveis no Machine Learning Studio, pode utilizar para dados de preparação. Para obter informações acerca deste assunto, consulte [utilizar conjuntos de dados de exemplo de Olá no Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).
> 
> 

Este tópico introdutórias também descreve como dados tooget prontos a utilizam no Machine Learning Studio e descreve os formatos de dados e os tipos de dados são suportados. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Obter dados pronto a utilizar no Azure Machine Learning Studio
Machine Learning Studio é concebida toowork com dados retangular ou tabela, tais como os dados de texto delimitado por ou estruturados dados a partir de uma base de dados, embora em algumas circunstâncias não retangular dados podem ser utilizados.

É melhor se os seus dados são relativamente limpo. Ou seja, poderá ser útil tootake care of problemas como cadeias unquoted antes de carregar dados de Olá na sua experiência.

No entanto, existem módulos disponíveis no Machine Learning Studio, que permitem algumas manipulação de dados dentro da sua experimentação. Dependendo de algoritmos de aprendizagem Olá que irá utilizar, poderá ser necessário toodecide como vai processar problemas estruturais de dados, como os valores em falta e dados dispersos e existem módulos que podem ajudar. Procure no Olá **transformação de dados** secção da paleta do módulo Olá para módulos que realizam estas funções.

Em qualquer momento na sua experimentação pode ver ou transferir dados Olá que são produzidos por um módulo clicando Olá porta de saída. Dependendo do módulo Olá, poderá transferir diferentes opções disponíveis ou pode estar toovisualize capaz de dados de Olá dentro do seu browser no Machine Learning Studio.

## <a name="data-formats-and-data-types-supported"></a>Tipos de dados e formatos de dados suportados
Pode importar um número de tipos de dados para a sua experimentação, consoante o mecanismo de utilizar dados tooimport e onde é proveniente de:

* Texto simples (*.txt)
* Valores separados por vírgulas (CSV) com um cabeçalho (. csv) ou sem (. nh.csv)
* Separador valores separados por (TSV) com um cabeçalho (.tsv) ou sem (. nh.tsv)
* Ficheiro do Excel
* Tabela do Azure
* Tabela do Hive
* Tabela de base de dados SQL
* Valores de OData
* Dados SVMLight (.svmlight) (consulte Olá [SVMLight definição](http://svmlight.joachims.org/) para obter informações de formato)
* Atributo de dados de formato de ficheiro de relação (ARFF) (.arff) (consulte Olá [definição ARFF](http://weka.wikispaces.com/ARFF) para obter informações de formato)
* Ficheiro zip (. zip)
* Ficheiro de objeto ou a área de trabalho de R (. RData)

Se importar dados num formato como ARFF inclui metadados, o Machine Learning Studio utiliza este cabeçalho de Olá toodefine de metadados e o tipo de dados de cada coluna.

Se importar dados, tais como TSV ou CSV com o formato que não inclua estes metadados, o Machine Learning Studio infere Olá o tipo de dados para cada coluna por dados Olá de amostragem. Se os dados de Olá também não tem cabeçalhos de coluna, o Machine Learning Studio fornece nomes predefinidos.

Pode especificar explicitamente ou alterar tipos de cabeçalhos e dados de Olá para colunas utilizando Olá [Editar metadados][edit-metadata].

seguinte Olá **tipos de dados** são reconhecidos pelo Machine Learning Studio:

* Cadeia
* Número inteiro
* duplo
* Valor booleano
* DateTime
* TimeSpan

O Machine Learning Studio utiliza um tipo de dados internos chamado ***dados tabela*** toopass dados entre módulos. Explicitamente pode converter os dados em formato de tabela de dados utilizando Olá [converter tooDataset] [ convert-to-dataset] módulo.

Qualquer módulo que aceita os formatos que não seja a tabela de dados irá converter Olá dados tooData tabela silenciosamente antes de transmitir módulo seguinte toohello.

Se necessário, pode converter a tabela de dados formato no CSV, TSV, ARFF, ou SVMLight utilizando outros módulos de conversão.
Procure no Olá **conversões de formato de dados** secção da paleta do módulo Olá para módulos que realizam estas funções.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
