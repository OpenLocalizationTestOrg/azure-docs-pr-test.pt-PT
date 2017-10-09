---
title: "aaaAzure soluções de armazenamento para o servidor R no HDInsight - Azure | Microsoft Docs"
description: "Saiba mais sobre Olá armazenamento diferentes opções disponíveis toousers com o servidor R no HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Soluções de armazenamento do Azure para o servidor R no HDInsight

Microsoft R Server no HDInsight tem uma variedade de dados de toopersist de soluções de armazenamento, código ou objetos que contêm os resultados da análise. Estas incluem Olá seguintes opções:

- [Blob do Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Armazenamento do Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/)
- [File storage do Azure](https://azure.microsoft.com/services/storage/files/)

Tem também a opção de Olá de aceder a várias contas de armazenamento do Azure ou contentores com o cluster HDI. File storage do Azure é uma opção de armazenamento de dados conveniente para utilização no nó de extremidade de Olá permite-lhe toomount uma partilha de ficheiros de armazenamento do Azure para, por exemplo, Olá Linux sistema de ficheiros. Mas partilhas de ficheiros do Azure podem ser montadas e utilizadas por qualquer sistema com um SO suportado, tais como o Windows ou Linux. 

Quando cria um cluster do Hadoop no HDInsight, especificou um **storage do Azure** conta ou um **arquivo Data Lake**. Um contentor de armazenamento específico da conta de que contém o sistema de ficheiros de Olá para cluster Olá por si (por exemplo, Olá sistema de ficheiros distribuído Hadoop). Para obter mais informações e orientações, consulte:

- [Utilizar o armazenamento do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md)
- [Utilizar o Data Lake Store com o Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md). 

Para obter mais informações sobre soluções de armazenamento do Azure Olá, consulte [introdução tooMicrosoft Storage do Azure](../storage/common/storage-introduction.md). 

Para obter orientações sobre a seleção de Olá mais adequado armazenamento opção toouse para o seu cenário, consulte [Deciding quando toouse Azure Blobs, ficheiros do Azure ou os discos de dados do Azure](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>Utilizar contas de armazenamento de Blobs do Azure com o servidor de R

Se necessário, pode aceder a várias contas de armazenamento do Azure ou contentores com o cluster HDI. toodo por isso, terá de toospecify Olá mais contas do storage no Olá IU ao criar o cluster de Olá e, em seguida, siga estes passos toouse-los com o servidor R.

> [!WARNING]
> Por motivos de desempenho, Olá cluster do HDInsight é criado no Olá mesmo centro de dados como conta de armazenamento primário Olá que especificar. Não é suportada a utilização de uma conta de armazenamento no cluster do HDInsight Olá numa localização diferente.

1. Criar um cluster do HDInsight com um nome de conta de armazenamento de **storage1** e um contentor predefinido denominada **container1**.
2. Especifique uma conta de armazenamento adicional chamada **storage2**.  
3. Copie o diretório do ficheiro Olá mycsv.csv toohello /share e executar uma análise em que o ficheiro.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. No código do R, defina o nó de nome de Olá demasiado**predefinido,** e definir o ficheiro e diretório tooprocess.  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

Olá todos os ficheiros e diretórios conta de armazenamento de ponto toohello referências wasb://container1@storage1.blob.core.windows.net. Este é Olá **predefinido a conta de armazenamento** que associado ao cluster do HDInsight Olá.

Agora, suponha que pretende tooprocess um ficheiro chamado mySpecial.csv que está localizado em Olá /private diretório de **container2** no **storage2**.

No seu código de R, aponte Olá nome nó referência toohello **storage2** conta de armazenamento.


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

Todos os Olá ficheiro e diretório referências agora toohello ponto da conta de armazenamento wasb://container2@storage2.blob.core.windows.net. Este é Olá **nome de nó** que tiver especificado.

Tiver tooconfigure Olá /user RevoShare/<SSH username> diretório **storage2** da seguinte forma:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>Utilizar um arquivo Azure Data Lake com o servidor de R

armazena toouse Data Lake com a sua conta do HDInsight, precisa de toogive seu cluster aceder ao tooeach do Azure Data Lake store que pretende que o toouse. Para obter instruções sobre como toouse Olá toocreate do portal do Azure, uma HDInsight cluster com uma conta do Azure Data Lake Store, como armazenamento de predefinido Olá ou como um arquivo de adicional, consulte [criar um cluster do HDInsight com o Data Lake Store utilizando o portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Em seguida, utilizar Olá loja no seu script R muito como fez uma conta do storage do Azure secundário conforme descrito no procedimento anterior Olá.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Adicionar o cluster acesso tooyour que armazena do Azure Data Lake
Aceder a um arquivo Data Lake, utilizando um Principal de serviço do Azure Active Directory (Azure AD) associado ao cluster do HDInsight.

tooadd um Principal de serviço do Azure AD:

1. Quando criar o cluster do HDInsight, selecione **identidade do AAD Cluster** de Olá **origem de dados** separador.

2. No Olá **identidade do AAD Cluster** caixa de diálogo em **selecione Principal de serviço do AD**, selecione **criar nova**.

Depois de dar um nome de Olá Principal de serviço e criar uma palavra-passe para o mesmo, clique em **gerir o acesso ADLS** Olá tooassociate armazena Principal de serviço com o Data Lake.

Também é possível tooadd cluster acesso tooone ou mais Data Lake armazena seguintes criação do cluster. Abra Olá entrada portal do Azure para um arquivo Data Lake e aceda demasiado**Explorador de dados > acesso > Adicionar**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>Como tooaccess Olá arquivo Data Lake do servidor R

Depois de concedeu ao aceder ao tooa Data Lake store, pode utilizar arquivo Olá no servidor R no HDInsight forma de Olá que faria com uma conta do storage do Azure secundário. Olá apenas diferença é que prefixo Olá **wasb: / /** alterações demasiado**adl: / /** da seguinte forma:


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


Olá comandos seguintes são utilizados tooconfigure Olá conta de armazenamento do Data Lake com o diretório de RevoShare Olá e adicionar um ficheiro. csv de exemplo Olá do exemplo anterior Olá:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>Utilizar o File storage do Azure com o servidor R

Há também uma opção de armazenamento de dados conveniente para utilização no nó de extremidade de Olá chamado [ficheiros do Azure] ((https://azure.microsoft.com/services/storage/files/). Permite-lhe toomount um toohello de partilha de ficheiros de armazenamento do Azure sistema de ficheiros do Linux. Esta opção pode ser útil para armazenar ficheiros de dados, os scripts de R e objetos de resultado que poderão ser necessário posteriormente, especialmente quando faz sentido toouse Olá nativa de sistema de ficheiros nó de extremidade Olá em vez do HDFS. 

Uma vantagem principal de ficheiros do Azure é esse ficheiro Olá partilhas podem ser montadas e utilizadas por qualquer sistema com um SO suportado, tais como o Windows ou Linux. Por exemplo, pode ser utilizado por outro cluster de HDInsight foi, ou alguém na sua equipa, pela VM do Azure ou mesmo um sistema local. Para obter mais informações, consulte:

- [Como toouse File storage do Azure com o Linux](../storage/files/storage-how-to-use-files-linux.md)
- [Como toouse File storage do Azure no Windows](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Passos seguintes

Agora que compreende as opções de armazenamento do Azure Olá, utilize seguinte de Olá liga toodiscover formas de obter as tarefas de ciência de dados feitas com o servidor R no HDInsight.

* [Descrição geral do servidor R no HDInsight](hdinsight-hadoop-r-server-overview.md)
* [Introdução ao servidor R no Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [Adicionar servidor RStudio tooHDInsight (se não adicionar durante a criação do cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Compute context options for R Server on HDInsight (Opções do contexto de cálculo para o R Server no HDInsight)](hdinsight-hadoop-r-server-compute-contexts.md)

