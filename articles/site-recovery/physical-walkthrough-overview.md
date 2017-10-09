---
title: "aaaReplicate físicos no local tooAzure de servidores com o Azure Site Recovery | Microsoft Docs"
description: "Fornece uma descrição geral dos passos de Olá para replicar as cargas de trabalho em execução no tooAzure de servidores físicos Windows/Linux no local com Olá serviço Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Replicar servidores físicos tooAzure com a recuperação de Site

Este artigo fornece uma descrição geral de Olá passos tooreplicate necessária no local Windows/Linux servidores físicos tooAzure, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço no Olá portal do Azure.


## <a name="step-1-review-architecture-and-prerequisites"></a>Passo 1: Rever pré-requisitos e arquitetura

Antes de iniciar a implementação, reveja a arquitetura do cenário de Olá e certifique-se de que compreende a todos os componentes de Olá tem tooset com a implementação de Olá.

Aceda demasiado[passo 1: rever a arquitetura de Olá](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Passo 2: Pré-requisitos de revisão

Certifique-se de que tem os pré-requisitos de Olá local para cada componente de implementação:

- **Pré-requisitos do Azure**: precisará de uma conta do Microsoft Azure, as redes do Azure e as contas de armazenamento.
- **Componentes da recuperação de Site local**: precisa de uma máquina com componentes da recuperação de Site no local.
- **Replicar máquinas**: tem de servidores que pretende tooreplicate toocomply no local e requisitos do Azure.

Aceda demasiado[passo 2: consultar pré-requisitos e limitações](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Passo 3: Capacidade de plano

Se estiver a fazer uma implementação completa tem toofigure saída que recursos de replicação tem. Se estiver a fazer uma rápida configurar tootest Olá ambiente, pode ignorar este passo.

Aceda demasiado[passo 3: planear a capacidade](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Passo 4: Planear o funcionamento em rede

É necessário toodo algum planeamento tooensure VMs do Azure são toonetworks ligado, após a ocorrência da ativação pós-falha, e que têm Olá direita endereços IP da rede.

Aceda demasiado[passo 4: planear o funcionamento em rede](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Passo 5: Preparar os recursos do Azure

Configure redes do Azure e de armazenamento antes de começar. 

Aceda demasiado[passo 5: preparar o Azure](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>Passo 6: Configurar um cofre

Configurar um tooorchestrate do Cofre de serviços de recuperação e gerir a replicação. Quando configurar o Cofre de Olá, especifique de que pretende tooreplicate, e onde pretende tooreplicate para.

Aceda demasiado[passo 6: configurar um cofre](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>Passo 7: Configurar definições de origem e de destino

Configurar definições para Olá origem e destino site (Azure). Definições de origem inclui executar configuração Unified tooinstall componentes da recuperação de Site do Olá no local.

Aceda demasiado[passo 7: Configurar Olá origem e de destino](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>Passo 8: Configurar uma política de replicação

Configurar uma política toospecify físicos como servidores devem replicar.

Aceda demasiado[passo 8: configurar uma política de replicação](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>Passo 9: Instalar o serviço de mobilidade Olá

Olá serviço de mobilidade tem de ser instalado em cada servidor que pretende tooreplicate. Existem algumas formas tooset serviço Olá, com a instalação de push ou pull.

Aceda demasiado[passo 9: instalar o serviço de mobilidade Olá](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>Passo 10: Ativar a replicação

Depois de Olá serviço de mobilidade está em execução num servidor, pode ativar a replicação para o mesmo. Depois de ativar, ocorre a replicação inicial Olá VM.

Aceda demasiado[passo 10: Ativar a replicação](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Passo 11: Executar uma ativação pós-falha de teste

Após a conclusão da replicação inicial e a replicação de diferenças está em execução, pode executar um toomake de ativação pós-falha de teste se de que tudo funciona conforme esperado.

Aceda demasiado[passo 11: executar uma ativação pós-falha de teste](physical-walkthrough-test-failover.md)

