---
title: "Olá o processo de ciência de dados de equipa em ação: utilizar o SQL Data Warehouse | Microsoft Docs"
description: "Processo de análise avançada e tecnologia em ação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>Olá o processo de ciência de dados de equipa em ação: utilizar o SQL Data Warehouse
Neste tutorial, iremos guiá-lo através de criar e implementar um modelo de machine learning utilizar o SQL Data Warehouse (armazém de dados do SQL Server) para um conjunto de dados publicamente disponível – hello [NYC Taxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados. modelo de classificação binária Olá construído prevê ou não uma sugestão é paga para uma viagem e modelos para classificação de várias classes e regressão também são abordados que prever distribuição Olá para quantidades de sugestão de Olá pagas.

procedimento Olá segue Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) fluxo de trabalho. Vamos mostrar como toosetup num ambiente de ciência de dados, como tooload Olá dados no armazém de dados do SQL Server e como utilizar o armazém de dados do SQL Server ou um Olá de tooexplore IPython bloco de notas em dados e engenheiro a toomodel funcionalidades. Em seguida, mostramos como toobuild e implementar um modelo com o Azure Machine Learning.

## <a name="dataset"></a>o conjunto de dados do Olá NYC Taxi viagens
Olá dados NYC Taxi viagem consiste em cerca de 20GB de ficheiros CSV comprimidos (GB de ~ 48 descomprimido), mais de 173 milhões de gravação viagens individuais e Olá fares paga para cada viagem. Cada registo viagem inclui localizações de recolha e drop-off Olá e vezes, são anónimos hack número de licença (controlador) e Olá número medallion (id exclusivo do taxi). dados Olá abrange todos os viagens no ano de Olá 2013 e são fornecidos na Olá seguir dois conjuntos de dados de cada mês:

1. Olá **trip_data.csv** ficheiro contém detalhes viagem, tais como o número de passageiros, recolha e dropoff pontos, duração de viagem e comprimento viagem. Seguem-se alguns registos de exemplo:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Olá **trip_fare.csv** ficheiro contém detalhes de fare Olá paga para cada viagem, tais como o tipo de pagamento, a quantidade de fare, surcharge e taxas, sugestões e tolls e quantidade total de Olá paga. Seguem-se alguns registos de exemplo:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Olá **chave exclusiva** utilizado toojoin viagem\_dados e viagem\_fare é composto por Olá seguintes três campos:

* Medallion,
* Hack\_licença e
* recolha\_datetime.

## <a name="mltasks"></a>Três tipos de tarefas de predição de endereços
Iremos formular três problemas de predição com base no Olá *sugestão\_quantidade* tooillustrate três tipos de modelação tarefas:

1. **Classificação binária**: toopredict ou não em que uma sugestão foi paga ou seja, para uma viagem, um *sugestão\_quantidade* que é superior ao $0 é um exemplo positivo, enquanto um *sugestão\_quantidade* $ 0 é um exemplo negativo.
2. **Classificação de várias classes**: intervalo de Olá toopredict de sugestão paga para viagem Olá. Iremos dividir Olá *sugestão\_quantidade* em cinco intervalos binários ou classes:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Tarefa de regressão**: quantidade de Olá toopredict de sugestão paga para uma viagem.  

## <a name="setup"></a>Configurar o ambiente de ciência de dados do Azure Olá para análise avançada
tooset configurar o ambiente de ciência de dados do Azure, siga estes passos.

**Criar a sua própria conta de armazenamento de Blobs do Azure**

* Quando aprovisionar o seu próprio armazenamento de Blobs do Azure, escolha uma localização de georreplicação para o armazenamento de Blobs do Azure em ou mais parecida possível demasiado**Sul Central nos**, que é onde está armazenada Olá dados NYC Taxi. Olá dados serão copiados utilizando o AzCopy do contentor de tooa de contentor de armazenamento de BLOBs público de Olá na sua própria conta do storage. Olá próximo do armazenamento de Blobs do Azure é EUA Central tooSouth, hello mais rapidamente esta tarefa (passo 4) será concluída.
* toocreate o seus próprios storage do Azure da conta, Olá siga os passos descritos em [contas do storage do Azure sobre](../storage/common/storage-create-storage-account.md). Ser se toomake notas sobre Olá os valores para as credenciais da conta de armazenamento seguintes, irá ser necessário posteriormente nestas instruções.
  
  * **Nome da conta de armazenamento**
  * **Chave de conta de armazenamento**
  * **Nome do contentor** (que quiser Olá toobe de dados armazenado no blob storage do Azure de Olá)

