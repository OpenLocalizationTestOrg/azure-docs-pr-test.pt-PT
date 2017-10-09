---
title: aaaAdministration e lista de tarefas de desenvolvimento nos BizTalk Services | Microsoft Docs
description: Planeamento e a tarefa ajudar para implementar os BizTalk Services do Azure.
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>Administração e a lista de tarefas de desenvolvimento nos serviços de BizTalk

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>Introdução
Ao trabalhar com os BizTalk Services do Microsoft Azure, existem várias tooconsider componentes baseados na nuvem e no local. tooget iniciado, considere Olá seguir o fluxo do processo:  

| Passo | Quem é responsável | Tarefa | Ligações relacionadas |
| --- | --- | --- | --- |
| 1. |Administrador |Criar Olá utilizando uma conta Microsoft ou uma conta organizacional de subscrição do Microsoft Azure |[Portal Clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |Administrador |Criar ou o aprovisionar um BizTalk Service. |[Criar um BizTalk Service com o portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |Administrador |Registar, ou a implementação de serviços de BizTalk da sua empresa |[Registar e atualizar uma implementação de serviço BizTalk no Olá Portal de serviços BizTalk](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |Administrador |Aplica-se a aplicação Olá utiliza o sistema de linha de negócio (LOB) no local do BizTalk Adapter Service tooconnect tooan ou utiliza uma fila ou um tópico de destino.  Crie Olá espaço de nomes de barramento de serviço de Azure. Atribua este espaço de nomes, o nome do emissor de barramento de serviço e o Programador de toohello de valores de chave do emissor de barramento de serviço. |[Como: criar ou modificar um espaço de nomes de serviço do Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md) e [valores de obter o nome do emissor e chave do emissor](biztalk-issuer-name-issuer-key.md) |
| 5. |Programador |Instale Olá SDK e crie Olá projeto dos BizTalk Services no Visual Studio. |[Instalar os BizTalk Services do Azure SDK](https://msdn.microsoft.com/library/azure/hh689760.aspx) e [criar mensagens avançado pontos finais no Azure](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |Programador |Implemente a sua tooyour de projeto do BizTalk Service que BizTalk Service alojada no Azure. |[Implementar e atualizar Olá projeto de serviços BizTalk](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |Administrador |Aplica-se de que se estiver a utilizar EDI.  Pode adicionar parceiros e criar contratos Olá Portal do Microsoft Azure BizTalk Services. Quando cria um contrato, pode adicionar bridge Olá e/ou as transformações criadas pelas definições de contrato Olá programador toohello. |[Configurar EDI, AS2 e EDIFACT no Portal de serviços BizTalk](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |Administrador |Utilizar Olá Portal clássico do Azure, monitorize o estado de funcionamento de Olá do seu BizTalk Service, incluindo as métricas do desempenho. |[Serviços BizTalk: Separadores Dashboard, Monitorizar e Dimensionar](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |Administrador |Utilizar Olá Portal do Microsoft Azure BizTalk Services, gerir artefactos de Olá utilizados pelo BizTalk Services e as mensagens de controlar como são processados por ficheiros de bridge de Olá. |[Utilizar Olá Portal de serviços BizTalk](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |Administrador |Crie tooback um plano de cópia de segurança, cópias de segurança Olá BizTalk Service. |[Continuidade do negócio e recuperação de desastres nos serviços de BizTalk](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>Passos Seguintes
[Tutoriais e amostras](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[Criar projeto Olá no Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[Instalar os BizTalk Services do Azure SDK](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>Conceitos
[Criar projeto Olá no Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI, AS2, EDIFACT mensagens e (tooBusiness de negócio)](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>Outros Recursos
[Adicionar origem, destino e Bridge de pontos finais de mensagens](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[Saiba e criar mapas de mensagem e transformações](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[Utilizar Olá BizTalk adaptador de serviço (BAS)](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)

