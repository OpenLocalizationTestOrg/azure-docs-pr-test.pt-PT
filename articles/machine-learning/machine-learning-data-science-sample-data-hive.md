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
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="9f51a-103">Dados de exemplo em tabelas do Hive do HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f51a-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="9f51a-104">Neste artigo, vamos descrever dados como toodown-sample armazenados nas tabelas do Hive do Azure HDInsight através de consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="9f51a-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="9f51a-105">Iremos abranger três métodos de amostragem popularmente utilizado:</span><span class="sxs-lookup"><span data-stu-id="9f51a-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="9f51a-106">Uniform amostragem aleatória</span><span class="sxs-lookup"><span data-stu-id="9f51a-106">Uniform random sampling</span></span>
* <span data-ttu-id="9f51a-107">Amostragem aleatória por grupos</span><span class="sxs-lookup"><span data-stu-id="9f51a-107">Random sampling by groups</span></span>
* <span data-ttu-id="9f51a-108">Amostragem stratified</span><span class="sxs-lookup"><span data-stu-id="9f51a-108">Stratified sampling</span></span>

<span data-ttu-id="9f51a-109">seguinte Olá **menu** liga tootopics que descrevem como toosample dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9f51a-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="9f51a-110">**Os dados de exemplo por que motivo?**</span><span class="sxs-lookup"><span data-stu-id="9f51a-110">**Why sample your data?**</span></span>
<span data-ttu-id="9f51a-111">Se o conjunto de dados de Olá planear tooanalyze for grande, é normalmente tooreduce de dados de exemplo toodown Olá uma boa ideia-tooa mais pequeno, mas representativo e mais fácil gerir o tamanho.</span><span class="sxs-lookup"><span data-stu-id="9f51a-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="9f51a-112">Isto facilita a compreensão de dados, exploração e engenharia da funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="9f51a-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="9f51a-113">A sua função na Olá o processo de ciência de dados de equipa é tooenable rápido fazer o protótipo de funções de processamento de dados de Olá e modelos de machine learning.</span><span class="sxs-lookup"><span data-stu-id="9f51a-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="9f51a-114">Esta tarefa de amostragem é um passo Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="9f51a-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="9f51a-115">Como consultas do Hive de toosubmit</span><span class="sxs-lookup"><span data-stu-id="9f51a-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="9f51a-116">Podem ser submetidas consultas do Hive a partir da consola de linha de comandos do Hadoop Olá no nó principal do Olá do cluster de Hadoop Olá.</span><span class="sxs-lookup"><span data-stu-id="9f51a-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="9f51a-117">toodo isto, iniciar sessão no nó principal do Olá de cluster de Hadoop Olá, abra Olá consola de linha de comandos do Hadoop e submeter consultas do Hive de Olá a partir daí.</span><span class="sxs-lookup"><span data-stu-id="9f51a-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="9f51a-118">Para obter instruções sobre como submeter consultas do Hive na consola de linha de comandos do Hadoop Olá, consulte [como tooSubmit consultas do Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="9f51a-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="9f51a-119"><a name="uniform"></a>Uniform amostragem aleatória</span><span class="sxs-lookup"><span data-stu-id="9f51a-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="9f51a-120">A amostragem aleatória Uniform significa que cada linha no conjunto de dados de Olá tem hipóteses de que está a ser objeto de amostragem.</span><span class="sxs-lookup"><span data-stu-id="9f51a-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="9f51a-121">Podem ser implementadas através da adição de um conjunto de dados do campo adicional rand() toohello na consulta do Olá interna "select" e na Olá consulta "select" externa, essa condição nesse campo aleatório.</span><span class="sxs-lookup"><span data-stu-id="9f51a-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="9f51a-122">Eis um exemplo de consulta:</span><span class="sxs-lookup"><span data-stu-id="9f51a-122">Here is an example query:</span></span>

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

<span data-ttu-id="9f51a-123">Aqui, `<sample rate, 0-1>` Especifica proporção Olá de registos que os utilizadores de Olá pretendem toosample.</span><span class="sxs-lookup"><span data-stu-id="9f51a-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="9f51a-124"><a name="group"></a>Amostragem aleatória por grupos</span><span class="sxs-lookup"><span data-stu-id="9f51a-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="9f51a-125">Quando dados categóricos de amostragem, poderá ser útil tooeither incluir ou excluir todas as instâncias de Olá de um valor específico de uma variável categórico.</span><span class="sxs-lookup"><span data-stu-id="9f51a-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="9f51a-126">Este é o que destina-se por "amostragem pelo grupo".</span><span class="sxs-lookup"><span data-stu-id="9f51a-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="9f51a-127">Por exemplo, se tiver uma categórico variável "State", que tem valores NY MA, AC, NJ, PA, etc., pretende que os registos de Olá mesmo Estado ser sempre em conjunto, se são amostragem ou não.</span><span class="sxs-lookup"><span data-stu-id="9f51a-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="9f51a-128">Eis um exemplo de consulta que amostras por grupo:</span><span class="sxs-lookup"><span data-stu-id="9f51a-128">Here is an example query that samples by group:</span></span>

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

## <span data-ttu-id="9f51a-129"><a name="stratified"></a>Amostragem stratified</span><span class="sxs-lookup"><span data-stu-id="9f51a-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="9f51a-130">Amostragem aleatória é stratified com relativamente tooa categórico variável quando amostras Olá obtidas têm valores que categórico que se encontrem no Olá rácio mesmo, tal como de que Olá amostras foram obtidas da população Olá principal.</span><span class="sxs-lookup"><span data-stu-id="9f51a-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="9f51a-131">Utilizar Olá mesmo exemplo, conforme apresentado acima, suponha que os seus dados têm populações secundárias por Estados, diga NJ tem as 100 observações, NY tem as 60 observações e WA tem as 300 observações.</span><span class="sxs-lookup"><span data-stu-id="9f51a-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="9f51a-132">Se especificar taxa Olá de stratified amostragem toobe 0,5, em seguida, hello exemplo obtido deve ter aproximadamente 50, 30 e as 150 observações de NJ, NY e WA, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="9f51a-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="9f51a-133">Eis um exemplo de consulta:</span><span class="sxs-lookup"><span data-stu-id="9f51a-133">Here is an example query:</span></span>

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


<span data-ttu-id="9f51a-134">Para obter informações sobre métodos de amostragem mais avançadas que estão disponíveis no ramo de registo, consulte [LanguageManual amostragem](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="9f51a-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

