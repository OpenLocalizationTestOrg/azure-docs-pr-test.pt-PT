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
# <a name="available-event-hubs-apis"></a><span data-ttu-id="1f387-103">APIs de Hubs de eventos disponível</span><span class="sxs-lookup"><span data-stu-id="1f387-103">Available Event Hubs APIs</span></span>

## <a name="runtime-apis"></a><span data-ttu-id="1f387-104">APIs de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="1f387-104">Runtime APIs</span></span>

<span data-ttu-id="1f387-105">Olá segue-se uma descrição de todos os clientes de tempo de execução de Event Hubs do Azure atualmente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1f387-105">hello following is a description of all currently available Azure Event Hubs runtime clients.</span></span> <span data-ttu-id="1f387-106">Embora alguns destas bibliotecas também incluem funcionalidades de gestão limitada, há também [bibliotecas específicas](#management-apis) dedicado toomanagement operações.</span><span class="sxs-lookup"><span data-stu-id="1f387-106">While some of these libraries also include limited management functionality, there are also [specific libraries](#management-apis) dedicated toomanagement operations.</span></span> <span data-ttu-id="1f387-107">Aborda core Olá estas bibliotecas é toosend e receber mensagens de um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="1f387-107">hello core focus of these libraries is toosend and receive messages from an event hub.</span></span>

