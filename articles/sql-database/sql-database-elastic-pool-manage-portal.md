---
title: "Portal do Azure: criar e gerir um conjunto elástico da base de dados SQL | Microsoft Docs"
description: "Saiba como toouse Olá portal do Azure e toomanage de intelligence incorporadas da base de dados de SQL, monitor e um desempenho de base de dados do conjunto elástico dimensionável toooptimize dimensionar e gerir custo."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="6a04d-103">Criar e gerir um conjunto elástico com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6a04d-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="6a04d-104">Este tópico mostra como toocreate e gerir dimensionável [conjuntos elásticos](sql-database-elastic-pool.md) com Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a04d-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="6a04d-105">Também pode criar e gerir um conjunto elástico do Azure com [PowerShell](sql-database-elastic-pool-manage-powershell.md), Olá REST API, ou [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="6a04d-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="6a04d-106">Também pode criar e mover bases de dados para dentro e fora conjuntos elásticos utilizando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="6a04d-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="6a04d-107">Criar um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-107">Create an elastic pool</span></span> 

<span data-ttu-id="6a04d-108">Existem duas formas de criar um conjunto elástico.</span><span class="sxs-lookup"><span data-stu-id="6a04d-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="6a04d-109">Pode fazê-lo a partir do zero se souber o programa de configuração Olá conjunto que pretende ou começa com uma recomendação do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="6a04d-110">Base de dados SQL tem intelligence incorporado que recomenda uma configuração de conjunto elástico se é mais económico para si com base nas Olá passado telemetria de utilização para as bases de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="6a04d-111">Pode criar vários conjuntos num servidor, mas não pode adicionar bases de dados de diferentes servidores ao hello mesmo conjunto.</span><span class="sxs-lookup"><span data-stu-id="6a04d-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a04d-112">Os conjuntos elásticos estão em disponibilidade geral (GA) em todas as regiões do Azure, exceto na Índia Ocidental, onde se encontra, de momento, em pré-visualização.</span><span class="sxs-lookup"><span data-stu-id="6a04d-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="6a04d-113">A GA dos conjuntos elásticos nesta região vai ocorrer assim que possível.</span><span class="sxs-lookup"><span data-stu-id="6a04d-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="6a04d-114">Passo 1: Criar um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="6a04d-115">Criar um conjunto elástico existente de um **servidor** painel no portal de Olá é Olá mais fácil forma toomove bases de dados existentes para um conjunto elástico.</span><span class="sxs-lookup"><span data-stu-id="6a04d-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="6a04d-116">Também pode criar um conjunto elástico pesquisando **agrupamento elástico de SQL** no Olá **Marketplace** ou clicar **+ adicionar** no Olá **conjuntos elásticos SQL**procurar painel.</span><span class="sxs-lookup"><span data-stu-id="6a04d-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="6a04d-117">São toospecify capaz de um servidor novo ou existente através deste agrupamento de aprovisionamento de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6a04d-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="6a04d-118">No Olá [portal do Azure](http://portal.azure.com/), clique em **mais serviços**  **>**  **servidores SQL**e, em seguida, clique em servidor Olá que contém Olá bases de dados que pretende que o agrupamento elástico de tooan tooadd.</span><span class="sxs-lookup"><span data-stu-id="6a04d-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="6a04d-119">Clique em **Novo conjunto**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-119">Click **New pool**.</span></span>

    ![Adicionar agrupamento tooa servidor](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="6a04d-121">**-OU-**</span><span class="sxs-lookup"><span data-stu-id="6a04d-121">**-OR-**</span></span>

    <span data-ttu-id="6a04d-122">Poderá ver uma mensagem a indicar que existem são recomendadas conjuntos elásticos para o servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="6a04d-123">Clique em Olá toosee mensagem de Olá recomendado conjuntos com base na telemetria de utilização de base de dados históricos e, em seguida, clique Olá camada toosee mais detalhes e personalizar o conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="6a04d-124">Consulte [compreender as recomendações de conjunto](#understand-elastic-pool-recommendations) mais adiante neste tópico para saber como a recomendação de Olá é feita.</span><span class="sxs-lookup"><span data-stu-id="6a04d-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![conjunto recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="6a04d-126">Olá **conjunto elástico** é apresentado o painel, que é onde especifica as definições de Olá para o seu conjunto.</span><span class="sxs-lookup"><span data-stu-id="6a04d-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="6a04d-127">Se clicou em **novo conjunto** no passo anterior Olá, Olá escalão de preço é **padrão** está selecionada por predefinição e não existem bases de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="6a04d-128">Pode criar um conjunto vazio ou especifique um conjunto de bases de dados existentes do toomove servidor para o conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="6a04d-129">Se estiver a criar um conjunto de recomendado, Olá recomendada preços camada, as definições de desempenho e são pré-preenchida a lista de bases de dados, mas ainda pode alterá-los.</span><span class="sxs-lookup"><span data-stu-id="6a04d-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configurar o conjunto elástico](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="6a04d-131">Especifique um nome para o conjunto elástico hello, ou deixe-o como predefinição de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="6a04d-132">Passo 2: escolher um escalão de preço</span><span class="sxs-lookup"><span data-stu-id="6a04d-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="6a04d-133">Olá escalão de preço do conjunto determina Olá funcionalidades elastics toohello disponível no agrupamento de Olá e Olá número máximo de eDTUs (eDTU máxima) e a base de dados do armazenamento (GBs) disponível tooeach.</span><span class="sxs-lookup"><span data-stu-id="6a04d-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="6a04d-134">Para obter detalhes, consulte o Escalões de serviços.</span><span class="sxs-lookup"><span data-stu-id="6a04d-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="6a04d-135">escalão de preço Olá toochange para o conjunto de Olá, clique em **escalão de preço**, clique em Olá pretende e, em seguida, clique em escalão de preço **selecione**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a04d-136">Depois de escolher Olá escalão de preço e consolidar as alterações ao clicar em **OK** no último passo Olá, não será Olá toochange capaz de escalão do conjunto de Olá de preço.</span><span class="sxs-lookup"><span data-stu-id="6a04d-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="6a04d-137">toochange Olá escalão de preço de um conjunto elástico existente, crie um conjunto elástico no escalão de preço pretendido Olá e migre Olá bases de dados toothis novo agrupamento.</span><span class="sxs-lookup"><span data-stu-id="6a04d-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Selecionar um escalão de preço](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="6a04d-139">Passo 3: Configurar o conjunto de Olá</span><span class="sxs-lookup"><span data-stu-id="6a04d-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="6a04d-140">Depois de definir Olá escalão de preço, clique em Configurar conjunto onde pode adicionar bases de dados, eDTUs de conjunto de conjunto e armazenamento (GBs do conjunto), e definir Olá min e max eDTUs para elastics Olá no agrupamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="6a04d-141">Clique em **Configurar conjunto**</span><span class="sxs-lookup"><span data-stu-id="6a04d-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="6a04d-142">Selecione as bases de dados de Olá pretende tooadd toohello agrupamento.</span><span class="sxs-lookup"><span data-stu-id="6a04d-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="6a04d-143">Este passo é opcional ao criar o conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="6a04d-144">Bases de dados podem ser adicionadas depois do conjunto de Olá ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="6a04d-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="6a04d-145">tooadd bases de dados, clique em **Adicionar base de dados**, clique em Olá as bases de dados que pretende tooadd e, em seguida, clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="6a04d-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Adicionar bases de dados](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="6a04d-147">Se as bases de dados de Olá que está a trabalhar tiverem telemetria de histórico de utilização suficiente, Olá **estimado a utilização de GB e eDTU** gráfico e Olá **utilização de eDTU real** toohelp de atualização de gráfico de barras facilitam a configuração decisões.</span><span class="sxs-lookup"><span data-stu-id="6a04d-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="6a04d-148">Além disso, Olá serviço poderá apresentar um toohelp de mensagem de recomendação poderá dimensionar Olá agrupamento.</span><span class="sxs-lookup"><span data-stu-id="6a04d-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="6a04d-149">Consulte a secção [Recomendações Dinâmicas](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="6a04d-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="6a04d-150">Utilizar controlos Olá Olá **configurar conjunto** página tooexplore definições e configurar o conjunto.</span><span class="sxs-lookup"><span data-stu-id="6a04d-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="6a04d-151">Consulte [limites dos conjuntos elásticos](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para obter mais detalhes sobre os limites para cada camada de serviço e consulte [considerações sobre preço e desempenho para conjuntos elásticos](sql-database-elastic-pool.md) de detalhado orientações sobre como dimensionar corretamente um conjunto elástico.</span><span class="sxs-lookup"><span data-stu-id="6a04d-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="6a04d-152">Para mais informações sobre as definições do conjunto, consulte [propriedades do conjunto elástico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="6a04d-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configurar o Conjunto Elástico](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="6a04d-154">Clique em **selecione** no Olá **configurar conjunto** painel depois de alterar as definições.</span><span class="sxs-lookup"><span data-stu-id="6a04d-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="6a04d-155">Clique em **OK** conjunto de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="6a04d-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="6a04d-156">Compreender as recomendações de conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="6a04d-157">Olá serviço de base de dados SQL avalia o histórico de utilização e recomenda um ou mais conjuntos quando é mais rentável do que utilizar bases de dados individuais.</span><span class="sxs-lookup"><span data-stu-id="6a04d-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="6a04d-158">Cada recomendação está configurada com um subconjunto exclusivo das bases de dados do servidor de Olá que melhor se adequam ao conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![conjunto recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="6a04d-160">recomendação de conjunto de Olá é composta por:</span><span class="sxs-lookup"><span data-stu-id="6a04d-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="6a04d-161">Um escalão de preço para o conjunto de Olá (básica, Standard, Premium ou Premium RS)</span><span class="sxs-lookup"><span data-stu-id="6a04d-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="6a04d-162">O número adequado de **eDTUs POR CONJUNTO** (também denominado Número máximo de eDTUs por conjunto)</span><span class="sxs-lookup"><span data-stu-id="6a04d-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="6a04d-163">Olá **número máximo de Edtus** e **número mínimo de Edtus** por base de dados</span><span class="sxs-lookup"><span data-stu-id="6a04d-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="6a04d-164">lista de Olá de bases de dados recomendadas para o conjunto de Olá</span><span class="sxs-lookup"><span data-stu-id="6a04d-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a04d-165">serviço de Olá tem Olá últimos 30 dias de telemetria em consideração quando recomenda conjuntos.</span><span class="sxs-lookup"><span data-stu-id="6a04d-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="6a04d-166">Para um considerada candidata para um conjunto elástico toobe de base de dados, deve existir, pelo menos, 7 dias.</span><span class="sxs-lookup"><span data-stu-id="6a04d-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="6a04d-167">As bases de dados que já estão num conjunto elástico não são consideradas candidatas para recomendações de conjunto elástico.</span><span class="sxs-lookup"><span data-stu-id="6a04d-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="6a04d-168">serviço de Olá avalia as necessidades de recursos e eficácia de custo de movimento Olá único bases de dados em cada camada de serviço para conjuntos do Olá mesmo escalão.</span><span class="sxs-lookup"><span data-stu-id="6a04d-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="6a04d-169">Por exemplo, todas as bases de dados Standard num servidor são avaliadas para determinar a respetiva adequação a um Conjunto Elástico Standard.</span><span class="sxs-lookup"><span data-stu-id="6a04d-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="6a04d-170">Isto significa que o serviço de Olá não faz recomendações entre escalões, tal como mover uma base de dados Standard para um conjunto Premium.</span><span class="sxs-lookup"><span data-stu-id="6a04d-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="6a04d-171">Depois de adicionar o conjunto de toohello de bases de dados, as recomendações são geradas dinamicamente com base no histórico de utilização de Olá das bases de dados de Olá que selecionou.</span><span class="sxs-lookup"><span data-stu-id="6a04d-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="6a04d-172">Estas recomendações são apresentadas no gráfico de utilização de GB e eDTU Olá e numa faixa de recomendação no topo de Olá da Olá **configurar conjunto** painel.</span><span class="sxs-lookup"><span data-stu-id="6a04d-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="6a04d-173">Estas recomendações estão tooassist pretendido na criação de um conjunto elástico otimizada para as bases de dados específicas.</span><span class="sxs-lookup"><span data-stu-id="6a04d-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![recomendações dinâmicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="6a04d-175">Gerir e monitorizar um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="6a04d-176">Pode utilizar Olá toomonitor portal do Azure e gerir um conjunto elástico e Olá bases de dados no agrupamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="6a04d-177">No portal de Olá, pode monitorizar a utilização de Olá do conjunto elástico e Olá bases de dados nesse agrupamento.</span><span class="sxs-lookup"><span data-stu-id="6a04d-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="6a04d-178">Também pode efetuar um conjunto de alterações de conjunto elástico tooyour e submeter todas as alterações em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="6a04d-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="6a04d-179">Estas alterações incluem a adição ou remoção de bases de dados, alterar as definições do conjunto elástico ou alterar as definições de base de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="6a04d-180">Olá gráfico a seguir mostra um agrupamento elástico de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6a04d-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="6a04d-181">Vista de Olá inclui:</span><span class="sxs-lookup"><span data-stu-id="6a04d-181">hello view includes:</span></span>

*  <span data-ttu-id="6a04d-182">Gráficos para monitorizar a utilização de recursos de agrupamento elástico Olá e bases de dados de Olá contidos no agrupamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="6a04d-183">Olá **configurar** conjunto botão toomake altera o agrupamento elástico toohello.</span><span class="sxs-lookup"><span data-stu-id="6a04d-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="6a04d-184">Olá **criar base de dados** botão que cria uma base de dados e adiciona-toohello de conjunto elástico atual.</span><span class="sxs-lookup"><span data-stu-id="6a04d-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="6a04d-185">As tarefas elásticas que o ajudam a gerem um grande número de bases de dados através da execução de scripts de Transact SQL em todas as bases de dados numa lista.</span><span class="sxs-lookup"><span data-stu-id="6a04d-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Vista de conjunto][2]

<span data-ttu-id="6a04d-187">Pode aceder tooa conjunto particular toosee a respetiva utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a04d-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="6a04d-188">Por predefinição, o agrupamento de Olá é a utilização de armazenamento e de eDTU tooshow configurado para Olá última hora.</span><span class="sxs-lookup"><span data-stu-id="6a04d-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="6a04d-189">gráfico de Olá pode ser métricas diferentes tooshow configurado através de vários intervalos de tempo.</span><span class="sxs-lookup"><span data-stu-id="6a04d-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="6a04d-190">Selecione um toowork do conjunto elástico com.</span><span class="sxs-lookup"><span data-stu-id="6a04d-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="6a04d-191">Em **monitorização de agrupamento elástico** é um gráfico com a etiqueta **utilização de recursos**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="6a04d-192">Clique em Olá gráfico.</span><span class="sxs-lookup"><span data-stu-id="6a04d-192">Click hello chart.</span></span>

    ![Monitorização do conjunto elástico][3]

    <span data-ttu-id="6a04d-194">Olá **métrica** abre painel, que mostra uma vista detalhada do Olá especificado métricas de janela de tempo especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Painel Métricas][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="6a04d-196">visualização de gráfico de Olá toocustomize</span><span class="sxs-lookup"><span data-stu-id="6a04d-196">toocustomize hello chart display</span></span>

<span data-ttu-id="6a04d-197">Pode editar gráfico Olá e Olá painel métrica toodisplay outras métricas, tais como a percentagem de CPU, percentagem de es de dados e a percentagem de es de registo utilizados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="6a04d-198">No painel de métrica de Olá, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-198">On hello metric blade, click **Edit**.</span></span>

    ![Clique em Editar][6]

2. <span data-ttu-id="6a04d-200">No Olá **editar gráfico** painel, selecione um intervalo de tempo (decorridos desde a hora, hoje em dia, ou últimos semana), ou clique em **personalizado** tooselect qualquer data intervalo no Olá últimas duas semanas.</span><span class="sxs-lookup"><span data-stu-id="6a04d-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="6a04d-201">Selecione o tipo de gráfico de Olá (barra ou linha), em seguida, selecione Olá toomonitor de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a04d-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="6a04d-202">Só as métricas com Olá mesma unidade de medida pode ser apresentada no Olá de gráfico em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="6a04d-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="6a04d-203">Por exemplo, se selecionar "percentagem de eDTU", em seguida, pode apenas selecionar outras métricas percentagem como unidade de Olá de medida.</span><span class="sxs-lookup"><span data-stu-id="6a04d-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Clique em Editar](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="6a04d-205">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="6a04d-206">Gerir e monitorizar bases de dados num agrupamento elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="6a04d-207">Bases de dados individuais também podem ser monitorizadas para potenciais problemas.</span><span class="sxs-lookup"><span data-stu-id="6a04d-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="6a04d-208">Em **monitorização de base de dados elásticas**, há um gráfico que mostra as métricas das cinco bases de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="6a04d-209">Por predefinição, Olá gráfico mostra Olá superior 5 as bases de dados no agrupamento de Olá pela utilização de eDTU médio no Olá horas anteriores.</span><span class="sxs-lookup"><span data-stu-id="6a04d-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="6a04d-210">Clique em Olá gráfico.</span><span class="sxs-lookup"><span data-stu-id="6a04d-210">Click hello chart.</span></span>

    ![Monitorização do conjunto elástico][4]

2. <span data-ttu-id="6a04d-212">Olá **utilização de recursos de base de dados** é apresentado o painel.</span><span class="sxs-lookup"><span data-stu-id="6a04d-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="6a04d-213">Isto fornece uma vista detalhada da utilização de base de dados de Olá no agrupamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="6a04d-214">Utilizar grelha Olá na parte inferior do Olá do painel de Olá, pode selecionar bases de dados no Olá conjunto toodisplay respetiva utilização no gráfico de Olá (segurança de bases de dados too5).</span><span class="sxs-lookup"><span data-stu-id="6a04d-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="6a04d-215">Também pode personalizar a janela de métricas e a hora de Olá apresentada no gráfico de Olá clicando **editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Painel de utilização de recursos de base de dados][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="6a04d-217">Vista de Olá toocustomize</span><span class="sxs-lookup"><span data-stu-id="6a04d-217">toocustomize hello view</span></span>

1. <span data-ttu-id="6a04d-218">No Olá **base de dados de utilização de recursos** painel, clique em **editar gráfico**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Clique em Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="6a04d-220">No Olá **editar** gráfico painel, selecione um intervalo de tempo (decorridos desde hora ou últimos 24 horas) ou clique em **personalizado** tooselect dia diferentes no Olá passado toodisplay 2 semanas.</span><span class="sxs-lookup"><span data-stu-id="6a04d-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Clique em personalizada](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="6a04d-222">Clique em Olá **comparar bases de dados ao** pendente tooselect um toouse métrica diferentes ao comparar a bases de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Editar gráfico Olá](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="6a04d-224">tooselect toomonitor de bases de dados</span><span class="sxs-lookup"><span data-stu-id="6a04d-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="6a04d-225">Na lista de base de dados de Olá do Olá **utilização de recursos de base de dados** painel, pode encontrar bases de dados específicos ao procurar nas páginas de Olá na lista de Olá ou ao escrever Olá nome de uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="6a04d-226">Utilize Olá caixa de verificação tooselect Olá da base de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-226">Use hello checkbox tooselect hello database.</span></span>

![Procure toomonitor de bases de dados][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="6a04d-228">Adicione um recurso de conjunto elástico tooan alerta</span><span class="sxs-lookup"><span data-stu-id="6a04d-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="6a04d-229">Pode adicionar regras tooan conjunto elástico que enviar correio eletrónico toopeople ou alerta pontos finais tooURL de cadeias ao conjunto elástico Olá chega a um limiar de utilização que configurou.</span><span class="sxs-lookup"><span data-stu-id="6a04d-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="6a04d-230">**um recurso de alerta tooany tooadd:**</span><span class="sxs-lookup"><span data-stu-id="6a04d-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="6a04d-231">Clique em Olá **utilização de recursos** Olá do gráfico tooopen **métrica** painel, clique em **Adicionar alerta**e, em seguida, preencha as informações de Olá Olá **adicionar um alerta regra** painel (**recursos** automaticamente é configurar o conjunto de Olá de toobe que está a trabalhar com).</span><span class="sxs-lookup"><span data-stu-id="6a04d-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="6a04d-232">Escreva um **nome** e **Descrição** que identifica tooyou alerta Olá e destinatários de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="6a04d-233">Escolha um **métrica** que pretende que o tooalert da lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="6a04d-234">gráfico de Olá dinamicamente mostra a utilização de recursos para esse toohelp métrica que escolher um limiar.</span><span class="sxs-lookup"><span data-stu-id="6a04d-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="6a04d-235">Escolha um **condição** (superior, inferior, etc.) e um **limiar**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="6a04d-236">Escolha um **período** de tempo que Olá métrica regra deve ser satisfeita antes de acionadores de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="6a04d-237">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-237">Click **OK**.</span></span>

<span data-ttu-id="6a04d-238">Para obter mais informações, consulte [criam alertas de base de dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6a04d-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="6a04d-239">Mover uma base de dados para um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="6a04d-240">Pode adicionar ou remover bases de dados a partir de um conjunto existente.</span><span class="sxs-lookup"><span data-stu-id="6a04d-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="6a04d-241">podem estar bases de dados de Olá noutros conjuntos.</span><span class="sxs-lookup"><span data-stu-id="6a04d-241">hello databases can be in other pools.</span></span> <span data-ttu-id="6a04d-242">No entanto, só é possível adicionar bases de dados que estão no Olá mesmo servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="6a04d-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="6a04d-243">No painel de Olá para o conjunto de Olá, sob **bases de dados elásticas** clique **configurar conjunto**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Clique em Configurar conjunto][1]

2. <span data-ttu-id="6a04d-245">No Olá **configurar conjunto** painel, clique em **adicionar toopool**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Clique em Adicionar toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="6a04d-247">No Olá **adicionar bases de dados** painel, base de dados de Olá selecione ou conjunto de toohello tooadd de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="6a04d-248">Em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-248">Then click **Select**.</span></span>

    ![Selecione tooadd de bases de dados](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="6a04d-250">Olá **configurar conjunto** painel agora listas Olá base de dados selecionada toobe adicionado, com o respetivo estado definido demasiado**pendente**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![Adições de agrupamento pendente](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="6a04d-252">No Olá **painel do conjunto de configurar**, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Clicar em Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="6a04d-254">Mover uma base de dados fora de um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="6a04d-255">No Olá **configurar conjunto** painel, base de dados de Olá selecione ou tooremove de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="6a04d-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![lista de bases de dados](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="6a04d-257">Clique em **remover do agrupamento de**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-257">Click **Remove from pool**.</span></span>

    ![lista de bases de dados](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="6a04d-259">Olá **configurar conjunto** painel agora listas Olá base de dados selecionada toobe removido com o respetivo estado definido demasiado**pendente**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![pré-visualização da base de dados adição e remoção](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="6a04d-261">No Olá **painel do conjunto de configurar**, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6a04d-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Clicar em Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="6a04d-263">Alterar as definições de desempenho de um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="6a04d-264">Como monitorizar a utilização de recursos de Olá de um conjunto elástico, poderá descobrir que são necessários alguns ajustes.</span><span class="sxs-lookup"><span data-stu-id="6a04d-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="6a04d-265">Talvez conjunto Olá necessita de uma alteração na Olá limites de desempenho ou o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6a04d-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="6a04d-266">Possivelmente, pretende que as definições de base de dados de Olá toochange no agrupamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="6a04d-267">Pode alterar a configuração de Olá do conjunto de Olá em qualquer altura tooget Olá melhor equilíbrio de desempenho e o custo.</span><span class="sxs-lookup"><span data-stu-id="6a04d-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="6a04d-268">Consulte [quando um conjunto elástico a utilizar?](sql-database-elastic-pool.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6a04d-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="6a04d-269">toochange Olá eDTUs ou armazenamento limites por agrupamento e eDTUs por base de dados:</span><span class="sxs-lookup"><span data-stu-id="6a04d-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="6a04d-270">Abra Olá **configurar conjunto** painel.</span><span class="sxs-lookup"><span data-stu-id="6a04d-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="6a04d-271">Em **as definições do conjunto elástico**, utilize o controlo de deslize toochange Olá as definições do conjunto.</span><span class="sxs-lookup"><span data-stu-id="6a04d-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Utilização de recursos de agrupamento elástico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="6a04d-273">Quando altera a definição de Olá, a apresentação de Olá mostra Olá estimado custo mensal de alteração de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Atualizar um conjunto elástico e o custo mensal novo](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="6a04d-275">Latência de operações do conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="6a04d-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="6a04d-276">Normalmente, a alteração Olá eDTUs de Mín por base de dados ou o número máximo de eDTUs por base de dados conclui em 5 minutos ou menos.</span><span class="sxs-lookup"><span data-stu-id="6a04d-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="6a04d-277">Alterar Olá eDTUs por conjunto depende da quantidade total de Olá de espaço utilizado por todas as bases de dados no agrupamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a04d-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="6a04d-278">Alterações em média 90 minutos ou menos por 100 GB.</span><span class="sxs-lookup"><span data-stu-id="6a04d-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="6a04d-279">Por exemplo, se espaço total Olá utilizado por todas as bases de dados no agrupamento de Olá é 200 GB, em seguida, Olá esperado de latência para alterar o conjunto de Olá eDTU por conjunto é 3 horas ou menos.</span><span class="sxs-lookup"><span data-stu-id="6a04d-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a04d-280">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6a04d-280">Next steps</span></span>

- <span data-ttu-id="6a04d-281">toounderstand que um conjunto elástico estiver, consulte [conjunto elástico da base de dados SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="6a04d-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="6a04d-282">Para obter orientações sobre como utilizar conjuntos elásticos, consulte [considerações sobre preço e desempenho para conjuntos elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="6a04d-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="6a04d-283">scripts de toorun Transact-SQL toouse as tarefas elásticas em qualquer número de bases de dados no agrupamento de Olá, consulte [descrição geral das tarefas elásticas](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a04d-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="6a04d-284">tooquery em qualquer número de bases de dados no agrupamento de Olá, consulte [descrição geral de consulta elástico](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a04d-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="6a04d-285">Para transações qualquer número de bases de dados no agrupamento de Olá, consulte [transações elásticas](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a04d-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
