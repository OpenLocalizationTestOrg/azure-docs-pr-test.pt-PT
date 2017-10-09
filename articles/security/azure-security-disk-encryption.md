---
title: "aaaAzure encriptação de disco para o Windows e as VMs de IaaS Linux | Microsoft Docs"
description: "Este artigo fornece uma descrição geral do Microsoft Azure disco encriptação para o Windows e as VMs de IaaS Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Encriptação de disco do Azure para o Windows e as VMs de Linux IaaS
Microsoft Azure é vivamente consolidada tooensuring sua privacidade de dados, soberania de dados e permite-lhe toocontrol seu Azure alojadas dados através de uma variedade de tecnologias avançadas tooencrypt, controlar e gerir chaves de encriptação, controlo & auditar o acesso aos dados. Isto proporciona aos clientes do Azure Olá flexibilidade toochoose Olá solução que melhor se adeque às suas necessidades de negócio. Neste documento, vamos apresenta-lhe tooa nova tecnologia solução "Encriptação de disco do Azure para o Windows e da VM do IaaS Linux" toohelp proteger e salvaguardar o dados toomeet os compromissos de segurança e conformidade organizacionais. documento de Olá fornece orientação detalhada no como toouse Olá disco Azure encriptação funcionalidades, incluindo Olá cenários e suportados Olá experiências de utilizador.

> [!NOTE]
> Algumas recomendações podem aumentar dados, a rede ou a utilização de recursos de computação, resultando em custos de licenciamento ou de subscrição adicionais.

