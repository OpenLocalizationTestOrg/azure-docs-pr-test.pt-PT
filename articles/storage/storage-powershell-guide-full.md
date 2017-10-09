---
title: aaaUsing Azure PowerShell com o Storage do Azure | Microsoft Docs
description: "Saiba como toouse Olá cmdlets do PowerShell do Azure para armazenamento do Azure toocreate e gerir contas de armazenamento trabalhar com blobs, tabelas, filas e ficheiros configurar e consultar a análise de armazenamento e criar assinaturas de acesso partilhado."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="c4aea-103">Utilizar o Azure PowerShell com o Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="c4aea-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="c4aea-104">Overview</span></span>
<span data-ttu-id="c4aea-105">O Azure PowerShell é um módulo que fornece toomanage de cmdlets do Azure através do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="c4aea-106">É uma shell de linha de comandos e linguagem de script baseada em tarefas concebida especialmente para a administração de sistemas.</span><span class="sxs-lookup"><span data-stu-id="c4aea-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="c4aea-107">Com o PowerShell, pode facilmente controlar e automatizar administração Olá dos seus serviços do Azure e aplicações.</span><span class="sxs-lookup"><span data-stu-id="c4aea-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="c4aea-108">Por exemplo, pode utilizar Olá tooperform cmdlets de Olá mesmas tarefas que pode realizar através de Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4aea-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c4aea-109">Neste guia, iremos irá explorar como toouse Olá [Cmdlets de armazenamento do Azure](/powershell/module/azurerm.storage/#storage) tooperform uma variedade de tarefas de desenvolvimento e de administração com o Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="c4aea-110">Este guia pressupõe que tem experiência anterior na utilização [Storage do Azure](https://azure.microsoft.com/documentation/services/storage/) e [do Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="c4aea-111">Guia de Olá fornece um número de scripts de utilização de Olá toodemonstrate do PowerShell com o Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="c4aea-112">Deve ser atualizado as variáveis do script de Olá, com base na sua configuração antes de executar cada script.</span><span class="sxs-lookup"><span data-stu-id="c4aea-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="c4aea-113">secção primeiro Olá este guia fornece uma leitura rápida no armazenamento do Azure e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="c4aea-114">Para obter informações detalhadas e instruções, iniciar a partir de Olá [pré-requisitos para utilizar o Azure PowerShell com o Storage do Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="c4aea-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="c4aea-115">Introdução ao Storage do Azure e do PowerShell em 5 minutos</span><span class="sxs-lookup"><span data-stu-id="c4aea-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="c4aea-116">Esta secção mostra-lhe como tooaccess Storage do Azure através do PowerShell em 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="c4aea-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="c4aea-117">**Novo tooAzure:** obter uma subscrição do Microsoft Azure e uma conta Microsoft associada essa subscrição.</span><span class="sxs-lookup"><span data-stu-id="c4aea-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="c4aea-118">Para obter informações sobre as opções de compra do Azure, consulte [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/), [opções de compra](https://azure.microsoft.com/pricing/purchase-options/), e [ofertas de membros](https://azure.microsoft.com/pricing/member-offers/) (para os membros de MSDN, Microsoft Partner Network, BizSpark e outros programas Microsoft).</span><span class="sxs-lookup"><span data-stu-id="c4aea-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="c4aea-119">Consulte [atribuir funções de administrador no Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) para obter mais informações sobre as subscrições do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="c4aea-120">**Depois de criar uma conta e subscrição do Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="c4aea-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="c4aea-121">Transfira e instale os mais recentes Olá [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="c4aea-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="c4aea-122">Início Windows PowerShell script ambiente integrado (ISE): Num computador local, aceda toohello **iniciar** menu.</span><span class="sxs-lookup"><span data-stu-id="c4aea-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="c4aea-123">Tipo **ferramentas administrativas** e clique em toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="c4aea-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="c4aea-124">No Olá **ferramentas administrativas** janela, clique com botão direito **ISE do Windows PowerShell**, clique em **executar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="c4aea-125">No **ISE do Windows PowerShell**, clique em **ficheiro** > **novo** toocreate um novo ficheiro de script.</span><span class="sxs-lookup"><span data-stu-id="c4aea-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="c4aea-126">Agora, iremos irá dar-lhe um script simple que mostra básico tooaccess de comandos do PowerShell do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="c4aea-127">script de Olá será primeiro solicitar a sua tooadd de credenciais de conta do Azure conta do Azure toohello PowerShell ambiente local.</span><span class="sxs-lookup"><span data-stu-id="c4aea-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="c4aea-128">Em seguida, o script de Olá predefinir Olá subscrição do Azure e criar uma nova conta de armazenamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="c4aea-129">Em seguida, o script de Olá irá criar um novo contentor nesta nova conta de armazenamento e carregar um contentor de toothat (blob) do ficheiro de imagem existente.</span><span class="sxs-lookup"><span data-stu-id="c4aea-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="c4aea-130">Depois de script de Olá apresenta uma lista de todos os blobs no contentor, irá criar um novo diretório de destino no computador local e transferir o ficheiro de imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="c4aea-131">No Olá seguinte secção de código, selecione o script de Olá entre comentários de Olá **#begin** e **#end**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="c4aea-132">Prima CTRL + C toocopy-toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="c4aea-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="c4aea-133">No **ISE do Windows PowerShell**, prima o script de Olá CTRL + V toocopy.</span><span class="sxs-lookup"><span data-stu-id="c4aea-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="c4aea-134">Clique em **ficheiro** > **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-134">Click **File** > **Save**.</span></span> <span data-ttu-id="c4aea-135">No Olá **guardar como** janela de caixa de diálogo, o nome de Olá do tipo de ficheiro de script de Olá, tais como "mystoragescript."</span><span class="sxs-lookup"><span data-stu-id="c4aea-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="c4aea-136">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-136">Click **Save**.</span></span>
7. <span data-ttu-id="c4aea-137">Agora, terá de variáveis de script tooupdate Olá com base nas suas definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="c4aea-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="c4aea-138">Tem de atualizar Olá **$SubscriptionName** variável com a sua própria subscrição.</span><span class="sxs-lookup"><span data-stu-id="c4aea-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="c4aea-139">Pode manter Olá outras variáveis conforme especificado no script de Olá ou atualizá-las conforme desejar.</span><span class="sxs-lookup"><span data-stu-id="c4aea-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="c4aea-140">**$SubscriptionName:** tem de atualizar esta variável com o seu próprio nome de subscrição.</span><span class="sxs-lookup"><span data-stu-id="c4aea-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="c4aea-141">Siga um dos seguintes três formas toolocate Olá nome da sua subscrição de Olá:</span><span class="sxs-lookup"><span data-stu-id="c4aea-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="c4aea-142">a.</span><span class="sxs-lookup"><span data-stu-id="c4aea-142">a.</span></span> <span data-ttu-id="c4aea-143">No **ISE do Windows PowerShell**, clique em **ficheiro** > **novo** toocreate um novo ficheiro de script.</span><span class="sxs-lookup"><span data-stu-id="c4aea-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="c4aea-144">Script toohello novo ficheiro de script a seguir de Olá cópia e clique em **depurar** > **executar**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="c4aea-145">Olá seguinte script será primeiro peça ao seu tooadd de credenciais de conta do Azure conta do Azure toohello PowerShell ambiente local e em seguida, mostra todas as subscrições de Olá que estão ligados toohello local a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="c4aea-146">Tome nota do nome Olá subscrição Olá que pretende que toouse ao seguir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="c4aea-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="c4aea-147">b.</span><span class="sxs-lookup"><span data-stu-id="c4aea-147">b.</span></span> <span data-ttu-id="c4aea-148">toolocate e copie a sua subscrição nome no Olá [portal do Azure](https://portal.azure.com), no Olá menu do Hub no Olá à esquerda, clique em **subscrições**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="c4aea-149">Copie o nome de Olá da subscrição que pretende que toouse durante a execução de scripts de Olá neste guia.</span><span class="sxs-lookup"><span data-stu-id="c4aea-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Portal do Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="c4aea-151">c.</span><span class="sxs-lookup"><span data-stu-id="c4aea-151">c.</span></span> <span data-ttu-id="c4aea-152">toolocate e copie a sua subscrição nome no Olá [Portal clássico do Azure](https://manage.windowsazure.com/), desloque para baixo e clique em **definições** no Olá à esquerda do lado do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="c4aea-153">Clique em **subscrições** toosee uma lista das suas subscrições.</span><span class="sxs-lookup"><span data-stu-id="c4aea-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="c4aea-154">Nome de Olá de cópia da subscrição que pretende que sejam toouse durante a execução de scripts de Olá fornecidos neste guia.</span><span class="sxs-lookup"><span data-stu-id="c4aea-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![Portal Clássico do Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="c4aea-156">**$StorageAccountName:** utilizar Olá fornecido nome de script de Olá ou introduza um novo nome para a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="c4aea-157">**Importante:** Olá nome da conta de armazenamento Olá tem de ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="c4aea-158">Tem de ser em minúsculas, demasiado!</span><span class="sxs-lookup"><span data-stu-id="c4aea-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="c4aea-159">**$Location:** utilizar Olá fornecido "EUA Oeste" no script de Olá ou escolher outras localizações do Azure, como EUA leste, Europa do Norte e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="c4aea-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="c4aea-160">**$ContainerName:** utilizar Olá fornecido nome de script de Olá ou introduza um novo nome para o contentor.</span><span class="sxs-lookup"><span data-stu-id="c4aea-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="c4aea-161">**$ImageToUpload:** introduza uma imagem de tooa caminho no seu computador local, como: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="c4aea-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="c4aea-162">**$DestinationFolder:** introduza um caminho os tooa diretório local toostore ficheiros transferidos do armazenamento do Azure, tais como: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="c4aea-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="c4aea-163">Depois de atualizar as variáveis do script de Olá no ficheiro de "mystoragescript.ps1" Olá, clique em **ficheiro** > **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="c4aea-164">Em seguida, clique em **depurar** > **executar** ou prima **F5** script de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="c4aea-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="c4aea-165">Após a execução do script Olá, deve ter uma pasta de destino local que inclua o ficheiro de imagem de Olá transferido.</span><span class="sxs-lookup"><span data-stu-id="c4aea-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="c4aea-166">Olá seguinte captura de ecrã mostra um exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="c4aea-166">hello following screenshot shows an example output:</span></span>

![Transferir Blobs](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="c4aea-168">Olá "com o PowerShell e o armazenamento do Azure em 5 minutos" secção introdução fornecida uma introdução rápida sobre toouse Azure PowerShell com o Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="c4aea-169">Para obter informações detalhadas e instruções, Aconselhamo-lo Olá tooread secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4aea-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="c4aea-170">Pré-requisitos para utilizar o Azure PowerShell com o Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="c4aea-171">Precisa de uma conta e subscrição toorun Olá cmdlets do Azure PowerShell fornecidos neste guia, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="c4aea-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="c4aea-172">O Azure PowerShell é um módulo que fornece toomanage de cmdlets do Azure através do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="c4aea-173">Para obter informações sobre como instalar e configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c4aea-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="c4aea-174">Recomendamos que pode transfere e instalar ou atualizar o módulo Azure PowerShell mais recente do toohello antes de utilizar este guia.</span><span class="sxs-lookup"><span data-stu-id="c4aea-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="c4aea-175">Pode executar cmdlets Olá na consola do Olá padrão do Windows PowerShell ou Olá Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="c4aea-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="c4aea-176">Por exemplo, tooopen **ISE do Windows PowerShell**, aceda toohello menu de iniciar, escreva ferramentas administrativas e clique em toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="c4aea-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="c4aea-177">Na janela do Olá ferramentas administrativas, clique no ISE do Windows PowerShell, clique em executar como administrador.</span><span class="sxs-lookup"><span data-stu-id="c4aea-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="c4aea-178">Como contas de armazenamento toomanage no Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="c4aea-179">Vamos observe gerir contas do storage no Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4aea-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="c4aea-180">Como tooset uma predefinição de subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="c4aea-181">toomanage o Storage do Azure com o Azure PowerShell, terá de tooauthenticate cliente ambiente com o Azure através de autenticação do Azure Active Directory ou a autenticação baseada em certificado.</span><span class="sxs-lookup"><span data-stu-id="c4aea-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="c4aea-182">Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tutorial.</span><span class="sxs-lookup"><span data-stu-id="c4aea-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="c4aea-183">Este guia utiliza a autenticação do Azure Active Directory de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="c4aea-184">No ISE do Windows PowerShell, escreva o Olá tooadd de comando a seguir a conta do Azure toohello PowerShell ambiente local:</span><span class="sxs-lookup"><span data-stu-id="c4aea-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="c4aea-185">Na janela de "Iniciar sessão tooMicrosoft Azure" Olá, endereço de correio eletrónico do tipo Olá e palavra-passe associada à sua conta.</span><span class="sxs-lookup"><span data-stu-id="c4aea-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="c4aea-186">Azure autentica guarda as informações de credencial de Olá e, em seguida, fecha a janela de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="c4aea-187">Em seguida, execute Olá Olá tooview de comandos do Azure contas no seu ambiente de PowerShell local e verifique se a sua conta é apresentada a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4aea-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="c4aea-188">Em seguida, executar Olá seguintes cmdlet tooview todas as subscrições de Olá que estão ligados toohello local a sessão do PowerShell e certifique-se de que a sua subscrição está listada:</span><span class="sxs-lookup"><span data-stu-id="c4aea-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="c4aea-189">tooset uma predefinição de subscrição do Azure, execute o cmdlet Olá Select-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="c4aea-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="c4aea-190">Verifique o nome de Olá da subscrição da predefinição de Olá executando o cmdlet Get-AzureSubscription de Olá:</span><span class="sxs-lookup"><span data-stu-id="c4aea-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="c4aea-191">toosee todos os Olá disponíveis cmdlets do PowerShell para o armazenamento do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="c4aea-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="c4aea-192">Como toocreate uma nova conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="c4aea-193">toouse storage do Azure, terá de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="c4aea-194">Pode criar uma nova conta de armazenamento do Azure após ter configurado a sua subscrição do computador tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="c4aea-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="c4aea-195">Execute Olá Get-AzureLocation cmdlet toofind todas as localizações de centros de dados disponíveis Olá:</span><span class="sxs-lookup"><span data-stu-id="c4aea-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="c4aea-196">Em seguida, execute Olá AzureStorageAccount novo cmdlet toocreate uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="c4aea-197">Olá exemplo seguinte cria uma nova conta de armazenamento no Centro de dados do Olá "EUA Oeste".</span><span class="sxs-lookup"><span data-stu-id="c4aea-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="c4aea-198">nome de Olá da sua conta de armazenamento tem de ser exclusivo no Azure e tem de ser em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c4aea-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="c4aea-199">Para as convenções de nomenclatura e restrições, consulte [sobre contas de armazenamento do Azure](storage-create-storage-account.md) e [nomenclatura e referência de contentores, Blobs e metadados](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="c4aea-200">Como tooset uma conta de armazenamento do Azure predefinida</span><span class="sxs-lookup"><span data-stu-id="c4aea-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="c4aea-201">Pode ter várias contas de armazenamento na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="c4aea-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="c4aea-202">Pode escolher um deles e defina-o como conta do storage predefinida Olá para todos os Olá armazenamento comandos no Olá mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="c4aea-203">Isto permite-lhe os comandos do toorun Olá Azure PowerShell armazenamento sem especificar o contexto de armazenamento Olá explicitamente.</span><span class="sxs-lookup"><span data-stu-id="c4aea-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="c4aea-204">tooset uma conta de armazenamento predefinido para a sua subscrição, pode executar o cmdlet do Set-AzureSubscription de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="c4aea-205">Em seguida, execute Olá Get-AzureSubscription cmdlet tooverify que a conta de armazenamento Olá está associada a sua conta de subscrição predefinida.</span><span class="sxs-lookup"><span data-stu-id="c4aea-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="c4aea-206">Este comando devolve as propriedades de subscrição de Olá na subscrição atual Olá, incluindo a respetiva conta de armazenamento atual.</span><span class="sxs-lookup"><span data-stu-id="c4aea-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="c4aea-207">Como toolist todo o armazenamento do Azure contas numa subscrição</span><span class="sxs-lookup"><span data-stu-id="c4aea-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="c4aea-208">Cada subscrição do Azure pode ter segurança too100 contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="c4aea-209">Para informações mais atualizadas à sua Olá, nos limites, consulte [subscrição do Azure e limites de serviço, Quotas e restrições](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="c4aea-210">Execute Olá cmdlet toofind nome Olá e estado Olá de contas de armazenamento na subscrição atual Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c4aea-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="c4aea-211">Como toocreate um contexto de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="c4aea-212">O contexto de armazenamento do Azure é um objeto de credenciais de armazenamento do PowerShell tooencapsulate Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="c4aea-213">Utilizar um contexto de armazenamento durante a execução de qualquer cmdlet subsequente permite tooauthenticate o pedido sem especificar explicitamente a conta de armazenamento Olá e a sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="c4aea-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="c4aea-214">Pode criar um contexto de armazenamento em várias formas, como a chave de acesso e o nome de conta do storage, token de assinatura (SAS) de acesso partilhado, cadeia de ligação, ou anonymous.</span><span class="sxs-lookup"><span data-stu-id="c4aea-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="c4aea-215">Para obter mais informações, consulte [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="c4aea-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="c4aea-216">Utilize um dos seguintes três formas toocreate de Olá um contexto de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="c4aea-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="c4aea-217">Executar Olá [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind cmdlet terminar a chave de acesso de armazenamento primário Olá para a sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="c4aea-218">Em seguida, chame Olá [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate um contexto de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="c4aea-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="c4aea-219">Gerar um token de assinatura de acesso partilhado para um contentor de armazenamento do Azure e utilizá-lo toocreate um contexto de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="c4aea-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="c4aea-220">Para obter mais informações, consulte [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) e [através de acesso partilhado assinaturas (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="c4aea-221">Em alguns casos, poderá ser útil pontos finais de serviço do toospecify Olá quando criar um contexto de armazenamento nova.</span><span class="sxs-lookup"><span data-stu-id="c4aea-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="c4aea-222">Isto poderá ser necessário quando tiver registado um nome de domínio personalizado para a sua conta de armazenamento com o serviço de Blob Olá ou se quiser toouse uma assinatura de acesso partilhado para aceder a recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="c4aea-223">Defina pontos finais de serviço Olá numa cadeia de ligação e utilizá-lo toocreate um contexto de armazenamento novo conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c4aea-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="c4aea-224">Para obter mais informações sobre como tooconfigure uma cadeia de ligação de armazenamento, consulte [configurar cadeias de ligação](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="c4aea-225">Agora que tem de configurar o computador e aprendeu como toomanage subscrições e contas de armazenamento com o Azure PowerShell, volte toohello seguinte secção toolearn como blobs toomanage do Azure e instantâneos do blob.</span><span class="sxs-lookup"><span data-stu-id="c4aea-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="c4aea-226">Como tooretrieve e voltar a gerar chaves de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="c4aea-227">Uma conta de armazenamento do Azure inclui duas chaves de conta.</span><span class="sxs-lookup"><span data-stu-id="c4aea-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="c4aea-228">Pode utilizar Olá seguintes cmdlet tooretrieve as suas chaves.</span><span class="sxs-lookup"><span data-stu-id="c4aea-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="c4aea-229">Utilize Olá seguintes cmdlet tooretrieve uma chave específica.</span><span class="sxs-lookup"><span data-stu-id="c4aea-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="c4aea-230">Os valores válidos são principais e secundários.</span><span class="sxs-lookup"><span data-stu-id="c4aea-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="c4aea-231">Se quiser tooregenerate as chaves, utilize Olá seguinte cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="c4aea-232">Valores válidos para - KeyType são "Primário" ou "Secundário"</span><span class="sxs-lookup"><span data-stu-id="c4aea-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="c4aea-233">Como blobs toomanage do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="c4aea-234">Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, tais como texto ou dados binários, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c4aea-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="c4aea-235">Esta secção assume que já estiver familiarizado com conceitos de serviço de armazenamento de Blobs do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="c4aea-236">Para obter informações detalhadas, consulte [introdução ao Blob storage através do .NET](storage-dotnet-how-to-use-blobs.md) e [conceitos do serviço Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="c4aea-237">Como toocreate um contentor</span><span class="sxs-lookup"><span data-stu-id="c4aea-237">How toocreate a container</span></span>
<span data-ttu-id="c4aea-238">Todos os BLOBs no armazenamento do Azure tem de ser um contentor.</span><span class="sxs-lookup"><span data-stu-id="c4aea-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="c4aea-239">Pode criar um contentor privado utilizando o cmdlet Olá AzureStorageContainer novo:</span><span class="sxs-lookup"><span data-stu-id="c4aea-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="c4aea-240">Existem três níveis de acesso de leitura anónimo: **desativar**, **Blob**, e **contentor**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="c4aea-241">tooprevent anónimo tooblobs, parâmetro de permissão de Olá do conjunto de acesso demasiado**desativar**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="c4aea-242">Por predefinição, o novo contentor de Olá é privado e pode ser acedido apenas por proprietário da conta Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="c4aea-243">público anónimo tooallow ler tooblob aceder a recursos, mas não toocontainer metadados ou toohello uma lista de blobs no contentor de Olá, defina o parâmetro de permissão de Olá demasiado**Blob**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="c4aea-244">público completa tooallow ler tooblob aceder a recursos, os metadados do contentor e Olá lista de blobs no contentor de Olá, defina o parâmetro de permissão de Olá demasiado**contentor**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="c4aea-245">Para obter mais informações, consulte [gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-245">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="c4aea-246">Como tooupload um blob para um contentor</span><span class="sxs-lookup"><span data-stu-id="c4aea-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="c4aea-247">O Blob Storage do Azure suporta blobs de blocos e blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="c4aea-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="c4aea-248">Para obter mais informações, consulte [compreender os Blobs de blocos, os BLobs de acréscimo e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="c4aea-249">tooupload os blobs no contentor de tooa, pode utilizar Olá [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="c4aea-250">Por predefinição, este comando carrega o blob de bloco tooa do Olá ficheiros locais.</span><span class="sxs-lookup"><span data-stu-id="c4aea-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="c4aea-251">tipo de Olá toospecify para BLOBs Olá, pode utilizar o parâmetro de - BlobType Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="c4aea-252">Olá exemplo a seguir executa Olá [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget Olá todos os ficheiros na pasta especificada Olá e, em seguida, transmite-os cmdlet seguinte toohello utilizando o operador de pipeline de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="c4aea-253">Olá [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet carrega o contentor de tooyour Olá ficheiros locais:</span><span class="sxs-lookup"><span data-stu-id="c4aea-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="c4aea-254">Como toodownload blobs a partir de um contentor</span><span class="sxs-lookup"><span data-stu-id="c4aea-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="c4aea-255">Olá seguinte o exemplo demonstra como toodownload blobs a partir de um contentor.</span><span class="sxs-lookup"><span data-stu-id="c4aea-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="c4aea-256">exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento utilizando Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso primária.</span><span class="sxs-lookup"><span data-stu-id="c4aea-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="c4aea-257">Em seguida, o exemplo de Olá obtém uma referência de blob utilizando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="c4aea-258">Em seguida, o exemplo de Olá utiliza Olá [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobs de toodownload cmdlet na pasta de destino local Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="c4aea-259">Como toocopy blobs a partir de um tooanother de contentor de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c4aea-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="c4aea-260">Pode copiar os blobs em contas do storage e regiões no modo assíncrono.</span><span class="sxs-lookup"><span data-stu-id="c4aea-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="c4aea-261">Olá exemplo seguinte demonstra como toocopy blobs do armazenamento de um contentor tooanother em duas contas de armazenamento diferente.</span><span class="sxs-lookup"><span data-stu-id="c4aea-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="c4aea-262">exemplo de Olá primeiro define variáveis para contas de armazenamento de origem e de destino e, em seguida, cria um contexto de armazenamento para cada conta.</span><span class="sxs-lookup"><span data-stu-id="c4aea-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="c4aea-263">Em seguida, o exemplo de Olá copia blobs a partir Olá origem contentor toohello destino contentor utilizando Olá [início AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="c4aea-264">exemplo de Olá assume que contas de armazenamento de origem e destino Olá e contentores de existir.</span><span class="sxs-lookup"><span data-stu-id="c4aea-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="c4aea-265">Tenha em atenção que este exemplo efetua uma cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="c4aea-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="c4aea-266">Pode monitorizar o estado de Olá de cada cópia executando Olá [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="c4aea-267">Como toocopy blobs a partir de uma localização secundária</span><span class="sxs-lookup"><span data-stu-id="c4aea-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="c4aea-268">Pode copiar os blobs da localização secundária de Olá de uma conta ativada RA-GRS.</span><span class="sxs-lookup"><span data-stu-id="c4aea-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="c4aea-269">Como toodelete um blob</span><span class="sxs-lookup"><span data-stu-id="c4aea-269">How toodelete a blob</span></span>
<span data-ttu-id="c4aea-270">toodelete um blob, obtenha primeiro uma referência de blob e, em seguida, chame o cmdlet Remove-AzureStorageBlob de Olá no mesmo.</span><span class="sxs-lookup"><span data-stu-id="c4aea-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="c4aea-271">Olá seguinte o exemplo elimina todos os blobs Olá num determinado contentor.</span><span class="sxs-lookup"><span data-stu-id="c4aea-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="c4aea-272">exemplo de Olá primeiro define as variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="c4aea-273">Em seguida, o exemplo de Olá obtém uma referência de blob utilizando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá e executa o cmdlet [remover AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs a partir de um contentor no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="c4aea-274">Como instantâneos do blob toomanage do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="c4aea-275">Azure permite-lhe criar um instantâneo de um blob.</span><span class="sxs-lookup"><span data-stu-id="c4aea-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="c4aea-276">Um instantâneo é uma versão só de leitura de um blob que é executada num ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="c4aea-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="c4aea-277">Assim que tiver sido criado um instantâneo,-lo pode ser ler, copiar, ou eliminada, mas não modificado.</span><span class="sxs-lookup"><span data-stu-id="c4aea-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="c4aea-278">Os instantâneos proporcionar uma tooback de forma a segurança de um blob como é apresentado um momento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="c4aea-279">Para obter mais informações, consulte [criar um instantâneo de um Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="c4aea-280">Como toocreate um instantâneo de blob</span><span class="sxs-lookup"><span data-stu-id="c4aea-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="c4aea-281">toocreate um snaphot de um blob, obtenha primeiro uma referência de blob e, em seguida, chame Olá `ICloudBlob.CreateSnapshot` método.</span><span class="sxs-lookup"><span data-stu-id="c4aea-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="c4aea-282">Olá exemplo seguinte define primeiro as variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="c4aea-283">Em seguida, o exemplo de Olá obtém uma referência de blob utilizando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá e executa o cmdlet [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="c4aea-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="c4aea-284">Como instantâneos de toolist um blob</span><span class="sxs-lookup"><span data-stu-id="c4aea-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="c4aea-285">Pode criar tantas instantâneos quantas quiser a um blob.</span><span class="sxs-lookup"><span data-stu-id="c4aea-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="c4aea-286">Pode listar os instantâneos de Olá associados à sua tootrack blob os instantâneos atuais.</span><span class="sxs-lookup"><span data-stu-id="c4aea-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="c4aea-287">Olá exemplo seguinte utiliza uma Olá predefinida de blob e chamadas [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) instantâneos de Olá toolist cmdlet desse blob.</span><span class="sxs-lookup"><span data-stu-id="c4aea-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="c4aea-288">Como toocopy um instantâneo de um blob</span><span class="sxs-lookup"><span data-stu-id="c4aea-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="c4aea-289">Pode copiar um instantâneo de um instantâneo do blob toorestore Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="c4aea-290">Para obter informações detalhadas e restrições, consulte [criar um instantâneo de um Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="c4aea-291">Olá exemplo seguinte define primeiro as variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="c4aea-292">Em seguida, o exemplo de Olá define variáveis de nome de contentor e BLOBs Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="c4aea-293">exemplo de Olá obtém uma referência de blob utilizando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá e executa o cmdlet [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="c4aea-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="c4aea-294">Em seguida, o exemplo de Olá executa Olá [início AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy Olá instantâneo um blob utilizando o objeto de ICloudBlob de Olá de blob de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="c4aea-295">Certifique-se as variáveis de Olá tooupdate com base na sua configuração antes de exemplo de Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="c4aea-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="c4aea-296">Tenha em atenção que Olá seguinte o exemplo assume que Olá contentores de origem e de destino e o blob de origem Olá já existe.</span><span class="sxs-lookup"><span data-stu-id="c4aea-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="c4aea-297">Agora que tem aprendeu como toomanage Azure blobs e BLOBs instantâneos com o Azure PowerShell, aceda a toolearn de secção seguinte toohello como toomanage tabelas, filas e os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="c4aea-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="c4aea-298">Como toomanage Azure tabelas e entidades de tabela</span><span class="sxs-lookup"><span data-stu-id="c4aea-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="c4aea-299">Serviço de armazenamento de tabela do Azure é um arquivo de dados NoSQL, que pode utilizar toostore e consultar conjuntos enormes de dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="c4aea-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="c4aea-300">componentes principais do Olá do serviço de Olá são propriedades, tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="c4aea-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="c4aea-301">Uma tabela é uma coleção de entidades.</span><span class="sxs-lookup"><span data-stu-id="c4aea-301">A table is a collection of entities.</span></span> <span data-ttu-id="c4aea-302">Uma entidade é um conjunto de propriedades.</span><span class="sxs-lookup"><span data-stu-id="c4aea-302">An entity is a set of properties.</span></span> <span data-ttu-id="c4aea-303">Cada entidade pode ter propriedades de too252, que são todos os pares nome-valor.</span><span class="sxs-lookup"><span data-stu-id="c4aea-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="c4aea-304">Esta secção assume que já estiver familiarizado com conceitos de serviço de armazenamento do Azure tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="c4aea-305">Para obter informações detalhadas, consulte [Olá compreender o modelo de dados do serviço tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx) e [introdução ao Table storage do Azure através do .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="c4aea-306">Olá subsecções a seguir, irá aprender como toomanage Table storage do Azure service com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="c4aea-307">Hello os cenários abrangidos incluem **criar**, **eliminar**, e **obter** **tabelas**, bem como **adicionar**, **consultar**, e **eliminar as entidades da tabela**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="c4aea-308">Como toocreate uma tabela</span><span class="sxs-lookup"><span data-stu-id="c4aea-308">How toocreate a table</span></span>
<span data-ttu-id="c4aea-309">Cada tabela têm de residir numa conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="c4aea-310">Olá exemplo seguinte demonstra como toocreate uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="c4aea-311">exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso a utilizar.</span><span class="sxs-lookup"><span data-stu-id="c4aea-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="c4aea-312">Em seguida, utiliza Olá [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="c4aea-313">Como tooretrieve uma tabela</span><span class="sxs-lookup"><span data-stu-id="c4aea-313">How tooretrieve a table</span></span>
<span data-ttu-id="c4aea-314">Pode consultar e obter uma ou todas as tabelas numa conta do Storage.</span><span class="sxs-lookup"><span data-stu-id="c4aea-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="c4aea-315">Olá exemplo seguinte demonstra como tooretrieve utilizando uma tabela indicada Olá [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="c4aea-316">Se chamar o cmdlet Get-AzureStorageTable de Olá sem quaisquer parâmetros, obtém todas as tabelas de armazenamento para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="c4aea-317">Como toodelete uma tabela</span><span class="sxs-lookup"><span data-stu-id="c4aea-317">How toodelete a table</span></span>
<span data-ttu-id="c4aea-318">Pode eliminar uma tabela a partir de uma conta de armazenamento utilizando Olá [remover AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="c4aea-319">Como toomanage tabela entidades</span><span class="sxs-lookup"><span data-stu-id="c4aea-319">How toomanage table entities</span></span>
<span data-ttu-id="c4aea-320">Atualmente, o Azure PowerShell não fornece as entidades da tabela toomanage cmdlets diretamente.</span><span class="sxs-lookup"><span data-stu-id="c4aea-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="c4aea-321">operações de tooperform em entidades de tabela, pode utilizar classes Olá indicadas na Olá [biblioteca de clientes do Storage do Azure para .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="c4aea-322">Como tooadd tabela entidades</span><span class="sxs-lookup"><span data-stu-id="c4aea-322">How tooadd table entities</span></span>
<span data-ttu-id="c4aea-323">tooadd uma tabela de tooa de entidade, primeiro crie um objeto que define as propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="c4aea-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="c4aea-324">Uma entidade pode ter propriedades de too255, incluindo 3 Propriedades do sistema: **PartitionKey**, **RowKey**, e **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="c4aea-325">É responsável por a inserir e a atualizar os valores de Olá de **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="c4aea-326">Olá servidor gere valor Olá **Timestamp**, que não pode ser modificado.</span><span class="sxs-lookup"><span data-stu-id="c4aea-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="c4aea-327">Em conjunto Olá **PartitionKey** e **RowKey** identificar de forma exclusiva cada entidade dentro de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c4aea-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="c4aea-328">**PartitionKey**: determina partição Olá entidade Olá armazenadas.</span><span class="sxs-lookup"><span data-stu-id="c4aea-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="c4aea-329">**RowKey**: identifica de forma exclusiva a entidade de Olá dentro de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="c4aea-330">Pode definir too252 propriedades personalizadas para uma entidade.</span><span class="sxs-lookup"><span data-stu-id="c4aea-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="c4aea-331">Para obter mais informações, consulte [Olá compreender o modelo de dados do serviço tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="c4aea-332">Olá exemplo seguinte demonstra como tabela de tooa tooadd entidades.</span><span class="sxs-lookup"><span data-stu-id="c4aea-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="c4aea-333">exemplo de Olá mostra como tooretrieve Olá tabela do empregado e adiciona várias entidades.</span><span class="sxs-lookup"><span data-stu-id="c4aea-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="c4aea-334">Em primeiro lugar, estabelece uma ligação tooAzure armazenamento Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso a utilizar.</span><span class="sxs-lookup"><span data-stu-id="c4aea-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="c4aea-335">Em seguida, obtém Olá fornecido tabela utilizando Olá [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="c4aea-336">Se a tabela Olá não existe, Olá [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet é utilizado toocreate uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="c4aea-337">Em seguida, o exemplo Olá define uma tabela de toohello adicionar entidade tooadd entidades de função personalizada, especificando a partição de cada entidade e a chave de linha.</span><span class="sxs-lookup"><span data-stu-id="c4aea-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="c4aea-338">Olá de chamadas de função Olá adicionar entidade [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet no Olá [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) classe toocreate um objeto de entidade.</span><span class="sxs-lookup"><span data-stu-id="c4aea-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="c4aea-339">Posteriormente, o exemplo de Olá chama Olá [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) método neste tooadd de objeto de entidade tooa tabela.</span><span class="sxs-lookup"><span data-stu-id="c4aea-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="c4aea-340">Como tooquery tabela entidades</span><span class="sxs-lookup"><span data-stu-id="c4aea-340">How tooquery table entities</span></span>
<span data-ttu-id="c4aea-341">tooquery uma tabela, utilize Olá [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="c4aea-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="c4aea-342">Olá seguinte exemplo assume que já tiver executado script Olá indicada na Olá como secção de entidades tooadd deste guia.</span><span class="sxs-lookup"><span data-stu-id="c4aea-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="c4aea-343">exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento utilizando o contexto de armazenamento de Olá, que inclui o nome de conta do storage Olá e a sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="c4aea-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="c4aea-344">Em seguida, este tenta tooretrieve Olá criado anteriormente "funcionários" tabela, utilizando Olá [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="c4aea-345">Chamar Olá [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet no Olá Microsoft.WindowsAzure.Storage.Table.TableQuery classe cria um novo objeto de consulta.</span><span class="sxs-lookup"><span data-stu-id="c4aea-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="c4aea-346">exemplo de Olá procura entidades Olá que têm uma coluna de 'ID' cujo valor é 1 conforme especificado num filtro de cadeia.</span><span class="sxs-lookup"><span data-stu-id="c4aea-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="c4aea-347">Para obter informações detalhadas, consulte [consultar tabelas e entidades](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="c4aea-348">Quando executar esta consulta, devolve todas as entidades que correspondem aos critérios de filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="c4aea-349">Como toodelete tabela entidades</span><span class="sxs-lookup"><span data-stu-id="c4aea-349">How toodelete table entities</span></span>
<span data-ttu-id="c4aea-350">Pode eliminar uma entidade com as chaves de partição e linha.</span><span class="sxs-lookup"><span data-stu-id="c4aea-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="c4aea-351">Olá seguinte exemplo assume que já tiver executado script Olá indicada na Olá como secção de entidades tooadd deste guia.</span><span class="sxs-lookup"><span data-stu-id="c4aea-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="c4aea-352">exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento utilizando o contexto de armazenamento de Olá, que inclui o nome de conta do storage Olá e a sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="c4aea-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="c4aea-353">Em seguida, este tenta tooretrieve Olá criado anteriormente "funcionários" tabela, utilizando Olá [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="c4aea-354">Se existir a tabela de Olá, o exemplo de Olá chama Olá [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve método uma entidade com base nos seus valores de chave de partição e da fila.</span><span class="sxs-lookup"><span data-stu-id="c4aea-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="c4aea-355">Em seguida, passe Olá entidade toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete de método.</span><span class="sxs-lookup"><span data-stu-id="c4aea-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="c4aea-356">Como toomanage Azure filas e mensagens de fila de espera</span><span class="sxs-lookup"><span data-stu-id="c4aea-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="c4aea-357">Armazenamento de filas do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acedidas de qualquer local no mundo Olá através de chamadas autenticadas com HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c4aea-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="c4aea-358">Esta secção assume que já estiver familiarizado com conceitos do serviço de armazenamento de filas do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="c4aea-359">Para obter informações detalhadas, consulte [introdução ao armazenamento de filas do Azure através do .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="c4aea-360">Esta secção irá mostrar como toomanage armazenamento de filas do Azure service com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="c4aea-361">Olá os cenários abrangidos incluem **a inserir** e **eliminar** fila de mensagens, bem como **criar**, **eliminar**e **obter filas**.</span><span class="sxs-lookup"><span data-stu-id="c4aea-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="c4aea-362">Como toocreate uma fila</span><span class="sxs-lookup"><span data-stu-id="c4aea-362">How toocreate a queue</span></span>
<span data-ttu-id="c4aea-363">Olá exemplo seguinte primeiro estabelece uma ligação tooAzure armazenamento Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso a utilizar.</span><span class="sxs-lookup"><span data-stu-id="c4aea-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="c4aea-364">Em seguida, chama [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate uma fila com o nome 'queuename'.</span><span class="sxs-lookup"><span data-stu-id="c4aea-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="c4aea-365">Para informações sobre as convenções de nomenclatura para o serviço de fila do Azure, consulte [nomenclatura de filas e metadados](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="c4aea-366">Como tooretrieve uma fila</span><span class="sxs-lookup"><span data-stu-id="c4aea-366">How tooretrieve a queue</span></span>
<span data-ttu-id="c4aea-367">Pode consultar e obter uma fila específica ou uma lista de todas as filas de Olá numa conta do Storage.</span><span class="sxs-lookup"><span data-stu-id="c4aea-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="c4aea-368">Olá exemplo seguinte demonstra como tooretrieve uma fila especificada utilizando Olá [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="c4aea-369">Se chamar Olá [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet sem quaisquer parâmetros, obtém uma lista de todas as filas de Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="c4aea-370">Como toodelete uma fila</span><span class="sxs-lookup"><span data-stu-id="c4aea-370">How toodelete a queue</span></span>
<span data-ttu-id="c4aea-371">toodelete uma fila e todas as mensagens de Olá nela contidas, chamada Olá remover AzureStorageQueue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="c4aea-372">Olá seguinte exemplo mostra como toodelete uma fila especificada utilizando Olá cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="c4aea-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="c4aea-373">Como tooinsert uma mensagem para uma fila</span><span class="sxs-lookup"><span data-stu-id="c4aea-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="c4aea-374">em primeiro lugar, tooinsert uma mensagem numa fila existente, crie uma nova instância do Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="c4aea-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="c4aea-375">Em seguida, chame Olá [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="c4aea-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="c4aea-376">Um CloudQueueMessage pode ser criado a partir de uma cadeia (no formato UTF-8) ou uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="c4aea-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="c4aea-377">Olá seguinte o exemplo demonstra como tooadd mensagem tooa fila.</span><span class="sxs-lookup"><span data-stu-id="c4aea-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="c4aea-378">exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso a utilizar.</span><span class="sxs-lookup"><span data-stu-id="c4aea-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="c4aea-379">Em seguida, obtém fila especificada Olá utilizando Olá [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c4aea-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="c4aea-380">Se a fila de Olá, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet é utilizado toocreate uma instância de Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="c4aea-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="c4aea-381">Posteriormente, o exemplo de Olá chama Olá [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método neste tooadd de objeto de mensagem tooa fila.</span><span class="sxs-lookup"><span data-stu-id="c4aea-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="c4aea-382">Eis o código que obtém uma fila e insere a mensagem de saudação 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="c4aea-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="c4aea-383">Como a fila toode em Olá junto da mensagem</span><span class="sxs-lookup"><span data-stu-id="c4aea-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="c4aea-384">O código remove uma mensagem da fila em dois passos.</span><span class="sxs-lookup"><span data-stu-id="c4aea-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="c4aea-385">Quando chamar Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) método, obterá Olá a seguinte mensagem numa fila.</span><span class="sxs-lookup"><span data-stu-id="c4aea-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="c4aea-386">Uma mensagem devolvida por **GetMessage** torna-se invisível tooany outro código de leitura de mensagens desta fila.</span><span class="sxs-lookup"><span data-stu-id="c4aea-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="c4aea-387">toofinish remover mensagem de saudação da fila de Olá, também tem de chamar Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="c4aea-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="c4aea-388">Este processo de dois passos da remoção de uma mensagem garante que se o código de falha tooprocess que pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="c4aea-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="c4aea-389">As chamadas de código **DeleteMessage** imediatamente após a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="c4aea-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="c4aea-390">Como toomanage ficheiros do Azure partilhas e ficheiros</span><span class="sxs-lookup"><span data-stu-id="c4aea-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="c4aea-391">File storage do Azure oferece um armazenamento partilhado para aplicações utilizando o protocolo SMB padrão do Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="c4aea-392">Máquinas virtuais do Microsoft Azure e serviços em nuvem podem partilhar os dados de ficheiros em componentes da aplicação através de partilhas montadas e as aplicações no local podem aceder a dados de ficheiros numa partilha através da API de armazenamento de ficheiros de Olá ou do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="c4aea-393">Para obter mais informações sobre o File storage do Azure, consulte [introdução ao File storage do Azure no Windows](storage-dotnet-how-to-use-files.md) e [API de REST do serviço de ficheiro](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4aea-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="c4aea-394">Como tooset e a consulta de análise de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c4aea-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="c4aea-395">Pode utilizar [análise de armazenamento do Azure](storage-analytics.md) toocollect métricas para as suas contas do storage do Azure e dados de registo sobre pedidos enviados tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-395">You can use [Azure Storage Analytics](storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="c4aea-396">Pode utilizar o armazenamento métricas toomonitor Olá estado de funcionamento de uma conta de armazenamento e armazenamento registo toodiagnose e resolver problemas com a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="c4aea-397">Pode configurar a monitorização utilizando Olá portal do Azure ou o Windows PowerShell ou através de programação utilizando a biblioteca de clientes do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="c4aea-398">Registo de armazenamento acontece do lado do servidor e permite-lhe detalhes toorecord para pedidos com êxito ou falhados na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4aea-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="c4aea-399">Estes registos permitem-lhe toosee detalhes de leitura, escrita e eliminação operações contra as tabelas, filas e blobs, bem como Olá algumas das razões para pedidos falhados.</span><span class="sxs-lookup"><span data-stu-id="c4aea-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="c4aea-400">toolearn como tooenable e ver as métricas do Storage de dados com o PowerShell, consulte [como tooenable as métricas do Storage através do PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="c4aea-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="c4aea-401">toolearn como tooenable e obter registos de armazenamento de dados com o PowerShell, consulte [como tooenable armazenamento registo com o PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) e [localizar os dados de registo registo armazenamento](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="c4aea-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="c4aea-402">Para obter informações detalhadas sobre como utilizar as métricas do Storage e armazenamento registo tootroubleshoot problemas de armazenamento, consulte [monitorização, Diagnosing e resolução de problemas de armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="c4aea-403">Como toomanage partilhado (SAS) de assinatura de acesso e política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="c4aea-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="c4aea-404">Assinaturas de acesso partilhado são uma parte importante do modelo de segurança de Olá para qualquer aplicação utilizando o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="c4aea-405">Estes são úteis para fornecer permissões limitadas tooyour armazenamento conta tooclients que não devem ter a chave de conta Olá.</span><span class="sxs-lookup"><span data-stu-id="c4aea-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="c4aea-406">Por predefinição, só o proprietário Olá Olá de conta do storage pode aceder a blobs, tabelas e filas dentro dessa conta.</span><span class="sxs-lookup"><span data-stu-id="c4aea-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="c4aea-407">Se a sua aplicação ou serviço necessitar da toomake estes clientes de tooother disponíveis recursos sem partilha a sua chave de acesso, tem três opções:</span><span class="sxs-lookup"><span data-stu-id="c4aea-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="c4aea-408">Defina toopermit acesso de leitura anónimo toohello contentor para um contentor permissões e os respetivos blobs.</span><span class="sxs-lookup"><span data-stu-id="c4aea-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="c4aea-409">Não é permitida para tabelas ou filas.</span><span class="sxs-lookup"><span data-stu-id="c4aea-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="c4aea-410">Utilize uma assinatura de acesso partilhado que concede acesso restrito direitos toocontainers, blobs, filas e tabelas para um intervalo de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="c4aea-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="c4aea-411">Utilize um tooobtain de política de acesso armazenado um nível adicional de controlo sobre assinaturas de acesso partilhado para um contentor ou os respetivos blobs, para uma fila ou para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c4aea-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="c4aea-412">Olá política de acesso armazenada permite-lhe a hora de início toochange Olá, hora de expiração ou permissões para uma assinatura ou toorevoke-lo Depois foi emitido.</span><span class="sxs-lookup"><span data-stu-id="c4aea-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="c4aea-413">Pode ser uma assinatura de acesso partilhado de uma das duas formas:</span><span class="sxs-lookup"><span data-stu-id="c4aea-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="c4aea-414">**SAS ad hoc**: Quando cria um SAS ad hoc, a hora de início de Olá, a hora de expiração e as permissões para Olá SAS são especificadas no Olá URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="c4aea-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="c4aea-415">Este tipo de SAS que pode ser criado num contentor de blob, tabela ou fila que é não revocable.</span><span class="sxs-lookup"><span data-stu-id="c4aea-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="c4aea-416">**SAS com a política de acesso armazenada**: uma política de acesso armazenada está definida um contentor de recursos um contentor de blob, tabela ou fila - e pode utilizá-lo toomanage restrições para um ou mais assinaturas de acesso partilhado.</span><span class="sxs-lookup"><span data-stu-id="c4aea-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="c4aea-417">Quando associa um SAS com uma política de acesso armazenada, Olá SAS herda as restrições de Olá - Olá iniciar tempo, hora de expiração e permissões - definidas para a política de acesso de Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="c4aea-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="c4aea-418">Este tipo de SAS é revocable.</span><span class="sxs-lookup"><span data-stu-id="c4aea-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="c4aea-419">Para obter mais informações, consulte [através de acesso partilhado assinaturas (SAS)](storage-dotnet-shared-access-signature-part-1.md) e [gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="c4aea-420">Olá secções seguintes, irá aprender como toocreate uma política de acesso de token e armazenadas de assinatura de acesso partilhado para as tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="c4aea-421">O Azure PowerShell fornece cmdlets semelhantes para contentores, blobs e filas bem.</span><span class="sxs-lookup"><span data-stu-id="c4aea-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="c4aea-422">scripts de Olá toorun nesta secção, transferir Olá [Azure PowerShell versão 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c4aea-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="c4aea-423">Como toocreate uma política com base no token de assinatura de acesso partilhado</span><span class="sxs-lookup"><span data-stu-id="c4aea-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="c4aea-424">Utilize Olá AzureStorageTableStoredAccessPolicy novo cmdlet toocreate uma nova política de acesso armazenada.</span><span class="sxs-lookup"><span data-stu-id="c4aea-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="c4aea-425">Em seguida, chame Olá [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate um novo token de assinatura de baseado em política de acesso partilhado para uma tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4aea-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="c4aea-426">Como toocreate um token de assinatura de acesso partilhado (não revocable) ad hoc</span><span class="sxs-lookup"><span data-stu-id="c4aea-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="c4aea-427">Olá utilize [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate um novo ad hoc (não revocable) assinatura de acesso partilhado token para uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="c4aea-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="c4aea-428">Como toocreate uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="c4aea-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="c4aea-429">Utilize Olá AzureStorageTableStoredAccessPolicy novo cmdlet toocreate uma nova política de acesso armazenados para uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="c4aea-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="c4aea-430">Como tooupdate uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="c4aea-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="c4aea-431">Utilize Olá conjunto AzureStorageTableStoredAccessPolicy cmdlet tooupdate uma política de acesso armazenada existente para uma tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="c4aea-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="c4aea-432">Como toodelete uma política de acesso armazenada</span><span class="sxs-lookup"><span data-stu-id="c4aea-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="c4aea-433">Utilize Olá remover AzureStorageTableStoredAccessPolicy cmdlet toodelete uma política de acesso armazenados numa tabela de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="c4aea-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="c4aea-434">Como toouse Storage do Azure dos EUA e o Azure China</span><span class="sxs-lookup"><span data-stu-id="c4aea-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="c4aea-435">Um ambiente do Azure é uma implementação independentemente do Microsoft Azure, tal como [Azure Government para EUA](https://azure.microsoft.com/features/gov/), [AzureCloud para o global Azure](https://portal.azure.com), e [AzureChinaCloud para o Azure operado pela 21Vianet na China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="c4aea-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="c4aea-436">Pode implementar novos ambientes do Azure para U.S government e o Azure China.</span><span class="sxs-lookup"><span data-stu-id="c4aea-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="c4aea-437">Storage do Azure com AzureChinaCloud toouse, terá de toocreate um contexto de armazenamento que estão associado com AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="c4aea-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="c4aea-438">Siga estes tooget passos tiver iniciado:</span><span class="sxs-lookup"><span data-stu-id="c4aea-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="c4aea-439">Executar Olá [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee Olá ambientes do Azure disponíveis:</span><span class="sxs-lookup"><span data-stu-id="c4aea-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="c4aea-440">Adicione um tooWindows de conta do Azure China do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c4aea-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="c4aea-441">Crie um contexto de armazenamento para uma conta de AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="c4aea-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="c4aea-442">toouse Storage do Azure com [E.U.A. Azure Government](https://azure.microsoft.com/features/gov/), deve definir um novo ambiente e, em seguida, criar um contexto de armazenamento novo com este ambiente:</span><span class="sxs-lookup"><span data-stu-id="c4aea-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="c4aea-443">Executar Olá [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee Olá ambientes do Azure disponíveis:</span><span class="sxs-lookup"><span data-stu-id="c4aea-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="c4aea-444">Adicione um tooWindows de conta do Azure US Government do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c4aea-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="c4aea-445">Crie um contexto de armazenamento para uma conta de AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="c4aea-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="c4aea-446">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="c4aea-446">For more information, see:</span></span>

* <span data-ttu-id="c4aea-447">[Guia para programadores do Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c4aea-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="c4aea-448">Descrição geral das diferenças quando criar uma aplicação no serviço China</span><span class="sxs-lookup"><span data-stu-id="c4aea-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="c4aea-449">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="c4aea-449">Next Steps</span></span>
<span data-ttu-id="c4aea-450">Neste guia, aprendeu como toomanage Storage do Azure com o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4aea-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="c4aea-451">Aqui estão alguns artigos relacionados e recursos para aprender mais sobre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="c4aea-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="c4aea-452">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="c4aea-453">Cmdlets do PowerShell do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="c4aea-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="c4aea-454">Referência do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4aea-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
