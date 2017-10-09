---
title: "dados de aaaLoad no Azure SQL Data Warehouse – Data Factory | Microsoft Docs"
description: "Este tutorial carrega dados para o Azure SQL Data Warehouse, utilizando o Azure Data Factory e utiliza uma base de dados do SQL Server como origem de dados de Olá."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="a87db-103">Carregar dados para o SQL Data Warehouse com o Data Factory</span><span class="sxs-lookup"><span data-stu-id="a87db-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="a87db-104">Pode utilizar os dados do Azure Data Factory tooload no Azure SQL Data Warehouse a partir de qualquer Olá [arquivos de dados de origem suportados](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="a87db-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="a87db-105">Por exemplo, pode carregar dados de uma base de dados SQL do Azure ou uma base de dados Oracle para um SQL data warehouse, utilizando o Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a87db-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="a87db-106">Tutorial neste artigo mostra como dados de tooload de um servidor de SQL no local da base de dados para um SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="a87db-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="a87db-107">**Estimativa de tempo**: Este tutorial guia sobre toocomplete de 10 a 15 minutos, depois de Olá pré-requisitos são cumpridos.</span><span class="sxs-lookup"><span data-stu-id="a87db-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a87db-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a87db-108">Prerequisites</span></span>

- <span data-ttu-id="a87db-109">É necessário um **base de dados do SQL Server** com tabelas que contenham dados Olá toobe copiadas toohello do armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a87db-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="a87db-110">É necessário um online **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="a87db-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="a87db-111">Se ainda não tiver um armazém de dados, saiba como demasiado[criar um Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a87db-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="a87db-112">É necessário um **conta do Storage do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a87db-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="a87db-113">Se ainda não tiver uma conta de armazenamento, saiba como demasiado[criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a87db-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="a87db-114">Para melhor desempenho, localize a conta de armazenamento Olá e Olá do armazém de dados no Olá mesma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="a87db-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="a87db-115">Configurar uma fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="a87db-115">Configure a data factory</span></span>
1. <span data-ttu-id="a87db-116">Inicie sessão no toohello [portal do Azure][].</span><span class="sxs-lookup"><span data-stu-id="a87db-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="a87db-117">Localize o seu armazém de dados e clique em tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="a87db-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="a87db-118">No painel principal Olá, clique em **carga dados** > **do Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="a87db-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Iniciar o Assistente de dados de carga](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="a87db-120">Se não tiver uma fábrica de dados na sua subscrição do Azure, verá um **nova fábrica de dados** caixa de diálogo no separador do browser Olá.</span><span class="sxs-lookup"><span data-stu-id="a87db-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="a87db-121">Preencha Olá informações necessárias e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a87db-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="a87db-122">Depois de criar a fábrica de dados de Olá, Olá **nova fábrica de dados** fecha a caixa de diálogo e ver Olá **selecione Data Factory** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a87db-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="a87db-123">Se tiver uma ou mais dos data factories já se encontra na Olá subscrição do Azure, consulte Olá **selecione Data Factory** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a87db-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="a87db-124">Na caixa de diálogo, pode selecionar uma fábrica de dados existente ou clique em **criar nova fábrica de dados** toocreate um novo.</span><span class="sxs-lookup"><span data-stu-id="a87db-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Configurar fábrica de dados](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="a87db-126">No Olá **selecione Data Factory** caixa de diálogo, Olá **carregar dados** opção está selecionada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="a87db-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="a87db-127">Clique em **seguinte** toostart criar uma tarefa de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a87db-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="a87db-128">Configurar propriedades de fábrica de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="a87db-128">Configure hello data factory properties</span></span>
<span data-ttu-id="a87db-129">Agora que criou uma fábrica de dados, o passo seguinte Olá é dados de Olá de tooconfigure carregar agenda.</span><span class="sxs-lookup"><span data-stu-id="a87db-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="a87db-130">Para **nome da tarefa**, introduza **DWLoadData fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="a87db-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="a87db-131">Utilizar predefinição de Olá **executar agora uma vez** opção, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a87db-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Configurar agenda de carga](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="a87db-133">Configurar Olá arquivo de dados de origem e de gateway</span><span class="sxs-lookup"><span data-stu-id="a87db-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="a87db-134">Agora, indique ao Data Factory sobre Olá no local do SQL Server da base de dados de que pretende que os dados de tooload.</span><span class="sxs-lookup"><span data-stu-id="a87db-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="a87db-135">Escolha **do SQL Server** dos dados de origem Olá suportado armazenar catálogo e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a87db-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![Selecione a origem do SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="a87db-137">A **base de dados do especifique Olá no local do SQL Server** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a87db-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="a87db-138">Olá primeiro **nome da ligação** campo é automaticamente preenchido.</span><span class="sxs-lookup"><span data-stu-id="a87db-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="a87db-139">campo segundo Olá pede-lhe nome Olá Olá **Gateway**.</span><span class="sxs-lookup"><span data-stu-id="a87db-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="a87db-140">Se estiver a utilizar uma fábrica de dados existente que já tem um gateway, pode reutilizar o gateway de Olá, selecionando-Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="a87db-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="a87db-141">Clique em Olá **criar Gateway** ligação toocreate um Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="a87db-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="a87db-142">Se o arquivo de dados de origem Olá for no local ou numa máquina virtual IaaS do Azure, é necessário um Gateway de gestão de dados.</span><span class="sxs-lookup"><span data-stu-id="a87db-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="a87db-143">Um gateway tem uma relação de 1-1, com uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="a87db-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="a87db-144">Não é possível utilizar a partir de outro fábrica de dados, mas pode ser utilizado por vários dados carregar tarefas com Olá mesma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="a87db-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="a87db-145">Um gateway pode ser utilizado tooconnect toomultiple os arquivos de dados quando executar tarefas de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="a87db-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="a87db-146">Para obter informações detalhadas sobre o gateway de Olá, consulte [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="a87db-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="a87db-147">A **criar Gateway** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a87db-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="a87db-148">Para nome, introduza **GatewayForDWLoading**e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a87db-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="a87db-149">A **configurar Gateway** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a87db-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="a87db-150">Clique em **lançar a configuração rápida neste computador** tooautomatically transferir, instalar e registar o Gateway de gestão de dados no seu computador atual.</span><span class="sxs-lookup"><span data-stu-id="a87db-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="a87db-151">progresso de Olá é apresentado numa janela de pop-up.</span><span class="sxs-lookup"><span data-stu-id="a87db-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="a87db-152">Se a máquina Olá não é possível ligar o arquivo de dados de toohello, pode manualmente [transferir e instalar o gateway de Olá](https://www.microsoft.com/download/details.aspx?id=39717) num computador que possam ligar toohello dados armazenar e, em seguida, utilize tooregister chave Olá.</span><span class="sxs-lookup"><span data-stu-id="a87db-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="a87db-153">configuração rápida Olá nativamente funciona com o Microsoft Edge e do Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="a87db-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="a87db-154">Se estiver a utilizar o Google Chrome, primeiro de instalar extensão do Olá ClickOnce do arquivo de web do Chrome.</span><span class="sxs-lookup"><span data-stu-id="a87db-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Inicie a configuração rápida](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="a87db-156">Aguarde toocomplete de configuração do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="a87db-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="a87db-157">Depois de gateway Olá for registado com êxito e estiver online, fecha a janela de pop-up Olá e o novo gateway de Olá aparece no campo gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="a87db-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="a87db-158">Em seguida, preencha o resto Olá necessário campos da seguinte forma, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a87db-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="a87db-159">**Nome do servidor**: nome do Olá no local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a87db-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="a87db-160">**Nome da base de dados**: base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a87db-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="a87db-161">**Encriptação de credenciais**: utilizar a predefinição de Olá "pelo browser do web".</span><span class="sxs-lookup"><span data-stu-id="a87db-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="a87db-162">**Tipo de autenticação**: escolha Olá tipo de autenticação que está a utilizar.</span><span class="sxs-lookup"><span data-stu-id="a87db-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="a87db-163">**Nome de utilizador** e **palavra-passe**: introduza o nome de utilizador Olá e a palavra-passe para um utilizador que tem permissão toocopy Olá dados.</span><span class="sxs-lookup"><span data-stu-id="a87db-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Inicie a configuração rápida](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="a87db-165">Olá passo seguinte consiste em tabelas de Olá toochoose que dados de Olá toocopy.</span><span class="sxs-lookup"><span data-stu-id="a87db-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="a87db-166">Pode filtrar as tabelas de Olá através da utilização de palavras-chave.</span><span class="sxs-lookup"><span data-stu-id="a87db-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="a87db-167">E pode pré-visualizar o esquema de dados e tabela de Olá no painel inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="a87db-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="a87db-168">Depois de concluir a seleção, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a87db-168">After you finish your selection, click **Next**.</span></span>

    ![Selecionar tabelas](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="a87db-170">Configurar o destino de Olá, o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a87db-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="a87db-171">Agora, indique ao fábrica de dados sobre as informações de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="a87db-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="a87db-172">As informações de ligação do SQL Data Warehouse é automaticamente preenchidas.</span><span class="sxs-lookup"><span data-stu-id="a87db-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="a87db-173">Introduza a palavra-passe de Olá Olá nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="a87db-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="a87db-174">e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a87db-174">and click **Next**.</span></span>

    ![Configurar o destino](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="a87db-176">Um mapeamento de tabela inteligente é apresentada que mapeia as tabelas de toodestination de origem com base nos nomes de tabela.</span><span class="sxs-lookup"><span data-stu-id="a87db-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="a87db-177">Se a tabela de Olá não existe no destino Olá, por predefinição ADF irá criar uma com Olá mesmo nome (Isto aplica-se tooSQL servidor ou base de dados do Azure SQL Server como origem).</span><span class="sxs-lookup"><span data-stu-id="a87db-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="a87db-178">Também pode escolher toomap tooan existente tabela.</span><span class="sxs-lookup"><span data-stu-id="a87db-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="a87db-179">Reveja e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a87db-179">Review and click **Next**.</span></span>

    ![Tabelas de mapa](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="a87db-181">Reveja o mapeamento de esquema Olá e procurar erros ou mensagens de aviso.</span><span class="sxs-lookup"><span data-stu-id="a87db-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="a87db-182">Mapeamento inteligente é baseado no nome da coluna.</span><span class="sxs-lookup"><span data-stu-id="a87db-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="a87db-183">Se houver uma conversão de tipo de dados não suportados entre a coluna de origem e destino Olá, verá uma mensagem de erro em conjunto com a tabela correspondente Olá.</span><span class="sxs-lookup"><span data-stu-id="a87db-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="a87db-184">Se escolher toolet automática de fábrica de dados criar tabelas de Olá, conversão de tipo de dados adequada pode ocorrer se for necessário incompatibilidade de Olá toofix entre os arquivos de origem e destino.</span><span class="sxs-lookup"><span data-stu-id="a87db-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Esquema de mapa](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="a87db-186">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a87db-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="a87db-187">Configurar definições de desempenho de Olá</span><span class="sxs-lookup"><span data-stu-id="a87db-187">Configure hello performance settings</span></span>
<span data-ttu-id="a87db-188">Configurações de desempenho de Olá, pode configura uma conta de armazenamento do Azure utilizada para dados de Olá de teste antes de que carrega para utilização do SQL Data Warehouse performantly [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="a87db-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="a87db-189">Depois da conclusão da cópia de Olá, dados intermédio de Olá no armazenamento serão limpa automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a87db-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="a87db-190">Selecione uma conta de armazenamento do Azure existente e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a87db-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Configurar o teste de blob](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="a87db-192">Reveja as informações de resumo e implemente o pipeline de Olá</span><span class="sxs-lookup"><span data-stu-id="a87db-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="a87db-193">Reveja a configuração de Olá e clique em **concluir** pipeline do botão toodeploy Olá.</span><span class="sxs-lookup"><span data-stu-id="a87db-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Implementar a fábrica de dados](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="a87db-195">Progresso de carregamento de dados de monitor</span><span class="sxs-lookup"><span data-stu-id="a87db-195">Monitor data loading progress</span></span>

<span data-ttu-id="a87db-196">Pode ver o progresso da implementação Olá e resulta na Olá **implementação** página.</span><span class="sxs-lookup"><span data-stu-id="a87db-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="a87db-197">Depois de implementação de Olá é concluída, clique em ligação Olá **clique aqui o pipeline de cópia de toomonitor** dados toomonitor ao carregar o progresso.</span><span class="sxs-lookup"><span data-stu-id="a87db-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![Monitorizar o pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="a87db-199">Olá recém-criado **DWLoadData fromSQLServer** pipeline de carregamento de dados é automaticamente selecionada Olá esquerda **Explorador de recursos**.</span><span class="sxs-lookup"><span data-stu-id="a87db-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Pipeline de vista](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="a87db-201">Clique no pipeline de Olá no meio de Olá Olá do painel toosee detalhadas de estado para cada tabela que mapeie tooan atividade.</span><span class="sxs-lookup"><span data-stu-id="a87db-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Atividade de tabela da vista](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="a87db-203">Mais clique para uma atividade e ver dados Olá carregar os detalhes no painel à direita Olá, incluindo o tamanho dos dados, linhas, débito, etc.</span><span class="sxs-lookup"><span data-stu-id="a87db-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Ver detalhes de atividade de tabela](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="a87db-205">toolaunch Esta monitorização vista posterior, aceda tooyour do armazém de dados do SQL Server, clique **carga dados > Azure Data Factory**, selecione a fábrica e escolha **monitorizar existente a carregar tarefas**.</span><span class="sxs-lookup"><span data-stu-id="a87db-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a87db-206">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a87db-206">Next steps</span></span>

<span data-ttu-id="a87db-207">toomigrate tooSQL a base de dados do armazém de dados, consulte [descrição geral da migração](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="a87db-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="a87db-208">toolearn mais informações sobre o Azure Data Factory e as respetivas capacidades do movimento de dados, consulte Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="a87db-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="a87db-209">Introdução tooAzure fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="a87db-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="a87db-210">Mover dados utilizando a atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="a87db-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="a87db-211">Mover tooand de dados do armazém de dados SQL do Azure utilizando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a87db-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="a87db-212">tooexplore os dados no armazém de dados do SQL Server, consulte Olá os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="a87db-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="a87db-213">Ligar tooSQL do armazém de dados com o Visual Studio e SSDT</span><span class="sxs-lookup"><span data-stu-id="a87db-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="a87db-214">[Dados do elemento visual com o Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a87db-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[portal do Azure]: https://portal.azure.com
