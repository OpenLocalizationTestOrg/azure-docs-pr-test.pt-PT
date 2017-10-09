---
title: "aaaPrerequisites para replicação tooAzure utilizando o Azure Site Recovery | Microsoft Docs"
description: "Saiba mais sobre Olá pré-requisitos para replicar as VMs e máquinas físicas tooAzure utilizando o serviço do Azure Site Recovery Olá."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>Pré-requisitos para a replicação do tooAzure no local utilizando a recuperação de Site

> [!div class="op_single_selector"]
> * [Replicar a partir do tooAzure do Azure](site-recovery-azure-to-azure-prereq.md)
> * [Replicar a partir do tooAzure no local](site-recovery-prereq.md)

O Azure Site Recovery pode ajudar a suportar a sua estratégia de recuperação (BCDR) de continuidade e desastre negócio através da orquestração da replicação de uma máquina virtual do Azure (VM) de tooanother região do Azure. Recuperação de site também replica servidores físicos no local e as VMs toohello nuvem (Azure) ou datacenter secundário tooa. Se ocorrer uma falha na sua localização principal, pode efetuar a ativação pós-falha de tooa localização secundária tookeep aplicações e cargas de trabalho disponíveis. Pode efetuar a localização primária de back-tooyour quando a localização principal Olá devolve toonormal operações. Para mais informações sobre a recuperação de sites, consulte [que é o Site Recovery?](site-recovery-overview.md).

Neste artigo, vamos resumem Olá pré-requisitos para iniciar a replicação de recuperação de Site a partir de um tooAzure de máquina no local.

