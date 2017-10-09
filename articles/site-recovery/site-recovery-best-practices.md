---
title: "os procedimentos de recuperação de Site aaaAzure | Microsoft Docs"
description: "Este artigo descreve as melhores práticas para implementação do Azure Site Recovery"
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Obter toodeploy pronto do Azure Site Recovery

Este artigo descreve como tooprepare para a implementação do Azure Site Recovery.

## <a name="protecting-hyper-v-virtual-machines"></a>Proteger máquinas virtuais de Hyper-V

Tem duas opções de implementação para proteger máquinas virtuais de Hyper-V. Pode replicar tooAzure de Hyper-VMs no local ou datacenter secundário tooa. Cada implementação tem requisitos diferentes.

**Requisito** | **Replicar tooAzure (com o VMM)** | **Replicar VMs Hyper-V tooAzure (sem VMM)** | **Replicar VMs Hyper-V toosecondary site (com o VMM)** | **Detalhes**
---|---|---|---|---
**VMM** | VMM em execução no System Center 2012 R2 <br/><br/>Pelo menos, uma cloud do VMM que contenha um ou mais grupos de anfitriões VMM. | ND | Servidores do VMM no Olá primária e secundária Web sites em execução, pelo menos, System Center 2012 SP1 com as atualizações mais recentes. <br/><br/> Pelo menos, uma cloud em cada servidor VMM. As nuvens devem ter o conjunto de perfis de capacidade de Hyper-V de Olá.<br/><br/> nuvem de origem Olá deve ter pelo menos um grupo de anfitriões VMM. | Opcional. Não precisa de toohave que System Center VMM implementado na ordem tooreplicate Hyper-V máquinas virtuais tooAzure mas se o fizer terá toomake se de que o servidor do VMM Olá está corretamente configurada. Que inclui certificando-se de que está a executar a versão do VMM direita Olá e que estão configuradas nuvens.
**Hyper-V** | Pelo menos um servidor de anfitrião de Hyper-V no site do Olá no local com o Windows Server 2012 R2 ou posterior | Pelo menos um servidor de Hyper-V em sites de origem e destino de Olá em execução, pelo menos, Windows Server 2012 com as atualizações mais recentes do Olá instalado e ligado toohello internet.<br/><br/> servidores de Hyper-V Olá têm de estar num grupo de anfitriões numa nuvem VMM. | Pelo menos um servidor de Hyper-V em sites de origem e destino de Olá em execução, pelo menos, Windows Server 2012 com as atualizações mais recentes do Olá instalado e ligado toohello internet.<br/><br/> servidores de Hyper-V Olá tem de estar localizados num grupo de anfitriões numa nuvem VMM. |
**Máquinas virtuais** | Pelo menos uma VM no servidor de anfitrião do Hyper-V de origem Olá | Pelo menos uma VM no servidor de anfitrião de Hyper-V de Olá na origem de Olá nuvem VMM | Pelo menos uma VM no servidor de anfitrião de Hyper-V de Olá na origem de Olá nuvem VMM. |  VMs replicar tooAzure devem estar em conformidade com os pré-requisitos de máquina virtual do Azure
**Conta do Azure** | Precisará de uma conta do Azure e um serviço de recuperação de sites de toohello de subscrição. | Precisará de uma conta do Azure e um serviço de recuperação de sites de toohello de subscrição. | ND | Se não tiver uma conta, comece com uma avaliação gratuita.
**Armazenamento do Azure** | Precisa de uma subscrição numa conta de armazenamento no Azure que tenha a georreplicação ativada. | Precisa de uma subscrição numa conta de armazenamento no Azure que tenha a georreplicação ativada. | ND | conta de Olá deve estar no Olá mesma região que o cofre do Azure Site Recovery Olá e estar associado a Olá mesma subscrição.
**Redes** | Configurar tooensure de mapeamento de rede que todas as máquinas que efetuar a ativação pós-falha no Olá mesma rede do Azure pode ligar tooeach outro, independentemente do plano de recuperação onde se encontram no. Além disso se um gateway de rede está configurado no destino Olá rede do Azure, as máquinas virtuais podem ligar tooother máquinas virtuais no local. Se não configurar a rede mapeamento apenas as máquinas com ativação pós-falha no Olá pode ligar o mesmo plano de recuperação. | ND |  <br/><br/>Configure tooensure de mapeamento de rede que as máquinas virtuais estão ligados tooappropriate redes após a ativação pós-falha e de que as máquinas virtuais de réplica ideal são colocadas em servidores de anfitrião do Hyper-V. Se não configurar rede máquinas replicadas de mapeamento não será ligada tooany rede VM após a ativação pós-falha. |  tooset segurança mapeamento da rede com o VMM, terá toomake certificar-se de que o VMM lógico e redes VM estão corretamente configuradas.
**Fornecedores e agentes** | Durante a implementação irá instalar Olá fornecedor do Azure Site Recovery nos servidores VMM. Nos servidores de Hyper-V em nuvens VMM irá instalar o agente de Azure Recovery Services Olá. | Durante a implementação, instalará Olá fornecedor do Azure Site Recovery e agente dos serviços de recuperação do Azure de Olá num servidor de anfitrião do Hyper-V Olá ou cluster| Durante a implementação irá instalar Olá fornecedor do Azure Site Recovery nos servidores VMM. Nos servidores de Hyper-V em nuvens VMM irá instalar o agente de Azure Recovery Services Olá. | Fornecedores e agentes tooSite recuperação através de Olá de ligar à internet através de uma ligação HTTPS encriptada. Não tem exceções de firewall tooadd ou criar um proxy para ligação de fornecedor Olá específico.
**Ligação à Internet** | Apenas os servidores VMM Olá precisam de uma ligação à internet | Apenas Olá servidores de anfitrião de Hyper-V precisam de uma ligação à internet | Só os servidores VMM precisam de ligação à Internet | Máquinas virtuais não precisa de qualquer item instalado nos mesmos e não se ligue diretamente toohello internet.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>Proteger máquinas virtuais de VMware ou servidores físicos

