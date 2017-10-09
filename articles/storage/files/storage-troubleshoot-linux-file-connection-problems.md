---
title: problemas de armazenamento de ficheiros do Azure aaaTroubleshoot no Linux | Microsoft Docs
description: "Resolução de problemas de armazenamento de ficheiros do Azure no Linux"
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
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 4bdc3c6ed2e48f245060a03632fca9bd14d33545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="d2713-103">Resolução de problemas de armazenamento de ficheiros do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="d2713-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="d2713-104">Este artigo apresenta uma lista de problemas comuns que estão relacionado tooMicrosoft File storage do Azure quando ligar a partir de clientes do Linux.</span><span class="sxs-lookup"><span data-stu-id="d2713-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="d2713-105">Também fornece possíveis causas e soluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="d2713-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="d2713-106">"[permissão negada] disco a quota excedida" quando tenta tooopen um ficheiro</span><span class="sxs-lookup"><span data-stu-id="d2713-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="d2713-107">No Linux, receberá uma mensagem de erro é semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="d2713-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="d2713-108">**<filename>[permissão negada] Quota de disco foi excedida**</span><span class="sxs-lookup"><span data-stu-id="d2713-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="d2713-109">Causa</span><span class="sxs-lookup"><span data-stu-id="d2713-109">Cause</span></span>

<span data-ttu-id="d2713-110">Atingiu o limite superior de Olá de identificadores abertos simultâneos que são permitidos para um ficheiro.</span><span class="sxs-lookup"><span data-stu-id="d2713-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="d2713-111">Solução</span><span class="sxs-lookup"><span data-stu-id="d2713-111">Solution</span></span>

