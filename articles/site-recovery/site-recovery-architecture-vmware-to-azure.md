---
title: "aaaHow é o trabalho tooAzure de replicação de VMware no Azure Site Recovery? | Microsoft Docs"
description: "Este artigo fornece uma descrição geral da arquitetura de utilizada quando replicar no local as VMs VMware e servidores físicos tooAzure com Olá serviço Azure Site Recovery e componentes"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-architecture
ms.openlocfilehash: f0fb834f8b251640f97e4d0163b2b9e54de691e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-vmware-replication-tooazure-work-in-site-recovery"></a>Como funciona tooAzure de replicação de VMware no Site Recovery?

Este artigo descreve os componentes de Olá e processos envolvidos quando replicar no local tooAzure de máquinas virtuais e servidores físicos Windows/Linux, do VMware com Olá [do Azure Site Recovery](site-recovery-overview.md) serviço.

Quando se replica tooAzure de servidores físicos no local, utiliza a replicação também Olá, mesmo componentes e processos como replicação de VM de VMware, com estas diferenças:

- Pode utilizar um servidor físico para o servidor de configuração de Olá, em vez de uma VM de VMware.
- Vai precisar de uma infraestrutura de VMware no local para a reativação pós-falha. Não pode falhar back tooa máquina física.

Publique quaisquer comentários na parte inferior deste artigo hello, ou colocar questões no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Componentes da arquitetura

Existem vários componentes envolvidos quando replicar VMs de VMware e servidores físicos tooAzure.

**Componente** | **Localização** | **Detalhes**
--- | --- | ---
**Azure** | No Azure, precisa de uma conta do Azure, de uma conta de armazenamento do Azure e de uma rede do Azure. | Dados replicados são guardados na conta do storage Olá e as VMs do Azure são criadas com dados Olá replicado quando ocorre a ativação pós-falha do seu site no local. Olá VMs do Azure ligar toohello rede virtual do Azure quando são criados.
**Servidor de configuração** | Um único-local no servidor de gestão (VMWare VM) que executa todos os componentes de local de Olá que são necessárias para a implementação de Olá, incluindo o servidor de configuração de Olá, o servidor de processos, o servidor de destino mestre | componente de servidor de configuração de Olá coordena as comunicações entre no local e o Azure e gere a replicação de dados.
 **Servidor de processos**:  | Instalado por predefinição no servidor de configuração de Olá. | Atua como um gateway de replicação. Recebe dados de replicação, otimiza-as com colocação em cache, compressão e encriptação e envia-tooAzure armazenamento.<br/><br/> servidor de processos de Olá também processa a instalação push de máquinas de tooprotected de serviço de mobilidade Olá e efetua a descoberta automática de VMs de VMware.<br/><br/> À medida que cresça a implementação pode adicionar mais processos dedicados independentes servidores toohandle aumentar volumes de tráfego de replicação.
 **Servidor de destino mestre** | Instalado por predefinição no servidor de configuração do Olá no local. | Processa dados de replicação durante a reativação pós-falha a partir do Azure.<br/><br/> Se os volumes de tráfego da reativação pós-falha forem elevados, pode implementar um servidor de destino mestre separado para a reativação pós-falha.
**Servidores de VMware** | VMs de VMware alojadas em servidores de ESXi vSphere e recomendamos um vCenter anfitriões do servidor toomanage Olá. | Adicionar servidores de VMware tooyour Cofre de serviços de recuperação.
**Máquinas replicadas** | Olá serviço de mobilidade será instalado em cada VM pretende tooreplicate de VMware. Pode ser instalado manualmente em cada máquina ou com uma instalação push do servidor de processos de Olá.

Saiba mais sobre os pré-requisitos de implementação de Olá e os requisitos para cada um destes componentes no Olá [matriz de suporte](site-recovery-support-matrix-to-azure.md).

**Figura 1: VMware tooAzure componentes**

![Componentes](./media/site-recovery-components/arch-enhanced.png)

## <a name="replication-process"></a>Processo de replicação

