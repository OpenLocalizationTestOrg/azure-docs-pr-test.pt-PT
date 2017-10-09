---
title: "aaaUsing emulador Express toorun e depuração do Azure num computador local, o serviço em nuvem | Microsoft Docs"
description: "Utilizar o emulador Express toorun e depuração um serviço em nuvem num computador local"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="cf34e-103">Utilizar o emulador Express toorun e depuração um Azure serviço em nuvem num computador local</span><span class="sxs-lookup"><span data-stu-id="cf34e-103">Using Emulator Express toorun and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="cf34e-104">Ao utilizar o emulador Express, pode testar e depurar um serviço em nuvem sem executar o Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="cf34e-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="cf34e-105">Pode definir o seu toouse de definições do projeto ou emulador Express ou Olá emulador completo, dependendo dos requisitos de Olá do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cf34e-105">You can set your project settings toouse either Emulator Express or hello full emulator, depending on hello requirements of your cloud service.</span></span> <span data-ttu-id="cf34e-106">Para obter mais informações sobre o emulador completo Olá, consulte [executa uma aplicação do Azure no emulador de computação de Olá](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="cf34e-106">For more information about hello full emulator, see [Run an Azure Application in hello Compute Emulator](storage/common/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="cf34e-107">Utilizando o emulador rápida no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf34e-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="cf34e-108">Quando cria um projeto do Azure no Azure SDK 2.3 ou posterior, emulador Express é automaticamente utilizado.</span><span class="sxs-lookup"><span data-stu-id="cf34e-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="cf34e-109">Para os projetos existentes que foram criados com uma versão anterior do Olá SDK do Azure, utilize Olá tooselect passos emulador Express os seguintes:</span><span class="sxs-lookup"><span data-stu-id="cf34e-109">For existing projects that were created with an earlier version of hello Azure SDK, use hello following steps tooselect Emulator Express:</span></span>

1. <span data-ttu-id="cf34e-110">Criar ou abrir um projeto de serviço em nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf34e-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="cf34e-111">No **Explorador de soluções**, clique no projeto Olá e, no menu de contexto de Olá, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="cf34e-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>

1. <span data-ttu-id="cf34e-112">Nas páginas de propriedades de projetos de Olá, selecione Olá **Web** separador.</span><span class="sxs-lookup"><span data-stu-id="cf34e-112">In hello projects properties pages, select hello **Web** tab.</span></span>

    ![Propriedades de um projeto de serviço em nuvem do Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="cf34e-114">Em **servidor de desenvolvimento Local**, selecione **utilize IIS Express opção**.</span><span class="sxs-lookup"><span data-stu-id="cf34e-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="cf34e-115">Em **emulador**, selecione **utilizar emulador Express**.</span><span class="sxs-lookup"><span data-stu-id="cf34e-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="cf34e-116">toolaunch Olá emulador Express, execute Olá os seguintes comandos numa linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="cf34e-116">toolaunch hello Emulator Express, run hello following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="cf34e-117">Limitações do emulador rápida</span><span class="sxs-lookup"><span data-stu-id="cf34e-117">Emulator Express limitations</span></span>
<span data-ttu-id="cf34e-118">os seguintes problemas de Olá é conhecido limitações do emulador Express:</span><span class="sxs-lookup"><span data-stu-id="cf34e-118">hello following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="cf34e-119">Emulador Express não é compatível com o servidor Web do IIS.</span><span class="sxs-lookup"><span data-stu-id="cf34e-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="cf34e-120">O serviço em nuvem pode conter várias funções, mas cada função é limitado tooone instância.</span><span class="sxs-lookup"><span data-stu-id="cf34e-120">Your cloud service can contain multiple roles, but each role is limited tooone instance.</span></span>
- <span data-ttu-id="cf34e-121">Não é possível aceder a números de porta abaixo 1000.</span><span class="sxs-lookup"><span data-stu-id="cf34e-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="cf34e-122">Se utilizar um fornecedor de autenticação que normalmente utiliza uma porta abaixo 1000, poderá ser necessário toochange este número de porta de tooa valor é superior a 1000.</span><span class="sxs-lookup"><span data-stu-id="cf34e-122">If you use an authentication provider that normally uses a port below 1000, you might need toochange this value tooa port number that's above 1000.</span></span>
- <span data-ttu-id="cf34e-123">Quaisquer limitações que se aplicam toohello emulador de computação do Azure também se aplicam tooEmulator rápida.</span><span class="sxs-lookup"><span data-stu-id="cf34e-123">Any limitations that apply toohello Azure Compute Emulator also apply tooEmulator Express.</span></span> <span data-ttu-id="cf34e-124">Por exemplo, não pode ter mais de 50 instâncias de função por implementação.</span><span class="sxs-lookup"><span data-stu-id="cf34e-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="cf34e-125">Para obter mais informações sobre Olá emulador de computação do Azure, consulte [executa uma aplicação do Azure no emulador de computação de Olá](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="cf34e-125">For more information about hello Azure Compute Emulator, see [Run an Azure Application in hello Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf34e-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cf34e-126">Next steps</span></span>
[<span data-ttu-id="cf34e-127">Depuração cloud services do Azure</span><span class="sxs-lookup"><span data-stu-id="cf34e-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)
