---
title: "aaaHow é o trabalho de recuperação de sites? | Microsoft Docs"
description: "Este artigo fornece uma descrição geral da arquitetura da Recuperação de Sites"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Como funciona o Azure Site Recovery para infraestruturas no local?

> [!div class="op_single_selector"]
> * [Replicar máquinas virtuais do Azure](site-recovery-azure-to-azure-architecture.md)
> * [Replicar máquinas no local](site-recovery-components.md)

Este artigo descreve a arquitetura subjacente do Olá [do Azure Site Recovery](site-recovery-overview.md) serviço e componentes de Olá que funcionam para replicar as cargas de trabalho do tooAzure no local.

Publique quaisquer comentários na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-tooazure"></a>Replicar tooAzure

Pode replicar e proteger Olá procedimentos seguintes no tooAzure de infraestrutura no local:

- **VMware**: VMs VMware no local em execução num [anfitrião suportado](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). É possível replicar VMs VMware que executam [sistemas operativos suportados](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
- **Hyper-V**: VMs Hyper-V no local em execução em [anfitriões suportados](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- **Máquinas físicas**: servidores físicos no local que executem o Windows ou Linux em [sistemas operativos suportados](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Pode replicar VMs Hyper-V que executem qualquer sistema operativo convidado [suportado pelo Hyper-V e o Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).

## <a name="vmware-tooazure"></a>TooAzure de VMware

Eis o que precisa para replicar VMs de VMware tooAzure.

Área | Componente | Detalhes
--- | --- | ---
**Servidor de configuração** | Um servidor de gestão único (VM VMware) executa todos os componentes no local - servidor de configuração, servidor de processos, servidor de destino mestre | servidor de configuração de Olá coordena as comunicações entre no local e o Azure e gere a replicação de dados.
 **Servidor de processos**:  | Instalado por predefinição no servidor de configuração de Olá. | Atua como um gateway de replicação. Recebe dados de replicação, otimiza-as com colocação em cache, compressão e encriptação e envia-tooAzure armazenamento.<br/><br/> servidor de processos de Olá também processa a instalação push de máquinas de tooprotected de serviço de mobilidade Olá e efetua a descoberta automática de VMs de VMware.<br/><br/> À medida que cresça a implementação pode adicionar mais processos dedicados independentes servidores toohandle aumentar volumes de tráfego de replicação.
 **Servidor de destino mestre** | Instalado por predefinição no servidor de configuração do Olá no local. | Processa dados de replicação durante a reativação pós-falha a partir do Azure.<br/><br/> Se os volumes de tráfego da reativação pós-falha forem elevados, pode implementar um servidor de destino mestre separado para a reativação pós-falha.
**Servidores de VMware** | VMs de VMware alojadas em servidores de ESXi vSphere e recomendamos um vCenter anfitriões do servidor toomanage Olá. | Adicionar servidores de VMware tooyour Cofre de serviços de recuperação.<br/><br/>
**Máquinas replicadas** | Olá serviço de mobilidade será instalado em cada VM pretende tooreplicate de VMware. Pode ser instalado manualmente em cada máquina ou com uma instalação push do servidor de processos de Olá.| -

**Figura 1: VMware tooAzure componentes**

![Componentes](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Processo de replicação

1. Configurar a implementação de Olá, incluindo os componentes do Azure e um cofre dos serviços de recuperação. No Cofre de Olá especificou de origem de replicação de Olá e de destino, configurar o servidor de configuração de Olá, adicionar servidores VMware, criar uma política de replicação, implementar o serviço de mobilidade Olá, ativar a replicação e executam uma ativação pós-falha de teste.
2.  Máquinas iniciam a replicação de acordo com a política de replicação de Olá, não sendo uma cópia inicial dos dados de Olá armazenamento tooAzure replicadas.
4. Começa a replicação de diferenças alterações tooAzure após a conclusão da replicação inicial Olá. As alterações registadas relativas a uma máquina são guardadas num ficheiro .hrl.
    - Replicação de máquinas comunicam com o servidor de configuração de Olá na porta HTTPS 443 entrada para a gestão de replicação.
    - Replicação de máquinas enviam servidor de processos de toohello de dados de replicação na porta HTTPS 9443 entrada (podem ser configuradas).
    - servidor de configuração de Olá orquestra a gestão de replicação com o Azure através da porta HTTPS 443 de saída.
    - servidor de processos de Olá recebe dados de máquinas de origem, otimiza e encripta- e envia-tooAzure armazenamento através da porta 443 saída.
    - Se ativar a consistência multi VM, em seguida, as máquinas no grupo de replicação de Olá comunicam entre si através da porta 20004. A consistência multi-VM é utilizada se agrupar várias máquinas em grupos de replicação que partilhem pontos de consistência de falhas e pontos de consistência de aplicação quando é efetuada a ativação pós-falha dos mesmos. Isto é útil se máquinas estão em execução Olá a mesma carga de trabalho e precisam de toobe consistente.
5. O tráfego é replicada tooAzure armazenamento pontos finais públicos, mais Olá internet. Em alternativa, pode utilizar o [peering público](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering) do Azure ExpressRoute. Replicar o tráfego através de uma VPN de site para site a partir de um tooAzure de site no local não é suportada.

**Figura 2: VMware tooAzure replicação**

![Melhorada](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Ativação pós-falha e reativação pós-falha

1. Depois de verificar que teste a ativação pós-falha está a funcionar conforme esperado, pode executar as ativações pós-falha não planeada tooAzure conforme necessário. A ativação pós-falha planeada não é suportada.
2. Pode efetuar a ativação pós-falha de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md), toofail através de várias VMs.
3. Quando executa uma ativação pós-falha, são criadas VMs de réplica no Azure. Consolidar uma ativação pós-falha toostart ao aceder aos Olá carga de trabalho a partir da réplica de Olá VM do Azure.
4. Quando o site no local primário estiver novamente disponível, pode fazer a reativação pós-falha. Configurar uma infraestrutura de reativação pós-falha, iniciar a replicação máquina Olá de Olá site secundário toohello primário e executar uma ativação pós-falha não planeada do site secundário Olá. Depois de consolidar esta ativação pós-falha, os dados serão back no local e terá tooenable replicação tooAzure novamente. [Saiba mais](site-recovery-failback-azure-to-vmware.md)

**Figura 3: Reativação pós-falha de VMware/servidor físico**

![Reativação pós-falha](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>TooAzure físico

Quando se replica tooAzure de servidores físicos no local, utiliza a replicação Olá também mesmo componentes e processos como [VMware tooAzure](#vmware-replication-to-azure), mas tenha em atenção estas diferenças:

- Pode utilizar um servidor físico para o servidor de configuração de Olá, em vez de uma VM de VMware
- Vai precisar de uma infraestrutura de VMware no local para a reativação pós-falha. Não pode falhar back tooa máquina física.

## <a name="hyper-v-tooazure"></a>TooAzure de Hyper-V

### <a name="replication-process"></a>Processo de replicação

1. Configurar Olá componentes do Azure. Recomendamos que configure as contas de armazenamento e de rede antes de iniciar a implementação do Site Recovery.
2. Cria um cofre dos Serviços de Replicação para o Site Recovery e configura as definições do cofre, incluindo:
    - Definições de origem e de destino. Se não estiver a gerir anfitriões Hyper-V numa nuvem VMM, para o destino de Olá, criar um contentor de sites do Hyper-V e adicione tooit de anfitriões Hyper-V. Anfitriões Hyper-V geridos no VMM, origem Olá estiver em nuvem do VMM de Olá. destino de Olá é o Azure.
    - Instalação de Olá fornecedor do Azure Site Recovery e agente dos serviços de recuperação do Microsoft Azure de Olá. Se tiver Olá VMM será instalado no mesmo fornecedor e Olá agente em cada anfitrião de Hyper-V. Se não tiver VMM, Olá fornecedor e o agente estão instalados em cada anfitrião.
    - Criar uma política de replicação para o site de Hyper-V Olá ou de nuvem VMM. política de Olá é VMs tooall aplicados localizadas em anfitriões do site de Olá ou na nuvem.
    - Ativa a replicação nas VMs de Hyper-V. Ocorre a replicação inicial em conformidade com as definições de política de replicação Olá.
4. As alterações de dados são registadas e começa a replicação de diferenças alterações tooAzure após a conclusão da replicação inicial Olá. As alterações registadas relativas a um item são guardadas num ficheiro .hrl.
5. Executar um toomake de ativação pós-falha de teste se tudo está a funcionar.

### <a name="failover-and-failback-process"></a>Processo de ativação pós-falha e de reativação pós-falha

1. Pode executar um planeadas ou imprevistas [ativação pós-falha](site-recovery-failover.md) de tooAzure de VMs de Hyper-V no local. Se executar uma ativação pós-falha planeada, em seguida, as VMs de origem são encerradas tooensure sem perda de dados.
2. Pode efetuar a ativação pós-falha de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) ativação pós-falha de tooorchestrate de várias máquinas.
4. Depois de executar a ativação pós-falha de Olá, deve ser Olá toosee capaz de criar as VMs da réplica no Azure. Pode atribuir um toohello de endereço IP público VM, se necessário.
5. Em seguida, consolidar toostart de ativação pós-falha de Olá aceder à carga de trabalho Olá da réplica de Olá VM do Azure.
6. Quando o site no local primário estiver novamente disponível, pode fazer a [reativação pós-falha](site-recovery-failback-from-azure-to-hyper-v.md). Pode iniciar uma ativação pós-falha planeada do site primário toohello do Azure. Para uma ativação pós-falha planeada que pode toofailback selecione toohello mesmo VM ou tooan alternativo de localização e sincronizar as alterações entre o Azure e no local, tooensure sem perda de dados. Quando as VMs são criadas no local, a consolidação de ativação pós-falha de Olá.

**Figura 4: A replicação de tooAzure de site Hyper-V**

![Componentes](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figura 5: TooAzure replicação de nuvens de Hyper-V no VMM**

![Componentes](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>Replicar site secundário tooa

Pode replicar Olá seguinte tooyour site secundário:

- **VMware**: VMs VMware no local em execução num [anfitrião suportado](site-recovery-support-matrix-to-sec-site.md#on-premises-servers). É possível replicar VMs VMware que executam [sistemas operativos suportados](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
- **Máquinas físicas**: servidores físicos no local que executem o Windows ou Linux em [sistemas operativos suportados](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: VMs Hyper-V no local em execução em [anfitriões Hyper-V suportados](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), geridos em clouds do VMM. [anfitriões suportados](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Pode replicar VMs Hyper-V que executem qualquer sistema operativo convidado [suportado pelo Hyper-V e o Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="vmwarephysical-tooa-secondary-site"></a>Tooa de VMware/físico de site secundário

Replicar VMs de VMware ou servidores físicos tooa secundário num site através de InMage Scout.

### <a name="components"></a>Componentes

**Área** | **Componente** | **Detalhes**
--- | --- | ---
**Servidor de processos** | Localizado no site primário | Implementar Olá processo servidor toohandle colocação em cache, compressão e otimização de dados.<br/><br/> Ele também faz a instalação push de Olá toomachines agente Unified pretende tooprotect.
**Servidor de configuração** | Localizado no site secundário | Gere o servidor de configuração de Olá, configurar e monitorizar a implementação, optar por utilizar o Web site da gestão Olá ou consola de vContinuum Olá.
**Servidor de vContinuum** | Opcional. Instalado no Olá mesma localização do servidor de configuração de Olá. | Fornece uma consola de gestão e monitorização do seu ambiente protegido.
**Servidor de destino mestre** | Localizado no site secundário Olá | servidor de destino mestre Olá contém dados replicados. Recebe dados do servidor de processos de Olá, cria uma máquina de réplica no site secundário Olá e detém Olá pontos de retenção de dados.<br/><br/> número de Olá de servidores de destino principal que tem de depende do número de Olá de máquinas que estiver a proteger.<br/><br/> Se pretender que o site primário de back-toohello toofail, precisa de um servidor de destino principal não existe demasiado. Olá agente Unified está instalado neste servidor.
**VMware ESX/ESXi e servidor vCenter** |  As VMs são alojadas em anfitriões ESX/ESXi. Os anfitriões são geridos com um servidor vCenter | É necessário um tooreplicate de infraestrutura do VMware VMs de VMware.
**VMs/servidores físicos** |  Agente instalado em VMs de VMware e servidores físicos que pretende tooreplicate de unificada. | agente de Olá atua como um fornecedor de comunicação entre todos os componentes de Olá.


### <a name="replication-process"></a>Processo de replicação

1. Configure servidores de componentes de Olá em cada site (configuração, processo, destino principal) e instale Olá agente Unified nas máquinas que pretende que o tooreplicate.
2. Após a replicação inicial, o agente de Olá em cada máquina envia servidor de processos de toohello de alterações de replicação de diferenças.
3. servidor de processos de Olá otimiza Olá dados e transfere-o servidor de destino mestre toohello no site secundário Olá. servidor de configuração de Olá gere o processo de replicação de Olá.

**Figura 6: VMware tooVMware replicação**

![TooVMware de VMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Site secundário tooa de Hyper-V

Eis o que precisa para replicar VMs Hyper-V tooa secundário site.


**Área** | **Componente** | **Detalhes**
--- | --- | ---
**Servidor VMM** | Recomenda-se um servidor VMM no site primário Olá e um no site secundário Olá | Cada servidor VMM deve ser toohello ligado à internet.<br/><br/> Cada servidor deve ter pelo menos um VMM nuvem privada, o com o conjunto de perfis de capacidade de Olá Hyper-V.<br/><br/> Instalar Olá fornecedor do Azure Site Recovery no servidor do VMM Olá. Olá fornecedor coordena e orquestra a replicação com Olá serviço de recuperação de sites através de Olá internet. As comunicações entre Olá fornecedor e o Azure são seguras e encriptadas.
**Servidor Hyper-V** |  Um ou mais servidores Hyper-V anfitrião em nuvens do VMM primárias e secundárias Olá.<br/><br/> Servidores devem ser toohello ligado à internet.<br/><br/> Dados são replicados entre Olá servidores primário e secundários Hyper-V anfitrião sobre Olá LAN ou VPN, utilizando o Kerberos ou autenticação de certificados.  
**VMs de Hyper-V** | Localizado no servidor de anfitrião de Hyper-V de origem Olá. | servidor de anfitrião de origem Olá deve ter, pelo menos, uma VM que pretende que o tooreplicate.

### <a name="replication-process"></a>Processo de replicação

1. Configurar Olá conta do Azure.
2. Cria um cofre dos Serviços de Replicação para o Site Recovery e configura as definições do cofre, incluindo:

    - origem de replicação de Olá e de destino (sites primários e secundários).
    - Instalação de Olá fornecedor do Azure Site Recovery e agente dos serviços de recuperação do Microsoft Azure de Olá. Olá fornecedor está instalado nos servidores do VMM e o agente de Olá em cada anfitrião de Hyper-V.
    - Cria uma política de replicação para a cloud do VMM de origem. política de Olá é aplicado tooall VMs localizadas em anfitriões na nuvem de Olá.
    - Ativa a replicação nas VMs de Hyper-V. Ocorre a replicação inicial em conformidade com as definições de política de replicação Olá.
4. As alterações de dados são registadas, replicação de diferenças alterações e toobegins após a conclusão da replicação inicial Olá. As alterações registadas relativas a um item são guardadas num ficheiro .hrl.
5. Executar um toomake de ativação pós-falha de teste se tudo está a funcionar.

**A figura 7: Replicação de tooVMM do VMM**

![No local tooon local](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Ativação pós-falha e reativação pós-falha

1. Executa uma [ativação pós-falha](site-recovery-failover.md) planeada ou não planeada entre os sites no local. Se executar uma ativação pós-falha planeada, em seguida, as VMs de origem são encerradas tooensure sem perda de dados.
2. Pode efetuar a ativação pós-falha de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md) ativação pós-falha de tooorchestrate de várias máquinas.
4. Se efetuar um ativação pós-falha não planeada tooa site secundário, depois de máquinas de ativação pós-falha de Olá na localização secundária Olá não são ativadas para proteção ou de replicação. Se executou uma ativação pós-falha planeada, após a ativação pós-falha de Olá, máquinas na localização secundária Olá estão protegidas.
5. Em seguida, a consolidação Olá ativação pós-falha toostart ao aceder aos Olá carga de trabalho da réplica de Olá VM.
6. Quando o site primário estiver novamente disponível, iniciar tooreplicate de replicação inversa do toohello de site secundário Olá primário. A replicação inversa coloca máquinas de virtuais Olá num estado protegido, mas o datacenter secundário Olá ainda é a localização do Active Directory Olá.
7. site primário de Olá toomake na localização de Active Directory Olá novamente, iniciar uma ativação pós-falha planeada do tooprimary secundária, seguido de outra replicação inversa.


## <a name="next-steps"></a>Passos seguintes

- [Saiba mais](site-recovery-hyper-v-azure-architecture.md) sobre o fluxo de trabalho do Hyper-V de Olá replicação.
- [Verificar pré-requisitos](site-recovery-prereq.md)
