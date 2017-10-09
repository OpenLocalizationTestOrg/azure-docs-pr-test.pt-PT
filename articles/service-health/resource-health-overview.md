---
title: "Descrição geral do Estado de funcionamento de recursos aaaAzure | Microsoft Docs"
description: "Descrição geral do Estado de funcionamento de recursos do Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Descrição geral do Estado de funcionamento de recursos do Azure
 
O estado de funcionamento dos recursos ajuda-o a diagnosticar e a obter suporte quando um problema do Azure afeta os seus recursos. Informa-sobre Olá atuais e anteriores estado de funcionamento dos seus recursos e ajuda a mitigar os problemas. O estado de funcionamento dos recursos fornece suporte técnico quando precisa de ajuda para resolver problemas relacionados com o serviço do Azure.

Enquanto [Azure estado](https://status.azure.com) informa sobre problemas de serviço que afetam a um conjunto amplo de clientes do Azure, o estado de funcionamento do recurso disponibiliza um dashboard personalizado do Estado de funcionamento de Olá dos seus recursos. Estado de funcionamento de recursos mostra-lhe Olá permanente os recursos foram disponíveis no Olá devedor tooAzure problemas de serviço. Isto torna simples para toounderstand se um SLA foi violado. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>O que é considerado um recurso e como funciona o estado de funcionamento do recurso decide se um recurso está em bom estado ou não?
Um recurso é uma instância de um tipo de recurso oferecido por um serviço do Azure através do Azure Resource Manager, por exemplo: uma máquina virtual, uma aplicação web ou uma base de dados do SQL Server.

Estado de funcionamento do recurso depende sinais emitidos pelo Olá diferentes serviços do Azure tooassess se um recurso está em bom estado ou não. Se um recurso é mau estado de funcionamento, o estado de funcionamento do recurso analisa informações adicionais toodetermine Olá origem problema Olá. Também identifica as ações a que Microsoft está a demorar problema de Olá toofix ou que as ações que pode tomar tooaddress Olá causam do problema Olá. 

Verifica a revisão Olá obter uma lista completa dos tipos de recursos e o estado de funcionamento [estado de funcionamento de recursos do Azure](resource-health-checks-resource-types.md) para obter detalhes adicionais sobre o modo como o estado de funcionamento é avaliado.

## <a name="health-status-provided-by-resource-health"></a>Estado de funcionamento fornecido pelo Estado de funcionamento de recursos
Estado de funcionamento de Olá de um recurso é um dos seguintes Estados de Olá:

### <a name="available"></a>Disponível
serviço de Olá não detetou quaisquer eventos afetar o estado de funcionamento de Olá dos recursos de Olá. Em casos onde recursos Olá recuperou de período de indisponibilidade não planeado durante Olá últimas 24 horas, verá Olá **recuperou recentemente** notificação.

![Máquina de virtual de disponibilidade de estado de funcionamento do recurso](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>Não disponível
serviço de Olá detetou uma plataforma em curso ou evento de plataforma não afetar o estado de funcionamento de Olá dos recursos de Olá.

#### <a name="platform-events"></a>Eventos de plataforma
Estes eventos são acionados por vários componentes de Olá infraestrutura do Azure e incluem tanto ações agendadas, como a manutenção planeada e incidentes inesperadas, como um reinício do anfitrião não planeada.

Estado de funcionamento do recurso fornece detalhes adicionais no evento Olá, o processo de recuperação Olá e permite-lhe toocontact suporte, mesmo se não tiver um Microsoft Active Directory suporta o contrato.

![Máquina de virtual de indisponível de estado de funcionamento do recurso devido tooplatform eventos](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Eventos de plataforma não
Estes eventos são acionados por ações executadas pelos utilizadores, por exemplo parar uma máquina virtual ou atingir Olá número máximo de ligações tooa a Cache de Redis.

![Máquina de virtual de indisponível de estado de funcionamento do recurso devido evento de plataforma toonon](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Desconhecido
Este estado de funcionamento indica que o estado de funcionamento do recurso não recebeu informações sobre este recurso durante mais de 10 minutos. Apesar deste Estado não é uma indicação definitiva Olá do Estado do recurso de Olá, é um ponto de dados importantes no processo de resolução de problemas de Olá:
* Se estiver a executar o recurso de Olá como Estado Olá esperado do recurso de Olá, atualizaremos tooAvailable após alguns minutos.
* Se ocorrerem problemas com recurso de Olá, hello o estado de funcionamento desconhecido pode sugerir recursos Olá é afetado por um evento na plataforma de Olá.

![Máquina virtual do Resource health desconhecido](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Comunicar um Estado incorreto
Se em qualquer momento considerar o estado de funcionamento atual Olá está incorreto, pode indique clicando **comunicar o estado de funcionamento incorreto**. Nos casos em que são afetados por um problema do Azure, Aconselhamo-lo toocontact suporte a partir do painel de estado de funcionamento de recursos de Olá. 

![Estado de funcionamento de recursos comunicar o estado incorreto](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Informação histórica
Pode aceder às cópias de segurança de dados históricos de estado de funcionamento de dias too14 clicando **ver histórico de** no painel de estado de funcionamento de recursos de Olá. 

![Histórico de relatórios do Estado de funcionamento do recurso](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>Introdução
tooopen estado de funcionamento de recursos para um recurso
1.  Inicie sessão no Olá portal do Azure.
2.  Navegue tooyour recursos.
3.  No menu de recursos de Olá localizado no lado esquerdo Olá, clique em **estado de funcionamento do recurso**.

![Abrir o estado de funcionamento de recursos a partir do painel de recursos](./media/resource-health-overview/from-resource-blade.png)

Pode também aceder ao estado de funcionamento do recurso clicando **mais serviços**e escrever **estado de funcionamento do recurso** no Olá de tooopen de caixa de texto de filtro **ajuda + suporte** painel. Por fim, clique em [ **estado de funcionamento do recurso**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Abra o estado de funcionamento de recursos do serviço mais](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Passos seguintes

Consulte estes toolearn de recursos mais informações sobre o estado de funcionamento de recursos:
-  [Tipos de recursos e o estado de funcionamento verifica-se no estado de funcionamento de recursos do Azure](resource-health-checks-resource-types.md)
-  [Perguntas mais frequentes sobre o estado de funcionamento de recursos do Azure](resource-health-faq.md)