Pode publicar quaisquer comentários na parte inferior de Olá artigo Olá. Também pode colocar questões técnicas no Olá [fórum do Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="azure-requirements"></a>Requisitos do Azure

**Requisito** | **Detalhes**
--- | ---
**Conta do Azure** | A [conta do Microsoft Azure](http://azure.microsoft.com/). Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
**O serviço de recuperação do site** | Para obter mais informações sobre preços para Olá serviço Azure Site Recovery, consulte [preços da recuperação de Site](https://azure.microsoft.com/pricing/details/site-recovery/). |
**Armazenamento do Azure** | É necessário um toostore replicado dados da conta de armazenamento do Azure. conta de armazenamento Olá tem de constar Olá mesma região que Olá do cofre dos serviços de recuperação do Azure. As VMs do Azure são criadas quando ocorre a ativação pós-falha.<br/><br/> Consoante o modelo de recursos de Olá pretende toouse para ativação pós-falha da VM do Azure, pode configurar uma conta através da utilização de Olá [modelo de implementação Azure Resource Manager](../storage/common/storage-create-storage-account.md) ou Olá [modelo de implementação clássica](../storage/common/storage-create-storage-account.md).<br/><br/>Pode utilizar o [armazenamento georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage) ou o armazenamento localmente redundante. Recomendamos o armazenamento georredundante. Com o armazenamento georredundante, dados são resilientes se ocorrer uma falha regional ou se não é possível recuperar a região primária Olá.<br/><br/> Pode utilizar uma conta de armazenamento do Azure standard ou pode utilizar o Premium Storage do Azure. [Armazenamento Premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) é normalmente utilizado para as VMs que necessitam de uma forma consistente de elevado desempenho de e/s e a latência baixa. Armazenamento premium, uma VM pode alojar cargas de trabalho de I/O intensivo. Se utilizar o armazenamento premium para os dados replicados, também vai precisar de uma conta de armazenamento standard. Uma conta de armazenamento standard armazena os registos de replicação que capturam as alterações em curso tooon de dados local.<br/><br/>
**Limitações de armazenamento** | Não é possível mover as contas de armazenamento que utiliza no grupo de recursos diferente do Site Recovery tooa ou mover tooor utilização com outra subscrição.<br/><br/> Atualmente, replicar toopremium contas do storage no Sul da Índia e Índia Central no não está disponível.
**Rede do Azure** | Precisa de uma rede do Azure, as VMs do Azure de toowhich ligar após a ativação pós-falha. Olá rede do Azure tem de constar Olá mesma região que Olá do cofre dos serviços de recuperação.<br/><br/> No portal do Azure Olá, pode criar uma rede do Azure utilizando Olá [modelo de implementação do Resource Manager](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ou Olá [modelo de implementação clássica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).<br/><br/> Se replicar a partir do System Center Virtual Machine Manager (VMM) tooAzure, tem de configurar o mapeamento de rede entre redes de VM do VMM e redes do Azure. Isto garante que as VMs do Azure ligar redes tooappropriate após a ativação pós-falha.
**Limitações de rede** | Não é possível mover a contas de rede que utiliza no grupo de recursos diferente do Site Recovery tooa ou mover tooor utilização com outra subscrição.
**Mapeamento da rede** | Se replicar VMs de Hyper-V do Microsoft em nuvens VMM, tem de configurar o mapeamento de rede. Isto garante que as VMs do Azure ligar redes tooappropriate quando são criados após a ativação pós-falha.

> [!NOTE]
> Olá secções seguintes descrevem Olá pré-requisitos para vários componentes do ambiente de cliente Olá. Para obter mais informações sobre o suporte para configurações específicas, consulte Olá [matriz de suporte](site-recovery-support-matrix.md).
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>Recuperação após desastre de VMs de VMware ou tooAzure de servidores físico Windows ou Linux
Olá, os seguintes componentes é necessário para recuperação após desastre de VMs de VMware ou servidores físicos do Windows ou Linux. Além disso são toohello aqueles descrito em [requisitos do Azure](#azure-requirements).


### <a name="configuration-server-or-additional-process-server"></a>Servidor de configuração ou o servidor de processos adicionais

Configure uma máquina no local como Olá configuração servidor tooorchestrate a comunicação entre sites no local de Olá e do Azure. máquina no local de Olá também gere a replicação de dados. <br/></br>

*   **VMware vCenter ou vSphere anfitrião pré-requisitos**

    | **Componente** | **Requisitos** |
    | --- | --- |
    | **vSphere** | Tem de ter um ou mais hipervisores vSphere de VMware.<br/><br/>Hipervisores devem executar o vSphere versão 6.0, 5.5 ou 5.1, com Olá atualizações mais recentes.<br/><br/>Recomendamos que anfitriões vSphere e servidores do vCenter que ambos de estar no Olá mesmo de rede como servidor de processos de Olá. A menos que tiver configurado a um servidor de processos dedicados, esta é a rede olá onde está localizado o servidor de configuração de Olá. |
    | **vCenter** | Recomendamos que implemente um toomanage do VMware vCenter server seus anfitriões vSphere. Tem de executar vCenter versão 6.0 ou 5.5, com as atualizações mais recentes do Olá.<br/><br/>**Limitação**: recuperação de sites não suporta a replicação entre instâncias do vCenter vMotion. Armazenamento DRS e armazenamento vMotion também não são suportadas uma VM de destino principal após uma operação de reproteção.||

* **Pré-requisitos de máquina replicada**

    | **Componente** | **Requisitos** |
    | --- | --- |
    | **No local máquinas** (VMs de VMware) | VMs replicadas tem de ter as ferramentas do VMware instalado e em execução.<br/><br/> As VMs têm de cumprir [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) para criar uma VM do Azure.<br/><br/>Capacidade do disco em cada máquina protegida não pode ser superior a 1,023 GB. <br/><br/>Um mínimo, 2 GB de espaço disponível na unidade de instalação de Olá é necessária para instalação de componentes.<br/><br/>Se quiser tooenable consistência de várias VMS, porta 20004 terá de ser aberta na firewall local do Olá VM.<br/><br/>Os nomes de computador tem de ser entre 1 e 63 carateres (pode utilizar letras, números e hífenes). nome de Olá tem de começar com uma letra ou número e terminar com uma letra ou número. <br/><br/>Depois de ativar a replicação para uma máquina, pode modificar Olá nome do Azure.<br/><br/> |
    | **Máquinas Windows** (física ou VMware) | Olá máquina tem de executar um dos seguintes Olá suportados sistemas operativos de 64 bits: <br/>-Windows Server 2012 R2<br/>-Windows Server 2012<br/>-Windows Server 2008 R2 com SP1 ou uma versão posterior<br/><br/> Olá sistema operativo tem de ser instalada no disco de SO de Olá da unidade C. tem de ser um disco básico do Windows e não dinâmica. o disco de dados de Olá pode ser dinâmico.<br/><br/>|
    | **Computadores Linux** (física ou VMware) | Olá máquina tem de executar um dos seguintes Olá suportados sistemas operativos de 64 bits: <br/>-Red Hat Enterprise Linux 7.2, 7.1, 6.8 ou 6.7<br/>-Centos 7.2, 7.1, 7.0, 6.8, 6.7, 6.6 ou 6.5<br/>-Servidor Ubuntu 14.04 LTS (para obter uma lista das versões suportadas do kernel para Ubuntu, consulte [sistemas operativos suportados](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions))<br/>-Kernel de compatível com o Enterprise Linux 6.5 ou 6.4, em execução ou Olá Red Hat oracle ou Unbreakable Enterprise Kernel versão 3 (UEK3)<br/>-SUSE Linux Enterprise Server 11 SP4 ou SP3 do SUSE Linux Enterprise Server 11<br/><br/>Os ficheiros de /etc/hosts nas máquinas protegidas tem de ter entradas que mapeiam Olá anfitrião local nome tooIP endereços associados a todos os adaptadores de rede.<br/><br/>Após a ativação pós-falha, se quiser tooconnect tooan VM do Azure que está a executar Linux utilizando um cliente Secure Shell (SSH), certifique-se de que o serviço SSH Olá na máquina de Olá protegido é definido toostart automaticamente no início do sistema. Certifique-se também que as regras de firewall permitem uma máquina de toohello protegido de ligação SSH.<br/><br/>nome de anfitrião Olá, pontos de montagem, nomes de dispositivos e caminhos de sistema de Linux e os nomes de ficheiros (por exemplo, /etc/ e /usr) tem de ser em inglês apenas.<br/><br/>Olá seguintes diretórios (se configurar como partições separadas ou sistemas de ficheiros) têm de estar todos no Olá mesmo disco (disco Olá SO) no servidor de origem Olá:<br/>- / (raiz)<br/>- / arranque<br/>-/usr<br/>-/ usr/local<br/>-/var<br/>- / etc<br/><br/>Atualmente, funcionalidades de v5 XFS, como a soma de verificação de metadados, não são suportadas pela recuperação de sites em sistemas de ficheiros XFS. Certifique-se de que os sistemas de ficheiros XFS não estiverem a utilizar quaisquer funcionalidades v5. Pode utilizar superblock XFS de Olá toocheck Olá xfs_info utilitário para a partição de Olá. Se **ftype** estiver definido demasiado**1**, as funcionalidades de v5 XFS estão a ser utilizadas.<br/><br/>Nos servidores Red Hat Enterprise Linux 7 e CentOS 7, o utilitário de lsof Olá tem de ser instalado e disponível.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Recuperação após desastre de tooAzure de VMs de Hyper-V (sem VMM)

Olá, os seguintes componentes é necessário para recuperação após desastre de VMs de Hyper-V em nuvens VMM. Além disso são toohello aqueles descrito em [requisitos do Azure](#azure-requirements).

| **Pré-requisito** | **Detalhes** |
| --- | --- |
| **Anfitrião Hyper-V** |Um ou mais servidores no local devem executar o Windows Server 2012 R2 com as atualizações mais recentes Olá e função de Hyper-V Olá ativada ou Microsoft Hyper-V Server 2012 R2.<br/><br/>Servidores Hyper-V tem de ter uma ou mais VMs.<br/><br/>Servidores Hyper-V tem de ser toohello ligado à Internet, diretamente ou através de um proxy.<br/><br/>Servidores Hyper-V tem de ter correções Olá descritas no artigo da Base de dados de conhecimento Olá [2961977](https://support.microsoft.com/kb/2961977) instalado.
|**Fornecedor e agente**| Durante a implementação da recuperação de Site, instale o fornecedor do Azure Site Recovery Olá. instalação do fornecedor de Olá também instala o agente de Azure Recovery Services Olá em cada servidor de Hyper-V que esteja a executar as VMs que pretende tooprotect. <br/><br/>Todos os servidores de Hyper-V no cofre tem de ter uma recuperação de Site Olá mesmas versões do fornecedor de Olá e o agente de Olá.<br/><br/>fornecedor de Olá tem tooconnect tooSite recuperação através de Olá Internet. Tráfego pode ser enviado diretamente ou através de um proxy. Proxy baseado em HTTPS não é suportada. servidor de proxy de Olá têm de permitir toohello acesso os seguintes URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>Se tiver regras de firewall baseadas no endereço IP no servidor de Olá, certifique-se de que as regras de Olá permitem tooAzure de comunicação.<br/><br/> Permitir Olá [intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e HTTPS (porta 443).<br/><br/> Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para Olá E.U.A. Tsunami (utilizado para gestão de identidade e controlo de acesso).


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>Recuperação após desastre de VMs de Hyper-V no VMM nuvens tooAzure

Olá, os seguintes componentes é necessário para recuperação após desastre de VMs de Hyper-V em nuvens VMM. Além disso são toohello aqueles descrito em [requisitos do Azure](#azure-requirements).

| **Pré-requisito** | **Detalhes** |
| --- | --- |
| **O Virtual Machine Manager** |Tem de ter um ou mais servidores VMM em execução no System Center 2012 R2 ou uma versão posterior. Cada servidor VMM tem de ter um ou mais nuvens configuradas. <br/><br/>Uma nuvem tem de ter:<br/>-Um ou mais grupos de anfitriões VMM.<br/>-Um ou mais servidores de anfitrião Hyper-V ou clusters em cada grupo anfitrião.<br/><br/>Para obter mais informações sobre como configurar as nuvens do VMM, consulte [como toocreate uma nuvem no Virtual Machine Manager 2012](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx). |
| **Hyper-V** |Servidores de anfitrião Hyper-V tem de estar em execução, pelo menos, Windows Server 2012 R2 com a função de Olá Hyper-V ativada ou Microsoft Hyper-V Server 2012 R2. atualizações mais recentes Olá tem de estar instaladas.<br/><br/> Um servidor de Hyper-V tem de ter uma ou mais VMs.<br/><br/> Um servidor anfitrião Hyper-V ou cluster que inclui VMs que pretende que o tooreplicate tem de ser gerido numa nuvem VMM.<br/><br/>Servidores Hyper-V tem de ser toohello ligado à Internet, diretamente ou através de um proxy.<br/><br/>Servidores Hyper-V tem de ter correções Olá descritas no artigo da Base de dados de conhecimento Olá [2961977](https://support.microsoft.com/kb/2961977) instalado.<br/><br/>Servidores de anfitrião Hyper-V tem acesso à Internet para tooAzure de replicação de dados. |
| **Fornecedor e agente** |Durante a implementação do Azure Site Recovery, instale o fornecedor do Azure Site Recovery no servidor do VMM Olá. Instale o agente de serviços de recuperação nos anfitriões Hyper-V. Olá fornecedor e agente necessita tooconnect tooAzure diretamente através de Olá Internet ou através de um proxy. Os proxies baseados em HTTPS não são suportados. servidor de proxy de Olá no servidor do VMM Olá e anfitriões Hyper-V deve permitir acesso a: <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Se tiver regras de firewall baseadas no endereço IP no servidor do VMM Olá, certifique-se de que as regras de Olá permitem tooAzure de comunicação.<br/><br/> Permitir Olá [intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e HTTPS (porta 443).<br/><br/>Permita intervalos de endereços IP para Olá região do Azure para a sua subscrição e para E.U.A. Tsunami Olá (utilizado para gestão de identidade e controlo de acesso).<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>Pré-requisitos de máquina replicada

| **Componente** | **Detalhes** |
| --- | --- |
| **VMs protegidas** | Recuperação de sites suporta todos os sistemas operativos que são suportados pelo [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).<br/><br/>As VMs têm de cumprir Olá [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) para criar uma VM do Azure. Os nomes de computador tem de ser entre 1 e 63 carateres (pode utilizar letras, números e hífenes). nome de Olá tem de começar com uma letra ou número e terminar com uma letra ou número. <br/><br/>Pode modificar o nome da VM Olá depois de ativar a replicação para Olá VM. <br/><br/> Capacidade do disco para cada máquina protegida não pode ser superior a 1,023 GB. Uma VM pode ter segurança discos too16 (cópia de segurança too16 TB).<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>Recuperação após desastre de VMs de Hyper-V no site de propriedade de cliente do VMM nuvens tooa

Olá, os seguintes componentes é necessário para recuperação após desastre de VMs de Hyper-V no site pertencentes ao cliente tooa nuvens VMM. Além disso são toohello aqueles descrito em [requisitos do Azure](#azure-requirements).

| **Componente** | **Detalhes** |
| --- | --- |
| **O Virtual Machine Manager** |  Recomendamos que implemente um servidor do VMM no site primário Olá e o site secundário Olá.<br/><br/> Pode [replicar entre nuvens num único servidor VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). tooreplicate entre nuvens num único servidor VMM, precisa de, pelo menos, dois nuvens configuradas no servidor do VMM Olá.<br/><br/> Servidores do VMM tem de estar em execução, pelo menos, System Center 2012 SP1, com as atualizações mais recentes do Olá.<br/><br/> Cada servidor VMM tem de ter uma ou mais nuvens. Todas as nuvens têm de ter Olá que conjunto de perfis de capacidade do Hyper-V. <br/><br/>As nuvens têm de ter um ou mais grupos de anfitriões do VMM. Para obter mais informações sobre como configurar as nuvens do VMM, consulte [preparar para a implementação do Azure Site Recovery](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric). |
| **Hyper-V** | Servidores Hyper-V tem de estar em execução, pelo menos, Windows Server 2012 com a função de Olá Hyper-V ativada e ter Olá atualizações mais recentes instaladas.<br/><br/> Um servidor de Hyper-V tem de ter uma ou mais VMs.<br/><br/>  Servidores de anfitrião Hyper-V tem de estar localizados em grupos de anfitriões em nuvens do VMM primárias e secundárias Olá.<br/><br/> Se executar o Hyper-V num cluster no Windows Server 2012 R2, recomendamos que instale a atualização de Olá descrita no artigo da Base de dados de conhecimento [2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Se executar o Hyper-V num cluster no Windows Server 2012 e tiver um cluster de baseadas no endereço IP estático, não é criado automaticamente um mediador de clusters. Tem de configurar manualmente o Mediador de clusters de Olá. Para mais informações sobre o Mediador de clusters de Olá, consulte [configurar função de Mediador de réplicas Olá para replicação cluster a cluster](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Fornecedor** | Durante a implementação da recuperação de Site, instale o fornecedor do Azure Site Recovery Olá nos servidores VMM. fornecedor de Olá comunica com a recuperação de Site através de replicação de tooorchestrate HTTPS (porta 443). Ocorre a replicação de dados entre Olá servidores primário e secundários Hyper-V através de Olá LAN ou através de uma ligação VPN.<br/><br/> fornecedor de Olá que está em execução no servidor do VMM Olá precisa de aceder toohello os seguintes URLs:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>fornecedor da recuperação de Site Olá têm de permitir a comunicação de firewall de Olá VMM servidores toohello [intervalos IP do datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e permitir que o protocolo HTTPS (porta 443) de Olá. |


## <a name="url-access"></a>Acesso de URL
Estes URLs têm de estar disponíveis de servidores de anfitrião do VMware, o VMM e o Hyper-V:

|**URL** | **O VMM tooVMM** | **O VMM tooAzure** | **TooAzure de Hyper-V** | **TooAzure de VMware** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | Permitir | Permitir | Permitir | Permitir |
|``*.backup.windowsazure.com`` | Não necessário | Permitir | Permitir | Permitir |
|``*.hypervrecoverymanager.windowsazure.com`` | Permitir | Permitir | Permitir | Permitir |
|``*.store.core.windows.net`` | Permitir | Permitir | Permitir | Permitir |
|``*.blob.core.windows.net`` | Não necessário | Permitir | Permitir | Permitir |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | Não necessário | Não necessário | Não necessário | Permitir a transferência do SQL Server |
|``time.windows.com`` | Permitir | Permitir | Permitir | Permitir|
|``time.nist.gov`` | Permitir | Permitir | Permitir | Permitir |
