---
title: "funcionalidades de aaaCreate para dados de um cluster de Hadoop através de consultas do Hive | Microsoft Docs"
description: Exemplos de consultas do Hive que geram funcionalidades em dados armazenados no cluster Azure HDInsight Hadoop.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Criar características para dados num cluster do Hadoop com consultas do Hive
Este documento mostra como as funcionalidades de toocreate para dados armazenados no cluster Azure HDInsight Hadoop através de consultas do Hive. Estas consultas do Hive utilizam incorporados do Hive funções definidas pelo utilizador (UDFs), scripts de Olá para os quais são fornecidas.

Olá operações necessárias toocreate funcionalidades podem ser consomem muita memória. desempenho de Olá de consultas do Hive se torne mais crítico nestes casos e pode ser melhorado determinados parâmetros de otimização. Olá otimização destes parâmetros mencionado na secção final Olá.

Exemplos de consultas de Olá que são apresentadas são toohello específico [NYC Taxi viagem dados](http://chriswhong.com/open-data/foil_nyc_taxi/) cenários também são fornecidos no [repositório do GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Estas consultas já tiver o esquema de dados especificado e estão pronto toobe submetido toorun. Na secção final Olá, os parâmetros que os utilizadores podem otimizar para que Olá o desempenho de consultas do Hive pode ser melhorado também são debatidos.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Isto **menu** liga tootopics que descrevem como toocreate funcionalidades para os dados em vários ambientes. Esta tarefa é um passo Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que tem:

* Criar uma conta de armazenamento do Azure. Se precisar de instruções, consulte [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Aprovisionar um cluster de Hadoop personalizado com Olá serviço HDInsight.  Se precisar de instruções, consulte [personalizar Azure HDInsight Clusters do Hadoop para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).
* dados de Olá foi carregado tooHive tabelas do Azure HDInsight Hadoop clusters. Se não tiver, siga [criar e carga tabelas de tooHive dados](machine-learning-data-science-move-hive-tables.md) tooupload dados tooHive tabelas pela primeira vez.
* Cluster de toohello de acesso remoto ativado. Se precisar de instruções, consulte [Olá acesso Head nó de Cluster do Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Geração de funcionalidade
Nesta secção são descritos vários exemplos de formas de Olá na qual podem gerar funcionalidades através de consultas do Hive. Depois de ter gerado funcionalidades adicionais, pode adicioná-los como tabela do colunas toohello existente ou criar uma nova tabela com funcionalidades adicionais Olá e a chave primária, o que, em seguida, pode ser associado com a tabela original Olá. Seguem-se exemplos de Olá apresentados:

1. [Frequência baseada geração de funcionalidade](#hive-frequencyfeature)
2. [Riscos de variáveis Categórico na classificação binária](#hive-riskfeature)
3. [Extrair as funcionalidades do campo Datetime](#hive-datefeatures)
4. [Extrair as funcionalidades do campo de texto](#hive-textfeatures)
5. [Calcular a distância entre GPS coordenadas](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>Frequência baseada geração de funcionalidade
É frequentemente frequências de Olá toocalculate útil de níveis de Olá de uma variável categórico ou frequências de Olá de determinados combinações de níveis de várias variáveis categórico. Os utilizadores podem utilizar Olá toocalculate de script a seguir estes frequências:

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>Riscos de variáveis Categórico na classificação binária
Na classificação binária, precisamos variáveis de categórico tooconvert não numéricos em funcionalidades numérico quando os modelos de Olá a ser utilizados apenas o funcionalidades numérico. Isto é feito ao substituir a cada nível de não sejam numéricos por um risco de um valor numérico. Nesta secção, mostramos algumas consultas do Hive genéricas que calcular valores de risco Olá (registo odds) de uma variável categórico.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

Neste exemplo, as variáveis `smooth_param1` e `smooth_param2` são conjunto toosmooth Olá risco valores calculados a partir dos dados de Olá. Riscos tem um intervalo entre -Inf e Inf. A riscos > 0 indica se a probabilidade de Olá que o destino Olá é igual too1 é superior a 0,5.

Depois de tabela de risco Olá é calculada, os utilizadores podem atribuir a tabela de tooa de valores de risco ao associá-lo com a tabela de risco Olá. a consulta de associação do Hive do Olá foi fornecida na secção anterior.

### <a name="hive-datefeatures"></a>Extrair as funcionalidades dos campos Datetime
Ramo de registo é fornecido com um conjunto de UDFs para processar os campos datetime. No ramo de registo, o formato de datetime Olá predefinido é ' aaaa-MM-dd 00:00:00 ' ('1970-01-01-12:21:32 ' por exemplo). Nesta secção, mostramos exemplos que extrair o dia de Olá de um mês, o mês Olá de um campo datetime e outros exemplos para converter uma cadeia de datetime num formato que cadeia do Olá predefinida formato tooa datetime predefinidas no formato.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

Esta consulta do Hive assume que Olá *&#60; campo datetime >* está no formato datetime, Olá predefinido.

Se um campo datetime não se encontra no formato predefinido das Olá, terá de campo de datetime tooconvert Olá para o carimbo de hora Unix primeiro e, em seguida, converter Olá Unix carimbo tooa datetime de cadeia que ocorre na predefinição Olá formato. Quando Olá datetime predefinidas no formato, os utilizadores podem aplicar Olá incorporado datetime UDFs tooextract funcionalidades.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

Esta consulta, se hello *&#60; campo datetime >* tem padrão Olá como *26/03/2015 04:12:39*, Olá *' &#60; padrão do campo de datetime Olá >'* deve ser `'MM/dd/yyyy HH:mm:ss'`. tootest, os utilizadores podem executar

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Olá *hivesampletable* nesta consulta vem pré-instalada em todos os clusters do Hadoop do Azure HDInsight por predefinição quando clusters Olá são aprovisionados.

### <a name="hive-textfeatures"></a>Extrair as funcionalidades de campos de texto
Quando a tabela de Hive Olá tem um campo de texto que contém uma cadeia de palavras são delimitados por espaços, hello seguinte consulta extrai o comprimento da cadeia de Olá e o número de Olá de palavras na cadeia de Olá Olá.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>Calcular as distâncias entre conjuntos de coordenadas GPS
consulta de Olá indicada nesta secção pode ser aplicado diretamente toohello NYC Taxi viagem dados. objetivo Olá esta consulta é tooshow como tooapply um embedded matemática funções no ramo de registo toogenerate funcionalidades.

Olá campos que são utilizados nesta consulta são coordenadas GPS Olá das localizações de recolha e dropoff, com o nome *recolha\_longitude*, *recolha\_latitude*,  *dropoff\_longitude*, e *dropoff\_latitude*. as consultas de Olá calcular distância direta de Olá entre coordenadas de recolha e dropoff Olá são:

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

as equações matemática Olá que calcular distância Olá entre duas coordenadas GPS podem ser encontradas no Olá <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Movable tipo Scripts</a> site, criada por Peter Lapisu. No seu Javascript, Olá função `toRad()` é apenas *lat_or_lon*pi/180 *, que converte tooradians graus. Aqui, *lat_or_lon* latitude Olá ou longitude. Uma vez que o ramo de registo não fornece a função de Olá `atan2`, mas fornece a função de Olá `atan`, Olá `atan2` função é implementada por `atan` funcionar em Olá acima consulta do Hive com a definição de Olá fornecida <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.

![Criar a área de trabalho](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Uma lista completa de ramo de registo UDFs incorporados podem ser encontrados na Olá **funções incorporadas** secção em Olá <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).  

## <a name="tuning"></a>Tópicos de avançadas: parâmetros de ramo de registo de otimizar tooImprove velocidade de consulta
Olá parâmetro predefinido definições do cluster de ramo de registo poderão não ser adequadas para consultas do Hive de Olá e os dados de Olá que consultas Olá são de processamento. Nesta secção, vamos discutir alguns parâmetros que os utilizadores podem otimizar que melhoram o desempenho de Olá de consultas do Hive. Os utilizadores precisam de parâmetro de Olá tooadd otimização consultas antes de consultas de Olá de processamento de dados.

1. **Espaço de área dinâmica para dados de Java**: para consultas que envolvem grandes conjuntos de dados de associação ou processar registos longos, **a ficar sem espaço de pilha** é um erro comum Olá. Isto pode ser otimizado ao definir os parâmetros *mapreduce.map.java.opts* e *mapreduce.task.io.sort.mb* toodesired valores. Segue-se um exemplo:
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Este parâmetro atribui 4GB de memória tooJava área dinâmica para dados espaço e também facilita a ordenação mais eficiente ao alocar mais memória para o mesmo. É um tooplay boa ideia com estas alocações se existir qualquer tarefa falha erros relacionados tooheap espaço.

1. **Tamanho do bloco de DFS** : este parâmetro define a unidade de menor Olá dos dados Olá arquivos de sistema de ficheiros. Por exemplo, se Olá DFS o tamanho do bloco é de 128MB, em seguida, quaisquer dados de tamanho inferior e cópia de segurança too128MB são armazenados num único bloco, enquanto os dados que são maiores do que 128MB é atribuído blocos adicionais. Escolher um tamanho de bloco muito pequenos faz com que grandes sobrecargas no Hadoop, uma vez que o nó de nome de Olá tem tooprocess muitos mais pedidos toofind Olá relevantes bloco relativas toohello ficheiro. Uma definição recomendada quando lidar com gigabytes (ou superior) os dados são:
   
        set dfs.block.size=128m;
2. **Otimizar a operação de associação no ramo** : enquanto as operações de associação a estrutura de mapa/reduzir Olá ocorrer normalmente no Olá reduzir fase, por vezes, podem ser conseguidos ganhos bastantes agendando associações na fase de mapa de Olá (também denominada "mapjoins"). toodirect Hive toodo isto sempre que possível, iremos pode definir:
   
        set hive.auto.convert.join=true;
3. **Especificar o número de Olá de mappers tooHive** : Hadoop enquanto permite Olá utilizador tooset Olá diversas reducers, número de Olá de mappers é, geralmente, não estar definido pelo utilizador Olá. Um truque que permite que algumas grau de controlo deste número é variáveis de Hadoop toochoose Olá *mapred.min.split.size* e *mapred.max.split.size* como tamanho Olá de mapa de cada tarefa é determinada por:
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    Olá, normalmente, o valor predefinido de *mapred.min.split.size* for 0, de *mapred.max.split.size* é **Long.MAX** e *dfs.block.size* é 64MB. Como é possível ver, tamanho de dados indicado Olá, otimização estes parâmetros por "definição"-las nos permite tootune Olá diversas mappers utilizado.
4. Outros mais alguns **opções avançadas** para otimizar o ramo de registo desempenho são mencionados abaixo. Estas permitem-lhe tooset Olá memória alocada toomap reduzir as tarefas e podem ser útil para ajustar o desempenho. . Tenha em atenção que Olá *mapreduce.reduce.memory.mb* não pode ser superior ao tamanho da memória física Olá de cada nó de trabalho no cluster de Hadoop do Olá.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

