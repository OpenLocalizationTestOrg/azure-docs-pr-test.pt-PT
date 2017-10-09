---
title: "manutenção aaaImpactful para VMs do Windows no Azure | Microsoft Docs"
description: "Manutenção impactful para máquinas virtuais do Windows."
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 98afaea0fdca796177e075b33615b03f1e7a0fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a>Manutenção impactful para máquinas virtuais

Existem alguns casos em que as suas VMs são reiniciadas devido tooplanned manutenção toohello subjacente infraestrutura. A disponibilidade de impactful toothe das suas VMs alojado no Azure, Olá seguem-se agora disponíveis para toouse:

-   Notificação enviada pelo menos de 30 dias antes de impacto Olá.

-   Visibilidade toohello as janelas de manutenção por cada VM.

-   Flexibilidade e controlo no momento exato de Olá para manutenção a afetar as suas VMs de definição.

Manutenção no Microsoft Azure está agendada no iterações. Iniciais iterações tem menor âmbito em risco de Olá de tooreduce ordem envolvido na implementação correções novas e capacidades. Iterações posteriores podem abranger várias regiões (nunca de Olá mesmo par de região). Uma VM está incluída numa iteração de manutenção única. Se uma iteração foi abortada, VMs restantes são incluídas no outra, futura, iteração.

Olá manutenção planeada iteração tem duas fases: Pre-emptive janela de manutenção e uma janela de manutenção agendada.

Olá **janela de manutenção Pre-emptive** fornece-lhe manutenção do Olá flexibilidade tooinitiate Olá nas suas VMs. Ao fazê-lo, pode determinar quando as suas VMs são afetadas, Olá sequência de atualização de Olá e a hora de Olá entre cada VM que está a ser mantido. Pode consultar toosee cada VM, se está a ser planeada para manutenção e verificar o resultado de Olá do último pedido manutenção iniciada.

Olá **janela de manutenção agendada** é quando o Azure agendou as VMs para manutenção de Olá. Durante este período de tempo, o que se segue a janela de manutenção preventivas, pode ainda de consulta para a janela de manutenção de Olá, mas já não será capaz de tooorchestrate manutenção de Olá.

## <a name="availability-considerations-during-planned-maintenance"></a>Considerações de disponibilidade durante a manutenção planeada 

### <a name="paired-regions"></a>Regiões emparelhadas

