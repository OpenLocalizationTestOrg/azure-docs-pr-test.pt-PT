---
title: "aaaGet iniciada com uma escala automática através da métrica personalizada no Azure | Microsoft Docs"
description: "Saiba como tooscale o recurso da métrica personalizada no Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="5ff92-103">Começar com uma escala automática da métrica personalizada no Azure</span><span class="sxs-lookup"><span data-stu-id="5ff92-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="5ff92-104">Este artigo descreve como tooscale seu recurso por uma métrica personalizada no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff92-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="5ff92-105">Escala de automática de Monitor do Azure aplicam-se apenas tooVirtual conjuntos de dimensionamento de máquina (VMSS), cloud services, planos de serviço de aplicações e ambientes do app service.</span><span class="sxs-lookup"><span data-stu-id="5ff92-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="5ff92-106">Permite começar a utilizar</span><span class="sxs-lookup"><span data-stu-id="5ff92-106">Lets get started</span></span>
<span data-ttu-id="5ff92-107">Este artigo pressupõe que tem uma aplicação web com o application insights configurados.</span><span class="sxs-lookup"><span data-stu-id="5ff92-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="5ff92-108">Se ainda não tiver uma, pode [configurar o Application Insights para o seu Web site ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="5ff92-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="5ff92-109">Abra [portal do Azure][2]</span><span class="sxs-lookup"><span data-stu-id="5ff92-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="5ff92-110">Clique no ícone de Monitor do Azure no painel de navegação esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="5ff92-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="5ff92-111">![Iniciar o Monitor do Azure][3]</span><span class="sxs-lookup"><span data-stu-id="5ff92-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="5ff92-112">Clique na definição tooview todos os recursos de Olá para que automaticamente a escala é aplicável, juntamente com o respetivo estado atual do dimensionamento automático de dimensionamento automático ![detetar escala automática no monitor do Azure][4]</span><span class="sxs-lookup"><span data-stu-id="5ff92-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="5ff92-113">Abra o painel de 'dimensionamento automático' no Monitor do Azure e selecione um recurso pretende tooscale</span><span class="sxs-lookup"><span data-stu-id="5ff92-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="5ff92-114">Nota: os passos de Olá abaixo utilizam um plano de serviço de aplicação associado uma aplicação web que tem informações de aplicação configuradas.</span><span class="sxs-lookup"><span data-stu-id="5ff92-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="5ff92-115">No painel de definição de dimensionamento de Olá para o recurso de Olá, tenha em atenção que a contagem atual de instâncias de Olá é 1.</span><span class="sxs-lookup"><span data-stu-id="5ff92-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="5ff92-116">Clique em 'Ativar dimensionamento automático'.</span><span class="sxs-lookup"><span data-stu-id="5ff92-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="5ff92-117">![Definição de dimensionamento para a nova aplicação web][5]</span><span class="sxs-lookup"><span data-stu-id="5ff92-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="5ff92-118">Forneça um nome para a definição de dimensionamento de Olá e Olá, clique em "Adicionar uma regra".</span><span class="sxs-lookup"><span data-stu-id="5ff92-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="5ff92-119">Tenha em atenção Olá escala opções da regra que abre-se como um painel de contexto Olá lado direito.</span><span class="sxs-lookup"><span data-stu-id="5ff92-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="5ff92-120">Por predefinição, define Olá opção tooscale sua instância contagem por 1 se Olá CPU percetage do recurso de Olá exceder 70%.</span><span class="sxs-lookup"><span data-stu-id="5ff92-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="5ff92-121">Origem de métrica de Olá de alteração na parte superior do Olá demasiado "Application Insights", selecione Olá app insights recurso Olá 'Resource' pendente e métrica personalizada, em seguida, selecione de Olá com base no qual pretende tooscale.</span><span class="sxs-lookup"><span data-stu-id="5ff92-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="5ff92-122">![Dimensionar por métrica personalizada][6]</span><span class="sxs-lookup"><span data-stu-id="5ff92-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="5ff92-123">Semelhante passo toohello acima, adicione uma regra de escala que irá aumentar no e diminuir a contagem de escalas Olá por 1 se a métrica personalizada Olá está abaixo de um limiar.</span><span class="sxs-lookup"><span data-stu-id="5ff92-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="5ff92-124">![Escala com base na cpu][7]</span><span class="sxs-lookup"><span data-stu-id="5ff92-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="5ff92-125">Definir Olá instância limites.</span><span class="sxs-lookup"><span data-stu-id="5ff92-125">Set hello you instance limits.</span></span> <span data-ttu-id="5ff92-126">Por exemplo, se quiser tooscale entre instâncias de 2 a 5 consoante flutuações de métrica personalizada Olá, definir 'mínima' demasiado '2', 'máximo' demasiado '5' e 'default' demasiado '2'</span><span class="sxs-lookup"><span data-stu-id="5ff92-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="5ff92-127">Nota: no caso de existir um problema ao ler métricas de recurso Olá e capacidade atual da Olá é inferior a capacidade predefinida de Olá, em seguida, disponibilidade de Olá tooensure do recurso de Olá, dimensionamento automático irá aumentar horizontalmente valor predefinido de toohello.</span><span class="sxs-lookup"><span data-stu-id="5ff92-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="5ff92-128">Se a capacidade atual da Olá já é superior à capacidade predefinida, o dimensionamento automático não será dimensionado no.</span><span class="sxs-lookup"><span data-stu-id="5ff92-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="5ff92-129">Clique em 'Guardar'</span><span class="sxs-lookup"><span data-stu-id="5ff92-129">Click on 'Save'</span></span>

<span data-ttu-id="5ff92-130">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="5ff92-130">Congratulations.</span></span> <span data-ttu-id="5ff92-131">Agora agora com êxito criado a sua tooauto de definição de dimensionamento dimensionamento da sua aplicação web com base numa métrica personalizada.</span><span class="sxs-lookup"><span data-stu-id="5ff92-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="5ff92-132">Nota: Olá mesmos passos são aplicável tooget iniciada com uma função de serviço VMSS ou nuvem.</span><span class="sxs-lookup"><span data-stu-id="5ff92-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
