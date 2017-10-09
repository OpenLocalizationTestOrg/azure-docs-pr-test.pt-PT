---
title: dados de aaaExplore no Azure blob storage com Pandas | Microsoft Docs
description: Como tooexplore dados armazenados no Azure contentor de blob Pandas a utilizar.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="8782f-103">Explorar dados no Armazenamento de Blobs do Azure com o Pandas</span><span class="sxs-lookup"><span data-stu-id="8782f-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="8782f-104">Este documento abrange como tooexplore dados armazenados no Azure blob contentor utilizando [Pandas](http://pandas.pydata.org/) pacote do Python.</span><span class="sxs-lookup"><span data-stu-id="8782f-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="8782f-105">seguinte Olá **menu** liga tootopics que descrevem como toouse ferramentas tooexplore dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8782f-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="8782f-106">Esta tarefa é um passo Olá [o processo de ciência de dados]().</span><span class="sxs-lookup"><span data-stu-id="8782f-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="8782f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8782f-107">Prerequisites</span></span>
<span data-ttu-id="8782f-108">Este artigo pressupõe que tem:</span><span class="sxs-lookup"><span data-stu-id="8782f-108">This article assumes that you have:</span></span>

* <span data-ttu-id="8782f-109">Criar uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8782f-109">Created an Azure storage account.</span></span> <span data-ttu-id="8782f-110">Se precisar de instruções, consulte [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="8782f-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="8782f-111">Armazenados os dados numa conta de armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8782f-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="8782f-112">Se precisar de instruções, consulte [mover dados tooand do armazenamento do Azure](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="8782f-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="8782f-113">Carregar dados de Olá para um DataFrame Pandas</span><span class="sxs-lookup"><span data-stu-id="8782f-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="8782f-114">tooexplore e manipular um conjunto de dados, primeiro deve ser transferido a partir Olá blob tooa local ficheiro de origem, que, em seguida, pode ser carregado num DataFrame Pandas.</span><span class="sxs-lookup"><span data-stu-id="8782f-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="8782f-115">Seguem-se passos de Olá toofollow para este procedimento:</span><span class="sxs-lookup"><span data-stu-id="8782f-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="8782f-116">Transferir dados Olá a partir do Azure blob com Olá seguinte exemplo de código de Python com o serviço blob.</span><span class="sxs-lookup"><span data-stu-id="8782f-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="8782f-117">Substitua a variável de Olá no Olá código com os seus valores específicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8782f-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. <span data-ttu-id="8782f-118">Ler Olá dados para um intervalo de dados Pandas de Olá transferidos ficheiros.</span><span class="sxs-lookup"><span data-stu-id="8782f-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="8782f-119">Agora, os dados de Olá tooexplore pronto e gerar funcionalidades neste conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="8782f-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="8782f-120"><a name="blob-dataexploration"></a>Exemplos de exploração de dados utilizando Pandas</span><span class="sxs-lookup"><span data-stu-id="8782f-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="8782f-121">Seguem-se alguns exemplos de formas dados tooexplore Pandas a utilizar:</span><span class="sxs-lookup"><span data-stu-id="8782f-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="8782f-122">Inspecione Olá **número de linhas e colunas**</span><span class="sxs-lookup"><span data-stu-id="8782f-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="8782f-123">**Inspecione** Olá algumas primeira ou últimas **linhas** no Olá seguinte conjunto de dados:</span><span class="sxs-lookup"><span data-stu-id="8782f-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="8782f-124">Verifique Olá **tipo de dados** cada coluna foi importada como utilizar o seguinte código de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="8782f-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="8782f-125">Verifique Olá **estatísticas básicas** para colunas de Olá na Olá conjunto de dados da seguinte forma</span><span class="sxs-lookup"><span data-stu-id="8782f-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="8782f-126">Observe o número de Olá de entradas para cada valor de coluna da seguinte forma</span><span class="sxs-lookup"><span data-stu-id="8782f-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="8782f-127">**Contagem de valores em falta** versus número real de Olá de entradas em cada coluna utilizando o seguinte código de exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="8782f-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="8782f-128">Se tiver **valores em falta** para uma coluna específica nos dados de Olá, pode colocá-los da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="8782f-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="8782f-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="8782f-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="8782f-130">Outra forma tooreplace os valores em falta é com a função de modo Olá:</span><span class="sxs-lookup"><span data-stu-id="8782f-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="8782f-131">dataframe_blobdata_mode = dataframe_blobdata.fillna ({< nome_coluna >: .mode()[0]}) dataframe_blobdata ['< nome_coluna >']</span><span class="sxs-lookup"><span data-stu-id="8782f-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="8782f-132">Criar um **histograma** desenhar utilizando variável número de intervalos binários tooplot Olá distribuição uma variável</span><span class="sxs-lookup"><span data-stu-id="8782f-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="8782f-133">Observe **correlações** entre variáveis utilizando um scatterplot ou função de correlação incorporada Olá</span><span class="sxs-lookup"><span data-stu-id="8782f-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