<span data-ttu-id="1f387-108">Consulte [informações adicionais](#additional-information) para obter mais detalhes sobre o estado atual de Olá de cada biblioteca de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="1f387-108">See [additional information](#additional-information) for more details on hello current status of each runtime library.</span></span>

| <span data-ttu-id="1f387-109">Idioma/plataforma</span><span class="sxs-lookup"><span data-stu-id="1f387-109">Language/Platform</span></span> | <span data-ttu-id="1f387-110">Pacote de cliente</span><span class="sxs-lookup"><span data-stu-id="1f387-110">Client package</span></span> | <span data-ttu-id="1f387-111">Pacote de EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="1f387-111">EventProcessorHost package</span></span> | <span data-ttu-id="1f387-112">Repositório</span><span class="sxs-lookup"><span data-stu-id="1f387-112">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f387-113">Padrão de .NET</span><span class="sxs-lookup"><span data-stu-id="1f387-113">.NET Standard</span></span> | [<span data-ttu-id="1f387-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="1f387-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [<span data-ttu-id="1f387-115">NuGet</span><span class="sxs-lookup"><span data-stu-id="1f387-115">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [<span data-ttu-id="1f387-116">GitHub</span><span class="sxs-lookup"><span data-stu-id="1f387-116">GitHub</span></span>](https://github.com/azure/azure-event-hubs-dotnet) |
| <span data-ttu-id="1f387-117">.NET framework</span><span class="sxs-lookup"><span data-stu-id="1f387-117">.NET Framework</span></span> | [<span data-ttu-id="1f387-118">NuGet</span><span class="sxs-lookup"><span data-stu-id="1f387-118">NuGet</span></span>](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [<span data-ttu-id="1f387-119">NuGet</span><span class="sxs-lookup"><span data-stu-id="1f387-119">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | <span data-ttu-id="1f387-120">N/D</span><span class="sxs-lookup"><span data-stu-id="1f387-120">N/A</span></span> |
| <span data-ttu-id="1f387-121">Java</span><span class="sxs-lookup"><span data-stu-id="1f387-121">Java</span></span> | [<span data-ttu-id="1f387-122">Maven</span><span class="sxs-lookup"><span data-stu-id="1f387-122">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [<span data-ttu-id="1f387-123">Maven</span><span class="sxs-lookup"><span data-stu-id="1f387-123">Maven</span></span>](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [<span data-ttu-id="1f387-124">GitHub</span><span class="sxs-lookup"><span data-stu-id="1f387-124">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-java) |
| <span data-ttu-id="1f387-125">Nó</span><span class="sxs-lookup"><span data-stu-id="1f387-125">Node</span></span> | [<span data-ttu-id="1f387-126">NPM</span><span class="sxs-lookup"><span data-stu-id="1f387-126">NPM</span></span>](https://www.npmjs.com/package/azure-event-hubs) | <span data-ttu-id="1f387-127">N/D</span><span class="sxs-lookup"><span data-stu-id="1f387-127">N/A</span></span> | [<span data-ttu-id="1f387-128">GitHub</span><span class="sxs-lookup"><span data-stu-id="1f387-128">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-node) |
| <span data-ttu-id="1f387-129">C</span><span class="sxs-lookup"><span data-stu-id="1f387-129">C</span></span> | <span data-ttu-id="1f387-130">N/D</span><span class="sxs-lookup"><span data-stu-id="1f387-130">N/A</span></span> | <span data-ttu-id="1f387-131">N/D</span><span class="sxs-lookup"><span data-stu-id="1f387-131">N/A</span></span> | [<span data-ttu-id="1f387-132">GitHub</span><span class="sxs-lookup"><span data-stu-id="1f387-132">GitHub</span></span>](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a><span data-ttu-id="1f387-133">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="1f387-133">Additional information</span></span>

#### <a name="net"></a><span data-ttu-id="1f387-134">.NET</span><span class="sxs-lookup"><span data-stu-id="1f387-134">.NET</span></span>
<span data-ttu-id="1f387-135">ecossistema de .NET Olá tem vários tempos de execução, por conseguinte, existem vários bibliotecas .NET para os Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1f387-135">hello .NET ecosystem has multiple runtimes, hence there are multiple .NET libraries for Event Hubs.</span></span> <span data-ttu-id="1f387-136">biblioteca de .NET padrão Olá pode ser executada através do .NET Core ou Olá .NET Framework, enquanto a biblioteca de .NET Framework Olá só pode ser executada num ambiente de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="1f387-136">hello .NET Standard library can be run using either .NET Core or hello .NET Framework, while hello .NET Framework library can only be run in a .NET Framework environment.</span></span> <span data-ttu-id="1f387-137">Para obter mais informações sobre estruturas de .NET, consulte [versões framework](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span><span class="sxs-lookup"><span data-stu-id="1f387-137">For more information on .NET Frameworks, see [framework versions](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).</span></span>

#### <a name="node"></a><span data-ttu-id="1f387-138">Nó</span><span class="sxs-lookup"><span data-stu-id="1f387-138">Node</span></span>

<span data-ttu-id="1f387-139">biblioteca de Node.js Olá está atualmente em pré-visualização e é mantido à medida que um projeto de lado por funcionários da Microsoft e os contribuintes externos.</span><span class="sxs-lookup"><span data-stu-id="1f387-139">hello Node.js library is currently in preview and is maintained as a side project by Microsoft employees and external contributors.</span></span> <span data-ttu-id="1f387-140">Todas as suas contribuições, incluindo o código de origem são boas-vindas e serão analisadas.</span><span class="sxs-lookup"><span data-stu-id="1f387-140">All contributions including source code are welcome and will be reviewed.</span></span>

## <a name="management-apis"></a><span data-ttu-id="1f387-141">APIs de gestão</span><span class="sxs-lookup"><span data-stu-id="1f387-141">Management APIs</span></span>

<span data-ttu-id="1f387-142">Olá segue-se uma lista de todas as bibliotecas de específica de gestão atualmente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1f387-142">hello following is a listing of all currently available management specific libraries.</span></span> <span data-ttu-id="1f387-143">Nenhuma destas bibliotecas contém operações de tempo de execução e são Olá único objetivo gerir entidades de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="1f387-143">None of these libraries contain runtime operations, and are for hello sole purpose of managing Event Hubs entities.</span></span>

| <span data-ttu-id="1f387-144">Idioma/plataforma</span><span class="sxs-lookup"><span data-stu-id="1f387-144">Language/Platform</span></span> | <span data-ttu-id="1f387-145">Pacote de gestão</span><span class="sxs-lookup"><span data-stu-id="1f387-145">Management package</span></span> | <span data-ttu-id="1f387-146">Repositório</span><span class="sxs-lookup"><span data-stu-id="1f387-146">Repository</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f387-147">Padrão de .NET</span><span class="sxs-lookup"><span data-stu-id="1f387-147">.NET Standard</span></span> | [<span data-ttu-id="1f387-148">NuGet</span><span class="sxs-lookup"><span data-stu-id="1f387-148">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [<span data-ttu-id="1f387-149">GitHub</span><span class="sxs-lookup"><span data-stu-id="1f387-149">GitHub</span></span>](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a><span data-ttu-id="1f387-150">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1f387-150">Next steps</span></span>
<span data-ttu-id="1f387-151">Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:</span><span class="sxs-lookup"><span data-stu-id="1f387-151">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="1f387-152">Descrição geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="1f387-152">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="1f387-153">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="1f387-153">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="1f387-154">FAQ dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="1f387-154">Event Hubs FAQ</span></span>](event-hubs-faq.md)