Tem duas opções de implementação para proteger máquinas virtuais de VMware ou servidores físicos do Windows/Linux. Pode replicá-los tooAzure ou datacenter secundário tooa. Cada implementação tem requisitos diferentes.

**Requisito** | **Replicar VMs/físico de VMware servidores tooAzure)** | * **Site de toosecondary de servidores do replicar VMs de VMware/físico**  
---|---|---
**Site primário** | **Servidor de processos**: um servidor Windows dedicado (físico ou virtual) | **Servidor de processos**: um servidor Windows dedicado (físico ou máquina virtual de VMware)<br/><br/>  
**Site no local secundário** | ND | **Servidor de configuração**: um servidor Windows dedicado (físico ou virtual) <br/><br/> **Servidor de destino mestre**: um servidor dedicado (físico ou virtual). Configure com máquinas do Windows tooprotect Windows ou Linux tooprotect Linux.
**Azure** | **Subscrição**: irá precisar de uma subscrição para Olá serviço de recuperação de Site. <br/><br/> **Conta de armazenamento**: precisa de uma conta de armazenamento com a georreplicação ativada. conta de Olá deve estar no Olá mesma região que Olá Cofre de recuperação de sites e estar associado a Olá mesma subscrição. <br/><br/> **Servidor de configuração**: irá precisar de tooset segurança do servidor de configuração de Olá como uma VM do Azure <br/><br/> **Servidor de destino mestre**: irá precisar de tooset segurança do servidor de destino mestre Olá como uma VM do Azure <br/><br/> Configure com máquinas do Windows tooprotect Windows ou Linux tooprotect Linux.<br/><br/> **Rede virtual do Azure**: irá precisar de uma Azure virtual network na qual Olá serão implementados o servidor de configuração e o servidor de destino principal. Deve ser Olá mesma subscrição e região cofre do Azure Site Recovery Olá | ND  
**Máquinas virtuais/servidores físicos** | Pelo menos, uma máquina virtual de VMware ou servidor físico do Windows/Linux<br/><br/>Durante a implementação Olá serviço de mobilidade será instalado em cada máquina| Pelo menos, uma VM de VMware ou servidor físico do Windows/Linux.<br/><br/> Durante a implementação do agente Unified de Olá está instalado em cada máquina.




