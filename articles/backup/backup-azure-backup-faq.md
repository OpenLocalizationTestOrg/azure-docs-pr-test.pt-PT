---
title: "aaaAzure FAQ acerca da cópia de segurança | Microsoft Docs"
description: "Respostas a perguntas toocommon sobre: incluindo serviços de recuperação cofres, o que pode criar cópias de segurança, como funciona, encriptação e os limites de funcionalidades de cópia de segurança do Azure. "
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "recuperação de cópia de segurança e após desastres; serviço de cópia de segurança"
ms.assetid: 1011bdd6-7a64-434f-abd7-2783436668d7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/21/2017
ms.author: markgal;arunak;trinadhk;
ms.openlocfilehash: 3338f7620bcc6ebf53c9c161191f2d8bca1a29da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-service"></a>Perguntas sobre Olá serviço de cópia de segurança do Azure
Este artigo tem respostas toocommon perguntas toohelp rapidamente a compreender os componentes de cópia de segurança do Azure Olá. Algumas das respostas hello, existem artigos de toohello ligações que tem informações abrangentes. Pode colocar perguntas sobre o Backup do Azure, clicando em **comentários** (toohello direita). Os comentários são apresentados na parte inferior de Olá deste artigo. Uma conta de Livefyre é toocomment necessária. Também pode publicar perguntas sobre Olá serviço de cópia de segurança do Azure no Olá [fórum de discussão](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

secções de Olá tooquickly análise neste artigo, utilize o direito de toohello de ligações de Olá, em **neste artigo**.


## <a name="recovery-services-vault"></a>Cofre dos serviços de recuperação

### <a name="is-there-any-limit-on-hello-number-of-vaults-that-can-be-created-in-each-azure-subscription-br"></a>Existe algum limite no número de Olá de cofres que podem ser criados em cada subscrição do Azure? <br/>
Sim. A partir de setembro de 2016, pode criar 25 cofres de Serviços de Recuperação e cópia de segurança por subscrição. Pode criar cópias de segurança dos serviços de recuperação too25 cofres, por região suportada de cópia de segurança do Azure, por subscrição. Se precisar de mais cofres, crie uma subscrição adicional.

### <a name="are-there-limits-on-hello-number-of-serversmachines-that-can-be-registered-against-each-vault-br"></a>Existem limites no número de Olá de servidores/máquinas que podem ser registados em relação a cada Cofre? <br/>
Sim, pode registar too50 máquinas por cofre. Para máquinas virtuais de IaaS do Azure, Olá limite é de 200 VMs por cofre. Se precisar de tooregister mais máquinas, crie outro cofre.

### <a name="if-my-organization-has-one-vault-how-can-i-isolate-one-servers-data-from-another-server-when-restoring-databr"></a>Se a minha organização tiver um cofre, como posso isolar os dados de um servidor de outro servidor quando restaurar os dados?<br/>
Olá, todos os servidores que são registado toohello mesmo cofre pode recuperar dados de cópia de segurança por outros servidores *que utilizam Olá a mesma frase de acesso*. Se tiver servidores cujos dados de cópia de segurança pretende tooisolate a partir de outros servidores na sua organização, utilize uma frase de acesso designada para esses servidores. Por exemplo, os servidores de recursos humanos podem utilizar uma frase de acesso de encriptação, os servidores de gestão de contas outra e os servidores de armazenamento uma terceira.

### <a name="can-i-migrate-my-backup-data-or-vault-between-subscriptions-br"></a>Posso "migrar" os meus dados de cópia de segurança ou o meu cofre entre subscrições? <br/>
Não. cofre Olá é criado um nível de subscrição e não pode ser reatribuídos tooanother subscrição quando for criado.

### <a name="recovery-services-vaults-are-resource-manager-based-are-backup-vaults-classic-mode-still-supported-br"></a>Os cofres dos Serviços de Recuperação baseiam-se no Resource Manager. Os cofres do Backup (modo clássico) ainda são suportados? <br/>
Todos os cofres de cópia de segurança existentes no Olá [portal clássico](https://manage.windowsazure.com) continuar toobe suportado. No entanto, já não pode utilizar cofres de cópia de segurança novo do Olá toodeploy portal clássico. A Microsoft recomenda utilizando cofres dos serviços de recuperação para todas as implementações, porque os melhoramentos futuros aplicam tooRecovery cofres dos serviços, apenas. Se tentar toocreate um cofre de cópia de segurança no portal clássico Olá, será redirecionado toohello [portal do Azure](https://portal.azure.com).

### <a name="can-i-migrate-a-backup-vault-tooa-recovery-services-vault-br"></a>Pode migrar um cofre de serviços de recuperação de tooa de Cofre de cópia de segurança? <br/>
Infelizmente não, não é possível migrar conteúdo Olá um tooa do Cofre de cópia de segurança que do cofre dos serviços de recuperação. Estamos a trabalhar no sentido de adicionar esta funcionalidade, mas não está disponível atualmente.

### <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Criei uma cópia de segurança das minhas VMs clássicas num cofre do Backup. Pode migrar as minhas VMs do modo de Gestor de tooResource modo clássico e protegê-los num cofre dos serviços de recuperação?
Pontos de recuperação VM Clássicos no Cofre de cópia de segurança não migra automaticamente tooa Cofre de serviços de recuperação quando move Olá VM do clássico tooResource modo Manager. Siga estes passos tootransfer as cópias de segurança VM:

1. No Cofre de cópia de segurança de Olá, aceda toohello **itens protegidos** separador e selecione Olá VM. Clique em [Parar Proteção](backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deixe a opção *Eliminar dados de cópia de segurança associados* **desmarcada**.
2. Elimine a extensão de cópia de segurança/instantâneo de Olá da Olá VM.
3. Migre máquina virtual de Olá do modo de Gestor de tooResource modo clássico. Certifique-se a informações de rede e de armazenamento de Olá máquina de virtual toohello correspondente também é migrada tooResource Manager modo.
4. Criar um cofre dos serviços de recuperação e configurar a cópia de segurança Olá migrar máquina virtual a utilizar **cópia de segurança** ação por cima do dashboard do cofre. Para informações detalhadas sobre a cópia de segurança dos serviços de recuperação do tooa VM do cofre, consulte o artigo Olá, [proteger as VMs do Azure com um cofre dos serviços de recuperação](backup-azure-vms-first-look-arm.md).

## <a name="azure-backup-agent"></a>Agente do Backup do Azure
Está disponível uma lista detalhada de perguntas em [FAQ on Azure file-folder backup](backup-azure-file-folder-backup-faq.md) (FAQ sobre a cópia de segurança de ficheiros/pastas do Azure).

## <a name="azure-vm-backup"></a>Cópias de segurança de VMs do Azure
Está disponível uma lista detalhada de perguntas em [FAQ on Azure VM backup](backup-azure-vm-backup-faq.md) (FAQ sobre as cópias de segurança de VMs do Azure).

## <a name="back-up-vmware-servers"></a>Fazer cópia de segurança dos servidores VMware

### <a name="can-i-back-up-vmware-vcenter-servers-tooazure"></a>Pode criar cópias de segurança tooAzure de servidores do VMware vCenter?

Sim. Pode utilizar o servidor de cópia de segurança do Azure tooback VMware vCenter e ESXi tooAzure. Para informações sobre a versão de VMware Olá suportado, consulte o artigo de Olá, [matriz de proteção do servidor de cópia de segurança do Azure](backup-mabs-protection-matrix.md). Para obter instruções passo a passo, consulte [tooback de servidor de cópia de segurança do Azure de utilização se um servidor VMware](backup-azure-backup-server-vmware.md).


## <a name="azure-backup-server-and-system-center-data-protection-manager"></a>Azure Backup Server e System Center Data Protection Manager
### <a name="can-i-use-azure-backup-server-toocreate-a-bare-metal-recovery-bmr-backup-for-a-physical-server-br"></a>Posso utilizar o servidor de cópia de segurança do Azure toocreate uma cópia de segurança de recuperação Bare bare Metal (BMR) para um servidor físico? <br/>
Sim.

### <a name="can-i-register-my-dpm-server-toomultiple-vaults-br"></a>Pode registar os meus cofres de toomultiple do servidor do DPM? <br/>
Não. Um servidor DPM ou MABS pode ser registado tooonly um cofre.

### <a name="which-version-of-system-center-data-protection-manager-is-supported-br"></a>Que versão do System Center Data Protection Manager é suportada? <br/>
Recomendamos que instale Olá [mais recente](http://aka.ms/azurebackup_agent) Azure Backup agent Olá update rollup mais recente (UR) para o System Center Data Protection Manager (DPM). A partir de Agosto de 2016, 11 de Rollup de atualização é a atualização mais recente Olá.

### <a name="i-have-installed-azure-backup-agent-tooprotect-my-files-and-folders-can-i-now-install-system-center-dpm-toowork-with-azure-backup-agent-tooprotect-on-premises-applicationvm-workloads-tooazure-br"></a>Instalei tooprotect de agente do Backup do Azure meus ficheiros e pastas. Posso agora a instalar o System Center DPM toowork com o Azure Backup agent tooprotect no local cargas de trabalho da VM/aplicações tooAzure? <br/>
toouse cópia de segurança do Azure com o System Center Data Protection Manager (DPM), instale primeiro o DPM e, em seguida, instale o agente de cópia de segurança do Azure. Instalar componentes do Backup do Azure Olá por esta ordem garante o agente de cópia de segurança do Azure Olá funciona com o DPM. Instalar agente do Backup do Azure de Olá antes de instalar o DPM não está aconselhado nem suportado.


## <a name="how-azure-backup-works"></a>Como funciona o Azure Backup
### <a name="if-i-cancel-a-backup-job-once-it-has-started-is-hello-transferred-backup-data-deleted-br"></a>Se cancelar uma tarefa de cópia de segurança depois de ser iniciada, é hello dados de cópia de segurança transferidos eliminados? <br/>
Não. Todos os dados transferidos para o Cofre de Olá, antes de tarefa de cópia de segurança de Olá foi cancelada, permanece no Cofre de Olá. Olá, Azure utiliza de cópia de segurança toooccasionally de mecanismo um ponto de verificação Adicionar dados de cópia de segurança de toohello de pontos de verificação durante a cópia de segurança. Porque não existem pontos de verificação nos dados de cópia de segurança de Olá, processo de cópia de segurança seguinte Olá pode validar a integridade de Olá dos ficheiros de Olá. tarefa de cópia de segurança seguinte Olá serão efetuadas cópias de segurança de dados de incremental toohello. Cópias de segurança incrementais apenas transferirem dados novos ou alterados, o que equivale toobetter de utilização de largura de banda.

Se cancelar uma tarefa de cópia de segurança para uma VM do Azure, os dados transferidos são ignorados. tarefa de cópia de segurança seguinte Olá transfere dados incrementais de Olá última tarefa bem sucedida cópia de segurança.

### <a name="are-there-limits-on-when-or-how-many-times-a-backup-job-can-be-scheduledbr"></a>Existem limites para quando ou para o número de vezes que uma tarefa de cópia de segurança pode ser agendada?<br/>
Sim. Pode executar tarefas de cópia de segurança no Windows Server ou estações de trabalho do Windows se toothree horas por dia. Pode executar tarefas de cópia de segurança no System Center DPM segurança tootwice por dia. Pode executar uma tarefa de cópia de segurança para as VMs do IaaS uma vez por dia. Pode utilizar Olá agendamento de política para o Windows Server ou toospecify de estação de trabalho do Windows agendas diárias ou semanais. Ao utilizar o System Center DPM, pode especificar agendamentos diários, semanais, mensais e anuais.

### <a name="why-is-hello-size-of-hello-data-transferred-toohello-recovery-services-vault-smaller-than-hello-data-i-backed-upbr"></a>Por que motivo é o tamanho de Olá de Olá dados transferidos toohello que dos serviços de recuperação mais pequeno do que os dados de Olá que minha cópia de segurança do Cofre?<br/>
 Todos os dados de Olá cópia de segurança do agente do Backup do Azure ou o SCDPM ou o servidor de cópia de segurança do Azure, são comprimidos e encriptados antes de serem transferidos. Assim que for aplicada Olá compressão e encriptação, dados de Olá no Cofre de cópia de segurança de Olá são 30-40% mais reduzidos.

## <a name="what-can-i-back-up"></a>Do que posso fazer uma cópia de segurança
### <a name="which-operating-systems-do-azure-backup-support-br"></a>Quais os sistemas operativos suportados pelo Azure Backup? <br/>
Cópia de segurança do Azure suporta Olá seguinte lista de sistemas operativos para fazer cópias de segurança: ficheiros e pastas e aplicações de carga de trabalho protegidas com o servidor de cópia de segurança do Azure e o System Center Data Protection Manager (DPM).

| Sistema Operativo | Plataforma | SKU |
|:--- | --- |:--- |
| Windows 8 e SPs mais recentes |64 bits |Enterprise, Pro |
| Windows 7 e SPs mais recentes |64 bits |Ultimate, Enterprise, Professional, Home Premium, Home Basic, Starter |
| Windows 8.1 e SPs mais recentes |64 bits |Enterprise, Pro |
| Windows 10 |64 bits |Enterprise, Pro, Home |
| Windows Server 2016 |64 bits |Standard, Datacenter, Essentials |
| Windows Server 2012 R2 SPs mais recentes |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 e SPs mais recentes |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2016 e SPs mais recentes |64 bits |Standard, Workgroup | 
| Windows Storage Server 2012 R2 e SPs mais recentes |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 e SPs mais recentes |64 bits |Standard, Workgroup |
| Windows Server 2012 R2 SPs mais recentes |64 bits |Essencial |
| Windows Server 2008 R2 SP1 |64 bits |Standard, Enterprise, Datacenter, Foundation |
| Windows Server 2008 SP2 |64 bits |Standard, Enterprise, Datacenter, Foundation |

**Para cópias de segurança de VMs do Azure:**

* **Linux**: o Azure Backup suporta [uma lista de distribuições apoiadas pelo Azure](../virtual-machines/linux/endorsed-distros.md), exceto Core OS Linux.  Outras Bring-Your-proprietário-as distribuições do Linux também podem funcionar desde que o agente VM de Olá está disponível na máquina virtual de Olá e suporte para o Python existe.
* **Windows Server**: não são suportadas as versões mais antigas do que o Windows Server 2008 R2.


### <a name="is-there-a-limit-on-hello-size-of-each-data-source-being-backed-up-br"></a>Existe um limite no tamanho Olá de cada origem de dados a cópia de segurança? <br/>
Não há nenhum limite na quantidade de Olá de dados que pode criar cópias de segurança tooa cofre. Cópia de segurança do Azure restringe o tamanho máximo do Olá Olá origem de dados, no entanto, estes limites são grandes. A partir de Agosto de 2015, Olá o tamanho máximo para uma origem de dados para sistemas de operativos Olá suportado é:

| S.No | Sistema operativo | Tamanho máximo da origem de dados |
|:---:|:--- |:--- |
| 1 |Windows Server 2012 ou posterior |54 400 GB |
| 2 |Windows 8 ou posterior |54 400 GB |
| 3 |Windows Server 2008, Windows Server 2008 R2 |1700 GB |
| 4 |Windows 7 |1700 GB |

Olá, a tabela seguinte explica como é determinado cada tamanho da origem de dados.

| Origem de dados | Detalhes |
|:---:|:--- |
| Volume |quantidade de Olá de dados a cópia de segurança do volume único de uma servidor ou máquina cliente |
| Máquina virtual do Hyper-V |Soma dos dados de todos os VHDs Olá da máquina virtual de Olá a cópia de segurança |
| Base dados do Microsoft SQL Server |Tamanho da SQL Database única para a cópia de segurança |
| Microsoft SharePoint |Soma de Olá conteúdo e a configuração bases de dados dentro de um farm do SharePoint a cópia de segurança |
| Microsoft Exchange |Soma de todas as bases de dados do Exchange num servidor Exchange para a cópia de segurança |
| Estado do Sistema/BMR |Cada cópia individual da BMR ou estado do sistema da máquina de Olá a cópia de segurança |

Para cópia de segurança de VM do Azure, cada VM pode ter segurança too16 discos de dados com cada disco de dados ser de tamanho de 1023GB ou menos. 

## <a name="retention-policy-and-recovery-points"></a>Pontos de recuperação e política de retenção
### <a name="is-there-a-difference-between-hello-retention-policy-for-dpm-and-windows-serverclient-that-is-on-windows-server-without-dpmbr"></a>Existe uma diferença entre a política de retenção de Olá para o DPM e o Windows Server/cliente (ou seja, de no Windows Server sem DPM)?<br/>
Não, o DPM e o Windows Server/cliente Windows têm políticas de retenção diárias, semanais, mensais e anuais.

### <a name="can-i-configure-my-retention-policies-selectively--ie-configure-weekly-and-daily-but-not-yearly-and-monthlybr"></a>Posso configurar as minhas políticas de retenção seletivamente – por exemplo, configurar políticas de retenção semanais e diárias, mas não anuais e mensais?<br/>
Sim, Olá estrutura de retenção do Backup do Azure permite-lhe toohave total flexibilidade na definição de política de retenção de Olá de acordo com os seus requisitos.

### <a name="can-i-schedule-a-backup-at-6pm-and-specify-retention-policies-at-a-different-timebr"></a>Posso "agendar uma cópia de segurança" para as 18:00 e especificar políticas de retenção noutra hora?<br/>
Não. Só podem ser aplicadas políticas de retenção em pontos de cópia de segurança. No Olá seguinte imagem, a política de retenção de Olá é especificada para cópias de segurança criadas às 12: 00 e 18: 00. <br/>

![Agendar Cópia de Segurança e Retenção](./media/backup-azure-backup-faq/Schedule.png)
<br/>

### <a name="if-a-backup-is-retained-for-a-long-duration-does-it-take-more-time-toorecover-an-older-data-point-br"></a>Se uma cópia de segurança for mantida durante um longo período de tempo, demora mais tempo toorecover um ponto de dados mais antigo? <br/>
Não – tempo Olá toorecover hello mais antigos ou Olá ponto mais recente é Olá mesmo. Cada ponto de recuperação funciona como um ponto completo.

### <a name="if-each-recovery-point-is-like-a-full-point-does-it-impact-hello-total-billable-backup-storagebr"></a>Se cada ponto de recuperação é como um ponto completo, afeta armazenamento de cópia de segurança faturável total Olá?<br/>
Os produtos de ponto de retenção de longa duração típicos armazenam cópias de segurança como pontos completos. pontos completos Olá são armazenamento *ineficaz* , mas são mais fáceis e toorestore mais rápida. As cópias incrementais são armazenamento *eficiente* , mas necessitam que toorestore uma cadeia de dados, que tem impacto no seu tempo de recuperação. Azure cópia de segurança armazenamento arquitetura fornecem Olá melhor de dois mundos ao armazenar os dados para restauros rápidos e incorrer em custos de armazenamento reduzido de forma ideal. Esta abordagem de armazenamento de dados garante que a largura de banda de entrada e de saída é utilizada com eficácia. Tanto Olá período de dados de armazenamento e Olá tempo necessários dados de Olá toorecover, é mantida tooa mínimo. Saiba mais sobre como as [cópias de segurança incrementais](https://azure.microsoft.com/blog/microsoft-azure-backup-save-on-long-term-storage/) são eficientes.

### <a name="is-there-a-limit-on-hello-number-of-recovery-points-that-can-be-createdbr"></a>Existe um limite do número de Olá de pontos de recuperação que podem ser criados?<br/>
Pode criar cópias de segurança too9999 pontos de recuperação por instância protegido. Uma instância protegida é um computador, servidor (física ou virtual) ou carga de trabalho configurada tooback segurança tooAzure de dados. Para obter mais informações, consulte explicações Olá de [cópia de segurança e retenção](./backup-introduction-to-azure-backup.md#backup-and-retention), e [o que é uma instância protegida](./backup-introduction-to-azure-backup.md#what-is-a-protected-instance)?

### <a name="how-many-recoveries-can-i-perform-on-hello-data-that-is-backed-up-tooazurebr"></a>Quantas recuperações posso efetuar nos dados de Olá cópia de segurança tooAzure?<br/>
Não há nenhum limite do número de Olá de recuperações do Backup do Azure.

### <a name="when-restoring-data-do-i-pay-for-hello-egress-traffic-from-azure-br"></a>Ao restaurar os dados, posso pagar para tráfego de saída Olá a partir do Azure? <br/>
Não. As recuperações são gratuitas e não lhe serem cobrados para tráfego de saída Olá.

## <a name="azure-backup-encryption"></a>Encriptação do Azure Backup
### <a name="is-hello-data-sent-tooazure-encrypted-br"></a>Dados de Olá são enviados tooAzure encriptado? <br/>
Sim. Os dados são encriptados na máquina SCDPM/cliente/servidor no local de Olá utilizando AES256 e dados de Olá são enviados através de uma ligação HTTPS segura.

### <a name="is-hello-backup-data-on-azure-encrypted-as-wellbr"></a>São dados de cópia de segurança de Olá no Azure também são encriptado?<br/>
Sim. Olá os dados enviados tooAzure permanece encriptado (Inativos). A Microsoft não desencripta os dados de cópia de segurança de Olá em qualquer momento. Quando efetuar cópias de segurança de uma VM do Azure, cópia de segurança do Azure baseia-se na encriptação de máquina virtual de Olá. Por exemplo, se a VM é encriptada utilizando a Azure Disk Encryption ou outras tecnologias de encriptação, o Backup do Azure utiliza essa toosecure encriptação os dados.

### <a name="what-is-hello-minimum-length-of-encryption-key-used-tooencrypt-backup-data-br"></a>Qual é Olá comprimento mínimo da chave de encriptação utilizado tooencrypt dados de cópia de segurança? <br/>
chave de encriptação de Olá deve ter pelo menos 16 carateres, quando estiver a utilizar o agente de cópia de segurança do Azure. Para VMs do Azure, não há nenhum toolength de limite das chaves utilizado pelo Azure KeyVault. 

### <a name="what-happens-if-i-misplace-hello-encryption-key-can-i-recover-hello-data-or-can-microsoft-recover-hello-data-br"></a>O que acontece se perder a chave de encriptação de Olá? Posso recuperar dados hello (ou) pode a Microsoft recuperar dados de Olá? <br/>
dados de cópia de segurança Olá tooencrypt utilizadas chaves Olá estão presentes apenas no local de cliente de Olá. A Microsoft não mantém uma cópia no Azure e não tem qualquer toohello a chave de acesso. Se o cliente de Olá perder a chave de Olá, a Microsoft não é possível recuperar dados de cópia de segurança de Olá.
