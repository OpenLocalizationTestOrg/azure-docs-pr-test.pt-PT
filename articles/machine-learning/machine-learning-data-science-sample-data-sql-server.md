---
title: aaaSample dados no SQL Server no Azure | Microsoft Docs
description: Dados de exemplo no SQL Server no Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="3c21a-103"><a name="heading"></a>Dados de exemplo no SQL Server no Azure</span><span class="sxs-lookup"><span data-stu-id="3c21a-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="3c21a-104">Este documento mostra como toosample dados armazenados no SQL Server no Azure com o SQL Server ou Olá linguagem de programação do Python.</span><span class="sxs-lookup"><span data-stu-id="3c21a-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="3c21a-105">Também mostra como toomove amostragem dados no Azure Machine Learning ao guardá-lo ficheiro tooa, carregá-lo tooan BLOBs do Azure e, em seguida, ao ler para o Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3c21a-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="3c21a-106">a amostragem de Python Olá utiliza Olá [pyodbc](https://code.google.com/p/pyodbc/) ODBC biblioteca tooconnect tooSQL Server no Azure e Olá [Pandas](http://pandas.pydata.org/) amostragem de Olá toodo de biblioteca.</span><span class="sxs-lookup"><span data-stu-id="3c21a-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="3c21a-107">código de SQL de exemplo de Olá este documento assume que Olá dados estão a ser um servidor de SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c21a-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="3c21a-108">Se não estiver, consulte demasiado[mover dados tooSQL Server no Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tópico para obter instruções sobre como toomove sua tooSQL dados Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="3c21a-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="3c21a-109">seguinte Olá **menu** liga tootopics que descrevem como toosample dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3c21a-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="3c21a-110">**Os dados de exemplo por que motivo?**</span><span class="sxs-lookup"><span data-stu-id="3c21a-110">**Why sample your data?**</span></span>
<span data-ttu-id="3c21a-111">Se o conjunto de dados de Olá planear tooanalyze for grande, é normalmente tooreduce de dados de exemplo toodown Olá uma boa ideia-tooa mais pequeno, mas representativo e mais fácil gerir o tamanho.</span><span class="sxs-lookup"><span data-stu-id="3c21a-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="3c21a-112">Isto facilita a compreensão de dados, exploração e engenharia da funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="3c21a-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="3c21a-113">A função no Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) é tooenable rápido fazer o protótipo de funções de processamento de dados de Olá e modelos de machine learning.</span><span class="sxs-lookup"><span data-stu-id="3c21a-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="3c21a-114">Esta tarefa de amostragem é um passo Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="3c21a-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="3c21a-115"><a name="SQL"></a>Utilizar o SQL Server</span><span class="sxs-lookup"><span data-stu-id="3c21a-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="3c21a-116">Esta secção descreve vários métodos com o SQL Server tooperform simple aleatória amostragem contra dados Olá na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="3c21a-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="3c21a-117">Escolha um método com base no seu tamanho de dados e a distribuição da mesma.</span><span class="sxs-lookup"><span data-stu-id="3c21a-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="3c21a-118">Olá dois itens abaixo mostram como toouse newid no SQL Server tooperform Olá amostragem.</span><span class="sxs-lookup"><span data-stu-id="3c21a-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="3c21a-119">Olá método que escolher depende aleatórias como pretende toobe de exemplo de Olá (pk_id no código de exemplo de Olá abaixo pressupõe-se toobe uma chave primária gerado automaticamente).</span><span class="sxs-lookup"><span data-stu-id="3c21a-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="3c21a-120">Amostra aleatória menos strict</span><span class="sxs-lookup"><span data-stu-id="3c21a-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="3c21a-121">Amostra aleatória mais</span><span class="sxs-lookup"><span data-stu-id="3c21a-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="3c21a-122">Tablesample pode ser utilizado para a amostragem, bem como demonstrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="3c21a-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="3c21a-123">Isto poderá ser uma abordagem de melhor se o tamanho de dados for grande (assumindo que não estão correlacionados dados em diferentes páginas) e para Olá consulta toocomplete num tempo razoável.</span><span class="sxs-lookup"><span data-stu-id="3c21a-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="3c21a-124">Pode explorar e gerar funcionalidades a partir destes amostras de dados armazenando-os numa nova tabela</span><span class="sxs-lookup"><span data-stu-id="3c21a-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="3c21a-125"><a name="sql-aml"></a>Ligar tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3c21a-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="3c21a-126">Pode utilizar consultas de exemplo de Olá acima diretamente no Azure Machine Learning de Olá [importar dados] [ import-data] dados toodown-exemplo hello módulo Olá viaje até e colocá-la para uma experimentação do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3c21a-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="3c21a-127">Uma captura de ecrã da utilização de dados do Olá leitor módulo tooread Olá amostragem é mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="3c21a-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![leitor sql][1]

## <span data-ttu-id="3c21a-129"><a name="python"></a>Utilizando a linguagem de programação Olá Python</span><span class="sxs-lookup"><span data-stu-id="3c21a-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="3c21a-130">Esta secção demonstra utilizando Olá [pyodbc biblioteca](https://code.google.com/p/pyodbc/) tooestablish um ODBC ligar tooa SQL server da base de dados no Python.</span><span class="sxs-lookup"><span data-stu-id="3c21a-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="3c21a-131">cadeia de ligação de base de dados de Olá é o seguinte: (substitua servername, dbname, nome de utilizador e palavra-passe com a sua configuração):</span><span class="sxs-lookup"><span data-stu-id="3c21a-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="3c21a-132">Olá [Pandas](http://pandas.pydata.org/) biblioteca no Python fornece um conjunto avançado de estruturas de dados e ferramentas de análise de dados para manipulação de dados para a programação do Python.</span><span class="sxs-lookup"><span data-stu-id="3c21a-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="3c21a-133">código de Olá abaixo lê uma amostra de 0.1% de dados de Olá de uma tabela na base de dados SQL do Azure para dados de Pandas:</span><span class="sxs-lookup"><span data-stu-id="3c21a-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="3c21a-134">Agora, pode trabalhar com dados Olá amostragem num intervalo de dados de Pandas Olá.</span><span class="sxs-lookup"><span data-stu-id="3c21a-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="3c21a-135"><a name="python-aml"></a>Ligar tooAzure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3c21a-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="3c21a-136">Pode utilizar Olá seguintes exemplo código toosave Olá dados de objeto de amostragem de baixo tooa ficheiro e carregá-la tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c21a-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="3c21a-137">Olá num blob Olá podem ser diretamente ler dados para uma experimentação do Azure Machine Learning utilizando Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c21a-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="3c21a-138">passos de Olá são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="3c21a-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="3c21a-139">Escrever Olá pandas moldura tooa local ficheiro de dados</span><span class="sxs-lookup"><span data-stu-id="3c21a-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="3c21a-140">Carregar ficheiro local tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="3c21a-140">Upload local file tooAzure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="3c21a-141">Ler dados de Blobs do Azure utilizando o Azure Machine Learning [importar dados] [ import-data] módulo, conforme mostrado no Olá ecrã captar abaixo:</span><span class="sxs-lookup"><span data-stu-id="3c21a-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![blob de leitor][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="3c21a-143">Olá o processo de ciência de dados de equipa no exemplo de ação</span><span class="sxs-lookup"><span data-stu-id="3c21a-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="3c21a-144">Para obter um exemplo de instruções ponto a ponto do Olá o processo de ciência de dados de equipa um utilizando um conjunto de dados público, consulte o artigo [processo de ciência de dados de equipa em ação: utilizar o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="3c21a-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