## <a name="overview"></a>Descrição geral
Encriptação de disco do Azure é uma nova capacidade que ajuda-o a encriptar os discos da máquina virtual do Windows e Linux IaaS. Tira partido do Azure Disk Encryption padrão da indústria de Olá [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funcionalidade do Windows e Olá [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funcionalidade de encriptação de volume do Linux tooprovide para Olá SO e discos de dados de Olá. solução Olá está integrada [Cofre de chaves do Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp controlar e gerir chaves de encriptação de disco Olá e segredos na sua subscrição do Cofre de chaves. solução Olá também garante que todos os dados nos discos da máquina virtual de Olá sejam encriptados Inativos no armazenamento do Azure.

Encriptação de disco do Azure para o Windows e as VMs de IaaS Linux está agora em **disponibilidade geral** em todas as regiões públicas do Azure e regiões de AzureGov para VMs padrão e VMs com o armazenamento premium.

### <a name="encryption-scenarios"></a>Cenários de encriptação
Olá solução da Azure Disk Encryption suporta Olá os seguintes cenários de cliente:

* Ativar a encriptação em novas VMs de IaaS criados a partir de VHD previamente encriptado e chaves de encriptação
* Ativar a encriptação em novas VMs de IaaS criados a partir de imagens de galeria do Azure Olá suportado
* Ativar a encriptação em VMs de IaaS existentes em execução no Azure
* Desativar a encriptação em VMs de IaaS Windows
* Desativar a encriptação em unidades de dados para as VMs de IaaS Linux
* Ativar a encriptação de disco gerido VMs
* Atualizar as definições de encriptação de um armazenamento de premium não encriptado VM existente
* Cópia de segurança e restauro de VMs encriptados, encriptada com a chave de encriptação de chaves

solução Olá suporta Olá os seguintes cenários para VMs de IaaS quando são ativados no Microsoft Azure:

* Integração com o Cofre de chaves do Azure
* O escalão Standard VMs: [A, D, DS, G, GS, F e série Sim forth VMs do IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Ativar a encriptação no Windows e Linux VMs de IaaS e as VMs de disco gerido de Olá suportada imagens de galeria do Azure
* Desativar a encriptação em unidades de dados e SO Windows VMs de IaaS e as VMs de disco gerido
* Desativar a encriptação em unidades de dados para VMs de disco gerido e as VMs de IaaS Linux
* Ativar a encriptação em VMs do IaaS SO de cliente do Windows em execução
* Ativar a encriptação em volumes com caminhos de montagem
* Ativar a encriptação em VMs do Linux configurado com o disco striping (RAID) utilizando mdadm
* Ativar a encriptação em VMs do Linux utilizando LVM para discos de dados
* Ativar a encriptação em VMs do Windows configurado com espaços de armazenamento
* Atualizar as definições de encriptação de um armazenamento de premium não encriptado VM existente
* Todos os público do Azure e AzureGov regiões são suportadas

solução Olá não suporta os seguintes cenários, funcionalidades e tecnologias de Olá:

* Escalão básico VMs do IaaS
* A desativação da encriptação numa unidade do SO para as VMs de IaaS Linux
* A desativação da encriptação numa unidade de dados se Olá disco do SO é encriptado para as VMs de Iaas Linux
* VMs de IaaS que são criados utilizando o método de criação de VM Olá clássico
* Ative a encriptação em Windows e as VMs de Linux IaaS imagens personalizadas do cliente não é suportada. Ativar enccryption com SO Linux LVM disco não é suportado atualmente. Este suporte ficará em breve.
* Integração com o serviço de gestão de chaves no local
* Ficheiros do Azure (sistema de ficheiros partilhados), o sistema de ficheiros de rede (NFS), volumes dinâmicos e VMs do Windows que estão configurados com sistemas RAID baseados em software
* Cópia de segurança e restauro de VMs encriptados, encriptados sem chave de encriptação de chaves.
* Atualize as definições de encriptação de uma VM do encriptados premium storage existente.

> [!NOTE]
> Cópia de segurança e restauro de VMs encriptadas só é suportada para VMs que estão encriptadas com a configuração de KEK Olá. Não é suportada em VMs que são encriptadas sem KEK. KEK é um parâmetro opcional que ativa a encriptação de VM. Este suporte está disponível em breve.
> Atualize as definições de encriptação de um armazenamento premium encriptado existente VM não são suportadas. Este suporte está disponível em breve.

### <a name="encryption-features"></a>Funcionalidades de encriptação
Ao ativar e implementar o Azure Disk Encryption para VMs IaaS do Azure, hello seguintes funcionalidades estão ativadas, consoante a configuração de Olá fornecida:

* Encriptação de volume de arranque do Olá SO volume tooprotect Olá Inativos no armazenamento do
* Encriptação de dados volumes tooprotect Olá os volumes de dados Inativos no armazenamento do
* A desativação da encriptação Olá SO e dados unidades para as VMs de IaaS Windows
* A desativação da encriptação de dados Olá unidades para as VMs de IaaS Linux (apenas se o SO unidade é não encriptadas)
* Proteger as chaves de encriptação de Olá e segredos na sua subscrição do Cofre de chaves
* Relatório de estado de encriptação de Olá de Olá encriptados VM do IaaS
* Remoção das definições de configuração de encriptação de disco da máquina de virtual IaaS Olá
* Cópia de segurança e restauro de VMs encriptadas utilizando o serviço de cópia de segurança do Azure Olá

> [!NOTE]
> Cópia de segurança e restauro de VMs encriptadas só é suportada para VMs que estão encriptadas com a configuração de KEK Olá. Não é suportada em VMs que são encriptadas sem KEK. KEK é um parâmetro opcional que ativa a encriptação de VM.

Encriptação de disco do Azure para as VMS de IaaS para Windows e Linux solução inclui:

* extensão de encriptação de disco de Olá para Windows.
* extensão de encriptação de disco de Olá para Linux.
* Olá, os cmdlets do PowerShell de encriptação de disco.
* Olá cmdlets de interface de linha de comandos do Azure (CLI) de encriptação de disco.
* Olá modelos do Azure Resource Manager de encriptação de disco.

Olá solução da Azure Disk Encryption é suportada em VMs de IaaS que estão a executar SO Windows ou Linux. Para obter mais informações sobre os sistemas de operativos Olá suportado, consulte Olá "pré-requisitos" secção.

> [!NOTE]
> Não há sem encargos adicionais para encriptar os discos da VM com o Azure Disk Encryption.

### <a name="value-proposition"></a>Proposta de valor
Quando aplica solução Olá encriptação-gestão de discos do Azure, pode satisfazer Olá seguintes necessidades comerciais:

* VMs de IaaS são protegidas inativos, dado que pode utilizar a encriptação de norma da indústria tecnologia tooaddress segurança e conformidade requisitos organizacionais.
* Arranque de VMs de IaaS em chaves controlado de cliente e as políticas e pode auditar a respetiva utilização no seu Cofre de chaves.

### <a name="encryption-workflow"></a>Fluxo de trabalho de encriptação
encriptação de disco tooenable para o Windows e VMs do Linux, Olá seguintes:

1. Escolha um cenário de encriptação entre Olá anterior a cenários de encriptação.
2. Optar ativamente por participar na encriptação de disco tooenabling através do modelo de encriptação de disco do Azure Resource Manager Olá, os cmdlets do PowerShell ou comando da CLI e especificar a configuração de encriptação de Olá.

   * Para o cenário encriptados de cliente do VHD Olá, carregue Olá encriptado VHD tooyour conta de armazenamento e o Cofre de chaves de tooyour materiais chave de encriptação de Olá. Em seguida, fornece encriptação tooenable configuração por Olá sobre uma nova VM do IaaS.
   * Para novas VMs que são criadas a partir Olá Marketplace e VMs existentes que já estão em execução no Azure, fornece encriptação tooenable configuração por Olá no Olá VM do IaaS.

3. Conceda acesso toohello plataforma Azure tooread Olá chave de encriptação material (chaves de encriptação BitLocker para sistemas Windows) e o frase de acesso para Linux da encriptação de tooenable seu Cofre de chaves no Olá VM do IaaS.

4. Fornece Olá Azure Active Directory (Azure AD) aplicação identidade toowrite Olá encriptação chave tooyour materiais Cofre de chaves. Se o fizer, permite que a encriptação em Olá VM do IaaS para cenários de Olá mencionado no passo 2.

5. Azure atualiza o modelo de serviço VM Olá com a encriptação e a configuração do Cofre de chaves de Olá e configura o VM encriptado.

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Fluxo de trabalho de desencriptação
encriptação de disco toodisable para VMs de IaaS, Olá concluir os seguintes passos de alto nível:

1. Escolha toodisable encriptação (desencriptação) numa VM IaaS em execução no Azure através do modelo de encriptação de disco do Azure Resource Manager Olá ou os cmdlets do PowerShell e especificar a configuração de desencriptação de Olá.

 Este passo desativa a encriptação de volume de dados do SO ou Olá Olá ou ambos num Olá VM do IaaS Windows a executar. No entanto, tal como mencionado na secção anterior Olá, a desativação da encriptação de disco de SO para Linux não é suportada. passo de desencriptação de Olá só é permitido para unidades de dados em VMs do Linux, desde que o disco do SO Olá não está encriptado.
2. Atualizações do Azure Olá modelo de serviço da VM e Olá VM do IaaS está marcado como desencriptada. conteúdo Olá Olá VM já não é encriptado em pausa.

> [!NOTE]
> operação de encriptação de desativar Olá não eliminar o Cofre e Olá encriptação chave material de chaves (chaves de encriptação BitLocker para sistemas Windows) ou o frase de acesso para Linux.
 > Não é suportada a desativação da encriptação de disco de SO do Linux. passo de desencriptação de Olá só é permitido para unidades de dados em VMs do Linux.
A desativação da encriptação de disco de dados para o Linux não é suportada se Olá disco do SO estiver encriptada.

## <a name="prerequisites"></a>Pré-requisitos
Antes de ativar o Azure Disk Encryption em VMs do IaaS do Azure para cenários de Olá suportado que foram abordados na secção "Descrição geral" de Olá, consulte Olá os seguintes pré-requisitos:

* Tem de ter recursos de toocreate uma subscrição do Azure Active Directory válido no Azure em regiões Olá suportado.
* Encriptação de disco do Azure é suportada em Olá seguintes versões do Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.
* Encriptação de disco do Azure é suportada em Olá seguintes versões de cliente do Windows: Windows 8 e o cliente Windows 10.

> [!NOTE]
> Para o Windows Server 2008 R2, tem de ter o .NET Framework 4.5 instalados antes de ativar a encriptação no Azure. Pode instalá-lo do Windows Update através da instalação de atualização opcional de Olá o Microsoft .NET Framework 4.5.2 para sistemas baseados em x64 do Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).

* A encriptação de disco do Azure é suportada no Olá seguir galeria do Azure com base distribuições de servidor Linux e versões:

| Distribuição de Linux | Versão | Tipo de volume suportado para a encriptação|
| --- | --- |--- |
| Ubuntu | 16.04-DIARIAMENTE-LTS | Disco do SO e dados |
| Ubuntu | 14.04.5-DAILY-LTS | Disco do SO e dados |
| Ubuntu | 12.10 | Disco de dados |
| Ubuntu | 12.04 | Disco de dados |
| RHEL | 7.3 | Disco do SO e dados |
| RHEL | 7.2 | Disco do SO e dados |
| RHEL | 6.8 | Disco do SO e dados |
| RHEL | 6.7 | Disco de dados |
| CentOS | 7.3 | Disco do SO e dados |
| CentOS | 7.2N | Disco do SO e dados |
| CentOS | 6.8 | Disco do SO e dados |
| CentOS | 7.1 | Disco de dados |
| CentOS | 7.0 | Disco de dados |
| CentOS | 6.7 | Disco de dados |
| CentOS | 6.6 | Disco de dados |
| CentOS | 6.5 | Disco de dados |
| openSUSE | 13.2 | Disco de dados |
| SLES | 12 SP1 | Disco de dados |
| SLES | 12-SP1 (Premium) | Disco de dados |
| SLES | HPC 12 | Disco de dados |
| SLES | 11-SP4 (Premium) | Disco de dados |
| SLES | 11 SP4 | Disco de dados |

* Encriptação de disco do Azure requer que o Cofre de chaves e VMs residem em Olá mesma subscrição e região do Azure.

> [!NOTE]
> Configurar recursos de Olá em regiões separadas causa uma falha na ativação da funcionalidade de Azure Disk Encryption Olá.

* tooset até e configurar o seu Cofre de chaves do Azure Disk Encryption, consulte a secção **definir configurar e configurar o seu Cofre de chaves do Azure Disk Encryption** no Olá *pré-requisitos* secção deste artigo.
* tooset até e configurar a aplicação do Azure AD no Azure Active directory para o Azure Disk Encryption, consulte a secção **configurar aplicação Olá do Azure AD no Azure Active Directory** no Olá *pré-requisitos* secção deste artigo.
* tooset até e configurar a política de acesso do Cofre de chaves Olá para aplicação Olá do Azure AD, consulte a secção **configurar a política de acesso do Cofre de chaves Olá para aplicação Olá do Azure AD** no Olá *pré-requisitos* secção Este artigo.
* tooprepare um VHD do Windows previamente encriptado, consulte a secção **preparar um VHD do Windows previamente encriptado** no Olá *apêndice*.
* tooprepare um VHD previamente encriptado do Linux, consulte a secção **preparar um VHD de Linux previamente encriptado** no Olá *apêndice*.
* Olá plataforma Azure necessita de acesso toohello encriptação chaves ou segredos no seu Cofre de chaves toomake-los máquina de virtual toohello disponível quando se efetua o arranque e desencripta o volume de máquina virtual SO Olá. toogrant permissões tooAzure plataforma do conjunto Olá **EnabledForDiskEncryption** propriedade no Cofre de chaves Olá. Para obter mais informações, consulte **definir configurar e configurar o seu Cofre de chaves do Azure Disk Encryption** no Olá anexo.
* O segredo do Cofre de chaves e os KEK URLs tem de ser com a versão. Azure impõe esta restrição do controlo de versões. Para segredo válido e KEK URLs, consulte Olá exemplos a seguir:

  * Exemplo de um URL válido secreto: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Exemplo de um URL válido da KEK: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* Azure Disk Encryption não suporta a especificação de números de porta como parte dos segredos do Cofre de chaves e KEK URLs. Para obter exemplos de URLs do Cofre de chaves suportadas e não suportados, consulte o seguinte Olá:

  * URL do Cofre de chaves inaceitável *https://contosovault.vault.azure.net:443/segredos/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * URL do Cofre de chaves aceitável: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* funcionalidade do Azure Disk Encryption de tooenable Olá, Olá VMs de IaaS tem de cumprir os requisitos de configuração de ponto final de rede de Olá:
  * tooget um token tooconnect tooyour Cofre de chaves, Olá VM do IaaS tem de ser tooconnect capaz de ponto final do Azure Active Directory de tooan, \[login.microsoftonline.com\].
  * toowrite Olá encriptação chaves tooyour Cofre de chaves, Olá VM do IaaS tem de ser ponto final do Cofre de chaves de toohello tooconnect possível.
  * Olá VM do IaaS tem de ser capaz de tooconnect ponto final da storage do Azure de tooan que anfitriões Olá repositório de extensão do Azure e uma conta de armazenamento do Azure que anfitriões Olá ficheiros VHD.

  > [!NOTE]
  > Se a política de segurança limita o acesso a partir de VMs do Azure toohello Internet, pode resolver Olá precedente URI e configurar um toohello de conectividade de saída de tooallow de regra específica IPs.
  >
  >tooconfigure e acesso Cofre de chaves do Azure atrás de uma firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)

* Utilize a versão mais recente do Olá do SDK do Azure PowerShell versão tooconfigure Azure Disk Encryption. Transferir a versão mais recente do Olá do [Azure PowerShell versão](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Encriptação de disco do Azure não é suportada em [SDK do Azure PowerShell versão 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016). Se está a receber um erro relacionado com toousing Azure PowerShell 1.1.0, consulte [tooAzure Azure disco encriptação erro relacionados com o PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun qualquer comando da CLI do Azure e associá-lo à sua subscrição do Azure, primeiro é necessário instalar a CLI do Azure:
  * tooinstall CLI do Azure e associá-lo à sua subscrição do Azure, consulte [como tooinstall e configurar a CLI do Azure](../cli-install-nodejs.md).
  * toouse CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager, consulte [comandos da CLI do Azure no modo Resource Manager](../virtual-machines/azure-cli-arm-commands.md).

* Quando a encriptar um disco gerido, é obrigatório tootake pré-requisitos um instantâneo do disco de Olá gerido ou uma cópia de segurança de disco de Olá fora da encriptação do Azure Disk Encryption tooenabling anterior.  Sem uma cópia de segurança no local, qualquer falha inesperada durante a encriptação poderá fazer disco Olá e VM inacessível sem uma opção de recuperação.  Conjunto AzureRmVMDiskEncryptionExtension atualmente não cópia de segurança discos geridos e será erro se utilizada relativamente um disco gerido, a menos que o parâmetro - skipVmBackup de Olá foi especificado.  Este parâmetro é toouse não seguro, a menos que já foi efetuada uma cópia de segurança fora do Azure Disk Encryption.   Quando Olá - skipVmBackup parâmetro for especificado, Olá cmdlet não irá fazer uma cópia de segurança tooencryption anterior do disco Olá gerido.  Por este motivo, é considerada um toomake pré-requisitos obrigatório se uma cópia de segurança de disco gerido Olá que VM se encontra em vigor anterior tooenabling Azure Disk Encryption no caso de recuperação posterior necessária.  
> [!NOTE]
 > parâmetro de - skipVmBackup Olá nunca deve ser utilizado, a menos que um instantâneo ou uma cópia de segurança já sido efetuada fora do Azure Disk Encryption. 

* Olá solução da Azure Disk Encryption utiliza protetor de chave externo Olá BitLocker para VMs IaaS do Windows. Para o domínio associado ao VMs, não EFETUE emitir quaisquer políticas de grupo que impõem protetores TPM. Para obter informações sobre a política de grupo Olá "Permitir que o BitLocker sem um TPM compatível", consulte [referência de política de grupo do BitLocker](https://technet.microsoft.com/library/ee706521).
* Política do BitLocker em máquinas de virtuais associados a um domínio com a política de grupo personalizado tem de incluir Olá definição os seguintes: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Azure Disk Encryption irá falhar quando as definições de política de grupo personalizada para o Bitlocker são incompatíveis. Nas máquinas que não tinha Olá correto definição de política, aplicar a nova política de Olá, forçando Olá nova política tooupdate (gpupdate.exe /force) e, em seguida, reiniciar poderão ser necessária.  
* toocreate uma aplicação do Azure AD, criar um cofre de chaves, ou configurar um cofre de chaves e ativar a encriptação, consulte Olá [script do PowerShell de pré-requisitos do Azure Disk Encryption](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* os pré-requisitos de encriptação de disco tooconfigure utilizando Olá CLI do Azure, consulte [este script de Bash](https://github.com/ejarvi/ade-cli-getting-started).
* toouse Olá Azure Backup service tooback cópias de segurança e restauro encriptado VMs, quando é ativada a encriptação com o Azure Disk Encryption, encriptam as suas VMs utilizando a configuração da chave Olá Azure Disk Encryption. serviço de cópia de segurança de Olá suporta VMs que estão encriptadas com a configuração de KEK apenas. Consulte [como tooback cópias de segurança e restauro encriptados máquinas virtuais com a encriptação da cópia de segurança do Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* Encriptar um volume com SO Linux, tenha em atenção de que está atualmente necessário no final de Olá do processo de Olá de um reinício VM. Isto pode ser feito através do portal de Olá, powershell ou a CLI.   progresso de Olá tootrack de encriptação, consultar mensagem de estado de saudação devolvida pelo Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus periodicamente.  Depois de concluída a encriptação, mensagem de estado de Olá Olá devolvida por este comando irá indicar isto.  Por exemplo, "ProgressMessage: disco do SO encriptados com êxito, reinicie Olá VM" neste Olá ponto VM pode ser reiniciada e utilizada.  

* Azure Disk Encryption para Linux necessita de discos de dados toohave um sistema de ficheiros montado no tooencryption anterior do Linux

* Recursivamente discos de dados montada não são suportados pelo Olá Azure Disk Encryption para Linux. Por exemplo, se hello sistema de destino tem montado um disco em /foo/bar e, em seguida, outra no /foo/bar/baz, encriptação Olá de /foo/bar/baz será concluída com êxito, mas a encriptação de barra/foo/irá falhar. 

* Azure Disk Encryption só é suportado nas imagens de galeria do Azure suportada que cumpre os pré-requisitos acima mencionados Olá. Imagens personalizadas do cliente não são suportadas devido toocustom esquemas de partição e comportamentos de processos que possam existir nestas imagens. Além disso, mesmo Galeria baseia imagem de VM que inicialmente cumpridos pré-requisitos, mas que foram modificada após a criação poderão não ser compatíveis.  Para que motivo, Olá sugerida procedimento para encriptar uma VM com Linux é toostart a partir de uma imagem de galeria limpa, encriptar Olá VM e, em seguida, adicionar personalizadas de software ou dados toohello VM conforme necessário.  

> [!NOTE]
> Cópia de segurança e restauro de VMs encriptadas só é suportada para VMs que estão encriptadas com a configuração de KEK Olá. Não é suportada em VMs que são encriptadas sem KEK. KEK é um parâmetro opcional que permite que a VM.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Configurar Olá aplicação do Azure AD no Azure Active Directory
Quando precisar de toobe encriptação ativada numa VM em execução no Azure, Azure Disk Encryption gera e escreve Olá encriptação chaves tooyour cofre da chave. Gestão de chaves de encriptação no seu Cofre de chaves requer autenticação do Azure AD.

Para este fim, crie uma aplicação do Azure AD. Pode encontrar passos detalhados para registar uma aplicação na secção de "Obter uma identidade para Olá aplicação" Olá da mensagem de blogue Olá [Cofre de chaves do Azure - passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Esta mensagem também contém um número de exemplos útil para definir e configurar o seu Cofre de chaves. Para efeitos de autenticação, pode utilizar a autenticação baseada em segredo do cliente ou autenticação de cliente baseada em certificados do Azure AD.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Autenticação baseada em segredo do cliente para o Azure AD
as secções de Olá que se seguem podem ajudá-lo a configurar uma autenticação baseada em segredo de cliente para o Azure AD.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Criar uma aplicação do Azure AD utilizando o Azure PowerShell
Utilize Olá seguir toocreate de cmdlet do PowerShell uma aplicação do Azure AD:

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId é Olá, Azure AD ClientID e $aadClientSecret é segredo do cliente Olá que deve utilizar tooenable posterior Azure Disk Encryption. Salvaguarde adequadamente o segredo do cliente Olá do Azure AD.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Configurar o ID de cliente Olá do Azure AD e o segredo de Olá portal clássico do Azure
Pode também configurar o ID de cliente do Azure AD e o segredo utilizando Olá [portal clássico do Azure]( https://manage.windowsazure.com). tooperform esta tarefa, Olá a seguir:

1. Clique em Olá **do Active Directory** separador.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Clique em **Adicionar aplicação**e, em seguida, tipo Olá nome da aplicação.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Clique no botão de seta de Olá e, em seguida, configure as propriedades da aplicação Olá.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Clique em marca de verificação Olá no Olá inferior esquerda canto toofinish. é apresentada a página de configuração de aplicação Olá e ID de cliente do Azure AD Olá é apresentada na Olá parte inferior da página Olá.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Guardar o segredo do cliente Olá do Azure AD, clicando em Olá **guardar** botão. Tenha em atenção o segredo do cliente Olá do Azure AD na caixa de texto Olá chaves. Salvaguarde adequadamente.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Olá precedente fluxo não é suportada em Olá portal clássico do Azure.

##### <a name="use-an-existing-application"></a>Utilizar uma aplicação existente
tooexecute Olá os seguintes comandos, obtenha e utilize Olá [módulo Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Olá seguintes comandos tem de ser executados a partir de uma nova janela do PowerShell. Utilize o Azure PowerShell ou os comandos janela Olá do Azure Resource Manager tooexecute Olá. Recomendamos esta abordagem porque estes cmdlets no módulo de MSOnline Olá ou do Azure AD PowerShell.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Autenticação baseada em certificado para o Azure AD
> [!NOTE]
> Autenticação baseada em certificado. do Azure AD não é atualmente suportada em VMs do Linux.

Olá secções que se seguem mostram como tooconfigure uma autenticação baseada em certificado para o Azure AD.

##### <a name="create-an-azure-ad-application"></a>Criar uma aplicação do Azure AD
toocreate uma aplicação do Azure AD, execute Olá os seguintes cmdlets do PowerShell:

> [!NOTE]
> Substitua o seguinte Olá `yourpassword` cadeia com a sua palavra-passe segura e a palavra-passe Olá de salvaguarda.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

Depois de concluir este passo, carregar um cofre de chaves de tooyour de ficheiro PFX e ativar Olá acesso políticas necessárias toodeploy tooa esse certificado VM.

##### <a name="use-an-existing-azure-ad-application"></a>Utilizar uma aplicação do Azure AD existente
Se estiver a configurar a autenticação baseada em certificado para uma aplicação existente, utilize os cmdlets do PowerShell Olá mostrados aqui. Ser se tooexecute-las a partir de uma nova janela do PowerShell.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

Depois de concluir este passo, carregar um cofre de chaves de tooyour de ficheiro PFX e ativar política de acesso de Olá necessários toodeploy Olá certificado tooa VM.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Carregar um cofre de chaves de tooyour de ficheiro PFX
Para obter uma explicação detalhada deste processo, consulte [Olá oficial blogue de equipa do Cofre de chaves do Azure](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). No entanto, os seguintes cmdlets do PowerShell de Olá é tudo o que precisa para a tarefa de Olá. Ser se tooexecute-las a partir da consola do Azure PowerShell.

> [!NOTE]
> Substitua o seguinte Olá `yourpassword` cadeia com a sua palavra-passe segura e a palavra-passe Olá de salvaguarda.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Implemente um certificado no seu tooan do Cofre de chaves existentes VM
Depois de concluir o carregamento Olá PFX, implemente um certificado no Olá Cofre de chaves tooan existente VM com o seguinte Olá:
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Configurar a política de acesso do Cofre de chaves Olá para aplicação Olá do Azure AD
A aplicação do Azure AD tem de chaves de Olá direitos tooaccess ou segredos no Cofre de Olá. Olá utilize [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissões toohello aplicação, ID de cliente de Olá (que foi gerado quando a aplicação Olá foi registada) a utilizar como Olá _– ServicePrincipalName_ valor do parâmetro. toolearn mais, consulte a mensagem de blogue de Olá [Cofre de chaves do Azure - passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Eis um exemplo de como tooperform esta tarefa através do PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Encriptação de disco do Azure requer Olá tooconfigure seguir a aplicação de cliente de tooyour do Azure AD de políticas de acesso: _WrapKey_ e _definir_ permissões.

## <a name="terminology"></a>Terminologia
toounderstand alguns dos termos comuns Olá utilizado por esta tecnologia, Olá utilize terminologia a tabela seguinte:

| Terminologia | Definição |
| --- | --- |
| Azure AD | Azure AD [do Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Uma conta do Azure AD é um pré-requisito para autenticar, armazenar e obter segredos a partir de um cofre de chaves. |
| Azure Key Vault | O Cofre de chaves é um serviço de gestão de serviços de criptografia, chave baseada em módulos de segurança de hardware validados Federal Information Processing Standards FIPS, que ajudam a salvaguardar as chaves criptográficas e segredos confidenciais. Para obter mais informações, consulte [Cofre de chaves](https://azure.microsoft.com/services/key-vault/) documentação. |
| ARM | Azure Resource Manager |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) é uma reconhecido do setor Windows volume encriptação tecnologia que tenha utilizado a encriptação de disco tooenable em VMs de IaaS do Windows. |
| BEK | Chaves de encriptação do BitLocker são volume de arranque de Olá SO tooencrypt utilizado e os volumes de dados. chaves do BitLocker Olá são salvaguardadas no Cofre de chaves como segredos. |
| CLI | Consulte [interface de linha de comandos do Azure](../cli-install-nodejs.md). |
| DM-Crypt |[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) subsistema de encriptação de disco baseado em Linux, transparente Olá que tenha utilizado a encriptação de disco tooenable em VMs de IaaS Linux. |
| KEK | Chave de encriptação de chaves é Olá chave assimétrica (RSA 2048) que pode utilizar tooprotect ou moldar segredo Olá. Pode fornecer uma segurança de hardware (HSM) de módulos-chave ou de chave protegida por software protegidos. Para obter mais detalhes, consulte [Cofre de chaves do Azure](https://azure.microsoft.com/services/key-vault/) documentação. |
| PS cmdlets | Consulte [cmdlets Azure PowerShell](/powershell/azure/overview). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Definir e configurar o seu Cofre de chaves para o Azure Disk Encryption
Ajuda do Azure Disk Encryption chaves de encriptação de disco de Olá de salvaguarda e segredos no seu Cofre de chaves. tooset se o seu Cofre de chaves para o Azure Disk Encryption, Olá concluir os passos em cada uma das seguintes secções de Olá.

#### <a name="create-a-key-vault"></a>Criar um cofre de chaves
toocreate um cofre de chaves, utilize uma das seguintes opções de Olá:

* [Modelo de Gestor de recursos "101-chave-cofre-criar"](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Cmdlets do Cofre de chaves do Azure PowerShell](/powershell/module/azurerm.keyvault/#key_vault)
* Azure Resource Manager
* Como demasiado[proteger o seu Cofre de chaves](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Se já tiver configurado um cofre de chaves para a sua subscrição, ignore a secção seguinte toohello.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Configurar uma chave de encriptação de chaves (opcional)
Se pretender toouse um KEK para uma camada adicional de segurança de chaves de encriptação do BitLocker Olá, adicione um cofre de chaves de tooyour KEK. Olá utilize [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate uma chave de encriptação de chaves no Cofre de chaves Olá. Também pode importar um KEK da sua gestão de chaves HSM no local. Para obter mais detalhes, consulte [documentação do Cofre de chave](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

Pode adicionar Olá KEK acedendo tooAzure Resource Manager ou utilizando a interface do Cofre de chaves.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Definir permissões do Cofre de chaves
Olá plataforma Azure necessita de acesso toohello encriptação chaves ou segredos no seu Cofre de chaves toomake-los toohello disponível VM para arrancar e desencriptação de volumes de Olá. toogrant permissões toohello plataforma do Azure, conjunto Olá **EnabledForDiskEncryption** propriedade chave Olá cofre utilizando o cmdlet do PowerShell Olá Cofre de chaves:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

Também pode definir Olá **EnabledForDiskEncryption** propriedade, visitando Olá [Explorador de recursos do Azure](https://resources.azure.com).

Conforme mencionado anteriormente, tem de definir Olá **EnabledForDiskEncryption** propriedade no seu Cofre de chaves. Caso contrário, Olá implementação irá falhar.

Pode configurar políticas de acesso para a sua aplicação do Azure AD da interface do Cofre de chaves de Olá, conforme mostrado aqui:

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

No Olá **políticas de acesso avançadas** separador, certifique-se de que o seu Cofre de chaves está ativada para a Azure Disk Encryption:

![Cofre de chaves do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Cenários de implementação de encriptação de disco e as experiências de utilizador
Pode ativar vários cenários de encriptação de disco e passos de Olá podem variar de acordo com o cenário de toohello. Olá secções seguintes abrangem os cenários de Olá mais detalhadamente.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Ativar a encriptação em novas VMs de IaaS criados a partir de Olá Marketplace
Pode ativar a encriptação de disco em nova VM do IaaS Windows de Olá Marketplace no Azure utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. No modelo de Olá início rápido do Azure, clique em **implementar tooAzure**, introduza a configuração de encriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.

2. Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable encriptação numa nova VM do IaaS.

> [!NOTE]
> Este modelo cria uma nova VM do Windows encriptados que utiliza a imagem de galeria Olá Windows Server 2012.

Pode ativar a encriptação de disco num novo IaaS VM de RedHat Linux 7.2 com uma matriz de RAID 0 200 GB ao utilizar este [modelo do Resource Manager](https://aka.ms/fde-rhel). Depois de implementar a modelo Olá, verificar o estado de encriptação de VM Olá utilizando Olá `Get-AzureRmVmDiskEncryptionStatus` cmdlet, conforme descrito em [SO de encriptação de unidade numa VM com Linux em execução](#encrypting-os-drive-on-a-running-linux-vm). Quando a máquina Olá devolve um Estado de _VMRestartPending_, reinicie Olá VM.

Olá tabela seguinte lista os parâmetros de modelo do Resource Manager Olá para novas VMs do cenário de Marketplace Olá utilizando o ID de cliente do Azure AD:

| Parâmetro | Descrição |
| --- | --- |
| adminUserName | Nome de utilizador de administrador para a máquina virtual de Olá. |
| adminPassword | Administração utilizador palavra-passe para a máquina virtual de Olá. |
| newStorageAccountName | Nome do toostore de conta de armazenamento Olá SO e dados os VHDs. |
| vmSize | Tamanho do Olá VM. Atualmente, é suportada apenas padrão A, D e G série. |
| virtualNetworkName | Nome da VNet que Olá NIC de VM de Olá deverão pertencer ao. |
| subnetName | Nome da sub-rede Olá Olá VNet que Olá VM NIC deverão pertencer ao. |
| AADClientID | ID de cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos tooyour cofre da chave. |
| AADClientSecret | Segredo do cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos tooyour cofre da chave. |
| keyVaultURL | URL da chave de Olá cofre que Olá chave deve ser carregada para o BitLocker. Pode obtê-lo utilizando o cmdlet Olá `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | URL da chave de encriptação de chaves de Olá que é utilizado tooencrypt Olá gerou a chave do BitLocker (opcional). |
| keyVaultResourceGroup | Grupo de recursos do Cofre de chaves Olá. |
| vmName | Nome da Olá VM Olá a operação de encriptação é toobe efetuada numa. |

> [!NOTE]
> _KeyEncryptionKeyURL_ é um parâmetro opcional. Pode colocar a sua própria chave de encriptação dados do KEK toofurther salvaguarda Olá (segredo frase de acesso) no seu Cofre de chaves.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>Ativar a encriptação em novas VMs de IaaS criados a partir de VHD encriptados de cliente e chaves de encriptação
Neste cenário, pode ativar a encriptação utilizando o modelo do Resource Manager Olá, os cmdlets do PowerShell ou comandos da CLI. Olá secções seguintes explicam no modelo do Resource Manager maior Olá de detalhe e comandos da CLI.

Siga as instruções de Olá a partir de um nestas secções para preparar imagens previamente encriptadas, que podem ser utilizadas no Azure. Depois de criada a imagem de Olá, pode utilizar os passos de Olá no Olá seguinte secção toocreate encriptados VM do Azure.

* [Preparar um VHD do Windows previamente encriptado](#preparing-a-pre-encrypted-windows-vhd)
* [Preparar um VHD de Linux previamente encriptado](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>Utilizar o modelo do Resource Manager Olá
Pode ativar a encriptação de disco no seu VHD encriptado utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. No modelo de Olá início rápido do Azure, clique em **implementar tooAzure**, introduza a configuração de encriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.

2. Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable encriptação em Olá nova VM do IaaS.

Olá tabela seguinte lista os parâmetros de modelo do Resource Manager Olá para o VHD encriptado:

| Parâmetro | Descrição |
| --- | --- |
| newStorageAccountName | Nome do Olá de toostore de conta de armazenamento Olá encriptados VHD de SO. Esta conta de armazenamento deve já ter sido criada na Olá mesmo grupo de recursos e a mesma localização que Olá VM. |
| osVhdUri | URI de Olá SO VHD a partir da conta de armazenamento Olá. |
| osType | Tipo de produto do SO (Windows/Linux). |
| virtualNetworkName | Nome da VNet que Olá NIC de VM de Olá deverão pertencer ao. Olá nome deve já ter sido criado na Olá mesmo grupo de recursos e a mesma localização que Olá VM. |
| subnetName | Nome da sub-rede Olá no Olá VNet que Olá VM NIC deverão pertencer ao. |
| vmSize | Tamanho do Olá VM. Atualmente, é suportada apenas padrão A, D e G série. |
| keyVaultResourceID | Olá ResourceID que identifica o Cofre de chaves Olá no Gestor de recursos do Azure. Pode obtê-lo utilizando o cmdlet do PowerShell Olá `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | URL da chave de encriptação de disco de Olá que é definida no Cofre de chaves Olá. |
| keyVaultKekUrl | URL da chave de encriptação de chaves de Olá para encriptar a chave de encriptação de disco Olá gerado. |
| vmName | Nome do Olá VM do IaaS. |

#### <a name="using-powershell-cmdlets"></a>Utilizando os cmdlets do PowerShell
Pode ativar a encriptação de disco no seu VHD encriptado utilizando o cmdlet do PowerShell Olá [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>Utilizar comandos da CLI
encriptação de disco tooenable para este cenário através da utilização de comandos da CLI, Olá seguintes:

1. Definir políticas de acesso no seu Cofre de chaves:

   * Conjunto Olá **EnabledForDiskEncryption** sinalizador:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Definir permissões tooAzure AD aplicação toowrite segredos tooyour Cofre de chaves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. encriptação de tooenable numa VM existente ou em execução, tipo:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Obter o estado de encriptação:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. encriptação de tooenable numa VM nova do seu VHD encriptado, Olá utilize seguir os parâmetros com Olá `azure vm create` comando:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Ativar a encriptação em existente ou VM do IaaS Windows a executar no Azure
Neste cenário, pode ativar a encriptação utilizando o modelo do Resource Manager Olá, os cmdlets do PowerShell ou comandos da CLI. Olá secções seguintes explicam mais detalhadamente como tooenable-lo utilizando Olá modelo do Resource Manager e os comandos da CLI.

#### <a name="using-hello-resource-manager-template"></a>Utilizar o modelo do Resource Manager Olá
Pode ativar a encriptação de disco existente ou VMs do IaaS Windows em execução no Azure utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. No modelo de Olá início rápido do Azure, clique em **implementar tooAzure**, introduza a configuração de encriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.

2. Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable a encriptação em Olá existente ou VM do IaaS a ser executado.

Olá tabela seguinte apresenta uma lista de parâmetros de modelo do Resource Manager Olá para existente ou executar as VMs que utilizam um ID de cliente do Azure AD:

| Parâmetro | Descrição |
| --- | --- |
| AADClientID | ID de cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos toohello cofre da chave. |
| AADClientSecret | Segredo do cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos toohello cofre da chave. |
| keyVaultName | Nome da chave de Olá cofre que Olá chave deve ser carregada para o BitLocker. Pode obtê-lo utilizando o cmdlet Olá `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL da chave de encriptação de chaves de Olá que é utilizado tooencrypt Olá gerou a chave do BitLocker. Este parâmetro é opcional se selecionar **nokek** na lista de Olá UseExistingKek lista pendente. Se selecionar **kek** na lista de Olá pendente UseExistingKek, tem de introduzir Olá _keyEncryptionKeyURL_ valor. |
| volumeType | Tipo de volume que é efetuar a operação de encriptação de Olá na. Os valores válidos são _SO_, _dados_, e _todos os_. |
| sequenceVersion | Versão de sequência de Olá BitLocker operação. Aumentar este número de versão sempre que é efetuar uma operação de encriptação de disco no Olá mesma VM. |
| vmName | Nome da Olá VM Olá a operação de encriptação é toobe efetuada numa. |

> [!NOTE]
> _KeyEncryptionKeyURL_ é um parâmetro opcional. Pode colocar a sua própria chave de encriptação dados do KEK toofurther salvaguarda Olá (segredo de encriptação do BitLocker) no Cofre de chaves Olá.

#### <a name="using-powershell-cmdlets"></a>Utilizando os cmdlets do PowerShell
Para obter informações sobre como ativar a encriptação com o Azure Disk Encryption utilizando cmdlets do PowerShell, consulte as mensagens de blogue Olá [explorar o Azure Disk Encryption com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [explorar o Azure Disk Encryption com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>Utilizar comandos da CLI
encriptação de tooenable em existente ou VM do IaaS Windows a executar no Azure através de comandos da CLI, Olá seguintes:

1. políticas de acesso de tooset no Cofre de chaves Olá:
   * Conjunto Olá **EnabledForDiskEncryption** sinalizador:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Definir permissões tooAzure AD aplicação toowrite segredos tooyour Cofre de chaves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. encriptação de tooenable numa VM existente ou em execução:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. Estado de encriptação tooget:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. encriptação de tooenable numa VM nova do seu VHD encriptado, Olá utilize seguir os parâmetros com Olá `azure vm create` comando:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Ativar a encriptação de uma VM do Linux IaaS existente ou em execução no Azure
Pode ativar a encriptação de disco num VM do Linux IaaS existente ou em execução no Azure utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Clique em **implementar tooAzure** no modelo de Olá início rápido do Azure, introduza a configuração de encriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.

2. Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable a encriptação em Olá existente ou VM do IaaS a ser executado.

Olá, a tabela seguinte lista os parâmetros do modelo do Resource Manager para existente ou executar as VMs que utilizam um ID de cliente do Azure AD:

| Parâmetro | Descrição |
| --- | --- |
| AADClientID | ID de cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos toohello cofre da chave. |
| AADClientSecret | Segredo do cliente da aplicação Olá do Azure AD que tenha permissões toowrite segredos tooyour cofre da chave. |
| keyVaultName | Nome da chave de Olá cofre que Olá chave deve ser carregada para o BitLocker. Pode obtê-lo utilizando o cmdlet Olá `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL da chave de encriptação de chaves de Olá que é utilizado tooencrypt Olá gerou a chave do BitLocker. Este parâmetro é opcional se selecionar **nokek** na lista de Olá UseExistingKek lista pendente. Se selecionar **kek** na lista de Olá pendente UseExistingKek, tem de introduzir Olá _keyEncryptionKeyURL_ valor. |
| volumeType | Tipo de volume que é efetuar a operação de encriptação de Olá na. Os valores suportados válidos são _SO_ ou _todos os_ (para RHEL 7.2, CentOS 7.2 e Ubuntu 16.04), e _dados_ (para todos os outras distribuições). |
| sequenceVersion | Versão de sequência de Olá BitLocker operação. Aumentar este número de versão sempre que é efetuar uma operação de encriptação de disco no Olá mesma VM. |
| vmName | Nome da Olá VM Olá a operação de encriptação é toobe efetuada numa. |
| frase de acesso | Escreva uma frase de acesso forte como chave de encriptação de dados de Olá. |

> [!NOTE]
> _KeyEncryptionKeyURL_ é um parâmetro opcional. Pode colocar a sua própria chave de encriptação dados do KEK toofurther salvaguarda Olá (segredo frase de acesso) no seu Cofre de chaves.

#### <a name="cli-commands"></a>Comandos da CLI
Pode ativar a encriptação de disco no seu VHD encriptado através da instalação e utilização Olá [comando da CLI](../cli-install-nodejs.md). encriptação de tooenable em existente ou VMs do IaaS Linux em execução no Azure através da utilização de comandos da CLI, Olá seguintes:

1. Definir políticas de acesso no Cofre de chaves Olá:

 * Conjunto Olá **EnabledForDiskEncryption** sinalizador:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * Definir permissões tooAzure AD aplicação toowrite segredos tooyour Cofre de chaves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. encriptação de tooenable numa VM existente ou em execução:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Obter o estado de encriptação:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. encriptação de tooenable numa VM nova do seu VHD encriptado, Olá utilize seguir os parâmetros com Olá `azure vm create` comando:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Obter o estado de encriptação de Olá de uma VM do IaaS encriptados
Pode obter o estado de encriptação de Olá utilizando o Gestor de recursos do Azure, [cmdlets do PowerShell](/powershell/azure/overview), ou comandos da CLI. Olá secções a seguir explica como toouse Olá portal clássico do Azure e tooget de comandos da CLI Olá estado de encriptação.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Obter o estado de encriptação de Olá de uma VM do Windows encriptada utilizando o Gestor de recursos do Azure
Pode obter estado de encriptação de Olá de Olá VM do IaaS do Azure Resource Manager, Olá seguinte:

1. Inicie sessão no toohello [portal clássico do Azure](https://portal.azure.com/)e, em seguida, clique em **máquinas virtuais** no painel esquerdo de Olá toosee uma vista de resumo de máquinas de virtuais Olá na sua subscrição. Pode filtrar a vista de máquinas virtuais de Olá, selecionando o nome da subscrição Olá na Olá **subscrição** na lista pendente.

2. Na parte superior de Olá de Olá **máquinas virtuais** página, clique em **colunas**.

3. No Olá **escolha coluna** painel, selecione **encriptação de disco**e, em seguida, clique em **atualização**. Deverá ver o estado de encriptação de Olá coluna Mostrar Olá encriptação de disco _ativado_ ou _não ativada_ para cada VM, conforme mostrado no Olá figura a seguir:

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Obter o estado de encriptação de Olá de uma VM do IaaS (Windows/Linux) encriptada utilizando o cmdlet do PowerShell de encriptação de disco de Olá
Pode obter o estado de encriptação de Olá de Olá VM do IaaS do cmdlet do PowerShell de encriptação de disco de Olá `Get-AzureRmVMDiskEncryptionStatus`. definições de encriptação de Olá tooget para a VM, introduza o seguinte Olá:

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

Pode inspecionar resultado Olá _Get-AzureRmVMDiskEncryptionStatus_ URLs da chave de encriptação.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Olá OSVolumeEncrypted e valores de definições de DataVolumesEncrypted estão definidos too_Encrypted_, que mostra que ambos os volumes são encriptados utilizando a Azure Disk Encryption. Para obter informações sobre como ativar a encriptação com o Azure Disk Encryption utilizando cmdlets do PowerShell, consulte as mensagens de blogue Olá [explorar o Azure Disk Encryption com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [explorar o Azure Disk Encryption com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> Em VMs do Linux, três toofour de demora minutos Olá `Get-AzureRmVMDiskEncryptionStatus` estado de encriptação do cmdlet tooreport Olá.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Obter o estado de encriptação de Olá de Olá VM do IaaS do comando de CLI de encriptação de disco Olá
Pode obter o estado de encriptação de Olá de Olá VM do IaaS utilizando o comando CLI de encriptação de disco Olá `azure vm show-disk-encryption-status`. definições de encriptação de Olá tooget para a VM, introduza a sua sessão do CLI do Azure:

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Desativar a encriptação sobre a execução de VM do IaaS Windows
Pode desativar a encriptação num Windows em execução ou VM do IaaS Linux através do modelo de encriptação de disco do Azure Resource Manager Olá ou os cmdlets do PowerShell e especificar a configuração de desencriptação de Olá.

##### <a name="windows-vm"></a>VM do Windows
passo de encriptação de desativar Olá desativa a encriptação de Olá SO, volume de dados de Olá ou ambos num Olá VM do IaaS Windows a executar. Não é possível desativar o volume de SO Olá e deixe o volume de dados de Olá encriptado. Quando for executado o passo de encriptação de desativar Olá, modelo de VM Olá do serviço de atualizações do modelo de implementação clássico do Azure Olá e Olá VM do IaaS Windows está marcado como desencriptada. conteúdo Olá Olá VM já não é encriptado em pausa. desencriptação de Olá não eliminar o Cofre e Olá encriptação chave material de chaves (chaves de encriptação BitLocker para Windows e o frase de acesso para Linux).

##### <a name="linux-vm"></a>VM com Linux
passo de encriptação de desativar Olá desativa a encriptação de volume de dados de Olá no Olá VM do IaaS Linux a executar. Este passo só funciona se o disco do SO Olá não estiver encriptado.

> [!NOTE]
> A desativação da encriptação no disco do SO Olá não é permitida em VMs do Linux.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Desativar a encriptação de uma VM do IaaS existente ou em execução
Pode desativar a encriptação de disco em execução VMs de IaaS do Windows utilizando Olá [modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. No modelo de Olá início rápido do Azure, clique em **implementar tooAzure**, introduza a configuração de desencriptação de Olá no Olá **parâmetros** painel e, em seguida, clique em **OK**.

2. Selecione a subscrição Olá, grupo de recursos, localização do grupo de recursos, termos legais e contrato e, em seguida, clique em **criar** tooenable encriptação numa nova VM do IaaS.

Para VMs com Linux, pode desativar a encriptação utilizando Olá [desativar a encriptação de uma VM com Linux em execução](https://aka.ms/decrypt-linuxvm) modelo.

Olá tabela seguinte lista os parâmetros do modelo do Resource Manager para desativar a encriptação de uma VM do IaaS em execução:

| Parâmetro | Descrição |
| --- | --- |
| vmName | Nome da Olá VM Olá a operação de encriptação é toobe efetuada numa.
| volumeType | Tipo de volume que é efetuar uma operação de desencriptação no. Os valores válidos são _SO_, _dados_, e _todos os_. Não é possível desativar a encriptação em com o volume de VM do IaaS Windows SO/arranque sem desativar a encriptação em Olá _dados_ volume. Note também que a desativação da encriptação no disco do SO Olá não é permitida em VMs do Linux. |
| sequenceVersion | Versão de sequência de Olá BitLocker operação. Aumentar este número de versão sempre que uma operação de desencriptação de disco for executada num Olá mesma VM. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Desativar a encriptação de uma VM do IaaS existente ou em execução
encriptação de toodisable numa IaaS VM em execução ou existente utilizando o cmdlet do PowerShell Olá, consulte [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). Este cmdlet suporta o Windows e VMs com Linux. encriptação de toodisable, instala uma extensão na máquina virtual de Olá. Se hello _nome_ parâmetro não for especificado, uma extensão com o nome predefinido de Olá _AzureDiskEncryption para VMs do Windows_ é criado.

Em VMs do Linux, Olá AzureDiskEncryptionForLinux extensão é utilizado.

> [!NOTE]
> Este cmdlet é reiniciado Olá máquina.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Ativar a encriptação em VM do IaaS previamente encriptado com o disco gerida do Azure
Utilizar Olá ARM do Azure gerida disco modelo toocreate uma VM encriptada a partir de um VHD previamente encriptado utilizando o modelo ARM Olá localizada em   
[Criar um novo disco gerido encriptado a partir de um blob VHD/armazenamento previamente encriptado] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Ativar a encriptação numa nova VM do IaaS Linux com o disco gerida do Azure
Utilizar toocreate de modelo de ARM do Azure gerida disco Olá que um novo encriptados VM do IaaS Linux utilizando o modelo ARM Olá localizado em   
[Implementação do RHEL 7.2 com a encriptação de disco completo] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Ativar a encriptação numa nova VM do IaaS do Windows com o disco gerida do Azure
 Utilizar toocreate de modelo de ARM do Azure gerida disco Olá que um novo encriptados VM do IaaS Linux utilizando o modelo ARM Olá localizado em   
 [Criar um novo encriptados IaaS geridos disco VM do Windows da imagem de galeria] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >É obrigatório toosnapshot e/ou a cópia de segurança um geridos com base em disco instância VM fora do e tooenabling anterior Azure Disk Encryption.  Pode ser obtido um instantâneo de disco gerido Olá do portal de Olá, ou cópia de segurança do Azure pode ser utilizada.  As cópias de segurança garantir que uma opção de recuperação em caso de Olá de qualquer falha inesperada durante a encriptação.  Assim que for efetuada uma cópia de segurança, Olá conjunto AzureRmVMDiskEncryptionExtension cmdlet pode ser utilizado tooencrypt gerido discos especificando Olá - skipVmBackup parâmetro.  Este comando irá falhar contra uma VM baseada em disco de gerido até que foi efetuada uma cópia de segurança e se este parâmetro foi especificado.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Atualizar as definições de encriptação de uma VM do premium não encriptada existente
  Utilize Olá existentes disco Azure encriptação suportada interfaces para executar a VM [cmdlets de PS, CLI ou ARM modelos] tooupdate definições de encriptação de Olá como o cliente do AAD ID/segredo, chave de encriptação da chave [KEK], chave de encriptação do BitLocker para a VM do Windows ou o frase de acesso para Definição de encriptação do etc. de VM Linux Olá atualização só é suportada para VMs por armazenamento premium não. É NNOT suportada para VMs por armazenamento premium.

## <a name="appendix"></a>Apêndice
### <a name="connect-tooyour-subscription"></a>Ligar tooyour subscrição
Antes de continuar, reveja Olá *pré-requisitos* secção deste artigo. Depois de assegurar que todos os pré-requisitos tiverem sido cumpridos, ligar tooyour subscrição, Olá seguinte:

1. Iniciar uma sessão do PowerShell do Azure e inicie sessão no tooyour conta do Azure com Olá os seguintes comandos:

    `Login-AzureRmAccount`

2. Se tiver várias subscrições e pretender um toouse toospecify, escreva Olá subscrições de Olá toosee da sua conta os seguintes:

    `Get-AzureRmSubscription`

3. subscrição de Olá toospecify pretende toouse, tipo:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. tooverify que subscrição Olá configurada está correta, escreva:

    `Get-AzureRmSubscription`

5. Olá tooconfirm Azure Disk Encryption os cmdlets estão instalados, tipo:

    `Get-command *diskencryption*`

6. Olá seguinte resultado confirma que a instalação do Azure PowerShell de encriptação de disco de Olá:

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Preparar um VHD do Windows previamente encriptado
as secções de Olá que se seguem são necessária tooprepare um VHD do Windows previamente encriptado para a implementação de um VHD encriptado no IaaS do Azure. Utilize Olá informações tooprepare e efetuar o arranque de uma nova VM (VHD do Windows) no Azure Site Recovery ou do Azure.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Atualizar grupo política tooallow TPM não para a proteção de SO
Configurar a definição de política de grupo do BitLocker de Olá **encriptação de unidade BitLocker**, que encontrará em **política de computador Local** > **configuração do computador**  >  **Modelos administrativos** > **componentes do Windows**. Alterar esta definição demasiado**unidades do sistema operativo** > **requer autenticação adicional durante o arranque** > **permitir BitLocker sem um TPM compatível**, conforme apresentado na Olá figura a seguir:

![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>Instalar componentes de funcionalidades do BitLocker
Para o Windows Server 2012 ou posterior, utilize Olá os seguintes comandos:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Para o Windows Server 2008 R2, utilize Olá os seguintes comandos:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Preparar o volume de SO Olá para o BitLocker utilizando`bdehdcfg`
toocompress Olá partição de SO e preparar máquina Olá para o BitLocker, executar Olá os seguintes comandos:

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>Proteger o volume de SO Olá ao utilizar o BitLocker
Olá utilize [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) encriptação tooenable de comando no volume de arranque de Olá com um protetor de chave externo. Também colocar chave externa de Olá (ficheiro .bek) numa unidade externa Olá ou volume. Encriptação está ativada num volume de arranque do sistema de Olá após o reinício seguinte Olá.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> Prepare Olá VM com um separado/recurso de dados VHD para obter a chave externa Olá utilizando o BitLocker.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Encriptar uma unidade de SO numa VM com Linux em execução
Encriptação de uma unidade de SO numa VM com Linux em execução é suportada no Olá distribuições os seguintes:

* RHEL 7.2
* CentOS 7.2
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>Pré-requisitos para encriptação de disco do SO

* Olá VM tem de ser criada de imagem do Marketplace Olá no Gestor de recursos do Azure.
* VM do Azure com, pelo menos, 4 GB de RAM (recomendado é de tamanho 7 GB).
* (Para RHEL e CentOS) Desative SELinux. toodisable SELinux, consulte "4.4.2 criação. Desativar o SELinux"Olá [Guia do administrador e utilizador SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) no Olá VM.
* Depois de desativar SELinux, reiniciar o computador Olá VM, pelo menos, uma vez.

##### <a name="steps"></a>Passos
1. Crie uma VM ao utilizar uma das distribuições de Olá especificadas anteriormente.

 A CentOS 7.2, a encriptação de disco do SO é suportada através de uma imagem especial. toouse esta imagem, especifique "7.2n" como Olá SKU quando criar Olá VM:
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Configure Olá VM de acordo com tooyour às necessidades. Se pretender tooencrypt todas as unidades de Olá (SO + dados), unidades de dados de Olá necessário toobe mountable de /etc/fstab e especificados.

 > [!NOTE]
 > Utilize o UUID =... toospecify unidades de dados no etc/fstab em vez de especificar o nome do dispositivo Olá blocos (por exemplo, /dev/sdb1). Durante a encriptação, a ordem de Olá de unidades de alterações num Olá VM. Se a VM depende de uma ordem específica de impedir que os dispositivos, ocorrerá uma falha toomount-las após a encriptação.

3. Terminar sessões SSH Olá.

4. Olá tooencrypt SO, especifique volumeType como **todos os** ou **SO** quando que [ativar a encriptação](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Todos os processos de espaço do utilizador que não estão em execução como `systemd` serviços devem ser desativados com um `SIGKILL`. Reinicie Olá VM. Quando ativar a encriptação de disco de SO numa VM em execução, planeie no período de indisponibilidade VM.

5. Periodicamente monitorizar o progresso de Olá de encriptação, utilizando instruções Olá no Olá [secção seguinte](#monitoring-os-encryption-progress).

6. Depois de Get-AzureRmVmDiskEncryptionStatus mostra "VMRestartPending", reinicie a VM ao iniciar sessão tooit ou utilizando o portal de Olá, PowerShell ou a CLI.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
Antes de reiniciar, recomendamos que guarde [diagnóstico de arranque](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) de Olá VM.

#### <a name="monitoring-os-encryption-progress"></a>Monitorizar o progresso de encriptação do SO
Pode monitorizar o progresso de encriptação de SO de três formas diferentes:

* Olá utilize `Get-AzureRmVmDiskEncryptionStatus` cmdlet e inspecionar o campo de ProgressMessage Olá:
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 Depois de Olá VM atinge "Foi iniciada de encriptação de disco de SO", que demora cerca de 40 minutos too50 num armazenamento Premium-cópia de VM.

 Porque [emitir #388](https://github.com/Azure/WALinuxAgent/issues/388) no WALinuxAgent, `OsVolumeEncrypted` e `DataVolumesEncrypted` apresentados como `Unknown` em algumas distribuições. Com WALinuxAgent versão 2.1.5 e posterior, este problema é resolvido automaticamente. Se vir `Unknown` no resultado de Olá, pode verificar o estado de encriptação de disco utilizando Olá Explorador de recursos do Azure.

 Aceda demasiado[Explorador de recursos do Azure](https://resources.azure.com/)e, em seguida, expanda esta hierarquia no painel de seleção de Olá esquerda:

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 No Olá InstanceView, desloque para baixo do Estado de encriptação de Olá toosee das suas unidades.

 ![Vista de instância VM](./media/azure-security-disk-encryption/vm-instanceview.png)

* Observe [diagnóstico de arranque](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). Mensagens de Olá extensão ADE devem ter o prefixo `[AzureDiskEncryption]`.

* Inicie sessão toohello VM através de SSH e obter o registo de extensão de Olá de:

    /var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 Recomendamos que não iniciar sessão toohello VM enquanto encriptação do SO estiver em curso. Copie registos de Olá apenas quando hello outros dois métodos falharem.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Preparar um VHD de Linux previamente encriptado
##### <a name="ubuntu-16"></a>Ubuntu 16
Configure a encriptação durante a instalação de distribuição Olá, Olá seguinte:

1. Selecione **configurar volumes encriptados** quando de partição discos Olá.

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Crie uma unidade de arranque separado, que não pode ser encriptada. Encriptar a unidade de raiz.

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Forneça uma frase de acesso. Este é o frase de acesso de Olá que carregar toohello Cofre de chaves.

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Conclua a criação de partições.

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Quando efetuar o arranque Olá VM e são pedidas a uma frase de acesso, utilize o frase de acesso de Olá fornecido no passo 3.

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Preparar Olá VM para carregar no Azure com [estas instruções](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). Ainda não executada último passo do Olá (Olá desaprovisionamento VM).

Configure toowork de encriptação com o Azure, Olá seguinte:

1. Crie um ficheiro em /usr/local/sbin/azure_crypt_key.sh, com conteúdo Olá Olá script a seguir. Preste atenção toohello KeyFileName, porque é o nome de ficheiro Olá frase de acesso utilizada pelo Azure.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Alterar a configuração de crypt Olá no *etc/crypttab*. Deve ter o seguinte aspeto:
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Se estiver a editar *azure_crypt_key.sh* no Windows e é copiada-tooLinux, execute `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Adicione o script de toohello permissões executável:
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Editar */etc/initramfs-tools/modules* acrescentando linhas:
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Executar `update-initramfs -u -k all` Olá do tooupdate Olá initramfs toomake `keyscript` entrem em vigor.

7. Agora pode desaprovisionar Olá VM.

 ![Ubuntu 16.04 programa de configuração](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Continuar passo seguinte toohello e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.

##### <a name="opensuse-132"></a>openSUSE 13.2
encriptação de tooconfigure durante a instalação de distribuição de Olá, Olá seguintes:
1. Quando particionar discos Olá, selecione **encriptar o grupo de Volume**e, em seguida, introduza uma palavra-passe. Esta é a palavra-passe de Olá que irá carregar tooyour Cofre de chaves.

 ![o programa de configuração openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Arranque Olá VM utilizando a palavra-passe.

 ![o programa de configuração openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Preparar hello VM para carregar tooAzure ao seguir as instruções Olá [preparar uma máquina virtual SLES ou openSUSE para o Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). Ainda não executada último passo do Olá (Olá desaprovisionamento VM).

tooconfigure toowork de encriptação com o Azure, Olá seguintes:
1. Editar Olá /etc/dracut.conf e adicionar Olá seguinte linha:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Comente estas linhas pela extremidade de Olá da Olá /usr/lib/dracut/modules.d/90crypt/module-setup.sh do ficheiro:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Acrescente Olá linha no início Olá Olá ficheiro /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh os seguintes:
 ```
    DRACUT_SYSTEMD=0
 ```
E altere todas as ocorrências de:
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
para:
```
    if [ 1 ]; then
```
4. Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e o acrescentem demasiado "device de abrir LUKS #":

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Executar `/usr/sbin/dracut -f -v` tooupdate Olá initrd.

6. Agora pode desaprovisionar Olá VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.

##### <a name="centos-7"></a>CentOS 7
encriptação de tooconfigure durante a instalação de distribuição de Olá, Olá seguintes:
1. Selecione **encriptar os meus dados** quando de partição de discos.

 ![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Certifique-se **encriptar** está selecionado para a partição de raiz.

 ![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Forneça uma frase de acesso. Este é o frase de acesso de Olá que irá carregar tooyour Cofre de chaves.

 ![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Quando efetuar o arranque Olá VM e são pedidas a uma frase de acesso, utilize o frase de acesso de Olá fornecido no passo 3.

 ![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Preparar Olá VM para carregar no Azure, utilizando instruções "CentOS 7.0 +" Olá [preparar uma máquina de virtual com base em CentOS para o Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). Ainda não executada último passo do Olá (Olá desaprovisionamento VM).

6. Agora pode desaprovisionar Olá VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.

tooconfigure toowork de encriptação com o Azure, Olá seguintes:

1. Editar Olá /etc/dracut.conf e adicionar Olá seguinte linha:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Comente estas linhas pela extremidade de Olá da Olá /usr/lib/dracut/modules.d/90crypt/module-setup.sh do ficheiro:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Acrescente Olá linha no início Olá Olá ficheiro /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh os seguintes:
```
    DRACUT_SYSTEMD=0
```
E altere todas as ocorrências de:
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
para
```
    if [ 1 ]; then
```
4. Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e de acréscimo isto após Olá "device de abrir LUKS #":
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Executar Olá "/ sbin/usr/dracut - f - v" tooupdate Olá initrd.

![Configuração do centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Carregar a conta do storage do Azure encriptada tooan VHD
Depois de ativar a encriptação BitLocker ou a encriptação de DM-Crypt, Olá local encriptado VHD necessidades toobe carregado tooyour conta do storage.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Carregar o segredo de encriptação de disco Olá para Olá previamente encriptado VM tooyour Cofre de chaves
segredo de encriptação de disco de Olá que obteve anteriormente deve ser também carregado como um segredo no Cofre de chaves. Cofre de chaves Olá necessita de encriptação de disco toohave e permissões ativadas para o cliente do Azure AD.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>Segredo de encriptação de disco não encriptado com uma KEK
tooset segurança segredo Olá no seu Cofre de chaves, utilize [conjunto AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). Se tiver uma máquina virtual do Windows, o ficheiro de bek Olá está codificado como uma cadeia base64 e, em seguida, carregada tooyour Cofre de chaves utilizando Olá `Set-AzureKeyVaultSecret` cmdlet. Para Linux Olá frase de acesso está codificado como uma cadeia base64 e, em seguida, carregada toohello Cofre de chaves. Além disso, certifique-se de que Olá etiquetas a seguir são definidas quando cria o segredo de Olá no Cofre de chaves Olá.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Olá utilize `$secretUrl` no passo seguinte do Olá para [expor o disco de SO de Olá sem utilizar KEK](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>Segredo de encriptação de disco encriptado com uma KEK
Antes de carregar o Cofre da chave secreta toohello Olá, opcionalmente, pode encriptá-lo utilizando uma chave de encriptação de chaves. Moldagem de Olá utilize [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encriptar o segredo de Olá utilizando a chave de encriptação de chaves Olá. Olá resultado desta operação de moldagem é uma cadeia de URL codificado em base64, que, em seguida, pode carregar como um segredo utilizando Olá [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Utilize `$KeyEncryptionKey` e `$secretUrl` no passo seguinte do Olá para [expor o disco Olá SO utilizando KEK](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>Especifique um URL secreto quando anexar um disco de SO
#### <a name="without-using-a-kek"></a>Sem utilizar um KEK
Enquanto estiver a anexar o disco de SO de Olá, terá de toopass `$secretUrl`. URL de Olá foi gerado na secção de "segredo de encriptação de disco não encriptada com uma KEK" Olá.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>Utilizar um KEK
Ao anexar o disco de SO de Olá, passe `$KeyEncryptionKey` e `$secretUrl`. URL de Olá foi gerado na secção de "segredo de encriptação de disco não encriptada com uma KEK" Olá.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Transferir este guia
Pode transferir este guia da Olá [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Para obter mais informações
[Explorar a encriptação de disco do Azure com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[Explorar a encriptação de disco do Azure com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
