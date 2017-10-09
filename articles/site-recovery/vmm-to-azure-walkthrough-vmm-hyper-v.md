---
title: "aaaPrepare System Center VMM para tooAzure de replicação de Hyper-V | Microsoft Docs"
description: "Descreve como servidor do System Center VMM tooprepare para tooAzure de replicação de Hyper-V, utilizando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Passo 6: Preparar servidores VMM e anfitriões Hyper-V para tooAzure de replicação de Hyper-V

Depois de configurar [componentes do Azure](vmm-to-azure-walkthrough-prepare-azure.md) para implementação de Olá, utilize instruções Olá na toointeract de anfitriões Hyper-V e servidores VMM do artigo tooprepare no local com o Azure Site Recovery.

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou coloque questões técnicas no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>Preparar servidores VMM

- É necessário pelo menos um servidor VMM que cumpre os requisitos de suporte de Olá para replicação de recuperação de sites (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- Certifique-se de já preparou servidor do VMM Olá para [mapeamento da rede](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Certifique-se de que o servidor VMM Olá pode aceder a estes URLs

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Se tiver regras de firewall baseadas no endereço IP, certifique-se de que permitem comunicação tooAzure.
- Permitir Olá [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e Olá porta HTTPS (443).
- Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).

Durante a implementação da recuperação de sites, Olá fornecedor da recuperação de Site de transferir e instalá-lo em cada servidor VMM. servidor do VMM Olá é registado no Cofre de serviços de recuperação de Olá.




## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 7: criar um cofre](vmm-to-azure-walkthrough-create-vault.md)

