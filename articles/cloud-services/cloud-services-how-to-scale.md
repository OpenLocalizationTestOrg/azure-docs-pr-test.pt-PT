---
title: "aaaAuto dimensionar um serviço em nuvem no portal clássico Olá | Microsoft Docs"
description: "(clássica) Saiba como toouse Olá tooconfigure portal clássico regras de dimensionamento automático para uma função de web do serviço de nuvem ou a função de trabalho no Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="e82d2-103">Como tooconfigure automática de dimensionamento para um serviço em nuvem no portal clássico Olá</span><span class="sxs-lookup"><span data-stu-id="e82d2-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e82d2-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e82d2-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="e82d2-105">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="e82d2-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="e82d2-106">Na página de escala de Olá do Olá portal clássico do Azure, pode configurar as definições de dimensionamento automático para a função da web ou função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e82d2-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="e82d2-107">Em alternativa, pode configurar o dimensionamento manual em vez de com base em regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="e82d2-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="e82d2-108">Este artigo foca-se as funções web e de trabalho do serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e82d2-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="e82d2-109">Quando cria uma máquina virtual (clássica) diretamente, está alojada num serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e82d2-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="e82d2-110">Algumas destas informações aplicam-se os tipos de toothese de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="e82d2-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="e82d2-111">Dimensionamento de um conjunto de disponibilidade de máquinas virtuais está apenas a encerrá-los e desativar a com base nas regras de dimensionamento de Olá que configura.</span><span class="sxs-lookup"><span data-stu-id="e82d2-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="e82d2-112">Para obter mais informações sobre as máquinas virtuais e conjuntos de disponibilidade, consulte [gerir Olá disponibilidade das Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e82d2-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="e82d2-113">Deve considerar Olá seguintes informações antes de configurar o dimensionamento para a sua aplicação:</span><span class="sxs-lookup"><span data-stu-id="e82d2-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="e82d2-114">Dimensionamento é afetado pela utilização do núcleo.</span><span class="sxs-lookup"><span data-stu-id="e82d2-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="e82d2-115">Instâncias de função maior utilizem mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="e82d2-115">Larger role instances use more cores.</span></span> <span data-ttu-id="e82d2-116">Pode dimensionar uma aplicação apenas dentro do limite de Olá de núcleos para a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="e82d2-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="e82d2-117">Por exemplo, diga a que sua subscrição tem um limite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="e82d2-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="e82d2-118">Se executar uma aplicação com dois serviços de cloud média (um total de 4 núcleos), pode apenas Dimensionar outras implementações de serviço em nuvem na sua subscrição por Olá restantes 16 núcleos.</span><span class="sxs-lookup"><span data-stu-id="e82d2-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="e82d2-119">Para obter mais informações acerca dos tamanhos, consulte [tamanhos do serviço em nuvem](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="e82d2-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="e82d2-120">Tem de criar uma fila e associá-la a uma função antes de a poder dimensionar a uma aplicação com base num limiar da mensagem.</span><span class="sxs-lookup"><span data-stu-id="e82d2-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="e82d2-121">Para obter mais informações, consulte [como toouse Olá o serviço de armazenamento de filas](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="e82d2-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="e82d2-122">Pode dimensionar recursos que estão ligado tooyour serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e82d2-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="e82d2-123">Para obter mais informações sobre ligar os recursos, consulte [como: ligar um serviço de nuvem do recurso tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="e82d2-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="e82d2-124">tooenable elevada disponibilidade da aplicação, deve garantir que é implementado com dois ou mais instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="e82d2-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="e82d2-125">Para obter mais informações, consulte [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="e82d2-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="e82d2-126">Dimensionamento de agenda</span><span class="sxs-lookup"><span data-stu-id="e82d2-126">Schedule scaling</span></span>
<span data-ttu-id="e82d2-127">Por predefinição, todas as funções não siga uma agenda específica.</span><span class="sxs-lookup"><span data-stu-id="e82d2-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="e82d2-128">Por conseguinte, aplicam-se as definições alteradas tooall vezes e todos os dias ao longo do ano Olá.</span><span class="sxs-lookup"><span data-stu-id="e82d2-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="e82d2-129">Se quiser, pode configurar o dimensionamento de manual ou automática para um dos seguintes modos de Olá:</span><span class="sxs-lookup"><span data-stu-id="e82d2-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="e82d2-130">Dias da semana</span><span class="sxs-lookup"><span data-stu-id="e82d2-130">Weekdays</span></span>
* <span data-ttu-id="e82d2-131">Fim de semana</span><span class="sxs-lookup"><span data-stu-id="e82d2-131">Weekends</span></span>
* <span data-ttu-id="e82d2-132">Nights semana</span><span class="sxs-lookup"><span data-stu-id="e82d2-132">Week nights</span></span>
* <span data-ttu-id="e82d2-133">Mornings semana</span><span class="sxs-lookup"><span data-stu-id="e82d2-133">Week mornings</span></span>
* <span data-ttu-id="e82d2-134">Datas específicas</span><span class="sxs-lookup"><span data-stu-id="e82d2-134">Specific dates</span></span>
* <span data-ttu-id="e82d2-135">Intervalos de data específica</span><span class="sxs-lookup"><span data-stu-id="e82d2-135">Specific date ranges</span></span>

<span data-ttu-id="e82d2-136">Olá agenda definição é configurada em Olá [portal clássico do Azure](https://manage.windowsazure.com/) no Olá</span><span class="sxs-lookup"><span data-stu-id="e82d2-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="e82d2-137">**Serviços em nuvem** > **\[seu serviço em nuvem\]** > **escala**  >   **\[Produção ou transição\]**  página.</span><span class="sxs-lookup"><span data-stu-id="e82d2-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="e82d2-138">Clique em Olá **configurar vezes agenda** botão para cada função que pretende toochange.</span><span class="sxs-lookup"><span data-stu-id="e82d2-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Dimensionamento automático com base numa agenda o serviço em nuvem][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="e82d2-140">Escala Manual</span><span class="sxs-lookup"><span data-stu-id="e82d2-140">Manual scale</span></span>
<span data-ttu-id="e82d2-141">No Olá **escala** página, pode manualmente aumentar ou diminuir Olá diversas instâncias em execução num serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e82d2-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="e82d2-142">Esta definição estiver configurada para cada agenda criou ou tooall tempo se não tiver criado uma agenda.</span><span class="sxs-lookup"><span data-stu-id="e82d2-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="e82d2-143">No Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços em nuvem**e, em seguida, clique no nome de Olá do dashboard do Olá nuvem serviço tooopen Olá.</span><span class="sxs-lookup"><span data-stu-id="e82d2-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e82d2-144">Se não vir o seu serviço em nuvem, poderá ser necessário toochange de **produção** demasiado**transição** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="e82d2-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="e82d2-145">Clique em **escala**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-145">Click **Scale**.</span></span>
3. <span data-ttu-id="e82d2-146">Selecione o agendamento de Olá pretende toochange dimensionamento opções para.</span><span class="sxs-lookup"><span data-stu-id="e82d2-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="e82d2-147">*Não períodos agendados* é a predefinição de Olá, se tiver não agendamentos definidos.</span><span class="sxs-lookup"><span data-stu-id="e82d2-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="e82d2-148">Determinar Olá **escala da métrica** secção e selecione **NONE**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="e82d2-149">Esta definição é a predefinição de Olá para todas as funções.</span><span class="sxs-lookup"><span data-stu-id="e82d2-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="e82d2-150">Cada função no serviço de nuvem Olá tem um controlo de deslize para alterar o número de Olá de toouse de instâncias.</span><span class="sxs-lookup"><span data-stu-id="e82d2-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![Dimensionar manualmente uma função de serviço em nuvem][manual_scale]
   
    <span data-ttu-id="e82d2-152">Se precisar de mais instâncias, poderá ser necessário toochange Olá [tamanho da máquina virtual de serviço de nuvem](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="e82d2-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="e82d2-153">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-153">Click **Save**.</span></span>  
   <span data-ttu-id="e82d2-154">Instâncias de função são adicionadas ou removidas consoante as suas seleções.</span><span class="sxs-lookup"><span data-stu-id="e82d2-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="e82d2-155">Sempre que consulte ![][tip_icon] mover o rato tooit e pode obter ajuda sobre o que uma definição específica faz.</span><span class="sxs-lookup"><span data-stu-id="e82d2-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="e82d2-156">Escala automática - CPU</span><span class="sxs-lookup"><span data-stu-id="e82d2-156">Automatic scale - CPU</span></span>
<span data-ttu-id="e82d2-157">Este modo dimensiona se percentagem média do Olá de utilização da CPU ficar acima ou abaixo limiares especificados.</span><span class="sxs-lookup"><span data-stu-id="e82d2-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="e82d2-158">Instâncias de função são criadas ou eliminadas quando isto acontece.</span><span class="sxs-lookup"><span data-stu-id="e82d2-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="e82d2-159">No Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços em nuvem**e, em seguida, clique no nome de Olá do dashboard do Olá nuvem serviço tooopen Olá.</span><span class="sxs-lookup"><span data-stu-id="e82d2-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e82d2-160">Se não vir o seu serviço em nuvem, poderá ser necessário toochange de **produção** demasiado**transição** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="e82d2-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="e82d2-161">Clique em **escala**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-161">Click **Scale**.</span></span>
3. <span data-ttu-id="e82d2-162">Selecione o agendamento de Olá pretende toochange dimensionamento opções para.</span><span class="sxs-lookup"><span data-stu-id="e82d2-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="e82d2-163">*Não períodos agendados* é a predefinição de Olá, se tiver não agendamentos definidos.</span><span class="sxs-lookup"><span data-stu-id="e82d2-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="e82d2-164">Determinar Olá **escala da métrica** secção e selecione **CPU**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="e82d2-165">Agora pode configurar um intervalo mínimo e máximo de instâncias de funções, utilização de CPU de destino Olá (tootrigger um trabalho de dimensionamento) e quantas instâncias tooscale e reduzir verticalmente pelo.</span><span class="sxs-lookup"><span data-stu-id="e82d2-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![Dimensionar uma função de serviço de nuvem por carga de cpu][cpu_scale]

> [!TIP]
> <span data-ttu-id="e82d2-167">Sempre que consulte ![][tip_icon] mover o rato tooit e pode obter ajuda sobre o que uma definição específica faz.</span><span class="sxs-lookup"><span data-stu-id="e82d2-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="e82d2-168">Escala automática - a fila</span><span class="sxs-lookup"><span data-stu-id="e82d2-168">Automatic scale - Queue</span></span>
<span data-ttu-id="e82d2-169">Este modo dimensiona automaticamente se Olá número de mensagens numa fila ficar acima ou abaixo de um limiar especificado.</span><span class="sxs-lookup"><span data-stu-id="e82d2-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="e82d2-170">Instâncias de função são criadas ou eliminadas quando isto acontece.</span><span class="sxs-lookup"><span data-stu-id="e82d2-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="e82d2-171">No Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços em nuvem**e, em seguida, clique no nome de Olá do dashboard do Olá nuvem serviço tooopen Olá.</span><span class="sxs-lookup"><span data-stu-id="e82d2-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e82d2-172">Se não vir o seu serviço em nuvem, poderá ser necessário toochange de **produção** demasiado**transição** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="e82d2-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="e82d2-173">Clique em **escala**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-173">Click **Scale**.</span></span>
3. <span data-ttu-id="e82d2-174">Determinar Olá **escala da métrica** secção e selecione **fila**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="e82d2-175">Agora pode configurar um intervalo mínimo e máximo de instâncias de funções, fila de Olá e número de mensagens de fila tooprocess para cada instância e quantas instâncias tooscale, acima e abaixo pelo.</span><span class="sxs-lookup"><span data-stu-id="e82d2-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![Dimensionar uma função de serviço de nuvem por uma fila de mensagens][queue_scale]

> [!TIP]
> <span data-ttu-id="e82d2-177">Sempre que consulte ![][tip_icon] mover o rato tooit e pode obter ajuda sobre o que uma definição específica faz.</span><span class="sxs-lookup"><span data-stu-id="e82d2-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="e82d2-178">Dimensionar recursos ligados</span><span class="sxs-lookup"><span data-stu-id="e82d2-178">Scale linked resources</span></span>
<span data-ttu-id="e82d2-179">Frequentemente, quando dimensionar uma função, seja a base de dados do tooscale benéfico Olá que aplicação Olá está também a utilizar.</span><span class="sxs-lookup"><span data-stu-id="e82d2-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="e82d2-180">Se ligar o serviço de nuvem de toohello de base de dados de Olá, pode aceder a Olá dimensionamento definições para o recurso de clicando Olá de ligação adequado.</span><span class="sxs-lookup"><span data-stu-id="e82d2-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="e82d2-181">No Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços em nuvem**e, em seguida, clique no nome de Olá do dashboard do Olá nuvem serviço tooopen Olá.</span><span class="sxs-lookup"><span data-stu-id="e82d2-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e82d2-182">Se não vir o seu serviço em nuvem, poderá ser necessário toochange de **produção** demasiado**transição** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="e82d2-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="e82d2-183">Clique em **escala**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-183">Click **Scale**.</span></span>
3. <span data-ttu-id="e82d2-184">Determinar Olá **ligado recursos** secção e clique em **gerir escala desta base de dados**.</span><span class="sxs-lookup"><span data-stu-id="e82d2-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e82d2-185">Se não vir um **ligado recursos** secção, provavelmente, não tem quaisquer recursos ligados.</span><span class="sxs-lookup"><span data-stu-id="e82d2-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