Cada região do Azure se encontra emparelhado com outro região dentro Olá mesma geografia, em conjunto, tornando um par regional. Quando executar a manutenção, Azure apenas irá atualizar instâncias de Máquina Virtual de Olá numa única região do seu par. Por exemplo, ao atualizar máquinas virtuais no Norte Central-nos de Olá, Azure irá não atualizar quaisquer máquinas virtuais no Sul Central-nos em Olá mesmo tempo. Isto será agendado num momento separado, ao ativar a ativação pós-falha ou com balanceamento de carga entre regiões. No entanto, noutras regiões como Europa do Norte pode estar em manutenção em Olá mesmo tempo, como EUA Leste.
Leia mais sobre [pares de região do Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Vs de VMs de instância únicas. Conjunto de dimensionamento da VM ou conjunto de disponibilidade

Quando implementar uma carga de trabalho utilizar máquinas virtuais no Azure, pode criar Olá VMs dentro de um conjunto de disponibilidade no aplicação tooyour do ordem tooprovide elevada disponibilidade. Esta configuração assegura que durante a eventos de uma interrupção ou a manutenção, pelo menos uma máquina virtual está disponível.

Dentro de um conjunto de disponibilidade, VMs individuais são distribuídas por cima too20 domínios de atualização. Durante a manutenção planeada, apenas um domínio com uma única atualização é afetado em qualquer momento. ordem de Olá dos domínios de atualização que está a ser afetado não pode continuar sequencialmente durante a manutenção planeada. Para única instância VMs (que não faz parte do conjunto de disponibilidade), não existe nenhuma forma toopredict ou a determinar qual e quantas VMs são afetadas em conjunto.

Conjuntos de dimensionamento de máquina virtual são um recurso de computação do Azure permite-lhe toodeploy e gerir um conjunto de VMs idênticas, como um único recurso.
conjunto de dimensionamento de Olá fornece garantias semelhantes tooan conjunto de disponibilidade no formato de domínios de atualização. 

Para obter mais informações sobre como configurar as máquinas virtuais de elevada disponibilidade, consulte [ *gerir a disponibilidade de Olá das máquinas virtuais Windows*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Eventos agendados

Serviço de metadados do Azure permite-lhe toodiscover informações sobre a Máquina Virtual alojada no Azure. Agendadas eventos, uma das categorias de Olá exposta, analisa as informações relativas eventos futuros (por exemplo, reiniciar o computador) para a aplicação possa preparar para os mesmos e limitar interrupção.

Para obter mais informações sobre eventos agendadas, consulte demasiado[Service de metadados do Azure - eventos agendada](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Deteção de manutenção e notificações

Agenda de manutenção é visível toocustomers ao nível de Olá de VMs individuais. Pode utilizar o Azure portal, tooquery API, o PowerShell ou o CLI para as janelas de manutenção preventivas e agendada. Além disso, espera receber uma notificação (e-mail) em caso de olá onde um (ou mais) das suas VMs são afetados durante o processo de Olá.

Manutenção preventivas e as fases de manutenção agendada começam com uma notificação. Espere tooreceive uma única notificação por subscrição do Azure. Olá é enviada notificação admin e coadministrador da subscrição toohello por predefinição. Também pode configurar o público-alvo Olá a notificação de manutenção.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Ver Olá janela de manutenção no portal de Olá 

Pode utilizar Olá portal do Azure e procure VMs agendadas para manutenção.

1.  Inicie sessão no toohello portal do Azure.

2.  Clique em e abra Olá **máquinas virtuais** painel.

3.  Clique em Olá **colunas** lista de Olá do botão tooopen de toochoose colunas disponíveis do

4.  Selecione e adicione Olá **janela de manutenção** colunas. As VMs que se encontram agendadas para manutenção tem janelas de manutenção de Olá anexadas. Depois de manutenção está concluída ou abortada para um, a janela de manutenção já não é apresentada.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Consultar os detalhes de manutenção com Olá API do Azure

Olá utilize [obter as informações VM API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) e procure Olá instância ver toodiscover Olá manutenção detalhes de uma VM individual. resposta Olá inclui Olá seguintes elementos:

  - isCustomerInitiatedMaintenanceAllowed: indica se pode agora iniciar preventivas volte a implementar no Olá VM.

  - preMaintenanceWindowStartTime: Olá hora de início da janela de manutenção preventivas Olá.

  - preMaintenanceWindowEndTime: Olá hora de fim da janela de manutenção preventivas Olá. Após este tempo, já não será capaz de tooinitiate manutenção nesta VM.
    
  - maintenanceWindowStartTime: Olá hora de início da janela de manutenção agendada Olá quando a VM são afetados.

  - maintenanceWindowEndTime: Olá hora de fim da janela de manutenção agendada Olá.
  
  - lastOperationResultCode: Olá resultado da sua última operação de manutenção a implementar.
 
  - lastOperationMessage: mensagem com descrição Olá resultado da sua última operação de manutenção a implementar.

## <a name="pre-emptive-redeploy"></a>Volte a implementar preventivas

Volte a implementar preventivas ação fornece Olá flexibilidade toocontrol Olá tempo quando manutenção está aplicado tooyour VMs no Azure. Manutenção planeada começa com uma janela de manutenção preventivas onde pode decidir no momento exato de Olá para cada um dos seus toobe VMs reiniciado. Seguem-se em que tal uma funcionalidade é útil de casos de utilização:

-   Coordenado toobe necessidade de manutenção com o cliente do fim de Olá.

-   janela de manutenção agendada Olá oferecida pelo Azure não é suficiente.
    Isto pode dever-se ao que janela Olá acontece toobe na hora mais agitada do Olá da semana ou é demasiado longo.

-   Para várias instâncias ou aplicações de várias camadas, é necessário tempo suficiente entre duas VMs ou de um determinado toofollow de sequência.

Quando chamar para implementar preventivas numa VM, move Olá VM tooan já atualizado nó e, em seguida, for ligado-la novamente, manter todas as suas opções de configuração e os recursos associados. Ao fazê-lo, o disco temporário Olá é perdido e endereços IP dinâmicos associados à interface de rede virtual são atualizados.

Volte a implementar preventivas está ativada uma vez por VM. Se ocorrer um erro durante o processo de Olá, operação Olá foi abortada, Olá VM não é afetada e é excluída da iteração de manutenção de Olá planeada. Irá ser contactado num horário posterior, com uma nova agenda e disponibilizadas um nova oportunidade tooschedule e sequência Olá impacto nas suas VMs.