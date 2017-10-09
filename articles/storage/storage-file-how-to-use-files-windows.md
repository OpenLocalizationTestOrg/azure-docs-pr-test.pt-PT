---
title: "partilham de aaaMount uma partilha de ficheiros do Azure e Olá de acesso no Windows | Microsoft Docs"
description: "Monte uma partilha de ficheiros do Azure e a partilha de Olá de acesso no Windows."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a><span data-ttu-id="efc39-103">Montar uma partilha de ficheiros do Azure e a partilha de Olá de acesso no Windows</span><span class="sxs-lookup"><span data-stu-id="efc39-103">Mount an Azure File share and access hello share in Windows</span></span>
<span data-ttu-id="efc39-104">[File storage do Azure](storage-dotnet-how-to-use-files.md) sistema de ficheiros de nuvem de fácil toouse da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="efc39-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="efc39-105">As partilhas de Ficheiros do Azure podem ser montadas no Windows e no Windows Server.</span><span class="sxs-lookup"><span data-stu-id="efc39-105">Azure File shares can be mounted in Windows and Windows Server.</span></span> <span data-ttu-id="efc39-106">Este artigo mostra três formas diferentes toomount uma partilha de ficheiros do Azure no Windows: com Olá IU do Explorador de ficheiros, através do PowerShell e através de Olá linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="efc39-106">This article shows three different ways toomount an Azure File share on Windows: with hello File Explorer UI, via PowerShell, and via hello Command Prompt.</span></span> 

<span data-ttu-id="efc39-107">Na ordem toomount um Azure de partilha de ficheiros fora Olá região do Azure está alojado no, tal como no local ou numa região diferente do Azure, Olá SO tem de suportar SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="efc39-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support SMB 3.0.</span></span> 

<span data-ttu-id="efc39-108">A partilha de Ficheiros do Azure pode ser montada num computador Windows no local ou numa VM do Azure, dependendo da versão do SO.</span><span class="sxs-lookup"><span data-stu-id="efc39-108">Azure File share can be mounted on Windows machine either on-premises or in Azure VM depending on OS version.</span></span> <span data-ttu-id="efc39-109">Tabela abaixo ilustra Olá</span><span class="sxs-lookup"><span data-stu-id="efc39-109">Below table illustrates hello</span></span> 

| <span data-ttu-id="efc39-110">Versão do Windows</span><span class="sxs-lookup"><span data-stu-id="efc39-110">Windows Version</span></span>        | <span data-ttu-id="efc39-111">Versão do SMB</span><span class="sxs-lookup"><span data-stu-id="efc39-111">SMB Version</span></span> |<span data-ttu-id="efc39-112">Montável em VM do Azure</span><span class="sxs-lookup"><span data-stu-id="efc39-112">Mountable On Azure VM</span></span>|<span data-ttu-id="efc39-113">Montável no Local</span><span class="sxs-lookup"><span data-stu-id="efc39-113">Mountable On-Premise</span></span>|
|------------------------|-------------|---------------------|---------------------|
| <span data-ttu-id="efc39-114">Windows 7</span><span class="sxs-lookup"><span data-stu-id="efc39-114">Windows 7</span></span>              | <span data-ttu-id="efc39-115">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="efc39-115">SMB 2.1</span></span>     | <span data-ttu-id="efc39-116">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-116">Yes</span></span>                 | <span data-ttu-id="efc39-117">Não</span><span class="sxs-lookup"><span data-stu-id="efc39-117">No</span></span>                  |
| <span data-ttu-id="efc39-118">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="efc39-118">Windows Server 2008 R2</span></span> | <span data-ttu-id="efc39-119">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="efc39-119">SMB 2.1</span></span>     | <span data-ttu-id="efc39-120">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-120">Yes</span></span>                 | <span data-ttu-id="efc39-121">Não</span><span class="sxs-lookup"><span data-stu-id="efc39-121">No</span></span>                  |
| <span data-ttu-id="efc39-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="efc39-122">Windows 8</span></span>              | <span data-ttu-id="efc39-123">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="efc39-123">SMB 3.0</span></span>     | <span data-ttu-id="efc39-124">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-124">Yes</span></span>                 | <span data-ttu-id="efc39-125">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-125">Yes</span></span>                 |
| <span data-ttu-id="efc39-126">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="efc39-126">Windows Server 2012</span></span>    | <span data-ttu-id="efc39-127">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="efc39-127">SMB 3.0</span></span>     | <span data-ttu-id="efc39-128">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-128">Yes</span></span>                 | <span data-ttu-id="efc39-129">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-129">Yes</span></span>                 |
| <span data-ttu-id="efc39-130">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="efc39-130">Windows Server 2012 R2</span></span> | <span data-ttu-id="efc39-131">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="efc39-131">SMB 3.0</span></span>     | <span data-ttu-id="efc39-132">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-132">Yes</span></span>                 | <span data-ttu-id="efc39-133">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-133">Yes</span></span>                 |
| <span data-ttu-id="efc39-134">Windows 10</span><span class="sxs-lookup"><span data-stu-id="efc39-134">Windows 10</span></span>             | <span data-ttu-id="efc39-135">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="efc39-135">SMB 3.0</span></span>     | <span data-ttu-id="efc39-136">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-136">Yes</span></span>                 | <span data-ttu-id="efc39-137">Sim</span><span class="sxs-lookup"><span data-stu-id="efc39-137">Yes</span></span>                 |

