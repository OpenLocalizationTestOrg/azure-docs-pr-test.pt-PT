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
# <a name="use-hello-beeline-client-with-apache-hive"></a>Utilizar o cliente de Beeline Olá com Apache Hive

Saiba como toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) consulta toorun do Hive no HDInsight.

Beeline for um cliente de ramo de registo que está incluído em nós de head Olá do cluster do HDInsight. Beeline utiliza JDBC tooconnect tooHiveServer2, um serviço alojado num cluster do HDInsight. Também pode utilizar Beeline tooaccess do Hive no HDInsight remotamente mais Olá internet. Olá, a tabela seguinte fornece as cadeias de ligação para utilização com Beeline:

| Em que executou Beeline do | Parâmetros |
| --- | --- | --- |
| Um SSH ligação tooa headnode ou o Microsoft edge nó | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Cluster de Olá externa | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Substitua `admin` com a conta de início de sessão do cluster Olá para o cluster.
>
> Substitua `password` com Olá palavra-passe da conta de início de sessão do cluster Olá.
>
> Substitua `clustername` com o nome de Olá de cluster do HDInsight.

## <a id="prereq"></a>Pré-requisitos

* Um Hadoop baseado em Linux num cluster do HDInsight.

  > [!IMPORTANT]
  > Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

* Um cliente SSH ou cliente Beeline local. A maior parte dos passos de Olá neste documento partem do princípio de que está a utilizar Beeline de um cluster de toohello de sessão SSH. Para informações sobre como executar Beeline do cluster de Olá fora, consulte Olá [utilizar Beeline remotamente](#remote) secção.

    Para obter mais informações sobre como utilizar o SSH, consulte [utilizar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Utilizar Beeline

1. Ao iniciar Beeline, tem de fornecer uma cadeia de ligação de HiveServer2 no cluster do HDInsight. comando de Olá toorun do cluster de Olá externa, terá também de fornecer nome de conta de início de sessão de cluster Olá (predefinição `admin`) e palavra-passe. Utilize Olá tabela toofind Olá ligação cadeia formato e parâmetros toouse os seguintes:

    | Em que executou Beeline do | Parâmetros |
    | --- | --- | --- |
    | Um SSH ligação tooa headnode ou o Microsoft edge nó | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Cluster de Olá externa | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Por exemplo, Olá os seguintes comandos pode ser utilizado toostart Beeline de um cluster de toohello de sessão SSH:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    Este comando inicia o cliente de Beeline Olá e liga tooHiveServer2 no nó principal do cluster Olá. Após a conclusão do comando de Olá, chegam a um `jdbc:hive2://headnodehost:10001/>` linha.

2. Comandos de beeline começam com uma `!` caráter, por exemplo `!help` apresenta a ajuda. No entanto Olá `!` podem ser omitidas para alguns comandos. Por exemplo, `help` também funciona.

    Não existe um `!sql`, que é utilizado tooexecute declarações HiveQL. No entanto, HiveQL é por isso, normalmente utilizada que pode omitir Olá anterior `!sql`. Olá duas instruções a seguir é equivalente:

    ```hiveql
    !sql show tables;
    show tables;
    ```

    Num cluster novo, apenas uma tabela está listada: **hivesampletable**.

3. Utilize Olá esquema de Olá do comando toodisplay para Olá hivesampletable os seguintes:

    ```hiveql
    describe hivesampletable;
    ```

    Este comando devolve Olá seguintes informações:

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

    Estas informações descrevem Olá as colunas na tabela de Olá. Enquanto, pode efetuar algumas consultas contra estes dados, vamos em vez disso, crie uma nova toodemonstrate de tabela como dados de tooload no ramo e aplicar um esquema.

4. Introduza Olá seguir as instruções toocreate uma tabela com o nome **log4jLogs** utilizando dados de exemplo fornecidos com o cluster do HDInsight Olá:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Estas instruções execute Olá seguintes ações:

    * `DROP TABLE`-Se a tabela de Olá existe, é eliminado.

    * `CREATE EXTERNAL TABLE`-Cria um **externo** tabela do Hive. Tabelas externas apenas armazenam a definição da tabela Olá no ramo de registo. dados de Olá for deixados na localização original Olá.

    * `ROW FORMAT`-Como dados de Olá estão formatados. Neste caso, os campos de Olá em cada registo são separados por um espaço.

    * `STORED AS TEXTFILE LOCATION`-Onde Olá dados são armazenados e o formato de ficheiro.

    * `SELECT`-Seleciona uma contagem de todas as linhas onde coluna **t4** contém um valor Olá **[erro]**. Esta consulta devolve um valor **3** porque existem três linhas que contêm este valor.

    * `INPUT__FILE__NAME LIKE '%.log'`-Hive tenta tooapply Olá esquema tooall ficheiros Olá diretório. Neste caso, o diretório de Olá contém ficheiros que não corresponde ao esquema Olá. dados de libertação da memória tooprevent nos resultados de Olá, esta declaração de diz ao ramo de registo que iremos deverá devolver apenas dados de ficheiros que termina em. registo.

  > [!NOTE]
  > As tabelas externas devem ser utilizadas ao esperar Olá subjacente dados toobe atualizada por uma origem externa. Por exemplo, um processo de carregamento de dados automática ou uma operação de MapReduce.
  >
  > Remover uma tabela externa **não** eliminar dados de Olá, definição de tabela só Olá.

    Olá saída deste comando é semelhante toohello seguinte texto:

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

5. utilizar tooexit Beeline, `!exit`.

## <a id="file"></a>Utilizar Beeline toorun um ficheiro de HiveQL

Utilize Olá os seguintes passos toocreate um ficheiro, em seguida, execute-o utilizando Beeline.

1. Seguinte de Olá utilize comando toocreate um ficheiro denominado **query.hql**:

    ```bash
    nano query.hql
    ```

2. Utilize Olá seguir texto como o conteúdo de Olá do ficheiro de Olá. Esta consulta cria uma nova tabela 'interna' com o nome **foram**:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Estas instruções execute Olá seguintes ações:

    * **Criar tabela não se existe** -se a tabela de Olá ainda não existir, será criado. Desde Olá **externo** palavra-chave não é utilizada, esta instrução cria uma tabela interna. Tabelas internas são armazenadas no armazém de dados do Hive Olá e são geridas completamente pelo ramo de registo.
    * **ARMAZENADOS ORC de AS** -armazena os dados de Olá no formato otimizada linha Columnar (ORC). Formato ORC é um formato altamente otimizado e eficiente para armazenar dados do Hive.
    * **SUBSTITUIR INSERT... SELECIONE** -seleciona linhas Olá **log4jLogs** tabela que contém **[erro]**, em seguida, inserções Olá dados em Olá **foram** tabela.

    > [!NOTE]
    > Ao contrário das tabelas externas, remover uma tabela interna elimina dados subjacentes Olá bem.

3. ficheiro de Olá toosave, utilize **Ctrl**+**_X**, em seguida, introduza **Y**e, finalmente, **Enter**.

4. Utilize Olá seguintes toorun Olá ficheiro Beeline a utilizar:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Olá `-i` parâmetro inicia Beeline, executa Olá as instruções no ficheiro de query.hql Olá. Uma vez concluída a consulta de Olá, chegam Olá `jdbc:hive2://headnodehost:10001/>` linha. Também pode executar um ficheiro através de Olá `-f` parâmetro, que sai Beeline após a conclusão da consulta de Olá.

5. tooverify Olá **foram** tabela ter sido criada, utilize Olá seguir tooreturn instrução Olá todas as linhas da **foram**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    Três linhas de dados devem ser devolvidas, todos os contentora **[erro]** na coluna t4:

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Utilizar Beeline remotamente

Se tiver Beeline instalado localmente, ou estiver a utilizar através de uma imagem do Docker como [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), tem de utilizar Olá os seguintes parâmetros:

* __Cadeia de ligação__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __Nome de início de sessão do cluster__:`-n admin`

* __Palavra-passe de início de sessão do cluster__`-p 'password'`

Substitua Olá `clustername` na cadeia de ligação de Olá com o nome de Olá de cluster do HDInsight.

Substitua `admin` com o nome de Olá do início de sessão do cluster e substitua `password` com Olá palavra-passe para o início de sessão do cluster.

## <a id="sparksql"></a>Utilizar Beeline com o Spark

O Spark fornece a suas próprias implementação do HiveServer2, o que é muitas vezes de servidor do refered tooas Olá Thrift de Spark. Este serviço utiliza consultas do Spark SQL tooresolve em vez do Hive e pode fornecer um melhor desempenho, dependendo da sua consulta.

tooconnect toohello Thrift de Spark servidor um Spark no HDInsight cluster, utilize porta `10002` em vez de `10001`. Por exemplo, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> servidor de Thrift de Spark Olá é não diretamente acessível over Olá internet. Apenas pode ligar tooit a partir de uma sessão SSH ou dentro de Olá a mesma rede Virtual do Azure como Olá cluster do HDInsight.

## <a id="summary"></a><a id="nextsteps"></a>Passos seguintes

Para obter informações mais gerais sobre o Hive no HDInsight, consulte Olá seguintes documentos:

* [Utilizar o Hive com o Hadoop no HDInsight](hdinsight-use-hive.md)

Para obter mais informações sobre outras formas pode trabalhar com o Hadoop no HDInsight, consulte Olá seguintes documentos:

* [Utilizar o Pig com o Hadoop no HDInsight](hdinsight-use-pig.md)
* [Utilizar o MapReduce com o Hadoop no HDInsight](hdinsight-use-mapreduce.md)

Se estiver a utilizar com o Hive no Tez, consulte Olá seguintes documentos:

* [Utilizar Olá Tez IU no HDInsight baseado em Windows](hdinsight-debug-tez-ui.md)
* [Utilizar Olá vista Ambari Tez no HDInsight baseado em Linux](hdinsight-debug-ambari-tez-view.md)

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
