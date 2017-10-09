---
title: "Descrição geral da API de Hubs de eventos de aaaAzure | Microsoft Docs"
description: "Descrição geral das APIs de Hubs de eventos do Azure disponíveis"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a>APIs de Hubs de eventos disponível

## <a name="runtime-apis"></a>APIs de tempo de execução

Olá segue-se uma descrição de todos os clientes de tempo de execução de Event Hubs do Azure atualmente disponíveis. Embora alguns destas bibliotecas também incluem funcionalidades de gestão limitada, há também [bibliotecas específicas](#management-apis) dedicado toomanagement operações. Aborda core Olá estas bibliotecas é toosend e receber mensagens de um hub de eventos.

Consulte [informações adicionais](#additional-information) para obter mais detalhes sobre o estado atual de Olá de cada biblioteca de tempo de execução.

| Idioma/plataforma | Pacote de cliente | Pacote de EventProcessorHost | Repositório |
| --- | --- | --- | --- |
| Padrão de .NET | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | N/D |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| Nó | [NPM](https://www.npmjs.com/package/azure-event-hubs) | N/D | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | N/D | N/D | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>Informações adicionais

#### <a name="net"></a>.NET
ecossistema de .NET Olá tem vários tempos de execução, por conseguinte, existem vários bibliotecas .NET para os Event Hubs. biblioteca de .NET padrão Olá pode ser executada através do .NET Core ou Olá .NET Framework, enquanto a biblioteca de .NET Framework Olá só pode ser executada num ambiente de .NET Framework. Para obter mais informações sobre estruturas de .NET, consulte [versões framework](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).

#### <a name="node"></a>Nó

biblioteca de Node.js Olá está atualmente em pré-visualização e é mantido à medida que um projeto de lado por funcionários da Microsoft e os contribuintes externos. Todas as suas contribuições, incluindo o código de origem são boas-vindas e serão analisadas.

## <a name="management-apis"></a>APIs de gestão

Olá segue-se uma lista de todas as bibliotecas de específica de gestão atualmente disponíveis. Nenhuma destas bibliotecas contém operações de tempo de execução e são Olá único objetivo gerir entidades de Event Hubs.

| Idioma/plataforma | Pacote de gestão | Repositório |
| --- | --- | --- | --- |
| Padrão de .NET | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>Passos seguintes
Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:

* [Descrição geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](event-hubs-create.md)
* [FAQ dos Hubs de Eventos](event-hubs-faq.md)