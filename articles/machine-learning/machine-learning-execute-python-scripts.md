---
title: aaaExecute Python scripts do machine learning | Microsoft Docs
description: "Destaca subjacente suporte para scripts Python no Azure Machine Learning e cenários de utilização básica, capacidades e limitações de princípios de design."
keywords: machine learning, pandas, pandas de python, python scripts, Python executar scripts do python
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Executar scripts de machine learning em Python no Azure Machine Learning Studio

Este tópico descreve os princípios de conceção de Olá subjacente Olá suportar para scripts Python no Azure Machine Learning. capacidades principais Olá fornecidas também descritas, incluindo:

- cenários de utilização básica de execução
- uma experimentação de pontuação num serviço web
- suporte para importar o código existente
- visualizações de exportação
- efetuar a seleção de funcionalidades supervisionado
- compreender algumas limitações

[Python](https://www.python.org/) é uma ferramenta indispensable no chest de ferramenta Olá de muitos cientistas de dados. Tem de:

* uma sintaxe elegante e concisa, 
* suporte em várias plataformas, 
* uma coleção de bibliotecas de elevado desempenho, vasta e 
* ferramentas de desenvolvimento madura. 

Python está a ser utilizado em todas as fases de um fluxo de trabalho normalmente utilizadas nas modelação do machine learning:

- ingestão de dados e processamento 
- construção de funcionalidade
- modelo de formação 
- validação do modelo
- implementação de modelos de Olá

Azure Machine Learning Studio suporta scripts do Python incorporar em várias partes de uma máquina experimentação de aprendizagem e também perfeitamente publicando-os como serviços web no Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>Princípios de conceção de scripts Python no Machine Learning

Olá interface primária tooPython no Azure Machine Learning Studio é através de Olá [executar Script de Python] [ execute-python-script] módulo mostrado na figura 1.

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

Figura 1. Olá **executar Script de Python** módulo.

Olá [executar Script de Python] [ execute-python-script] módulo no Azure ML Studio aceita segurança toothree entradas e produz segurança saídas tootwo (abordadas na Olá secção a seguir), como o respetivo analogue R, hello [ Executar Script do R] [ execute-r-script] módulo. Olá toobe de código do Python executado é introduzido na caixa de parâmetro de Olá especial nomeado como ponto de entrada função chamada `azureml_main`. Seguem-se a estrutura chave Olá princípios utilizado tooimplement este módulo:

1. *Tem de ser idiomatic para utilizadores do Python.* A maioria dos utilizadores de Python fator respetivo código como funções dentro de módulos. Por isso, colocar uma grande quantidade de instruções executável de um módulo de nível superior é relativamente raro. Como resultado, caixa de script de Olá também aceita uma função de Python especial nomeada como toojust oposição a uma sequência de instruções. Olá objetos expostos na função Olá são tipos de biblioteca padrão do Python, tais como [Pandas](http://pandas.pydata.org/) pacotes de dados e [NumPy](http://www.numpy.org/) matrizes.
2. *Tem de ter alta-fidelidade, entre locais e execuções de nuvem.* Olá back-end utilizado tooexecute Olá código Python baseia-se no [Anaconda](https://store.continuum.io/cshop/anaconda/), um amplamente utilizado distribuição do Python científicos várias plataformas. Inclui too200 fechar de pacotes de Python Olá mais comuns. Por conseguinte, os cientistas de dados podem depurar e qualificar o respetivo código no seu ambiente do Azure Machine Learning compatível Anaconda local. Em seguida, utilizar um ambiente de desenvolvimento existente, tal como [IPython](http://ipython.org/) bloco de notas ou [ferramentas do Python para Visual Studio](http://aka.ms/ptvs), toorun como parte de uma experimentação do Azure ML. Olá `azureml_main` ponto de entrada é uma função de Python clássica e por isso *** podem ser criadas sem código do Azure ML específico ou Olá SDK instalado.
3. *Tem de ser totalmente integrada composta com outros módulos do Azure Machine Learning.* Olá [executar Script de Python] [ execute-python-script] módulo aceita, como entradas e saídas, conjuntos de dados do Azure Machine Learning padrão. estrutura subjacente Olá transparente e eficiente pontes tempos de execução de Olá, Azure ML e Python. Por isso, o Python pode ser utilizado em conjunto com existentes do Azure ML fluxos de trabalho, incluindo os que chamam para o R e SQLite. Consequentemente, scientist de dados foi compor fluxos de trabalho que:
   * utilizar o Python e Pandas para dados pré-processadas e limpeza
   * Olá feed tooa SQL transformação de dados, associar várias funcionalidades de tooform de conjuntos de dados
   * modelos de formação utilizando algoritmos Olá no Azure Machine Learning 
   * avaliar e pós-cópia processar os resultados de Olá utilizando R.


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>Cenários de utilização básica no ML de scripts do Python

Nesta secção, iremos encontrar algumas das utilizações de básico Olá da Olá [executar Script de Python] [ execute-python-script] módulo. Módulo de Python toohello entradas são expostos como frames Jumbo Pandas dados. Olá função tem de devolver um intervalo de dados único Pandas empacotado dentro de um Python [sequência](https://docs.python.org/2/c-api/sequence.html) como uma cadeia de identificação, lista ou NumPy matriz. primeiro elemento de Olá desta sequência, em seguida, é devolvido em Olá primeiro à porta de saída do módulo Olá. Este esquema é mostrada na figura 2.

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

Figura 2. Mapeamento de portas de entrada tooparameters e devolver valor toooutput porta.

Mais detalhadas semântica de como portas de entrada Olá obtêm tooparameters mapeado de Olá `azureml_main` função são apresentadas na tabela 1:

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

Tabela 1. Mapeamento de parâmetros de toofunction de portas de entrada.

mapeamento de Olá entre as portas de entrada e de parâmetros de função é posicional:

- porta de entrada ligado primeiro Olá é mapeada toohello primeiro parâmetro da função de Olá. 
- segunda entrada Olá (se ligado) é mapeada toohello segundo parâmetro da função de Olá.

Consulte *Python para análise de dados* (O'Reilly, 2012) da McKinney para obter mais informações no Python Pandas e como pode ser utilizado toomanipulate dados eficaz e eficiente. 


## <a name="translation-of-input-and-output-types"></a>Conversão de tipos de entrada e de saída 
Conjuntos de dados de entrada no Azure ML são frames Jumbo toodata convertida em Pandas. Pacotes de dados de saída são convertidos conjuntos de dados de back-tooAzure ML. Olá conversões a seguir é efetuada:

1. Colunas de cadeia e numérica são convertidas como-é e os valores em falta num conjunto de dados são too'NA convertida ' valores Pandas. Olá conversão mesmo acontece em Olá forma novamente (valores NA Pandas são valores de toomissing convertida no Azure ML).
2. Os vetores de índice Pandas não são suportados no Azure ML. Todos os pacotes de dados de entrada na função de Python Olá sempre dispor de um índice numérico de 64 bits do 0 toohello número de linhas menos 1. 
3. Conjuntos de dados de ML do Azure não podem ter nomes de colunas duplicados e nomes de colunas que não são cadeias. Se um intervalo de dados de saída contém colunas não numéricos, Olá framework chamadas `str` nos nomes das colunas de Olá. Da mesma forma, os nomes de colunas duplicados são automaticamente mangled tooinsure Olá nomes são exclusivos. sufixo Olá (2) está adicionado duplicado primeiro toohello, (3) duplicado segundo toohello e assim sucessivamente.


## <a name="operationalizing-python-scripts"></a>Operacionalizar Python scripts

Qualquer [executar Script de Python] [ execute-python-script] módulos utilizados na experimentação de classificação são denominados quando publicado como um serviço web. Por exemplo, a figura 3 mostra uma experimentação de classificação que contém o código de Olá tooevaluate uma única expressão de Python. 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

Figura 3. Serviço Web para avaliação de uma expressão de Python.

Um serviço web criado a partir desta fase experimental:

- demora como entrada uma expressão de Python (como uma cadeia)
- envia-toohello interpretador de Python 
- Devolve uma tabela que contém a expressão de Olá e resultado Olá avaliada.


## <a name="importing-existing-python-script-modules"></a>Importar os módulos de script de Python existentes

Um caso de utilização comuns para muitos cientistas de dados é tooincorporate Python os scripts existentes para experimentações do Azure ML. Em vez de exigir que todo o código ser concatenado e colar na caixa de um script único, Olá [executar Script de Python] [ execute-python-script] módulo aceita um ficheiro zip que contém os módulos do Python na porta de entrada terceiro Olá. ficheiro de Olá é deszipado pela estrutura de execução de Olá no tempo de execução e conteúdo Olá é adicionado toohello o caminho de biblioteca do interpretador Python de Olá. Olá `azureml_main` função pode, em seguida, importar estes módulos diretamente o ponto de entrada.

Por exemplo, considere ficheiro Olá Hello.py que contém uma função de "Olá, mundo" simple.

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

Figura 4. Função definida pelo utilizador no ficheiro Hello.py.

Em seguida, vamos criar um ficheiro Hello.zip contém Hello.py:

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

Figura 5. Ficheiro zip que contém o código de Python definido pelo utilizador.

Carregue o ficheiro zip Olá como um conjunto de dados para o Azure Machine Learning Studio. Em seguida, criar e executar uma experimentação que utiliza o código de Python Olá no ficheiro de Hello.zip Olá através da porta entrada terceira toohello de Olá a ligá-la **executar Script de Python** módulo, conforme mostrado na figura que.

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

Figura 6. Experimentação de exemplo com o código de Python definido pelo utilizador carregado como um ficheiro zip.

saída de módulo Olá mostra que o ficheiro zip Olá foi descompactado e essa função Olá `print_hello` tiver sido executado.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

A figura 7. A função definida pelo utilizador em utilização no interior Olá [executar Script de Python] [ execute-python-script] módulo.


## <a name="working-with-visualizations"></a>Trabalhar com visualizações

Plots criadas utilizando MatplotLib que pode ser visualizado no browser Olá podem ser devolvidos por Olá [executar Script de Python][execute-python-script]. Mas Olá rastreia não é automaticamente redirecionada tooimages conforme forem ao utilizar o R. Para que o utilizador Olá tem de os guardar explicitamente qualquer rastreia tooPNG ficheiros que se encontrem toobe devolveu tooAzure back-Machine Learning. 

imagens de toogenerate de MatplotLib, tem de concluir Olá seguinte procedimento:

* mudar de back-end de Olá demasiado "AGG" de Olá predefinido com base em Qt compositor 
* criar um novo objeto de figura 
* obter o eixo Olá e gerar rastreia todos os para a mesma 
* Guardar Olá figura tooa PNG ficheiro 

Este processo é ilustrado no Olá figura 8, que cria uma matriz de desenho de gráfico de dispersão utilizando a função de scatter_matrix Olá no Pandas a seguir.

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

Figura 8. O código de toosave MatplotLib figuras tooimages.

A figura 9 mostra uma experimentação que utiliza o script de Olá apresentado anteriormente tooreturn rastreia através de porta de saída segundo Olá.

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

Figura 9. Visualizar rastreia gerado a partir do código Python.

É tooreturn possíveis figuras vários ao guardá-las imagens diferentes, hello do Azure Machine Learning em tempo de execução escolherá todas as imagens e concatena-los para visualização.


## <a name="advanced-examples"></a>Exemplos avançados

ambiente de Anaconda Olá instalado no Azure Machine Learning contém pacotes comuns, tais como NumPy, SciPy e saber o Scikits. Estes pacotes podem ser efetivamente utilizados para várias tarefas de processamento de dados num de machine learning pipeline. Por exemplo, hello seguinte experimentação e script ilustram utilização Olá learners ensemble em mais de Scikits toocompute funcionalidade importância pontuações das classificações para um conjunto de dados. pontuações Olá podem ser utilizados tooperform supervisionado a seleção de funcionalidades antes de a ser sejam fornecidas outro modelo de ML.

Eis Olá Python função utilizada toocompute Olá importância pontuações e funcionalidades de Olá de ordem com base no pontuações Olá:

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

A figura 10. Função toorank as funcionalidades de por pontuações.
 Olá experimentação seguinte, em seguida, calcula e devolve pontuações de importância Olá das funcionalidades no conjunto de dados do Olá "Pima britânico Diabetes" no Azure Machine Learning:

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

Figura 11. Funcionalidades de toorank de experimentação no conjunto de dados do Olá Pima britânico Diabetes.

## <a name="limitations"></a>Limitações
Olá [executar Script de Python] [ execute-python-script] tem atualmente Olá seguintes limitações:

1. *Uma execução.* runtime do Python Olá está atualmente uma e, consequentemente, não permitir acesso toohello toohello ou de rede local sistema de ficheiros de forma persistente. Todos os ficheiros guardados localmente são isolados e eliminados depois de concluir o módulo Olá. Olá código Python não é possível aceder a maioria dos diretórios no computador de Olá que é executada no, a exceção de Olá Olá diretório atual e nos seus subdiretórios.
2. *Falta de desenvolvimento sofisticado e suporte de depuração.* módulo de Python Olá não suporta atualmente funcionalidades IDE como intellisense e a depuração. Além disso, se o módulo Olá falha no tempo de execução, hello rastreio da pilha Python completo está disponível. Mas tem de ser visualizado no registo de saída de Olá para o módulo Olá. Recomendamos atualmente desenvolver e depurar scripts Python num ambiente, tais como IPython e, em seguida, importar o código de Olá para o módulo Olá.
3. *Saída de moldura de dados individual.* ponto de entrada do Python Olá é apenas permitido tooreturn um intervalo de dados individual como saída. Não é possível atualmente tooreturn que Python arbitrário objetos, tais como modelos de formação diretamente fazer uma cópia de tempo de execução do toohello Azure Machine Learning. Como [executar Script do R][execute-r-script], que tem Olá mesma limitação, é possível em muitos casos toopickle objetos para um byte matriz e, em seguida, devolvem que dentro de um intervalo de dados.
4. *Incapacidade toocustomize instalação Python*. Atualmente, hello apenas forma tooadd Python nos módulos personalizados é através do mecanismo de ficheiro zip do Olá descrito anteriormente. Apesar de ser exequível para módulos pequenos, é complexa para módulos grande (especialmente dos com DLLs nativas) ou um grande número de módulos. 

## <a name="conclusions"></a>Conclusões
Olá [executar Script de Python] [ execute-python-script] módulo permite um scientist dados tooincorporate código de Python existente para fluxos de trabalho do alojado na nuvem machine learning no Azure Machine Learning e tooseamlessly operacionalize-los como parte de um serviço web. módulo de script de Python Olá interoperates naturalmente com outros módulos no Azure Machine Learning. módulo Olá pode ser utilizado para um intervalo de tarefas de exploração toopre-o processamento de dados e a extração da funcionalidade e, em seguida, tooevaluation e pós-processamento de resultados de Olá. tempo de execução do back-end Olá utilizado para execução baseia Anaconda, uma distribuição do Python bem testada e amplamente utilizada. Este back-end torna simples para si ativos de código existente tooon quadro numa nuvem Olá.

Esperamos tooprovide funcionalidades adicionais toohello [executar Script de Python] [ execute-python-script] módulo, tal como Olá tootrain de capacidade e operacionalizar modelos no Python e tooadd melhor suporte para Olá desenvolvimento e depuração do código no Azure Machine Learning Studio.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte Olá [Centro para programadores do Python](https://azure.microsoft.com/develop/python/).

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