> [!Note]  
> <span data-ttu-id="efc39-138">Recomendamos sempre tendo hello mais recente KB para a sua versão do Windows.</span><span class="sxs-lookup"><span data-stu-id="efc39-138">We always recommend taking hello most recent KB for your version of Windows.</span></span>

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a><span data-ttu-id="efc39-139"></a>Pré-requisitos para Montar a Partilha de Ficheiros do Azure com o Windows</span><span class="sxs-lookup"><span data-stu-id="efc39-139"></a>Prerequisites for Mounting Azure File Share with Windows</span></span> 
* <span data-ttu-id="efc39-140">**Nome da conta de armazenamento**: toomount partilha de um ficheiro do Azure, será necessário Olá nome Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="efc39-140">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="efc39-141">**Chave de conta de armazenamento**: a partilha de um ficheiro de Azure toomount, será necessário Olá chave de armazenamento () principais ou secundários.</span><span class="sxs-lookup"><span data-stu-id="efc39-141">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="efc39-142">Atualmente, não são suportadas chaves SAS para a montagem.</span><span class="sxs-lookup"><span data-stu-id="efc39-142">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="efc39-143">**Confirme que a porta 445 está aberta**: o armazenamento de Ficheiros do Azure utiliza o protocolo SMB.</span><span class="sxs-lookup"><span data-stu-id="efc39-143">**Ensure port 445 is open**: Azure File storage uses SMB protocol.</span></span> <span data-ttu-id="efc39-144">SMB comunica através da porta TCP 445 - Verifique o toosee se a firewall não está a bloquear as portas TCP 445 do computador cliente.</span><span class="sxs-lookup"><span data-stu-id="efc39-144">SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-with-file-explorer"></a><span data-ttu-id="efc39-145">Montar a partilha de ficheiros do Azure Olá com o Explorador de ficheiros</span><span class="sxs-lookup"><span data-stu-id="efc39-145">Mount hello Azure File share with File Explorer</span></span>
> [!Note]  
> <span data-ttu-id="efc39-146">Tenha em atenção que Olá instruções a seguir são apresentadas no Windows 10 e poderão ser algo diferentes em versões mais antigas.</span><span class="sxs-lookup"><span data-stu-id="efc39-146">Note that hello following instructions are shown on Windows 10 and may differ slightly on older releases.</span></span> 

1. <span data-ttu-id="efc39-147">**Abra o Explorador de ficheiros**: Isto pode ser feito através da abertura de Olá Menu Iniciar ou premindo atalho Win + I.</span><span class="sxs-lookup"><span data-stu-id="efc39-147">**Open File Explorer**: This can be done by opening from hello Start Menu, or by pressing Win+E shortcut.</span></span>

