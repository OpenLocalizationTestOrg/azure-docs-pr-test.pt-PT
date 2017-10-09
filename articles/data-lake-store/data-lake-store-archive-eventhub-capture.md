---
title: dados de aaaCapture dos Event Hubs no Azure Data Lake Store | Microsoft Docs
description: "Dados de toocapture de utilização do Azure Data Lake Store dos Event Hubs"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a><span data-ttu-id="08f4e-103">Dados de toocapture de utilização do Azure Data Lake Store dos Event Hubs</span><span class="sxs-lookup"><span data-stu-id="08f4e-103">Use Azure Data Lake Store toocapture data from Event Hubs</span></span>

<span data-ttu-id="08f4e-104">Saiba como toouse dados do Azure Data Lake Store toocapture recebidos pelo Event Hubs do Azure.</span><span class="sxs-lookup"><span data-stu-id="08f4e-104">Learn how toouse Azure Data Lake Store toocapture data received by Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08f4e-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08f4e-105">Prerequisites</span></span>

* <span data-ttu-id="08f4e-106">**Uma subscrição do Azure**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-106">**An Azure subscription**.</span></span> <span data-ttu-id="08f4e-107">Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08f4e-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="08f4e-108">**Uma conta do Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-108">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="08f4e-109">Para obter instruções sobre como um, ver toocreate [introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08f4e-109">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md).</span></span>

*  <span data-ttu-id="08f4e-110">**Um espaço de nomes de Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-110">**An Event Hubs namespace**.</span></span> <span data-ttu-id="08f4e-111">Para obter instruções, consulte [criar um espaço de nomes de Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span><span class="sxs-lookup"><span data-stu-id="08f4e-111">For instructions, see [Create an Event Hubs namespace](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace).</span></span> <span data-ttu-id="08f4e-112">Certifique-se conta de Data Lake Store Olá e espaço de nomes de Hubs de eventos de Olá Olá mesma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="08f4e-112">Make sure hello Data Lake Store account and hello Event Hubs namespace are in hello same Azure subscription.</span></span>


## <a name="assign-permissions-tooevent-hubs"></a><span data-ttu-id="08f4e-113">Atribua permissões tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="08f4e-113">Assign permissions tooEvent Hubs</span></span>

<span data-ttu-id="08f4e-114">Nesta secção, vai criar uma pasta dentro da conta de olá onde pretende que os dados de Olá toocapture dos Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="08f4e-114">In this section, you create a folder within hello account where you want toocapture hello data from Event Hubs.</span></span> <span data-ttu-id="08f4e-115">É também atribuir permissões tooEvent Hubs para que este pode escrever dados para uma conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="08f4e-115">You also assign permissions tooEvent Hubs so that it can write data into a Data Lake Store account.</span></span> 

1. <span data-ttu-id="08f4e-116">Abra a conta de Data Lake Store olá onde pretende toocapture dados dos Event Hubs e, em seguida, clique em **Explorador de dados**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-116">Open hello Data Lake Store account where you want toocapture data from Event Hubs and then click on **Data Explorer**.</span></span>

    <span data-ttu-id="08f4e-117">![Explorador de dados do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Explorador de dados do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-117">![Data Lake Store data explorer](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")</span></span>

2.  <span data-ttu-id="08f4e-118">Clique em **nova pasta** e, em seguida, introduza um nome para a pasta onde pretende que toocapture Olá dados.</span><span class="sxs-lookup"><span data-stu-id="08f4e-118">Click **New Folder** and then enter a name for folder where you want toocapture hello data.</span></span>

    <span data-ttu-id="08f4e-119">![Crie uma nova pasta no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "crie uma nova pasta no Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-119">![Create a new folder in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")</span></span>

3. <span data-ttu-id="08f4e-120">Atribua permissões na raiz de Olá de Olá Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="08f4e-120">Assign permissions at hello root of hello Data Lake Store.</span></span> 

    <span data-ttu-id="08f4e-121">a.</span><span class="sxs-lookup"><span data-stu-id="08f4e-121">a.</span></span> <span data-ttu-id="08f4e-122">Clique em **Explorador de dados**, selecione de raiz de Olá da Olá conta do Data Lake Store e, em seguida, clique em **acesso**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-122">Click **Data Explorer**, select hello root of hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="08f4e-123">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-123">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="08f4e-124">b.</span><span class="sxs-lookup"><span data-stu-id="08f4e-124">b.</span></span> <span data-ttu-id="08f4e-125">Em **acesso**, clique em **adicionar**, clique em **selecionar utilizador ou grupo**e, em seguida, procure `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="08f4e-125">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="08f4e-126">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-126">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")</span></span>
    
    <span data-ttu-id="08f4e-127">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-127">Click **Select**.</span></span>

    <span data-ttu-id="08f4e-128">c.</span><span class="sxs-lookup"><span data-stu-id="08f4e-128">c.</span></span> <span data-ttu-id="08f4e-129">Em **atribuir permissões**, clique em **selecionar permissões**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-129">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="08f4e-130">Definir **permissões** demasiado**executar**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-130">Set **Permissions** too**Execute**.</span></span> <span data-ttu-id="08f4e-131">Definir **adicionar ao** demasiado**esta pasta e todos os elementos subordinados**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-131">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="08f4e-132">Definir **adicionar como** demasiado**uma entrada de permissão de acesso e uma entrada de permissão predefinidas**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-132">Set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="08f4e-133">![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "atribuir permissões para a raiz do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-133">![Assign permissions for Data Lake Store root](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")</span></span>

    <span data-ttu-id="08f4e-134">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-134">Click **OK**.</span></span>

4. <span data-ttu-id="08f4e-135">Atribua permissões para a pasta de Olá sob a conta do Data Lake Store onde pretende que os dados de toocapture.</span><span class="sxs-lookup"><span data-stu-id="08f4e-135">Assign permissions for hello folder under Data Lake Store account where you want toocapture data.</span></span>

    <span data-ttu-id="08f4e-136">a.</span><span class="sxs-lookup"><span data-stu-id="08f4e-136">a.</span></span> <span data-ttu-id="08f4e-137">Clique em **Explorador de dados**, selecione a pasta de Olá na Olá conta do Data Lake Store e, em seguida, clique em **acesso**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-137">Click **Data Explorer**, select hello folder in hello Data Lake Store account, and then click **Access**.</span></span>

    <span data-ttu-id="08f4e-138">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-138">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")</span></span>

    <span data-ttu-id="08f4e-139">b.</span><span class="sxs-lookup"><span data-stu-id="08f4e-139">b.</span></span> <span data-ttu-id="08f4e-140">Em **acesso**, clique em **adicionar**, clique em **selecionar utilizador ou grupo**e, em seguida, procure `Microsoft.EventHubs`.</span><span class="sxs-lookup"><span data-stu-id="08f4e-140">Under **Access**, click **Add**, click **Select User or Group**, and then search for `Microsoft.EventHubs`.</span></span> 

    <span data-ttu-id="08f4e-141">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-141">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="08f4e-142">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-142">Click **Select**.</span></span>

    <span data-ttu-id="08f4e-143">c.</span><span class="sxs-lookup"><span data-stu-id="08f4e-143">c.</span></span> <span data-ttu-id="08f4e-144">Em **atribuir permissões**, clique em **selecionar permissões**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-144">Under **Assign Permissions**, click **Select Permissions**.</span></span> <span data-ttu-id="08f4e-145">Definir **permissões** demasiado**ler, escrever,** e **executar**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-145">Set **Permissions** too**Read, Write,** and **Execute**.</span></span> <span data-ttu-id="08f4e-146">Definir **adicionar ao** demasiado**esta pasta e todos os elementos subordinados**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-146">Set **Add to** too**This folder and all children**.</span></span> <span data-ttu-id="08f4e-147">Finalmente, defina o **adicionar como** demasiado**uma entrada de permissão de acesso e uma entrada de permissão predefinidas**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-147">Finally, set **Add as** too**An access permission entry and a default permission entry**.</span></span>

    <span data-ttu-id="08f4e-148">![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "atribuir permissões para a pasta do Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-148">![Assign permissions for Data Lake Store folder](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")</span></span>
    
    <span data-ttu-id="08f4e-149">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-149">Click **OK**.</span></span> 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a><span data-ttu-id="08f4e-150">Configurar os Event Hubs toocapture dados tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="08f4e-150">Configure Event Hubs toocapture data tooData Lake Store</span></span>

<span data-ttu-id="08f4e-151">Nesta secção, vai criar um Hub de eventos dentro de um espaço de nomes de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="08f4e-151">In this section, you create an Event Hub within an Event Hubs namespace.</span></span> <span data-ttu-id="08f4e-152">Também configurar Olá Hub de eventos toocapture dados tooan conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="08f4e-152">You also configure hello Event Hub toocapture data tooan Azure Data Lake Store account.</span></span> <span data-ttu-id="08f4e-153">Esta secção assume que já criou um espaço de nomes de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="08f4e-153">This section assumes that you have already created an Event Hubs namespace.</span></span>

2. <span data-ttu-id="08f4e-154">De Olá **descrição geral** painel do espaço de nomes de Event Hubs Olá, clique em **+ Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-154">From hello **Overview** pane of hello Event Hubs namespace, click **+ Event Hub**.</span></span>

    <span data-ttu-id="08f4e-155">![Criar o Hub de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "criar o Hub de eventos")</span><span class="sxs-lookup"><span data-stu-id="08f4e-155">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")</span></span>

3. <span data-ttu-id="08f4e-156">Fornece seguinte Olá valores tooconfigure Event Hubs toocapture tooData data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="08f4e-156">Provide hello following values tooconfigure Event Hubs toocapture data tooData Lake Store.</span></span>

    <span data-ttu-id="08f4e-157">![Criar o Hub de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "criar o Hub de eventos")</span><span class="sxs-lookup"><span data-stu-id="08f4e-157">![Create Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")</span></span>

    <span data-ttu-id="08f4e-158">a.</span><span class="sxs-lookup"><span data-stu-id="08f4e-158">a.</span></span> <span data-ttu-id="08f4e-159">Forneça um nome para Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="08f4e-159">Provide a name for hello Event Hub.</span></span>
    
    <span data-ttu-id="08f4e-160">b.</span><span class="sxs-lookup"><span data-stu-id="08f4e-160">b.</span></span> <span data-ttu-id="08f4e-161">Para este tutorial, defina **contagem da partição** e **mensagem retenção** valores predefinidos de toohello.</span><span class="sxs-lookup"><span data-stu-id="08f4e-161">For this tutorial, set **Partition Count** and **Message Retention** toohello default values.</span></span>
    
    <span data-ttu-id="08f4e-162">c.</span><span class="sxs-lookup"><span data-stu-id="08f4e-162">c.</span></span> <span data-ttu-id="08f4e-163">Definir **capturar** demasiado**no**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-163">Set **Capture** too**On**.</span></span> <span data-ttu-id="08f4e-164">Conjunto Olá **janela de tempo** (frequência toocapture) e **tamanho da janela** (toocapture de tamanho de dados).</span><span class="sxs-lookup"><span data-stu-id="08f4e-164">Set hello **Time Window** (how frequently toocapture) and **Size Window** (data size toocapture).</span></span> 
    
    <span data-ttu-id="08f4e-165">d.</span><span class="sxs-lookup"><span data-stu-id="08f4e-165">d.</span></span> <span data-ttu-id="08f4e-166">Para **capturar fornecedor**, selecione **Azure Data Lake Store** e hello selecione Olá Data Lake Store que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="08f4e-166">For **Capture Provider**, select **Azure Data Lake Store** and hello select hello Data Lake Store you created earlier.</span></span> <span data-ttu-id="08f4e-167">Para **caminho do Data Lake**, introduza o nome de Olá da pasta de Olá que criou no Olá conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="08f4e-167">For **Data Lake Path**, enter hello name of hello folder you created in hello Data Lake Store account.</span></span> <span data-ttu-id="08f4e-168">Só precisa de pasta de toohello tooprovide Olá caminho relativo.</span><span class="sxs-lookup"><span data-stu-id="08f4e-168">You only need tooprovide hello relative path toohello folder.</span></span>

    <span data-ttu-id="08f4e-169">e.</span><span class="sxs-lookup"><span data-stu-id="08f4e-169">e.</span></span> <span data-ttu-id="08f4e-170">Deixe Olá **formatos de nome de ficheiro de captura de exemplo** valor predefinido de toohello.</span><span class="sxs-lookup"><span data-stu-id="08f4e-170">Leave hello **Sample capture file name formats** toohello default value.</span></span> <span data-ttu-id="08f4e-171">Esta opção é regida pelas estrutura de pastas de Olá que é criada na pasta de captura Olá.</span><span class="sxs-lookup"><span data-stu-id="08f4e-171">This option governs hello folder structure that is created under hello capture folder.</span></span>

    <span data-ttu-id="08f4e-172">f.</span><span class="sxs-lookup"><span data-stu-id="08f4e-172">f.</span></span> <span data-ttu-id="08f4e-173">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08f4e-173">Click **Create**.</span></span>

## <a name="test-hello-setup"></a><span data-ttu-id="08f4e-174">O programa de configuração do teste Olá</span><span class="sxs-lookup"><span data-stu-id="08f4e-174">Test hello setup</span></span>

<span data-ttu-id="08f4e-175">Pode agora testar solução Olá através do envio de dados toohello Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="08f4e-175">You can now test hello solution by sending data toohello Azure Event Hub.</span></span> <span data-ttu-id="08f4e-176">Siga as instruções de Olá em [enviar eventos tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span><span class="sxs-lookup"><span data-stu-id="08f4e-176">Follow hello instructions at [Send events tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md).</span></span> <span data-ttu-id="08f4e-177">Depois de começar a enviar dados de Olá, ver dados Olá refletidos no Data Lake Store utilizando a estrutura de pastas de Olá que especificou.</span><span class="sxs-lookup"><span data-stu-id="08f4e-177">Once you start sending hello data, you see hello data reflected in Data Lake Store using hello folder structure you specified.</span></span> <span data-ttu-id="08f4e-178">Por exemplo, verá uma estrutura de pasta, conforme mostrado no Olá seguinte captura de ecrã, no Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="08f4e-178">For example, you see a folder structure, as shown in hello following screenshot, in your Data Lake Store.</span></span>

<span data-ttu-id="08f4e-179">![Exemplo de dados de EventHub no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "EventHub de amostra de dados no Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="08f4e-179">![Sample EventHub data in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")</span></span>

> [!NOTE]
> <span data-ttu-id="08f4e-180">Mesmo se não tiver mensagens entra de Event Hubs, os Event Hubs escreve ficheiros vazios com apenas os cabeçalhos de Olá na Olá conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="08f4e-180">Even if you do not have messages coming into Event Hubs, Event Hubs writes empty files with just hello headers into hello Data Lake Store account.</span></span> <span data-ttu-id="08f4e-181">Olá ficheiros são escritos no Olá mesmo intervalo de tempo que forneceu ao criar Olá Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="08f4e-181">hello files are written at hello same time interval that you provided while creating hello Event Hubs.</span></span>
> 
>

## <a name="analyze-data-in-data-lake-store"></a><span data-ttu-id="08f4e-182">Analisar dados no Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="08f4e-182">Analyze data in Data Lake Store</span></span>

<span data-ttu-id="08f4e-183">Assim que estiver dados Olá no Data Lake Store, pode executar tarefas analíticas tooprocess e crunch dados Olá.</span><span class="sxs-lookup"><span data-stu-id="08f4e-183">Once hello data is in Data Lake Store, you can run analytical jobs tooprocess and crunch hello data.</span></span> <span data-ttu-id="08f4e-184">Consulte [USQL Avro exemplo](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sobre toodo este utilizando o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="08f4e-184">See [USQL Avro Example](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) on how toodo this using Azure Data Lake Analytics.</span></span>
  

## <a name="see-also"></a><span data-ttu-id="08f4e-185">Consultar também</span><span class="sxs-lookup"><span data-stu-id="08f4e-185">See also</span></span>
* [<span data-ttu-id="08f4e-186">Secure data in Data Lake Store (Proteger dados no Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="08f4e-186">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="08f4e-187">Copiar dados de armazenamento de Blobs tooData arquivo Lake do Azure</span><span class="sxs-lookup"><span data-stu-id="08f4e-187">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
