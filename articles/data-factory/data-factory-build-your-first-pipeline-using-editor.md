---
title: "aaaBuild a primeira fábrica de dados (portal do Azure) | Microsoft Docs"
description: "Neste tutorial, crie um exemplo de pipeline do Azure Data Factory com o Editor do Data Factory no Olá portal do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="25363-103">Tutorial: Criar a primeira fábrica de dados do Azure com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="25363-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25363-104">Descrição geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25363-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="25363-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="25363-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="25363-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="25363-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="25363-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25363-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="25363-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25363-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="25363-109">API REST</span><span class="sxs-lookup"><span data-stu-id="25363-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="25363-110">Neste artigo, saiba como toouse [portal do Azure](https://portal.azure.com/) toocreate a primeira fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="25363-111">toodo Olá tutorial, utilizando outras ferramentas/SDKs, selecione uma das opções de Olá Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="25363-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="25363-112">pipeline de Olá neste tutorial tem uma atividade: **atividade do ramo de registo do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="25363-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="25363-113">Esta atividade executa um script de ramo de registo num cluster do Azure HDInsight transformações dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="25363-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="25363-114">pipeline de Olá é agendada toorun depois de um mês entre Olá especificado tempos de início e de fim.</span><span class="sxs-lookup"><span data-stu-id="25363-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="25363-115">pipeline de dados de Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="25363-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="25363-116">Para um tutorial sobre como os dados de toocopy utilizando o Azure Data Factory, consulte [Tutorial: copiar dados do Blob Storage tooSQL da base de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="25363-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="25363-117">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="25363-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="25363-118">Além disso, pode encadeiam duas atividades (executadas uma atividade após outro) definindo o conjunto de dados de saída de Olá de uma atividade como Olá de entrada de conjunto de dados de Olá outra atividade.</span><span class="sxs-lookup"><span data-stu-id="25363-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="25363-119">Para obter mais informações, veja [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) (agendamento e execução no Data Factory).</span><span class="sxs-lookup"><span data-stu-id="25363-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25363-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25363-120">Prerequisites</span></span>
1. <span data-ttu-id="25363-121">Leia [descrição geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e Olá concluída **pré-requisito** passos.</span><span class="sxs-lookup"><span data-stu-id="25363-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="25363-122">Este artigo fornece uma descrição geral conceptual dos Olá serviço Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="25363-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="25363-123">Recomendamos que leia [introdução tooAzure Data Factory](data-factory-introduction.md) artigo para obter uma descrição detalhada do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="25363-124">Criar fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="25363-124">Create data factory</span></span>
<span data-ttu-id="25363-125">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="25363-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="25363-126">Um pipeline pode conter uma atividade ou mais.</span><span class="sxs-lookup"><span data-stu-id="25363-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="25363-127">Por exemplo, dados de toocopy uma atividade de cópia de um arquivo de dados de destino de tooa de origem e um toorun de atividade do ramo de registo do HDInsight um tootransform de script de ramo de registo introduzir dados de saída de tooproduct de dados.</span><span class="sxs-lookup"><span data-stu-id="25363-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="25363-128">Vamos começar a criar a fábrica de dados de Olá neste passo.</span><span class="sxs-lookup"><span data-stu-id="25363-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="25363-129">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="25363-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="25363-130">Clique em **novo** no menu à esquerda Olá, clique em **dados + análise**e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="25363-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Criar painel](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="25363-132">No Olá **nova fábrica de dados** painel, introduza **GetStartedDF** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="25363-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Painel Nova fábrica de dados](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="25363-134">nome de Olá do Olá do Azure data factory deve ser **globalmente exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="25363-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="25363-135">Se receber o erro de Olá: **nome "GetStartedDF" da fábrica de dados não está disponível**.</span><span class="sxs-lookup"><span data-stu-id="25363-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="25363-136">Altere o nome de Olá do Olá data factory (por exemplo, Seunomegetstarteddf) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="25363-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="25363-137">Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="25363-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="25363-138">nome de Olá da fábrica de dados de Olá pode ser registado como um **DNS** nome no Olá futuro e, por conseguinte, ficar publicamente visível.</span><span class="sxs-lookup"><span data-stu-id="25363-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="25363-139">Selecione Olá **subscrição do Azure** onde pretende toobe de fábrica de dados de Olá criado.</span><span class="sxs-lookup"><span data-stu-id="25363-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="25363-140">Selecione o **grupo de recursos** existente ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="25363-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="25363-141">Tutorial de Olá, crie um grupo de recursos denominado: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="25363-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="25363-142">Selecione Olá **localização** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="25363-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="25363-143">São apresentadas apenas as regiões suportadas pelo serviço Data Factory de Olá Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="25363-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="25363-144">Selecione **Pin toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="25363-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="25363-145">Clique em **criar** no Olá **nova fábrica de dados** painel.</span><span class="sxs-lookup"><span data-stu-id="25363-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="25363-146">toocreate instâncias do Data Factory, tem de ser um membro de Olá [contribuinte da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função ao nível do grupo de recursos/subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="25363-147">No dashboard de Olá, verá a seguinte Olá mosaico com o estado: implementação fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="25363-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![Estado de criação da fábrica de dados](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="25363-149">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="25363-149">Congratulations!</span></span> <span data-ttu-id="25363-150">Criou com êxito a sua primeira fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="25363-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="25363-151">Depois de Olá a fábrica de dados foi criada com êxito, será apresentada a página de fábrica do Olá dados, que mostra-lhe Olá conteúdos da fábrica de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Painel Data Factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="25363-153">Antes de criar um pipeline na fábrica de dados de Olá, terá de toocreate algumas entidades do Data Factory primeiro.</span><span class="sxs-lookup"><span data-stu-id="25363-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="25363-154">Primeiro criar serviços ligados toolink dados arquivos/computações tooyour armazenar, definir a entrada e saída de dados de entrada/saída toorepresent conjuntos de dados nos arquivos de dados ligados e, em seguida, criar o pipeline de Olá com uma atividade que utiliza estes conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="25363-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="25363-155">Criar serviços ligados</span><span class="sxs-lookup"><span data-stu-id="25363-155">Create linked services</span></span>
<span data-ttu-id="25363-156">Neste passo, pode liga a sua conta do Storage do Azure e uma fábrica de dados a pedido do Azure HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="25363-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="25363-157">Olá contém Olá dados de entrada e de saída do pipeline de Olá neste exemplo de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="25363-158">Olá serviço ligado do HDInsight é toorun utilizado um script de ramo de registo especificado na atividade de Olá de pipeline de Olá neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="25363-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="25363-159">Identificar quais [arquivo de dados](data-factory-data-movement-activities.md)/[serviços de computação](data-factory-compute-linked-services.md) são utilizados no seu cenário e ligar esses fábrica de dados de toohello serviços criando serviços ligados.</span><span class="sxs-lookup"><span data-stu-id="25363-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="25363-160">Criar o serviço ligado do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="25363-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="25363-161">Neste passo, ligar a fábrica de dados de tooyour de conta do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="25363-162">Neste tutorial, utilize Olá mesma conta de armazenamento do Azure ficheiro de script de dados de entrada/saída toostore e Olá HQL.</span><span class="sxs-lookup"><span data-stu-id="25363-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="25363-163">Clique em **autor e implementar** no Olá **DATA FACTORY** painel **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="25363-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="25363-164">Deverá ver Olá Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="25363-164">You should see hello Data Factory Editor.</span></span>

   ![Mosaico Criar e implementar](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="25363-166">Clique em **Novo arquivo de dados** e escolha **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="25363-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Menu Novo armazenamento de dados – Armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="25363-168">Deverá ver Olá script JSON para criar um Storage do Azure ligado serviço num editor de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Serviço ligado do Storage do Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="25363-170">Substitua **nome da conta** com o nome de Olá da sua conta de armazenamento do Azure e **chave da conta** com a chave de acesso de Olá de Olá conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="25363-171">toolearn como tooget o armazenamento de acesso da chave, consulte Olá obter informações sobre como tooview, copiar e voltar a gerar armazenamento aceder às chaves na [gerir a sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="25363-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="25363-172">Clique em **implementar** no comando Olá barra toodeploy Olá ligado serviço.</span><span class="sxs-lookup"><span data-stu-id="25363-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Botão Implementar](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="25363-174">Depois de Olá serviço ligado é implementado com êxito, Olá **rascunho-1** janela deve desaparecer e verá **AzureStorageLinkedService** na vista de árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="25363-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Serviço Ligado do Storage no menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="25363-176">Criar o serviço ligado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="25363-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="25363-177">Neste passo, pode liga a uma fábrica de dados a pedido HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="25363-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="25363-178">cluster do HDInsight Olá é automaticamente criada no tempo de execução e eliminado depois de ter é processado e ficado inativo para o período de tempo especificado Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="25363-179">No Olá **Editor do Data Factory**, clique em **... Mais**, em **Nova computação** e selecione **Cluster de HDInsight a Pedido**.</span><span class="sxs-lookup"><span data-stu-id="25363-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nova computação](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="25363-181">Copie e cole o seguinte fragmento toohello de Olá **rascunho-1** janela.</span><span class="sxs-lookup"><span data-stu-id="25363-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="25363-182">fragmento JSON de Olá descreve Olá as propriedades utilizadas toocreate Olá HDInsight cluster a pedido.</span><span class="sxs-lookup"><span data-stu-id="25363-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    <span data-ttu-id="25363-183">Olá tabela que se segue fornece descrições para as propriedades JSON de Olá utilizadas no fragmento de Olá:</span><span class="sxs-lookup"><span data-stu-id="25363-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="25363-184">Propriedade</span><span class="sxs-lookup"><span data-stu-id="25363-184">Property</span></span> | <span data-ttu-id="25363-185">Descrição</span><span class="sxs-lookup"><span data-stu-id="25363-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="25363-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="25363-186">ClusterSize</span></span> |<span data-ttu-id="25363-187">Especifica o tamanho de cluster do HDInsight Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="25363-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="25363-188">TimeToLive</span></span> | <span data-ttu-id="25363-189">Especifica esse tempo de inatividade Olá para o cluster do HDInsight Olá, antes de ser eliminado.</span><span class="sxs-lookup"><span data-stu-id="25363-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="25363-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="25363-190">linkedServiceName</span></span> | <span data-ttu-id="25363-191">Especifica a conta de armazenamento Olá, que é utilizado toostore os registos de Olá que são gerados pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="25363-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="25363-192">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="25363-192">Note hello following points:</span></span>

   * <span data-ttu-id="25363-193">Olá Data Factory cria um **baseado em Linux** cluster do HDInsight com Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="25363-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="25363-194">Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="25363-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="25363-195">Também pode utilizar o **seu próprio cluster do HDInsight** em vez de utilizar um cluster do HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="25363-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="25363-196">Veja [HDInsight Linked Service (Serviço Ligado do HDInsight)](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="25363-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="25363-197">cluster do HDInsight Olá cria um **contentor predefinido** no armazenamento de BLOBs de Olá especificado na Olá JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="25363-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="25363-198">HDInsight não é eliminado deste contentor quando cluster Olá é eliminado.</span><span class="sxs-lookup"><span data-stu-id="25363-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="25363-199">Este comportamento é propositado.</span><span class="sxs-lookup"><span data-stu-id="25363-199">This behavior is by design.</span></span> <span data-ttu-id="25363-200">Com o serviço ligado do HDInsight a pedido, é criado um cluster do HDInsight sempre que é processado um setor, exceto se houver um cluster em direto (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="25363-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="25363-201">cluster de Olá é eliminado automaticamente quando o processamento de Olá terminar.</span><span class="sxs-lookup"><span data-stu-id="25363-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="25363-202">À medida que são processados mais setores, verá muitos contentores no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="25363-203">Se não precisar deles para resolução de problemas de tarefas Olá, poderá ser útil toodelete-los armazenamento de Olá tooreduce custo.</span><span class="sxs-lookup"><span data-stu-id="25363-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="25363-204">os nomes de Olá destes contentores seguem um padrão: "adf**nomedafábricadedados**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="25363-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="25363-205">Utilize ferramentas como [Explorador de armazenamento do Microsoft](http://storageexplorer.com/) toodelete contentores no seu Azure armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="25363-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="25363-206">Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="25363-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="25363-207">Clique em **implementar** no comando Olá barra toodeploy Olá ligado serviço.</span><span class="sxs-lookup"><span data-stu-id="25363-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Implementar o serviço ligado de HDInsight a pedido](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="25363-209">Confirme se vê tanto **AzureStorageLinkedService** e **HDInsightOnDemandLinkedService** na vista de árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="25363-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Vista de árvore com serviços ligados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="25363-211">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="25363-211">Create datasets</span></span>
<span data-ttu-id="25363-212">Neste passo, poderá criar conjuntos de dados toorepresent Olá entrada e saída dados para o processamento do ramo de registo.</span><span class="sxs-lookup"><span data-stu-id="25363-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="25363-213">Estes conjuntos de dados Consulte toohello **AzureStorageLinkedService** que criou anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="25363-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="25363-214">Olá tooan de pontos de serviço ligado conta de armazenamento do Azure e os conjuntos de dados especificam um contentor, pasta, nome de ficheiro no armazenamento de Olá que contém a entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="25363-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="25363-215">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="25363-215">Create input dataset</span></span>
1. <span data-ttu-id="25363-216">No Olá **Editor do Data Factory**, clique em **... Mais** na barra de comando Olá, clique em **novo conjunto de dados**e selecione **Blob storage do Azure**.</span><span class="sxs-lookup"><span data-stu-id="25363-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Novo conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="25363-218">Copie e cole Olá seguinte janela do fragmento toohello rascunho-1.</span><span class="sxs-lookup"><span data-stu-id="25363-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="25363-219">No fragmento JSON de Olá, está a criar um conjunto de dados denominado **AzureBlobInput** que representa dados de entrada para uma atividade no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="25363-220">Além disso, especificar que os dados de entrada de Olá estão localizados no contentor de blob Olá denominado **adfgetstarted** e pasta Olá **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="25363-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    <span data-ttu-id="25363-221">Olá tabela que se segue fornece descrições para as propriedades JSON de Olá utilizadas no fragmento de Olá:</span><span class="sxs-lookup"><span data-stu-id="25363-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="25363-222">Propriedade</span><span class="sxs-lookup"><span data-stu-id="25363-222">Property</span></span> | <span data-ttu-id="25363-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="25363-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="25363-224">tipo</span><span class="sxs-lookup"><span data-stu-id="25363-224">type</span></span> |<span data-ttu-id="25363-225">a propriedade de tipo Olá estiver definida demasiado**AzureBlob** porque os dados que residem no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="25363-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="25363-226">linkedServiceName</span></span> |<span data-ttu-id="25363-227">Refere-se toohello **AzureStorageLinkedService** que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="25363-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="25363-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="25363-228">folderPath</span></span> | <span data-ttu-id="25363-229">Especifica o blob Olá **contentor** e Olá **pasta** que contém a entrada de blobs.</span><span class="sxs-lookup"><span data-stu-id="25363-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="25363-230">fileName</span><span class="sxs-lookup"><span data-stu-id="25363-230">fileName</span></span> |<span data-ttu-id="25363-231">Esta propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="25363-231">This property is optional.</span></span> <span data-ttu-id="25363-232">Se omitir esta propriedade, serão escolhidos todos os ficheiros de Olá de Olá folderPath.</span><span class="sxs-lookup"><span data-stu-id="25363-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="25363-233">Neste tutorial, apenas Olá **input.log** está a ser processado.</span><span class="sxs-lookup"><span data-stu-id="25363-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="25363-234">tipo</span><span class="sxs-lookup"><span data-stu-id="25363-234">type</span></span> |<span data-ttu-id="25363-235">ficheiros de registo de Olá estão no formato de texto, pelo que iremos utilizar **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="25363-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="25363-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="25363-236">columnDelimiter</span></span> |<span data-ttu-id="25363-237">colunas nos ficheiros de registo Olá são delimitadas por **vírgula (`,`)**</span><span class="sxs-lookup"><span data-stu-id="25363-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="25363-238">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="25363-238">frequency/interval</span></span> |<span data-ttu-id="25363-239">a frequência definida demasiado**mês** e o intervalo é **1**, que significa que Olá entrada setores estão disponíveis mensalmente.</span><span class="sxs-lookup"><span data-stu-id="25363-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="25363-240">externo</span><span class="sxs-lookup"><span data-stu-id="25363-240">external</span></span> | <span data-ttu-id="25363-241">Esta propriedade for definida demasiado**verdadeiro** se os dados de entrada de Olá não forem gerados por este pipeline.</span><span class="sxs-lookup"><span data-stu-id="25363-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="25363-242">Neste tutorial, ficheiros de input.log Olá não é gerado por este pipeline, pelo que definimos Olá propriedade tootrue.</span><span class="sxs-lookup"><span data-stu-id="25363-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="25363-243">Para obter mais informações sobre estas propriedades JSON, veja [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) (Conector de Blobs do Azure).</span><span class="sxs-lookup"><span data-stu-id="25363-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="25363-244">Clique em **implementar** no comando Olá barra toodeploy Olá recém-criado dataset.</span><span class="sxs-lookup"><span data-stu-id="25363-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="25363-245">Deverá ver o conjunto de dados de Olá na vista de árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="25363-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="25363-246">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="25363-246">Create output dataset</span></span>
<span data-ttu-id="25363-247">Agora, crie Olá dataset toorepresent Olá saída dados de saída armazenados no Olá Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="25363-248">No Olá **Editor do Data Factory**, clique em **... Mais** na barra de comando Olá, clique em **novo conjunto de dados**e selecione **Blob storage do Azure**.</span><span class="sxs-lookup"><span data-stu-id="25363-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="25363-249">Copie e cole Olá seguinte janela do fragmento toohello rascunho-1.</span><span class="sxs-lookup"><span data-stu-id="25363-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="25363-250">No fragmento JSON de Olá, está a criar um conjunto de dados denominado **AzureBlobOutput**e especificar Olá estrutura de dados de Olá que são produzidos pelo script de ramo de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="25363-251">Além disso, especifica que os resultados de Olá são armazenados no contentor de blob Olá denominado **adfgetstarted** e pasta Olá **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="25363-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="25363-252">Olá **disponibilidade** secção especifica o conjunto de dados de saída que Olá é produzido mensalmente.</span><span class="sxs-lookup"><span data-stu-id="25363-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    <span data-ttu-id="25363-253">Consulte **criar conjunto de dados de entrada Olá** secção para obter descrições destas propriedades.</span><span class="sxs-lookup"><span data-stu-id="25363-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="25363-254">Não pode definir a propriedade externa Olá um conjunto de dados de saída como Olá conjunto de dados é produzido pelo serviço do Data Factory Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="25363-255">Clique em **implementar** no comando Olá barra toodeploy Olá recém-criado dataset.</span><span class="sxs-lookup"><span data-stu-id="25363-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="25363-256">Certifique-se de que esse conjunto de dados de Olá é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="25363-256">Verify that hello dataset is created successfully.</span></span>

    ![Vista de árvore com serviços ligados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="25363-258">Criar pipeline</span><span class="sxs-lookup"><span data-stu-id="25363-258">Create pipeline</span></span>
<span data-ttu-id="25363-259">Neste passo, irá criar o seu primeiro pipeline com uma atividade **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="25363-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="25363-260">Setor de entrada está disponível mensalmente (frequência: mês, intervalo: 1), o setor de saída é produzido mensalmente e propriedade do agendador Olá atividade Olá seja também definida toomonthly.</span><span class="sxs-lookup"><span data-stu-id="25363-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="25363-261">Olá as definições de conjunto de dados de saída de Olá e agendador de atividade Olá têm de corresponder.</span><span class="sxs-lookup"><span data-stu-id="25363-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="25363-262">Atualmente, o conjunto de dados de saída é que unidades Olá agenda, pelo que deve criar um conjunto de dados de saída, mesmo se Olá atividade não produzir qualquer saída.</span><span class="sxs-lookup"><span data-stu-id="25363-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="25363-263">Se a atividade de Olá não incluir entradas, pode ignorar o conjunto de dados de entrada Olá criar.</span><span class="sxs-lookup"><span data-stu-id="25363-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="25363-264">Propriedades de Olá utilizadas em Olá JSON a seguir são explicadas em final Olá desta secção.</span><span class="sxs-lookup"><span data-stu-id="25363-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="25363-265">No Olá **Editor do Data Factory**, clique em **reticências (…) Comandos mais** e, em seguida, clique em **novo pipeline**.</span><span class="sxs-lookup"><span data-stu-id="25363-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![botão Novo pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="25363-267">Copie e cole Olá seguinte janela do fragmento toohello rascunho-1.</span><span class="sxs-lookup"><span data-stu-id="25363-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="25363-268">Substitua **storageaccountname** com o nome de Olá da sua conta de armazenamento no Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="25363-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    <span data-ttu-id="25363-269">No fragmento JSON de Olá, está a criar um pipeline que consiste numa única atividade que utiliza o ramo de registo tooprocess dados num cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="25363-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="25363-270">ficheiro de script de ramo de registo de Olá **partitionweblogs.hql**, é armazenada no Olá conta do storage do Azure (especificado pelo scriptLinkedService Olá, denominado **AzureStorageLinkedService**) e, em  **script** pasta no contentor de Olá **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="25363-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="25363-271">Olá **define** secção é utilizado toospecify Olá runtime as definições que são transmitidas toohello script de ramo de registo como valores de configuração do ramo de registo (por exemplo ${hiveconf: inputtable}, ${hiveconf}).</span><span class="sxs-lookup"><span data-stu-id="25363-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="25363-272">Olá **iniciar** e **final** propriedades de pipeline de Olá Especifica o período ativo de Olá de pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="25363-273">No JSON de atividade de Olá, especifique esse Olá script de ramo de registo é executado na computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="25363-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="25363-274">Consulte "JSON do Pipeline" em [Pipelines e atividades no Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON utilizadas no exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="25363-275">Confirme o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="25363-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="25363-276">**Input.log** ficheiro existe Olá **inputdata** pasta de Olá **adfgetstarted** contentor no Olá blob storage do Azure</span><span class="sxs-lookup"><span data-stu-id="25363-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="25363-277">**partitionweblogs.hql** ficheiro existe Olá **script** pasta de Olá **adfgetstarted** contentor no Olá blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="25363-278">Passos de pré-requisitos concluída Olá em Olá [descrição geral do Tutorial](data-factory-build-your-first-pipeline.md) se não vir estes ficheiros.</span><span class="sxs-lookup"><span data-stu-id="25363-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="25363-279">Confirme se substituiu **storageaccountname** com o nome de Olá da sua conta de armazenamento no Olá pipeline de JSON.</span><span class="sxs-lookup"><span data-stu-id="25363-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="25363-280">Clique em **implementar** no comando Olá barra pipeline de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="25363-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="25363-281">Desde Olá **iniciar** e **final** são definidas no passado Olá e **isPaused** é conjunto toofalse, pipeline Olá executa (atividade no pipeline de Olá) imediatamente depois da implementação.</span><span class="sxs-lookup"><span data-stu-id="25363-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="25363-282">Confirme que vê o pipeline de Olá na vista de árvore Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![Vista de árvore com o pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="25363-284">Parabéns, criou com êxito o seu primeiro pipeline!</span><span class="sxs-lookup"><span data-stu-id="25363-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="25363-285">Monitorizar o pipeline</span><span class="sxs-lookup"><span data-stu-id="25363-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="25363-286">Monitorizar o pipeline com a Vista de Diagrama</span><span class="sxs-lookup"><span data-stu-id="25363-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="25363-287">Clique em **X** painéis de Editor do Data Factory tooclose toonavigate fazer uma cópia do painel do Data Factory toohello e clique em **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="25363-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Mosaico do diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="25363-289">Na vista de diagrama Olá, verá uma descrição geral dos pipelines Olá e conjuntos de dados utilizados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="25363-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Vista de Diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="25363-291">tooview todas as atividades no pipeline de Olá, contexto pipeline Olá diagrama e clique em abrir Pipeline.</span><span class="sxs-lookup"><span data-stu-id="25363-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Menu Abrir pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="25363-293">Confirme que vê atividade HDInsightHive de Olá no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Vista Abrir pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="25363-295">fazer uma cópia de toonavigate toohello de vista anterior, clique em **fábrica de dados** no menu de trilho Olá na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="25363-296">No Olá **vista de diagrama**, faça duplo clique em dataset Olá **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="25363-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="25363-297">Confirme que Olá setor estiver no **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="25363-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="25363-298">Esta operação pode demorar alguns minutos para Olá tooshow de setor no estado pronto.</span><span class="sxs-lookup"><span data-stu-id="25363-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="25363-299">Se tal não acontecer depois de aguardar algum tempo para, consulte o artigo se tiver Olá o ficheiro de entrada (input.log) colocado no contentor de direito de Olá (adfgetstarted) e a pasta (inputdata adequados).</span><span class="sxs-lookup"><span data-stu-id="25363-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Setor de entrada no estado pronto](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="25363-301">Clique em **X** tooclose **AzureBlobInput** painel.</span><span class="sxs-lookup"><span data-stu-id="25363-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="25363-302">No Olá **vista de diagrama**, faça duplo clique em dataset Olá **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="25363-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="25363-303">Verá o setor que Olá que está atualmente a ser processado.</span><span class="sxs-lookup"><span data-stu-id="25363-303">You see that hello slice that is currently being processed.</span></span>

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="25363-305">Quando o processamento terminar, verá o setor de Olá no **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="25363-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="25363-307">A criação de um cluster do HDInsight a pedido demora, por norma, algum tempo (cerca de 20 minutos).</span><span class="sxs-lookup"><span data-stu-id="25363-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="25363-308">Por conseguinte, esperar pipeline Olá demorar demasiado **aproximadamente 30 minutos** tooprocess Olá setor.</span><span class="sxs-lookup"><span data-stu-id="25363-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="25363-309">Quando Olá setor estiver no **pronto** de estado, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contentor de armazenamento de BLOBs para Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![dados de saída](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="25363-311">Clique em Olá setor toosee detalhes acerca do mesmo num **setor de dados** painel.</span><span class="sxs-lookup"><span data-stu-id="25363-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Detalhes do setor de dados](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="25363-313">Clique numa atividade executada nos Olá **atividade é executada lista** toosee detalhes sobre uma atividade executam (atividade do ramo de registo no nosso cenário) **detalhes da execução da atividade** janela.</span><span class="sxs-lookup"><span data-stu-id="25363-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Detalhes da execução da atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="25363-315">A partir de ficheiros de registo de Olá, pode ver a consulta do Hive Olá que foi executada e informações de estado.</span><span class="sxs-lookup"><span data-stu-id="25363-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="25363-316">Estes registos são úteis para resolver eventuais problemas.</span><span class="sxs-lookup"><span data-stu-id="25363-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="25363-317">Consulte o artigo [Monitor and manage pipelines using Azure portal blades (Monitorizar e gerir pipelines com os painéis do Portal do Azure)](data-factory-monitor-manage-pipelines.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="25363-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25363-318">ficheiro de entrada Olá é eliminado quando o setor de Olá é processado com êxito.</span><span class="sxs-lookup"><span data-stu-id="25363-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="25363-319">Por conseguinte, se pretender setor de Olá toorerun ou Olá novamente o tutorial, carregue Olá ficheiro de entrada (input.log) toohello na pasta inputdata do contentor adfgetstarted de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="25363-320">Monitorizar o pipeline com a Aplicação de Monitorização e Gestão</span><span class="sxs-lookup"><span data-stu-id="25363-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="25363-321">Também pode utilizar o Monitor e gerir aplicações toomonitor seus pipelines.</span><span class="sxs-lookup"><span data-stu-id="25363-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="25363-322">Para obter detalhes sobre a utilização desta aplicação, veja [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App (Monitorizar e gerir pipelines do Azure Data Factory com a Aplicação de Monitorização e Gestão)](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="25363-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="25363-323">Clique em **Monitor & Gerir** mosaico na Olá home page da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="25363-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![Mosaico Monitorizar e Gerir](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="25363-325">Deverá ver a **Aplicação de Monitorização e Gestão**.</span><span class="sxs-lookup"><span data-stu-id="25363-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="25363-326">Olá alteração **hora de início** e **hora de fim** toomatch início e fim do seu pipeline e clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="25363-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![Aplicação Monitorizar e Gerir](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="25363-328">Selecione uma janela de atividade no Olá **atividade Windows** lista toosee detalhes acerca do mesmo.</span><span class="sxs-lookup"><span data-stu-id="25363-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Detalhes da janela de atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="25363-330">Resumo</span><span class="sxs-lookup"><span data-stu-id="25363-330">Summary</span></span>
<span data-ttu-id="25363-331">Neste tutorial, criou um dados de tooprocess da fábrica de dados do Azure executando o script de ramo de registo num cluster de hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="25363-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="25363-332">Utilizou Olá Editor do Data Factory no Olá toodo portal do Azure de Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="25363-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="25363-333">Criou uma **fábrica de dados** do Azure.</span><span class="sxs-lookup"><span data-stu-id="25363-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="25363-334">Criar dois **serviços ligados**:</span><span class="sxs-lookup"><span data-stu-id="25363-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="25363-335">**Armazenamento do Azure** ligado serviço toolink o armazenamento de Blobs do Azure que contém a fábrica de dados de toohello de ficheiros de entrada/saída.</span><span class="sxs-lookup"><span data-stu-id="25363-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="25363-336">**O Azure HDInsight** a pedido ligado serviço toolink uma fábrica de dados a pedido do HDInsight Hadoop cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="25363-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="25363-337">O Azure Data Factory cria do HDInsight Hadoop, dados de entrada do cluster just-in-time tooprocess e produzir dados de saída.</span><span class="sxs-lookup"><span data-stu-id="25363-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="25363-338">Criar dois **conjuntos de dados**, que descrevem dados de entrada e de saída para a atividade do ramo de registo do HDInsight no pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="25363-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="25363-339">Criar um **pipeline** com uma atividade do **Ramo de Registo do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="25363-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25363-340">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="25363-340">Next Steps</span></span>
<span data-ttu-id="25363-341">Neste artigo, criou um pipeline com uma atividade de transformação (Atividade do HDInsight) que executa um Script de ramo de registo num cluster do HDInsight a pedido.</span><span class="sxs-lookup"><span data-stu-id="25363-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="25363-342">toosee como toouse um toocopy de dados de atividade de cópia de tooAzure um Blob do Azure SQL, consulte [Tutorial: copiar dados de um tooAzure de Blobs do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="25363-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="25363-343">Veja Também</span><span class="sxs-lookup"><span data-stu-id="25363-343">See Also</span></span>
| <span data-ttu-id="25363-344">Tópico</span><span class="sxs-lookup"><span data-stu-id="25363-344">Topic</span></span> | <span data-ttu-id="25363-345">Descrição</span><span class="sxs-lookup"><span data-stu-id="25363-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="25363-346">Pipelines</span><span class="sxs-lookup"><span data-stu-id="25363-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="25363-347">Este artigo ajuda-o a compreender os pipelines e atividades no Azure Data Factory e como toouse-los tooconstruct ponto a ponto condicionados por dados fluxos de trabalho para o seu cenário ou empresa.</span><span class="sxs-lookup"><span data-stu-id="25363-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="25363-348">Conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="25363-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="25363-349">Este artigo ajuda-o a compreender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="25363-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="25363-350">Agendamento e execução</span><span class="sxs-lookup"><span data-stu-id="25363-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="25363-351">Este artigo explica os aspetos de agendamento e execução de Olá do modelo de aplicação do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="25363-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="25363-352">Monitorizar e gerir pipelines com a Aplicação de Monitorização</span><span class="sxs-lookup"><span data-stu-id="25363-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="25363-353">Este artigo descreve como toomonitor, gerir e depurar pipelines utilizando Olá de monitorização e gestão de aplicações.</span><span class="sxs-lookup"><span data-stu-id="25363-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