**Aprovisione a instância de armazém de dados do Azure SQL.**
Siga a documentação de Olá em [criar um SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision uma instância do SQL Data Warehouse. Certifique-se de que efetua notações no Olá seguir as credenciais do SQL Data Warehouse que serão utilizadas em passos posteriores.

* **Nome do servidor**: <server Name>. database.windows.net
* **Nome SQLDW (base de dados)**
* **Nome de Utilizador**
* **Palavra-passe**

**Instale Visual Studio e ferramentas de dados do SQL Server.** Para obter instruções, consulte [instalar o Visual Studio 2015 e/ou o SSDT (SQL Server Data Tools) para o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).

**Ligar tooyour armazém de dados do Azure SQL com o Visual Studio.** Para obter instruções, consulte os passos 1 e 2 no [ligar tooAzure SQL Data Warehouse com o Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).

> [!NOTE]
> Execute hello seguinte consulta SQL na base de dados de Olá que criou no SQL Data Warehouse (em vez de consulta Olá fornecida no passo 3 do Olá ligar tópico,) demasiado**criar uma chave mestra**.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Crie uma área de trabalho do Azure Machine Learning na sua subscrição do Azure.** Para obter instruções, consulte [criar uma área de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).

## <a name="getdata"></a>Carregar dados de Olá para o SQL Data Warehouse
Abra uma consola de comandos do Windows PowerShell. Execute o seguinte de Olá comandos do PowerShell toodownload Olá exemplo SQL ficheiros de script que partilhamos no GitHub tooa diretório local que especificou com o parâmetro Olá *- DestDir*. Pode alterar Olá valor do parâmetro *- DestDir* tooany de diretório local. Se *- DestDir* não existir, será criado pelo Olá script do PowerShell.

> [!NOTE]
> Poderá ser necessário demasiado**executar como administrador** ao executar Olá seguinte script do PowerShell se o *DestDir* directory precisar tooit de toocreate ou toowrite de privilégios de administrador.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

Após a execução com êxito, o atual diretório de trabalho alterado demasiado*- DestDir*. Deve ser capaz de ecrã de toosee como abaixo:

![][19]

No seu *- DestDir*, executar Olá seguinte script do PowerShell no modo de administrador:

    ./SQLDW_Data_Import.ps1

Quando executa Olá script do PowerShell para Olá pela primeira vez, será pedido informações de Olá tooinput do seu armazém de dados de SQL do Azure e a sua conta de armazenamento de Blobs do Azure. Quando tiver concluído este script do PowerShell em execução para Olá a primeira vez, credenciais de Olá entrada será escrita o ficheiro de configuração de tooa SQLDW.conf no diretório de trabalho presente Olá. Olá executar futura deste ficheiro de script do PowerShell tem Olá opção tooread necessárias de todos os parâmetros deste ficheiro de configuração. Se precisar de toochange alguns parâmetros, pode escolher tooinput parâmetros Olá no ecrã de Olá após a linha ao eliminar este ficheiro de configuração e inputting valores de parâmetros de Olá, conforme solicitado ou valores de parâmetros de Olá toochange editando Olá SQLDW.conf ficheiro no seu *- DestDir* diretório.

> [!NOTE]
> Na ordem tooavoid esquema nome entra em conflito com as que já existem no armazém de dados do SQL do Azure, quando a ler parâmetros diretamente a partir do ficheiro de SQLDW.conf Olá, 3 dígitos aleatório é adicionado um número toohello nome de esquema do ficheiro de SQLDW.conf Olá como nome de esquema predefinido Olá para cada execução. Olá script do PowerShell pode solicitar-lhe um nome de esquema: pode ser especificado o nome de Olá critério de utilizador.
> 
> 

Isto **script do PowerShell** ficheiro conclui Olá seguintes tarefas:

* **Transfere e instala o AzCopy**, se o AzCopy já não está instalado
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **Copia a conta de armazenamento de BLOBs privada de tooyour dados** a partir do blob público de Olá com AzCopy
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Carrega dados utilizando o Polybase (executando LoadDataToSQLDW.sql) tooyour armazém de dados do Azure SQL** da sua conta de armazenamento de BLOBs privada com Olá os seguintes comandos.
  
  * Criar um esquema
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * Criar uma credencial com âmbito de base de dados
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Criar uma origem de dados externo para um blob de armazenamento do Azure
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * Crie um formato de ficheiro externo para um ficheiro csv. Os dados são descomprimidos e os campos são separados com caráter de pipe Olá.
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * Crie tabelas de viagem para o conjunto de dados do NYC taxi e fare externo no armazenamento de Blobs do Azure.
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - Carregar dados das tabelas externas no armazenamento de Blobs do Azure tooSQL do armazém de dados

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - Criar uma tabela de dados de exemplo (NYCTaxi_Sample) e inserir dados tooit de selecionar as consultas SQL em tabelas de viagem e fare Olá. (Alguns passos destas instruções necessita toouse nesta tabela de exemplo.)

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

localização geográfica de Olá das suas contas de armazenamento afeta tempos de carregamento.

> [!NOTE]
> Consoante Olá localização geográfica da conta de armazenamento de BLOBs privada, o processo de Olá de cópia de dados de uma conta de armazenamento privada do blob público tooyour pode demorar cerca de 15 minutos ou processar o mesmo já e hello de carregamento dos dados da sua conta de armazenamento tooyour armazém de dados do Azure SQL, pode demorar de 20 minutos ou mais.  
> 
> 

Tem de toodecide o que fazer se tiver origem duplicada e ficheiros de destino.

> [!NOTE]
> Se toobe ficheiros. csv de Olá copiado a partir da conta de armazenamento de BLOBs privada armazenamento tooyour Olá blob público já existir na sua conta de armazenamento de BLOBs privada, AzCopy irá pedir-lhe se pretende toooverwrite-los. Se não pretender toooverwrite-las, entrada  **n**  quando lhe for pedido. Se quiser toooverwrite **todos os** dos mesmos, de entrada **um** quando lhe for pedido. Também pode introduzir **y** . csv de toooverwrite ficheiros individualmente.
> 
> 

![Desenhar #21][21]

Pode utilizar os seus próprios dados. Se os dados na sua máquina no local na sua aplicação de vida real, pode continuar a utilizar AzCopy tooupload no local dados tooyour privada blob storage do Azure. Só precisa de toochange Olá **origem** localização, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, no Olá comandos do AzCopy de Olá PowerShell script toohello local diretório do ficheiro que contenha os dados.

> [!TIP]
> Se os dados já existir no seu armazenamento de Blobs do Azure privada na sua aplicação de vida real, pode ignorar Olá AzCopy passo na Olá script do PowerShell e o carregar diretamente Olá dados tooAzure armazém de dados do SQL Server. Isto irá necessitar adicionais edita de Olá script tootailor-toohello formato dos seus dados.
> 
> 

Este script do Powershell plugs também no Olá informações do armazém de dados do Azure SQL Olá exploração exemplo para ficheiros de dados SQLDW_Explorations.sql, SQLDW_Explorations.ipynb e SQLDW_Explorations_Scripts.py para que estes três ficheiros estejam toobe pronto tentou instantaneamente após a conclusão da Olá script do PowerShell.

Após uma execução bem sucedida, verá o ecrã, conforme mostrado abaixo:

![][20]

## <a name="dbexplore"></a>Exploração de dados e de engenharia da funcionalidade no Azure SQL Data Warehouse
Nesta secção, iremos executar geração de exploração e funcionalidade de dados através da execução de consultas SQL no armazém de dados do SQL do Azure diretamente utilizando **ferramentas de dados do Visual Studio**. Todas as consultas de SQL Server utilizadas nesta secção podem ser encontradas no script de exemplo de Olá denominado *SQLDW_Explorations.sql*. Este ficheiro já foi transferido tooyour diretório local pelo script de PowerShell Olá. Também pode obter a [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql). Mas ficheiro Olá no GitHub, não dispõe de informações do armazém de dados do Azure SQL Olá ligadas.

Ligar tooyour armazém de dados do SQL do Azure com o Visual Studio com o nome de início de sessão do armazém de dados do SQL Server Olá e a palavra-passe e abrir Olá **SQL Server Object Explorer** base de dados do tooconfirm Olá e tabelas foram importadas. Obter Olá *SQLDW_Explorations.sql* ficheiro.

> [!NOTE]
> tooopen um editor de consultas do armazém de dados paralelo (PDW), utilize Olá **nova consulta** comando enquanto o PDW está selecionado na Olá **SQL Server Object Explorer**. editor de consultas de SQL Server standard Olá não é suportado pelo PDW.
> 
> 

Seguem-se o tipo de Olá de dados efetuar tarefas de geração de exploração e funcionalidade nesta secção:

* Explore as distribuições de dados de alguns campos no variando intervalos de tempo.
* Investigue a qualidade dos dados de campos de latitude e longitude de Olá.
* Gerar etiquetas de classificação de várias classes e binária com base no Olá **sugestão\_quantidade**.
* Gerar funcionalidades e computação/comparar as distâncias de viagem.
* Associar tabelas Olá dois e extrair amostra aleatória que será utilizado toobuild modelos.

### <a name="data-import-verification"></a>Verificação de importação de dados
Estas consultas fornecem uma verificação rápida do número de Olá de linhas e colunas no Olá tabelas povoadas anteriormente utilizando em massa de paralela do Polybase importar,

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**Saída:** deve obter 173,179,759 linhas e colunas de 14.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploração: Distribuição de viagem por medallion
Esta consulta de exemplo identifica medallions Olá (taxi números) concluir mais do que 100 viagens dentro do período de tempo especificado. consulta de Olá seria beneficiar de acesso de tabela Olá particionada desde que está a ter pelo esquema de partição Olá da **recolha\_datetime**. Consultar o conjunto de dados completo Olá também faz com que a utilização de tabela particionada Olá e/ou a análise de índice.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**Saída:** consulta Olá deve devolver uma tabela com linhas especificando medallions Olá 13,369 (taxis) e Olá diversas viagem concluída no 2013. a coluna último Olá contém uma contagem de Olá do número de Olá de viagens foi concluída.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploração: Distribuição de viagem medallion e hack_license
Neste exemplo identifica medallions Olá (taxi números) e hack_license números (controladores do) que foram concluídos mais do que 100 viagens durante um período de tempo especificado.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**Saída:** consulta Olá deve devolver uma tabela com 13,369 linhas especificando Olá 13,369 carro/controlador IDs concluiu mais esse viagens 100 em 2013. a coluna último Olá contém uma contagem de Olá do número de Olá de viagens foi concluída.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Avaliação de qualidade de dados: verificar os registos com incorreto longitude e/ou latitude
Neste exemplo investiga se qualquer um dos campos de longitude e/ou latitude Olá ou contém um valor inválido (radian graus devem ser entre -90 e 90), ou ter (0, 0) coordenadas.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**Saída:** consulta Olá devolve 837,467 viagens com campos de longitude e/ou latitude inválidos.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploração: Tipped vs distribuição viagens não tipped
Neste exemplo localiza o número de Olá de viagens foram tipped vs número Olá que não foram tipped num período de tempo especificado (ou em Olá conjunto de dados completo se que abrangem ano completa Olá, que está definido aqui). Esta distribuição reflete Olá etiqueta binário distribuição toobe posteriormente utilizado para a modelação de classificação binária.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**Saída:** Olá consulta deve seguinte Olá retorno sugestão frequências para o ano de Olá 2013: 90,447,622 tipped e 82,264,709 tipped em não.

### <a name="exploration-tip-classrange-distribution"></a>Exploração: Distribuição de classe/intervalo de sugestão
Neste exemplo calcula a distribuição de Olá de intervalos de sugestão num determinado momento período (ou em Olá conjunto de dados completo se que abrangem ano completa Olá). Esta é a distribuição de Olá das classes de etiqueta Olá que serão utilizados mais tarde para a modelação de classificação de várias classes.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**Saída:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>Exploração: Computação e comparar distância viagem
Neste exemplo converte longitude de recolha e drop-off Olá e pontos de geografia de tooSQL latitude, calcula distância de viagem Olá utilizando a diferença de pontos de geografia SQL e devolve uma amostra aleatória de resultados de Olá para comparação. exemplo de Olá limita os resultados de Olá toovalid coordena a utilizar apenas Olá qualidade assessment a consulta de dados abrangida anteriormente.

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>Engenharia da funcionalidade utilizando funções do SQL Server
Por vezes, as funções do SQL Server podem ser uma opção eficiente para engenharia da funcionalidade. Nestas instruções, iremos definido uma SQL Server função toocalculate Olá direta distância entre localizações de recolha e dropoff Olá. Pode executar Olá seguintes scripts do SQL Server no **ferramentas de dados do Visual Studio**.

Eis o script SQL Olá que define a função de distância Olá.

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

Eis um exemplo toocall funcionalidades de toogenerate esta função na sua consulta SQL:

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**Saída:** esta consulta gera uma tabela (com 2,803,538 linhas) com a recolha e dropoff latitudes e longitudes e Olá correspondente direcionam as distâncias em quilómetros. Seguem-se os resultados de Olá primeiros 3 linhas:

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40.731804 |-74.001083 |40.736622 |-73.988953 |.7169601222 |
| 2 |40.715794 |-74,010635 |40.725338 |-74.00399 |.7448343721 |
| 3 |40.761456 |-73.999886 |40.766544 |-73.988228 |0.7037227967 |

### <a name="prepare-data-for-model-building"></a>Preparar a criação de modelo de dados
Olá associações de consulta seguinte Olá **nyctaxi\_viagem** e **nyctaxi\_fare** tabelas, gera uma etiqueta de classificação binária **tipped**, um etiqueta de classificação de classe Multi **sugestão\_classe**e extrai um exemplo de Olá conjunto de dados completo associados. a amostragem Olá é feita ao aceder a um subconjunto de viagens Olá com base na hora de recolha.  Esta consulta pode ser copiada e colada diretamente no Olá [Azure Machine Learning Studio](https://studio.azureml.net) [importar dados] [ import-data] módulo para a ingestão de dados direta de instância de base de dados do SQL Olá no Azure. consulta de Olá exclui registos com incorreto (0, 0) coordenadas.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

Quando estiver pronto tooproceed tooAzure Machine Learning, o utilizador pode optar por:  

1. Guardar Olá final SQL tooextract e exemplo Olá dados e copiar-colar Olá consulta diretamente para um [importar dados] [ import-data] módulo no Azure Machine Learning, ou
2. Manter Olá amostragem e foi desenvolvidos dados planear toouse para criação de um novo armazém de dados do SQL Server do modelo de tabela e utilizam a nova tabela de Olá no Olá [importar dados] [ import-data] módulo no Azure Machine Learning. Olá script do PowerShell no passo anterior execute este procedimento para si. Pode ler diretamente a partir desta tabela no módulo de importar dados de Olá.

## <a name="ipnb"></a>Exploração de dados e de engenharia da funcionalidade no bloco de notas do IPython
Nesta secção, iremos efetuar exploração de dados e a geração de funcionalidade utilizando ambos os Python e as consultas SQL contra Olá armazém de dados do SQL Server criado anteriormente. Um exemplo IPython bloco de notas com o nome **SQLDW_Explorations.ipynb** e um ficheiro de script de Python **SQLDW_Explorations_Scripts.py** ter sido transferido tooyour diretório local. Também estão disponíveis no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW). Estes dois ficheiros são idênticos em Python scripts. ficheiro de script de Python Olá é fornecido tooyou no caso de não dispõe de um servidor de IPython bloco de notas. Estes dois exemplos Python ficheiros concebidos em **Python 2.7**.

Olá informações necessárias do armazém de dados do Azure SQL no exemplo Olá IPython bloco de notas e Olá Python máquina local de tooyour transferido do ficheiro de script tenha sido ligada pelo script de PowerShell Olá anteriormente. São executáveis sem qualquer modificação.

Se já tiver configurado uma área de trabalho do AzureML, diretamente pode carregar o exemplo de Olá serviço de bloco de notas do AzureML IPython do bloco de notas IPython toohello e iniciar a executá-lo. Seguem-se Olá passos tooupload tooAzureML serviço IPython bloco de notas:

1. Inicie sessão na área de trabalho do tooyour AzureML, clique em "Studio" na parte superior do Olá e clique em "PORTÁTEIS" no lado esquerdo do Olá da página web de Olá.
   
    ![Desenhar #22][22]
2. Clique em "Novo" no canto inferior esquerdo de Olá da página web de Olá e selecione "Python 2". Em seguida, forneça um bloco de notas do nome toohello e clique em Olá marca de verificação toocreate Olá nova em branco IPython bloco de notas.
   
    ![Desenhar #23][23]
3. Clique em Símbolo de "Jupyter" Olá no canto superior esquerdo do Olá Olá novo IPython bloco de notas.
   
    ![Desenhar #24][24]
4. Arrastar e largar toohello de IPython bloco de notas do exemplo Olá **árvore** página do seu serviço de bloco de notas do AzureML IPython e clique em **carregar**. Em seguida, o exemplo de Olá IPython bloco de notas será carregado toohello serviço bloco de notas do AzureML IPython.
   
    ![Desenhar #25][25]

No Olá toorun de ordem de exemplo IPython bloco de notas ou Olá o ficheiro de script de Python, hello seguintes pacotes de Python são necessários. Se estiver a utilizar o serviço de bloco de notas do AzureML IPython Olá, estes pacotes foram instalados previamente.

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

Olá recomendado sequência quando criar soluções de analíticas avançadas em AzureML com dados de grandes dimensões é a seguinte Olá:

* Ler um exemplo de dados de Olá pequeno para um intervalo de dados em memória.
* Efetuar algumas visualizações e explorations utilizando Olá amostras de dados.
* Experimentar a engenharia da funcionalidade utilizando dados Olá amostragem.
* Exploração de dados maior, manipulação de dados e de engenharia da funcionalidade, utilize Python tooissue SQL consultas diretamente Olá armazém de dados do SQL Server.
* Decida toobe de tamanho de exemplo de Olá adequado para a criação de modelo do Azure Machine Learning.

seguinte Olá é alguns dados exploração, visualização de dados e exemplos de engenharia da funcionalidade. Mais explorations de dados podem ser encontrados no exemplo Olá IPython bloco de notas e ficheiro de script de Python de exemplo de Olá.

### <a name="initialize-database-credentials"></a>Inicializar as credenciais da base de dados
Inicializar as definições de ligação de base de dados no Olá seguintes variáveis:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>Criar a ligação de base de dados
Segue-se a cadeia de ligação de Olá que cria a base de dados do Olá ligação toohello.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Número de relatório de linhas e colunas na tabela < nyctaxi_trip >
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de linhas = 173179759  
* Número total de colunas = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>Número de relatório de linhas e colunas na tabela < nyctaxi_fare >
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de linhas = 173179759  
* Número total de colunas = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>Leia-in de uma amostra de dados de pequena de Olá a base de dados do armazém de dados SQL
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tabela de exemplo do tempo tooread Olá é 14.096495 segundos.  
Número de linhas e colunas obter = (1000, 21).

### <a name="descriptive-statistics"></a>Estatísticas descritivas
Agora, está pronto tooexplore dados de Olá amostragem. Vamos começar a utilizar ao procurar algumas estatísticas descritivas para Olá **viagem\_distância** (ou quaisquer outros campos escolher toospecify).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>Visualização: Exemplo de desenho de caixa
Em seguida vamos ver desenho de caixa de Olá para Olá viagem distância toovisualize Olá quantiles.

    df1.boxplot(column='trip_distance',return_type='dict')

![Desenhar #1][1]

### <a name="visualization-distribution-plot-example"></a>Visualização: Exemplo de desenho de distribuição
Plots visualizar distribuição Olá e um histograma para as distâncias viagem de Olá amostragem.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Desenhar #2][2]

### <a name="visualization-bar-and-line-plots"></a>Barra de visualização: E rastreia de linha
Neste exemplo, vamos bin distância de viagem Olá em cinco intervalos binários e visualizar Olá discretização resultados.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Iremos pode desenhar Olá acima distribuição bin na barra de uma ou linha desenho com:

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Desenhar #3][3]

e

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Desenhar #4][4]

### <a name="visualization-scatterplot-examples"></a>Visualização: Exemplos de Scatterplot
Vamos mostrar o desenho de gráfico de dispersão entre **viagem\_tempo\_no\_seg** e **viagem\_distância** toosee se não houver qualquer correlação

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Desenhar #6][6]

Da mesma forma, pode verificar a relação Olá entre **taxa\_código** e **viagem\_distância**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Desenhar #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>Exploração de dados em amostras de dados através de consultas SQL no bloco de notas do IPython
Nesta secção, vamos explorar as distribuições de dados utilizando os dados de Olá amostragem que são mantidos numa tabela nova Olá que criámos acima. Tenha em atenção que podem ser executadas explorations semelhantes utilizando tabelas original Olá.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>Exploração: O número de relatório de linhas e colunas no Olá amostragem tabela
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>Exploração: Tipped/não tripped distribuição
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>Exploração: Distribuição de classe de sugestão
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>Exploração: Desenhar distribuição de sugestão Olá pela classe
    tip_class_dist['tip_freq'].plot(kind='bar')

![Desenhar #26][26]

#### <a name="exploration-daily-distribution-of-trips"></a>Exploração: Distribuição diária viagens
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploração: Viagem distribuição por medallion
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>Exploração: Viagem distribuição através da licença medallion e acesso
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>Exploração: Distribuição de tempo de viagem
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>Exploração: Distribuição de distância viagem
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>Exploração: Distribuição de tipo de pagamento
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Verificar o formulário de final Olá da tabela de featurized Olá
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>Criar modelos no Azure Machine Learning
Iremos agora está pronto tooproceed toomodel criação e implementação de modelo no [Azure Machine Learning](https://studio.azureml.net). dados de Olá estão pronto toobe utilizado em qualquer um dos problemas de predição de Olá identificados anteriormente, nomeadamente:

1. **Classificação binária**: toopredict ou não uma sugestão foi paga para uma viagem.
2. **Classificação de várias classes**: intervalo de Olá toopredict de sugestão paga, de acordo com toohello classes definidas anteriormente.
3. **Tarefa de regressão**: quantidade de Olá toopredict de sugestão paga para uma viagem.  

toobegin Olá modelação exercício, inicie sessão no tooyour **Azure Machine Learning** área de trabalho. Se ainda não tiver criado uma área de trabalho de aprendizagem, consulte o artigo [criar uma área de trabalho do Azure ML](machine-learning-create-workspace.md).

1. tooget iniciado com o Azure Machine Learning, consulte [que é o Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)
2. Inicie sessão no demasiado[Azure Machine Learning Studio](https://studio.azureml.net).
3. página de Studio Home Olá fornece uma variedade de informações, vídeos, tutoriais, ligações toohello referência de módulos e outros recursos. Para obter mais informações sobre o Azure Machine Learning, consulte Olá [Centro de documentação do Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

Uma experimentação de preparação típica é constituída por Olá os seguintes passos:

1. Criar um **+ novo** experimentação.
2. Obter dados de Olá no Azure ML.
3. Pré-processar, transformar e manipular dados de Olá conforme necessário.
4. Gere funcionalidades conforme necessário.
5. Dividir os dados de Olá em conjuntos de dados de formação / / testes validação (ou tem conjuntos de dados separados para cada).
6. Selecione um ou mais algoritmos do machine learning consoante Olá toosolve de problema de aprendizagem. Por exemplo, classificação binária, classificação de várias classes, regressão.
7. Preparar um ou mais modelos utilizando o conjunto de dados de formação de Olá.
8. Conjunto de dados de validação Olá utilizando model(s) treinado Olá de pontuação.
9. Avalie Olá model(s) toocompute Olá relevantes métricas para Olá problema de aprendizagem.
10. Ajustar Olá model(s) e selecione Olá melhor toodeploy de modelo.

Neste exercício, vamos já explorou e foi desenvolvido dados Olá no armazém de dados do SQL Server e decidir tooingest de tamanho de exemplo de Olá no Azure ML. Eis Olá procedimento toobuild um ou mais dos modelos de previsão Olá:

1. Obter dados Olá do Azure ML com Olá [importar dados] [ import-data] módulo, disponível no Olá **dados de entrada e saída** secção. Para obter mais informações, consulte Olá [importar dados] [ import-data] página de referência do módulo.
   
    ![Dados de importação do Azure ML][17]
2. Selecione **SQL Database do Azure** como Olá **origem de dados** no Olá **propriedades** painel.
3. Introduza o nome DNS de base de dados de Olá no Olá **nome do servidor de base de dados** campo. Formato:`tcp:<your_virtual_machine_DNS_name>,1433`
4. Introduza Olá **nome de base de dados** no campo correspondente Olá.
5. Introduza Olá *nome de utilizador do SQL Server* no Olá **nome de conta de utilizador do servidor**e Olá *palavra-passe* no Olá **palavra-passe de conta de utilizador do**.
6. Verifique Olá **aceita qualquer certificado de servidor** opção.
7. No Olá **consulta de base de dados** editar a área de texto, cole a consulta de Olá que extrai Olá necessário campos (incluindo quaisquer campos calculados como etiquetas Olá) da base de dados e pendente amostras de tamanho da amostra Olá dados toohello assim o desejar.

Um exemplo de uma experimentação de classificação binária ler os dados diretamente a partir da base de dados do SQL Data Warehouse Olá é na figura Olá abaixo (Lembre-se de que tooreplace Olá nomes das tabelas nyctaxi_trip e nyctaxi_fare pelo esquema Olá nome e Olá os nomes das tabelas utilizadas na sua EXPLICAÇÃO passo a passo). Podem ser construídas experimentações semelhantes para classificação de várias classes e problemas de regressão.

![Formação do Azure ML][10]

> [!IMPORTANT]
> No Olá modelação de extração de dados e fazendo a amostragem exemplos de consultas fornecidos nas secções anteriores, **todas as etiquetas para exercícios de modelação Olá três estão incluídas na consulta de Olá**. Um passo importante (obrigatório) em cada um dos Olá modelação exercícios é demasiado**excluir** Olá desnecessárias etiquetas para Olá outros dois problemas e quaisquer outros **fugas de destino**. Por exemplo, quando utilizar a classificação do binária, utilize etiqueta Olá **tipped** e excluir os campos de Olá **sugestão\_classe**, **sugestão\_quantidade**, e **total\_quantidade**. Olá última são fugas de destino, desde que o implica sugestão Olá paga.
> 
> tooexclude quaisquer colunas desnecessárias ou fugas de destino, pode utilizar Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo ou Olá [Editar metadados] [ edit-metadata]. Para obter mais informações, consulte [selecionar colunas no conjunto de dados] [ select-columns] e [Editar metadados] [ edit-metadata] páginas de referência.
> 
> 

## <a name="mldeploy"></a>Implementar modelos no Azure Machine Learning
Quando o modelo estiver pronto, pode facilmente implementá-lo como um serviço web diretamente a partir da experimentação Olá. Para obter mais informações sobre a implementação de serviços web do Azure ML, consulte [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy um novo serviço web, tem de:

1. Crie uma experimentação de classificação.
2. Implemente o serviço web de Olá.

toocreate uma classificação de experimentação de um **concluído** experimentação de preparação, clique em **criar classificação experimentação** na barra de ação inferior Olá.

![A classificação do Azure][18]

O Azure Machine Learning tentará toocreate uma experimentação de classificação com base nos componentes de Olá do experimentação de preparação de Olá. Em particular, irá:

1. Guarde o modelo treinado Olá e remover módulos de formação do modelo de Olá.
2. Identificar uma lógica **porta de entrada** toorepresent Olá esperado esquema de dados de entrada.
3. Identificar uma lógica **porta de saída** esquema de saída do serviço do toorepresent Olá web esperado.

Quando é criado Olá experimentação de classificação, reveja-lo e efetue a ajustar conforme necessário. Um ajuste típico é conjunto de dados entrada tooreplace Olá e/ou a consulta com um que exclui os campos de etiqueta, como estes não estarão disponíveis quando o serviço de Olá é chamado. Também é que um boa prática tooreduce Olá o tamanho de Olá entrada tooa de consulta e/ou conjunto de dados poucos registos, apenas suficiente esquema da entrada Olá tooindicate. Para a porta de saída Olá, é comum tooexclude campos de entrada de todos os e incluir apenas Olá **etiquetas classificadas** e **probabilidades classificadas** no Olá saída utilizando Olá [selecionar colunas no conjunto de dados ] [ select-columns] módulo.

É fornecido um classificação experimentação de exemplo na figura Olá abaixo. Quando está preparado toodeploy, clique em Olá **publicar o serviço de WEB** botão na barra de ação inferior Olá.

![A publicação do Azure ML][11]

## <a name="summary"></a>Resumo
toorecap que que efetuou neste tutorial explicação passo a passo, criou um ambiente de ciência de dados do Azure, trabalhou com um grande conjunto de dados público, colocá-lo através de Olá processo de ciência de dados de equipa, todas as forma de Olá de formação de toomodel de aquisição de dados e, em seguida, toohello a implementação de um serviço web Azure Machine Learning.

### <a name="license-information"></a>Informações de licença
Estas instruções de exemplo e o respetivo que acompanha scripts e IPython notebook(s) são partilhadas pela Microsoft em licença MIT de Olá. Verifique o ficheiro de LICENSE.txt Olá no diretório de Olá do código de exemplo de Olá no GitHub para obter mais detalhes.

## <a name="references"></a>Referências
• [Andrés Monroy NYC Taxi viagens página de transferência](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC Taxi viagem dados por Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi e Limousine Commission investigação e estatísticas](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