## <a name="azure-virtual-machine-requirements"></a>Requisitos das máquinas Virtuais do Azure

Pode implementar máquinas virtuais tooreplicate recuperação de sites e servidores físicos a executar qualquer sistema operativo suportado pelo Azure. Estes incluem a maioria das versões do Windows e do Linux. Irá necessitar de toomake Certifique-se que as máquinas virtuais que pretende que o tooprotect em conformidade com os requisitos do Azure no local.


## <a name="optimizing-your-deployment"></a>Otimizar a implementação

Utilize Olá seguintes sugestões toohelp otimizar e dimensionar a sua implementação.

- **Tamanho do volume de sistema operativo**: Quando replicar o Olá de tooAzure uma máquina virtual volume de sistema de operativo tem de ser inferior a 1 TB. Se tiver mais volumes do que isto, pode manualmente movê-los tooa outro disco antes de começar a implementação.
- **Tamanho do disco de dados**: Se estiver a replicar tooAzure pode ter segurança too32 discos de dados numa máquina virtual, cada um com um máximo de 1 TB. Pode replicar e fazer a ativação pós-falha eficazmente de máquinas virtuais com aproximadamente 32 TB.
- **Os limites do plano de recuperação**: recuperação de sites pode dimensionar toothousands de máquinas virtuais. Planos de recuperação são concebidos como um modelo para as aplicações que deve efetuar a ativação pós-falha em conjunto, de modo que limitam o número de Olá de máquinas de um too50 do plano de recuperação.
- **Limites do serviço do Azure**: cada subscrição do Azure inclui um conjunto de limites predefinidos relativos a núcleos, serviços cloud, etc. Recomendamos que execute uma disponibilidade do teste de ativação pós-falha toovalidate Olá de recursos na sua subscrição. Pode modificar estes limites através do suporte do Azure.
- **Planeamento da capacidade**: planeie o dimensionamento e o desempenho.
- **Largura de banda de replicação**: se tiver pouca largura de banda, tenha em conta que:
    - **ExpressRoute**: o Site Recovery funciona com o Azure ExpressRoute e otimizadores WAN, como o Riverbed.
    - **Tráfego de replicação**: recuperação de Site utiliza efetua uma replicação inicial inteligente utilizando apenas os blocos de dados e não Olá VHD completo. Durante a replicação contínua, só são replicadas as alterações.
    - **Tráfego de rede**: pode controlar o tráfego de rede utilizado para replicação ao configurar o QoS do Windows com uma política com base no endereço IP de destino Olá e porta.  Além disso, se estiver a replicar tooAzure recuperação de sites com o agente do Backup do Azure Olá. Pode configurar a limitação para esse agente.
- **RTO**: Se pretender toomeasure Olá tempo objetivo de recuperação (RTO) que pode esperar com a recuperação de Site sugerimos que execute uma ativação pós-falha de teste e vista tooanalyze de tarefas de recuperação de Site Olá quanto tempo demora toocomplete operações Olá. Se estiver a efetuar a ativação pós-falha tooAzure, para Olá RTO melhor, recomendamos que automatizar todas as ações manuais através da integração com a automatização do Azure e recuperação esquemas.
- **O RPO**: recuperação de sites suporta um objetivo de ponto de recuperação quase síncrona (RPO), quando se replica tooAzure. Tal pressupõe uma largura de banda suficiente entre o seu datacenter e o Azure.
