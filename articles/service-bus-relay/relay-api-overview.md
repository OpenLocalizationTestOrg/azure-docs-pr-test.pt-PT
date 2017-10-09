---
title: "Descrição geral da API de reencaminhamento de aaaAzure | Microsoft Docs"
description: "Descrição geral das APIs de reencaminhamento do Azure disponíveis"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a><span data-ttu-id="23ce3-103">APIs de reencaminhamento disponíveis</span><span class="sxs-lookup"><span data-stu-id="23ce3-103">Available Relay APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="23ce3-104">APIs de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="23ce3-104">Runtime APIs</span></span>

<span data-ttu-id="23ce3-105">Olá tabela seguinte apresenta uma lista de todos os clientes de tempo de execução de reencaminhamento atualmente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="23ce3-105">hello following table lists all currently available Relay runtime clients.</span></span>

<span data-ttu-id="23ce3-106">Olá [informações adicionais](#additional-information) secção contém informações adicionais sobre o estado de Olá de cada biblioteca de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="23ce3-106">hello [additional information](#additional-information) section contains more information about hello status of each runtime library.</span></span>

| <span data-ttu-id="23ce3-107">Idioma/plataforma</span><span class="sxs-lookup"><span data-stu-id="23ce3-107">Language/Platform</span></span> | <span data-ttu-id="23ce3-108">Funcionalidade disponível</span><span class="sxs-lookup"><span data-stu-id="23ce3-108">Available feature</span></span> | <span data-ttu-id="23ce3-109">Pacote de cliente</span><span class="sxs-lookup"><span data-stu-id="23ce3-109">Client package</span></span> | <span data-ttu-id="23ce3-110">Repositório</span><span class="sxs-lookup"><span data-stu-id="23ce3-110">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="23ce3-111">Padrão de .NET</span><span class="sxs-lookup"><span data-stu-id="23ce3-111">.NET Standard</span></span> | <span data-ttu-id="23ce3-112">Ligações Híbridas</span><span class="sxs-lookup"><span data-stu-id="23ce3-112">Hybrid Connections</span></span> | [<span data-ttu-id="23ce3-113">Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="23ce3-113">Microsoft.Azure.Relay</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [<span data-ttu-id="23ce3-114">GitHub</span><span class="sxs-lookup"><span data-stu-id="23ce3-114">GitHub</span></span>](https://github.com/azure/azure-relay-dotnet) |
| <span data-ttu-id="23ce3-115">.NET framework</span><span class="sxs-lookup"><span data-stu-id="23ce3-115">.NET Framework</span></span> | <span data-ttu-id="23ce3-116">Reencaminhamento do WCF</span><span class="sxs-lookup"><span data-stu-id="23ce3-116">WCF Relay</span></span> | [<span data-ttu-id="23ce3-117">Windowsazure</span><span class="sxs-lookup"><span data-stu-id="23ce3-117">WindowsAzure.ServiceBus</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | <span data-ttu-id="23ce3-118">N/D</span><span class="sxs-lookup"><span data-stu-id="23ce3-118">N/A</span></span> |
| <span data-ttu-id="23ce3-119">Nó</span><span class="sxs-lookup"><span data-stu-id="23ce3-119">Node</span></span> | <span data-ttu-id="23ce3-120">Ligações Híbridas</span><span class="sxs-lookup"><span data-stu-id="23ce3-120">Hybrid Connections</span></span> | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [<span data-ttu-id="23ce3-121">GitHub</span><span class="sxs-lookup"><span data-stu-id="23ce3-121">GitHub</span></span>](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a><span data-ttu-id="23ce3-122">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="23ce3-122">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="23ce3-123">.NET</span><span class="sxs-lookup"><span data-stu-id="23ce3-123">.NET</span></span>
<span data-ttu-id="23ce3-124">ecossistema de .NET Olá tem vários tempos de execução, por conseguinte, existem vários bibliotecas .NET para os Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="23ce3-124">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="23ce3-125">biblioteca de .NET padrão Olá pode ser executada através do .NET Core ou Olá .NET Framework, enquanto a biblioteca de .NET Framework Olá só pode ser executada num ambiente de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="23ce3-125">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="23ce3-126">Para obter mais informações sobre estruturas de .NET, consulte [versões framework](/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="23ce3-126">For more information on .NET Frameworks, see [framework versions](/dotnet/articles/standard/frameworks#framework-versions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="23ce3-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="23ce3-127">Next steps</span></span>
<span data-ttu-id="23ce3-128">toolearn mais informações sobre o reencaminhamento do Azure, visite estas ligações:</span><span class="sxs-lookup"><span data-stu-id="23ce3-128">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="23ce3-129">O que é o Reencaminhamento do Azure?</span><span class="sxs-lookup"><span data-stu-id="23ce3-129">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="23ce3-130">FAQ de Reencaminhamento</span><span class="sxs-lookup"><span data-stu-id="23ce3-130">Relay FAQ</span></span>](relay-faq.md)