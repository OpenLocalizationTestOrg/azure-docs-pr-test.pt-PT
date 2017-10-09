---
title: "Ferramentas do Azure do Data Lake: Execução local do U-SQL e depuração local com o Visual Studio Code | Microsoft Docs"
description: Saiba como depurar toouse do Azure Data Lake Tools para Visual Studio Code toolocal executada e local.
Keywords: "VScode, ferramentas do Azure Data Lake, execução, ficheiros de armazenamento de pré-visualização de depuração Local, depurar Local, Local carregar toostorage caminho"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="61013-104">Execução local do U-SQL e de depuração local com o Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="61013-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61013-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="61013-105">Prerequisites</span></span>
<span data-ttu-id="61013-106">Certifique-se de que tem Olá os seguintes pré-requisitos antes de iniciar estes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="61013-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="61013-107">Ferramenta de Lake de dados do Azure para Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="61013-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="61013-108">Para obter instruções, consulte [utilização do Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="61013-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="61013-109">C# para Visual Studio Code (se pretender depuração local tooperform U-SQL).</span><span class="sxs-lookup"><span data-stu-id="61013-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![Instalar c# nas ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="61013-111">Olá execução local do U-SQL e funcionalidades de depuração atualmente suportam apenas utilizadores do Windows.</span><span class="sxs-lookup"><span data-stu-id="61013-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="61013-112">Configurar o ambiente de execução local Olá U-SQL</span><span class="sxs-lookup"><span data-stu-id="61013-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="61013-113">Selecione a paleta de comando Ctrl + Shift + P tooopen Olá e, em seguida, introduza **ADL: Transferir o LocalRun dependência** pacotes de Olá toodownload.</span><span class="sxs-lookup"><span data-stu-id="61013-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Transferir pacotes de dependência de LocalRun ADL Olá](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="61013-115">Localizar Olá dependência de pacotes do caminho de Olá mostrado na Olá **saída** painel e, em seguida, instalar BuildTools e Win10SDK 10240.</span><span class="sxs-lookup"><span data-stu-id="61013-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="61013-116">Eis um caminho de exemplo:</span><span class="sxs-lookup"><span data-stu-id="61013-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="61013-117">![Localize os pacotes de dependência de Olá](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="61013-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="61013-118">a.</span><span class="sxs-lookup"><span data-stu-id="61013-118">a.</span></span> <span data-ttu-id="61013-119">tooinstall BuildTools, siga as instruções do Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="61013-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![Instalar BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="61013-121">b.</span><span class="sxs-lookup"><span data-stu-id="61013-121">b.</span></span> <span data-ttu-id="61013-122">tooinstall Win10SDK 10240, siga as instruções do Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="61013-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Instalar Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="61013-124">Configure a variável de ambiente de Olá.</span><span class="sxs-lookup"><span data-stu-id="61013-124">Set up hello environment variable.</span></span> <span data-ttu-id="61013-125">Conjunto Olá **SCOPE_CPP_SDK** variável de ambiente para:</span><span class="sxs-lookup"><span data-stu-id="61013-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="61013-126">Reinicie Olá SO toomake certificar-se de que as definições de variáveis de ambiente de Olá entram em vigor.</span><span class="sxs-lookup"><span data-stu-id="61013-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Certifique-se a variável de ambiente de SCOPE_CPP_SDK Olá está instalado](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="61013-128">Iniciar o serviço de execução local Olá e submeter conta local do Olá U-SQL tarefa tooa</span><span class="sxs-lookup"><span data-stu-id="61013-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="61013-129">Para o utilizador do primeiro tempo Olá, é Olá toodownload pedido ADL: dependência de LocalRun transferir pacotes se não estiver já instalados.</span><span class="sxs-lookup"><span data-stu-id="61013-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="61013-130">Selecione a paleta de comando Ctrl + Shift + P tooopen Olá e, em seguida, introduza **ADL: iniciar o serviço de execução Local**.</span><span class="sxs-lookup"><span data-stu-id="61013-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="61013-131">Selecione **aceitar** tooaccept Olá termos de licenciamento de Software Microsoft para Olá pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="61013-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Aceitar os termos de licenciamento de Software do Olá Microsoft](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="61013-133">Abre a consola do Olá cmd.</span><span class="sxs-lookup"><span data-stu-id="61013-133">hello cmd console opens.</span></span> <span data-ttu-id="61013-134">Para os utilizadores da primeira vez, terá de tooenter **3**e, em seguida, localize o caminho de pasta local Olá para os seus dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="61013-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="61013-135">Para outras opções, pode utilizar os valores predefinidos de Olá.</span><span class="sxs-lookup"><span data-stu-id="61013-135">For other options, you can use hello default values.</span></span> 

   ![Ferramentas do Data Lake para Visual Studio Code cmd de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="61013-137">Selecione a paleta de comando Ctrl + Shift + P tooopen Olá, introduza **ADL: Submeter tarefa**e, em seguida, selecione **Local** conta local do toosubmit Olá tarefa tooyour.</span><span class="sxs-lookup"><span data-stu-id="61013-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Ferramentas do Data Lake para Visual Studio Code selecione local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="61013-139">Depois de submeter a tarefa de Olá, pode ver os detalhes de submissão de Olá.</span><span class="sxs-lookup"><span data-stu-id="61013-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="61013-140">Selecione os detalhes de submissão de Olá tooview **jobUrl** no Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="61013-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="61013-141">Também pode ver o estado da submissão Olá tarefa da consola do Olá cmd.</span><span class="sxs-lookup"><span data-stu-id="61013-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="61013-142">Introduza **7** na consola de cmd Olá se quiser tooknow mais detalhes da tarefa.</span><span class="sxs-lookup"><span data-stu-id="61013-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="61013-143">![Data Lake Tools para execução a saída de local de Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![ferramentas do Data Lake para locais de Visual Studio Code executar cmd Estado](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="61013-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="61013-144">Iniciar uma depuração local para a tarefa de U-SQL Olá</span><span class="sxs-lookup"><span data-stu-id="61013-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="61013-145">Para o utilizador do primeiro tempo Olá, é Olá toodownload pedido ADL: dependência de LocalRun transferir pacotes se não estiver já instalados.</span><span class="sxs-lookup"><span data-stu-id="61013-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="61013-146">Selecione a paleta de comando Ctrl + Shift + P tooopen Olá e, em seguida, introduza **ADL: iniciar o serviço de execução Local**.</span><span class="sxs-lookup"><span data-stu-id="61013-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="61013-147">Abre a consola do Olá cmd.</span><span class="sxs-lookup"><span data-stu-id="61013-147">hello cmd console opens.</span></span> <span data-ttu-id="61013-148">Certifique-se de que Olá **DataRoot** está definido.</span><span class="sxs-lookup"><span data-stu-id="61013-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="61013-149">Defina um ponto de interrupção no seu c# code-behind.</span><span class="sxs-lookup"><span data-stu-id="61013-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="61013-150">No editor de scripts Olá, selecione a consola de comandos do Ctrl + Shift + P tooopen Olá e, em seguida, introduza **depurar Local** toostart o serviço de depuração local.</span><span class="sxs-lookup"><span data-stu-id="61013-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Ferramentas do Data Lake para resultados de local de depuração do Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="61013-152">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="61013-152">Next steps</span></span>
- <span data-ttu-id="61013-153">Para utilizar as ferramentas do Azure Data Lake para Visual Studio Code, consulte [utilização do Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="61013-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="61013-154">Para obter informações de introdução no Data Lake Analytics, consulte [Tutorial: introdução ao Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61013-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="61013-155">Para informações sobre as ferramentas do Data Lake para Visual Studio, consulte [Tutorial: desenvolver scripts SQL-U, utilizando ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="61013-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="61013-156">Para informações de Olá sobre o desenvolvimento das assemblagens, consulte [assemblagens de desenvolver U-SQL para tarefas do Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="61013-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