2. <span data-ttu-id="efc39-148">**Navegue até o item de "Este PC" toohello no lado esquerdo Olá da janela de Olá. Isto vai alterar menus Olá disponíveis no Friso de Olá. No menu de computador Olá, selecione "Unidade de rede de mapa"**.</span><span class="sxs-lookup"><span data-stu-id="efc39-148">**Navigate toohello "This PC" item on hello left-hand side of hello window. This will change hello menus available in hello ribbon. Under hello Computer menu, select "Map Network Drive"**.</span></span>
    
    ![Uma captura de ecrã de Olá "Unidade de rede de mapa" menu pendente](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. <span data-ttu-id="efc39-150">**Caminho UNC Olá cópia a partir do painel de "Ligar" Olá no portal do Azure de Olá**: uma descrição detalhada do como toofind estas informações podem ser encontradas [aqui](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span><span class="sxs-lookup"><span data-stu-id="efc39-150">**Copy hello UNC path from hello "Connect" pane in hello Azure portal**: A detailed description of how toofind this information can be found [here](storage-file-how-to-use-files-portal.md#connect-to-file-share).</span></span>

    ![caminho UNC Olá a partir do painel de ligação de armazenamento de ficheiros do Azure Olá](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. <span data-ttu-id="efc39-152">**Selecione a letra de unidade de Olá e introduza o caminho UNC Olá.**</span><span class="sxs-lookup"><span data-stu-id="efc39-152">**Select hello Drive letter and enter hello UNC path.**</span></span> 
    
    ![Uma captura de ecrã da caixa de diálogo de "Unidade de rede de mapa" Olá](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. <span data-ttu-id="efc39-154">**Olá utilize prepended com o nome da conta de armazenamento `Azure\` como Olá nome de utilizador e uma chave de conta de armazenamento como palavra-passe de Olá.**</span><span class="sxs-lookup"><span data-stu-id="efc39-154">**Use hello Storage Account Name prepended with `Azure\` as hello username and a Storage Account Key as hello password.**</span></span>
    
    ![Uma captura de ecrã da caixa de diálogo de credenciais de rede Olá](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. <span data-ttu-id="efc39-156">**Utilize a patilha de Ficheiros do Azure como pretendido**.</span><span class="sxs-lookup"><span data-stu-id="efc39-156">**Use Azure File share as desired**.</span></span>
    
    ![A partilha de Ficheiros do Azure está agora montada](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. <span data-ttu-id="efc39-158">**Quando está pronto toodismount (a ou desligar) partilha de ficheiros do Azure Olá, pode fazer com o botão direito clicando na entrada de Olá para partilha de Olá Olá "localizações de rede" no Explorador de ficheiros e selecionando "Desligar"**.</span><span class="sxs-lookup"><span data-stu-id="efc39-158">**When you are ready toodismount (or disconnect) hello Azure File share, you can do so by right clicking on hello entry for hello share under hello "Network locations" in File Explorer and selecting "Disconnect"**.</span></span>

## <a name="mount-hello-azure-file-share-with-powershell"></a><span data-ttu-id="efc39-159">Montar a partilha de ficheiros do Azure Olá com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="efc39-159">Mount hello Azure File share with PowerShell</span></span>
1. <span data-ttu-id="efc39-160">**Seguinte de Olá utilize comando partilha de ficheiros do Azure de Olá toomount**: memorizar tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` com informações adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="efc39-160">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. <span data-ttu-id="efc39-161">**Partilha de ficheiros do Azure Olá utilização conforme o desejado**.</span><span class="sxs-lookup"><span data-stu-id="efc39-161">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="efc39-162">**Quando tiver terminado, desmontar a partilha de ficheiros do Azure de Olá utilizando Olá os seguintes comandos**.</span><span class="sxs-lookup"><span data-stu-id="efc39-162">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> <span data-ttu-id="efc39-163">Pode utilizar Olá `-Persist` parâmetro no `New-PSDrive` toomake Olá ficheiros do Azure partilha toohello visível restante Olá SO enquanto montada.</span><span class="sxs-lookup"><span data-stu-id="efc39-163">You may use hello `-Persist` parameter on `New-PSDrive` toomake hello Azure File share visible toohello rest of hello OS while mounted.</span></span>

## <a name="mount-hello-azure-file-share-with-command-prompt"></a><span data-ttu-id="efc39-164">Montar a partilha de ficheiros do Azure Olá com linha de comandos</span><span class="sxs-lookup"><span data-stu-id="efc39-164">Mount hello Azure File share with Command Prompt</span></span>
1. <span data-ttu-id="efc39-165">**Seguinte de Olá utilize comando partilha de ficheiros do Azure de Olá toomount**: memorizar tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` com informações adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="efc39-165">**Use hello following command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` with hello proper information.</span></span>

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. <span data-ttu-id="efc39-166">**Partilha de ficheiros do Azure Olá utilização conforme o desejado**.</span><span class="sxs-lookup"><span data-stu-id="efc39-166">**Use hello Azure File share as desired**.</span></span>

3. <span data-ttu-id="efc39-167">**Quando tiver terminado, desmontar a partilha de ficheiros do Azure de Olá utilizando Olá os seguintes comandos**.</span><span class="sxs-lookup"><span data-stu-id="efc39-167">**When you are finished, dismount hello Azure File share using hello following command**.</span></span>

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> <span data-ttu-id="efc39-168">Pode configurar Olá ficheiros do Azure partilha tooautomatically restabelecer a ligação em reinício por persistentes Olá credenciais no Windows.</span><span class="sxs-lookup"><span data-stu-id="efc39-168">You can configure hello Azure File share tooautomatically reconnect on reboot by persisting hello credentials in Windows.</span></span> <span data-ttu-id="efc39-169">Olá seguir comando serão mantidas credenciais Olá:</span><span class="sxs-lookup"><span data-stu-id="efc39-169">hello following command will persist hello credentials:</span></span>
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a><span data-ttu-id="efc39-170">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="efc39-170">Next steps</span></span>
<span data-ttu-id="efc39-171">Consulte as ligações para obter mais informações sobre o Armazenamento de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="efc39-171">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="efc39-172">FAQ</span><span class="sxs-lookup"><span data-stu-id="efc39-172">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="efc39-173">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="efc39-173">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="efc39-174">Artigos e vídeos concetuais</span><span class="sxs-lookup"><span data-stu-id="efc39-174">Conceptual articles and videos</span></span>
* <span data-ttu-id="efc39-175">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/) (Armazenamento de Ficheiros do Azure: um prático sistema de ficheiros SMB na cloud para Windows e Linux)</span><span class="sxs-lookup"><span data-stu-id="efc39-175">[Azure File storage: a frictionless cloud SMB file system for Windows and Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)</span></span>
* [<span data-ttu-id="efc39-176">Como toouse File storage do Azure com o Linux</span><span class="sxs-lookup"><span data-stu-id="efc39-176">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a><span data-ttu-id="efc39-177">Suporte de ferramentas para o armazenamento de Ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="efc39-177">Tooling support for Azure File storage</span></span>
* [<span data-ttu-id="efc39-178">Using Azure PowerShell with Azure Storage (Utilizar o Azure PowerShell com o Armazenamento do Azure)</span><span class="sxs-lookup"><span data-stu-id="efc39-178">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="efc39-179">Como toouse AzCopy com armazenamento do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="efc39-179">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="efc39-180">Utilizar Olá CLI do Azure com o Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="efc39-180">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="efc39-181">Resolver problemas do armazenamento de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="efc39-181">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a><span data-ttu-id="efc39-182">Publicações no blogue</span><span class="sxs-lookup"><span data-stu-id="efc39-182">Blog posts</span></span>
* [<span data-ttu-id="efc39-183">Azure File storage is now generally available (O Armazenamento de Ficheiros do Azure está agora disponível normalmente)</span><span class="sxs-lookup"><span data-stu-id="efc39-183">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* <span data-ttu-id="efc39-184">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Por dentro do armazenamento de Ficheiros do Azure)</span><span class="sxs-lookup"><span data-stu-id="efc39-184">[Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/)</span></span>
* [<span data-ttu-id="efc39-185">Introducing Microsoft Azure File Service (Introdução ao Serviço de Ficheiros do Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="efc39-185">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="efc39-186">Migrar dados tooAzure ficheiro</span><span class="sxs-lookup"><span data-stu-id="efc39-186">Migrating data tooAzure File </span></span>](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a><span data-ttu-id="efc39-187">Referência</span><span class="sxs-lookup"><span data-stu-id="efc39-187">Reference</span></span>
* [<span data-ttu-id="efc39-188">Storage Client Library for .NET reference (Referência da Biblioteca de Clientes do Armazenamento para .NET)</span><span class="sxs-lookup"><span data-stu-id="efc39-188">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="efc39-189">File Service REST API reference (Referência da API REST do Serviço do Ficheiros)</span><span class="sxs-lookup"><span data-stu-id="efc39-189">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
