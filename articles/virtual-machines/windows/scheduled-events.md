---
title: aaaScheduled eventos para VMs do Windows no Azure | Microsoft Docs
description: "Eventos agendados utilizando o serviço de Azure metadados Olá para nas suas máquinas virtuais do Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="74b1c-103">Serviço de metadados do Azure: Agendados eventos (pré-visualização) para VMs do Windows</span><span class="sxs-lookup"><span data-stu-id="74b1c-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="74b1c-104">Pré-visualizações que são efetuados tooyou disponível numa condição de Olá concorda toohello termos de utilização.</span><span class="sxs-lookup"><span data-stu-id="74b1c-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="74b1c-105">Para obter mais informações, consulte [Termos de Utilização Suplementares do Microsoft Azure para Pré-visualizações do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="74b1c-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="74b1c-106">Eventos agendados é uma das Olá subservices em Olá Service de metadados do Azure.</span><span class="sxs-lookup"><span data-stu-id="74b1c-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="74b1c-107">É responsável por analisar informações sobre eventos futuros (por exemplo, reiniciar o computador) para a aplicação possa preparar para os mesmos e limitar interrupção.</span><span class="sxs-lookup"><span data-stu-id="74b1c-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="74b1c-108">Está disponível para todos os tipos de Máquina Virtual do Azure, incluindo PaaS e IaaS.</span><span class="sxs-lookup"><span data-stu-id="74b1c-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="74b1c-109">Eventos agendados fornece as suas máquinas virtuais tempo tooperform preventivo tarefas efeito de Olá toominimize de um evento.</span><span class="sxs-lookup"><span data-stu-id="74b1c-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="74b1c-110">Eventos agendados está disponível para Linux e VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="74b1c-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="74b1c-111">Para obter informações sobre eventos agendada no Linux, consulte [eventos agendados para VMs com Linux](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="74b1c-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="74b1c-112">Por que motivo agendada eventos?</span><span class="sxs-lookup"><span data-stu-id="74b1c-112">Why Scheduled Events?</span></span>

<span data-ttu-id="74b1c-113">Com eventos agendadas, que pode tomar passos toolimit Olá impacto plataforma intiated manutenção ou ações iniciadas pelo utilizador no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="74b1c-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="74b1c-114">Cargas de trabalho de várias instâncias, que utilizam o estado de toomaintain de técnicas de replicação, podem ser toooutages vulnerável a acontecer em múltiplas instâncias.</span><span class="sxs-lookup"><span data-stu-id="74b1c-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="74b1c-115">Como falhas poderão resultar em tarefas dispendiosas (por exemplo, os índices reconstrução) ou mesmo uma perda de réplica.</span><span class="sxs-lookup"><span data-stu-id="74b1c-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="74b1c-116">Em muitos outros casos, hello global disponibilidade do serviço pode ser melhorada através de uma sequência de encerramento correto, tais como concluir (ou cancelamento) transações em trânsito, reatribuição tarefas tooother VMs no cluster de Olá (ativação pós-falha manual) ou remover Olá Máquina virtual de um conjunto de Balanceador de carga de rede.</span><span class="sxs-lookup"><span data-stu-id="74b1c-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="74b1c-117">Existem casos onde enviar notificações de administrador sobre um evento futuros ou registar um evento deste tipo ajudar a melhorar a possibilidade de assistência de Olá das aplicações alojadas na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="74b1c-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="74b1c-118">Casos de utilização do Azure metadados analisa agendada eventos do serviço no seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="74b1c-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="74b1c-119">Plataforma iniciou a manutenção (por exemplo, a implementação de SO do anfitrião)</span><span class="sxs-lookup"><span data-stu-id="74b1c-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="74b1c-120">Chamadas iniciada pelo utilizador (por exemplo, os reinícios de utilizador ou redeploys uma VM)</span><span class="sxs-lookup"><span data-stu-id="74b1c-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="74b1c-121">Noções básicas de Olá</span><span class="sxs-lookup"><span data-stu-id="74b1c-121">hello basics</span></span>  

