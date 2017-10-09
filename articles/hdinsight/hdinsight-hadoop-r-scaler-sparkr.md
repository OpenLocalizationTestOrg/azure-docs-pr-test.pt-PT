---
title: aaaUse ScaleR e SparkR com o Azure HDInsight | Microsoft Docs
description: Utilize o ScaleR e SparkR com o servidor R e o HDInsight
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a>Combinar ScaleR e SparkR no HDInsight

Este artigo mostra como toopredict voo atrasos de chegada utilizando um **ScaleR** associado ao modelo de regressão logística dos dados em atrasos dos voos e meteorologia **SparkR**. Este cenário demonstra capacidades Olá de ScaleR para manipulação de dados no Spark utilizado com o servidor R da Microsoft para análise. combinação de Olá destas tecnologias permite-lhe funcionalidades mais recentes de Olá tooapply no processamento distribuído.

Embora ambos os pacotes são executadas no motor de execução do Spark do Hadoop, estes ficam bloqueados de dados em memória partilha como cada necessitam os seus próprios respetivas sessões de Spark. Até que este problema é resolvido numa versão futura do R Server, a solução de Olá é toomaintain sessões de Spark sem sobreposição e tooexchange dados através de ficheiros intermédios. instruções de Olá aqui mostram se estes requisitos são tooachieve simples.

Utilizamos um exemplo aqui inicialmente partilhado uma peça em Strata 2016 Mario Inchiosa e Roni Burd que também está disponível através do webinar Olá [criação de uma plataforma de ciência de dados dimensionável com R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). exemplo de Olá utiliza SparkR toojoin Olá airlines conhecidos chegada atraso conjunto de dados com dados de Meteorologia à partida e chegada aeroportos. dados Olá associados, em seguida, são utilizados como modelo de regressão logística da entrada tooa ScaleR para prever o atraso de chegada de voo.

Olá instruções de código foi originalmente escrito para o R Server em execução no Spark de um cluster do HDInsight no Azure. Mas o conceito de Olá de combinar Olá utilização SparkR e ScaleR um script também é válido no contexto de Olá dos ambientes no local. No seguinte Olá, iremos presumem um nível intermédio de dados de conhecimento do R e R Olá [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) biblioteca de R Server. Introduzirmos também a utilização de [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) ao walking através deste cenário.

## <a name="hello-airline-and-weather-datasets"></a>conjuntos de dados de Olá, companhia aérea e meteorologia

Olá **AirOnTime08to12CSV** pública airlines de conjunto de dados contém informações sobre chegada de trânsito e detalhes de partida para todas as flights comerciais dentro Olá Estados Unidos, Outubro de 1987 tooDecember 2012. Este é um conjunto de dados de grandes dimensões: existem registos quase milhões de 150 no total. É apenas em 4 GB descompactado. Está disponível a partir do Olá [E.U.A. government arquivos](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236). Mais comodamente, está disponível como um ficheiro zip (AirOnTimeCSV.zip) que contém um conjunto de 303 mensais ficheiros CSV diferentes de Olá [repositório de conjunto de dados de análise rotações](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)

toosee Olá efeitos de Meteorologia num atrasos dos voos, iremos também precisa de dados de Meteorologia Olá em cada aeroportos Olá. Estes dados podem ser transferidos como ficheiros zip no formato não processado, por mês, do Olá [repositório National Oceanic e administração Atmospheric](http://www.ncdc.noaa.gov/orders/qclcd/). Para efeitos deste exemplo de Olá, solicitar dados Meteorologia do Maio de 2007 – Dezembro de 2012 e utilizado Olá horária os ficheiros de dados dentro de cada um dos zips do Olá 68 mensal. os ficheiros zip mensal do Olá também contém um mapeamento (YYYYMMstation.txt) entre Olá Meteorologia estação ID (WBAN), airport Olá que está associado (CallSign) e Olá desvio de fuso horário do airport do UTC (fuso horário). Toda esta informação é necessária ao associar com Olá companhia aérea atraso e meteorologia dados.

## <a name="setting-up-hello-spark-environment"></a>Configurar o ambiente de Spark Olá

Step-by-Olá primeiro passo é tooset segurança ambiente de Spark Olá. Vamos começar por apontar toohello diretório que contém o nosso diretórios de dados de entrada, criar um contexto de computação do Spark e criar uma função de registo para o registo informativa toohello consola:

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

Em seguida adicionamos "Spark_Home" toohello caminho de pesquisa para pacotes de R, de modo que pode utilizar SparkR e iniciar uma sessão de SparkR:

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a>A preparar os dados de Meteorologia Olá

dados de Meteorologia do tooprepare Olá, iremos subconjunto-necessárias para a modelação de colunas de toohello: 

- "Visibilidade"
- "DryBulbCelsius"
- "DewPointCelsius"
- "RelativeHumidity"
- "WindSpeed"
- "Altimeter"

Em seguida, iremos adicionar um código de airport associado Olá Meteorologia estação e converter medidas Olá de tooUTC de hora local.

Vamos começar por criar um código de airport do ficheiro toomap Olá Meteorologia estação (WBAN) informações tooan. Iremos foi possível obter esta correlação do ficheiro de mapeamento de Olá incluído com dados de Meteorologia Olá. Por Olá mapeamento *CallSign* (por exemplo, LAX) campo no ficheiro de dados de Meteorologia Olá demasiado*origem* nos dados de companhia aérea Olá. No entanto, iremos apenas aconteceu toohave outro mapeamento no manualmente que mapeie *WBAN* demasiado*AirportID* (por exemplo, 12892 para LAX) e inclui *fuso horário* que foi guardado tooa Um ficheiro CSV chamado "wban-para-airport-id-tz. CSV"que podemos utilizar. Por exemplo:

| AirportID | WBAN | Fuso horário
|-----------|------|---------
| 10685 | 54831 | -6
| 14871 | 24232 | -8
| .. | .. | ..

Olá, código de leituras cada dos dados de Meteorologia não processados por hora Olá os seguintes ficheiros, de colunas de toohello subconjuntos é necessário, intercala o ficheiro de mapeamento de estação Meteorologia Olá, ajusta Olá tempos de data de medidas tooUTC e, em seguida, escreve uma nova versão do ficheiro de Olá:

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a>Importação Olá companhia aérea e meteorologia dados tooSpark DataFrames

Agora podemos utilizar Olá SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport Olá meteorologia e companhia aérea dados tooSpark DataFrames de função. Esta função, como muitos outros métodos de Spark, são executadas lentamente, o que significa que são colocados em fila para execução, mas não foi executados até que necessárias.

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a>Limpeza de dados e a transformação

Junto fazemos algumas limpeza Olá companhia aérea de dados tiver importámos toorename colunas. Vamos apenas manter variáveis Olá necessárias e arredondar vezes distanciamento agendada para baixo toohello mais próximo tooenable de hora a intercalação com dados de mais recentes Meteorologia Olá à partida:

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

Agora, iremos efetuar operações similares Olá Meteorologia de dados:

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a>Associar Olá meteorologia e companhia aérea dados

Agora, utilizamos Olá SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) funcionar toodo uma associação externa à esquerda de Olá companhia aérea Meteorologia dados por distanciamento AirportID e e datetime. associação externa Olá permite-nos tooretain todos os dados de companhia aérea Olá regista, mesmo se não houver nenhum dado Meteorologia correspondente. Seguintes associação Olá, iremos remover algumas colunas redundantes e mudar o nome Olá mantido colunas tooremove Olá entrado DataFrame prefixo que foi introduzido pela associação Olá.

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

