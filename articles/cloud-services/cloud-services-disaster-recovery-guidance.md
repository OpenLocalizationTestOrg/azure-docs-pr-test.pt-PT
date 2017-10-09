---
title: "aaaWhat toodo no evento Olá de uma interrupção do serviço do Azure que tem impacto nos Cloud Services do Azure | Microsoft Docs"
description: "Saiba que toodo no evento Olá de uma interrupção do serviço do Azure que tem impacto nos Cloud Services do Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Que toodo no evento Olá de uma interrupção do serviço do Azure que tem impacto nos Cloud Services do Azure
Na Microsoft, trabalhamos toomake rígido se de que nossos serviços estão sempre disponível tooyou quando que precisar. Força se para além dos nosso controlo, por vezes, um impacto no-nos de formas que provocar interrupções de serviço não planeada.

A Microsoft fornece um contrato de nível de serviço (SLA) para os respetivos serviços, como um compromisso de tempo de atividade e conectividade. Olá SLA para serviços do Azure individuais pode ser encontrado em [contratos de nível de serviço do Azure](https://azure.microsoft.com/support/legal/sla/).

O Azure já tem muitas funcionalidades de plataforma incorporado que suportam aplicações altamente disponíveis. Para mais informações sobre estes serviços, leia o artigo [recuperação após desastre e elevada disponibilidade para aplicações do Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Este artigo abrange um cenário de recuperação de desastre verdadeiro, quando uma região toda sofre uma falha devido desastre natural toomajor ou interrupção do serviço ampla. Estes são ocorrências raras, mas tem de preparar para a possibilidade de Olá se houver uma falha de uma região de toda. Se uma região toda sofre uma interrupção do serviço, cópias de localmente redundante Olá dos seus dados seria temporariamente indisponíveis. Se tiver ativado a georreplicação, três cópias adicionais dos blobs de armazenamento do Azure e tabelas são armazenadas numa região diferente. O evento de uma falha regional completa ou de um desastre no qual Olá região primária não é recuperável Olá, Azure remaps todas a região de georreplicação Olá DNS entradas toohello.

> [!NOTE]
> Lembre-se de que não têm qualquer controlo sobre este processo e ocorrerá apenas para interrupções ao serviço em todo o datacenter. Por este motivo, deve também dependem outra estratégias de cópia de segurança específicos da aplicação tooachieve Olá nível mais elevado de disponibilidade. Para obter mais informações, consulte [recuperação após desastre e elevada disponibilidade de aplicações incorporadas no Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). Se quiser tooaffect capaz de toobe o seus próprios ativação pós-falha, é aconselhável utilização Olá tooconsider [armazenamento georredundante com acesso de leitura (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), que cria uma cópia só de leitura de dados noutra região.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Opção 1: Utilizar uma implementação de cópia de segurança através do Gestor de tráfego do Azure
solução de recuperação de desastre mais robusta Olá envolve manter múltiplas implementações da aplicação em regiões diferentes, em seguida, utilizar [Traffic Manager do Azure](../traffic-manager/traffic-manager-overview.md) toodirect tráfego entre as mesmas. Traffic Manager do Azure fornece várias [métodos de encaminhamento](../traffic-manager/traffic-manager-routing-methods.md), para que possa escolher se toomanage as implementações com um modelo de cópia de segurança/primário ou toosplit de tráfego entre eles.

![Serviços Cloud do Azure de balanceamento em regiões com o Gestor de tráfego do Azure](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Para Olá mais rápida resposta toohello perda de uma região, é importante que configure o Gestor de tráfego [monitorização de pontos finais](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-tooa-new-region"></a>Opção 2: Implementar a sua região novo de tooa de aplicação
Manter múltiplas implementações de Active Directory, conforme descrito na opção anterior Olá incorreu dos custos adicionais. Se o objetivo de tempo de recuperação (RTO) é flexível o suficiente e tem código original Olá ou compilado pacote de serviços em nuvem, pode criar uma nova instância da sua aplicação noutra região e atualizar a registos toopoint toohello nova implementação de DNS.

Para obter mais detalhes sobre como toocreate e implementar uma aplicação de serviço na nuvem, consulte [como toocreate e implementar um serviço em nuvem](cloud-services-how-to-create-deploy-portal.md).

Dependendo das suas origens de dados de aplicação, poderá ser necessário procedimentos de recuperação de Olá toocheck para a origem de dados de aplicação.

* Para origens de dados do Storage do Azure, consulte [replicação de armazenamento do Azure](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck nas opções de Olá que estão disponíveis com base no Olá escolher o modelo de replicação para a sua aplicação.
* Para origens de base de dados SQL, leia o artigo [descrição geral: na nuvem de recuperação de desastre de base de dados e de continuidade do negócio com a SQL Database](../sql-database/sql-database-business-continuity.md) toocheck nas opções de Olá que estão disponíveis com base no modelo de replicação de Olá escolhido para a sua aplicação.


## <a name="option-3-wait-for-recovery"></a>Opção 3: Aguardar para recuperação
Neste caso, é necessária nenhuma ação da sua parte, mas o seu serviço estará disponível até região Olá é restaurada. Pode ver o estado do serviço atual Olá no Olá [Dashboard de estado de funcionamento do serviço de Azure](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Passos seguintes
mais informações sobre como tooimplement uma recuperação após desastre e a estratégia de elevada disponibilidade, consulte o artigo toolearn [recuperação após desastre e elevada disponibilidade para aplicações do Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

toodevelop uma compreensão técnica detalhada das capacidades de uma plataforma em nuvem, consulte [orientações técnica do Azure resiliência](../resiliency/resiliency-technical-guidance.md).