<span data-ttu-id="74b1c-122">Serviço de metadados do Azure expõe informações sobre como executar máquinas virtuais com um ponto final de REST acessível a partir do Olá VM.</span><span class="sxs-lookup"><span data-stu-id="74b1c-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="74b1c-123">informações de Olá estão disponíveis através de um IP não encaminhável, para que não está exposta fora Olá VM.</span><span class="sxs-lookup"><span data-stu-id="74b1c-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="74b1c-124">Âmbito</span><span class="sxs-lookup"><span data-stu-id="74b1c-124">Scope</span></span>
<span data-ttu-id="74b1c-125">Eventos agendados estão anexado tooall máquinas virtuais num serviço em nuvem ou tooall máquinas virtuais num conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="74b1c-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="74b1c-126">Como resultado, deve verificar Olá `Resources` campo no Olá eventos tooidentify que as VMs que vão toobe afetado.</span><span class="sxs-lookup"><span data-stu-id="74b1c-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="74b1c-127">Detetar ponto final de Olá</span><span class="sxs-lookup"><span data-stu-id="74b1c-127">Discovering hello endpoint</span></span>
<span data-ttu-id="74b1c-128">No caso de olá onde é criada uma Máquina Virtual numa rede Virtual (VNet), o serviço de metadados de Olá está disponível a partir de um IP estático não encaminhável, `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="74b1c-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="74b1c-129">Se Olá Máquina Virtual não está a ser criado dentro de uma rede Virtual, casos de predefinição Olá para serviços em nuvem e as VMs clássicas, lógica adicional é necessário toodiscover Olá endpoint toouse.</span><span class="sxs-lookup"><span data-stu-id="74b1c-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="74b1c-130">Consulte toothis exemplo toolearn como demasiado[detetar ponto final de anfitrião Olá](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="74b1c-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="74b1c-131">Controlo de versões</span><span class="sxs-lookup"><span data-stu-id="74b1c-131">Versioning</span></span> 
<span data-ttu-id="74b1c-132">Olá instância metadados do serviço é com a versão.</span><span class="sxs-lookup"><span data-stu-id="74b1c-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="74b1c-133">As versões são obrigatórias e a versão atual do Olá `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="74b1c-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="74b1c-134">Pré-visualização as versões anteriores dos eventos agendadas suportados {mais recente} como Olá api-version.</span><span class="sxs-lookup"><span data-stu-id="74b1c-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="74b1c-135">Este formato já não é suportado e será preterido no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="74b1c-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="74b1c-136">Utilizar cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="74b1c-136">Using headers</span></span>
<span data-ttu-id="74b1c-137">Quando consultar Olá metadados do serviço, tem de fornecer o cabeçalho de Olá `Metadata: true` tooensure Olá pedido não foi inadvertidamente redirecionado o pedido.</span><span class="sxs-lookup"><span data-stu-id="74b1c-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="74b1c-138">Ativar eventos agendados</span><span class="sxs-lookup"><span data-stu-id="74b1c-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="74b1c-139">Olá pela primeira vez, que efetue um pedido para eventos agendados, Azure implicitamente ativa Olá funcionalidade na sua máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="74b1c-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="74b1c-140">Como resultado, deve esperar uma resposta atrasada na sua primeira chamada de cópia de segurança tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="74b1c-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="74b1c-141">Manutenção iniciada pelo utilizador</span><span class="sxs-lookup"><span data-stu-id="74b1c-141">User initiated maintenance</span></span>
<span data-ttu-id="74b1c-142">Utilizador iniciou a manutenção de máquina virtual através do portal do Azure, Olá API, CLI, ou PowerShell resulta num evento agendado.</span><span class="sxs-lookup"><span data-stu-id="74b1c-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="74b1c-143">Isto permite-lhe lógica de preparação de manutenção de Olá tootest na sua aplicação e permite aos seus tooprepare de aplicações para manutenção iniciada pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="74b1c-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="74b1c-144">Reinício de uma máquina virtual agendas de um evento com o tipo `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="74b1c-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="74b1c-145">Voltar a implementar uma máquina virtual agendas de um evento com o tipo `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="74b1c-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="74b1c-146">Atualmente um máximo de 10 operações de manutenção iniciada pelo utilizador pode ser simultaneamente agendado.</span><span class="sxs-lookup"><span data-stu-id="74b1c-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="74b1c-147">Este limite irá ser flexibilizada antes de disponibilidade geral eventos agendados.</span><span class="sxs-lookup"><span data-stu-id="74b1c-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="74b1c-148">Atualmente manutenção iniciada pelo utilizador, resultando em eventos agendado não é configurável.</span><span class="sxs-lookup"><span data-stu-id="74b1c-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="74b1c-149">Capacidade está a ser planeada para uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="74b1c-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="74b1c-150">Utilizar a API de Olá</span><span class="sxs-lookup"><span data-stu-id="74b1c-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="74b1c-151">Consulta de eventos</span><span class="sxs-lookup"><span data-stu-id="74b1c-151">Query for events</span></span>
<span data-ttu-id="74b1c-152">Pode consultar eventos agendada, simplesmente ao efetuar o seguinte Olá chamada:</span><span class="sxs-lookup"><span data-stu-id="74b1c-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="74b1c-153">Uma resposta contém uma matriz de eventos agendadas.</span><span class="sxs-lookup"><span data-stu-id="74b1c-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="74b1c-154">Uma matriz vazia significa que não existem atualmente não há eventos agendados.</span><span class="sxs-lookup"><span data-stu-id="74b1c-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="74b1c-155">No caso de olá onde existem eventos agendados, resposta Olá contém uma matriz de eventos:</span><span class="sxs-lookup"><span data-stu-id="74b1c-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="74b1c-156">Propriedades do evento</span><span class="sxs-lookup"><span data-stu-id="74b1c-156">Event properties</span></span>
|<span data-ttu-id="74b1c-157">Propriedade</span><span class="sxs-lookup"><span data-stu-id="74b1c-157">Property</span></span>  |  <span data-ttu-id="74b1c-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="74b1c-158">Description</span></span> |
| - | - |
| <span data-ttu-id="74b1c-159">EventId</span><span class="sxs-lookup"><span data-stu-id="74b1c-159">EventId</span></span> | <span data-ttu-id="74b1c-160">Identificador exclusivo global para este evento.</span><span class="sxs-lookup"><span data-stu-id="74b1c-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="74b1c-161">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="74b1c-161">Example:</span></span> <br><ul><li><span data-ttu-id="74b1c-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="74b1c-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="74b1c-163">EventType</span><span class="sxs-lookup"><span data-stu-id="74b1c-163">EventType</span></span> | <span data-ttu-id="74b1c-164">Impacto faz com que a este evento.</span><span class="sxs-lookup"><span data-stu-id="74b1c-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="74b1c-165">Valores:</span><span class="sxs-lookup"><span data-stu-id="74b1c-165">Values:</span></span> <br><ul><li> <span data-ttu-id="74b1c-166">`Freeze`: Olá Máquina Virtual é agendada toopause para alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="74b1c-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="74b1c-167">Olá CPU está suspenso, mas não há nenhum impacto na memória, ficheiros abertos ou ligações de rede.</span><span class="sxs-lookup"><span data-stu-id="74b1c-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="74b1c-168">`Reboot`: Olá Máquina Virtual está agendada para reiniciar o computador (memória não persistentes é perdida).</span><span class="sxs-lookup"><span data-stu-id="74b1c-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="74b1c-169">`Redeploy`: Olá Máquina Virtual é um nó de tooanother toomove agendada (discos efémeras perdem).</span><span class="sxs-lookup"><span data-stu-id="74b1c-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="74b1c-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="74b1c-170">ResourceType</span></span> | <span data-ttu-id="74b1c-171">Tipo de recurso que afeta este evento.</span><span class="sxs-lookup"><span data-stu-id="74b1c-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="74b1c-172">Valores:</span><span class="sxs-lookup"><span data-stu-id="74b1c-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="74b1c-173">Recursos</span><span class="sxs-lookup"><span data-stu-id="74b1c-173">Resources</span></span>| <span data-ttu-id="74b1c-174">Lista de recursos que tem impacto este evento.</span><span class="sxs-lookup"><span data-stu-id="74b1c-174">List of resources this event impacts.</span></span> <span data-ttu-id="74b1c-175">Isto é garantido toocontain máquinas no máximo uma [domínio de atualização](manage-availability.md), mas não pode conter todas as máquinas no Olá UD.</span><span class="sxs-lookup"><span data-stu-id="74b1c-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="74b1c-176">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="74b1c-176">Example:</span></span> <br><ul><li> <span data-ttu-id="74b1c-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="74b1c-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="74b1c-178">Estado do evento</span><span class="sxs-lookup"><span data-stu-id="74b1c-178">Event Status</span></span> | <span data-ttu-id="74b1c-179">Estado deste evento.</span><span class="sxs-lookup"><span data-stu-id="74b1c-179">Status of this event.</span></span> <br><br> <span data-ttu-id="74b1c-180">Valores:</span><span class="sxs-lookup"><span data-stu-id="74b1c-180">Values:</span></span> <ul><li><span data-ttu-id="74b1c-181">`Scheduled`: Este evento é agendada toostart após a hora de Olá especificada no Olá `NotBefore` propriedade.</span><span class="sxs-lookup"><span data-stu-id="74b1c-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="74b1c-182">`Started`: Este evento foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="74b1c-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="74b1c-183">Não `Completed` ou estado semelhante nunca é fornecido; já não vai ser devolvido eventos hello aquando da conclusão do evento de Olá.</span><span class="sxs-lookup"><span data-stu-id="74b1c-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="74b1c-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="74b1c-184">NotBefore</span></span>| <span data-ttu-id="74b1c-185">Tempo após o qual este evento pode iniciar.</span><span class="sxs-lookup"><span data-stu-id="74b1c-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="74b1c-186">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="74b1c-186">Example:</span></span> <br><ul><li> <span data-ttu-id="74b1c-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="74b1c-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="74b1c-188">Agendamento de eventos</span><span class="sxs-lookup"><span data-stu-id="74b1c-188">Event scheduling</span></span>
<span data-ttu-id="74b1c-189">Cada evento está agendado uma quantidade mínima de tempo em Olá futura com base no tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="74b1c-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="74b1c-190">Este tempo é refletido num evento `NotBefore` propriedade.</span><span class="sxs-lookup"><span data-stu-id="74b1c-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="74b1c-191">EventType</span><span class="sxs-lookup"><span data-stu-id="74b1c-191">EventType</span></span>  | <span data-ttu-id="74b1c-192">Tenha em atenção mínima</span><span class="sxs-lookup"><span data-stu-id="74b1c-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="74b1c-193">Fixar</span><span class="sxs-lookup"><span data-stu-id="74b1c-193">Freeze</span></span>| <span data-ttu-id="74b1c-194">15 minutos</span><span class="sxs-lookup"><span data-stu-id="74b1c-194">15 minutes</span></span> |
| <span data-ttu-id="74b1c-195">Reiniciar</span><span class="sxs-lookup"><span data-stu-id="74b1c-195">Reboot</span></span> | <span data-ttu-id="74b1c-196">15 minutos</span><span class="sxs-lookup"><span data-stu-id="74b1c-196">15 minutes</span></span> |
| <span data-ttu-id="74b1c-197">Voltar a implementar</span><span class="sxs-lookup"><span data-stu-id="74b1c-197">Redeploy</span></span> | <span data-ttu-id="74b1c-198">10 minutos</span><span class="sxs-lookup"><span data-stu-id="74b1c-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="74b1c-199">A partir de um evento</span><span class="sxs-lookup"><span data-stu-id="74b1c-199">Starting an event</span></span> 

