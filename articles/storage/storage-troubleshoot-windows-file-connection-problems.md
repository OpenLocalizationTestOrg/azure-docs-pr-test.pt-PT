---
title: problemas de armazenamento de ficheiros do Azure aaaTroubleshoot no Windows | Microsoft Docs
description: "Resolução de problemas de armazenamento de ficheiros do Azure no Windows"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="674e3-103">Resolução de problemas de armazenamento de ficheiros do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="674e3-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="674e3-104">Este artigo apresenta uma lista de problemas comuns que estão relacionado tooMicrosoft File storage do Azure ao ligar a partir de clientes do Windows.</span><span class="sxs-lookup"><span data-stu-id="674e3-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="674e3-105">Também fornece possíveis causas e soluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="674e3-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="674e3-106">Além disso, a resolução de problemas de toohello passos neste artigo, também pode utilizar [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) para garantir que esse Olá Windows, ambiente de cliente tem de pré-requisitos corretos.</span><span class="sxs-lookup"><span data-stu-id="674e3-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="674e3-107">AzFileDiagnostics automatiza a deteção da maioria dos sintomas Olá mencionadas neste artigo e ajuda a configurar o seu ambiente tooget um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="674e3-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="674e3-108">Também pode encontrar estas informações no Olá [Troubleshooter as partilhas de ficheiros do Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) que fornece os passos tooassist que com problemas de partilhas de ficheiros de ligar/mapeamento/a montagem do Azure.</span><span class="sxs-lookup"><span data-stu-id="674e3-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="674e3-109">Erro de 53, erro 67 ou erro 87 quando montar ou desmontar uma partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="674e3-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="674e3-110">Quando tenta toomount um partilha de ficheiros no local ou a partir do Centro de dados diferentes, poderá receber Olá seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="674e3-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="674e3-111">Ocorreu um erro de sistema 53.</span><span class="sxs-lookup"><span data-stu-id="674e3-111">System error 53 has occurred.</span></span> <span data-ttu-id="674e3-112">caminho de rede Olá não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="674e3-112">hello network path was not found.</span></span>
- <span data-ttu-id="674e3-113">Ocorreu um erro de sistema 67.</span><span class="sxs-lookup"><span data-stu-id="674e3-113">System error 67 has occurred.</span></span> <span data-ttu-id="674e3-114">Não é possível localizar o nome da rede Olá.</span><span class="sxs-lookup"><span data-stu-id="674e3-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="674e3-115">Ocorreu um erro de sistema 87.</span><span class="sxs-lookup"><span data-stu-id="674e3-115">System error 87 has occurred.</span></span> <span data-ttu-id="674e3-116">Olá parâmetro está incorreto.</span><span class="sxs-lookup"><span data-stu-id="674e3-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="674e3-117">Causa 1: Canal de comunicação sem encriptação</span><span class="sxs-lookup"><span data-stu-id="674e3-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="674e3-118">Por motivos de segurança, ligações tooAzure partilhas de ficheiros estão bloqueadas se o canal de comunicação de Olá não está encriptada e se a tentativa de ligação de Olá não é feita a partir do Olá mesmo centro de dados onde residem Olá partilhas de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="674e3-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="674e3-119">Encriptação de canal de comunicação é fornecida apenas se o cliente do utilizador Olá SO suporta encriptação SMB.</span><span class="sxs-lookup"><span data-stu-id="674e3-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="674e3-120">Windows 8, Windows Server 2012 e versões posteriores do sistema de cada negociar pedidos que incluem o SMB 3.0, que suporta a encriptação.</span><span class="sxs-lookup"><span data-stu-id="674e3-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="674e3-121">Solução para causa 1</span><span class="sxs-lookup"><span data-stu-id="674e3-121">Solution for cause 1</span></span>

