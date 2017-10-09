---
title: "Migração de plataforma do Centro de segurança de aaaAzure | Microsoft Docs"
description: "Este documento explica a forma de toohello algumas alterações dados do Centro de segurança do Azure é recolhida."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Migração da plataforma do centro de segurança do Azure

A partir da precoce de Junho de 2017, o Centro de segurança do Azure lança importante alterações toohello forma segurança dados são recolhidos e armazenados.  Estas alterações desbloquear novas capacidades, como a capacidade de Olá tooeasily dados de segurança de pesquisa e melhor alinha com outra gestão do Azure e a monitorização dos serviços.

> [!NOTE]
> migração de plataforma Olá não deve afetar os recursos de produção e não é necessária a partir do seu lado ação.


## <a name="whats-happening-during-this-platform-migration"></a>O que acontece durante a migração da plataforma?

Centro de segurança utilizado anteriormente, dados de segurança do Olá o agente de monitorização do Azure toocollect das suas VMs. Isto inclui informações sobre configurações de segurança, que são utilizados tooidentify vulnerabilidades, e eventos de segurança, que são utilizados toodetect ameaças. Esses dados estão armazenados na(s) sua(s) conta(s) de armazenamento no Azure.

Passa, que Centro de segurança utiliza Olá Microsoft Monitoring Agent – isto é Olá mesmo agente utilizado por Olá Operations Management Suite e o serviço de análise de registos. Dados recolhidos a partir deste agente estão armazenados em qualquer um dos existente *Log Analytics* [área de trabalho](../log-analytics/log-analytics-manage-access.md) associado à sua subscrição do Azure ou um workspace(s) nova, tendo em conta Olá geolocalização de Olá VM .

## <a name="agent"></a>Agente

Como parte da transição Olá, Olá Microsoft Monitoring Agent (para [Windows](../log-analytics/log-analytics-windows-agents.md) ou [Linux](../log-analytics/log-analytics-linux-agents.md)) está instalado em todas as VMs do Azure a partir da qual atualmente a ser recolhidos dados.  Se Olá que VM já tem Olá Microsoft Monitoring Agent instalada, o Centro de segurança tira partido Olá atual agente foi instalado.

Para um período de tempo (normalmente, alguns dias), ambos os agentes serão executado lado a lado tooensure uma transição tranquila sem qualquer perda de dados. Este procedimento activará Microsoft toovalidate Olá novo pipeline de dados está operacional antes de discontinuing a utilização de pipeline atual Olá. Uma vez verificado, Olá o agente de monitorização do Azure irá ser removido as suas VMs. Não é necessário qualquer trabalho da sua parte. Receberá um e-mail quando todos os clientes tiverem sido migrados.
 
Não é recomendado que, desinstalar manualmente Olá o agente de monitorização do Azure durante a migração de Olá como pode resultar em falta irregulares nos dados de segurança. Consulte o [suporte e serviço de apoio ao cliente da Microsoft](https://support.microsoft.com/contactus/) se precisar de mais assistência. 

Olá Microsoft Monitoring Agent para o Windows necessita de utilizar a porta TCP 443, leia [guia de resolução de problemas do Azure segurança Center](security-center-troubleshooting-guide.md) para obter mais informações.


> [!NOTE] 
> Uma vez que Olá Microsoft Monitoring Agent pode ser utilizado por outra gestão do Azure e monitorização dos serviços, Olá agente será não ser desinstalado automaticamente quando desativar a recolha de dados no Centro de segurança. No entanto, pode desinstalar manualmente o agente de Olá se for necessário.

## <a name="workspace"></a>Área de trabalho

Conforme descrito anteriormente, dados recolhidos do Microsoft Monitoring Agent (em nome do Centro de segurança) são armazenadas numa análise registo existente de Olá workspace(s) associado à sua subscrição do Azure ou um workspace(s) nova, tendo em Olá de conta geolocalização de Olá VM.

No portal do Azure Olá, pode procurar toosee uma lista de áreas de trabalho das Log Analytics, incluindo quaisquer criado pelo centro de segurança. Será criado um grupo de recursos relacionados para as novas áreas de trabalho. Ambos seguem a convenção de nomenclatura:

- Área de trabalho: *DefaultWorkspace-[subscrição-ID]-[geo]*
- Grupo de Recursos: *DefaultResouceGroup-[geo]* 
 
Para áreas de trabalho criadas pelo centro de segurança do Azure, os dados são retidos durante 30 dias. Para áreas de trabalho existentes, retenção baseia-se na área de trabalho Olá escalão de preço.

> [!NOTE]
> Os dados recolhidos anteriormente pelo centro de segurança permanecem na(s) sua(s) conta(s) de armazenamento. Depois de concluída a migração de Olá, pode eliminar estas contas de armazenamento.

### <a name="oms-security-solution"></a>Solução de segurança do OMS 

Para clientes existentes que não têm a solução de segurança do OMS instalada, a Microsoft instala-a na sua área de trabalho, mas apenas em VM do Azure. Não desinstale essa solução, pois não há nenhuma correção automática se tal for efetuado na consola de gestão do OMS.


## <a name="other-updates"></a>Outras atualizações

Em conjunto com a migração de plataforma Olá, iremos são disponibilizando algumas atualizações secundárias adicionais:

- São suportadas outras versões do SO. Ver lista Olá [aqui](security-center-faq.md#virtual-machines).
- lista de Olá de vulnerabilidades do SO será expandida. Ver lista Olá [aqui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
- Os [preços](https://azure.microsoft.com/pricing/details/security-center/) serão calculados por hora (anteriormente era por dia), resultando em poupança de custos para alguns clientes.
- Recolha de dados será necessário e ativada automaticamente para clientes no escalão de preço padrão Olá.
- O centro de segurança do Azure começará a descobrir soluções antimalware que não foram implementadas com as extensões do Azure. A descoberta do Symantec Endpoint Protection e do Defender para Windows 2016 estará disponível pela primeira vez.
- Políticas de prevenção e notificações apenas são configuráveis em Olá *subscrição* nível, mas preços ainda podem ser definidos ao hello *grupo de recursos* nível

