---
title: aaaBuild e implementar um modelo de machine learning utilizar o SQL Server numa VM do Azure | Microsoft Docs
description: "Processo de análise avançada e tecnologia em ação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="f0036-103">Olá o processo de ciência de dados de equipa em ação: utilizar o SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0036-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="f0036-104">Neste tutorial, a guiá-lo através do processo de Olá de criar e implementar um modelo de machine learning com o SQL Server e um conjunto de dados publicamente disponível – hello [NYC Taxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="f0036-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="f0036-105">procedimento Olá segue um fluxo de trabalho de ciências de dados padrão: inserção e explorar dados Olá, criar learning de toofacilitate de funcionalidades, em seguida, criar e implementar um modelo.</span><span class="sxs-lookup"><span data-stu-id="f0036-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="f0036-106"><a name="dataset"></a>NYC Taxi viagens descrição do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="f0036-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="f0036-107">Olá dados NYC Taxi viagem cerca de 20GB de ficheiros CSV comprimidos (GB de ~ 48 descomprimido), que inclui mais de milhões de 173 viagens individuais e Olá fares paga para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="f0036-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="f0036-108">Cada registo viagem inclui a localização de recolha e drop-off Olá e a hora, acesso anónimos (controlador) número de licença e número de medallion (id exclusivo do taxi).</span><span class="sxs-lookup"><span data-stu-id="f0036-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="f0036-109">dados Olá abrange todos os viagens no ano de Olá 2013 e são fornecidos na Olá seguir dois conjuntos de dados de cada mês:</span><span class="sxs-lookup"><span data-stu-id="f0036-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="f0036-110">Olá 'trip_data' CSV contém detalhes viagem, tais como o número de passageiros, recolha e dropoff pontos, duração de viagem e comprimento viagem.</span><span class="sxs-lookup"><span data-stu-id="f0036-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="f0036-111">Seguem-se alguns registos de exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0036-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="f0036-112">Olá 'trip_fare' CSV contém detalhes de fare Olá paga para cada viagem, tais como o tipo de pagamento, a quantidade de fare, surcharge e taxas, sugestões e tolls e quantidade total de Olá paga.</span><span class="sxs-lookup"><span data-stu-id="f0036-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="f0036-113">Seguem-se alguns registos de exemplo:</span><span class="sxs-lookup"><span data-stu-id="f0036-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="f0036-114">viagem de toojoin de chave exclusivo Olá\_dados e viagem\_fare é composto por campos Olá: medallion, acesso\_licenciamento e a recolha\_datetime.</span><span class="sxs-lookup"><span data-stu-id="f0036-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="f0036-115"><a name="mltasks"></a>Exemplos de predição de tarefas</span><span class="sxs-lookup"><span data-stu-id="f0036-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="f0036-116">Iremos irá formular três problemas de predição com base no Olá *sugestão\_quantidade*, nomeadamente:</span><span class="sxs-lookup"><span data-stu-id="f0036-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="f0036-117">Classificação do binária: prever ou não uma sugestão foi paga para uma viagem, ou seja, um *sugestão\_quantidade* que é superior ao $0 é um exemplo positivo, enquanto um *sugestão\_quantidade* $ 0 é um exemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="f0036-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="f0036-118">Classificação de várias classes: intervalo de Olá toopredict de sugestão paga para viagem Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="f0036-119">Iremos dividir Olá *sugestão\_quantidade* em cinco intervalos binários ou classes:</span><span class="sxs-lookup"><span data-stu-id="f0036-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="f0036-120">Tarefa de regressão: quantidade de Olá toopredict de sugestão paga para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="f0036-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="f0036-121"><a name="setup"></a>Configurar a definição Olá dados do Azure ciência ambiente para análise avançada</span><span class="sxs-lookup"><span data-stu-id="f0036-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="f0036-122">Como pode ver partir Olá [planear o ambiente](machine-learning-data-science-plan-your-environment.md) guia, existem várias opções toowork com Olá NYC Taxi viagens conjunto de dados do Azure:</span><span class="sxs-lookup"><span data-stu-id="f0036-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="f0036-123">Trabalhar com dados Olá em blobs do Azure e o modelo no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f0036-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="f0036-124">Carregar dados de Olá para uma base de dados do SQL Server e o modelo no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f0036-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="f0036-125">Neste tutorial, iremos demonstrar importação de paralelo em massa de Olá tooa de dados do SQL Server, exploração de dados, a funcionalidade de engenharia e para baixo amostragem utilizando o SQL Server Management Studio, bem como utilizar IPython bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="f0036-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="f0036-126">[Scripts de exemplo](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) e [IPython blocos de notas](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) são partilhados no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0036-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="f0036-127">Um toowork de bloco de notas do exemplo IPython com dados Olá em blobs do Azure também está disponível no Olá mesma localização.</span><span class="sxs-lookup"><span data-stu-id="f0036-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="f0036-128">tooset configurar o ambiente de ciência de dados do Azure:</span><span class="sxs-lookup"><span data-stu-id="f0036-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="f0036-129">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f0036-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="f0036-130">Criar uma área de trabalho do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f0036-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="f0036-131">[Aprovisionar uma máquina de Virtual de ciência de dados](machine-learning-data-science-setup-sql-server-virtual-machine.md), que fornece um SQL Server e um servidor de IPython bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="f0036-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f0036-132">scripts de exemplo de Olá e IPython blocos de notas serão transferidos tooyour máquinas de ciência de dados durante o processo de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="f0036-133">Quando tiver concluído a Olá script de pós-instalação de VM, exemplos de Olá estarão disponíveis na biblioteca de documentos da VM:</span><span class="sxs-lookup"><span data-stu-id="f0036-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="f0036-134">Scripts de exemplo:`C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="f0036-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="f0036-135">Blocos de notas do exemplo IPython:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="f0036-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="f0036-136">onde `<user_name>` é o nome de início de sessão do Windows da VM.</span><span class="sxs-lookup"><span data-stu-id="f0036-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="f0036-137">Iremos dar toohello pastas de exemplo como **Scripts de exemplo** e **blocos de notas do exemplo IPython**.</span><span class="sxs-lookup"><span data-stu-id="f0036-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="f0036-138">Com base no tamanho do conjunto de dados de Olá, localização da origem de dados e ambiente de destino do Azure selecionada Olá, este cenário é semelhante demasiado[cenário \#5: SQL Server numa VM do Azure de destino do conjunto de dados grande nos ficheiros de locais,](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="f0036-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="f0036-139"><a name="getdata"></a>Obter Olá dados a partir da origem público</span><span class="sxs-lookup"><span data-stu-id="f0036-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="f0036-140">Olá tooget [NYC Taxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados da sua localização pública, poderá utilizar qualquer um dos métodos de Olá descritos na [tooand mover dados do Blob Storage do Azure](machine-learning-data-science-move-azure-blob.md) toocopy Olá dados tooyour nova a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f0036-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="f0036-141">dados de Olá toocopy utilizando o AzCopy:</span><span class="sxs-lookup"><span data-stu-id="f0036-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="f0036-142">Inicie sessão na máquina de virtual tooyour (VM)</span><span class="sxs-lookup"><span data-stu-id="f0036-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="f0036-143">Criar um novo diretório num disco de dados da VM Olá (Nota: não utilize Olá disco temporário vem com Olá VM como um disco de dados).</span><span class="sxs-lookup"><span data-stu-id="f0036-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="f0036-144">Na janela de linha de comandos, execute Olá seguinte linha de comandos do Azcopy, substituindo < path_to_data_folder > com a sua pasta de dados que criou no (2):</span><span class="sxs-lookup"><span data-stu-id="f0036-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="f0036-145">Quando tiver concluído a Olá AzCopy, um total de 24 zipado ficheiros CSV (12 para viagem\_dados e 12 para viagem\_fare) deve estar na pasta de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="f0036-146">Descomprimir ficheiros de Olá transferido.</span><span class="sxs-lookup"><span data-stu-id="f0036-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="f0036-147">Tenha em atenção a pasta de olá onde residem os ficheiros de Olá descomprimido.</span><span class="sxs-lookup"><span data-stu-id="f0036-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="f0036-148">Esta pasta irá ser referido tooas Olá < caminho\_para\_dados\_ficheiros\>.</span><span class="sxs-lookup"><span data-stu-id="f0036-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="f0036-149"><a name="dbload"></a>Dados de importação em massa na base de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0036-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="f0036-150">Olá desempenho de carregamento/transferência de grandes quantidades de dados tooan SQL da base de dados e consultas subsequentes pode ser melhorado utilizando *particionada tabelas e vistas*.</span><span class="sxs-lookup"><span data-stu-id="f0036-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="f0036-151">Nesta secção, iremos segui instruções Olá descritas em [paralelo em massa importar utilizando o SQL Server partição tabelas de dados](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate um nova base de dados e carregar Olá dados em tabelas particionadas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="f0036-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="f0036-152">Enquanto tem sessão iniciada no tooyour VM, iniciar **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="f0036-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="f0036-153">Estabelecer ligação utilizando a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="f0036-153">Connect using Windows Authentication.</span></span>
   
    ![Ligação SSMS][12]
3. <span data-ttu-id="f0036-155">Se ainda não tiver alterado o modo de autenticação do SQL Server Olá e criado um novo utilizador de início de sessão do SQL Server, abra o ficheiro de script de Olá denominado **alterar\_auth.sql** no Olá **Scripts de exemplo** pasta.</span><span class="sxs-lookup"><span data-stu-id="f0036-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="f0036-156">Alterar o nome de utilizador predefinido Olá e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="f0036-156">Change hello  default user name and password.</span></span> <span data-ttu-id="f0036-157">Clique em **! Executar** no script de Olá toorun do Olá barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="f0036-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Executar o Script][13]
4. <span data-ttu-id="f0036-159">Certifique-se de e/ou alterar Olá predefinido da base de dados e registo pastas tooensure que recém-criado bases de dados será armazenado no disco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f0036-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="f0036-160">imagem de VM do SQL Server de Olá está otimizada para cargas de datawarehousing está pré-configurada com discos de dados e de registo.</span><span class="sxs-lookup"><span data-stu-id="f0036-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="f0036-161">Se a VM não inclui um disco de dados e adicionar novos discos rígidos virtuais durante o processo de configuração VM de Olá, altere pastas predefinidas de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f0036-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="f0036-162">Nome do SQL Server de Olá de contexto no Olá à esquerda painel e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f0036-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![Propriedades do SQL Server][14]
   * <span data-ttu-id="f0036-164">Selecione **definições de base de dados** de Olá **selecionar uma página** lista toohello esquerda.</span><span class="sxs-lookup"><span data-stu-id="f0036-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="f0036-165">Certifique-se de e/ou alterar Olá **localizações predefinidas de base de dados** toohello **disco de dados** localizações à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="f0036-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="f0036-166">Este é onde novas bases de dados residem se criada com as definições de localização do Olá predefinidas.</span><span class="sxs-lookup"><span data-stu-id="f0036-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![Predefinições de base de dados do SQL Server][15]  
5. <span data-ttu-id="f0036-168">toocreate uma nova base de dados e um conjunto de grupos de ficheiros toohold Olá tabelas particionadas, abra o script de exemplo de Olá **criar\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="f0036-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="f0036-169">script de Olá irá criar uma nova base de dados com o nome **TaxiNYC** e 12 grupos de ficheiros na localização de dados do Olá predefinida.</span><span class="sxs-lookup"><span data-stu-id="f0036-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="f0036-170">Cada grupo de ficheiros irá conter um mês de viagem\_dados e viagem\_fare dados.</span><span class="sxs-lookup"><span data-stu-id="f0036-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="f0036-171">Modificar o nome da base de dados de Olá, se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="f0036-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="f0036-172">Clique em **! Executar** script de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="f0036-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="f0036-173">Em seguida, crie duas tabelas de partição, um para viagem Olá\_dados e outra para viagem Olá\_fare.</span><span class="sxs-lookup"><span data-stu-id="f0036-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="f0036-174">Abra o script de exemplo de Olá **criar\_particionada\_table.sql**, que irá:</span><span class="sxs-lookup"><span data-stu-id="f0036-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="f0036-175">Crie uma partição função toosplit Olá de dados por mês.</span><span class="sxs-lookup"><span data-stu-id="f0036-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="f0036-176">Crie um toomap de esquema de partição de dados tooa outro grupo de ficheiros cada mês.</span><span class="sxs-lookup"><span data-stu-id="f0036-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="f0036-177">Criar dois esquema de partição de tabelas particionadas toohello mapeada: **nyctaxi\_viagem** vai conter viagem Olá\_dados e **nyctaxi\_fare** vai conter viagem Olá \_fare dados.</span><span class="sxs-lookup"><span data-stu-id="f0036-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="f0036-178">Clique em **! Executar** toorun Olá script e criar tabelas de Olá particionada.</span><span class="sxs-lookup"><span data-stu-id="f0036-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="f0036-179">No Olá **Scripts de exemplo** pasta, existem dois scripts do PowerShell de exemplo fornecidos toodemonstrate importações de paralelo em massa tooSQL servidor de tabelas de dados.</span><span class="sxs-lookup"><span data-stu-id="f0036-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="f0036-180">**BCP\_paralelas\_generic.ps1** é um script genérico tooparallel em massa importar dados para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f0036-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="f0036-181">Modificar este script tooset Olá entrada e de destino variáveis conforme indicado nas linhas de comentários de Olá no script de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="f0036-182">**BCP\_paralelas\_nyctaxi.ps1** é uma versão de pré-configurada do script genérico Olá e pode ser utilizado tootooload ambas as tabelas de dados de NYC Taxi viagens Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="f0036-183">Contexto Olá **bcp\_paralelas\_nyctaxi.ps1** nome do script e clique em **editar** tooopen-lo no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0036-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="f0036-184">Olá revisão variáveis da configuração predefinida e modificar de acordo com nome de base de dados selecionada tooyour, pasta de dados de entrada, pasta de registo de destino e ficheiros de formato de exemplo do caminhos toohello **nyctaxi_trip.xml** e **nyctaxi\_ fare.XML** (fornecidas Olá **Scripts de exemplo** pasta).</span><span class="sxs-lookup"><span data-stu-id="f0036-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Dados de importação em volume][16]
   
    <span data-ttu-id="f0036-186">Também pode selecionar o modo de autenticação de Olá, a predefinição é a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="f0036-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="f0036-187">Clique em seta verde Olá no Olá toorun de barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="f0036-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="f0036-188">script de Olá iniciará 24 operações de importação de em massa em paralelo, 12 para cada tabela particionada.</span><span class="sxs-lookup"><span data-stu-id="f0036-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="f0036-189">Pode monitorizar o progresso de importação de dados de Olá, abrindo a pasta de dados predefinida do Olá do SQL Server como conjunto acima.</span><span class="sxs-lookup"><span data-stu-id="f0036-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="f0036-190">relatórios de script do PowerShell Olá Olá inicial e final vezes.</span><span class="sxs-lookup"><span data-stu-id="f0036-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="f0036-191">Quando todos os em massa importações concluída, é comunicado Olá hora de fim.</span><span class="sxs-lookup"><span data-stu-id="f0036-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="f0036-192">Verificação Olá destino registo pasta tooverify que Olá em massa importações teve êxito, ou seja, sem erros reportados na pasta de registo de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="f0036-193">A base de dados está agora pronto para exploração, engenharia da funcionalidade e outras operações conforme pretendido.</span><span class="sxs-lookup"><span data-stu-id="f0036-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="f0036-194">Uma vez que as tabelas de Olá são particionadas toohello de acordo com **recolha\_datetime** campo, consultas, que incluem **recolha\_datetime** condições em Olá  **ONDE** cláusula será vantajoso contar com o esquema de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="f0036-195">No **SQL Server Management Studio**, explore o script de exemplo de Olá fornecido **exemplo\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="f0036-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="f0036-196">toorun qualquer uma das consultas de exemplo de Olá, realce Olá linhas de consulta, em seguida, clique em **! Executar** na barra de ferramentas Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="f0036-197">Olá dados NYC Taxi viagens será carregado no duas tabelas separadas.</span><span class="sxs-lookup"><span data-stu-id="f0036-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="f0036-198">operações de associação de tooimprove, recomenda-se vivamente tabelas de Olá tooindex.</span><span class="sxs-lookup"><span data-stu-id="f0036-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="f0036-199">script de exemplo de Olá **criar\_particionada\_index.sql** cria índices particionados na chave de associação composto Olá **medallion, acesso\_licença e recolha\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="f0036-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="f0036-200"><a name="dbexplore"></a>Exploração de dados e de engenharia da funcionalidade no SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0036-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="f0036-201">Nesta secção, iremos efetuar geração de exploração e funcionalidade de dados através da execução de consultas SQL diretamente no Olá **SQL Server Management Studio** utilizar Olá do SQL Server da base de dados criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f0036-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="f0036-202">Um script de exemplo com o nome **exemplo\_queries.sql** é fornecido na Olá **Scripts de exemplo** pasta.</span><span class="sxs-lookup"><span data-stu-id="f0036-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="f0036-203">Modificar o nome de base de dados do Olá script toochange Olá, se for diferente do predefinido Olá: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="f0036-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="f0036-204">Neste exercício, iremos:</span><span class="sxs-lookup"><span data-stu-id="f0036-204">In this exercise, we will:</span></span>

* <span data-ttu-id="f0036-205">Ligar demasiado**SQL Server Management Studio** utilizando a autenticação do Windows ou utilizando a autenticação do SQL Server e Olá nome de início de sessão do SQL Server e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="f0036-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="f0036-206">Explore as distribuições de dados de alguns campos no variando intervalos de tempo.</span><span class="sxs-lookup"><span data-stu-id="f0036-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="f0036-207">Investigue a qualidade dos dados de campos de latitude e longitude de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="f0036-208">Gerar etiquetas de classificação de várias classes e binária com base no Olá **sugestão\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="f0036-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="f0036-209">Gerar funcionalidades e computação/comparar as distâncias de viagem.</span><span class="sxs-lookup"><span data-stu-id="f0036-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="f0036-210">Associar tabelas Olá dois e extrair amostra aleatória que será utilizado toobuild modelos.</span><span class="sxs-lookup"><span data-stu-id="f0036-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="f0036-211">Quando estiver pronto tooproceed tooAzure Machine Learning, o utilizador pode optar por:</span><span class="sxs-lookup"><span data-stu-id="f0036-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="f0036-212">Guardar Olá final SQL tooextract e exemplo Olá dados e copiar-colar Olá consulta diretamente para um [importar dados] [ import-data] módulo no Azure Machine Learning, ou</span><span class="sxs-lookup"><span data-stu-id="f0036-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="f0036-213">Manter Olá amostragem e foi desenvolvidos dados planear toouse para criação de uma nova base de dados do modelo de tabela e utilizam nova tabela de Olá Olá [importar dados] [ import-data] módulo no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f0036-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="f0036-214">Nesta secção, irá guardar Olá consulta final tooextract e exemplo Olá os dados.</span><span class="sxs-lookup"><span data-stu-id="f0036-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="f0036-215">segundo método de Olá é demonstrado nos Olá [exploração de dados e funcionalidade de engenharia no bloco de notas do IPython](#ipnb) secção.</span><span class="sxs-lookup"><span data-stu-id="f0036-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="f0036-216">Para uma verificação rápida do número de Olá de linhas e colunas no Olá tabelas preenchido anteriormente utilizando a importação de paralelo em massa,</span><span class="sxs-lookup"><span data-stu-id="f0036-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="f0036-217">Exploração: Distribuição de viagem por medallion</span><span class="sxs-lookup"><span data-stu-id="f0036-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="f0036-218">Neste exemplo identifica medallion Olá (taxi números) com mais do que 100 viagens dentro de um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="f0036-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="f0036-219">consulta de Olá seria beneficiar de acesso de tabela Olá particionada desde que está a ter pelo esquema de partição Olá da **recolha\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="f0036-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="f0036-220">Consultar o conjunto de dados completo Olá também faz com que a utilização de tabela particionada Olá e/ou a análise de índice.</span><span class="sxs-lookup"><span data-stu-id="f0036-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="f0036-221">Exploração: Distribuição de viagem medallion e hack_license</span><span class="sxs-lookup"><span data-stu-id="f0036-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="f0036-222">Avaliação de qualidade de dados: Verificar os registos com incorreto longitude e/ou latitude</span><span class="sxs-lookup"><span data-stu-id="f0036-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="f0036-223">Neste exemplo investiga se qualquer um dos campos de longitude e/ou latitude Olá ou contém um valor inválido (radian graus devem ser entre -90 e 90), ou ter (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="f0036-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="f0036-224">Exploração: Vs Tipped. Distribuição de Tipped viagens não</span><span class="sxs-lookup"><span data-stu-id="f0036-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="f0036-225">Neste exemplo localiza o número de Olá de viagens foram tipped vs tipped não num determinado momento período (ou em Olá conjunto de dados completo se que abrangem ano completa Olá).</span><span class="sxs-lookup"><span data-stu-id="f0036-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="f0036-226">Esta distribuição reflete Olá etiqueta binário distribuição toobe posteriormente utilizado para a modelação de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="f0036-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="f0036-227">Exploração: Distribuição de classe/intervalo de sugestão</span><span class="sxs-lookup"><span data-stu-id="f0036-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="f0036-228">Neste exemplo calcula a distribuição de Olá de intervalos de sugestão num determinado momento período (ou em Olá conjunto de dados completo se que abrangem ano completa Olá).</span><span class="sxs-lookup"><span data-stu-id="f0036-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="f0036-229">Esta é a distribuição de Olá das classes de etiqueta Olá que serão utilizados mais tarde para a modelação de classificação de várias classes.</span><span class="sxs-lookup"><span data-stu-id="f0036-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="f0036-230">Exploração: Computação e comparar distância viagem</span><span class="sxs-lookup"><span data-stu-id="f0036-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="f0036-231">Neste exemplo converte longitude de recolha e drop-off Olá e pontos de geografia de tooSQL latitude, calcula distância de viagem Olá utilizando a diferença de pontos de geografia SQL e devolve uma amostra aleatória de resultados de Olá para comparação.</span><span class="sxs-lookup"><span data-stu-id="f0036-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="f0036-232">exemplo de Olá limita os resultados de Olá toovalid coordena a utilizar apenas Olá qualidade assessment a consulta de dados abrangida anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f0036-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="f0036-233">Engenharia da funcionalidade em consultas SQL</span><span class="sxs-lookup"><span data-stu-id="f0036-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="f0036-234">Olá etiqueta geração geografia conversão exploração consultas e também podem ser utilizado toogenerate etiquetas/funcionalidades removendo Olá contando parte.</span><span class="sxs-lookup"><span data-stu-id="f0036-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="f0036-235">Exemplos SQL de engenharia funcionalidades adicionais são fornecidos na Olá [exploração de dados e funcionalidade de engenharia no bloco de notas do IPython](#ipnb) secção.</span><span class="sxs-lookup"><span data-stu-id="f0036-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="f0036-236">É mais eficientes toorun Olá funcionalidade geração consultas no conjunto de dados completo Olá ou um subconjunto do mesmo através de consultas SQL que executam diretamente na instância de base de dados do SQL Server de Olá grande.</span><span class="sxs-lookup"><span data-stu-id="f0036-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="f0036-237">consultas de Olá podem ser executadas na **SQL Server Management Studio**, IPython bloco de notas ou qualquer ferramenta/ambiente de desenvolvimento que pode aceder ao hello da base de dados localmente ou remotamente.</span><span class="sxs-lookup"><span data-stu-id="f0036-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="f0036-238">A preparar os dados para a criação de modelo</span><span class="sxs-lookup"><span data-stu-id="f0036-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="f0036-239">Olá associações de consulta seguinte Olá **nyctaxi\_viagem** e **nyctaxi\_fare** tabelas, gera uma etiqueta de classificação binária **tipped**, um etiqueta de classificação de classe Multi **sugestão\_classe**e extrai uma amostra aleatória de 1% do Olá conjunto de dados completa associados.</span><span class="sxs-lookup"><span data-stu-id="f0036-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="f0036-240">Esta consulta pode ser copiada e colada diretamente no Olá [Azure Machine Learning Studio](https://studio.azureml.net) [importar dados] [ import-data] módulo para a ingestão de dados direta da base de dados do Olá do SQL Server instância no Azure.</span><span class="sxs-lookup"><span data-stu-id="f0036-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="f0036-241">consulta de Olá exclui registos com incorreto (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="f0036-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="f0036-242"><a name="ipnb"></a>Exploração de dados e de engenharia da funcionalidade no bloco de notas do IPython</span><span class="sxs-lookup"><span data-stu-id="f0036-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="f0036-243">Nesta secção, iremos efetuar exploração de dados e a geração de funcionalidade através de consultas de Python e SQL na base de dados do SQL Server Olá criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f0036-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="f0036-244">Um exemplo IPython bloco de notas com o nome **machine-Learning-data-science-process-sql-story.ipynb** é fornecido na Olá **blocos de notas do exemplo IPython** pasta.</span><span class="sxs-lookup"><span data-stu-id="f0036-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="f0036-245">Este bloco de notas também está disponível no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="f0036-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="f0036-246">Olá recomendado sequência quando trabalhar com macrodados é seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="f0036-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="f0036-247">Ler um exemplo de dados de Olá pequeno para um intervalo de dados em memória.</span><span class="sxs-lookup"><span data-stu-id="f0036-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="f0036-248">Efetuar algumas visualizações e explorations utilizando Olá amostras de dados.</span><span class="sxs-lookup"><span data-stu-id="f0036-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="f0036-249">Experimentar a engenharia da funcionalidade utilizando dados Olá amostragem.</span><span class="sxs-lookup"><span data-stu-id="f0036-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="f0036-250">Para maior exploração de dados, a manipulação de dados e de engenharia da funcionalidade, utilize as consultas de SQL do Python tooissue diretamente na base de dados do SQL Server Olá Olá VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0036-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="f0036-251">Decida toouse de tamanho de exemplo de Olá para criação de modelo do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f0036-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="f0036-252">Quando está preparado tooproceed tooAzure Machine Learning, o utilizador pode optar por:</span><span class="sxs-lookup"><span data-stu-id="f0036-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="f0036-253">Guardar Olá final SQL tooextract e exemplo Olá dados e copiar-colar Olá consulta diretamente para um [importar dados] [ import-data] módulo no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f0036-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="f0036-254">Este método é demonstrado nos Olá [edifício modelos no Azure Machine Learning](#mlmodel) secção.</span><span class="sxs-lookup"><span data-stu-id="f0036-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="f0036-255">Manter Olá amostragem e os dados foi desenvolvidos planear toouse para criação de uma nova tabela de base de dados do modelo, em seguida, utilizar a nova tabela de Olá no Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="f0036-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="f0036-256">Olá seguem-se alguns exploração de dados, visualização de dados e funcionalidade exemplos de engenharia.</span><span class="sxs-lookup"><span data-stu-id="f0036-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="f0036-257">Para obter mais exemplos, consulte o bloco de notas do Olá exemplo IPython de SQL no Olá **blocos de notas do exemplo IPython** pasta.</span><span class="sxs-lookup"><span data-stu-id="f0036-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="f0036-258">Inicializar as credenciais da base de dados</span><span class="sxs-lookup"><span data-stu-id="f0036-258">Initialize Database Credentials</span></span>
<span data-ttu-id="f0036-259">Inicializar as definições de ligação de base de dados no Olá seguintes variáveis:</span><span class="sxs-lookup"><span data-stu-id="f0036-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="f0036-260">Criar a ligação de base de dados</span><span class="sxs-lookup"><span data-stu-id="f0036-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="f0036-261">Número de relatório de linhas e colunas na tabela nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="f0036-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="f0036-262">Número total de linhas = 173179759</span><span class="sxs-lookup"><span data-stu-id="f0036-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="f0036-263">Número total de colunas = 14</span><span class="sxs-lookup"><span data-stu-id="f0036-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="f0036-264">Leia-in de uma amostra de dados de pequena de Olá base de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0036-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="f0036-265">Tabela de exemplo do tempo tooread Olá é 6.492000 segundos</span><span class="sxs-lookup"><span data-stu-id="f0036-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="f0036-266">Número de linhas e colunas obter = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="f0036-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="f0036-267">Estatísticas descritivas</span><span class="sxs-lookup"><span data-stu-id="f0036-267">Descriptive Statistics</span></span>
<span data-ttu-id="f0036-268">Agora está pronto tooexplore dados de Olá amostragem.</span><span class="sxs-lookup"><span data-stu-id="f0036-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="f0036-269">Iremos começar a utilizar ao procurar estatísticas descritivas para Olá **viagem\_distância** (ou qualquer outro) campo (s):</span><span class="sxs-lookup"><span data-stu-id="f0036-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="f0036-270">Visualização: Exemplo de desenho de caixa</span><span class="sxs-lookup"><span data-stu-id="f0036-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="f0036-271">Em seguida, observe o desenho de caixa de Olá para Olá viagem distância toovisualize Olá quantiles</span><span class="sxs-lookup"><span data-stu-id="f0036-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Desenhar #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="f0036-273">Visualização: Exemplo de desenho de distribuição</span><span class="sxs-lookup"><span data-stu-id="f0036-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Desenhar #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="f0036-275">Visualização: Barra e Plots de linha</span><span class="sxs-lookup"><span data-stu-id="f0036-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="f0036-276">Neste exemplo, vamos bin distância de viagem Olá em cinco intervalos binários e visualizar Olá discretização resultados.</span><span class="sxs-lookup"><span data-stu-id="f0036-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="f0036-277">Iremos pode desenhar Olá acima distribuição bin na barra de uma ou linha desenho tal como indicado abaixo</span><span class="sxs-lookup"><span data-stu-id="f0036-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Desenhar #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Desenhar #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="f0036-280">Visualização: Exemplo de Scatterplot</span><span class="sxs-lookup"><span data-stu-id="f0036-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="f0036-281">Vamos mostrar o desenho de gráfico de dispersão entre **viagem\_tempo\_no\_seg** e **viagem\_distância** toosee se não houver qualquer correlação</span><span class="sxs-lookup"><span data-stu-id="f0036-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Desenhar #6][6]

<span data-ttu-id="f0036-283">Da mesma forma, pode verificar a relação Olá entre **taxa\_código** e **viagem\_distância**.</span><span class="sxs-lookup"><span data-stu-id="f0036-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Desenhar #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="f0036-285">Olá amostragem secundárias dados no SQL Server</span><span class="sxs-lookup"><span data-stu-id="f0036-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="f0036-286">Quando preparar dados para o modelo de criação num [Azure Machine Learning Studio](https://studio.azureml.net), ou pode optar Olá **toouse de consulta SQL diretamente no módulo de importar dados de Olá** ou manter Olá foi desenvolvido e amostragem dados numa tabela nova, que pode utilizar num Olá [importar dados] [ import-data] módulo com um simples **SELECIONAR * FROM < sua\_novo\_tabela\_nome >**.</span><span class="sxs-lookup"><span data-stu-id="f0036-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="f0036-287">Nesta secção, que iremos criar uma nova toohold Olá da tabela amostragem e foi desenvolvido dados.</span><span class="sxs-lookup"><span data-stu-id="f0036-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="f0036-288">Um exemplo de uma consulta SQL direta para a criação de modelo é fornecido na Olá [exploração de dados e funcionalidade de engenharia no SQL Server](#dbexplore) secção.</span><span class="sxs-lookup"><span data-stu-id="f0036-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="f0036-289">Crie uma tabela de exemplo e Populate com % 1 de Olá associado tabelas.</span><span class="sxs-lookup"><span data-stu-id="f0036-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="f0036-290">Remova a primeira tabela se existir.</span><span class="sxs-lookup"><span data-stu-id="f0036-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="f0036-291">Nesta secção, vamos associar tabelas Olá **nyctaxi\_viagem** e **nyctaxi\_fare**, a extrair uma amostra aleatória de 1% e manter dados Olá amostragem um novo nome de tabela  **nyctaxi\_um\_por cento**:</span><span class="sxs-lookup"><span data-stu-id="f0036-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="f0036-292">Exploração de dados através de consultas de SQL no bloco de notas do IPython</span><span class="sxs-lookup"><span data-stu-id="f0036-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="f0036-293">Nesta secção, vamos explorar as distribuições de dados utilizando os dados de 1% amostragem Olá, que são mantidos numa tabela nova Olá que criámos acima.</span><span class="sxs-lookup"><span data-stu-id="f0036-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="f0036-294">Tenha em atenção que podem ser executadas explorations semelhantes utilizando tabelas original Olá, utilizando opcionalmente **TABLESAMPLE** toolimit exploração de Olá exemplo ou ao limitar Olá resulta tooa dado período de tempo utilizando Olá **recolha \_datetime** partições, conforme ilustrado nas Olá [exploração de dados e funcionalidade de engenharia no SQL Server](#dbexplore) secção.</span><span class="sxs-lookup"><span data-stu-id="f0036-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="f0036-295">Exploração: Distribuição diária viagens</span><span class="sxs-lookup"><span data-stu-id="f0036-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="f0036-296">Exploração: Viagem distribuição por medallion</span><span class="sxs-lookup"><span data-stu-id="f0036-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="f0036-297">Geração de funcionalidade através de consultas SQL no bloco de notas do IPython</span><span class="sxs-lookup"><span data-stu-id="f0036-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="f0036-298">Nesta secção, irá gerar novas etiquetas e funcionalidades, utilizando diretamente as consultas SQL, operar na tabela de 1% exemplo Olá criámos na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="f0036-299">Geração de etiqueta: Gerar etiquetas de classe</span><span class="sxs-lookup"><span data-stu-id="f0036-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="f0036-300">No seguinte exemplo de Olá, iremos gerar dois conjuntos de toouse etiquetas para a modelação:</span><span class="sxs-lookup"><span data-stu-id="f0036-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="f0036-301">Binário de classe de etiquetas **tipped** (prever se uma sugestão terá)</span><span class="sxs-lookup"><span data-stu-id="f0036-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="f0036-302">Etiquetas de várias classes **sugestão\_classe** (prever bin de sugestão de Olá ou intervalo)</span><span class="sxs-lookup"><span data-stu-id="f0036-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="f0036-303">Engenharia da funcionalidade: Funcionalidades de contagem para colunas Categórico</span><span class="sxs-lookup"><span data-stu-id="f0036-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="f0036-304">Neste exemplo transforma um campo categórico num campo numérico ao substituir cada categoria com contagem de Olá dos respetivos ocorrências nos dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="f0036-305">Engenharia da funcionalidade: Funcionalidades de reciclagem para colunas numérico</span><span class="sxs-lookup"><span data-stu-id="f0036-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="f0036-306">Neste exemplo transforma um campo numérico contínuo em intervalos de categoria predefinidas, ou seja, transformação campo numérico para um campo categórico.</span><span class="sxs-lookup"><span data-stu-id="f0036-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="f0036-307">Engenharia da funcionalidade: Extrair as funcionalidades de localização de Decimal Latitude/Longitude</span><span class="sxs-lookup"><span data-stu-id="f0036-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="f0036-308">Neste exemplo divide representação decimal de Olá de um campo de latitude e/ou longitude em vários campos de região de granularidade diferente, tais como país, cidade, town, blocos, etc. Tenha em atenção que Olá novos georreplicação-campos não são mapeados tooactual localizações.</span><span class="sxs-lookup"><span data-stu-id="f0036-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="f0036-309">Para obter informações sobre localizações de geocode de mapeamento, consulte [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="f0036-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="f0036-310">Verificar o formulário de final Olá da tabela de featurized Olá</span><span class="sxs-lookup"><span data-stu-id="f0036-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="f0036-311">Iremos agora está pronto tooproceed toomodel criação e implementação de modelo no [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f0036-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="f0036-312">dados de Olá estão prontos para qualquer um dos problemas de predição de Olá identificados anteriormente, nomeadamente:</span><span class="sxs-lookup"><span data-stu-id="f0036-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="f0036-313">Classificação do binária: toopredict ou não uma sugestão foi paga para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="f0036-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="f0036-314">Classificação de várias classes: intervalo de Olá toopredict de sugestão paga, de acordo com toohello classes definidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f0036-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="f0036-315">Tarefa de regressão: quantidade de Olá toopredict de sugestão paga para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="f0036-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="f0036-316"><a name="mlmodel"></a>Criar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f0036-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="f0036-317">exercício de modelação de Olá toobegin, registo, na área de trabalho do tooyour Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f0036-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="f0036-318">Se ainda não tiver criado uma área de trabalho de aprendizagem, consulte o artigo [criar uma área de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f0036-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="f0036-319">tooget iniciado com o Azure Machine Learning, consulte [que é o Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="f0036-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="f0036-320">Inicie sessão no demasiado[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f0036-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="f0036-321">página de Studio Home Olá fornece uma variedade de informações, vídeos, tutoriais, ligações toohello referência de módulos e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="f0036-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="f0036-322">Fore mais informações sobre o Azure Machine Learning, consulte Olá [Centro de documentação do Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="f0036-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="f0036-323">Uma experimentação de preparação típico é composta pelos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="f0036-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="f0036-324">Criar um **+ novo** experimentação.</span><span class="sxs-lookup"><span data-stu-id="f0036-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="f0036-325">Obter dados de Olá tooAzure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f0036-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="f0036-326">Pré-processar, transformar e manipular dados de Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f0036-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="f0036-327">Gere funcionalidades conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f0036-327">Generate features as needed.</span></span>
5. <span data-ttu-id="f0036-328">Dividir os dados de Olá em conjuntos de dados de formação / / testes validação (ou tem conjuntos de dados separados para cada).</span><span class="sxs-lookup"><span data-stu-id="f0036-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="f0036-329">Selecione um ou mais algoritmos do machine learning consoante Olá toosolve de problema de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="f0036-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="f0036-330">Por exemplo, classificação binária, classificação de várias classes, regressão.</span><span class="sxs-lookup"><span data-stu-id="f0036-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="f0036-331">Preparar um ou mais modelos utilizando o conjunto de dados de formação de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="f0036-332">Conjunto de dados de validação Olá utilizando model(s) treinado Olá de pontuação.</span><span class="sxs-lookup"><span data-stu-id="f0036-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="f0036-333">Avalie Olá model(s) toocompute Olá relevantes métricas para Olá problema de aprendizagem.</span><span class="sxs-lookup"><span data-stu-id="f0036-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="f0036-334">Ajustar Olá model(s) e selecione Olá melhor toodeploy de modelo.</span><span class="sxs-lookup"><span data-stu-id="f0036-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="f0036-335">Neste exercício, vamos já explorou e foi desenvolvido dados Olá no SQL Server e decidir tooingest de tamanho de exemplo de Olá no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f0036-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="f0036-336">toobuild um ou mais dos modelos de predição de Olá decidimos:</span><span class="sxs-lookup"><span data-stu-id="f0036-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="f0036-337">Obter dados de Olá tooAzure Machine Learning utilizando Olá [importar dados] [ import-data] módulo, disponível no Olá **dados de entrada e saída** secção.</span><span class="sxs-lookup"><span data-stu-id="f0036-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="f0036-338">Para obter mais informações, consulte Olá [importar dados] [ import-data] página de referência do módulo.</span><span class="sxs-lookup"><span data-stu-id="f0036-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Importar dados de aprendizagem do Azure][17]
2. <span data-ttu-id="f0036-340">Selecione **SQL Database do Azure** como Olá **origem de dados** no Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="f0036-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="f0036-341">Introduza o nome DNS de base de dados de Olá no Olá **nome do servidor de base de dados** campo.</span><span class="sxs-lookup"><span data-stu-id="f0036-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="f0036-342">Formato:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="f0036-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="f0036-343">Introduza Olá **nome de base de dados** no campo correspondente Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="f0036-344">Introduza Olá **nome de utilizador do SQL Server** no Olá * * nome do servidor utilizador aqccount e Olá palavra-passe no Olá **palavra-passe de conta de utilizador do**.</span><span class="sxs-lookup"><span data-stu-id="f0036-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="f0036-345">Verifique **aceita qualquer certificado de servidor** opção.</span><span class="sxs-lookup"><span data-stu-id="f0036-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="f0036-346">No Olá **consulta de base de dados** editar a área de texto, cole a consulta de Olá que extrai Olá necessário campos (incluindo quaisquer campos calculados como etiquetas Olá) da base de dados e pendente amostras de tamanho da amostra Olá dados toohello assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="f0036-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="f0036-347">É um exemplo de uma experimentação de classificação binária ler os dados diretamente a partir da base de dados do SQL Server Olá na figura Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="f0036-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="f0036-348">Podem ser construídas experimentações semelhantes para classificação de várias classes e problemas de regressão.</span><span class="sxs-lookup"><span data-stu-id="f0036-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure Machine Learning formação][10]

> [!IMPORTANT]
> <span data-ttu-id="f0036-350">No Olá modelação de extração de dados e fazendo a amostragem exemplos de consultas fornecidos nas secções anteriores, **todas as etiquetas para exercícios de modelação Olá três estão incluídas na consulta de Olá**.</span><span class="sxs-lookup"><span data-stu-id="f0036-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="f0036-351">Um passo importante (obrigatório) em cada um dos Olá modelação exercícios é demasiado**excluir** Olá desnecessárias etiquetas para Olá outros dois problemas e quaisquer outros **fugas de destino**.</span><span class="sxs-lookup"><span data-stu-id="f0036-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="f0036-352">Para por exemplo, quando utilizar a classificação do binária, utilize etiqueta Olá **tipped** e excluir os campos de Olá **sugestão\_classe**, **sugestão\_quantidade**, e **total\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="f0036-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="f0036-353">Olá última são fugas de destino, desde que o implica sugestão Olá paga.</span><span class="sxs-lookup"><span data-stu-id="f0036-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="f0036-354">colunas desnecessárias tooexclude e/ou fugas de destino, pode utilizar Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo ou Olá [Editar metadados] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="f0036-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="f0036-355">Para obter mais informações, consulte [selecionar colunas no conjunto de dados] [ select-columns] e [Editar metadados] [ edit-metadata] páginas de referência.</span><span class="sxs-lookup"><span data-stu-id="f0036-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="f0036-356"><a name="mldeploy"></a>Modelos de implementação no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f0036-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="f0036-357">Quando o modelo estiver pronto, pode facilmente implementá-lo como um serviço web diretamente a partir da experimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="f0036-358">Para obter mais informações sobre a implementação de serviços web do Azure Machine Learning, consulte [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f0036-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="f0036-359">toodeploy um novo serviço web, tem de:</span><span class="sxs-lookup"><span data-stu-id="f0036-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="f0036-360">Crie uma experimentação de classificação.</span><span class="sxs-lookup"><span data-stu-id="f0036-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="f0036-361">Implemente o serviço web de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-361">Deploy hello web service.</span></span>

<span data-ttu-id="f0036-362">toocreate uma classificação de experimentação de um **concluído** experimentação de preparação, clique em **criar classificação experimentação** na barra de ação inferior Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![A classificação do Azure][18]

<span data-ttu-id="f0036-364">O Azure Machine Learning tentará toocreate uma experimentação de classificação com base nos componentes de Olá do experimentação de preparação de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="f0036-365">Em particular, irá:</span><span class="sxs-lookup"><span data-stu-id="f0036-365">In particular, it will:</span></span>

1. <span data-ttu-id="f0036-366">Guarde o modelo treinado Olá e remover módulos de formação do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="f0036-367">Identificar uma lógica **porta de entrada** toorepresent Olá esperado esquema de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="f0036-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="f0036-368">Identificar uma lógica **porta de saída** esquema de saída do serviço do toorepresent Olá web esperado.</span><span class="sxs-lookup"><span data-stu-id="f0036-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="f0036-369">Quando é criado Olá experimentação de classificação, reveja-lo e ajustar conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f0036-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="f0036-370">Um ajuste típico é conjunto de dados entrada tooreplace Olá e/ou a consulta com um que exclui os campos de etiqueta, como estes não estarão disponíveis quando o serviço de Olá é chamado.</span><span class="sxs-lookup"><span data-stu-id="f0036-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="f0036-371">Também é que um boa prática tooreduce Olá o tamanho de Olá entrada tooa de consulta e/ou conjunto de dados poucos registos, apenas suficiente esquema da entrada Olá tooindicate.</span><span class="sxs-lookup"><span data-stu-id="f0036-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="f0036-372">Para a porta de saída Olá, é comum tooexclude campos de entrada de todos os e incluir apenas Olá **etiquetas classificadas** e **probabilidades classificadas** no Olá saída utilizando Olá [selecionar colunas no conjunto de dados ] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="f0036-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="f0036-373">É um classificação experimentação de exemplo na figura Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="f0036-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="f0036-374">Quando está preparado toodeploy, clique em Olá **publicar o serviço de WEB** botão na barra de ação inferior Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publicar de aprendizagem do Azure][11]

<span data-ttu-id="f0036-376">toorecap, neste tutorial explicação passo a passo, criou um ambiente de ciência de dados do Azure, trabalhado com um conjunto de dados grande público todas as forma de Olá de toomodel de aquisição de dados de preparação e implementação de um serviço web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f0036-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="f0036-377">Informações de licença</span><span class="sxs-lookup"><span data-stu-id="f0036-377">License Information</span></span>
<span data-ttu-id="f0036-378">Estas instruções de exemplo e o respetivo que acompanha scripts e IPython notebook(s) são partilhadas pela Microsoft em licença MIT de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0036-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="f0036-379">Verifique o ficheiro de LICENSE.txt Olá no diretório de Olá do código de exemplo de Olá no GitHub para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="f0036-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="f0036-380">Referências</span><span class="sxs-lookup"><span data-stu-id="f0036-380">References</span></span>
<span data-ttu-id="f0036-381">• [Andrés Monroy NYC Taxi viagens página de transferência](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="f0036-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="f0036-382">• [FOILing NYC Taxi viagem dados por Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="f0036-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="f0036-383">• [NYC Taxi e Limousine Commission investigação e estatísticas](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="f0036-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
