---
title: aaaWebJobs no App Service do Azure
description: "Saiba como os testes toobuild WebJobs toorun fundo, interagir com serviços como o armazenamento e de barramento de serviço e criar tarefas agendadas."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="a9dcc-103">Utilizar WebJobs no Serviço de Aplicações do Azure</span><span class="sxs-lookup"><span data-stu-id="a9dcc-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="a9dcc-104">Este artigo contém ligações toodocumentation recursos sobre como toouse WebJobs do Azure e Olá SDK de WebJobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="a9dcc-105">Scripts de toorun uma forma fácil de fornecer de WebJobs do Azure ou programas como em segundo plano a processos no [Web Apps do App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a9dcc-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="a9dcc-106">Pode carregar e executar um ficheiro executável, tal como como cmd, bat,. exe (.NET), ps1, ostrar, php, py, js e jar.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="a9dcc-107">Estes programas run WebJobs com base numa agenda (cron) ou continuamente.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="a9dcc-108">Olá SDK de WebJobs-torna mais fácil toouse Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="a9dcc-109">Olá SDK de WebJobs tem um enlace e o sistema de Acionador que funciona com o Blobs Storage do Microsoft Azure, filas e tabelas, bem como as filas do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="a9dcc-110">Criar, implementar e gerir WebJobs são totalmente integrada com ferramentas integrada no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="a9dcc-111">Pode criar WebJobs a partir de modelos, publicar e gerir (executar/paragem/monitor/depuração)-los.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="a9dcc-112">dashboard de WebJobs Olá no Olá portal do Azure fornece capacidades de gestão poderosas que dão-lhe controlo total sobre a execução de Olá de WebJobs, incluindo Olá capacidade tooinvoke individuais as funções dentro de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="a9dcc-113">dashboard de Olá também apresenta os tempos de execução de função e de saída de registo.</span><span class="sxs-lookup"><span data-stu-id="a9dcc-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