De forma semelhante, vamos associar Olá meteorologia e companhia aérea dados com base em chegada AirportID e datetime:

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a>Guardar resultados tooCSV para o exchange com ScaleR

Que conclui as associações de Olá precisamos toodo com SparkR. Iremos guardar dados de Olá de Olá final Spark DataFrame "joinedDF5" tooa CSV para tooScaleR de entrada e, em seguida, feche terminar sessão de SparkR Olá. Podemos dizer explicitamente SparkR toosave Olá CSV resultante no 80 partições separado tooenable suficientes o paralelismo na processamento ScaleR:

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a>Importar tooXDF para utilização por ScaleR

Iremos utilizar um ficheiro CSV Olá da companhia aérea associada e os dados de Meteorologia como-é para a modelação através de uma origem de dados de texto ScaleR. Mas iremos importá-lo tooXDF em primeiro lugar, uma vez que é mais eficiente ao executar várias operações Olá conjunto de dados:

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a>Dividir os dados para formação e teste

Podemos utilizar rxDataStep toosplit saída dados de 2012 Olá para fins de teste e manter rest Olá para formação:

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a>Dar formação e testar um modelo de regressão logística da

Agora vamos está pronto toobuild um modelo. toosee Olá influência dos dados de Meteorologia num atraso na hora da chegada de Olá, utilizamos rotina de regressão logística da ScaleR. Iremos utilizá-lo toomodel se um atraso de chegada de superior a 15 minutos é deve influenciado pelos Meteorologia Olá em aeroportos de partida e chegada Olá:

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

Agora vamos ver como este no Olá testar dados ao efetuar algumas predições e observar ROC e AUC.

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a>Classificação noutro local

Também podemos utilizar o modelo de Olá para classificação de dados noutra plataforma. Guardar ficheiro RDS tooan e, em seguida, transferir e importando esse RDS para um destino de classificação de ambiente, tais como o SQL Server R Services. É importante tooensure que níveis de fator de Olá de Olá dados toobe classificada correspondem no qual Olá modelo foi criado. Que pode ser conseguida correspondência extraindo e guardar as informações de coluna Olá associado Olá modelação dados através da ScaleR `rxCreateColInfo()` função e, em seguida, aplicar essa origem de dados de entrada do coluna informações toohello para predição. Seguir Olá iremos guardar algumas linhas do conjunto de dados de teste de Olá e extrair e utilizar informações de coluna Olá deste exemplo no script de predição de Olá:

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a>Resumo

Neste artigo, vamos tiver mostrado como é possível toocombine utilização SparkR para manipulação de dados com ScaleR para o desenvolvimento de modelo no Spark do Hadoop. Este cenário requer manter sessões separadas do Spark, apenas a executar uma sessão a uma hora e trocar dados através de ficheiros CSV. Embora simples, este processo deve ser ainda mais fáceis uma versão de R Server lançamentos, quando SparkR ScaleR pode partilhar uma sessão de Spark e, por isso, partilhar DataFrames de Spark.

## <a name="next-steps-and-more-information"></a>Passos seguintes e obter mais informações

- Para obter mais informações sobre a utilização do servidor R no Spark, consulte Olá [guia de introdução no MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)

- Para obter informações gerais sobre o R Server, consulte Olá [começar a utilizar o R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) artigo.

- Para obter informações sobre o servidor R no HDInsight, consulte [servidor R no Descrição geral do Azure HDInsight](hdinsight-hadoop-r-server-overview.md) e [R Server no Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).

Para obter mais informações sobre a utilização de SparkR, consulte:

- [Apache SparkR documento](https://spark.apache.org/docs/2.1.0/sparkr.html)

- [Descrição geral de SparkR](https://docs.databricks.com/spark/latest/sparkr/overview.html) de Databricks
