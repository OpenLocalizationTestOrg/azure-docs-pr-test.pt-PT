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
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Resolução de problemas de armazenamento de ficheiros do Azure no Linux

Este artigo apresenta uma lista de problemas comuns que estão relacionado tooMicrosoft File storage do Azure quando ligar a partir de clientes do Linux. Também fornece possíveis causas e soluções para esses problemas.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>"[permissão negada] disco a quota excedida" quando tenta tooopen um ficheiro

No Linux, receberá uma mensagem de erro é semelhante Olá seguinte:

**<filename>[permissão negada] Quota de disco foi excedida**

### <a name="cause"></a>Causa

Atingiu o limite superior de Olá de identificadores abertos simultâneos que são permitidos para um ficheiro.

### <a name="solution"></a>Solução

Reduza o número de Olá de identificadores abertos em simultâneo fechando alguns identificadores e, em seguida, repita a operação de Olá. Para obter mais informações, consulte [lista de verificação de armazenamento do Microsoft Azure, desempenho e escalabilidade](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Ficheiro lento copiar tooand do File storage do Azure no Linux

-   Se não tiver um requisito de tamanho de e/s mínimo específico, recomendamos que utilize 1 MB como Olá tamanho de e/s para um desempenho ideal.
-   Se souber o tamanho de final Olá de um ficheiro que estiver a expandir utilizando escritas e o software não surgir problemas de compatibilidade de uma cauda unwritten no ficheiro de Olá contém zeros, em seguida, defina o tamanho do ficheiro Olá antecipadamente em vez de efetuar cada escrita um expandir escreva.
-   Utilize o método de cópia correta de Olá:
    -   Utilize [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) para qualquer transferência entre duas partilhas de ficheiros.
    -   Utilize [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre partilhas de ficheiros no computador local.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>"Montar error(112): anfitrião encontra-se para baixo" devido a um limite de tempo de restabelecimento de ligação

Quando o cliente Olá está inativo há muito tempo, ocorre um erro de "112" montagem no cliente de Linux Olá. Após o período de tempo inativo alargado, Olá cliente desligar e ligação Olá exceder o tempo limite.  

### <a name="cause"></a>Causa

ligação de Olá pode ficar inactiva para Olá seguintes motivos:

-   Falhas de comunicação de rede que impedem a estabelecer novamente um servidor de toohello de ligação de TCP quando é utilizada a opção de montagem "de forma recuperável" Olá predefinida
-   Correções de restabelecimento de ligação recente que não estão presentes na kernels anteriores

### <a name="solution"></a>Solução

Este problema de restabelecimento de ligação na kernel de Linux Olá agora é corrigido como parte da Olá seguintes alterações:

- [Corrija restabelecer a ligação toonot diferir smb3 sessão restabelecimento de ligação de tempo depois de restabelecimento de ligação de socket](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Chamar o serviço de eco imediatamente após o restabelecimento de ligação de socket](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: Corrigir um danos de memória possível restabelecer a ligação](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: Corrigir uma possível duplo bloqueio de exclusão mútua durante a restabelecer ligação (para o kernel v4.9 e posterior)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

No entanto, estas alterações não podem ser convertidos, uma serem ainda tooall Olá as distribuições do Linux. Esta correção e outras correções de restabelecimento de ligação são efetuadas no Olá seguir populares Linux kernels: 4.4.40, 4.8.16 e 4.9.1. Pode obter esta correção atualizando tooone destas versões de kernel recomendada.

### <a name="workaround"></a>Solução

Pode contornar este problema, especificando uma montagem de disco rígida. Isto força o Olá cliente toowait até é estabelecida uma ligação ou até mesmo explicitamente for interrompido e pode ser utilizados tooprevent erros devido a tempos limite de rede. No entanto, esta solução pode fazer com que aguarda indefinida. Ser preparado toostop ligações conforme necessário.

Se não é possível atualizar versões de kernel mais recentes toohello, pode contornar este problema por manter um ficheiro na partilha de ficheiros do Azure de Olá que escrever tooevery 30 segundos ou menos. Tem de ser uma operação de escrita, tais como conversão Olá criados ou modificados data no ficheiro de Olá. Caso contrário, poderá obter resultados em cache e a operação não pode acionar restabelecimento de ligação de Olá.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>"Montar error(115): operação agora em curso" ao montar o File storage do Azure utilizando o SMB 3.0

### <a name="cause"></a>Causa

Algumas distribuições de Linux ainda não suportam funcionalidades de encriptação no SMB 3.0 e os utilizadores podem receber uma mensagem de erro "115" se estes tentarem toomount File storage do Azure utilizando o SMB 3.0 devido a uma funcionalidade em falta.

### <a name="solution"></a>Solução

Funcionalidade de encriptação para SMB 3.0 para Linux foi introduzida no 4.11 kernel. Esta funcionalidade permite a montagem do Azure da partilha de ficheiros no local ou uma região do Azure diferente. Momento Olá da publicação, esta funcionalidade foi backported tooUbuntu 17.04 e Ubuntu 16.10. Se o cliente SMB de Linux não suporta a encriptação, Monte o File storage do Azure utilizando o SMB 2.1 a partir de uma VM com Linux do Azure que se encontra no mesmo centro de dados de Olá como Olá conta de armazenamento de ficheiros.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Desempenho lento numa partilha de ficheiros do Azure montado numa VM com Linux

### <a name="cause"></a>Causa

Uma causa possível de desempenho lento está desativada a colocação em cache.

### <a name="solution"></a>Solução

toocheck se a colocação em cache está desativada, procure Olá **cache =** entrada. 

**Cache = none** indica que a colocação em cache está desativada.  Remontagem Olá partilha utilizando o comando de montagem Olá predefinido ou adicionando explicitamente Olá **cache = strict** opção toohello montagem comando tooensure que predefinido "strict" ou colocação em cache no modo de colocação em cache está ativada.

Em alguns cenários, Olá **serverino** montagem opção pode causar Olá **ls** stat do comando toorun em relação a cada entrada de diretório. Este comportamento resulta numa degradação do desempenho quando está a listar um grande diretório. Pode verificar as opções de montagem Olá seu **etc/fstab** entrada:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Também pode verificar se as opções corretas Olá estão a ser utilizadas executando Olá **sudo montagem | grep cifs** comando e a verificar o resultado, tais como Olá saídas de exemplo a seguir:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Se hello **cache = strict** ou **serverino** opção é não está presente, desmontar e Monte o File storage do Azure novamente executando o comando de montagem de Olá de Olá [documentação](../storage-how-to-use-files-linux.md). Em seguida, voltar esse Olá **etc/fstab** entrada tem opções corretas Olá.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Carimbos de data / hora foram perdidas ao copiar ficheiros do Windows tooLinux

Em plataformas Linux/Unix, Olá **cp -p** comando falha se o ficheiro 1 e 2 são propriedade de diferentes utilizadores.

### <a name="cause"></a>Causa

Olá sinalizador force **f** no COPYFILE resulta na execução **cp -p -f** no Unix. Este comando também falha carimbo de hora Olá toopreserve Olá do ficheiro de que não possui.

### <a name="workaround"></a>Solução

Utilize o utilizador da conta de armazenamento Olá para copiar ficheiros de Olá:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Precisa de ajuda? Contacte o suporte.

Se ainda precisar de ajuda, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
