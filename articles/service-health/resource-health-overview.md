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
# <a name="azure-resource-health-overview"></a><span data-ttu-id="987dd-103">Descrição geral do Estado de funcionamento de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="987dd-103">Azure resource health overview</span></span>
 
<span data-ttu-id="987dd-104">O estado de funcionamento dos recursos ajuda-o a diagnosticar e a obter suporte quando um problema do Azure afeta os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="987dd-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="987dd-105">Informa-sobre Olá atuais e anteriores estado de funcionamento dos seus recursos e ajuda a mitigar os problemas.</span><span class="sxs-lookup"><span data-stu-id="987dd-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="987dd-106">O estado de funcionamento dos recursos fornece suporte técnico quando precisa de ajuda para resolver problemas relacionados com o serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="987dd-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="987dd-107">Enquanto [Azure estado](https://status.azure.com) informa sobre problemas de serviço que afetam a um conjunto amplo de clientes do Azure, o estado de funcionamento do recurso disponibiliza um dashboard personalizado do Estado de funcionamento de Olá dos seus recursos.</span><span class="sxs-lookup"><span data-stu-id="987dd-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="987dd-108">Estado de funcionamento de recursos mostra-lhe Olá permanente os recursos foram disponíveis no Olá devedor tooAzure problemas de serviço.</span><span class="sxs-lookup"><span data-stu-id="987dd-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="987dd-109">Isto torna simples para toounderstand se um SLA foi violado.</span><span class="sxs-lookup"><span data-stu-id="987dd-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="987dd-110">O que é considerado um recurso e como funciona o estado de funcionamento do recurso decide se um recurso está em bom estado ou não?</span><span class="sxs-lookup"><span data-stu-id="987dd-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="987dd-111">Um recurso é uma instância de um tipo de recurso oferecido por um serviço do Azure através do Azure Resource Manager, por exemplo: uma máquina virtual, uma aplicação web ou uma base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="987dd-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="987dd-112">Estado de funcionamento do recurso depende sinais emitidos pelo Olá diferentes serviços do Azure tooassess se um recurso está em bom estado ou não.</span><span class="sxs-lookup"><span data-stu-id="987dd-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="987dd-113">Se um recurso é mau estado de funcionamento, o estado de funcionamento do recurso analisa informações adicionais toodetermine Olá origem problema Olá.</span><span class="sxs-lookup"><span data-stu-id="987dd-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="987dd-114">Também identifica as ações a que Microsoft está a demorar problema de Olá toofix ou que as ações que pode tomar tooaddress Olá causam do problema Olá.</span><span class="sxs-lookup"><span data-stu-id="987dd-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="987dd-115">Verifica a revisão Olá obter uma lista completa dos tipos de recursos e o estado de funcionamento [estado de funcionamento de recursos do Azure](resource-health-checks-resource-types.md) para obter detalhes adicionais sobre o modo como o estado de funcionamento é avaliado.</span><span class="sxs-lookup"><span data-stu-id="987dd-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="987dd-116">Estado de funcionamento fornecido pelo Estado de funcionamento de recursos</span><span class="sxs-lookup"><span data-stu-id="987dd-116">Health status provided by resource health</span></span>
<span data-ttu-id="987dd-117">Estado de funcionamento de Olá de um recurso é um dos seguintes Estados de Olá:</span><span class="sxs-lookup"><span data-stu-id="987dd-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="987dd-118">Disponível</span><span class="sxs-lookup"><span data-stu-id="987dd-118">Available</span></span>
<span data-ttu-id="987dd-119">serviço de Olá não detetou quaisquer eventos afetar o estado de funcionamento de Olá dos recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="987dd-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="987dd-120">Em casos onde recursos Olá recuperou de período de indisponibilidade não planeado durante Olá últimas 24 horas, verá Olá **recuperou recentemente** notificação.</span><span class="sxs-lookup"><span data-stu-id="987dd-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Máquina de virtual de disponibilidade de estado de funcionamento do recurso](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="987dd-122">Não disponível</span><span class="sxs-lookup"><span data-stu-id="987dd-122">Unavailable</span></span>
<span data-ttu-id="987dd-123">serviço de Olá detetou uma plataforma em curso ou evento de plataforma não afetar o estado de funcionamento de Olá dos recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="987dd-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="987dd-124">Eventos de plataforma</span><span class="sxs-lookup"><span data-stu-id="987dd-124">Platform events</span></span>
<span data-ttu-id="987dd-125">Estes eventos são acionados por vários componentes de Olá infraestrutura do Azure e incluem tanto ações agendadas, como a manutenção planeada e incidentes inesperadas, como um reinício do anfitrião não planeada.</span><span class="sxs-lookup"><span data-stu-id="987dd-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="987dd-126">Estado de funcionamento do recurso fornece detalhes adicionais no evento Olá, o processo de recuperação Olá e permite-lhe toocontact suporte, mesmo se não tiver um Microsoft Active Directory suporta o contrato.</span><span class="sxs-lookup"><span data-stu-id="987dd-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Máquina de virtual de indisponível de estado de funcionamento do recurso devido tooplatform eventos](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="987dd-128">Eventos de plataforma não</span><span class="sxs-lookup"><span data-stu-id="987dd-128">Non-Platform events</span></span>
<span data-ttu-id="987dd-129">Estes eventos são acionados por ações executadas pelos utilizadores, por exemplo parar uma máquina virtual ou atingir Olá número máximo de ligações tooa a Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="987dd-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Máquina de virtual de indisponível de estado de funcionamento do recurso devido evento de plataforma toonon](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="987dd-131">Desconhecido</span><span class="sxs-lookup"><span data-stu-id="987dd-131">Unknown</span></span>
<span data-ttu-id="987dd-132">Este estado de funcionamento indica que o estado de funcionamento do recurso não recebeu informações sobre este recurso durante mais de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="987dd-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="987dd-133">Apesar deste Estado não é uma indicação definitiva Olá do Estado do recurso de Olá, é um ponto de dados importantes no processo de resolução de problemas de Olá:</span><span class="sxs-lookup"><span data-stu-id="987dd-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="987dd-134">Se estiver a executar o recurso de Olá como Estado Olá esperado do recurso de Olá, atualizaremos tooAvailable após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="987dd-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="987dd-135">Se ocorrerem problemas com recurso de Olá, hello o estado de funcionamento desconhecido pode sugerir recursos Olá é afetado por um evento na plataforma de Olá.</span><span class="sxs-lookup"><span data-stu-id="987dd-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Máquina virtual do Resource health desconhecido](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="987dd-137">Comunicar um Estado incorreto</span><span class="sxs-lookup"><span data-stu-id="987dd-137">Report an incorrect status</span></span>
<span data-ttu-id="987dd-138">Se em qualquer momento considerar o estado de funcionamento atual Olá está incorreto, pode indique clicando **comunicar o estado de funcionamento incorreto**.</span><span class="sxs-lookup"><span data-stu-id="987dd-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="987dd-139">Nos casos em que são afetados por um problema do Azure, Aconselhamo-lo toocontact suporte a partir do painel de estado de funcionamento de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="987dd-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Estado de funcionamento de recursos comunicar o estado incorreto](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="987dd-141">Informação histórica</span><span class="sxs-lookup"><span data-stu-id="987dd-141">Historical Information</span></span>
<span data-ttu-id="987dd-142">Pode aceder às cópias de segurança de dados históricos de estado de funcionamento de dias too14 clicando **ver histórico de** no painel de estado de funcionamento de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="987dd-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Histórico de relatórios do Estado de funcionamento do recurso](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="987dd-144">Introdução</span><span class="sxs-lookup"><span data-stu-id="987dd-144">Getting started</span></span>
<span data-ttu-id="987dd-145">tooopen estado de funcionamento de recursos para um recurso</span><span class="sxs-lookup"><span data-stu-id="987dd-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="987dd-146">Inicie sessão no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="987dd-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="987dd-147">Navegue tooyour recursos.</span><span class="sxs-lookup"><span data-stu-id="987dd-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="987dd-148">No menu de recursos de Olá localizado no lado esquerdo Olá, clique em **estado de funcionamento do recurso**.</span><span class="sxs-lookup"><span data-stu-id="987dd-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Abrir o estado de funcionamento de recursos a partir do painel de recursos](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="987dd-150">Pode também aceder ao estado de funcionamento do recurso clicando **mais serviços**e escrever **estado de funcionamento do recurso** no Olá de tooopen de caixa de texto de filtro **ajuda + suporte** painel.</span><span class="sxs-lookup"><span data-stu-id="987dd-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="987dd-151">Por fim, clique em [ **estado de funcionamento do recurso**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="987dd-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Abra o estado de funcionamento de recursos do serviço mais](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="987dd-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="987dd-153">Next steps</span></span>

<span data-ttu-id="987dd-154">Consulte estes toolearn de recursos mais informações sobre o estado de funcionamento de recursos:</span><span class="sxs-lookup"><span data-stu-id="987dd-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="987dd-155">Tipos de recursos e o estado de funcionamento verifica-se no estado de funcionamento de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="987dd-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="987dd-156">Perguntas mais frequentes sobre o estado de funcionamento de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="987dd-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




