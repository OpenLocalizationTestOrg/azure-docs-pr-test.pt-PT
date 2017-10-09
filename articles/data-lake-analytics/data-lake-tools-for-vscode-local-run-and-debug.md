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
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>Execução local do U-SQL e de depuração local com o Visual Studio Code

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que tem Olá os seguintes pré-requisitos antes de iniciar estes procedimentos:
- Ferramenta de Lake de dados do Azure para Visual Studio Code. Para obter instruções, consulte [utilização do Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- C# para Visual Studio Code (se pretender depuração local tooperform U-SQL).

   ![Instalar c# nas ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > Olá execução local do U-SQL e funcionalidades de depuração atualmente suportam apenas utilizadores do Windows. 


## <a name="set-up-hello-u-sql-local-run-environment"></a>Configurar o ambiente de execução local Olá U-SQL

1. Selecione a paleta de comando Ctrl + Shift + P tooopen Olá e, em seguida, introduza **ADL: Transferir o LocalRun dependência** pacotes de Olá toodownload.  

   ![Transferir pacotes de dependência de LocalRun ADL Olá](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. Localizar Olá dependência de pacotes do caminho de Olá mostrado na Olá **saída** painel e, em seguida, instalar BuildTools e Win10SDK 10240. Eis um caminho de exemplo:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![Localize os pacotes de dependência de Olá](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools, siga as instruções do Assistente de Olá.   

  ![Instalar BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240, siga as instruções do Assistente de Olá.  

  ![Instalar Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. Configure a variável de ambiente de Olá. Conjunto Olá **SCOPE_CPP_SDK** variável de ambiente para:  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. Reinicie Olá SO toomake certificar-se de que as definições de variáveis de ambiente de Olá entram em vigor.  

   ![Certifique-se a variável de ambiente de SCOPE_CPP_SDK Olá está instalado](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>Iniciar o serviço de execução local Olá e submeter conta local do Olá U-SQL tarefa tooa 
Para o utilizador do primeiro tempo Olá, é Olá toodownload pedido ADL: dependência de LocalRun transferir pacotes se não estiver já instalados.
1. Selecione a paleta de comando Ctrl + Shift + P tooopen Olá e, em seguida, introduza **ADL: iniciar o serviço de execução Local**.
2. Selecione **aceitar** tooaccept Olá termos de licenciamento de Software Microsoft para Olá pela primeira vez. 

   ![Aceitar os termos de licenciamento de Software do Olá Microsoft](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. Abre a consola do Olá cmd. Para os utilizadores da primeira vez, terá de tooenter **3**e, em seguida, localize o caminho de pasta local Olá para os seus dados de entrada e saída. Para outras opções, pode utilizar os valores predefinidos de Olá. 

   ![Ferramentas do Data Lake para Visual Studio Code cmd de execução local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. Selecione a paleta de comando Ctrl + Shift + P tooopen Olá, introduza **ADL: Submeter tarefa**e, em seguida, selecione **Local** conta local do toosubmit Olá tarefa tooyour.

   ![Ferramentas do Data Lake para Visual Studio Code selecione local](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. Depois de submeter a tarefa de Olá, pode ver os detalhes de submissão de Olá. Selecione os detalhes de submissão de Olá tooview **jobUrl** no Olá **saída** janela. Também pode ver o estado da submissão Olá tarefa da consola do Olá cmd. Introduza **7** na consola de cmd Olá se quiser tooknow mais detalhes da tarefa.

   ![Data Lake Tools para execução a saída de local de Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![ferramentas do Data Lake para locais de Visual Studio Code executar cmd Estado](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>Iniciar uma depuração local para a tarefa de U-SQL Olá  
Para o utilizador do primeiro tempo Olá, é Olá toodownload pedido ADL: dependência de LocalRun transferir pacotes se não estiver já instalados.
  
1. Selecione a paleta de comando Ctrl + Shift + P tooopen Olá e, em seguida, introduza **ADL: iniciar o serviço de execução Local**. Abre a consola do Olá cmd. Certifique-se de que Olá **DataRoot** está definido.
3. Defina um ponto de interrupção no seu c# code-behind.
4. No editor de scripts Olá, selecione a consola de comandos do Ctrl + Shift + P tooopen Olá e, em seguida, introduza **depurar Local** toostart o serviço de depuração local.

![Ferramentas do Data Lake para resultados de local de depuração do Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>Passos seguintes
- Para utilizar as ferramentas do Azure Data Lake para Visual Studio Code, consulte [utilização do Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).
- Para obter informações de introdução no Data Lake Analytics, consulte [Tutorial: introdução ao Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Para informações sobre as ferramentas do Data Lake para Visual Studio, consulte [Tutorial: desenvolver scripts SQL-U, utilizando ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Para informações de Olá sobre o desenvolvimento das assemblagens, consulte [assemblagens de desenvolver U-SQL para tarefas do Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).
