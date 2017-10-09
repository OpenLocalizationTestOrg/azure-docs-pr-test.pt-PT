---
title: "aaaOperations arquitetura de gestão. o conjunto (OMS) | Microsoft Docs"
description: "O Microsoft Operations Management Suite (OMS) é a solução de gestão de TI baseada na nuvem da Microsoft que o ajuda a gerir e a proteger a sua infraestrutura no local e na nuvem.  Este artigo identifica os serviços de diferentes Olá incluídos no OMS e fornece ligações tootheir detalhadas conteúdo."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>Arquitetura de OMS
O [Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) é uma coleção de serviços baseados na nuvem para gerir os seus ambientes no local e na nuvem.  Este artigo descreve Olá diferentes no local e componentes de nuvem do OMS e da sua arquitetura de informática em nuvem de nível elevado.  Pode consultar a documentação toohello para cada serviço para obter mais detalhes.

## <a name="log-analytics"></a>Log Analytics
Todos os dados recolhidos pelo [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) é armazenado no repositório OMS Olá que está alojado no Azure.  Origens ligadas geram dados recolhidos no repositório do Olá OMS.  Atualmente, existem três tipos de origens de dados ligadas.

* Um agente instalado um [Windows](../log-analytics/log-analytics-windows-agents.md) ou [Linux](../log-analytics/log-analytics-linux-agents.md) computador diretamente ligado tooOMS.
* Um grupo de gestão do System Center Operations Manager (SCOM) [ligado tooLog análise](../log-analytics/log-analytics-om-agents.md) .  Agentes do SCOM continuam toocommunicate com servidores de gestão que reencaminhar eventos e dados de desempenho tooLog análise.
* Uma [conta de armazenamento do Azure](../log-analytics/log-analytics-azure-storage.md) que recolhe dados do [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) a partir de uma função de trabalho, função Web ou máquina virtual no Azure.

Origens de dados definem os dados de Olá que recolhe de análise de registos de origens ligadas, incluindo os registos de eventos e contadores de desempenho.  Soluções facilmente podem ser adicionadas tooyour área de trabalho de Olá e adicionar a funcionalidade tooOMS [OMS soluções galeria](../log-analytics/log-analytics-add-solutions.md).  Algumas soluções podem exigir um tooLog de ligação direta de análise de agentes do SCOM, enquanto outros podem exigir um toobe adicionais agente instalado.

Análise de registos tem um portal baseado na web que pode utilizar os recursos OMS toomanage, adicionar e configurar soluções do OMS e ver e analisar dados no repositório OMS Olá.

![Arquitetura do Log Analytics de elevado nível](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Automatização do Azure
[Os runbooks de automatização do Azure](http://azure.microsoft.com/documentation/services/automation) são executados no Olá em nuvem do Azure e pode aceder a recursos que se encontrem no Azure, nos outros serviços em nuvem ou acessível a partir do Olá Internet pública.  Também pode designar máquinas no local no seu centro de dados locais com o [Função de Trabalho de Runbook Híbrida](../automation/automation-hybrid-runbook-worker.md) para que os runbooks podem aceder a recursos locais.

[Configurações de DSC](../automation/automation-dsc-overview.md) armazenados na automatização do Azure pode ser máquinas de virtuais tooAzure diretamente aplicado.  Outras máquinas virtuais e físicas pode solicitar as configurações do servidor de solicitação do Automation DSC do Azure Olá.

A automatização do Azure tem uma solução OMS que mostra as estatísticas e liga toolaunch Olá portal do Azure para quaisquer operações.

![Arquitetura de Automatização do Azure de elevado nível](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Azure Backup
Os dados protegidos na [Azure Backup](http://azure.microsoft.com/documentation/services/backup) são armazenados num cofre de cópias de segurança localizado numa região geográfica específica.  Olá os dados são replicados no Olá mesma região e, dependendo do tipo de Olá de cofre, também pode ser replicada tooanother região para a redundância adicional.

A Cópia de Segurança do Azure tem três cenários fundamentais.

* Máquinas Windows com a Cópia de Segurança do Azure.  Isto permite-lhe toobackup ficheiros e pastas a partir de qualquer Windows server ou o cliente diretamente tooyour Cofre de cópia de segurança do Azure.  
* System Center Data Protection Manager (DPM) ou Servidor do Microsoft Azure Backup. Isto permite-lhe tooleverage DPM ou o servidor de cópia de segurança do Microsoft Azure toobackup ficheiros e pastas além tooapplication cargas de trabalho, tais como o armazenamento de toolocal SQL e SharePoint e, em seguida, replicar tooyour Cofre de cópia de segurança do Azure.
* Extensões da Máquina Virtual do Azure.  Isto permite-lhe toobackup máquinas virtuais do Azure tooyour Cofre de cópia de segurança do Azure.

Cópia de segurança do Azure tem uma solução OMS que mostra as estatísticas e liga toolaunch Olá portal do Azure para quaisquer operações.

![Arquitetura do Azure Backup de elevado nível](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
O [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) programa a replicação, ativação pós-falha e reativação pós-falha de máquinas virtuais e servidores físicos. Dados de replicação são trocados entre anfitriões Hyper-V, hipervisores do VMware e servidores físicos nos centros de dados primários e secundários, ou entre Olá Centro de dados e de armazenamento do Azure.  O Site Recovery armazena metadados em cofres localizados numa região geográfica específica do Azure. Não existem dados replicados são guardados por Olá serviço de recuperação de Site.

O Azure Site Recovery tem três cenários de replicação fundamentais.

**Replicação de máquinas virtuais de Hyper-V**

* Se as máquinas virtuais de Hyper-V geridas em nuvens VMM, pode replicar tooa secundário center ou tooAzure o armazenamento de dados.  Replicação tooAzure é através de uma ligação de internet segura.  Centro de dados secundário replicação tooa é Olá LAN.
* Se as máquinas virtuais de Hyper-V não são geridas pelo VMM, pode replicar tooAzure armazenamento apenas.  Replicação tooAzure é através de uma ligação de internet segura.

**Replicar máquinas virtuais VMWare**

* Pode replicar VMware máquinas virtuais tooa datacenter secundário com armazenamento de VMware ou tooAzure.  Replicação tooAzure pode ocorrer ao longo de um site para site VPN ou Azure ExpressRoute ou através de uma ligação de Internet segura. Datacenter secundário de tooa de replicação ocorre através de Olá canal de dados do InMage Scout.

**Replicação de servidores físicos do Windows e Linux** 

* Pode replicar servidores físicos tooa datacenter ou tooAzure armazenamento secundário. Replicação tooAzure pode ocorrer ao longo de um site para site VPN ou Azure ExpressRoute ou através de uma ligação de Internet segura. Datacenter secundário de tooa de replicação ocorre através de Olá canal de dados do InMage Scout.  O Azure Site Recovery tem uma solução OMS apresenta algumas estatísticas, mas tem de utilizar Olá portal do Azure para quaisquer operações.

![Arquitetura do Azure Site Recovery de elevado nível](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre o [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Saiba mais sobre o [Automatização do Azure](https://azure.microsoft.com/documentation/services/automation).
* Saiba mais sobre o [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Saiba mais sobre o [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

