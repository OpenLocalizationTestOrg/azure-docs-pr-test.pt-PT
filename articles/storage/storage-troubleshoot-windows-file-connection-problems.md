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
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Resolução de problemas de armazenamento de ficheiros do Azure no Windows

Este artigo apresenta uma lista de problemas comuns que estão relacionado tooMicrosoft File storage do Azure ao ligar a partir de clientes do Windows. Também fornece possíveis causas e soluções para esses problemas. Além disso, a resolução de problemas de toohello passos neste artigo, também pode utilizar [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) para garantir que esse Olá Windows, ambiente de cliente tem de pré-requisitos corretos. AzFileDiagnostics automatiza a deteção da maioria dos sintomas Olá mencionadas neste artigo e ajuda a configurar o seu ambiente tooget um desempenho ideal. Também pode encontrar estas informações no Olá [Troubleshooter as partilhas de ficheiros do Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) que fornece os passos tooassist que com problemas de partilhas de ficheiros de ligar/mapeamento/a montagem do Azure.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Erro de 53, erro 67 ou erro 87 quando montar ou desmontar uma partilha de ficheiros do Azure

Quando tenta toomount um partilha de ficheiros no local ou a partir do Centro de dados diferentes, poderá receber Olá seguintes erros:

- Ocorreu um erro de sistema 53. caminho de rede Olá não foi encontrado.
- Ocorreu um erro de sistema 67. Não é possível localizar o nome da rede Olá.
- Ocorreu um erro de sistema 87. Olá parâmetro está incorreto.

### <a name="cause-1-unencrypted-communication-channel"></a>Causa 1: Canal de comunicação sem encriptação

Por motivos de segurança, ligações tooAzure partilhas de ficheiros estão bloqueadas se o canal de comunicação de Olá não está encriptada e se a tentativa de ligação de Olá não é feita a partir do Olá mesmo centro de dados onde residem Olá partilhas de ficheiros do Azure. Encriptação de canal de comunicação é fornecida apenas se o cliente do utilizador Olá SO suporta encriptação SMB.

Windows 8, Windows Server 2012 e versões posteriores do sistema de cada negociar pedidos que incluem o SMB 3.0, que suporta a encriptação.

### <a name="solution-for-cause-1"></a>Solução para causa 1

Ligar a partir de um cliente que suporta um dos seguintes Olá:

- Cumpre os requisitos de Olá do Windows 8 e Windows Server 2012 ou versões posteriores
- Liga-se de uma máquina virtual no Olá mesmo centro de dados como Olá conta do storage do Azure que é utilizada para a partilha de ficheiros do Azure Olá

### <a name="cause-2-port-445-is-blocked"></a>Causa 2: A porta 445 está bloqueada

