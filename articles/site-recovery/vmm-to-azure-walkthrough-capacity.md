---
title: "aaaPlan capacidade e dimensionamento de VM de Hyper-V tooAzure de replicação (com o VMM) com o Azure Site Recovery | Microsoft Docs"
description: Utilizar esta capacidade de tooplan artigo e escala quando replicar VMs de Hyper-V no VMM nuvens tooAzure, com o Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a>Passo 3: Planear a capacidade e dimensionamento para replicação de tooAzure do Hyper-V (com o VMM)

Depois de ter revisto Olá [os pré-requisitos de implementação](vmm-to-azure-walkthrough-prerequisites.md), utilize este toofigure artigo saída planeamento de capacidade e dimensionamento, quando replicar no local VMs de Hyper-V no tooAzure de nuvens do System Center Virtual Machine Manager (VMM), com [do Azure Site Recovery](site-recovery-overview.md).

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou coloque questões técnicas no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>Como começar a planear a capacidade?


Recolher informações sobre o seu ambiente de replicação e, em seguida, capacidade de plano utilizando dados Olá, juntamente com considerações de Olá realçados neste artigo.


## <a name="gather-information"></a>Reunir informações

1. Recolher informações sobre o ambiente de replicação, incluindo VMs, discos por VMs e armazenamento por disco.
2. Identifica a taxa de alteração (renovação) diária para os dados replicados. Transferir Olá [ferramenta o planeamento de capacidade do Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) taxa de alteração de Olá tooget. Recomendamos que execute esta ferramenta através de uma semana toocapture médias.
 

## <a name="figure-out-capacity"></a>Descobrir a capacidade

Com base nas informações de Olá tiver recolha, executar Olá [ferramenta de Planeador de capacidade de recuperação de sites](http://aka.ms/asr-capacity-planner-excel) tooanalyze o ambiente de origem e cargas de trabalho, estimar necessidades de largura de banda e de recursos do servidor de localização de origem Olá e Olá recursos (máquinas virtuais e armazenamento, etc.), que necessita na localização de destino Olá. Pode executar a ferramenta de Olá em alguns dos modos de:

- Planear rápido: execute a ferramenta de Olá neste modo projeções de rede e o servidor de tooget com base num número médio de VMs, discos, armazenamento e a taxa de alteração.
- Detalhadas de planeamento: execute a ferramenta de Olá neste modo e forneça detalhes de cada carga de trabalho ao nível da VM. Analisar a compatibilidade da VM e obter projeções de rede e servidor.

Agora, execute a ferramenta de Olá:

1. Transferir Olá [ferramenta](http://aka.ms/asr-capacity-planner-excel)
2. Planeador de rápida Olá toorun, siga [estas instruções](site-recovery-capacity-planner.md#run-the-quick-planner)e o cenário de Olá selecione **tooAzure de Hyper-V**.
3. toorun Olá Planeador de detalhado, siga [estas instruções](site-recovery-capacity-planner.md#run-the-detailed-planner)e o cenário de Olá selecione **Hyper-V tooAzure**.

## <a name="control-network-bandwidth"></a>Largura de banda de rede de controlo

Depois de ter largura de banda Olá calculada que precisa, tem duas opções para controlar Olá quantidade de largura de banda utilizada na replicação:

* **Limitar largura de banda**: tráfego do Hyper-V que replica tooAzure passa através de um anfitrião Hyper-V específico. Pode limitar a largura de banda no servidor de anfitrião Olá.
* **Influenciar a largura de banda**: pode influenciar a largura de banda Olá utilizada na replicação através de um par de chaves de registo.

### <a name="throttle-bandwidth"></a>Limitar largura de banda
1. Abra Olá MMC da cópia de segurança do Microsoft Azure snap-in no servidor de anfitrião do Hyper-V Olá. Por predefinição, um atalho para cópia de segurança do Microsoft Azure está disponível no ambiente de trabalho Olá ou em c:\Programas\Microsoft c:\Programas\Microsoft Azure Recovery Services agent\bin\wabadmin..
2. No snap-in Olá clique **alterar propriedades**.
3. No Olá **limitação** separador selecione **ativar a limitação para operações de cópia de segurança de utilização de largura de banda de internet**e definir limites de Olá para o trabalho e de descanso horas. Intervalos válidos são de Kbps 512 too102 Mbps, por segundo.

    ![Limitar largura de banda](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

Também pode utilizar Olá [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação. Exemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que não é necessária nenhuma limitação.

### <a name="influence-network-bandwidth"></a>Influência da largura de banda de rede
1. No registo de Olá navegue demasiado**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tráfego de largura de banda de Olá tooinfluence num disco replicação, modificar Olá de valor de Olá **UploadThreadsPerVM**, ou crie a chave de Olá, se não existir.
   * largura de banda do tooinfluence Olá para tráfego de reativação pós-falha a partir do Azure, modifique o valor de Olá **DownloadThreadsPerVM**.
2. valor predefinido de Olá é 4. Numa rede "sobreaprovisionada", estas chaves do registo devem ser Olá valores predefinidos alteradas. Olá máximo é 32. Monitorizar o valor de Olá toooptimize de tráfego.

## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 4: planear o funcionamento em rede](vmm-to-azure-walkthrough-network.md).