1. Configurar a implementação de Olá, incluindo os componentes do Azure e um cofre dos serviços de recuperação. No Cofre de Olá especificou de origem de replicação de Olá e de destino, configurar o servidor de configuração de Olá, adicionar servidores VMware, criar uma política de replicação, implementar o serviço de mobilidade Olá, ativar a replicação e executam uma ativação pós-falha de teste.
2.  Máquinas iniciam a replicação de acordo com a política de replicação de Olá, não sendo uma cópia inicial dos dados de Olá armazenamento tooAzure replicadas.
4. Começa a replicação de diferenças alterações tooAzure após a conclusão da replicação inicial Olá. As alterações registadas relativas a uma máquina são guardadas num ficheiro .hrl.
    - Replicação de máquinas comunicam com o servidor de configuração de Olá na porta HTTPS 443 entrada para a gestão de replicação.
    - Replicação de máquinas enviam servidor de processos de toohello de dados de replicação na porta HTTPS 9443 entrada (podem ser configuradas).
    - servidor de configuração de Olá orquestra a gestão de replicação com o Azure através da porta HTTPS 443 de saída.
    - servidor de processos de Olá recebe dados de máquinas de origem, otimiza e encripta- e envia-tooAzure armazenamento através da porta 443 saída.
    - Se ativar a consistência multi VM, em seguida, as máquinas no grupo de replicação de Olá comunicam entre si através da porta 20004. A consistência multi-VM é utilizada se agrupar várias máquinas em grupos de replicação que partilhem pontos de consistência de falhas e pontos de consistência de aplicação quando é efetuada a ativação pós-falha dos mesmos. Isto é útil se máquinas estão em execução Olá a mesma carga de trabalho e precisam de toobe consistente.
5. O tráfego é replicada tooAzure armazenamento pontos finais públicos, mais Olá internet. Em alternativa, pode utilizar o [peering público](../expressroute/expressroute-circuit-peerings.md#public-peering) do Azure ExpressRoute. Replicar o tráfego através de uma VPN de site para site a partir de um tooAzure de site no local não é suportada.

**Figura 2: VMware tooAzure replicação**

![Melhorada](./media/site-recovery-components/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Processo de ativação pós-falha e de reativação pós-falha

1. Depois de verificar que teste a ativação pós-falha está a funcionar conforme esperado, pode executar as ativações pós-falha não planeada tooAzure conforme necessário. A ativação pós-falha planeada não é suportada.
2. Pode efetuar a ativação pós-falha de um único computador ou criar [planos de recuperação](site-recovery-create-recovery-plans.md), toofail através de várias VMs.
3. Quando executa uma ativação pós-falha, são criadas VMs de réplica no Azure. Consolidar uma ativação pós-falha toostart ao aceder aos Olá carga de trabalho a partir da réplica de Olá VM do Azure.
4. Quando o site no local primário estiver novamente disponível, pode fazer a reativação pós-falha. Configurar uma infraestrutura de reativação pós-falha, iniciar a replicação máquina Olá de Olá site secundário toohello primário e executar uma ativação pós-falha não planeada do site secundário Olá. Depois de consolidar esta ativação pós-falha, os dados serão back no local e terá tooenable replicação tooAzure novamente. [Saiba mais](site-recovery-failback-azure-to-vmware.md)

Existem alguns requisitos para a reativação pós-falha:


- **Servidor de processo temporário no Azure**: Se pretender toofail novamente a partir do Azure após a ativação pós-falha, precisará tooset se uma VM do Azure como um servidor de processos, toohandle replicação a partir do Azure. É possível eliminar esta VM após a conclusão da reativação pós-falha.
- **Ligação VPN**: para reativação pós-falha, terá uma ligação VPN (ou Azure ExpressRoute) configurada a partir da site no local do Olá rede Azure toohello.
- **Servidor de destino principal independente no local**: servidor de destino mestre Olá no local processa a reativação pós-falha. servidor de destino mestre Olá é instalado por predefinição no servidor de gestão de Olá, mas se está a reativar maiores volumes de tráfego deve configurar um servidor de destino principal independente no local para esta finalidade.
- **Política de reativação pós-falha**: tooreplicate back tooyour no local site, precisa de uma política de reativação pós-falha. Esta foi criada automaticamente quando criou a política de replicação.
- **Infraestrutura do VMware**: terá de ser novamente tooan no local VM de VMware. Isto significa que terá de uma infraestrutura de VMware no local, mesmo se está a replicar tooAzure de servidores físicos no local.

**Figura 3: Reativação pós-falha de VMware/servidor físico**

![Reativação pós-falha](./media/site-recovery-components/enhanced-failback.png)


## <a name="next-steps"></a>Passos seguintes

Olá revisão [matriz de suporte](site-recovery-support-matrix-to-azure.md)
