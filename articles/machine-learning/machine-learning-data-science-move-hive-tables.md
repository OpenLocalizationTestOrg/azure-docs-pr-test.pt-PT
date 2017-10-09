---
title: aaaCreate tabelas de ramo de registo e carregar dados do Blob Storage do Azure | Microsoft Docs
description: Criar as tabelas do Hive e carregar os dados nas tabelas de toohive de blob
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Criar as tabelas do Hive e carregar dados do Blob Storage do Azure
Este tópico apresenta genéricas consultas do Hive que criar tabelas do Hive e carregar dados do blob storage do Azure. Algumas orientações também são fornecidas na criação de partições de tabelas do Hive e sobre como utilizar Olá otimizada linha Columnar (ORC) formatação tooimprove desempenho das consultas.

Isto **menu** liga tootopics que descrevem como dados tooingest em ambientes de destino onde os dados de Olá podem ser armazenados e processados durante Olá o processo de ciência de dados de equipa (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que tem:

* Criar uma conta de armazenamento do Azure. Se precisar de instruções, consulte [contas do storage do Azure sobre](../storage/common/storage-create-storage-account.md).
* Aprovisionar um cluster de Hadoop personalizado com Olá serviço HDInsight.  Se precisar de instruções, consulte [personalizar o Azure HDInsight Hadoop clusters para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).
* Cluster de toohello ativados de acesso remoto, tem sessão iniciada e abrir a consola da linha de comandos do Hadoop Olá. Se precisar de instruções, consulte [Olá acesso Head nó de Cluster do Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Carregar o armazenamento de BLOBs de tooAzure de dados
Se tiver criado uma máquina virtual do Azure ao seguir as instruções de Olá fornecidas [configurar uma máquina virtual do Azure para análise avançada](machine-learning-data-science-setup-virtual-machine.md), este ficheiro de script deve ter sido transferido toohello *c:\\ Os utilizadores\\\<nome de utilizador\>\\documentos\\Scripts de ciência de dados* diretório na máquina virtual de Olá. Estas consultas do Hive apenas requerem que ligue no seu próprio esquema de dados e a configuração de armazenamento de Blobs do Azure no Olá campos apropriados toobe pronto para submissão.

Partimos do princípio que Olá dados para as tabelas do Hive são num **descomprimidos** formato tabular, e que dados Olá foi carregadas toohello predefinida (ou tooan adicional) contentor Olá da conta de armazenamento utilizada pelo cluster de Hadoop Olá.

Se quiser toopractice no Olá **NYC Taxi viagem dados**, tem de:

* **Transferir** Olá 24 [NYC Taxi viagem dados](http://www.andresmh.com/nyctaxitrips) ficheiros (12 viagem e 12 Fare ficheiros),
* **deszipe** todos os ficheiros para os ficheiros. csv e, em seguida,
* **carregar** -los toohello predefinida (ou contentor adequado) de Olá conta do storage do Azure que foi criada pelo procedimento de Olá descrito em Olá [personalizar o Azure HDInsight Hadoop clusters para o processo de análise avançada e tecnologia ](machine-learning-data-science-customize-hadoop-cluster.md) tópico. Olá processo tooupload Olá. csv ficheiros toohello contentor predefinido da conta do storage Olá pode ser encontrado no [página](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>Como consultas do Hive de toosubmit
Consultas do Hive podem ser submetidas utilizando:

1. [Submeter consultas do Hive através da linha de comandos do Hadoop no headnode do cluster de Hadoop](#headnode)
2. [Submeter consultas do Hive com Olá Editor do Hive](#hive-editor)
3. [Submeter consultas do Hive com comandos do PowerShell do Azure](#ps)

Consultas do Hive são como o SQL Server. Se estiver familiarizado com o SQL Server, pode encontrar Olá [ramo de registo para a folha de Cheat utilizadores do SQL Server](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) útil.

Ao submeter uma consulta do Hive, também pode controlar o destino de Olá de saída de Olá de consultas do Hive, se este estar num Olá ecrã ou tooa ficheiro local no nó principal Olá ou tooan BLOBs do Azure.

### <a name="headnode"></a> 1. Submeter consultas do Hive através da linha de comandos do Hadoop no headnode do cluster de Hadoop
Se Olá Hive consulta é complexa, submetê-lo diretamente no nó principal do Olá do cluster de Hadoop Olá normalmente leva toofaster por sua vez em torno de submetê-lo com um Editor do Hive ou scripts do PowerShell do Azure.

Inicie sessão no nó principal do toohello do cluster de Hadoop Olá, abra Olá linha de comandos do Hadoop no ambiente de trabalho de Olá do nó principal Olá e introduza o comando `cd %hive_home%\bin`.

Tem três as consultas do Hive de toosubmit formas no Olá linha de comandos do Hadoop:

* diretamente
* utilizar .hql ficheiros
* com Olá consola comandos de ramo de registo

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Submeta consultas do Hive diretamente no Hadoop linha de comandos.
Pode executar o comando como `hive -e "<your hive query>;` toosubmit de consultas do Hive simples diretamente no Hadoop linha de comandos. Eis um exemplo, onde Olá comando que envia a consulta do Hive de Olá destaca de caixa de Olá vermelho e Olá caixa verde destaca Olá resultado da consulta de Hive Olá.

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Submeter consultas do Hive nos ficheiros de .hql
Quando a consulta do Hive de Olá é mais complicada e tem várias linhas, a edição de consultas na linha de comandos ou consola de comandos do ramo de registo não é prática. Uma alternativa é toouse um editor de texto no nó principal do Olá de Olá Hadoop cluster toosave Olá consultas do Hive num ficheiro .hql num diretório local do nó principal Olá. Em seguida, pode ser submetida a consulta do Hive de Olá no ficheiro de .hql Olá utilizando Olá `-f` argumento da seguinte forma:

    hive -f "<path toohello .hql file>"

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Suprimir a impressão de ecrã de estado de progresso de consultas do Hive**

Por predefinição, depois de consulta do Hive é submetida numa linha de comandos do Hadoop, progresso de Olá da tarefa de mapa/reduza Olá está impresso no ecrã. toosuppress Olá impressão de ecrã de progresso da tarefa mapa/reduza Olá, pode utilizar um argumento `-S` ("S" em maiúsculas) no Olá comando linha da seguinte forma:

    hive -S -f "<path toohello .hql file>"
.    ramo de registo -S -i "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Submeta consultas do Hive na consola de comandos do ramo de registo.
Primeiro também pode introduzir a consola de comandos do ramo de registo Olá executando o comando `hive` na linha de comandos do Hadoop e, em seguida, submeter consultas do Hive na consola de comandos do ramo de registo. Eis um exemplo. Neste exemplo, Olá duas caixas vermelho realce Olá comandos utilizados tooenter Olá consola de comandos do Hive e Olá consulta do Hive submeteu na consola de comandos do ramo de registo, respetivamente. caixa de Olá verde realça um resultado Olá de consulta do Hive de Olá.

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

exemplos anteriores Olá diretamente os resultados da consulta do Hive Olá no ecrã de saída. Também pode escrever Olá tooa local Ficheirodesaída no nó principal Olá ou tooan BLOBs do Azure. Em seguida, pode utilizar outras ferramentas toofurther analisar a saída de Olá de consultas do Hive.

**Saída do ficheiro local de tooa resultados de consulta do Hive.**
toooutput Hive consulta resultados tooa diretório local no nó principal Olá, que tem consulta de Hive toosubmit Olá Olá Hadoop linha de comandos da seguinte forma:

    hive -e "<hive query>" > <local path in hello head node>

No seguinte exemplo de Olá, saída Olá de consulta do Hive é escrita num ficheiro `hivequeryoutput.txt` no diretório `C:\apps\temp`.

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Saída tooan de resultados de consulta do Hive BLOBs do Azure**

Também pode apresentar Olá Hive consulta resultados tooan BLOBs do Azure, dentro do contentor predefinido de Olá do cluster de Hadoop Olá. consulta do Hive de Olá para este é o seguinte:

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

No seguinte exemplo de Olá, saída Olá de consulta do Hive é escrita diretório de blob tooa `queryoutputdir` dentro do contentor predefinido de Olá do cluster de Hadoop Olá. Aqui, basta nome do diretório Olá tooprovide, sem o nome do blob Olá. Emitido um erro se fornecer nomes de diretório e BLOBs, tais como `wasb:///queryoutputdir/queryoutput.txt`.

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Se abrir o contentor predefinido de Olá do cluster de Hadoop Olá através do Explorador de armazenamento do Azure, pode ver a saída de Olá da consulta do Hive de Olá conforme mostrado no Olá figura a seguir. Pode aplicar Olá filtro (realçado por caixa vermelha) tooonly obter Olá blob com especificado letras nos nomes.

![Criar a área de trabalho](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Submeter consultas do Hive com Olá Editor do Hive
Também pode utilizar Olá consulta consola (Editor do Hive) ao introduzir um URL de formulário Olá *https://&#60; Nome do cluster de Hadoop >.azurehdinsight.net/Home/HiveEditor* num browser. Tem de ser registadas no Olá consulte esta consola e, por isso, terá das credenciais de cluster do Hadoop.

### <a name="ps"></a> 3. Submeter consultas do Hive com comandos do PowerShell do Azure
Também pode utilizar consultas do PowerShell toosubmit do Hive. Para obter instruções, consulte [tarefas submeter o Hive com o PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Criar tabelas e a base de dados do Hive
Olá consultas do Hive são partilhadas no Olá [repositório do GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) , podendo ser transferido a partir daí.

Segue-se a consulta do Hive Olá que cria uma tabela do Hive.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Seguem-se Olá as descrições dos campos de Olá que precisa de tooplug no e outras configurações:

* **&#60; nome de base de dados >**: nome de Olá da base de dados de Olá que pretende que o toocreate. Se pretender apenas toouse Olá predefinido da base de dados, Olá consulta *criar base de dados...*  pode ser omitido.
* **&#60; nome da tabela >**: nome de Olá da tabela de Olá que pretende que o toocreate na base de dados especificada Olá. Se pretender que a base de dados predefinida de Olá toouse, tabela Olá pode ser diretamente referida pela *&#60; nome da tabela >* sem &#60; nome de base de dados >.
* **&#60; o separador de campo >**: separador de Olá delimits campos no toobe de ficheiro de dados de Olá carregado toohello tabela de Hive.
* **&#60; o separador de linha >**: separador de Olá delimits linhas no ficheiro de dados de Olá.
* **&#60; localização de armazenamento >**: Olá dados Olá de toosave de localização do armazenamento do Azure de tabelas do Hive. Se não especificar *localização &#60; localização de armazenamento >*, Olá da base de dados e hello tabelas são armazenadas no *hive/Armazém/* diretório no contentor predefinido de Olá do cluster de ramo de registo de Olá por predefinição. Se pretender que a localização de armazenamento toospecify Olá, a localização de armazenamento Olá tem toobe dentro do contentor predefinido de Olá para a base de dados de Olá e tabelas. Esta localização tem toobe que referida como contentor predefinido de toohello relativo de localização do cluster de Olá Olá no formato *' wasb: / / / &#60; diretório 1 > /'* ou *' wasb: / / / &#60; diretório 1 > / &#60; diretório 2 > /'*, etc. Após Olá consulta for executada, diretórios relativo Olá são criados dentro do contentor do Olá predefinido.
* **TBLPROPERTIES("Skip.Header.line.Count"="1")**: se o ficheiro de dados de Olá tem uma linha de cabeçalho, terá de tooadd esta propriedade **no fim de Olá** de Olá *criar tabela* consulta. Caso contrário, a linha de cabeçalho de Olá está carregada como uma tabela de registos toohello. Se o ficheiro de dados de Olá não tiver uma linha de cabeçalho, esta configuração pode ser omitida na consulta de Olá.

## <a name="load-data"></a>Carregar dados tooHive tabelas
Segue-se a consulta do Hive Olá que carrega dados para uma tabela do Hive.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; dados de tooblob caminho >**: esteja tabela do Hive de toohello toobe carregado Olá blob ficheiros no contentor predefinido Olá Olá cluster do HDInsight Hadoop, Olá *&#60; dados de tooblob caminho >* deve estar no formato de Olá *' wasb: / / / &#60; diretório neste contentor > / &#60; nome de ficheiro do blob >'*. ficheiro de blob Olá também pode ter um contentor adicional de Olá cluster do HDInsight Hadoop. Neste caso, *&#60; dados de tooblob caminho >* deve estar no formato de Olá *' wasb: / / &#60; nome do contentor > @&#60; nome da conta de armazenamento >.blob.core.windows.net/ &#60; nome de ficheiro do blob >'*.

  > [!NOTE]
  > Olá blob dados toobe carregado tooHive tabela tem toobe predefinido Olá ou contentor adicional Olá da conta de armazenamento para o cluster de Hadoop Olá. Caso contrário, Olá *carga dados* consulta falha complaining que não pode aceder a dados Olá.
  >
  >

## <a name="partition-orc"></a>Tópicos de avançadas: particionar a tabela e o arquivo de dados do Hive no formato ORC
Se os dados de Olá ficarem grandes, a criação de partições de tabela Olá é vantajoso para consultas que apenas necessitam tooscan alguns partições da tabela de Olá. Por exemplo, é toopartition razoável Olá registar dados de um web site por datas.

Na adição toopartitioning tabelas de ramo de registo, também é vantajoso toostore dados de ramo de registo de Olá no formato de otimizada linha Columnar (ORC) de Olá. Para obter mais informações sobre ORC formatação, consulte <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">ficheiros ORC utilizando melhora o desempenho ao ramo de registo é ler, escrever e processar dados</a>.

### <a name="partitioned-table"></a>Tabela particionada
Segue-se a consulta do Hive do Olá que cria uma tabela particionada e carrega dados para a mesma.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

Ao consultar tabelas particionadas, recomenda-se condição de partição de Olá tooadd no Olá **início** de Olá `where` cláusula deste melhora efficacy Olá de procura significativamente.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Armazenar dados do Hive no formato ORC
Diretamente não é possível carregar os dados a partir do blob storage para as tabelas do Hive, que é armazenado num formato ORC Olá. Seguem-se passos de Olá esse Olá que necessita para tootake tooload dados a partir do Azure blobs tabelas tooHive armazenadas num formato ORC.

Criar uma tabela externa **ARMAZENADOS TEXTFILE de AS** e carregar dados a partir da tabela de toohello de armazenamento de Blobs.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Criar uma tabela interna com Olá mesmo esquema como tabela externa de Olá no passo 1, com Olá mesmo o delimitador de campos e armazenar Olá ramo de registo de dados no formato ORC Olá.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

Selecione os dados da tabela externa de Olá no passo 1 e inserir na tabela ORC Olá

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Se tabela TEXTFILE Olá *&#60; nome de base de dados >. &#60; nome da tabela externa textfile >* tem partições, no passo 3, hello `SELECT * FROM <database name>.<external textfile table name>` comando seleciona Olá variável partição como um campo no Olá devolveu um conjunto de dados. Inserir-Olá *&#60; nome de base de dados >. &#60; nome da tabela ORC >* falhar desde *&#60; nome de base de dados >. &#60; nome da tabela ORC >* não tem a variável de partição Olá como um campo no esquema de tabela Olá. Neste caso, terá de toospecifically Olá selecione campos toobe inserido demasiado*&#60; nome de base de dados >. &#60; nome da tabela ORC >* da seguinte forma:
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

É seguro toodrop Olá *&#60; nome da tabela externa textfile >* quando utilizando a seguinte consulta depois de todos os dados de Olá foi inserida na *&#60; nome de base de dados >. &#60; nome da tabela ORC >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

Depois de seguir este procedimento, deve ter uma tabela com dados no Olá ORC formato pronto toouse.  
