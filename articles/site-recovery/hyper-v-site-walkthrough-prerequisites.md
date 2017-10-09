---
title: "Pré-requisitos de Olá de aaaReview para replicação de tooAzure Hyper-V (sem VMM do System Center) utilizando o Azure Site Recovery | Microsoft Docs"
description: "Descreve Olá pré-requisitos para configurar a replicação, ativação pós-falha e recuperação de tooAzure de VMs de Hyper-V no local com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>Passo 2: Consultar Olá pré-requisitos para replicação de tooAzure do Hyper-V (sem VMM)

Pré-requisitos de Olá estão resumidos na tabela de Olá.


**Pré-requisito** | **Detalhes** 
--- | --- 
**Azure** | Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).
**Servidores no local** | [Saiba mais](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sobre os requisitos para anfitriões de Hyper-V Olá no local.
**VMs de Hyper-V no local** | As VMs que pretende tooreplicate devem estar a executar um [sistema operativo suportado](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs do Azure** | Anfitriões Hyper-V tem de aceder toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se tiver regras de firewall baseadas no endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e Olá porta HTTPS (443).<br/></br> Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).



## <a name="next-steps"></a>Passos seguintes

- Se estiver a fazer uma implementação completa, aceda demasiado[passo 3: planear a capacidade](hyper-v-site-walkthrough-capacity.md)
- Se estiver a fazer uma implementação de teste simples, aceda demasiado[passo 4: planear o funcionamento em rede](hyper-v-site-walkthrough-network.md).