<span data-ttu-id="74b1c-200">Depois de ter aprendidas de um evento futura e concluir a lógica de encerramento correto, pode aprovar eventos pendentes Olá efetuando uma `POST` chamar o serviço de metadados de toohello com Olá `EventId`.</span><span class="sxs-lookup"><span data-stu-id="74b1c-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="74b1c-201">Isto indica tooAzure que pode a Encurte notificação mínimo Olá (quando possível).</span><span class="sxs-lookup"><span data-stu-id="74b1c-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="74b1c-202">Confirmar um evento permite Olá eventos tooproceed todas `Resources` no evento Olá, não apenas Olá a máquina virtual que reconhece eventos Olá.</span><span class="sxs-lookup"><span data-stu-id="74b1c-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="74b1c-203">Pode, por conseguinte, optar por tooelect uma confirmação de Olá toocoordinate leader, que pode ser tão simple como máquina primeiro Olá Olá `Resources` campo.</span><span class="sxs-lookup"><span data-stu-id="74b1c-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="74b1c-204">Exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="74b1c-204">PowerShell sample</span></span> 

<span data-ttu-id="74b1c-205">Olá seguintes consultas de exemplo Olá metadados de serviço para os eventos agendados e aprova cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="74b1c-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="74b1c-206">C\# exemplo</span><span class="sxs-lookup"><span data-stu-id="74b1c-206">C\# sample</span></span> 

<span data-ttu-id="74b1c-207">Olá exemplo seguinte é de um cliente simple que comunica com o serviço de metadados de Olá.</span><span class="sxs-lookup"><span data-stu-id="74b1c-207">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="74b1c-208">Eventos agendados podem ser representados Olá seguinte estruturas de dados a utilizar:</span><span class="sxs-lookup"><span data-stu-id="74b1c-208">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="74b1c-209">Olá seguintes consultas de exemplo Olá metadados de serviço para os eventos agendados e aprova cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="74b1c-209">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="74b1c-210">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="74b1c-210">Python sample</span></span> 

<span data-ttu-id="74b1c-211">Olá seguintes consultas de exemplo Olá metadados de serviço para os eventos agendados e aprova cada evento pendente.</span><span class="sxs-lookup"><span data-stu-id="74b1c-211">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="74b1c-212">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="74b1c-212">Next steps</span></span> 

- <span data-ttu-id="74b1c-213">Saiba mais sobre Olá APIs disponíveis no Olá [metadados de instância de serviço](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="74b1c-213">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="74b1c-214">Saiba mais sobre [planeada manutenção de máquinas virtuais do Windows no Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="74b1c-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