Erro de sistema 53 ou erro de sistema 67 pode ocorrer se a porta 445 comunicação de saída tooan ficheiros do Azure armazenamento Centro de dados está bloqueada. Resumo de Olá toosee de ISPs que permitem ou não permitir acesso de porta 445, aceda demasiado[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand se é este motivo de Olá atrás de mensagem de "Erro de sistema 53" Olá, pode utilizar o ponto final do Portqry tooquery Olá TCP:445. Se o ponto final de TCP:445 Olá é apresentada como filtrado, Olá a porta TCP está bloqueada. Eis um exemplo de consulta:

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

Se a porta TCP 445 está bloqueada por uma regra ao longo do caminho de rede Olá, verá Olá seguinte saída:

  `TCP port 445 (microsoft-ds service): FILTERED`

Para obter mais informações sobre como toouse Portqry, consulte [descrição do utilitário de linha de comandos Olá Portqry.exe](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Solução para causa 2

Trabalhar com a porta de tooopen do departamento de IT 445 saída demasiado[intervalos de IP de Azure](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>Causa 3: NTLMv1 está ativado

Erro de sistema 53 ou erro de sistema 87 pode ocorrer se estiver ativada NTLMv1 comunicação no cliente Olá. File storage do Azure suporta apenas a autenticação NTLMv2. Ter NTLMv1 ativado cria um cliente menos seguras. Por conseguinte, a comunicação está bloqueada para o File storage do Azure. 

toodetermine se esta é a causa de Olá erro Olá, certifique-se de que Olá seguinte subchave de registo está definida tooa valor de 3:

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**

Para obter mais informações, consulte Olá [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) tópico no TechNet.

### <a name="solution-for-cause-3"></a>Solução para causa 3

Reverter Olá **LmCompatibilityLevel** valor toohello valor predefinido 3 na Olá seguinte subchave de registo:

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Erro 1816 "insuficiente quota é tooprocess disponíveis este comando" quando copiar tooan partilha de ficheiros do Azure

### <a name="cause"></a>Causa

Ocorre um erro 1816 quando atingir o limite superior de Olá de identificadores abertos simultâneos que são permitidos para um ficheiro num computador de olá onde a partilha de ficheiros de Olá está a ser montada.

### <a name="solution"></a>Solução

Reduza o número de Olá de identificadores abertos em simultâneo fechando alguns identificadores e, em seguida, tente novamente. Para obter mais informações, consulte [lista de verificação de armazenamento do Microsoft Azure, desempenho e escalabilidade](storage-performance-checklist.md).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>Ficheiro lento copiar tooand do File storage do Azure no Windows

Poderá ver um desempenho lento quando tenta tootransfer ficheiros toohello serviço de ficheiros do Azure.

- Se não tiver um requisito de tamanho de e/s mínimo específico, recomendamos que utilize 1 MB como Olá tamanho de e/s para um desempenho ideal.
-   Se souber tamanho final do Olá de um ficheiro que estiver a expandir com escreve e o software não tem problemas de compatibilidade quando hello seguimento unwritten no ficheiro de Olá contém zeros, em seguida, conjunto Olá tamanho do ficheiro seguinte com antecedência em vez de efetuar cada escrita uma escrita expandir.
-   Utilize o método de cópia correta de Olá:
    -   Utilize [AzCopy](storage-use-azcopy.md#file-copy) para qualquer transferência entre duas partilhas de ficheiros.
    -   Utilize [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre partilhas de ficheiros no computador local.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Considerações para Windows 8.1 ou Windows Server 2012 R2

Para clientes que estejam a executar o Windows 8.1 ou Windows Server 2012 R2, certifique-se que Olá [KB3114025](https://support.microsoft.com/help/3114025) correção está instalada. Esta correção melhora o desempenho de Olá de create e feche identificadores.

Pode executar Olá toocheck de script a seguir se tiver sido instalada a correção de Olá:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Se a correção está instalada, hello seguinte resultado é apresentado:

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> Imagens do Windows Server 2012 R2 no Azure Marketplace tem correções KB3114025 instalado por predefinição, a partir de Dezembro de 2015.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>Não existem pasta com uma letra de unidade na **meu computador**

Se mapear uma partilha de ficheiros do Azure como um administrador através de utilização de rede, a partilha de Olá aparece toobe em falta.

### <a name="cause"></a>Causa

Por predefinição, o Explorador de ficheiros do Windows não é executado como administrador. Se executar o net utilização a partir de uma linha de comandos administrativa, mapear unidade de rede Olá como administrador. Dado que as unidades mapeadas centrada no utilizador, conta de utilizador Olá, que é registada no não apresentar unidades Olá se estão montados numa conta de utilizador diferente.

### <a name="solution"></a>Solução
Monte a partilha de Olá partir de uma linha de comandos de não administrador. Em alternativa, pode seguir [neste tópico do TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure Olá **EnableLinkedConnections** valor de registo.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Comando net use falha se a conta de armazenamento de Olá contém uma barra

### <a name="cause"></a>Causa

comando de net use Olá interpreta uma barra (/) como uma opção de linha de comandos. Se o nome da sua conta de utilizador for iniciado com uma barra, o mapeamento de unidade de Olá falha.

### <a name="solution"></a>Solução

Pode utilizar qualquer um dos Olá passos toowork em torno do problema Olá os seguintes:

- Execute o seguinte comando do PowerShell de Olá:

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  De um ficheiro batch, pode executar o comando de Olá desta forma:

  `Echo new-smbMapping ... | powershell -command –`

- Colocar carateres de aspas à volta de Olá toowork chave em torno este problema – a menos que a barra de Olá é o primeiro caráter de Olá. Se estiver, utilize o modo interativo Olá e introduza a palavra-passe em separado ou voltar a gerar a chaves tooget uma chave que não iniciar com uma barra.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>Aplicação ou serviço não é possível aceder a uma unidade de armazenamento de ficheiros do Azure montada

### <a name="cause"></a>Causa

Unidades estão montadas por utilizador. Se a aplicação ou serviço está em execução com uma conta de utilizador diferente Olá que montar a unidade de Olá, aplicação Olá não verão a unidade de Olá.

### <a name="solution"></a>Solução

Utilize uma das seguintes soluções de Olá:

-   Montar a unidade de Olá partir Olá mesma conta de utilizador que contém a aplicação Olá. Pode utilizar uma ferramenta como o PsExec.
- Transmita o nome de conta do storage Olá e a chave Olá utilizador nome e palavra-passe parâmetros do comando de net use Olá.

Depois de seguir estas instruções, poderá receber Olá seguir a mensagem de erro quando executa net utilização para a conta de serviço de sistema/rede Olá: "erro de sistema 1312 foi excedido. Uma sessão de início de sessão especificado não existe. -Pode já ter foi terminada." Se isto ocorrer, certifique-se de que nome de utilizador Olá que é transmitido a utilização de toonet inclui informações de domínio (por exemplo: "[nome da conta de armazenamento]. file.core.windows .net").

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>Erro "Está a copiar um destino de tooa de ficheiro que não suporta encriptação"

Quando um ficheiro é copiado através de rede de Olá, ficheiro Olá é desencriptado no computador de origem Olá, transmitidas em texto não encriptado e encriptados novamente no destino Olá. No entanto, poderá ver Olá os seguintes erros quando está a tentar toocopy um ficheiro encriptado: "Está a copiar Olá tooa o destino de ficheiro que não suporta encriptação."

### <a name="cause"></a>Causa
Este problema pode ocorrer se estiver a utilizar o sistema de encriptação de ficheiros (EFS). Ficheiros encriptados por BitLocker podem ser copiados tooAzure o File storage. No entanto, o File storage do Azure não suporta NTFS EFS.

### <a name="workaround"></a>Solução
toocopy um ficheiro através de rede de Olá, primeiro tem de desencriptá-lo. Utilize um dos seguintes métodos de Olá:

- Olá utilize **copiar /d** comando. Permite que Olá encriptado ficheiros toobe guardado como ficheiros desencriptados no destino Olá.
- Definir Olá seguinte chave de registo:
  - Caminho = HKLM\Software\Policies\Microsoft\Windows\System
  - Tipo de valor = DWORD
  - Nome = CopyFileAllowDecryptedRemoteDestination
  - Valor = 1

Lembre-se de que essa chave de registo de Olá definição afeta todas as operações de cópia que são efetuadas toonetwork partilhas.

## <a name="need-help-contact-support"></a>Precisa de ajuda? Contacte o suporte.
Se ainda precisar de ajuda, [contacte o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