<span data-ttu-id="d2713-112">Reduza o número de Olá de identificadores abertos em simultâneo fechando alguns identificadores e, em seguida, repita a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d2713-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="d2713-113">Para obter mais informações, consulte [lista de verificação de armazenamento do Microsoft Azure, desempenho e escalabilidade](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d2713-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="d2713-114">Ficheiro lento copiar tooand do File storage do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="d2713-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="d2713-115">Se não tiver um requisito de tamanho de e/s mínimo específico, recomendamos que utilize 1 MB como Olá tamanho de e/s para um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="d2713-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="d2713-116">Se souber o tamanho de final Olá de um ficheiro que estiver a expandir utilizando escritas e o software não surgir problemas de compatibilidade de uma cauda unwritten no ficheiro de Olá contém zeros, em seguida, defina o tamanho do ficheiro Olá antecipadamente em vez de efetuar cada escrita um expandir escreva.</span><span class="sxs-lookup"><span data-stu-id="d2713-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="d2713-117">Utilize o método de cópia correta de Olá:</span><span class="sxs-lookup"><span data-stu-id="d2713-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="d2713-118">Utilize [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) para qualquer transferência entre duas partilhas de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="d2713-118">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="d2713-119">Utilize [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre partilhas de ficheiros no computador local.</span><span class="sxs-lookup"><span data-stu-id="d2713-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="d2713-120">"Montar error(112): anfitrião encontra-se para baixo" devido a um limite de tempo de restabelecimento de ligação</span><span class="sxs-lookup"><span data-stu-id="d2713-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="d2713-121">Quando o cliente Olá está inativo há muito tempo, ocorre um erro de "112" montagem no cliente de Linux Olá.</span><span class="sxs-lookup"><span data-stu-id="d2713-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="d2713-122">Após o período de tempo inativo alargado, Olá cliente desligar e ligação Olá exceder o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="d2713-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="d2713-123">Causa</span><span class="sxs-lookup"><span data-stu-id="d2713-123">Cause</span></span>

<span data-ttu-id="d2713-124">ligação de Olá pode ficar inactiva para Olá seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="d2713-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="d2713-125">Falhas de comunicação de rede que impedem a estabelecer novamente um servidor de toohello de ligação de TCP quando é utilizada a opção de montagem "de forma recuperável" Olá predefinida</span><span class="sxs-lookup"><span data-stu-id="d2713-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="d2713-126">Correções de restabelecimento de ligação recente que não estão presentes na kernels anteriores</span><span class="sxs-lookup"><span data-stu-id="d2713-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="d2713-127">Solução</span><span class="sxs-lookup"><span data-stu-id="d2713-127">Solution</span></span>

<span data-ttu-id="d2713-128">Este problema de restabelecimento de ligação na kernel de Linux Olá agora é corrigido como parte da Olá seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="d2713-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="d2713-129">Corrija restabelecer a ligação toonot diferir smb3 sessão restabelecimento de ligação de tempo depois de restabelecimento de ligação de socket</span><span class="sxs-lookup"><span data-stu-id="d2713-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="d2713-130">Chamar o serviço de eco imediatamente após o restabelecimento de ligação de socket</span><span class="sxs-lookup"><span data-stu-id="d2713-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="d2713-131">CIFS: Corrigir um danos de memória possível restabelecer a ligação</span><span class="sxs-lookup"><span data-stu-id="d2713-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="d2713-132">CIFS: Corrigir uma possível duplo bloqueio de exclusão mútua durante a restabelecer ligação (para o kernel v4.9 e posterior)</span><span class="sxs-lookup"><span data-stu-id="d2713-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="d2713-133">No entanto, estas alterações não podem ser convertidos, uma serem ainda tooall Olá as distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="d2713-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="d2713-134">Esta correção e outras correções de restabelecimento de ligação são efetuadas no Olá seguir populares Linux kernels: 4.4.40, 4.8.16 e 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="d2713-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="d2713-135">Pode obter esta correção atualizando tooone destas versões de kernel recomendada.</span><span class="sxs-lookup"><span data-stu-id="d2713-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="d2713-136">Solução</span><span class="sxs-lookup"><span data-stu-id="d2713-136">Workaround</span></span>

<span data-ttu-id="d2713-137">Pode contornar este problema, especificando uma montagem de disco rígida.</span><span class="sxs-lookup"><span data-stu-id="d2713-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="d2713-138">Isto força o Olá cliente toowait até é estabelecida uma ligação ou até mesmo explicitamente for interrompido e pode ser utilizados tooprevent erros devido a tempos limite de rede.</span><span class="sxs-lookup"><span data-stu-id="d2713-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="d2713-139">No entanto, esta solução pode fazer com que aguarda indefinida.</span><span class="sxs-lookup"><span data-stu-id="d2713-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="d2713-140">Ser preparado toostop ligações conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="d2713-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="d2713-141">Se não é possível atualizar versões de kernel mais recentes toohello, pode contornar este problema por manter um ficheiro na partilha de ficheiros do Azure de Olá que escrever tooevery 30 segundos ou menos.</span><span class="sxs-lookup"><span data-stu-id="d2713-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="d2713-142">Tem de ser uma operação de escrita, tais como conversão Olá criados ou modificados data no ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d2713-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="d2713-143">Caso contrário, poderá obter resultados em cache e a operação não pode acionar restabelecimento de ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d2713-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="d2713-144">"Montar error(115): operação agora em curso" ao montar o File storage do Azure utilizando o SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="d2713-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="d2713-145">Causa</span><span class="sxs-lookup"><span data-stu-id="d2713-145">Cause</span></span>

<span data-ttu-id="d2713-146">Algumas distribuições de Linux ainda não suportam funcionalidades de encriptação no SMB 3.0 e os utilizadores podem receber uma mensagem de erro "115" se estes tentarem toomount File storage do Azure utilizando o SMB 3.0 devido a uma funcionalidade em falta.</span><span class="sxs-lookup"><span data-stu-id="d2713-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="d2713-147">Solução</span><span class="sxs-lookup"><span data-stu-id="d2713-147">Solution</span></span>

<span data-ttu-id="d2713-148">Funcionalidade de encriptação para SMB 3.0 para Linux foi introduzida no 4.11 kernel.</span><span class="sxs-lookup"><span data-stu-id="d2713-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="d2713-149">Esta funcionalidade permite a montagem do Azure da partilha de ficheiros no local ou uma região do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="d2713-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="d2713-150">Momento Olá da publicação, esta funcionalidade foi backported tooUbuntu 17.04 e Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="d2713-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="d2713-151">Se o cliente SMB de Linux não suporta a encriptação, Monte o File storage do Azure utilizando o SMB 2.1 a partir de uma VM com Linux do Azure que se encontra no mesmo centro de dados de Olá como Olá conta de armazenamento de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="d2713-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="d2713-152">Desempenho lento numa partilha de ficheiros do Azure montado numa VM com Linux</span><span class="sxs-lookup"><span data-stu-id="d2713-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="d2713-153">Causa</span><span class="sxs-lookup"><span data-stu-id="d2713-153">Cause</span></span>

<span data-ttu-id="d2713-154">Uma causa possível de desempenho lento está desativada a colocação em cache.</span><span class="sxs-lookup"><span data-stu-id="d2713-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="d2713-155">Solução</span><span class="sxs-lookup"><span data-stu-id="d2713-155">Solution</span></span>

<span data-ttu-id="d2713-156">toocheck se a colocação em cache está desativada, procure Olá **cache =** entrada.</span><span class="sxs-lookup"><span data-stu-id="d2713-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="d2713-157">**Cache = none** indica que a colocação em cache está desativada.</span><span class="sxs-lookup"><span data-stu-id="d2713-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="d2713-158">Remontagem Olá partilha utilizando o comando de montagem Olá predefinido ou adicionando explicitamente Olá **cache = strict** opção toohello montagem comando tooensure que predefinido "strict" ou colocação em cache no modo de colocação em cache está ativada.</span><span class="sxs-lookup"><span data-stu-id="d2713-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="d2713-159">Em alguns cenários, Olá **serverino** montagem opção pode causar Olá **ls** stat do comando toorun em relação a cada entrada de diretório.</span><span class="sxs-lookup"><span data-stu-id="d2713-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="d2713-160">Este comportamento resulta numa degradação do desempenho quando está a listar um grande diretório.</span><span class="sxs-lookup"><span data-stu-id="d2713-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="d2713-161">Pode verificar as opções de montagem Olá seu **etc/fstab** entrada:</span><span class="sxs-lookup"><span data-stu-id="d2713-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="d2713-162">Também pode verificar se as opções corretas Olá estão a ser utilizadas executando Olá **sudo montagem | grep cifs** comando e a verificar o resultado, tais como Olá saídas de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2713-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="d2713-163">Se hello **cache = strict** ou **serverino** opção é não está presente, desmontar e Monte o File storage do Azure novamente executando o comando de montagem de Olá de Olá [documentação](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d2713-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](../storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="d2713-164">Em seguida, voltar esse Olá **etc/fstab** entrada tem opções corretas Olá.</span><span class="sxs-lookup"><span data-stu-id="d2713-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="d2713-165">Carimbos de data / hora foram perdidas ao copiar ficheiros do Windows tooLinux</span><span class="sxs-lookup"><span data-stu-id="d2713-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="d2713-166">Em plataformas Linux/Unix, Olá **cp -p** comando falha se o ficheiro 1 e 2 são propriedade de diferentes utilizadores.</span><span class="sxs-lookup"><span data-stu-id="d2713-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="d2713-167">Causa</span><span class="sxs-lookup"><span data-stu-id="d2713-167">Cause</span></span>

<span data-ttu-id="d2713-168">Olá sinalizador force **f** no COPYFILE resulta na execução **cp -p -f** no Unix.</span><span class="sxs-lookup"><span data-stu-id="d2713-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="d2713-169">Este comando também falha carimbo de hora Olá toopreserve Olá do ficheiro de que não possui.</span><span class="sxs-lookup"><span data-stu-id="d2713-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="d2713-170">Solução</span><span class="sxs-lookup"><span data-stu-id="d2713-170">Workaround</span></span>

<span data-ttu-id="d2713-171">Utilize o utilizador da conta de armazenamento Olá para copiar ficheiros de Olá:</span><span class="sxs-lookup"><span data-stu-id="d2713-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="d2713-172">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="d2713-172">Need help?</span></span> <span data-ttu-id="d2713-173">Contacte o suporte.</span><span class="sxs-lookup"><span data-stu-id="d2713-173">Contact support.</span></span>

<span data-ttu-id="d2713-174">Se ainda precisar de ajuda, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="d2713-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
