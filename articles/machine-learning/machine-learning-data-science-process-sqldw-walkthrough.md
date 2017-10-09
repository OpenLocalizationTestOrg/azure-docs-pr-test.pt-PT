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
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="15a75-103">Olá o processo de ciência de dados de equipa em ação: utilizar o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="15a75-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="15a75-104">Neste tutorial, iremos guiá-lo através de criar e implementar um modelo de machine learning utilizar o SQL Data Warehouse (armazém de dados do SQL Server) para um conjunto de dados publicamente disponível – hello [NYC Taxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="15a75-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="15a75-105">modelo de classificação binária Olá construído prevê ou não uma sugestão é paga para uma viagem e modelos para classificação de várias classes e regressão também são abordados que prever distribuição Olá para quantidades de sugestão de Olá pagas.</span><span class="sxs-lookup"><span data-stu-id="15a75-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="15a75-106">procedimento Olá segue Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="15a75-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="15a75-107">Vamos mostrar como toosetup num ambiente de ciência de dados, como tooload Olá dados no armazém de dados do SQL Server e como utilizar o armazém de dados do SQL Server ou um Olá de tooexplore IPython bloco de notas em dados e engenheiro a toomodel funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="15a75-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="15a75-108">Em seguida, mostramos como toobuild e implementar um modelo com o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15a75-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="15a75-109"><a name="dataset"></a>o conjunto de dados do Olá NYC Taxi viagens</span><span class="sxs-lookup"><span data-stu-id="15a75-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="15a75-110">Olá dados NYC Taxi viagem consiste em cerca de 20GB de ficheiros CSV comprimidos (GB de ~ 48 descomprimido), mais de 173 milhões de gravação viagens individuais e Olá fares paga para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="15a75-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="15a75-111">Cada registo viagem inclui localizações de recolha e drop-off Olá e vezes, são anónimos hack número de licença (controlador) e Olá número medallion (id exclusivo do taxi).</span><span class="sxs-lookup"><span data-stu-id="15a75-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="15a75-112">dados Olá abrange todos os viagens no ano de Olá 2013 e são fornecidos na Olá seguir dois conjuntos de dados de cada mês:</span><span class="sxs-lookup"><span data-stu-id="15a75-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="15a75-113">Olá **trip_data.csv** ficheiro contém detalhes viagem, tais como o número de passageiros, recolha e dropoff pontos, duração de viagem e comprimento viagem.</span><span class="sxs-lookup"><span data-stu-id="15a75-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="15a75-114">Seguem-se alguns registos de exemplo:</span><span class="sxs-lookup"><span data-stu-id="15a75-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="15a75-115">Olá **trip_fare.csv** ficheiro contém detalhes de fare Olá paga para cada viagem, tais como o tipo de pagamento, a quantidade de fare, surcharge e taxas, sugestões e tolls e quantidade total de Olá paga.</span><span class="sxs-lookup"><span data-stu-id="15a75-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="15a75-116">Seguem-se alguns registos de exemplo:</span><span class="sxs-lookup"><span data-stu-id="15a75-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="15a75-117">Olá **chave exclusiva** utilizado toojoin viagem\_dados e viagem\_fare é composto por Olá seguintes três campos:</span><span class="sxs-lookup"><span data-stu-id="15a75-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="15a75-118">Medallion,</span><span class="sxs-lookup"><span data-stu-id="15a75-118">medallion,</span></span>
* <span data-ttu-id="15a75-119">Hack\_licença e</span><span class="sxs-lookup"><span data-stu-id="15a75-119">hack\_license and</span></span>
* <span data-ttu-id="15a75-120">recolha\_datetime.</span><span class="sxs-lookup"><span data-stu-id="15a75-120">pickup\_datetime.</span></span>

## <span data-ttu-id="15a75-121"><a name="mltasks"></a>Três tipos de tarefas de predição de endereços</span><span class="sxs-lookup"><span data-stu-id="15a75-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="15a75-122">Iremos formular três problemas de predição com base no Olá *sugestão\_quantidade* tooillustrate três tipos de modelação tarefas:</span><span class="sxs-lookup"><span data-stu-id="15a75-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="15a75-123">**Classificação binária**: toopredict ou não em que uma sugestão foi paga ou seja, para uma viagem, um *sugestão\_quantidade* que é superior ao $0 é um exemplo positivo, enquanto um *sugestão\_quantidade* $ 0 é um exemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="15a75-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="15a75-124">**Classificação de várias classes**: intervalo de Olá toopredict de sugestão paga para viagem Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="15a75-125">Iremos dividir Olá *sugestão\_quantidade* em cinco intervalos binários ou classes:</span><span class="sxs-lookup"><span data-stu-id="15a75-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="15a75-126">**Tarefa de regressão**: quantidade de Olá toopredict de sugestão paga para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="15a75-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="15a75-127"><a name="setup"></a>Configurar o ambiente de ciência de dados do Azure Olá para análise avançada</span><span class="sxs-lookup"><span data-stu-id="15a75-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="15a75-128">tooset configurar o ambiente de ciência de dados do Azure, siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="15a75-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="15a75-129">**Criar a sua própria conta de armazenamento de Blobs do Azure**</span><span class="sxs-lookup"><span data-stu-id="15a75-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="15a75-130">Quando aprovisionar o seu próprio armazenamento de Blobs do Azure, escolha uma localização de georreplicação para o armazenamento de Blobs do Azure em ou mais parecida possível demasiado**Sul Central nos**, que é onde está armazenada Olá dados NYC Taxi.</span><span class="sxs-lookup"><span data-stu-id="15a75-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="15a75-131">Olá dados serão copiados utilizando o AzCopy do contentor de tooa de contentor de armazenamento de BLOBs público de Olá na sua própria conta do storage.</span><span class="sxs-lookup"><span data-stu-id="15a75-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="15a75-132">Olá próximo do armazenamento de Blobs do Azure é EUA Central tooSouth, hello mais rapidamente esta tarefa (passo 4) será concluída.</span><span class="sxs-lookup"><span data-stu-id="15a75-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="15a75-133">toocreate o seus próprios storage do Azure da conta, Olá siga os passos descritos em [contas do storage do Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="15a75-134">Ser se toomake notas sobre Olá os valores para as credenciais da conta de armazenamento seguintes, irá ser necessário posteriormente nestas instruções.</span><span class="sxs-lookup"><span data-stu-id="15a75-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="15a75-135">**Nome da conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="15a75-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="15a75-136">**Chave de conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="15a75-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="15a75-137">**Nome do contentor** (que quiser Olá toobe de dados armazenado no blob storage do Azure de Olá)</span><span class="sxs-lookup"><span data-stu-id="15a75-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="15a75-138">**Aprovisione a instância de armazém de dados do Azure SQL.**</span><span class="sxs-lookup"><span data-stu-id="15a75-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="15a75-139">Siga a documentação de Olá em [criar um SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision uma instância do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="15a75-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="15a75-140">Certifique-se de que efetua notações no Olá seguir as credenciais do SQL Data Warehouse que serão utilizadas em passos posteriores.</span><span class="sxs-lookup"><span data-stu-id="15a75-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="15a75-141">**Nome do servidor**: <server Name>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="15a75-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="15a75-142">**Nome SQLDW (base de dados)**</span><span class="sxs-lookup"><span data-stu-id="15a75-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="15a75-143">**Nome de Utilizador**</span><span class="sxs-lookup"><span data-stu-id="15a75-143">**Username**</span></span>
* <span data-ttu-id="15a75-144">**Palavra-passe**</span><span class="sxs-lookup"><span data-stu-id="15a75-144">**Password**</span></span>

