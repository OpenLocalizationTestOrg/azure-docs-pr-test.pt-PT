---
title: aaaUse Beeline com Apache Hive - Azure HDInsight | Microsoft Docs
description: "Saiba como toouse Olá Beeline cliente toorun Hive consulta com o Hadoop no HDInsight. Beeline é um utilitário para trabalhar com HiveServer2 através de JDBC."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: ramo de registo do beeline beeline de ramo de registo
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="78355-105">Utilizar o cliente de Beeline Olá com Apache Hive</span><span class="sxs-lookup"><span data-stu-id="78355-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="78355-106">Saiba como toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) consulta toorun do Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78355-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="78355-107">Beeline for um cliente de ramo de registo que está incluído em nós de head Olá do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78355-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="78355-108">Beeline utiliza JDBC tooconnect tooHiveServer2, um serviço alojado num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78355-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="78355-109">Também pode utilizar Beeline tooaccess do Hive no HDInsight remotamente mais Olá internet.</span><span class="sxs-lookup"><span data-stu-id="78355-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="78355-110">Olá, a tabela seguinte fornece as cadeias de ligação para utilização com Beeline:</span><span class="sxs-lookup"><span data-stu-id="78355-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="78355-111">Em que executou Beeline do</span><span class="sxs-lookup"><span data-stu-id="78355-111">Where you run Beeline from</span></span> | <span data-ttu-id="78355-112">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="78355-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="78355-113">Um SSH ligação tooa headnode ou o Microsoft edge nó</span><span class="sxs-lookup"><span data-stu-id="78355-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="78355-114">Cluster de Olá externa</span><span class="sxs-lookup"><span data-stu-id="78355-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="78355-115">Substitua `admin` com a conta de início de sessão do cluster Olá para o cluster.</span><span class="sxs-lookup"><span data-stu-id="78355-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="78355-116">Substitua `password` com Olá palavra-passe da conta de início de sessão do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="78355-117">Substitua `clustername` com o nome de Olá de cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78355-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="78355-118"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="78355-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="78355-119">Um Hadoop baseado em Linux num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78355-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="78355-120">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="78355-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="78355-121">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="78355-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="78355-122">Um cliente SSH ou cliente Beeline local.</span><span class="sxs-lookup"><span data-stu-id="78355-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="78355-123">A maior parte dos passos de Olá neste documento partem do princípio de que está a utilizar Beeline de um cluster de toohello de sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="78355-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="78355-124">Para informações sobre como executar Beeline do cluster de Olá fora, consulte Olá [utilizar Beeline remotamente](#remote) secção.</span><span class="sxs-lookup"><span data-stu-id="78355-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="78355-125">Para obter mais informações sobre como utilizar o SSH, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="78355-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="78355-126"><a id="beeline"></a>Utilizar Beeline</span><span class="sxs-lookup"><span data-stu-id="78355-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="78355-127">Ao iniciar Beeline, tem de fornecer uma cadeia de ligação de HiveServer2 no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78355-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="78355-128">comando de Olá toorun do cluster de Olá externa, terá também de fornecer nome de conta de início de sessão de cluster Olá (predefinição `admin`) e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="78355-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="78355-129">Utilize Olá tabela toofind Olá ligação cadeia formato e parâmetros toouse os seguintes:</span><span class="sxs-lookup"><span data-stu-id="78355-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="78355-130">Em que executou Beeline do</span><span class="sxs-lookup"><span data-stu-id="78355-130">Where you run Beeline from</span></span> | <span data-ttu-id="78355-131">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="78355-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="78355-132">Um SSH ligação tooa headnode ou o Microsoft edge nó</span><span class="sxs-lookup"><span data-stu-id="78355-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="78355-133">Cluster de Olá externa</span><span class="sxs-lookup"><span data-stu-id="78355-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="78355-134">Por exemplo, Olá os seguintes comandos pode ser utilizado toostart Beeline de um cluster de toohello de sessão SSH:</span><span class="sxs-lookup"><span data-stu-id="78355-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="78355-135">Este comando inicia o cliente de Beeline Olá e liga tooHiveServer2 no nó principal do cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="78355-136">Após a conclusão do comando de Olá, chegam a um `jdbc:hive2://headnodehost:10001/>` linha.</span><span class="sxs-lookup"><span data-stu-id="78355-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="78355-137">Comandos de beeline começam com uma `!` caráter, por exemplo `!help` apresenta a ajuda.</span><span class="sxs-lookup"><span data-stu-id="78355-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="78355-138">No entanto Olá `!` podem ser omitidas para alguns comandos.</span><span class="sxs-lookup"><span data-stu-id="78355-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="78355-139">Por exemplo, `help` também funciona.</span><span class="sxs-lookup"><span data-stu-id="78355-139">For example, `help` also works.</span></span>

    <span data-ttu-id="78355-140">Não existe um `!sql`, que é utilizado tooexecute declarações HiveQL.</span><span class="sxs-lookup"><span data-stu-id="78355-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="78355-141">No entanto, HiveQL é por isso, normalmente utilizada que pode omitir Olá anterior `!sql`.</span><span class="sxs-lookup"><span data-stu-id="78355-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="78355-142">Olá duas instruções a seguir é equivalente:</span><span class="sxs-lookup"><span data-stu-id="78355-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="78355-143">Num cluster novo, apenas uma tabela está listada: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="78355-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="78355-144">Utilize Olá esquema de Olá do comando toodisplay para Olá hivesampletable os seguintes:</span><span class="sxs-lookup"><span data-stu-id="78355-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="78355-145">Este comando devolve Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="78355-145">This command returns hello following information:</span></span>

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    <span data-ttu-id="78355-146">Estas informações descrevem Olá as colunas na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="78355-147">Enquanto, pode efetuar algumas consultas contra estes dados, vamos em vez disso, crie uma nova toodemonstrate de tabela como dados de tooload no ramo e aplicar um esquema.</span><span class="sxs-lookup"><span data-stu-id="78355-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="78355-148">Introduza Olá seguir as instruções toocreate uma tabela com o nome **log4jLogs** utilizando dados de exemplo fornecidos com o cluster do HDInsight Olá:</span><span class="sxs-lookup"><span data-stu-id="78355-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="78355-149">Estas instruções execute Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="78355-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="78355-150">`DROP TABLE`-Se a tabela de Olá existe, é eliminado.</span><span class="sxs-lookup"><span data-stu-id="78355-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="78355-151">`CREATE EXTERNAL TABLE`-Cria um **externo** tabela do Hive.</span><span class="sxs-lookup"><span data-stu-id="78355-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="78355-152">Tabelas externas apenas armazenam a definição da tabela Olá no ramo de registo.</span><span class="sxs-lookup"><span data-stu-id="78355-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="78355-153">dados de Olá for deixados na localização original Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="78355-154">`ROW FORMAT`-Como dados de Olá estão formatados.</span><span class="sxs-lookup"><span data-stu-id="78355-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="78355-155">Neste caso, os campos de Olá em cada registo são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="78355-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="78355-156">`STORED AS TEXTFILE LOCATION`-Onde Olá dados são armazenados e o formato de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="78355-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="78355-157">`SELECT`-Seleciona uma contagem de todas as linhas onde coluna **t4** contém um valor Olá **[erro]**.</span><span class="sxs-lookup"><span data-stu-id="78355-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="78355-158">Esta consulta devolve um valor **3** porque existem três linhas que contêm este valor.</span><span class="sxs-lookup"><span data-stu-id="78355-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="78355-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive tenta tooapply Olá esquema tooall ficheiros Olá diretório.</span><span class="sxs-lookup"><span data-stu-id="78355-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="78355-160">Neste caso, o diretório de Olá contém ficheiros que não corresponde ao esquema Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="78355-161">dados de libertação da memória tooprevent nos resultados de Olá, esta declaração de diz ao ramo de registo que iremos deverá devolver apenas dados de ficheiros que termina em. registo.</span><span class="sxs-lookup"><span data-stu-id="78355-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="78355-162">As tabelas externas devem ser utilizadas ao esperar Olá subjacente dados toobe atualizada por uma origem externa.</span><span class="sxs-lookup"><span data-stu-id="78355-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="78355-163">Por exemplo, um processo de carregamento de dados automática ou uma operação de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="78355-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="78355-164">Remover uma tabela externa **não** eliminar dados de Olá, definição de tabela só Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="78355-165">Olá saída deste comando é semelhante toohello seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="78355-165">hello output of this command is similar toohello following text:</span></span>

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. <span data-ttu-id="78355-166">utilizar tooexit Beeline, `!exit`.</span><span class="sxs-lookup"><span data-stu-id="78355-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="78355-167"><a id="file"></a>Utilizar Beeline toorun um ficheiro de HiveQL</span><span class="sxs-lookup"><span data-stu-id="78355-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="78355-168">Utilize Olá os seguintes passos toocreate um ficheiro, em seguida, execute-o utilizando Beeline.</span><span class="sxs-lookup"><span data-stu-id="78355-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="78355-169">Seguinte de Olá utilize comando toocreate um ficheiro denominado **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="78355-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="78355-170">Utilize Olá seguir texto como o conteúdo de Olá do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="78355-171">Esta consulta cria uma nova tabela 'interna' com o nome **foram**:</span><span class="sxs-lookup"><span data-stu-id="78355-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="78355-172">Estas instruções execute Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="78355-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="78355-173">**Criar tabela não se existe** -se a tabela de Olá ainda não existir, será criado.</span><span class="sxs-lookup"><span data-stu-id="78355-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="78355-174">Desde Olá **externo** palavra-chave não é utilizada, esta instrução cria uma tabela interna.</span><span class="sxs-lookup"><span data-stu-id="78355-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="78355-175">Tabelas internas são armazenadas no armazém de dados do Hive Olá e são geridas completamente pelo ramo de registo.</span><span class="sxs-lookup"><span data-stu-id="78355-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="78355-176">**ARMAZENADOS ORC de AS** -armazena os dados de Olá no formato otimizada linha Columnar (ORC).</span><span class="sxs-lookup"><span data-stu-id="78355-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="78355-177">Formato ORC é um formato altamente otimizado e eficiente para armazenar dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="78355-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="78355-178">**SUBSTITUIR INSERT... SELECIONE** -seleciona linhas Olá **log4jLogs** tabela que contém **[erro]**, em seguida, inserções Olá dados em Olá **foram** tabela.</span><span class="sxs-lookup"><span data-stu-id="78355-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="78355-179">Ao contrário das tabelas externas, remover uma tabela interna elimina dados subjacentes Olá bem.</span><span class="sxs-lookup"><span data-stu-id="78355-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="78355-180">ficheiro de Olá toosave, utilize **Ctrl**+**_X**, em seguida, introduza **Y**e, finalmente, **Enter**.</span><span class="sxs-lookup"><span data-stu-id="78355-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="78355-181">Utilize Olá seguintes toorun Olá ficheiro Beeline a utilizar:</span><span class="sxs-lookup"><span data-stu-id="78355-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="78355-182">Olá `-i` parâmetro inicia Beeline, executa Olá as instruções no ficheiro de query.hql Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="78355-183">Uma vez concluída a consulta de Olá, chegam Olá `jdbc:hive2://headnodehost:10001/>` linha.</span><span class="sxs-lookup"><span data-stu-id="78355-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="78355-184">Também pode executar um ficheiro através de Olá `-f` parâmetro, que sai Beeline após a conclusão da consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="78355-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="78355-185">tooverify Olá **foram** tabela ter sido criada, utilize Olá seguir tooreturn instrução Olá todas as linhas da **foram**:</span><span class="sxs-lookup"><span data-stu-id="78355-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="78355-186">Três linhas de dados devem ser devolvidas, todos os contentora **[erro]** na coluna t4:</span><span class="sxs-lookup"><span data-stu-id="78355-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="78355-187"><a id="remote"></a>Utilizar Beeline remotamente</span><span class="sxs-lookup"><span data-stu-id="78355-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="78355-188">Se tiver Beeline instalado localmente, ou estiver a utilizar através de uma imagem do Docker como [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), tem de utilizar Olá os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="78355-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="78355-189">__Cadeia de ligação__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="78355-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="78355-190">__Nome de início de sessão do cluster__:`-n admin`</span><span class="sxs-lookup"><span data-stu-id="78355-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="78355-191">__Palavra-passe de início de sessão do cluster__`-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="78355-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="78355-192">Substitua Olá `clustername` na cadeia de ligação de Olá com o nome de Olá de cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78355-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="78355-193">Substitua `admin` com o nome de Olá do início de sessão do cluster e substitua `password` com Olá palavra-passe para o início de sessão do cluster.</span><span class="sxs-lookup"><span data-stu-id="78355-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="78355-194"><a id="sparksql"></a>Utilizar Beeline com o Spark</span><span class="sxs-lookup"><span data-stu-id="78355-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="78355-195">O Spark fornece a suas próprias implementação do HiveServer2, o que é muitas vezes de servidor do refered tooas Olá Thrift de Spark.</span><span class="sxs-lookup"><span data-stu-id="78355-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="78355-196">Este serviço utiliza consultas do Spark SQL tooresolve em vez do Hive e pode fornecer um melhor desempenho, dependendo da sua consulta.</span><span class="sxs-lookup"><span data-stu-id="78355-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="78355-197">tooconnect toohello Thrift de Spark servidor um Spark no HDInsight cluster, utilize porta `10002` em vez de `10001`.</span><span class="sxs-lookup"><span data-stu-id="78355-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="78355-198">Por exemplo, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="78355-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78355-199">servidor de Thrift de Spark Olá é não diretamente acessível over Olá internet.</span><span class="sxs-lookup"><span data-stu-id="78355-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="78355-200">Apenas pode ligar tooit a partir de uma sessão SSH ou dentro de Olá a mesma rede Virtual do Azure como Olá cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78355-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="78355-201"><a id="summary"></a><a id="nextsteps"></a>Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="78355-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="78355-202">Para obter informações mais gerais sobre o Hive no HDInsight, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="78355-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="78355-203">Utilizar o Hive com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="78355-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="78355-204">Para obter mais informações sobre outras formas pode trabalhar com o Hadoop no HDInsight, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="78355-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="78355-205">Utilizar o Pig com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="78355-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="78355-206">Utilizar o MapReduce com o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="78355-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="78355-207">Se estiver a utilizar com o Hive no Tez, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="78355-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="78355-208">Utilizar Olá Tez IU no HDInsight baseado em Windows</span><span class="sxs-lookup"><span data-stu-id="78355-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="78355-209">Utilizar Olá vista Ambari Tez no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="78355-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