<span data-ttu-id="674e3-122">Ligar a partir de um cliente que suporta um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="674e3-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="674e3-123">Cumpre os requisitos de Olá do Windows 8 e Windows Server 2012 ou versões posteriores</span><span class="sxs-lookup"><span data-stu-id="674e3-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="674e3-124">Liga-se de uma máquina virtual no Olá mesmo centro de dados como Olá conta do storage do Azure que é utilizada para a partilha de ficheiros do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="674e3-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="674e3-125">Causa 2: A porta 445 está bloqueada</span><span class="sxs-lookup"><span data-stu-id="674e3-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="674e3-126">Erro de sistema 53 ou erro de sistema 67 pode ocorrer se a porta 445 comunicação de saída tooan ficheiros do Azure armazenamento Centro de dados está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="674e3-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="674e3-127">Resumo de Olá toosee de ISPs que permitem ou não permitir acesso de porta 445, aceda demasiado[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="674e3-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="674e3-128">toounderstand se é este motivo de Olá atrás de mensagem de "Erro de sistema 53" Olá, pode utilizar o ponto final do Portqry tooquery Olá TCP:445.</span><span class="sxs-lookup"><span data-stu-id="674e3-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="674e3-129">Se o ponto final de TCP:445 Olá é apresentada como filtrado, Olá a porta TCP está bloqueada.</span><span class="sxs-lookup"><span data-stu-id="674e3-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="674e3-130">Eis um exemplo de consulta:</span><span class="sxs-lookup"><span data-stu-id="674e3-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="674e3-131">Se a porta TCP 445 está bloqueada por uma regra ao longo do caminho de rede Olá, verá Olá seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="674e3-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="674e3-132">Para obter mais informações sobre como toouse Portqry, consulte [descrição do utilitário de linha de comandos Olá Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="674e3-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="674e3-133">Solução para causa 2</span><span class="sxs-lookup"><span data-stu-id="674e3-133">Solution for cause 2</span></span>

<span data-ttu-id="674e3-134">Trabalhar com a porta de tooopen do departamento de IT 445 saída demasiado[intervalos de IP de Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="674e3-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="674e3-135">Causa 3: NTLMv1 está ativado</span><span class="sxs-lookup"><span data-stu-id="674e3-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="674e3-136">Erro de sistema 53 ou erro de sistema 87 pode ocorrer se estiver ativada NTLMv1 comunicação no cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="674e3-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="674e3-137">File storage do Azure suporta apenas a autenticação NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="674e3-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="674e3-138">Ter NTLMv1 ativado cria um cliente menos seguras.</span><span class="sxs-lookup"><span data-stu-id="674e3-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="674e3-139">Por conseguinte, a comunicação está bloqueada para o File storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="674e3-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="674e3-140">toodetermine se esta é a causa de Olá erro Olá, certifique-se de que Olá seguinte subchave de registo está definida tooa valor de 3:</span><span class="sxs-lookup"><span data-stu-id="674e3-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="674e3-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="674e3-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="674e3-142">Para obter mais informações, consulte Olá [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) tópico no TechNet.</span><span class="sxs-lookup"><span data-stu-id="674e3-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="674e3-143">Solução para causa 3</span><span class="sxs-lookup"><span data-stu-id="674e3-143">Solution for cause 3</span></span>

<span data-ttu-id="674e3-144">Reverter Olá **LmCompatibilityLevel** valor toohello valor predefinido 3 na Olá seguinte subchave de registo:</span><span class="sxs-lookup"><span data-stu-id="674e3-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="674e3-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="674e3-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="674e3-146">Erro 1816 "insuficiente quota é tooprocess disponíveis este comando" quando copiar tooan partilha de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="674e3-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="674e3-147">Causa</span><span class="sxs-lookup"><span data-stu-id="674e3-147">Cause</span></span>

<span data-ttu-id="674e3-148">Ocorre um erro 1816 quando atingir o limite superior de Olá de identificadores abertos simultâneos que são permitidos para um ficheiro num computador de olá onde a partilha de ficheiros de Olá está a ser montada.</span><span class="sxs-lookup"><span data-stu-id="674e3-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="674e3-149">Solução</span><span class="sxs-lookup"><span data-stu-id="674e3-149">Solution</span></span>

<span data-ttu-id="674e3-150">Reduza o número de Olá de identificadores abertos em simultâneo fechando alguns identificadores e, em seguida, tente novamente.</span><span class="sxs-lookup"><span data-stu-id="674e3-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="674e3-151">Para obter mais informações, consulte [lista de verificação de armazenamento do Microsoft Azure, desempenho e escalabilidade](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="674e3-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="674e3-152">Ficheiro lento copiar tooand do File storage do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="674e3-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="674e3-153">Poderá ver um desempenho lento quando tenta tootransfer ficheiros toohello serviço de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="674e3-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="674e3-154">Se não tiver um requisito de tamanho de e/s mínimo específico, recomendamos que utilize 1 MB como Olá tamanho de e/s para um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="674e3-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="674e3-155">Se souber tamanho final do Olá de um ficheiro que estiver a expandir com escreve e o software não tem problemas de compatibilidade quando hello seguimento unwritten no ficheiro de Olá contém zeros, em seguida, conjunto Olá tamanho do ficheiro seguinte com antecedência em vez de efetuar cada escrita uma escrita expandir.</span><span class="sxs-lookup"><span data-stu-id="674e3-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="674e3-156">Utilize o método de cópia correta de Olá:</span><span class="sxs-lookup"><span data-stu-id="674e3-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="674e3-157">Utilize [AzCopy](storage-use-azcopy.md#file-copy) para qualquer transferência entre duas partilhas de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="674e3-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="674e3-158">Utilize [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre partilhas de ficheiros no computador local.</span><span class="sxs-lookup"><span data-stu-id="674e3-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="674e3-159">Considerações para Windows 8.1 ou Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="674e3-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="674e3-160">Para clientes que estejam a executar o Windows 8.1 ou Windows Server 2012 R2, certifique-se que Olá [KB3114025](https://support.microsoft.com/help/3114025) correção está instalada.</span><span class="sxs-lookup"><span data-stu-id="674e3-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="674e3-161">Esta correção melhora o desempenho de Olá de create e feche identificadores.</span><span class="sxs-lookup"><span data-stu-id="674e3-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="674e3-162">Pode executar Olá toocheck de script a seguir se tiver sido instalada a correção de Olá:</span><span class="sxs-lookup"><span data-stu-id="674e3-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="674e3-163">Se a correção está instalada, hello seguinte resultado é apresentado:</span><span class="sxs-lookup"><span data-stu-id="674e3-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="674e3-164">Imagens do Windows Server 2012 R2 no Azure Marketplace tem correções KB3114025 instalado por predefinição, a partir de Dezembro de 2015.</span><span class="sxs-lookup"><span data-stu-id="674e3-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="674e3-165">Não existem pasta com uma letra de unidade na **meu computador**</span><span class="sxs-lookup"><span data-stu-id="674e3-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="674e3-166">Se mapear uma partilha de ficheiros do Azure como um administrador através de utilização de rede, a partilha de Olá aparece toobe em falta.</span><span class="sxs-lookup"><span data-stu-id="674e3-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="674e3-167">Causa</span><span class="sxs-lookup"><span data-stu-id="674e3-167">Cause</span></span>

<span data-ttu-id="674e3-168">Por predefinição, o Explorador de ficheiros do Windows não é executado como administrador.</span><span class="sxs-lookup"><span data-stu-id="674e3-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="674e3-169">Se executar o net utilização a partir de uma linha de comandos administrativa, mapear unidade de rede Olá como administrador.</span><span class="sxs-lookup"><span data-stu-id="674e3-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="674e3-170">Dado que as unidades mapeadas centrada no utilizador, conta de utilizador Olá, que é registada no não apresentar unidades Olá se estão montados numa conta de utilizador diferente.</span><span class="sxs-lookup"><span data-stu-id="674e3-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="674e3-171">Solução</span><span class="sxs-lookup"><span data-stu-id="674e3-171">Solution</span></span>
<span data-ttu-id="674e3-172">Monte a partilha de Olá partir de uma linha de comandos de não administrador.</span><span class="sxs-lookup"><span data-stu-id="674e3-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="674e3-173">Em alternativa, pode seguir [neste tópico do TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure Olá **EnableLinkedConnections** valor de registo.</span><span class="sxs-lookup"><span data-stu-id="674e3-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="674e3-174">Comando net use falha se a conta de armazenamento de Olá contém uma barra</span><span class="sxs-lookup"><span data-stu-id="674e3-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="674e3-175">Causa</span><span class="sxs-lookup"><span data-stu-id="674e3-175">Cause</span></span>

<span data-ttu-id="674e3-176">comando de net use Olá interpreta uma barra (/) como uma opção de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="674e3-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="674e3-177">Se o nome da sua conta de utilizador for iniciado com uma barra, o mapeamento de unidade de Olá falha.</span><span class="sxs-lookup"><span data-stu-id="674e3-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="674e3-178">Solução</span><span class="sxs-lookup"><span data-stu-id="674e3-178">Solution</span></span>

<span data-ttu-id="674e3-179">Pode utilizar qualquer um dos Olá passos toowork em torno do problema Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="674e3-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="674e3-180">Execute o seguinte comando do PowerShell de Olá:</span><span class="sxs-lookup"><span data-stu-id="674e3-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="674e3-181">De um ficheiro batch, pode executar o comando de Olá desta forma:</span><span class="sxs-lookup"><span data-stu-id="674e3-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="674e3-182">Colocar carateres de aspas à volta de Olá toowork chave em torno este problema – a menos que a barra de Olá é o primeiro caráter de Olá.</span><span class="sxs-lookup"><span data-stu-id="674e3-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="674e3-183">Se estiver, utilize o modo interativo Olá e introduza a palavra-passe em separado ou voltar a gerar a chaves tooget uma chave que não iniciar com uma barra.</span><span class="sxs-lookup"><span data-stu-id="674e3-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="674e3-184">Aplicação ou serviço não é possível aceder a uma unidade de armazenamento de ficheiros do Azure montada</span><span class="sxs-lookup"><span data-stu-id="674e3-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="674e3-185">Causa</span><span class="sxs-lookup"><span data-stu-id="674e3-185">Cause</span></span>

<span data-ttu-id="674e3-186">Unidades estão montadas por utilizador.</span><span class="sxs-lookup"><span data-stu-id="674e3-186">Drives are mounted per user.</span></span> <span data-ttu-id="674e3-187">Se a aplicação ou serviço está em execução com uma conta de utilizador diferente Olá que montar a unidade de Olá, aplicação Olá não verão a unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="674e3-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="674e3-188">Solução</span><span class="sxs-lookup"><span data-stu-id="674e3-188">Solution</span></span>

<span data-ttu-id="674e3-189">Utilize uma das seguintes soluções de Olá:</span><span class="sxs-lookup"><span data-stu-id="674e3-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="674e3-190">Montar a unidade de Olá partir Olá mesma conta de utilizador que contém a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="674e3-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="674e3-191">Pode utilizar uma ferramenta como o PsExec.</span><span class="sxs-lookup"><span data-stu-id="674e3-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="674e3-192">Transmita o nome de conta do storage Olá e a chave Olá utilizador nome e palavra-passe parâmetros do comando de net use Olá.</span><span class="sxs-lookup"><span data-stu-id="674e3-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="674e3-193">Depois de seguir estas instruções, poderá receber Olá seguir a mensagem de erro quando executa net utilização para a conta de serviço de sistema/rede Olá: "erro de sistema 1312 foi excedido.</span><span class="sxs-lookup"><span data-stu-id="674e3-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="674e3-194">Uma sessão de início de sessão especificado não existe.</span><span class="sxs-lookup"><span data-stu-id="674e3-194">A specified logon session does not exist.</span></span> <span data-ttu-id="674e3-195">-Pode já ter foi terminada."</span><span class="sxs-lookup"><span data-stu-id="674e3-195">It may already have been terminated."</span></span> <span data-ttu-id="674e3-196">Se isto ocorrer, certifique-se de que nome de utilizador Olá que é transmitido a utilização de toonet inclui informações de domínio (por exemplo: "[nome da conta de armazenamento]. file.core.windows .net").</span><span class="sxs-lookup"><span data-stu-id="674e3-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="674e3-197">Erro "Está a copiar um destino de tooa de ficheiro que não suporta encriptação"</span><span class="sxs-lookup"><span data-stu-id="674e3-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="674e3-198">Quando um ficheiro é copiado através de rede de Olá, ficheiro Olá é desencriptado no computador de origem Olá, transmitidas em texto não encriptado e encriptados novamente no destino Olá.</span><span class="sxs-lookup"><span data-stu-id="674e3-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="674e3-199">No entanto, poderá ver Olá os seguintes erros quando está a tentar toocopy um ficheiro encriptado: "Está a copiar Olá tooa o destino de ficheiro que não suporta encriptação."</span><span class="sxs-lookup"><span data-stu-id="674e3-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="674e3-200">Causa</span><span class="sxs-lookup"><span data-stu-id="674e3-200">Cause</span></span>
<span data-ttu-id="674e3-201">Este problema pode ocorrer se estiver a utilizar o sistema de encriptação de ficheiros (EFS).</span><span class="sxs-lookup"><span data-stu-id="674e3-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="674e3-202">Ficheiros encriptados por BitLocker podem ser copiados tooAzure o File storage.</span><span class="sxs-lookup"><span data-stu-id="674e3-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="674e3-203">No entanto, o File storage do Azure não suporta NTFS EFS.</span><span class="sxs-lookup"><span data-stu-id="674e3-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="674e3-204">Solução</span><span class="sxs-lookup"><span data-stu-id="674e3-204">Workaround</span></span>
<span data-ttu-id="674e3-205">toocopy um ficheiro através de rede de Olá, primeiro tem de desencriptá-lo.</span><span class="sxs-lookup"><span data-stu-id="674e3-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="674e3-206">Utilize um dos seguintes métodos de Olá:</span><span class="sxs-lookup"><span data-stu-id="674e3-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="674e3-207">Olá utilize **copiar /d** comando.</span><span class="sxs-lookup"><span data-stu-id="674e3-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="674e3-208">Permite que Olá encriptado ficheiros toobe guardado como ficheiros desencriptados no destino Olá.</span><span class="sxs-lookup"><span data-stu-id="674e3-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="674e3-209">Definir Olá seguinte chave de registo:</span><span class="sxs-lookup"><span data-stu-id="674e3-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="674e3-210">Caminho = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="674e3-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="674e3-211">Tipo de valor = DWORD</span><span class="sxs-lookup"><span data-stu-id="674e3-211">Value type = DWORD</span></span>
  - <span data-ttu-id="674e3-212">Nome = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="674e3-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="674e3-213">Valor = 1</span><span class="sxs-lookup"><span data-stu-id="674e3-213">Value = 1</span></span>

<span data-ttu-id="674e3-214">Lembre-se de que essa chave de registo de Olá definição afeta todas as operações de cópia que são efetuadas toonetwork partilhas.</span><span class="sxs-lookup"><span data-stu-id="674e3-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="674e3-215">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="674e3-215">Need help?</span></span> <span data-ttu-id="674e3-216">Contacte o suporte.</span><span class="sxs-lookup"><span data-stu-id="674e3-216">Contact support.</span></span>
<span data-ttu-id="674e3-217">Se ainda precisar de ajuda, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="674e3-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
