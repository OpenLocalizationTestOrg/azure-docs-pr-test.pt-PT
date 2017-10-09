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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="72df5-103">Soluções de armazenamento do Azure para o servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="72df5-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="72df5-104">Microsoft R Server no HDInsight tem uma variedade de dados de toopersist de soluções de armazenamento, código ou objetos que contêm os resultados da análise.</span><span class="sxs-lookup"><span data-stu-id="72df5-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="72df5-105">Estas incluem Olá seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="72df5-105">These include hello following options:</span></span>

- [<span data-ttu-id="72df5-106">Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="72df5-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="72df5-107">Armazenamento do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="72df5-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="72df5-108">File storage do Azure</span><span class="sxs-lookup"><span data-stu-id="72df5-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="72df5-109">Tem também a opção de Olá de aceder a várias contas de armazenamento do Azure ou contentores com o cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="72df5-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="72df5-110">File storage do Azure é uma opção de armazenamento de dados conveniente para utilização no nó de extremidade de Olá permite-lhe toomount uma partilha de ficheiros de armazenamento do Azure para, por exemplo, Olá Linux sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="72df5-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="72df5-111">Mas partilhas de ficheiros do Azure podem ser montadas e utilizadas por qualquer sistema com um SO suportado, tais como o Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="72df5-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="72df5-112">Quando cria um cluster do Hadoop no HDInsight, especificou um **storage do Azure** conta ou um **arquivo Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="72df5-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="72df5-113">Um contentor de armazenamento específico da conta de que contém o sistema de ficheiros de Olá para cluster Olá por si (por exemplo, Olá sistema de ficheiros distribuído Hadoop).</span><span class="sxs-lookup"><span data-stu-id="72df5-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="72df5-114">Para obter mais informações e orientações, consulte:</span><span class="sxs-lookup"><span data-stu-id="72df5-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="72df5-115">Utilizar o armazenamento do Azure com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="72df5-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="72df5-116">[Utilizar o Data Lake Store com o Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="72df5-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="72df5-117">Para obter mais informações sobre soluções de armazenamento do Azure Olá, consulte [introdução tooMicrosoft Storage do Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="72df5-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="72df5-118">Para obter orientações sobre a seleção de Olá mais adequado armazenamento opção toouse para o seu cenário, consulte [Deciding quando toouse Azure Blobs, ficheiros do Azure ou os discos de dados do Azure](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="72df5-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="72df5-119">Utilizar contas de armazenamento de Blobs do Azure com o servidor de R</span><span class="sxs-lookup"><span data-stu-id="72df5-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="72df5-120">Se necessário, pode aceder a várias contas de armazenamento do Azure ou contentores com o cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="72df5-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="72df5-121">toodo por isso, terá de toospecify Olá mais contas do storage no Olá IU ao criar o cluster de Olá e, em seguida, siga estes passos toouse-los com o servidor R.</span><span class="sxs-lookup"><span data-stu-id="72df5-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="72df5-122">Por motivos de desempenho, Olá cluster do HDInsight é criado no Olá mesmo centro de dados como conta de armazenamento primário Olá que especificar.</span><span class="sxs-lookup"><span data-stu-id="72df5-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="72df5-123">Não é suportada a utilização de uma conta de armazenamento no cluster do HDInsight Olá numa localização diferente.</span><span class="sxs-lookup"><span data-stu-id="72df5-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="72df5-124">Criar um cluster do HDInsight com um nome de conta de armazenamento de **storage1** e um contentor predefinido denominada **container1**.</span><span class="sxs-lookup"><span data-stu-id="72df5-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="72df5-125">Especifique uma conta de armazenamento adicional chamada **storage2**.</span><span class="sxs-lookup"><span data-stu-id="72df5-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="72df5-126">Copie o diretório do ficheiro Olá mycsv.csv toohello /share e executar uma análise em que o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="72df5-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="72df5-127">No código do R, defina o nó de nome de Olá demasiado**predefinido,** e definir o ficheiro e diretório tooprocess.</span><span class="sxs-lookup"><span data-stu-id="72df5-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

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

<span data-ttu-id="72df5-128">Olá todos os ficheiros e diretórios conta de armazenamento de ponto toohello referências wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="72df5-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="72df5-129">Este é Olá **predefinido a conta de armazenamento** que associado ao cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="72df5-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="72df5-130">Agora, suponha que pretende tooprocess um ficheiro chamado mySpecial.csv que está localizado em Olá /private diretório de **container2** no **storage2**.</span><span class="sxs-lookup"><span data-stu-id="72df5-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="72df5-131">No seu código de R, aponte Olá nome nó referência toohello **storage2** conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72df5-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


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

<span data-ttu-id="72df5-132">Todos os Olá ficheiro e diretório referências agora toohello ponto da conta de armazenamento wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="72df5-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="72df5-133">Este é Olá **nome de nó** que tiver especificado.</span><span class="sxs-lookup"><span data-stu-id="72df5-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="72df5-134">Tiver tooconfigure Olá /user RevoShare/<SSH username> diretório **storage2** da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="72df5-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="72df5-135">Utilizar um arquivo Azure Data Lake com o servidor de R</span><span class="sxs-lookup"><span data-stu-id="72df5-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="72df5-136">armazena toouse Data Lake com a sua conta do HDInsight, precisa de toogive seu cluster aceder ao tooeach do Azure Data Lake store que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="72df5-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="72df5-137">Para obter instruções sobre como toouse Olá toocreate do portal do Azure, uma HDInsight cluster com uma conta do Azure Data Lake Store, como armazenamento de predefinido Olá ou como um arquivo de adicional, consulte [criar um cluster do HDInsight com o Data Lake Store utilizando o portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="72df5-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="72df5-138">Em seguida, utilizar Olá loja no seu script R muito como fez uma conta do storage do Azure secundário conforme descrito no procedimento anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="72df5-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="72df5-139">Adicionar o cluster acesso tooyour que armazena do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="72df5-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="72df5-140">Aceder a um arquivo Data Lake, utilizando um Principal de serviço do Azure Active Directory (Azure AD) associado ao cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72df5-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="72df5-141">tooadd um Principal de serviço do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="72df5-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="72df5-142">Quando criar o cluster do HDInsight, selecione **identidade do AAD Cluster** de Olá **origem de dados** separador.</span><span class="sxs-lookup"><span data-stu-id="72df5-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="72df5-143">No Olá **identidade do AAD Cluster** caixa de diálogo em **selecione Principal de serviço do AD**, selecione **criar nova**.</span><span class="sxs-lookup"><span data-stu-id="72df5-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="72df5-144">Depois de dar um nome de Olá Principal de serviço e criar uma palavra-passe para o mesmo, clique em **gerir o acesso ADLS** Olá tooassociate armazena Principal de serviço com o Data Lake.</span><span class="sxs-lookup"><span data-stu-id="72df5-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="72df5-145">Também é possível tooadd cluster acesso tooone ou mais Data Lake armazena seguintes criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="72df5-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="72df5-146">Abra Olá entrada portal do Azure para um arquivo Data Lake e aceda demasiado**Explorador de dados > acesso > Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="72df5-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="72df5-147">Como tooaccess Olá arquivo Data Lake do servidor R</span><span class="sxs-lookup"><span data-stu-id="72df5-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="72df5-148">Depois de concedeu ao aceder ao tooa Data Lake store, pode utilizar arquivo Olá no servidor R no HDInsight forma de Olá que faria com uma conta do storage do Azure secundário.</span><span class="sxs-lookup"><span data-stu-id="72df5-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="72df5-149">Olá apenas diferença é que prefixo Olá **wasb: / /** alterações demasiado**adl: / /** da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="72df5-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


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


<span data-ttu-id="72df5-150">Olá comandos seguintes são utilizados tooconfigure Olá conta de armazenamento do Data Lake com o diretório de RevoShare Olá e adicionar um ficheiro. csv de exemplo Olá do exemplo anterior Olá:</span><span class="sxs-lookup"><span data-stu-id="72df5-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="72df5-151">Utilizar o File storage do Azure com o servidor R</span><span class="sxs-lookup"><span data-stu-id="72df5-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="72df5-152">Há também uma opção de armazenamento de dados conveniente para utilização no nó de extremidade de Olá chamado [ficheiros do Azure] ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="72df5-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="72df5-153">Permite-lhe toomount um toohello de partilha de ficheiros de armazenamento do Azure sistema de ficheiros do Linux.</span><span class="sxs-lookup"><span data-stu-id="72df5-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="72df5-154">Esta opção pode ser útil para armazenar ficheiros de dados, os scripts de R e objetos de resultado que poderão ser necessário posteriormente, especialmente quando faz sentido toouse Olá nativa de sistema de ficheiros nó de extremidade Olá em vez do HDFS.</span><span class="sxs-lookup"><span data-stu-id="72df5-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="72df5-155">Uma vantagem principal de ficheiros do Azure é esse ficheiro Olá partilhas podem ser montadas e utilizadas por qualquer sistema com um SO suportado, tais como o Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="72df5-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="72df5-156">Por exemplo, pode ser utilizado por outro cluster de HDInsight foi, ou alguém na sua equipa, pela VM do Azure ou mesmo um sistema local.</span><span class="sxs-lookup"><span data-stu-id="72df5-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="72df5-157">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="72df5-157">For more information, see:</span></span>

- [<span data-ttu-id="72df5-158">Como toouse File storage do Azure com o Linux</span><span class="sxs-lookup"><span data-stu-id="72df5-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="72df5-159">Como toouse File storage do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="72df5-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="72df5-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="72df5-160">Next steps</span></span>

<span data-ttu-id="72df5-161">Agora que compreende as opções de armazenamento do Azure Olá, utilize seguinte de Olá liga toodiscover formas de obter as tarefas de ciência de dados feitas com o servidor R no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72df5-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="72df5-162">Descrição geral do servidor R no HDInsight</span><span class="sxs-lookup"><span data-stu-id="72df5-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="72df5-163">Introdução ao servidor R no Hadoop</span><span class="sxs-lookup"><span data-stu-id="72df5-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="72df5-164">Adicionar servidor RStudio tooHDInsight (se não adicionar durante a criação do cluster)</span><span class="sxs-lookup"><span data-stu-id="72df5-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="72df5-165">Compute context options for R Server on HDInsight (Opções do contexto de cálculo para o R Server no HDInsight)</span><span class="sxs-lookup"><span data-stu-id="72df5-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

