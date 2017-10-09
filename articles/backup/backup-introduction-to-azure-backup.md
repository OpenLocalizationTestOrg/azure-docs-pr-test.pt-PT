---
title: "aaaWhat é o Backup do Azure? | Microsoft Docs"
description: "Utilize tooback de cópia de segurança do Azure a cópia de segurança e restaurar dados e cargas de trabalho a partir de servidores Windows, estações de trabalho do Windows, servidores do System Center DPM e máquinas virtuais do Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "cópia de segurança e restauro; serviços de recuperação; soluções de cópia de segurança"
ms.assetid: 0d2a7f08-8ade-443a-93af-440cbf7c36c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/11/2017
ms.author: markgal;trinadhk;anuragm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 953a19600f67a6b7451f71b1e3234d913816d18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-features-in-azure-backup"></a>Descrição geral das funcionalidades de Olá na cópia de segurança do Azure
Cópia de segurança do Azure é serviço de baseado no Azure de Olá a pedido pode utilizar tooback cópias de segurança (ou proteger) e restaurar os dados no Olá nuvem da Microsoft. O Azure Backup substitui a solução de cópia de segurança no local ou fora das instalações por uma solução baseada na nuvem que é fiável, segura e competitiva em termos de custos. Cópia de segurança do Azure oferece vários componentes que lhe transfere e implementar em computadores apropriados Olá, servidor, ou na nuvem de Olá. componente de Olá ou o agente, que implementa depende que pretende tooprotect. Todos os componentes do Backup do Azure (independentemente se estiver a proteger dados no local ou na nuvem de Olá) podem ser utilizado tooback segurança cofre dos serviços de recuperação de tooa de dados no Azure. Consulte Olá [tabela de componentes do Backup do Azure](backup-introduction-to-azure-backup.md#which-azure-backup-components-should-i-use) (posteriormente neste artigo) para obter informações sobre os dados específicos do componente toouse tooprotect, aplicações ou cargas de trabalho.

[Veja uma descrição geral do vídeo do Azure Backup](https://azure.microsoft.com/documentation/videos/what-is-azure-backup/)

## <a name="why-use-azure-backup"></a>Porquê utilizar o Backup do Azure?
Soluções de cópia de segurança tradicionais evoluíram cloud de Olá tootreat como um ponto final ou armazenamento estáticos ou de destino, semelhante toodisks banda. Embora esta abordagem seja simple, é limitada e não beneficiar da plataforma em nuvem subjacente, o que traduz tooan solução ineficaz dispendiosas. Outras soluções são dispendiosas porque pode ficar pagar para o tipo errado de Olá do armazenamento ou de armazenamento que não precisa. Outras soluções, muitas vezes, são ineficazes porque não oferecem tipo de Olá ou a quantidade de armazenamento que precisa ou tarefas administrativas necessitam demasiado tempo. Em contrapartida, o Azure Backup fornece estas principais vantagens:

**Gestão de armazenamento automática** - ambientes híbridos, muitas vezes, necessitam de armazenamento heterogéneo - algumas no local e Olá algumas na nuvem. Com o Azure Backup, não existe nenhum custo para a utilização de dispositivos de armazenamento no local. O Azure Backup atribui automaticamente e gere o armazenamento de cópia de segurança, e utiliza um modelo de pagamento enquanto utiliza. Pay-como-utiliza significa que apenas paga armazenamento Olá que consumir. Para obter mais informações, consulte Olá [do Azure de preços do artigo](https://azure.microsoft.com/pricing/details/backup).

**Dimensionamento ilimitado** - cópia de segurança do Azure utiliza Olá subjacente energia e dimensionamento ilimitado da Olá do Azure na nuvem toodeliver elevada disponibilidade - com nenhuma manutenção ou o overhead de monitorização. Pode configurar alertas tooprovide sobre eventos, mas não precisa de tooworry sobre elevada disponibilidade para os seus dados na nuvem de Olá.

**Várias opções de armazenamento** - um aspeto de elevada disponibilidade é a replicação do armazenamento. O Azure Backup oferece dois tipos de replicação: [armazenamento localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) e [armazenamento georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage). Escolha a opção de armazenamento de cópia de segurança de Olá com base na necessidade:

* Armazenamento localmente redundante (LRS) replica os dados três vezes (cria três cópias dos seus dados) no Centro de dados emparelhado no Olá mesma região. O LRS é uma opção de baixo custo para proteger os dados contra falhas de hardware locais.

* Armazenamento georredundante (GRS) replica o dados tooa região secundária a (centenas de quilómetros localização primária de Olá Olá de dados de origem). O GRS custa mais do que o LRS, mas o GRS proporciona um nível mais elevado de durabilidade aos seus dados, mesmo se ocorrer uma indisponibilidade regional.

**Transferência de dados ilimitada** - cópia de segurança do Azure não limita a quantidade de Olá de entrada ou saídos a transferência de dados de. Cópia de segurança do Azure também não cobram dinheiro para dados de Olá que são transferidos. No entanto, se utilizar Olá do Azure para importar/exportar serviço tooimport grandes quantidades de dados, há um custo associado de dados de entrada. Para mais informações sobre este custo, veja [Fluxo de trabalho de cópia de segurança offline no Azure Backup](backup-azure-backup-import-export.md). Dados de saída refere-se toodata transferido de um cofre dos serviços de recuperação durante uma operação de restauro.

**Encriptação de dados** -permite que a encriptação de dados de transmissão segura e de armazenamento dos seus dados na nuvem pública Olá. Armazenar Olá encriptação frase de acesso localmente e nunca é transmitida ou armazenada no Azure. Se for necessário toorestore nenhum dos dados de Olá, só tem frase de acesso de encriptação ou da chave.

**Cópia de segurança consistentes com aplicações** -se efetuar cópias de segurança de um servidor de ficheiros, a máquina virtual ou a base de dados SQL, é preciso tooknow que um ponto de recuperação tem todas as necessárias dados toorestore Olá cópia de segurança. Cópia de segurança do Azure fornece cópias de segurança consistentes com aplicações, que certificar-se de que as correções adicionais não são necessários toorestore Olá dados. Restaurar os dados consistentes da aplicação reduz o tempo de restauro Olá, permitindo-lhe tooa retorno tooquickly estado de execução.

**Retenção de longo prazo** -em vez de mudança de cópias de segurança de disco tootape e mover Olá banda tooan localização fora das instalações, pode utilizar o Azure para a retenção de curta e longo prazo. Azure não limita o comprimento de Olá de tempo dados permanecem no Cofre de cópia de segurança ou dos serviços de recuperação. Pode manter os dados num cofre o tempo que pretender. O Azure Backup tem um limite de 9999 pontos de recuperação por instância protegida. Consulte Olá [cópia de segurança e retenção](backup-introduction-to-azure-backup.md#backup-and-retention) secção neste artigo para obter uma explicação de como este limite pode afetar as suas necessidades de cópia de segurança.  

## <a name="which-azure-backup-components-should-i-use"></a>Que componentes do Azure Backup devo utilizar?
Se não tem a certeza que componentes de cópia de segurança do Azure funciona para as suas necessidades, consulte Olá seguinte tabela para obter informações sobre o que pode proteger com cada componente. Olá portal do Azure fornece um assistente, o que está incorporado no portal de Olá, tooguide que escolher Olá toodownload componente e implementar. Assistente de Olá, o que faz parte da criação do cofre dos serviços de recuperação de Olá, servem como orientação para Olá os passos para selecionar um objetivo de cópia de segurança e escolher Olá tooprotect de dados ou aplicação.

| Componente | Benefícios | Limites | O que está protegido? | Onde estão armazenadas as cópias de segurança? |
| --- | --- | --- | --- | --- |
| Agente do Backup do Azure (MARS) |<li>Os ficheiros e as pastas de cópia de segurança no SO Windows físico ou virtual (as VMs podem estar no local ou no Azure)<li>Nenhum servidor de cópia de segurança separado necessário. |<li>Criar cópias de segurança 3 vezes por dia <li>Sem deteção de aplicações; restauro apenas ao nível do ficheiro, pasta e volume, <li>  Sem suporte para Linux. |<li>Ficheiros, <li>Pastas |Cofre dos Serviços de Recuperação |
| System Center DPM |<li>Instantâneos de deteção de aplicações (VSS)<li>Total flexibilidade para quando tootake cópias de segurança<li>Granularidade de recuperação (tudo)<li>Pode utilizar o cofre dos Serviços de Recuperação<li>Apoio técnico para Linux para VMs de Hyper-V e VMware <li>Criar cópias de segurança e restaurar VMs VMware com o DPM 2012 R2 |Não é possível fazer cópias de segurança da carga de trabalho do Oracle.|<li>Ficheiros, <li>Pastas,<li> Volumes, <li>VMs,<li> Aplicações,<li> Cargas de trabalho |<li>Cofre dos Serviços de Recuperação,<li> Disco ligado localmente,<li>  Banda (apenas no local) |
| Servidor do Backup do Azure |<li>Instantâneos da deteção de aplicações (VSS)<li>Total flexibilidade para quando tootake cópias de segurança<li>Granularidade de recuperação (tudo)<li>Pode utilizar o cofre dos Serviços de Recuperação<li>Apoio técnico para Linux para VMs de Hyper-V e VMware<li>Criar cópias de segurança e restaurar VMs VMware <li>Não necessita de uma licença do System Center |<li>Não é possível fazer cópias de segurança da carga de trabalho do Oracle.<li>Requer sempre a subscrição do Azure em direto<li>Sem suporte para cópia de segurança em fila |<li>Ficheiros, <li>Pastas,<li> Volumes, <li>VMs,<li> Aplicações,<li> Cargas de trabalho |<li>Cofre dos Serviços de Recuperação,<li> Disco ligado localmente |
| Cópia de segurança da VM do IaaS do Azure |<li>Cópias de segurança nativas para o Windows/Linux<li>Não é necessária qualquer instalação do agente específico<li>Cópia de segurança ao nível dos recursos de infraestrutura sem ser necessária qualquer infraestrutura de cópia de segurança |<li>Criar cópia de segurança de VMs uma vez por dia <li>Restaurar VMs apenas ao nível do disco<li>Não é possível efetuar a cópia de segurança no local |<li>VMs, <li>Todos os discos (com o PowerShell) |<p>Cofre dos Serviços de Recuperação</p> |

## <a name="what-are-hello-deployment-scenarios-for-each-component"></a>Quais são os cenários de implementação de Olá para cada componente?
| Componente | Pode ser implementado no Azure? | Pode ser implementado no local? | Armazenamento de destino suportado |
| --- | --- | --- | --- |
| Agente do Backup do Azure (MARS) |<p>**Sim**</p> <p>agente de cópia de segurança do Azure de Olá pode ser implementado em qualquer VM do Windows Server que é executada no Azure.</p> |<p>**Sim**</p> <p>agente de cópia de segurança de Olá pode ser implementado em qualquer máquina física ou VM do Windows Server.</p> |<p>Cofre dos Serviços de Recuperação</p> |
| System Center DPM |<p>**Sim**</p><p>Saiba mais sobre [como tooprotect as cargas de trabalho no Azure utilizando o System Center DPM](backup-azure-dpm-introduction.md).</p> |<p>**Sim**</p> <p>Saiba mais sobre [como tooprotect cargas de trabalho e VMs no datacenter](https://technet.microsoft.com/system-center-docs/dpm/data-protection-manager).</p> |<p>Disco ligado localmente,</p> <p>Cofre dos Serviços de Recuperação,</p> <p>banda (apenas no local)</p> |
| Servidor do Backup do Azure |<p>**Sim**</p><p>Saiba mais sobre [como tooprotect as cargas de trabalho no Azure utilizando o servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md).</p> |<p>**Sim**</p> <p>Saiba mais sobre [como tooprotect as cargas de trabalho no Azure utilizando o servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md).</p> |<p>Disco ligado localmente,</p> <p>Cofre dos Serviços de Recuperação</p> |
| Cópia de segurança da VM do IaaS do Azure |<p>**Sim**</p><p>Parte dos recursos de infraestrutura do Azure</p><p>Especializada para a [cópia de segurança da infraestrutura do Azure como máquinas virtuais do serviço (IaaS)](backup-azure-vms-introduction.md).</p> |<p>**Não**</p> <p>Utilize o System Center DPM tooback segurança das máquinas virtuais no seu centro de dados.</p> |<p>Cofre dos Serviços de Recuperação</p> |

## <a name="which-applications-and-workloads-can-be-backed-up"></a>Podem ser efetuadas cópias de segurança a que aplicações e cargas de trabalho?
Olá, a tabela seguinte fornece uma matriz de dados de Olá e cargas de trabalho que podem ser protegidas utilizando a cópia de segurança do Azure. a coluna de solução de cópia de segurança do Azure de Olá tem documentação de implementação de toohello ligações para essa solução. Cada componente do Azure Backup pode ser implementado num ambiente de modelo Clássico (Gestor de Serviços-implementação) ou de Gestor de Recursos-implementação.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

| Dados ou Carga de Trabalho | Ambiente de origem | Solução do Backup do Azure |
| --- | --- | --- |
| Ficheiros e pastas |Windows Server |<p>[Agente do Backup do Azure](backup-configure-vault.md),</p> <p>[O System Center DPM](backup-azure-dpm-introduction.md) (+ Olá agente de cópia de segurança do Azure),</p> <p>[Servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de cópia de segurança do Azure Olá)</p> |
| Ficheiros e pastas |Computador Windows |<p>[Agente do Backup do Azure](backup-configure-vault.md),</p> <p>[O System Center DPM](backup-azure-dpm-introduction.md) (+ Olá agente de cópia de segurança do Azure),</p> <p>[Servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de cópia de segurança do Azure Olá)</p> |
| Máquina virtual do Hyper-V (Windows) |Windows Server |<p>[O System Center DPM](backup-azure-backup-sql.md) (+ Olá agente de cópia de segurança do Azure),</p> <p>[Servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de cópia de segurança do Azure Olá)</p> |
| Máquina virtual do Hyper-V (Linux) |Windows Server |<p>[O System Center DPM](backup-azure-backup-sql.md) (+ Olá agente de cópia de segurança do Azure),</p> <p>[Servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de cópia de segurança do Azure Olá)</p> |
| Microsoft SQL Server |Windows Server |<p>[O System Center DPM](backup-azure-backup-sql.md) (+ Olá agente de cópia de segurança do Azure),</p> <p>[Servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de cópia de segurança do Azure Olá)</p> |
| Microsoft SharePoint |Windows Server |<p>[O System Center DPM](backup-azure-backup-sql.md) (+ Olá agente de cópia de segurança do Azure),</p> <p>[Servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de cópia de segurança do Azure Olá)</p> |
| Microsoft Exchange |Windows Server |<p>[O System Center DPM](backup-azure-backup-sql.md) (+ Olá agente de cópia de segurança do Azure),</p> <p>[Servidor de cópia de segurança do Azure](backup-azure-microsoft-azure-backup.md) (inclui o agente de cópia de segurança do Azure Olá)</p> |
| VMs do IaaS do Azure (Windows) |em execução no Azure |[Azure Backup (extensão da VM)](backup-azure-vms-introduction.md) |
| VMs do IaaS do Azure (Linux) |em execução no Azure |[Azure Backup (extensão da VM)](backup-azure-vms-introduction.md) |

## <a name="linux-support"></a>Apoio Técnico para Linux
Olá tabela seguinte mostra os componentes de cópia de segurança do Azure de Olá que têm suporte para Linux.  

| Componente | Apoio Técnico para Linux (aprovado pelo Azure) |
| --- | --- |
| Agente do Backup do Azure (MARS) |Nenhum (Apenas agente baseado no Windows) |
| System Center DPM |<li> Cópia de segurança consistente com ficheiros de VMs de Convidado Linux no Hyper-V e no VMWare<br/> <li> Restauro de VMs de Convidado do Linux do Hyper-V e do VMWare </br> </br>  *A cópia de segurança consistente com ficheiro não está disponível para a VM do Azure* <br/> |
| Servidor do Backup do Azure |<li>Cópia de segurança consistente com ficheiros de VMs de Convidado Linux no Hyper-V e no VMWare<br/> <li> Restauro de VMs de Convidado do Linux do Hyper-V e do VMWare </br></br> *A cópia de segurança consistente com ficheiro não está disponível para a VM do Azure*  |
| Cópia de segurança da VM do IaaS do Azure |Cópia de segurança consistente com a aplicação utilizando [arquitetura de script anterior script posterior](backup-azure-linux-app-consistent.md)<br/> [Recuperação de ficheiros granular](backup-azure-restore-files-from-vm.md)<br/> [Restaurar todos os discos da VM](backup-azure-arm-restore-vms.md#restore-backed-up-disks)<br/> [Restauro da VM](backup-azure-arm-restore-vms.md#create-a-new-vm-from-restore-point) |

## <a name="using-premium-storage-vms-with-azure-backup"></a>Utilizar VMs de Armazenamento Premium com o Azure Backup
O Azure Backup protege VMs de Armazenamento Premium. Armazenamento Premium do Azure é a unidade de estado sólido (SSD)-com base em cargas de trabalho do armazenamento concebido toosupport I/O intensivo. O Armazenamento Premium é apelativo para cargas de trabalho de máquina virtual (VM). Para obter mais informações sobre o Premium Storage, consulte o artigo de Olá, [Premium Storage: armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual de Azure](../storage/common/storage-premium-storage.md).

### <a name="back-up-premium-storage-vms"></a>Criar cópia de segurança das VMs do Premium Storage
Ao efetuar uma cópia de segurança de VMs do Premium Storage, serviço de cópia de segurança de Olá cria uma localização de transição temporária, com o nome "AzureBackup-", na conta do Premium Storage Olá. tamanho de Olá do Olá localização de transição é igual toohello tamanho de instantâneo de ponto de recuperação Olá. Não se esqueça de Olá conta do Premium Storage tem espaço livre suficiente tooaccommodate Olá localização de transição temporária. Para obter mais informações, consulte o artigo de Olá, [limitações de armazenamento premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets). Depois de concluída a tarefa de cópia de segurança de Olá, Olá localização de transição é eliminado. Olá preços de armazenamento utilizado para Olá localização de transição são consistente com todos os [preços do Premium storage](../storage/common/storage-premium-storage.md#pricing-and-billing).

> [!NOTE]
> Não modifique ou edite Olá localização de transição.
>
>

### <a name="restore-premium-storage-vms"></a>Restaurar VMs do Premium Storage
VMs do Premium Storage pode ser armazenamento de armazenamento Premium ou toonormal tooeither restaurada. Restaurar uma VM do Premium Storage recuperação ponto back tooPremium armazenamento é o processo normal de Olá de restauro. No entanto, pode ser económico toorestore um armazenamento de toostandard de ponto de recuperação de VM do Premium Storage. Este tipo de restauro pode ser utilizado se precisar de um subconjunto de ficheiros a partir Olá VM.

## <a name="using-managed-disk-vms-with-azure-backup"></a>Utilizar VMs de disco gerido com o Azure Backup
O Azure Backup protege VMs de disco gerido. Os discos geridos libertam-no da gestão de contas de armazenamento de máquinas virtuais e simplificam bastante o aprovisionamento das VMs.

### <a name="back-up-managed-disk-vms"></a>Cópia de segurança de VMs de disco gerido
A criação de cópias de segurança de VMs em discos geridos não difere da criação de cópias de segurança de VMs do Resource Manager. No portal do Azure Olá, pode configurar a tarefa de cópia de segurança de Olá diretamente a partir de Olá vista da Máquina Virtual ou de serviços de recuperação Olá cofre vista. Pode criar cópias de segurança de VMs em discos geridos através de coleções de RestorePoint criadas sobre os discos geridos. A cópia de segurança do Azure também suporta a criação de cópia de segurança de VMs de discos geridos encriptados com o Azure Disk Encryption (ADE).

### <a name="restore-managed-disk-vms"></a>Restaurar VMs de disco gerido
Cópia de segurança do Azure permite-lhe toorestore uma VM com discos geridos concluída ou restauro geridos conta de armazenamento de tooa de discos. Azure gere os discos de Olá gerido durante o processo de restauro Olá. (Cliente Olá) gere a conta de armazenamento de Olá criada como parte do processo de restauro Olá. Quando restaurar VMs geridas do encriptados, hello da VM chaves e segredos devem existir na operação de restauro do Olá Cofre de chaves anterior toostarting Olá.

## <a name="what-are-hello-features-of-each-backup-component"></a>Quais são as funcionalidades de Olá de cada componente de cópia de segurança?
Olá seguintes secções fornece tabelas resumem disponibilidade Olá ou suporte de várias funcionalidades em cada componente de cópia de segurança do Azure. Consulte as informações de Olá após cada tabela para obter suporte adicional ou detalhes.

### <a name="storage"></a>Armazenamento
| Funcionalidade | Agente do Backup do Azure | System Center DPM | Servidor do Backup do Azure | Cópia de segurança da VM do IaaS do Azure |
| --- | --- | --- | --- | --- |
| Cofre dos Serviços de Recuperação |![Sim][green] |![Sim][green] |![Sim][green] |![Sim][green] |
| Armazenamento em disco | |![Sim][green] |![Sim][green] | |
| Armazenamento em banda | |![Sim][green] | | |
| Compressão <br/>(no cofre dos Serviços de Recuperação) |![Sim][green] |![Sim][green] |![Sim][green] | |
| Cópia de segurança incremental |![Sim][green] |![Sim][green] |![Sim][green] |![Sim][green] |
| Eliminação de discos duplicados | |![Parcialmente][yellow] |![Parcialmente][yellow] | | |

![chave da tabela](./media/backup-introduction-to-azure-backup/table-key.png)

Olá Cofre de serviços de recuperação é o destino de armazenamento preferencial Olá em todos os componentes. O System Center DPM e o servidor de cópia de segurança do Azure fornecem também Olá opção toohave uma cópia de disco local. No entanto, apenas o System Center DPM disponibiliza Olá opção toowrite tooa banda armazenamento o dispositivo de dados.

#### <a name="compression"></a>Compressão
As cópias de segurança são comprimidas tooreduce Olá necessário espaço de armazenamento. único componente de Olá que não utiliza a compressão é a extensão da VM Olá. Olá, cópias de extensão VM de Olá todos os dados de cópia de segurança da sua toohello de conta de armazenamento dos serviços de recuperação cofre na mesma região. Sem compressão é utilizada quando a transferência de dados de Olá. Transferência de dados de Olá sem compressão ligeiramente enche armazenamento Olá utilizado. No entanto, armazenar os dados de Olá sem compressão permite restauro mais rápido, se necessitar de nesse ponto de recuperação.


#### <a name="disk-deduplication"></a>Eliminação de Discos Duplicados
Pode tirar partido da eliminação de duplicados ao implementar o System Center DPM ou o Azure Backup Server [numa máquina virtual Hyper-V](http://blogs.technet.com/b/dpm/archive/2015/01/06/deduplication-of-dpm-storage-reduce-dpm-storage-consumption.aspx). Windows Server efetua a eliminação de dados duplicados (a nível do anfitrião de Olá) nos discos rígidos virtuais (VHDs) que estão anexados toohello máquina como armazenamento de cópia de segurança.

> [!NOTE]
> A eliminação de duplicados não está disponível no Azure para nenhum componente do Backup. Quando o System Center DPM e o servidor de cópia de segurança são implementados no Azure, discos de armazenamento de Olá ligados toohello que VM não é possível ter duplicados eliminada.
>
>

### <a name="incremental-backup-explained"></a>A cópia de segurança incremental explicada
Todos os componentes de cópia de segurança do Azure suportam a cópia de segurança incremental, independentemente do armazenamento de destino Olá (disco, banda, cofre dos serviços de recuperação). Cópia de segurança incremental assegura que as cópias de segurança são armazenamento e a hora eficiente, transferindo apenas as alterações efetuadas desde a última cópia de segurança Olá.

#### <a name="comparing-full-differential-and-incremental-backup"></a>Comparação entre cópias de segurança Completas, Diferenciais e Incrementais

O consumo de armazenamento, o objetivo de tempo de recuperação (RTO) e o consumo de rede variam em cada tipo de método de cópia de segurança. tookeep Olá cópia de segurança custo total de propriedade (TCO) para baixo, terá de toounderstand como solução de cópia de segurança melhores toochoose Olá. Olá seguinte imagem compara a cópia de segurança completa, cópia de segurança diferencial e cópia de segurança Incremental. Na imagem de Olá, a origem de dados A é composta por armazenamento 10 bloqueia A1-A10, que são uma cópia de segurança mensal. A2 blocos, A3, A4 e A9 alterar no Olá primeiro mês e bloquear alterações A5 Olá mês seguinte.

![imagem que mostra a comparação dos métodos de cópia de segurança](./media/backup-introduction-to-azure-backup/backup-method-comparison.png)

Com **cópia de segurança completa**, cada cópia de segurança contém origem de dados completo de Olá. A cópia de segurança completa consome uma grande quantidade de largura de banda de rede e de armazenamento sempre que é transferida uma cópia de segurança.

**Cópia de segurança diferencial** armazena só Olá blocos que foram alterados desde Olá inicial cópia de segurança completa, que resulta numa quantidade menor de consumo de armazenamento e de rede. As cópias de segurança diferenciais não retêm cópias redundantes de dados não alterados. No entanto, uma vez que os blocos de dados de Olá permanecerem inalterados entre cópias de segurança subsequentes são transferidos e armazenados, as cópias de segurança diferenciais são ineficazes. No Olá segundo mês, os blocos alterados A2, A3, A4 e A9 são cópias de segurança. No Olá terceiro mês, estes blocos mesmos são cópias de segurança novamente, juntamente com os blocos alterados A5. Olá os blocos alterado continuar toobe cópia de segurança até acontece Olá próxima cópia de segurança completa.

**Cópia de segurança incremental** obtém uma eficiência de armazenamento e de rede elevada armazenando apenas Olá blocos de dados que foram alterados desde a cópia de segurança anterior Olá. Com a cópia de segurança incremental, não é necessário tootake cópias de segurança regulares completa. Exemplo de Olá, após Olá cópia de segurança completa para Olá primeiro mês, os blocos alterados A2, A3, A4 e A9 que estão marcados como alterado em transferidos para Olá segundo mês. Olá terceiro mês, só alterar bloco A5 é marcado e transferidos. Mover menos dados poupa recursos de armazenamento e de rede, o que reduz o TCO.   

### <a name="security"></a>Segurança
| Funcionalidade | Agente do Backup do Azure | System Center DPM | Servidor do Backup do Azure | Cópia de segurança da VM do IaaS do Azure |
| --- | --- | --- | --- | --- |
| Segurança da rede<br/> (tooAzure) |![Sim][green] |![Sim][green] |![Sim][green] |![Parcialmente][yellow] |
| Segurança de dados<br/> (no Azure) |![Sim][green] |![Sim][green] |![Sim][green] |![Parcialmente][yellow] |

![chave da tabela](./media/backup-introduction-to-azure-backup/table-key.png)

#### <a name="network-security"></a>Segurança da rede
Todo o tráfego de cópia de segurança da sua toohello de servidores que do cofre dos serviços de recuperação é encriptado utilizando 256 padrão de encriptação avançado. dados de cópia de segurança de Olá são enviados através de uma ligação HTTPS segura. dados de cópia de segurança de Olá também são armazenados no Cofre de serviços de recuperação de Olá em formato encriptado. Apenas, hello do cliente do Azure, terá de Olá frase de acesso toounlock estes dados. Microsoft não é possível desencriptar os dados de cópia de segurança de Olá em qualquer momento.

> [!WARNING]
> Depois de estabelecer o Cofre de serviços de recuperação Olá, só o utilizador tem a chave de encriptação de toohello de acesso. A Microsoft mantém uma cópia da sua chave de encriptação nunca e não tem acesso toohello chave. Se a chave de Olá está no local incorreto, a Microsoft não é possível recuperar dados de cópia de segurança de Olá.
>
>

#### <a name="data-security"></a>Segurança de dados
Cópia de segurança de VMs do Azure necessita de configurar a encriptação *dentro* Olá máquina. Utilize o BitLocker nas máquinas virtuais do Windows e o **dm crypt** nas máquinas virtuais do Linux. O Backup do Azure não encripta automaticamente dados de cópia de segurança fornecidos através deste caminho.

### <a name="network"></a>Rede
| Funcionalidade | Agente do Backup do Azure | System Center DPM | Servidor do Backup do Azure | Cópia de segurança da VM do IaaS do Azure |
| --- | --- | --- | --- | --- |
| Compressão de rede <br/>(demasiado**servidor de cópia de segurança**) | |![Sim][green] |![Sim][green] | |
| Compressão de rede <br/>(demasiado**cofre dos serviços de recuperação**) |![Sim][green] |![Sim][green] |![Sim][green] | |
| Protocolo de rede <br/>(demasiado**servidor de cópia de segurança**) | |TCP |TCP | |
| Protocolo de rede <br/>(demasiado**cofre dos serviços de recuperação**) |HTTPS |HTTPS |HTTPS |HTTPS |

![chave da tabela](./media/backup-introduction-to-azure-backup/table-key-2.png)

Olá extensão da VM (na VM do IaaS Olá) lê Olá dados diretamente a partir de Olá conta do storage do Azure através de rede de armazenamento Olá, pelo que não é necessário toocompress este tráfego.

Se utilizar um servidor do System Center DPM ou o servidor de cópia de segurança do Azure como um servidor secundário de cópia de segurança, comprima os dados de Olá vai do servidor de cópia de segurança de toohello do Olá servidor primário. A compressão de dados antes de realizar cópias de segurança tooDPM ou servidor de cópia de segurança do Azure, poupa largura de banda.

#### <a name="network-throttling"></a>Limitação de rede
agente de cópia de segurança do Azure Olá oferece a limitação de rede, que lhe permite toocontrol como largura de banda de rede é utilizada durante a transferência de dados. A limitação pode ser útil se precisar de tooback dos dados durante as horas de trabalho, mas não pretende que o processo de cópia de segurança de Olá toointerfere com outro tráfego de internet. Transferência de limitação para dados aplica-se tooback cópias de segurança e restaurar as atividades.

## <a name="backup-and-retention"></a>Cópia de segurança e retenção

O Azure Backup tem um limite de 9999 pontos de recuperação, também conhecidos como cópias de segurança ou instantâneos de cópia de segurança, por *nstância protegida*. Uma instância protegida é um computador, servidor (física ou virtual) ou carga de trabalho configurada tooback segurança tooAzure de dados. Para obter mais informações, consulte a secção de Olá, [o que é uma instância protegida](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Uma instância está protegida depois de uma cópia de segurança de dados ter sido guardada. Olá cópia de segurança dos dados é a proteção de Olá. Se os dados de origem Olá foi perdidos ou ter ficado danificados, a cópia de segurança de Olá foi restaurar dados de origem de Olá. Olá tabela seguinte mostra os frequência de cópia de segurança máximo Olá para cada componente. A configuração de política de cópia de segurança determina rapidez que consumir pontos de recuperação Olá. Por exemplo, se criar um ponto de recuperação por dia, pode manter os pontos de recuperação durante 27 anos antes de os esgotar. Se tirar um ponto de recuperação mensal, pode manter os pontos de recuperação anos 833 antes de executar a. Olá serviço de cópia de segurança não definir um limite de tempo de expiração num ponto de recuperação.

|  | Agente do Backup do Azure | System Center DPM | Servidor do Backup do Azure | Cópia de segurança da VM do IaaS do Azure |
| --- | --- | --- | --- | --- |
| Frequência de cópia de segurança<br/> (Cofre de serviços de tooRecovery) |Três cópias de segurança por dia |Duas cópias de segurança por dia |Duas cópias de segurança por dia |Uma cópia de segurança por dia |
| Frequência de cópia de segurança<br/> (toodisk) |Não aplicável |<li>A cada 15 minutos para o SQL Server <li>A cada hora para outras cargas de trabalho |<li>A cada 15 minutos para o SQL Server <li>A cada hora para outras cargas de trabalho</p> |Não aplicável |
| Opções de retenção |Diariamente, semanalmente, mensalmente, anualmente |Diariamente, semanalmente, mensalmente, anualmente |Diariamente, semanalmente, mensalmente, anualmente |Diariamente, semanalmente, mensalmente, anualmente |
| Número máximo de pontos de recuperação por instância protegida |9999|9999|9999|9999|
| Período de retenção máximo |Depende da frequência da cópia de segurança |Depende da frequência da cópia de segurança |Depende da frequência da cópia de segurança |Depende da frequência da cópia de segurança |
| Pontos de recuperação no disco local |Não aplicável |<li>64 para Servidores de Ficheiros<li>448 para Servidores de Aplicações |<li>64 para Servidores de Ficheiros<li>448 para Servidores de Aplicações |Não aplicável |
| Pontos de recuperação em banda |Não aplicável |Ilimitado |Não aplicável |Não aplicável |

## <a name="what-is-a-protected-instance"></a>O que é uma instância protegida
Uma instância protegida é um computador com o Windows tooa referência genérico, um servidor (física ou virtual) ou base de dados do SQL que foi configurado tooback segurança tooAzure. Uma instância está protegida depois de configurar uma política de cópia de segurança para o computador Olá, servidor ou base de dados e criar uma cópia de segurança dos dados de Olá. Subsequentes cópias dos dados de cópia de segurança de Olá para essa instância protegido (que são chamados pontos de recuperação), aumentar a quantidade de Olá de armazenamento consumida. Pode criar cópias de segurança too9999 pontos de recuperação para uma instância protegido. Se eliminar um ponto de recuperação do armazenamento, não contagem contra total de ponto de recuperação 9999 Olá.
Alguns exemplos comuns de instâncias protegidas são máquinas virtuais, servidores de aplicações, bases de dados e computadores pessoais com sistema de operativo do Windows hello. Por exemplo:

* Uma máquina virtual em execução Olá Hyper-V ou IaaS do Azure hipervisor recursos de infraestrutura. sistemas operativos de convidado de Olá para a máquina virtual de Olá pode ser Windows Server ou Linux.
* Um servidor de aplicações: servidor de aplicação Olá pode ser uma máquina física ou virtual com o Windows Server e cargas de trabalho com dados que necessita de toobe uma cópia de segurança. Cargas de trabalho comuns são Microsoft SQL Server, Microsoft Exchange server, Microsoft SharePoint server e função de servidor de ficheiros de Olá no Windows Server. tooback estas cargas de trabalho precisa de System Center Data Protection Manager (DPM) ou servidor de cópia de segurança do Azure.
* Um computador pessoal, estação de trabalho ou portátil com sistema de operativo do Windows hello.


## <a name="what-is-a-recovery-services-vault"></a>O que é um cofre dos Serviços de Recuperação?
Um cofre dos serviços de recuperação é que uma entidade de armazenamento online no Azure utilizada toohold dados como cópias de segurança, pontos de recuperação e as políticas de cópia de segurança. Pode utilizar dados de cópia de segurança dos serviços de recuperação cofres toohold para servidores no local e serviços do Azure e estações de trabalho. Os cofres dos serviços de recuperação tornam mais fácil tooorganize os dados de cópia de segurança, enquanto minimizam os custos gerais de gestão. Pode criar o número de cofres dos Serviços de Recuperação que quiser numa subscrição.

Cofres de cópia de segurança que são baseadas no Azure do Service Manager, foram versão primeiro de Olá do Cofre de Olá. Recuperação cofres dos serviços, que adiciona funcionalidades de modelo do Azure Resource Manager Olá, têm a versão de segundo Olá do Cofre de Olá. Consulte Olá [artigo de descrição geral do cofre dos serviços de recuperação](backup-azure-recovery-services-vault-overview.md) para obter uma descrição completa das diferenças de funcionalidade Olá. Já não pode criar utilize Olá portal toocreate cofres de cópia de segurança, mas ainda são suportados cofres de cópia de segurança.

> [!IMPORTANT]
> Agora pode atualizar os cópia de segurança cofres tooRecovery os cofres dos serviços. Para obter mais informações, consulte o artigo de Olá [atualizar um tooa do Cofre de cópia de segurança do cofre dos serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft encoraja tooupgrade a cópia de segurança cofres dos cofres dos serviços de tooRecovery.<br/> **15 de Outubro de 2017**, deixará de estar cofres de cópia de segurança do toouse capaz de PowerShell toocreate. <br/> **Até 1 de novembro de 2017**:
>- Qualquer restantes cofres de cópia de segurança serão os cofres dos serviços de tooRecovery automaticamente atualizado.
>- Não será capaz de tooaccess os dados de cópia de segurança no portal clássico Olá. Em vez disso, utilize Olá tooaccess portal do Azure os dados de cópia de segurança cofres dos serviços de recuperação.
>

## <a name="how-does-azure-backup-differ-from-azure-site-recovery"></a>Qual é a diferença entre o Backup do Azure e o Azure Site Recovery?
O Azure Backup e o Azure Site Recovery estão relacionados na medida em que ambos os serviços criam cópias de segurança dos dados e podem restaurá-los. No entanto, estes serviços servem objetivos diferentes ao oferecer continuidade empresarial e recuperação após desastre na sua empresa. Utilize tooprotect de cópia de segurança do Azure e restaurar dados a um nível mais granular. Por exemplo, se uma apresentação num computador portátil ter ficado danificada, teria de utilizar apresentação de Olá toorestore de cópia de segurança do Azure. Se quisesse configuração de Olá tooreplicate e os dados numa VM através de outro datacenter, utilize o Azure Site Recovery.

Cópia de segurança do Azure protege os dados no local e na nuvem de Olá. O Azure Site Recovery coordena a replicação da máquina virtual e do servidor físico, a ativação pós-falha e a reativação pós-falha. Ambos os serviços são importantes porque a sua solução de recuperação após desastre tem dos dados seguros e recuperáveis (cópia de segurança) tookeep *e* manter as cargas de trabalho disponíveis (recuperação de sites) quando ocorrem falhas.

os seguintes conceitos de Olá pode ajudar a tomar decisões importantes em torno da cópia de segurança e recuperação após desastre.

| Conceito | Detalhes | Cópia de segurança | Recuperação após desastre (DR) |
| --- | --- | --- | --- |
| Objetivo de ponto de recuperação (RPO) |quantidade de Olá de perda de dados aceitável se uma recuperação tiver toobe concluído. |As soluções de cópia de segurança têm uma grande variação no respetivo RPO aceitável. Normalmente, as cópias de segurança de máquinas virtuais têm um RPO de um dia, enquanto as cópias de segurança de bases de dados têm RPOs tão baixos como 15 minutos. |As soluções de recuperação após desastre têm RPOs baixas. Olá cópia da DR pode estar protegido por alguns segundos ou minutos. |
| Objetivo de tempo de recuperação (RTO) |Olá período de tempo que demora toocomplete uma recuperação ou restauro. |Devido a Olá RPO maior, a quantidade de Olá de dados que uma solução de cópia de segurança necessidades tooprocess é normalmente muito superior, que servem como toolonger RTOs. Por exemplo, pode demorar dias toorestore dados de bandas, consoante o tempo de Olá que demora a banda de Olá tootransport partir de uma localização fora das instalações. |As soluções de recuperação após desastre têm RTOs menores porque são estão mais sincronizadas com a origem de Olá. Alterações menos necessário toobe processado. |
| Retenção |Quanto dados precisam de toobe armazenado |Para cenários que necessitem de uma recuperação operacional (danos em dados, eliminação de ficheiros inadvertida, falha de SO), os dados de cópia de segurança são, normalmente, mantidos durante 30 dias ou menos.<br>A partir de um ponto de vista de compatibilidade, os dados poderão ter toobe armazenado durante meses ou mesmo anos. Dados de cópia de segurança são, idealmente, adequados para o arquivo nestes casos. |Recuperação após desastre tem apenas dados recuperação operacional, que normalmente demoram algumas horas ou cópia de segurança tooa dia. Devido à captura de dados detalhados Olá utilizada em soluções de DR, os dados de DR para a retenção de longo prazo não é recomendado utilizar. |

## <a name="next-steps"></a>Passos seguintes
Utilize um dos seguintes tutoriais para obter instruções detalhadas, passo a passo, para proteger dados no Windows Server ou proteger uma máquina virtual (VM) de Olá no Azure:

* [Fazer uma Cópia de Segurança de Ficheiros e Pastas](backup-try-azure-backup-in-10-mins.md)
* [Fazer uma Cópia de Segurança de Máquinas Virtuais do Azure](backup-azure-vms-first-look-arm.md)

Para obter detalhes sobre como proteger outras cargas de trabalho, veja um dos seguintes artigos:

* [Fazer uma cópia de segurança do seu Windows Server](backup-configure-vault.md)
* [Fazer uma cópia de segurança de cargas de trabalho de aplicações](backup-azure-microsoft-azure-backup.md)
* [Cópia de segurança das VMs IaaS do Azure](backup-azure-vms-prepare.md)

[green]: ./media/backup-introduction-to-azure-backup/green.png
[yellow]: ./media/backup-introduction-to-azure-backup/yellow.png
[red]: ./media/backup-introduction-to-azure-backup/red.png
