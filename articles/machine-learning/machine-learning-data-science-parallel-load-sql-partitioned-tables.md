---
title: "aaaBuild e otimizar as tabelas para rápido paralela importação de dados para um SQL Server numa VM do Azure | Microsoft Docs"
description: "Importação de Dados em Massa e em Paralelo com Tabelas de Partição de SQL"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Importação de Dados em Massa e em Paralelo com Tabelas de Partição de SQL
Este documento descreve como toobuild particionada tabelas para importar o rápido paralela em massa de dados tooa do SQL Server da base de dados. Para macrodados carregamento/transferência tooa SQL da base de dados, pode ser melhorada importar dados toohello BD SQL e consultas subsequentes utilizando *particionada tabelas e vistas*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Criar uma nova base de dados e um conjunto de grupos de ficheiros
* [Criar uma nova base de dados](https://technet.microsoft.com/library/ms176061.aspx), se não existir já.
* Adicione grupos de ficheiros toohello base de dados que vai conter ficheiros físicos Olá particionada. Isto pode ser feito com [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) se a nova ou [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) se a base de dados de Olá já existe.
* Adicione um ou mais ficheiros (conforme necessário) tooeach da base de dados grupo de ficheiros.
  
  > [!NOTE]
  > Especifique o grupo de ficheiros do destino Olá que contém dados para este nomes de ficheiro de base de dados física de partição e olá onde serão armazenados os dados do grupo de ficheiros de Olá.
  > 
  > 

Olá exemplo seguinte cria uma nova base de dados com três grupos de ficheiros que não sejam Olá primário e de grupos de registos, que contém um ficheiro físico em cada um. ficheiros de base de dados de Olá são criados na pasta de dados do SQL Server predefinida de Olá, conforme configurado na instância do SQL Server Olá. Para obter mais informações sobre localizações de ficheiros predefinidos Olá, consulte [localizações de ficheiros para a predefinição e com o nome de instâncias do SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a>Criar uma tabela particionada
Crie tabelas particionadas toohello esquema de dados, toohello mapeada da base de dados os grupos de ficheiros criadas no passo anterior Olá de acordo com. Quando os dados em massa importada toohello particionada tabelas, os registos serão distribuídos entre grupos de ficheiros de Olá em conformidade com o esquema de partição tooa, conforme descrito abaixo.

**toocreate uma tabela de partições, tem de:**

* [Criar uma função de partição](https://msdn.microsoft.com/library/ms187802.aspx) que define o intervalo de Olá de valores/limites toobe incluídos na tabela cada partição individual, por exemplo, partições toolimit por mês (alguns\_datetime\_campo) no ano de Olá 2013:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Criar um esquema de partição](https://msdn.microsoft.com/library/ms179854.aspx) que mapeia cada intervalo de partição Olá partição função tooa físico grupo de ficheiros, por ex.:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  intervalos de Olá tooverify em vigor em cada partição de acordo com esquema/função toohello, executar Olá seguinte consulta:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Criar tabela particionada](https://msdn.microsoft.com/library/ms174979.aspx)(s) de acordo com o esquema de dados de tooyour e especificar o campo de esquema e restrição de partição de Olá utilizado toopartition tabela de Olá, por exemplo:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Para obter mais informações, consulte [índices e criar tabelas Particionadas](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Dados de Olá importação em volume para cada tabela de partição individual
* É possível utilizar BCP, inserção em massa ou outros métodos, tais como [Assistente de migração do SQL Server](http://sqlazuremw.codeplex.com/). exemplo de Olá fornecido utiliza o método BCP Olá.
* [Alterar a base de dados de Olá](https://msdn.microsoft.com/library/bb522682.aspx) registo esquema tooBULK_LOGGED toominimize custos, por exemplo, o registo de transações de toochange:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* dados tooexpedite carregar, inicie operações de importação em massa Olá em paralelo. Para dicas sobre expediting em massa importar de macrodados para bases de dados do SQL Server, consulte o artigo [carregar 1TB no inferior a 1 hora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Olá seguinte script do PowerShell é um exemplo dos dados paralelos carregar com o BCP.

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Criar índices toooptimize associações e desempenho das consultas
* Se será extrair dados para a modelação de várias tabelas, crie índices sobre as chaves de associação de Olá desempenho de associação de Olá tooimprove.
* [Criar índices](https://technet.microsoft.com/library/ms188783.aspx) (em cluster ou não em cluster) filtragem hello mesmo grupo de ficheiros para cada partição, para por ex.:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  ou,
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > Pode optar por toocreate índices Olá antes em massa importar dados de Olá. Criação de índices antes de importar em massa irá retardar do carregamento de dados de Olá.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Processo de análise avançada e tecnologia de exemplo de ação
Para obter um exemplo de instruções ponto a ponto com Olá Cortana processo de análise de um conjunto de dados público, consulte [Cortana o processo de análise em ação: utilizar o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

