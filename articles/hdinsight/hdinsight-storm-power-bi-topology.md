---
title: aaaUse Apache Storm com o Power BI - Azure HDInsight | Microsoft Docs
description: "Crie um relatório do Power BI com dados de uma topologia de c# em execução num cluster do Apache Storm no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="ac050-103">Utilizar dados de toovisualize do Power BI a partir de uma topologia do Apache Storm</span><span class="sxs-lookup"><span data-stu-id="ac050-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="ac050-104">Power BI permite-lhe toovisually apresenta dados como relatórios.</span><span class="sxs-lookup"><span data-stu-id="ac050-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="ac050-105">Este documento fornece um exemplo de como toouse Apache Storm no HDInsight toogenerate dados para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="ac050-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="ac050-106">Olá passos neste documento dependem de um ambiente de desenvolvimento do Windows com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ac050-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="ac050-107">projeto compilado Olá pode ser o cluster de HDInsight baseado em Linux tooa submetido.</span><span class="sxs-lookup"><span data-stu-id="ac050-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ac050-108">Apenas clusters baseados em Linux criados após 10/28/2016 suporte SCP.NET topologias.</span><span class="sxs-lookup"><span data-stu-id="ac050-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="ac050-109">toouse uma topologia de c# com um cluster baseado em Linux, atualização Olá pacote Microsoft.SCP.Net.SDK NuGet utilizado pelo seu tooversion projeto 0.10.0.6 ou superior.</span><span class="sxs-lookup"><span data-stu-id="ac050-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="ac050-110">versão de Olá do pacote de Olá também tem de corresponder à versão principal do Olá do Storm instalado no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac050-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="ac050-111">Por exemplo, o Storm nas versões 3.3 e 3.4 do HDInsight utilizam a versão 0.10.x do Storm, enquanto o HDInsight 3.5 utiliza o Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="ac050-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="ac050-112">Topologias de c# em clusters baseados em Linux tem de utilizar o .NET 4.5 e utilizar Mono toorun num cluster do HDInsight Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="ac050-113">A maioria dos aspetos funcionam.</span><span class="sxs-lookup"><span data-stu-id="ac050-113">Most things work.</span></span> <span data-ttu-id="ac050-114">No entanto, deve verificar Olá [Mono compatibilidade](http://www.mono-project.com/docs/about-mono/compatibility/) documento para incompatibilidades potenciais.</span><span class="sxs-lookup"><span data-stu-id="ac050-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="ac050-115">Para uma versão de Java deste projeto, que funciona com o HDInsight baseado em Windows ou baseado em Linux, consulte [processar eventos provenientes dos Hubs de eventos do Azure com o Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ac050-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac050-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac050-116">Prerequisites</span></span>

* <span data-ttu-id="ac050-117">Um utilizador do Azure Active Directory com [Power BI](https://powerbi.com) acesso.</span><span class="sxs-lookup"><span data-stu-id="ac050-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="ac050-118">Um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac050-118">An HDInsight cluster.</span></span> <span data-ttu-id="ac050-119">Para obter mais informações, consulte [introdução ao Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ac050-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ac050-120">Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="ac050-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ac050-121">Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).</span><span class="sxs-lookup"><span data-stu-id="ac050-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ac050-122">Visual Studio (uma das seguintes versões de Olá)</span><span class="sxs-lookup"><span data-stu-id="ac050-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="ac050-123">Visual Studio 2012 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="ac050-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="ac050-124">Visual Studio 2013 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="ac050-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="ac050-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ac050-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="ac050-126">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="ac050-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="ac050-127">Olá ferramentas do HDInsight para Visual Studio: consulte [começar a utilizar as ferramentas do HDInsight Olá para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre as informações da instalação.</span><span class="sxs-lookup"><span data-stu-id="ac050-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="ac050-128">Como funciona</span><span class="sxs-lookup"><span data-stu-id="ac050-128">How it works</span></span>

<span data-ttu-id="ac050-129">Este exemplo contém uma topologia de C# que aleatoriamente gera dados de registo de serviços de informação Internet (IIS).</span><span class="sxs-lookup"><span data-stu-id="ac050-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="ac050-130">Estes dados, em seguida, são escritos tooa base de dados SQL e a partir daí é toogenerate utilizados relatórios no Power BI.</span><span class="sxs-lookup"><span data-stu-id="ac050-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="ac050-131">Olá ficheiros implementar Olá funcionalidade principal deste exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac050-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="ac050-132">**SqlAzureBolt.cs**: escreve informações produzidas Olá Storm topologia tooSQL da base de dados.</span><span class="sxs-lookup"><span data-stu-id="ac050-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="ac050-133">**IISLogsTable.sql**: Olá Transact-SQL instruções utilizadas toogenerate Olá base de dados que Olá dados são armazenados no.</span><span class="sxs-lookup"><span data-stu-id="ac050-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="ac050-134">Crie tabela Olá na base de dados do SQL Server antes de iniciar a topologia de Olá no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac050-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="ac050-135">Transferir o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="ac050-135">Download hello example</span></span>

<span data-ttu-id="ac050-136">Transferir Olá [exemplo HDInsight c# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="ac050-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="ac050-137">toodownload, quer bifurcação/clone-o utilizando [git](http://git-scm.com/), ou utilize Olá **transferir** toodownload ligação um. zip do arquivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="ac050-138">Criar uma base de dados</span><span class="sxs-lookup"><span data-stu-id="ac050-138">Create a database</span></span>

1. <span data-ttu-id="ac050-139">toocreate uma base de dados, utilize os passos de Olá Olá [tutorial de base de dados SQL](../sql-database/sql-database-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ac050-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="ac050-140">Base de dados do Connect toohello pela seguinte Olá os passos em Olá [ligar tooa base de dados SQL com o Visual Studio](../sql-database/sql-database-connect-query.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ac050-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="ac050-141">No Object Explorer, base de dados de Olá com o botão direito e selecione **nova consulta**.</span><span class="sxs-lookup"><span data-stu-id="ac050-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="ac050-142">Cole conteúdo Olá Olá **IISLogsTable.sql** ficheiros incluídos no Olá transferidas projeto na janela de consulta Olá e, em seguida, utilize Ctrl + Shift + consulta de Olá I tooexecute.</span><span class="sxs-lookup"><span data-stu-id="ac050-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="ac050-143">Deverá receber uma mensagem que Olá comandos foi concluídos com êxito.</span><span class="sxs-lookup"><span data-stu-id="ac050-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="ac050-144">Configurar o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="ac050-144">Configure hello sample</span></span>

1. <span data-ttu-id="ac050-145">De Olá [portal do Azure](https://portal.azure.com), selecione a base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ac050-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="ac050-146">De Olá **Essentials** secção Olá SQL painel base de dados, selecione **Mostrar cadeias de ligação de base de dados**.</span><span class="sxs-lookup"><span data-stu-id="ac050-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="ac050-147">Na lista de Olá que aparece, copie Olá **ADO.NET (autenticação do SQL Server)** informações.</span><span class="sxs-lookup"><span data-stu-id="ac050-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="ac050-148">Exemplo de Olá abrir no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ac050-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="ac050-149">De **Explorador de soluções**, abra Olá **App. config** de ficheiros e, em seguida, localize Olá seguir entrada:</span><span class="sxs-lookup"><span data-stu-id="ac050-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="ac050-150">Substitua Olá **# # TOBEFILLED # #** valor com a cadeia de ligação de base de dados de Olá copiou no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="ac050-151">Substitua **{sua\_username}** e **{sua\_palavra-passe}** com Olá nome de utilizador e palavra-passe para a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="ac050-152">Guarde e feche ficheiros Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="ac050-153">Implementar o exemplo de Olá</span><span class="sxs-lookup"><span data-stu-id="ac050-153">Deploy hello sample</span></span>

1. <span data-ttu-id="ac050-154">De **Explorador de soluções**, contexto Olá **StormToSQL** projeto e selecione **submeter tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ac050-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="ac050-155">Cluster do HDInsight Olá selecione de Olá **Cluster do Storm** caixa de diálogo de lista pendente.</span><span class="sxs-lookup"><span data-stu-id="ac050-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ac050-156">Poderá demorar alguns segundos para Olá **Cluster do Storm** toopopulate pendente com nomes de servidor.</span><span class="sxs-lookup"><span data-stu-id="ac050-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="ac050-157">Se lhe for solicitado, introduza as credenciais de início de sessão Olá para a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac050-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="ac050-158">Se tiver mais do que uma subscrição, inicie sessão toohello que contenha o seu cluster Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac050-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="ac050-159">Quando foi submetida topologia Olá, Olá __Visualizador de topologia__ aparece.</span><span class="sxs-lookup"><span data-stu-id="ac050-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="ac050-160">tooview esta topologia, a entrada de SqlAzureWriterTopology Olá selecione na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![topologias de Olá, com topologia Olá selecionado](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="ac050-162">Pode utilizar estas informações de toosee vista na topologia de Olá ou faça duplo clique num componente do entrada (por exemplo, Olá SqlAzureBolt) toosee informações tooa específico numa topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="ac050-163">Depois de Olá topologia tem foi executada para alguns minutos, janela de consulta SQL de retorno toohello utilizou toocreate Olá da base de dados.</span><span class="sxs-lookup"><span data-stu-id="ac050-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="ac050-164">Substitua as instruções existente Olá Olá seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="ac050-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="ac050-165">Utilize Ctrl + Shift + consulta de Olá I tooexecute e deverá receber resultados toohello semelhante, os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="ac050-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="ac050-166">Estes dados tem sido escritos da topologia do Storm Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="ac050-167">Criar um relatório</span><span class="sxs-lookup"><span data-stu-id="ac050-167">Create a report</span></span>

1. <span data-ttu-id="ac050-168">Ligar toohello [conector da SQL Database do Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="ac050-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="ac050-169">Dentro do **bases de dados**, selecione **obter**.</span><span class="sxs-lookup"><span data-stu-id="ac050-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="ac050-170">Selecione **SQL Database do Azure**e, em seguida, selecione **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ac050-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac050-171">Poderá ser pedido toodownload Olá Power BI Desktop toocontinue.</span><span class="sxs-lookup"><span data-stu-id="ac050-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="ac050-172">Se assim for, utilize Olá tooconnect passos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac050-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="ac050-173">Abra o ambiente de trabalho do Power BI e selecione __obter dados__.</span><span class="sxs-lookup"><span data-stu-id="ac050-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="ac050-174">2 selecione __Azure__e, em seguida, __SQL database do Azure__.</span><span class="sxs-lookup"><span data-stu-id="ac050-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="ac050-175">Introduza Olá informações tooconnect tooyour SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac050-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="ac050-176">Pode encontrar estas informações visitando Olá [portal do Azure](https://portal.azure.com) e selecionando a base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ac050-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ac050-177">Também pode definir o intervalo de atualização de Olá e filtros personalizados utilizando **ativar opções avançadas** de Olá ligar a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac050-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="ac050-178">Depois de se ligar, verá um novo conjunto de dados com Olá que mesmo nome como base de dados de Olá à.</span><span class="sxs-lookup"><span data-stu-id="ac050-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="ac050-179">Selecione toobegin de conjunto de dados de Olá conceber um relatório.</span><span class="sxs-lookup"><span data-stu-id="ac050-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="ac050-180">De **campos**, expanda Olá **IISLOGS** entrada.</span><span class="sxs-lookup"><span data-stu-id="ac050-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="ac050-181">toocreate um relatório que apresenta uma lista de Olá URI stems, selecionar Olá caixa de verificação **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="ac050-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Criar um relatório](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="ac050-183">Em seguida, arraste **método** toohello relatório.</span><span class="sxs-lookup"><span data-stu-id="ac050-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="ac050-184">Olá de toolist de atualizações de relatório Olá stems e método HTTP correspondente Olá utilizada para Olá pedido de HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac050-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![adicionar dados de método Olá](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="ac050-186">De Olá **visualizações** coluna, selecione de Olá **campos** ícone e, em seguida, selecione Olá seta para baixo junto demasiado**método** no Olá **valores**secção.</span><span class="sxs-lookup"><span data-stu-id="ac050-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="ac050-187">Selecione toodisplay tiverem sido acedida uma contagem de quantas vezes um URI, **contagem**.</span><span class="sxs-lookup"><span data-stu-id="ac050-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Contagem de tooa dos métodos de alteração](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="ac050-189">Em seguida, selecione Olá **gráfico de colunas Stacked** toochange como Olá informações a apresentar.</span><span class="sxs-lookup"><span data-stu-id="ac050-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![A alteração gráficos empilhados de tooa](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="ac050-191">relatório de Olá toosave, selecione **guardar** e introduza um nome para o relatório de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="ac050-192">Parar a topologia de Olá</span><span class="sxs-lookup"><span data-stu-id="ac050-192">Stop hello topology</span></span>

<span data-ttu-id="ac050-193">topologia de Olá continua toorun até pará-la ou eliminar Olá Storm num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac050-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="ac050-194">toostop Olá topologia, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ac050-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="ac050-195">No Visual Studio, devolver o Visualizador de topologia toohello e selecione a topologia de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="ac050-196">Selecione Olá **Kill** topologia do botão toostop Olá.</span><span class="sxs-lookup"><span data-stu-id="ac050-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kill botão na topologia de Olá resumo](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="ac050-198">Elimina o cluster</span><span class="sxs-lookup"><span data-stu-id="ac050-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="ac050-199">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ac050-199">Next steps</span></span>

<span data-ttu-id="ac050-200">Neste documento, aprendeu como toosend dados a partir de um tooSQL de topologia do Storm base de dados, em seguida, visualize os dados de Olá através do Power BI.</span><span class="sxs-lookup"><span data-stu-id="ac050-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="ac050-201">Para obter informações sobre como toowork com outras tecnologias do Azure a utilizar o Storm no HDInsight, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="ac050-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="ac050-202">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac050-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
