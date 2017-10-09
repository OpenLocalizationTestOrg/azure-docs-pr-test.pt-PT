---
title: dados de aaaSample em tabelas do Azure HDInsight Hive | Microsoft Docs
description: Para baixo a amostragem de dados nas tabelas do Hive do Azure HDInsight (Hadopop)
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Dados de exemplo em tabelas do Hive do HDInsight
Neste artigo, vamos descrever dados como toodown-sample armazenados nas tabelas do Hive do Azure HDInsight através de consultas do Hive. Iremos abranger três métodos de amostragem popularmente utilizado:

* Uniform amostragem aleatória
* Amostragem aleatória por grupos
* Amostragem stratified

seguinte Olá **menu** liga tootopics que descrevem como toosample dados de vários ambientes de armazenamento.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Os dados de exemplo por que motivo?**
Se o conjunto de dados de Olá planear tooanalyze for grande, é normalmente tooreduce de dados de exemplo toodown Olá uma boa ideia-tooa mais pequeno, mas representativo e mais fácil gerir o tamanho. Isto facilita a compreensão de dados, exploração e engenharia da funcionalidade. A sua função na Olá o processo de ciência de dados de equipa é tooenable rápido fazer o protótipo de funções de processamento de dados de Olá e modelos de machine learning.

Esta tarefa de amostragem é um passo Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>Como consultas do Hive de toosubmit
Podem ser submetidas consultas do Hive a partir da consola de linha de comandos do Hadoop Olá no nó principal do Olá do cluster de Hadoop Olá. toodo isto, iniciar sessão no nó principal do Olá de cluster de Hadoop Olá, abra Olá consola de linha de comandos do Hadoop e submeter consultas do Hive de Olá a partir daí. Para obter instruções sobre como submeter consultas do Hive na consola de linha de comandos do Hadoop Olá, consulte [como tooSubmit consultas do Hive](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a>Uniform amostragem aleatória
A amostragem aleatória Uniform significa que cada linha no conjunto de dados de Olá tem hipóteses de que está a ser objeto de amostragem. Podem ser implementadas através da adição de um conjunto de dados do campo adicional rand() toohello na consulta do Olá interna "select" e na Olá consulta "select" externa, essa condição nesse campo aleatório.

Eis um exemplo de consulta:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

Aqui, `<sample rate, 0-1>` Especifica proporção Olá de registos que os utilizadores de Olá pretendem toosample.

## <a name="group"></a>Amostragem aleatória por grupos
Quando dados categóricos de amostragem, poderá ser útil tooeither incluir ou excluir todas as instâncias de Olá de um valor específico de uma variável categórico. Este é o que destina-se por "amostragem pelo grupo".
Por exemplo, se tiver uma categórico variável "State", que tem valores NY MA, AC, NJ, PA, etc., pretende que os registos de Olá mesmo Estado ser sempre em conjunto, se são amostragem ou não.

Eis um exemplo de consulta que amostras por grupo:

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a>Amostragem stratified
Amostragem aleatória é stratified com relativamente tooa categórico variável quando amostras Olá obtidas têm valores que categórico que se encontrem no Olá rácio mesmo, tal como de que Olá amostras foram obtidas da população Olá principal. Utilizar Olá mesmo exemplo, conforme apresentado acima, suponha que os seus dados têm populações secundárias por Estados, diga NJ tem as 100 observações, NY tem as 60 observações e WA tem as 300 observações. Se especificar taxa Olá de stratified amostragem toobe 0,5, em seguida, hello exemplo obtido deve ter aproximadamente 50, 30 e as 150 observações de NJ, NY e WA, respetivamente.

Eis um exemplo de consulta:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Para obter informações sobre métodos de amostragem mais avançadas que estão disponíveis no ramo de registo, consulte [LanguageManual amostragem](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).

