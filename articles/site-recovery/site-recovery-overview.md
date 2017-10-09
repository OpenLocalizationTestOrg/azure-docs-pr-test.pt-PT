---
title: "aaaWhat é o Azure Site Recovery? | Microsoft Docs"
description: "Fornece uma descrição geral de Olá serviço Azure Site Recovery e resume os cenários de implementação."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>O que é a Recuperação de Sites?

Bem-vindo toohello serviço de Azure Site Recovery! Este artigo fornece uma rápida descrição geral do serviço de Olá.

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Continuidade do negócio e recuperação após desastre (BCDR) com os Serviços de Recuperação do Azure

Como uma organização necessita de toofigure enviados como que vai tookeep os dados seguros e aplicações/cargas de trabalho em execução quando planeada e falhas não planeadas ocorrerem.

Serviços de recuperação do Azure a estratégia BCDR tooyour contribuir:

- **O serviço de Recuperação de Sites**: o Site Recovery ajuda a garantir a continuidade do negócio, mantendo as aplicações em execução em VMs e os servidores físicos disponíveis, se um site ficar em baixo. Recuperação de site são replicados cargas de trabalho em execução em VMs e servidores físicos, para que estes permanecem disponíveis numa localização secundária se o site primário Olá não está disponível. Recupera a cargas de trabalho toohello site primário quando está a funcionar e execute novamente.
- **Serviço de cópia de segurança**: Além disso, Olá [cópia de segurança do Azure](https://docs.microsoft.com/azure/backup/) serviço mantém os seus dados seguros e recuperáveis ao realizar cópias de segurança tooAzure.

O Site Recovery pode gerir a replicação de:

- VMs do Azure a replicarem entre regiões do Azure.
- No local e servidores físicos a replicar tooAzure ou site secundário tooa de máquinas virtuais.


## <a name="what-does-site-recovery-provide"></a>O que proporciona o Site Recovery?

**Funcionalidade** | **Detalhes**
--- | ---
**Implementar uma solução BCDR simples** | Utilizar a recuperação de sites, pode configurar e gerir a replicação, a ativação pós-falha e a reativação pós-falha a partir de uma única localização no Olá portal do Azure.
**Replicar VMs do Azure** | Pode configurar a sua estratégia BCDR, de forma a que as VMs do Azure sejam replicadas entre regiões do Azure.
**Replicar VMs locais fora do local** | Pode replicar VMs no local e servidores físicos tooAzure ou tooa secundário localização no local. Replicação tooAzure elimina Olá custo e a complexidade de manter um datacenter secundário.
**Replicar qualquer carga de trabalho** | Pode replicar qualquer carga de trabalho em execução em VMs do Azure, VMs Hyper-V no local, VMs VMware e servidores físicos do Windows/Linux suportados.
**Manter os dados resiliente e seguros** | A recuperação de sites orquestra a replicação, sem intercetar dados da aplicação. Dados replicados são guardados no armazenamento do Azure, com resiliência Olá que proporciona. Quando ocorre a ativação pós-falha, as VMs do Azure são criadas com base nos dados de Olá replicado.
**Cumprir os RTOs e RPOs** | Mantenha os objetivos de tempo de recuperação (RTO) e os objetivos de ponto de recuperação (RPO) dentro dos limites da organização. O Site Recovery fornece replicação contínua para as VMs do Azure e as VMs VMware, e frequência de replicação de apenas 30 segundos para Hyper-V. Pode reduzir ainda mais os objetivos de tempo de recuperação (RTO), integrando com a integração do [Gestor de Tráfego do Azure](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/).
**Manter as aplicações consistentes durante uma ativação pós-falha** | Pode configurar pontos de recuperação com instantâneos consistentes com a aplicação. Os instantâneos consistentes com a aplicação capturam os dados do disco, todos os dados na memória e todas as transações em processamento.
**Testar sem interrupções** | Pode facilmente executar as ativações pós-falha de teste toosupport simulações de recuperação de desastre, sem afetar a replicação em curso.
**Executar ativações pós-falha flexíveis** | Pode executar as ativações pós-falha planeadas para as falhas esperadas sem nenhuma perda de dados ou as ativações pós-falha não planeadas com perda mínima de dados (dependendo da frequência de replicação), perante desastres inesperados. Facilmente pode falhar back tooyour site primário quando se encontra disponível novamente.
**Criar planos de recuperação** | Pode personalizar e sequenciar a ativação pós-falha e a recuperação de aplicações multicamada em várias VMs, com planos de recuperação. Pode agrupar as máquinas em planos e adicionar scripts e ações manuais. Os planos de recuperação podem ser integrados nos runbooks de automatização do Azure.
**Integrar com tecnologias BCDR existentes** | O Site Recovery integra-se com outras tecnologias BCDR. Por exemplo, pode utilizar a recuperação de sites tooprotect Olá do SQL Server back-end de cargas de trabalho empresariais, incluindo suporte nativo para o SQL Server AlwaysOn, toomanage Olá ativação pós-falha dos grupos de disponibilidade.
**Integrar com a biblioteca de automatização Olá** | Uma biblioteca de Automatização do Azure completa fornece scripts específicos de aplicação, prontos para produção, que podem ser transferidos e integrados com o Site Recovery.
**Gerir definições de rede** | O Site Recovery integra-se no Azure com uma gestão simples da rede de aplicações, incluindo a reserva de endereços IP, a configuração de balanceadores de carga e a integração do Gestor de Tráfego do Azure para alternância de rede eficiente.


## <a name="what-can-i-replicate"></a>O que posso replicar?

**Suportado** | **Detalhes**
--- | ---
**O que posso replicar?** | VMs do Azure entre regiões do Azure (em pré-visualização)<br/><br/>  As VMs de VMware, VMs de Hyper-V, tooAzure servidores físicos (Windows e Linux) no local < br /<br/> No local as VMs de VMware, VMs de Hyper-V, site secundário do tooa servidores físicos. Site secundário do replicação tooa só é suportado para VMs de Hyper-V, se os anfitriões Hyper-V são geridos pelo System Center VMM.
**Que regiões são suportadas pelo Site Recovery?** | [Regiões suportadas](https://azure.microsoft.com/regions/services/) |
**Quais são os sistemas operativos de que as máquinas replicadas precisam?** | [Requisitos de VMs do Azure](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)<br></br>[Requisitos de VMs VMware](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> Para VMs Hyper-V, qualquer [SO convidado](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) suportado pelo Azure e Hyper-V é suportado.<br/><br/> [Requisitos do servidor físico](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**De que servidores/anfitriões de VMware preciso?** | As VMs VMware podem estar localizadas em [servidores de anfitriões vSphere/VCenter suportados](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)
**Que cargas de trabalho posso replicar?** | Pode replicar qualquer carga de trabalho em execução numa máquina de replicação suportada. Além disso, a utilização de equipa de recuperação de Site Olá efetuou a específico da aplicação de teste para um [número de aplicações](site-recovery-workload.md#workload-summary).


## <a name="azure-portal-considerations"></a>Considerações sobre o portal do Azure

* Recuperação de sites pode ser implementada em Olá [portal do Azure](https://portal.azure.com).
* No portal clássico do Azure Olá, pode gerir a recuperação de sites com o modelo de gestão de serviços clássico Olá.
- portal clássico Olá só deve ser toomaintain utilizadas implementações de recuperação de Site existentes. Não é possível criar novos cofres no portal clássico Olá.

## <a name="next-steps"></a>Passos seguintes
* Leia mais sobre o [suporte de cargas de trabalho](site-recovery-workload.md)
* Introdução ao [replicação de VM do Azure entre regiões](site-recovery-azure-to-azure.md), [tooAzure de replicação de VMware](vmware-walkthrough-overview.md), ou [tooAzure de replicação de Hyper-V](hyper-v-site-walkthrough-overview.md).
