---
title: aaaUsing New Relic com o Azure | Microsoft Docs
description: "Saiba como toouse Olá toomanage de serviço do New Relic e monitorizar a sua aplicação do Azure."
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="32d57-103">Novo Relic de gestão de desempenho de aplicações no Azure</span><span class="sxs-lookup"><span data-stu-id="32d57-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="32d57-104">Pode adicionar o desempenho de trabalho do New Relic monitorização tooyour Azure aplicações alojadas.</span><span class="sxs-lookup"><span data-stu-id="32d57-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="32d57-105">Juntamente com os capacidades abrangentes de monitorização, resolução de problemas e otimizar as suas aplicações do Azure, pode também é elegíveis para um preço com desconto durante para produtos da New Relic através da utilização do Azure.</span><span class="sxs-lookup"><span data-stu-id="32d57-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="32d57-106">O que é New Relic?</span><span class="sxs-lookup"><span data-stu-id="32d57-106">What is New Relic?</span></span>
<span data-ttu-id="32d57-107">Com [produtos do New Relic](https://newrelic.com/products), pode resolver erros de aplicação, se antecipar aos problemas potenciais e compreender o desempenho de Olá de todo o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="32d57-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="32d57-108">É concebida toosave tempo quando identificar e diagnosticar problemas de desempenho e a funcionalidade guarda informações Olá terá toosolve estes problemas na ponta dos seus dedos.</span><span class="sxs-lookup"><span data-stu-id="32d57-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="32d57-109">Novo Olá de faixas Relic carregar o tempo e débito para as suas web transações, tanto a partir do servidor de Olá e browsers dos utilizadores.</span><span class="sxs-lookup"><span data-stu-id="32d57-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="32d57-110">Mostra quanto tempo demora na base de dados de Olá, analisa consultas lentas e pedidos web, fornece monitorização de disponibilidade e alertas, controla exceções da aplicação e todo muito mais.</span><span class="sxs-lookup"><span data-stu-id="32d57-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="32d57-111">Preços especiais</span><span class="sxs-lookup"><span data-stu-id="32d57-111">Special pricing</span></span>
<span data-ttu-id="32d57-112">Novo Relic padrão é utilizadores tooAzure livre.</span><span class="sxs-lookup"><span data-stu-id="32d57-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="32d57-113">Novo Relic profissional é oferecido com base no tamanho da instância de Cloud Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="32d57-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="32d57-114">Para obter informações sobre preços, consulte Olá [página do New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) no Olá Azure Marketplace ou contacte New Relic (sales@newrelic.com) para preços de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="32d57-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="32d57-115">Clientes do Azure recebem uma subscrição de avaliação de duas semanas do novo Relic Pro quando implementam o agente do New Relic Olá.</span><span class="sxs-lookup"><span data-stu-id="32d57-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="32d57-116">Inscreva-se New Relic utilizando Olá Azure Store</span><span class="sxs-lookup"><span data-stu-id="32d57-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="32d57-117">New Relic integra-se de forma totalmente integrada com as funções de funções da Web do Azure e de trabalho.</span><span class="sxs-lookup"><span data-stu-id="32d57-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="32d57-118">Pode rapidamente e facilmente inscreva New Relic diretamente a partir de Olá loja do Azure.</span><span class="sxs-lookup"><span data-stu-id="32d57-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="32d57-119">Para obter instruções, consulte Olá [Azure armazenar instruções de inscrição](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) do New Relic.</span><span class="sxs-lookup"><span data-stu-id="32d57-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="32d57-120">Ver os seus dados</span><span class="sxs-lookup"><span data-stu-id="32d57-120">View your data</span></span>
<span data-ttu-id="32d57-121">Assim que tiver efetuado a inscrição, pode tirar partido do incrível aplicação de New Relic monitorização e análise condicionada por dados.</span><span class="sxs-lookup"><span data-stu-id="32d57-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="32d57-122">toocheck o desempenho da aplicação no New Relic:</span><span class="sxs-lookup"><span data-stu-id="32d57-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="32d57-123">A partir do Portal do Azure Olá, selecione gerir.</span><span class="sxs-lookup"><span data-stu-id="32d57-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="32d57-124">Inicie sessão com o seu e-mail de conta do New Relic e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="32d57-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="32d57-125">Selecione a aplicação de Olá aplicação índice tooview dados de todos os da sua aplicação no Olá [página de descrição geral APM](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="32d57-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="32d57-126">Utilizar New Relic com o Azure</span><span class="sxs-lookup"><span data-stu-id="32d57-126">Using New Relic with Azure</span></span>
<span data-ttu-id="32d57-127">Para obter mais informações sobre a utilização do New Relic e o Azure, consulte [site de documentação do New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), incluindo:</span><span class="sxs-lookup"><span data-stu-id="32d57-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="32d57-128">New Relic para .NET</span><span class="sxs-lookup"><span data-stu-id="32d57-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="32d57-129">Instrumentar uma função de trabalho .NET no serviço em nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="32d57-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="32d57-130">New Relic para a plataforma de nuvem do Microsoft Azure Olá</span><span class="sxs-lookup"><span data-stu-id="32d57-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="32d57-131">New Relic para Olá dos serviços de aplicações do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="32d57-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="32d57-132">Resolução de problemas de Relic/Azure novo</span><span class="sxs-lookup"><span data-stu-id="32d57-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