<span data-ttu-id="15a75-145">**Instale Visual Studio e ferramentas de dados do SQL Server.**</span><span class="sxs-lookup"><span data-stu-id="15a75-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="15a75-146">Para obter instruções, consulte [instalar o Visual Studio 2015 e/ou o SSDT (SQL Server Data Tools) para o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="15a75-147">**Ligar tooyour armazém de dados do Azure SQL com o Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="15a75-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="15a75-148">Para obter instruções, consulte os passos 1 e 2 no [ligar tooAzure SQL Data Warehouse com o Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="15a75-149">Execute hello seguinte consulta SQL na base de dados de Olá que criou no SQL Data Warehouse (em vez de consulta Olá fornecida no passo 3 do Olá ligar tópico,) demasiado**criar uma chave mestra**.</span><span class="sxs-lookup"><span data-stu-id="15a75-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="15a75-150">**Crie uma área de trabalho do Azure Machine Learning na sua subscrição do Azure.**</span><span class="sxs-lookup"><span data-stu-id="15a75-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="15a75-151">Para obter instruções, consulte [criar uma área de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="15a75-152"><a name="getdata"></a>Carregar dados de Olá para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="15a75-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="15a75-153">Abra uma consola de comandos do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15a75-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="15a75-154">Execute o seguinte de Olá comandos do PowerShell toodownload Olá exemplo SQL ficheiros de script que partilhamos no GitHub tooa diretório local que especificou com o parâmetro Olá *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="15a75-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="15a75-155">Pode alterar Olá valor do parâmetro *- DestDir* tooany de diretório local.</span><span class="sxs-lookup"><span data-stu-id="15a75-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="15a75-156">Se *- DestDir* não existir, será criado pelo Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15a75-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="15a75-157">Poderá ser necessário demasiado**executar como administrador** ao executar Olá seguinte script do PowerShell se o *DestDir* directory precisar tooit de toocreate ou toowrite de privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="15a75-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="15a75-158">Após a execução com êxito, o atual diretório de trabalho alterado demasiado*- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="15a75-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="15a75-159">Deve ser capaz de ecrã de toosee como abaixo:</span><span class="sxs-lookup"><span data-stu-id="15a75-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="15a75-160">No seu *- DestDir*, executar Olá seguinte script do PowerShell no modo de administrador:</span><span class="sxs-lookup"><span data-stu-id="15a75-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="15a75-161">Quando executa Olá script do PowerShell para Olá pela primeira vez, será pedido informações de Olá tooinput do seu armazém de dados de SQL do Azure e a sua conta de armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="15a75-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="15a75-162">Quando tiver concluído este script do PowerShell em execução para Olá a primeira vez, credenciais de Olá entrada será escrita o ficheiro de configuração de tooa SQLDW.conf no diretório de trabalho presente Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="15a75-163">Olá executar futura deste ficheiro de script do PowerShell tem Olá opção tooread necessárias de todos os parâmetros deste ficheiro de configuração.</span><span class="sxs-lookup"><span data-stu-id="15a75-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="15a75-164">Se precisar de toochange alguns parâmetros, pode escolher tooinput parâmetros Olá no ecrã de Olá após a linha ao eliminar este ficheiro de configuração e inputting valores de parâmetros de Olá, conforme solicitado ou valores de parâmetros de Olá toochange editando Olá SQLDW.conf ficheiro no seu *- DestDir* diretório.</span><span class="sxs-lookup"><span data-stu-id="15a75-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="15a75-165">Na ordem tooavoid esquema nome entra em conflito com as que já existem no armazém de dados do SQL do Azure, quando a ler parâmetros diretamente a partir do ficheiro de SQLDW.conf Olá, 3 dígitos aleatório é adicionado um número toohello nome de esquema do ficheiro de SQLDW.conf Olá como nome de esquema predefinido Olá para cada execução.</span><span class="sxs-lookup"><span data-stu-id="15a75-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="15a75-166">Olá script do PowerShell pode solicitar-lhe um nome de esquema: pode ser especificado o nome de Olá critério de utilizador.</span><span class="sxs-lookup"><span data-stu-id="15a75-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="15a75-167">Isto **script do PowerShell** ficheiro conclui Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="15a75-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="15a75-168">**Transfere e instala o AzCopy**, se o AzCopy já não está instalado</span><span class="sxs-lookup"><span data-stu-id="15a75-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
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
* <span data-ttu-id="15a75-169">**Copia a conta de armazenamento de BLOBs privada de tooyour dados** a partir do blob público de Olá com AzCopy</span><span class="sxs-lookup"><span data-stu-id="15a75-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="15a75-170">**Carrega dados utilizando o Polybase (executando LoadDataToSQLDW.sql) tooyour armazém de dados do Azure SQL** da sua conta de armazenamento de BLOBs privada com Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="15a75-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="15a75-171">Criar um esquema</span><span class="sxs-lookup"><span data-stu-id="15a75-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="15a75-172">Criar uma credencial com âmbito de base de dados</span><span class="sxs-lookup"><span data-stu-id="15a75-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="15a75-173">Criar uma origem de dados externo para um blob de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="15a75-173">Create an external data source for an Azure storage blob</span></span>
    
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
  * <span data-ttu-id="15a75-174">Crie um formato de ficheiro externo para um ficheiro csv.</span><span class="sxs-lookup"><span data-stu-id="15a75-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="15a75-175">Os dados são descomprimidos e os campos são separados com caráter de pipe Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
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
  * <span data-ttu-id="15a75-176">Crie tabelas de viagem para o conjunto de dados do NYC taxi e fare externo no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="15a75-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
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

    - <span data-ttu-id="15a75-177">Carregar dados das tabelas externas no armazenamento de Blobs do Azure tooSQL do armazém de dados</span><span class="sxs-lookup"><span data-stu-id="15a75-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

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

    - <span data-ttu-id="15a75-178">Criar uma tabela de dados de exemplo (NYCTaxi_Sample) e inserir dados tooit de selecionar as consultas SQL em tabelas de viagem e fare Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="15a75-179">(Alguns passos destas instruções necessita toouse nesta tabela de exemplo.)</span><span class="sxs-lookup"><span data-stu-id="15a75-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

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

<span data-ttu-id="15a75-180">localização geográfica de Olá das suas contas de armazenamento afeta tempos de carregamento.</span><span class="sxs-lookup"><span data-stu-id="15a75-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="15a75-181">Consoante Olá localização geográfica da conta de armazenamento de BLOBs privada, o processo de Olá de cópia de dados de uma conta de armazenamento privada do blob público tooyour pode demorar cerca de 15 minutos ou processar o mesmo já e hello de carregamento dos dados da sua conta de armazenamento tooyour armazém de dados do Azure SQL, pode demorar de 20 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="15a75-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="15a75-182">Tem de toodecide o que fazer se tiver origem duplicada e ficheiros de destino.</span><span class="sxs-lookup"><span data-stu-id="15a75-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="15a75-183">Se toobe ficheiros. csv de Olá copiado a partir da conta de armazenamento de BLOBs privada armazenamento tooyour Olá blob público já existir na sua conta de armazenamento de BLOBs privada, AzCopy irá pedir-lhe se pretende toooverwrite-los.</span><span class="sxs-lookup"><span data-stu-id="15a75-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="15a75-184">Se não pretender toooverwrite-las, entrada  **n**  quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="15a75-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="15a75-185">Se quiser toooverwrite **todos os** dos mesmos, de entrada **um** quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="15a75-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="15a75-186">Também pode introduzir **y** . csv de toooverwrite ficheiros individualmente.</span><span class="sxs-lookup"><span data-stu-id="15a75-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![Desenhar #21][21]

<span data-ttu-id="15a75-188">Pode utilizar os seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="15a75-188">You can use your own data.</span></span> <span data-ttu-id="15a75-189">Se os dados na sua máquina no local na sua aplicação de vida real, pode continuar a utilizar AzCopy tooupload no local dados tooyour privada blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="15a75-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="15a75-190">Só precisa de toochange Olá **origem** localização, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, no Olá comandos do AzCopy de Olá PowerShell script toohello local diretório do ficheiro que contenha os dados.</span><span class="sxs-lookup"><span data-stu-id="15a75-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="15a75-191">Se os dados já existir no seu armazenamento de Blobs do Azure privada na sua aplicação de vida real, pode ignorar Olá AzCopy passo na Olá script do PowerShell e o carregar diretamente Olá dados tooAzure armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="15a75-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="15a75-192">Isto irá necessitar adicionais edita de Olá script tootailor-toohello formato dos seus dados.</span><span class="sxs-lookup"><span data-stu-id="15a75-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="15a75-193">Este script do Powershell plugs também no Olá informações do armazém de dados do Azure SQL Olá exploração exemplo para ficheiros de dados SQLDW_Explorations.sql, SQLDW_Explorations.ipynb e SQLDW_Explorations_Scripts.py para que estes três ficheiros estejam toobe pronto tentou instantaneamente após a conclusão da Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15a75-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="15a75-194">Após uma execução bem sucedida, verá o ecrã, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="15a75-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="15a75-195"><a name="dbexplore"></a>Exploração de dados e de engenharia da funcionalidade no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="15a75-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="15a75-196">Nesta secção, iremos executar geração de exploração e funcionalidade de dados através da execução de consultas SQL no armazém de dados do SQL do Azure diretamente utilizando **ferramentas de dados do Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="15a75-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="15a75-197">Todas as consultas de SQL Server utilizadas nesta secção podem ser encontradas no script de exemplo de Olá denominado *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="15a75-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="15a75-198">Este ficheiro já foi transferido tooyour diretório local pelo script de PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="15a75-199">Também pode obter a [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="15a75-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="15a75-200">Mas ficheiro Olá no GitHub, não dispõe de informações do armazém de dados do Azure SQL Olá ligadas.</span><span class="sxs-lookup"><span data-stu-id="15a75-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="15a75-201">Ligar tooyour armazém de dados do SQL do Azure com o Visual Studio com o nome de início de sessão do armazém de dados do SQL Server Olá e a palavra-passe e abrir Olá **SQL Server Object Explorer** base de dados do tooconfirm Olá e tabelas foram importadas.</span><span class="sxs-lookup"><span data-stu-id="15a75-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="15a75-202">Obter Olá *SQLDW_Explorations.sql* ficheiro.</span><span class="sxs-lookup"><span data-stu-id="15a75-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="15a75-203">tooopen um editor de consultas do armazém de dados paralelo (PDW), utilize Olá **nova consulta** comando enquanto o PDW está selecionado na Olá **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="15a75-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="15a75-204">editor de consultas de SQL Server standard Olá não é suportado pelo PDW.</span><span class="sxs-lookup"><span data-stu-id="15a75-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="15a75-205">Seguem-se o tipo de Olá de dados efetuar tarefas de geração de exploração e funcionalidade nesta secção:</span><span class="sxs-lookup"><span data-stu-id="15a75-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="15a75-206">Explore as distribuições de dados de alguns campos no variando intervalos de tempo.</span><span class="sxs-lookup"><span data-stu-id="15a75-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="15a75-207">Investigue a qualidade dos dados de campos de latitude e longitude de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="15a75-208">Gerar etiquetas de classificação de várias classes e binária com base no Olá **sugestão\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="15a75-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="15a75-209">Gerar funcionalidades e computação/comparar as distâncias de viagem.</span><span class="sxs-lookup"><span data-stu-id="15a75-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="15a75-210">Associar tabelas Olá dois e extrair amostra aleatória que será utilizado toobuild modelos.</span><span class="sxs-lookup"><span data-stu-id="15a75-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="15a75-211">Verificação de importação de dados</span><span class="sxs-lookup"><span data-stu-id="15a75-211">Data import verification</span></span>
<span data-ttu-id="15a75-212">Estas consultas fornecem uma verificação rápida do número de Olá de linhas e colunas no Olá tabelas povoadas anteriormente utilizando em massa de paralela do Polybase importar,</span><span class="sxs-lookup"><span data-stu-id="15a75-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="15a75-213">**Saída:** deve obter 173,179,759 linhas e colunas de 14.</span><span class="sxs-lookup"><span data-stu-id="15a75-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="15a75-214">Exploração: Distribuição de viagem por medallion</span><span class="sxs-lookup"><span data-stu-id="15a75-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="15a75-215">Esta consulta de exemplo identifica medallions Olá (taxi números) concluir mais do que 100 viagens dentro do período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="15a75-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="15a75-216">consulta de Olá seria beneficiar de acesso de tabela Olá particionada desde que está a ter pelo esquema de partição Olá da **recolha\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="15a75-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="15a75-217">Consultar o conjunto de dados completo Olá também faz com que a utilização de tabela particionada Olá e/ou a análise de índice.</span><span class="sxs-lookup"><span data-stu-id="15a75-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="15a75-218">**Saída:** consulta Olá deve devolver uma tabela com linhas especificando medallions Olá 13,369 (taxis) e Olá diversas viagem concluída no 2013.</span><span class="sxs-lookup"><span data-stu-id="15a75-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="15a75-219">a coluna último Olá contém uma contagem de Olá do número de Olá de viagens foi concluída.</span><span class="sxs-lookup"><span data-stu-id="15a75-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="15a75-220">Exploração: Distribuição de viagem medallion e hack_license</span><span class="sxs-lookup"><span data-stu-id="15a75-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="15a75-221">Neste exemplo identifica medallions Olá (taxi números) e hack_license números (controladores do) que foram concluídos mais do que 100 viagens durante um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="15a75-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="15a75-222">**Saída:** consulta Olá deve devolver uma tabela com 13,369 linhas especificando Olá 13,369 carro/controlador IDs concluiu mais esse viagens 100 em 2013.</span><span class="sxs-lookup"><span data-stu-id="15a75-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="15a75-223">a coluna último Olá contém uma contagem de Olá do número de Olá de viagens foi concluída.</span><span class="sxs-lookup"><span data-stu-id="15a75-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="15a75-224">Avaliação de qualidade de dados: verificar os registos com incorreto longitude e/ou latitude</span><span class="sxs-lookup"><span data-stu-id="15a75-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="15a75-225">Neste exemplo investiga se qualquer um dos campos de longitude e/ou latitude Olá ou contém um valor inválido (radian graus devem ser entre -90 e 90), ou ter (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="15a75-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="15a75-226">**Saída:** consulta Olá devolve 837,467 viagens com campos de longitude e/ou latitude inválidos.</span><span class="sxs-lookup"><span data-stu-id="15a75-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="15a75-227">Exploração: Tipped vs distribuição viagens não tipped</span><span class="sxs-lookup"><span data-stu-id="15a75-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="15a75-228">Neste exemplo localiza o número de Olá de viagens foram tipped vs número Olá que não foram tipped num período de tempo especificado (ou em Olá conjunto de dados completo se que abrangem ano completa Olá, que está definido aqui).</span><span class="sxs-lookup"><span data-stu-id="15a75-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="15a75-229">Esta distribuição reflete Olá etiqueta binário distribuição toobe posteriormente utilizado para a modelação de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="15a75-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="15a75-230">**Saída:** Olá consulta deve seguinte Olá retorno sugestão frequências para o ano de Olá 2013: 90,447,622 tipped e 82,264,709 tipped em não.</span><span class="sxs-lookup"><span data-stu-id="15a75-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="15a75-231">Exploração: Distribuição de classe/intervalo de sugestão</span><span class="sxs-lookup"><span data-stu-id="15a75-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="15a75-232">Neste exemplo calcula a distribuição de Olá de intervalos de sugestão num determinado momento período (ou em Olá conjunto de dados completo se que abrangem ano completa Olá).</span><span class="sxs-lookup"><span data-stu-id="15a75-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="15a75-233">Esta é a distribuição de Olá das classes de etiqueta Olá que serão utilizados mais tarde para a modelação de classificação de várias classes.</span><span class="sxs-lookup"><span data-stu-id="15a75-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

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

<span data-ttu-id="15a75-234">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="15a75-234">**Output:**</span></span>

| <span data-ttu-id="15a75-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="15a75-235">tip_class</span></span> | <span data-ttu-id="15a75-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="15a75-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="15a75-237">1</span><span class="sxs-lookup"><span data-stu-id="15a75-237">1</span></span> |<span data-ttu-id="15a75-238">82230915</span><span class="sxs-lookup"><span data-stu-id="15a75-238">82230915</span></span> |
| <span data-ttu-id="15a75-239">2</span><span class="sxs-lookup"><span data-stu-id="15a75-239">2</span></span> |<span data-ttu-id="15a75-240">6198803</span><span class="sxs-lookup"><span data-stu-id="15a75-240">6198803</span></span> |
| <span data-ttu-id="15a75-241">3</span><span class="sxs-lookup"><span data-stu-id="15a75-241">3</span></span> |<span data-ttu-id="15a75-242">1932223</span><span class="sxs-lookup"><span data-stu-id="15a75-242">1932223</span></span> |
| <span data-ttu-id="15a75-243">0</span><span class="sxs-lookup"><span data-stu-id="15a75-243">0</span></span> |<span data-ttu-id="15a75-244">82264625</span><span class="sxs-lookup"><span data-stu-id="15a75-244">82264625</span></span> |
| <span data-ttu-id="15a75-245">4</span><span class="sxs-lookup"><span data-stu-id="15a75-245">4</span></span> |<span data-ttu-id="15a75-246">85765</span><span class="sxs-lookup"><span data-stu-id="15a75-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="15a75-247">Exploração: Computação e comparar distância viagem</span><span class="sxs-lookup"><span data-stu-id="15a75-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="15a75-248">Neste exemplo converte longitude de recolha e drop-off Olá e pontos de geografia de tooSQL latitude, calcula distância de viagem Olá utilizando a diferença de pontos de geografia SQL e devolve uma amostra aleatória de resultados de Olá para comparação.</span><span class="sxs-lookup"><span data-stu-id="15a75-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="15a75-249">exemplo de Olá limita os resultados de Olá toovalid coordena a utilizar apenas Olá qualidade assessment a consulta de dados abrangida anteriormente.</span><span class="sxs-lookup"><span data-stu-id="15a75-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

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

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="15a75-250">Engenharia da funcionalidade utilizando funções do SQL Server</span><span class="sxs-lookup"><span data-stu-id="15a75-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="15a75-251">Por vezes, as funções do SQL Server podem ser uma opção eficiente para engenharia da funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="15a75-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="15a75-252">Nestas instruções, iremos definido uma SQL Server função toocalculate Olá direta distância entre localizações de recolha e dropoff Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="15a75-253">Pode executar Olá seguintes scripts do SQL Server no **ferramentas de dados do Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="15a75-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="15a75-254">Eis o script SQL Olá que define a função de distância Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-254">Here is hello SQL script that defines hello distance function.</span></span>

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

<span data-ttu-id="15a75-255">Eis um exemplo toocall funcionalidades de toogenerate esta função na sua consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="15a75-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="15a75-256">**Saída:** esta consulta gera uma tabela (com 2,803,538 linhas) com a recolha e dropoff latitudes e longitudes e Olá correspondente direcionam as distâncias em quilómetros.</span><span class="sxs-lookup"><span data-stu-id="15a75-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="15a75-257">Seguem-se os resultados de Olá primeiros 3 linhas:</span><span class="sxs-lookup"><span data-stu-id="15a75-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="15a75-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="15a75-258">pickup_latitude</span></span> | <span data-ttu-id="15a75-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="15a75-259">pickup_longitude</span></span> | <span data-ttu-id="15a75-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="15a75-260">dropoff_latitude</span></span> | <span data-ttu-id="15a75-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="15a75-261">dropoff_longitude</span></span> | <span data-ttu-id="15a75-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="15a75-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="15a75-263">1</span><span class="sxs-lookup"><span data-stu-id="15a75-263">1</span></span> |<span data-ttu-id="15a75-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="15a75-264">40.731804</span></span> |<span data-ttu-id="15a75-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="15a75-265">-74.001083</span></span> |<span data-ttu-id="15a75-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="15a75-266">40.736622</span></span> |<span data-ttu-id="15a75-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="15a75-267">-73.988953</span></span> |<span data-ttu-id="15a75-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="15a75-268">.7169601222</span></span> |
| <span data-ttu-id="15a75-269">2</span><span class="sxs-lookup"><span data-stu-id="15a75-269">2</span></span> |<span data-ttu-id="15a75-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="15a75-270">40.715794</span></span> |<span data-ttu-id="15a75-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="15a75-271">-74,010635</span></span> |<span data-ttu-id="15a75-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="15a75-272">40.725338</span></span> |<span data-ttu-id="15a75-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="15a75-273">-74.00399</span></span> |<span data-ttu-id="15a75-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="15a75-274">.7448343721</span></span> |
| <span data-ttu-id="15a75-275">3</span><span class="sxs-lookup"><span data-stu-id="15a75-275">3</span></span> |<span data-ttu-id="15a75-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="15a75-276">40.761456</span></span> |<span data-ttu-id="15a75-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="15a75-277">-73.999886</span></span> |<span data-ttu-id="15a75-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="15a75-278">40.766544</span></span> |<span data-ttu-id="15a75-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="15a75-279">-73.988228</span></span> |<span data-ttu-id="15a75-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="15a75-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="15a75-281">Preparar a criação de modelo de dados</span><span class="sxs-lookup"><span data-stu-id="15a75-281">Prepare data for model building</span></span>
<span data-ttu-id="15a75-282">Olá associações de consulta seguinte Olá **nyctaxi\_viagem** e **nyctaxi\_fare** tabelas, gera uma etiqueta de classificação binária **tipped**, um etiqueta de classificação de classe Multi **sugestão\_classe**e extrai um exemplo de Olá conjunto de dados completo associados.</span><span class="sxs-lookup"><span data-stu-id="15a75-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="15a75-283">a amostragem Olá é feita ao aceder a um subconjunto de viagens Olá com base na hora de recolha.</span><span class="sxs-lookup"><span data-stu-id="15a75-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="15a75-284">Esta consulta pode ser copiada e colada diretamente no Olá [Azure Machine Learning Studio](https://studio.azureml.net) [importar dados] [ import-data] módulo para a ingestão de dados direta de instância de base de dados do SQL Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="15a75-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="15a75-285">consulta de Olá exclui registos com incorreto (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="15a75-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

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

<span data-ttu-id="15a75-286">Quando estiver pronto tooproceed tooAzure Machine Learning, o utilizador pode optar por:</span><span class="sxs-lookup"><span data-stu-id="15a75-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="15a75-287">Guardar Olá final SQL tooextract e exemplo Olá dados e copiar-colar Olá consulta diretamente para um [importar dados] [ import-data] módulo no Azure Machine Learning, ou</span><span class="sxs-lookup"><span data-stu-id="15a75-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="15a75-288">Manter Olá amostragem e foi desenvolvidos dados planear toouse para criação de um novo armazém de dados do SQL Server do modelo de tabela e utilizam a nova tabela de Olá no Olá [importar dados] [ import-data] módulo no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15a75-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="15a75-289">Olá script do PowerShell no passo anterior execute este procedimento para si.</span><span class="sxs-lookup"><span data-stu-id="15a75-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="15a75-290">Pode ler diretamente a partir desta tabela no módulo de importar dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="15a75-291"><a name="ipnb"></a>Exploração de dados e de engenharia da funcionalidade no bloco de notas do IPython</span><span class="sxs-lookup"><span data-stu-id="15a75-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="15a75-292">Nesta secção, iremos efetuar exploração de dados e a geração de funcionalidade utilizando ambos os Python e as consultas SQL contra Olá armazém de dados do SQL Server criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="15a75-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="15a75-293">Um exemplo IPython bloco de notas com o nome **SQLDW_Explorations.ipynb** e um ficheiro de script de Python **SQLDW_Explorations_Scripts.py** ter sido transferido tooyour diretório local.</span><span class="sxs-lookup"><span data-stu-id="15a75-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="15a75-294">Também estão disponíveis no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="15a75-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="15a75-295">Estes dois ficheiros são idênticos em Python scripts.</span><span class="sxs-lookup"><span data-stu-id="15a75-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="15a75-296">ficheiro de script de Python Olá é fornecido tooyou no caso de não dispõe de um servidor de IPython bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="15a75-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="15a75-297">Estes dois exemplos Python ficheiros concebidos em **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="15a75-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="15a75-298">Olá informações necessárias do armazém de dados do Azure SQL no exemplo Olá IPython bloco de notas e Olá Python máquina local de tooyour transferido do ficheiro de script tenha sido ligada pelo script de PowerShell Olá anteriormente.</span><span class="sxs-lookup"><span data-stu-id="15a75-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="15a75-299">São executáveis sem qualquer modificação.</span><span class="sxs-lookup"><span data-stu-id="15a75-299">They are executable without any modification.</span></span>

<span data-ttu-id="15a75-300">Se já tiver configurado uma área de trabalho do AzureML, diretamente pode carregar o exemplo de Olá serviço de bloco de notas do AzureML IPython do bloco de notas IPython toohello e iniciar a executá-lo.</span><span class="sxs-lookup"><span data-stu-id="15a75-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="15a75-301">Seguem-se Olá passos tooupload tooAzureML serviço IPython bloco de notas:</span><span class="sxs-lookup"><span data-stu-id="15a75-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="15a75-302">Inicie sessão na área de trabalho do tooyour AzureML, clique em "Studio" na parte superior do Olá e clique em "PORTÁTEIS" no lado esquerdo do Olá da página web de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![Desenhar #22][22]
2. <span data-ttu-id="15a75-304">Clique em "Novo" no canto inferior esquerdo de Olá da página web de Olá e selecione "Python 2".</span><span class="sxs-lookup"><span data-stu-id="15a75-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="15a75-305">Em seguida, forneça um bloco de notas do nome toohello e clique em Olá marca de verificação toocreate Olá nova em branco IPython bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="15a75-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![Desenhar #23][23]
3. <span data-ttu-id="15a75-307">Clique em Símbolo de "Jupyter" Olá no canto superior esquerdo do Olá Olá novo IPython bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="15a75-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![Desenhar #24][24]
4. <span data-ttu-id="15a75-309">Arrastar e largar toohello de IPython bloco de notas do exemplo Olá **árvore** página do seu serviço de bloco de notas do AzureML IPython e clique em **carregar**.</span><span class="sxs-lookup"><span data-stu-id="15a75-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="15a75-310">Em seguida, o exemplo de Olá IPython bloco de notas será carregado toohello serviço bloco de notas do AzureML IPython.</span><span class="sxs-lookup"><span data-stu-id="15a75-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![Desenhar #25][25]

<span data-ttu-id="15a75-312">No Olá toorun de ordem de exemplo IPython bloco de notas ou Olá o ficheiro de script de Python, hello seguintes pacotes de Python são necessários.</span><span class="sxs-lookup"><span data-stu-id="15a75-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="15a75-313">Se estiver a utilizar o serviço de bloco de notas do AzureML IPython Olá, estes pacotes foram instalados previamente.</span><span class="sxs-lookup"><span data-stu-id="15a75-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="15a75-314">pandas</span><span class="sxs-lookup"><span data-stu-id="15a75-314">pandas</span></span>
    - <span data-ttu-id="15a75-315">numpy</span><span class="sxs-lookup"><span data-stu-id="15a75-315">numpy</span></span>
    - <span data-ttu-id="15a75-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="15a75-316">matplotlib</span></span>
    - <span data-ttu-id="15a75-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="15a75-317">pyodbc</span></span>
    - <span data-ttu-id="15a75-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="15a75-318">PyTables</span></span>

<span data-ttu-id="15a75-319">Olá recomendado sequência quando criar soluções de analíticas avançadas em AzureML com dados de grandes dimensões é a seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="15a75-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="15a75-320">Ler um exemplo de dados de Olá pequeno para um intervalo de dados em memória.</span><span class="sxs-lookup"><span data-stu-id="15a75-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="15a75-321">Efetuar algumas visualizações e explorations utilizando Olá amostras de dados.</span><span class="sxs-lookup"><span data-stu-id="15a75-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="15a75-322">Experimentar a engenharia da funcionalidade utilizando dados Olá amostragem.</span><span class="sxs-lookup"><span data-stu-id="15a75-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="15a75-323">Exploração de dados maior, manipulação de dados e de engenharia da funcionalidade, utilize Python tooissue SQL consultas diretamente Olá armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="15a75-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="15a75-324">Decida toobe de tamanho de exemplo de Olá adequado para a criação de modelo do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15a75-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="15a75-325">seguinte Olá é alguns dados exploração, visualização de dados e exemplos de engenharia da funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="15a75-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="15a75-326">Mais explorations de dados podem ser encontrados no exemplo Olá IPython bloco de notas e ficheiro de script de Python de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="15a75-327">Inicializar as credenciais da base de dados</span><span class="sxs-lookup"><span data-stu-id="15a75-327">Initialize database credentials</span></span>
<span data-ttu-id="15a75-328">Inicializar as definições de ligação de base de dados no Olá seguintes variáveis:</span><span class="sxs-lookup"><span data-stu-id="15a75-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="15a75-329">Criar a ligação de base de dados</span><span class="sxs-lookup"><span data-stu-id="15a75-329">Create database connection</span></span>
<span data-ttu-id="15a75-330">Segue-se a cadeia de ligação de Olá que cria a base de dados do Olá ligação toohello.</span><span class="sxs-lookup"><span data-stu-id="15a75-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="15a75-331">Número de relatório de linhas e colunas na tabela < nyctaxi_trip ></span><span class="sxs-lookup"><span data-stu-id="15a75-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
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

* <span data-ttu-id="15a75-332">Número total de linhas = 173179759</span><span class="sxs-lookup"><span data-stu-id="15a75-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="15a75-333">Número total de colunas = 14</span><span class="sxs-lookup"><span data-stu-id="15a75-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="15a75-334">Número de relatório de linhas e colunas na tabela < nyctaxi_fare ></span><span class="sxs-lookup"><span data-stu-id="15a75-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
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

* <span data-ttu-id="15a75-335">Número total de linhas = 173179759</span><span class="sxs-lookup"><span data-stu-id="15a75-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="15a75-336">Número total de colunas = 11</span><span class="sxs-lookup"><span data-stu-id="15a75-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="15a75-337">Leia-in de uma amostra de dados de pequena de Olá a base de dados do armazém de dados SQL</span><span class="sxs-lookup"><span data-stu-id="15a75-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
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

<span data-ttu-id="15a75-338">Tabela de exemplo do tempo tooread Olá é 14.096495 segundos.</span><span class="sxs-lookup"><span data-stu-id="15a75-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="15a75-339">Número de linhas e colunas obter = (1000, 21).</span><span class="sxs-lookup"><span data-stu-id="15a75-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="15a75-340">Estatísticas descritivas</span><span class="sxs-lookup"><span data-stu-id="15a75-340">Descriptive statistics</span></span>
<span data-ttu-id="15a75-341">Agora, está pronto tooexplore dados de Olá amostragem.</span><span class="sxs-lookup"><span data-stu-id="15a75-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="15a75-342">Vamos começar a utilizar ao procurar algumas estatísticas descritivas para Olá **viagem\_distância** (ou quaisquer outros campos escolher toospecify).</span><span class="sxs-lookup"><span data-stu-id="15a75-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="15a75-343">Visualização: Exemplo de desenho de caixa</span><span class="sxs-lookup"><span data-stu-id="15a75-343">Visualization: Box plot example</span></span>
<span data-ttu-id="15a75-344">Em seguida vamos ver desenho de caixa de Olá para Olá viagem distância toovisualize Olá quantiles.</span><span class="sxs-lookup"><span data-stu-id="15a75-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Desenhar #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="15a75-346">Visualização: Exemplo de desenho de distribuição</span><span class="sxs-lookup"><span data-stu-id="15a75-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="15a75-347">Plots visualizar distribuição Olá e um histograma para as distâncias viagem de Olá amostragem.</span><span class="sxs-lookup"><span data-stu-id="15a75-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Desenhar #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="15a75-349">Barra de visualização: E rastreia de linha</span><span class="sxs-lookup"><span data-stu-id="15a75-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="15a75-350">Neste exemplo, vamos bin distância de viagem Olá em cinco intervalos binários e visualizar Olá discretização resultados.</span><span class="sxs-lookup"><span data-stu-id="15a75-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="15a75-351">Iremos pode desenhar Olá acima distribuição bin na barra de uma ou linha desenho com:</span><span class="sxs-lookup"><span data-stu-id="15a75-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Desenhar #3][3]

<span data-ttu-id="15a75-353">e</span><span class="sxs-lookup"><span data-stu-id="15a75-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Desenhar #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="15a75-355">Visualização: Exemplos de Scatterplot</span><span class="sxs-lookup"><span data-stu-id="15a75-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="15a75-356">Vamos mostrar o desenho de gráfico de dispersão entre **viagem\_tempo\_no\_seg** e **viagem\_distância** toosee se não houver qualquer correlação</span><span class="sxs-lookup"><span data-stu-id="15a75-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Desenhar #6][6]

<span data-ttu-id="15a75-358">Da mesma forma, pode verificar a relação Olá entre **taxa\_código** e **viagem\_distância**.</span><span class="sxs-lookup"><span data-stu-id="15a75-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Desenhar #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="15a75-360">Exploração de dados em amostras de dados através de consultas SQL no bloco de notas do IPython</span><span class="sxs-lookup"><span data-stu-id="15a75-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="15a75-361">Nesta secção, vamos explorar as distribuições de dados utilizando os dados de Olá amostragem que são mantidos numa tabela nova Olá que criámos acima.</span><span class="sxs-lookup"><span data-stu-id="15a75-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="15a75-362">Tenha em atenção que podem ser executadas explorations semelhantes utilizando tabelas original Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="15a75-363">Exploração: O número de relatório de linhas e colunas no Olá amostragem tabela</span><span class="sxs-lookup"><span data-stu-id="15a75-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="15a75-364">Exploração: Tipped/não tripped distribuição</span><span class="sxs-lookup"><span data-stu-id="15a75-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="15a75-365">Exploração: Distribuição de classe de sugestão</span><span class="sxs-lookup"><span data-stu-id="15a75-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="15a75-366">Exploração: Desenhar distribuição de sugestão Olá pela classe</span><span class="sxs-lookup"><span data-stu-id="15a75-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Desenhar #26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="15a75-368">Exploração: Distribuição diária viagens</span><span class="sxs-lookup"><span data-stu-id="15a75-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="15a75-369">Exploração: Viagem distribuição por medallion</span><span class="sxs-lookup"><span data-stu-id="15a75-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="15a75-370">Exploração: Viagem distribuição através da licença medallion e acesso</span><span class="sxs-lookup"><span data-stu-id="15a75-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="15a75-371">Exploração: Distribuição de tempo de viagem</span><span class="sxs-lookup"><span data-stu-id="15a75-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="15a75-372">Exploração: Distribuição de distância viagem</span><span class="sxs-lookup"><span data-stu-id="15a75-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="15a75-373">Exploração: Distribuição de tipo de pagamento</span><span class="sxs-lookup"><span data-stu-id="15a75-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="15a75-374">Verificar o formulário de final Olá da tabela de featurized Olá</span><span class="sxs-lookup"><span data-stu-id="15a75-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="15a75-375"><a name="mlmodel"></a>Criar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="15a75-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="15a75-376">Iremos agora está pronto tooproceed toomodel criação e implementação de modelo no [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="15a75-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="15a75-377">dados de Olá estão pronto toobe utilizado em qualquer um dos problemas de predição de Olá identificados anteriormente, nomeadamente:</span><span class="sxs-lookup"><span data-stu-id="15a75-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="15a75-378">**Classificação binária**: toopredict ou não uma sugestão foi paga para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="15a75-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="15a75-379">**Classificação de várias classes**: intervalo de Olá toopredict de sugestão paga, de acordo com toohello classes definidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="15a75-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="15a75-380">**Tarefa de regressão**: quantidade de Olá toopredict de sugestão paga para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="15a75-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="15a75-381">toobegin Olá modelação exercício, inicie sessão no tooyour **Azure Machine Learning** área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="15a75-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="15a75-382">Se ainda não tiver criado uma área de trabalho de aprendizagem, consulte o artigo [criar uma área de trabalho do Azure ML](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="15a75-383">tooget iniciado com o Azure Machine Learning, consulte [que é o Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="15a75-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="15a75-384">Inicie sessão no demasiado[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="15a75-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="15a75-385">página de Studio Home Olá fornece uma variedade de informações, vídeos, tutoriais, ligações toohello referência de módulos e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="15a75-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="15a75-386">Para obter mais informações sobre o Azure Machine Learning, consulte Olá [Centro de documentação do Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="15a75-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="15a75-387">Uma experimentação de preparação típica é constituída por Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="15a75-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="15a75-388">Criar um **+ novo** experimentação.</span><span class="sxs-lookup"><span data-stu-id="15a75-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="15a75-389">Obter dados de Olá no Azure ML.</span><span class="sxs-lookup"><span data-stu-id="15a75-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="15a75-390">Pré-processar, transformar e manipular dados de Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="15a75-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="15a75-391">Gere funcionalidades conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="15a75-391">Generate features as needed.</span></span>
5. <span data-ttu-id="15a75-392">Dividir os dados de Olá em conjuntos de dados de formação / / testes validação (ou tem conjuntos de dados separados para cada).</span><span class="sxs-lookup"><span data-stu-id="15a75-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="15a75-393">Selecione um ou mais algoritmos do machine learning consoante Olá toosolve de problema de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="15a75-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="15a75-394">Por exemplo, classificação binária, classificação de várias classes, regressão.</span><span class="sxs-lookup"><span data-stu-id="15a75-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="15a75-395">Preparar um ou mais modelos utilizando o conjunto de dados de formação de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="15a75-396">Conjunto de dados de validação Olá utilizando model(s) treinado Olá de pontuação.</span><span class="sxs-lookup"><span data-stu-id="15a75-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="15a75-397">Avalie Olá model(s) toocompute Olá relevantes métricas para Olá problema de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="15a75-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="15a75-398">Ajustar Olá model(s) e selecione Olá melhor toodeploy de modelo.</span><span class="sxs-lookup"><span data-stu-id="15a75-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="15a75-399">Neste exercício, vamos já explorou e foi desenvolvido dados Olá no armazém de dados do SQL Server e decidir tooingest de tamanho de exemplo de Olá no Azure ML.</span><span class="sxs-lookup"><span data-stu-id="15a75-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="15a75-400">Eis Olá procedimento toobuild um ou mais dos modelos de previsão Olá:</span><span class="sxs-lookup"><span data-stu-id="15a75-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="15a75-401">Obter dados Olá do Azure ML com Olá [importar dados] [ import-data] módulo, disponível no Olá **dados de entrada e saída** secção.</span><span class="sxs-lookup"><span data-stu-id="15a75-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="15a75-402">Para obter mais informações, consulte Olá [importar dados] [ import-data] página de referência do módulo.</span><span class="sxs-lookup"><span data-stu-id="15a75-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Dados de importação do Azure ML][17]
2. <span data-ttu-id="15a75-404">Selecione **SQL Database do Azure** como Olá **origem de dados** no Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="15a75-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="15a75-405">Introduza o nome DNS de base de dados de Olá no Olá **nome do servidor de base de dados** campo.</span><span class="sxs-lookup"><span data-stu-id="15a75-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="15a75-406">Formato:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="15a75-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="15a75-407">Introduza Olá **nome de base de dados** no campo correspondente Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="15a75-408">Introduza Olá *nome de utilizador do SQL Server* no Olá **nome de conta de utilizador do servidor**e Olá *palavra-passe* no Olá **palavra-passe de conta de utilizador do**.</span><span class="sxs-lookup"><span data-stu-id="15a75-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="15a75-409">Verifique Olá **aceita qualquer certificado de servidor** opção.</span><span class="sxs-lookup"><span data-stu-id="15a75-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="15a75-410">No Olá **consulta de base de dados** editar a área de texto, cole a consulta de Olá que extrai Olá necessário campos (incluindo quaisquer campos calculados como etiquetas Olá) da base de dados e pendente amostras de tamanho da amostra Olá dados toohello assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="15a75-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="15a75-411">Um exemplo de uma experimentação de classificação binária ler os dados diretamente a partir da base de dados do SQL Data Warehouse Olá é na figura Olá abaixo (Lembre-se de que tooreplace Olá nomes das tabelas nyctaxi_trip e nyctaxi_fare pelo esquema Olá nome e Olá os nomes das tabelas utilizadas na sua EXPLICAÇÃO passo a passo).</span><span class="sxs-lookup"><span data-stu-id="15a75-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="15a75-412">Podem ser construídas experimentações semelhantes para classificação de várias classes e problemas de regressão.</span><span class="sxs-lookup"><span data-stu-id="15a75-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Formação do Azure ML][10]

> [!IMPORTANT]
> <span data-ttu-id="15a75-414">No Olá modelação de extração de dados e fazendo a amostragem exemplos de consultas fornecidos nas secções anteriores, **todas as etiquetas para exercícios de modelação Olá três estão incluídas na consulta de Olá**.</span><span class="sxs-lookup"><span data-stu-id="15a75-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="15a75-415">Um passo importante (obrigatório) em cada um dos Olá modelação exercícios é demasiado**excluir** Olá desnecessárias etiquetas para Olá outros dois problemas e quaisquer outros **fugas de destino**.</span><span class="sxs-lookup"><span data-stu-id="15a75-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="15a75-416">Por exemplo, quando utilizar a classificação do binária, utilize etiqueta Olá **tipped** e excluir os campos de Olá **sugestão\_classe**, **sugestão\_quantidade**, e **total\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="15a75-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="15a75-417">Olá última são fugas de destino, desde que o implica sugestão Olá paga.</span><span class="sxs-lookup"><span data-stu-id="15a75-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="15a75-418">tooexclude quaisquer colunas desnecessárias ou fugas de destino, pode utilizar Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo ou Olá [Editar metadados] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="15a75-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="15a75-419">Para obter mais informações, consulte [selecionar colunas no conjunto de dados] [ select-columns] e [Editar metadados] [ edit-metadata] páginas de referência.</span><span class="sxs-lookup"><span data-stu-id="15a75-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="15a75-420"><a name="mldeploy"></a>Implementar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="15a75-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="15a75-421">Quando o modelo estiver pronto, pode facilmente implementá-lo como um serviço web diretamente a partir da experimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="15a75-422">Para obter mais informações sobre a implementação de serviços web do Azure ML, consulte [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="15a75-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="15a75-423">toodeploy um novo serviço web, tem de:</span><span class="sxs-lookup"><span data-stu-id="15a75-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="15a75-424">Crie uma experimentação de classificação.</span><span class="sxs-lookup"><span data-stu-id="15a75-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="15a75-425">Implemente o serviço web de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-425">Deploy hello web service.</span></span>

<span data-ttu-id="15a75-426">toocreate uma classificação de experimentação de um **concluído** experimentação de preparação, clique em **criar classificação experimentação** na barra de ação inferior Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![A classificação do Azure][18]

<span data-ttu-id="15a75-428">O Azure Machine Learning tentará toocreate uma experimentação de classificação com base nos componentes de Olá do experimentação de preparação de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="15a75-429">Em particular, irá:</span><span class="sxs-lookup"><span data-stu-id="15a75-429">In particular, it will:</span></span>

1. <span data-ttu-id="15a75-430">Guarde o modelo treinado Olá e remover módulos de formação do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="15a75-431">Identificar uma lógica **porta de entrada** toorepresent Olá esperado esquema de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="15a75-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="15a75-432">Identificar uma lógica **porta de saída** esquema de saída do serviço do toorepresent Olá web esperado.</span><span class="sxs-lookup"><span data-stu-id="15a75-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="15a75-433">Quando é criado Olá experimentação de classificação, reveja-lo e efetue a ajustar conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="15a75-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="15a75-434">Um ajuste típico é conjunto de dados entrada tooreplace Olá e/ou a consulta com um que exclui os campos de etiqueta, como estes não estarão disponíveis quando o serviço de Olá é chamado.</span><span class="sxs-lookup"><span data-stu-id="15a75-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="15a75-435">Também é que um boa prática tooreduce Olá o tamanho de Olá entrada tooa de consulta e/ou conjunto de dados poucos registos, apenas suficiente esquema da entrada Olá tooindicate.</span><span class="sxs-lookup"><span data-stu-id="15a75-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="15a75-436">Para a porta de saída Olá, é comum tooexclude campos de entrada de todos os e incluir apenas Olá **etiquetas classificadas** e **probabilidades classificadas** no Olá saída utilizando Olá [selecionar colunas no conjunto de dados ] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="15a75-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="15a75-437">É fornecido um classificação experimentação de exemplo na figura Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="15a75-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="15a75-438">Quando está preparado toodeploy, clique em Olá **publicar o serviço de WEB** botão na barra de ação inferior Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![A publicação do Azure ML][11]

## <a name="summary"></a><span data-ttu-id="15a75-440">Resumo</span><span class="sxs-lookup"><span data-stu-id="15a75-440">Summary</span></span>
<span data-ttu-id="15a75-441">toorecap que que efetuou neste tutorial explicação passo a passo, criou um ambiente de ciência de dados do Azure, trabalhou com um grande conjunto de dados público, colocá-lo através de Olá processo de ciência de dados de equipa, todas as forma de Olá de formação de toomodel de aquisição de dados e, em seguida, toohello a implementação de um serviço web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="15a75-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="15a75-442">Informações de licença</span><span class="sxs-lookup"><span data-stu-id="15a75-442">License information</span></span>
<span data-ttu-id="15a75-443">Estas instruções de exemplo e o respetivo que acompanha scripts e IPython notebook(s) são partilhadas pela Microsoft em licença MIT de Olá.</span><span class="sxs-lookup"><span data-stu-id="15a75-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="15a75-444">Verifique o ficheiro de LICENSE.txt Olá no diretório de Olá do código de exemplo de Olá no GitHub para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="15a75-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="15a75-445">Referências</span><span class="sxs-lookup"><span data-stu-id="15a75-445">References</span></span>
<span data-ttu-id="15a75-446">• [Andrés Monroy NYC Taxi viagens página de transferência](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="15a75-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="15a75-447">• [FOILing NYC Taxi viagem dados por Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="15a75-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="15a75-448">• [NYC Taxi e Limousine Commission investigação e estatísticas](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="15a75-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
