---
title: "implementação do Mobile Engagement aaaAzure para a aplicação de jogos"
description: "Tooimplement de cenário de aplicação de jogos do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="8fda3-103">Implementar o Mobile Engagement com a aplicação de jogos</span><span class="sxs-lookup"><span data-stu-id="8fda3-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="8fda3-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="8fda3-104">Overview</span></span>
<span data-ttu-id="8fda3-105">Um arranque de jogos tem de iniciar uma aplicação de jogos de role-play/estratégia de fishing com base.</span><span class="sxs-lookup"><span data-stu-id="8fda3-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="8fda3-106">jogos de Olá foi configurado e em execução durante 6 meses.</span><span class="sxs-lookup"><span data-stu-id="8fda3-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="8fda3-107">Este jogo enorme concluído com êxito e tem milhões de transferências e se o período de retenção do Olá é tooother muito elevada em comparação com arranque jogos aplicações.</span><span class="sxs-lookup"><span data-stu-id="8fda3-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="8fda3-108">A reunião de revisão trimestral Olá, intervenientes concordarem que precisam tooincrease média de receitas por utilizador (ARPU).</span><span class="sxs-lookup"><span data-stu-id="8fda3-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="8fda3-109">Pacotes de no jogo Premium estão disponíveis como ofertas especiais.</span><span class="sxs-lookup"><span data-stu-id="8fda3-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="8fda3-110">Estes pacotes de jogos permitem aspecto de Olá tooupgrade de utilizadores e o desempenho da respetiva linhas fishing e lures ou tackles no jogo Olá.</span><span class="sxs-lookup"><span data-stu-id="8fda3-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="8fda3-111">No entanto, as vendas do pacote são muito baixos.</span><span class="sxs-lookup"><span data-stu-id="8fda3-111">However, package sales are very low.</span></span> <span data-ttu-id="8fda3-112">Para decidirem experiência de cliente de Olá tooanalyze primeiro com uma ferramenta de análise e, em seguida, toodevelop utilizando um envolvimento programa tooincrease vendas avançadas segmentação.</span><span class="sxs-lookup"><span data-stu-id="8fda3-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="8fda3-113">Com base no Olá [Azure Mobile Engagement – guia de introdução com melhores práticas](mobile-engagement-getting-started-best-practices.md) criem uma estratégia de envolvimento.</span><span class="sxs-lookup"><span data-stu-id="8fda3-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="8fda3-114">Objetivos e KPIs</span><span class="sxs-lookup"><span data-stu-id="8fda3-114">Objectives and KPIs</span></span>
<span data-ttu-id="8fda3-115">Principais intervenientes para jogo Olá cumpram.</span><span class="sxs-lookup"><span data-stu-id="8fda3-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="8fda3-116">Todos os concorda com um objetivo de principal - vendas de pacote premium tooincrease por 15%.</span><span class="sxs-lookup"><span data-stu-id="8fda3-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="8fda3-117">Criarem toomeasure indicadores do negócio chave de desempenho (KPIs) e unidade neste objetivo</span><span class="sxs-lookup"><span data-stu-id="8fda3-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="8fda3-118">O nível do jogo Olá estes pacotes adquiridos?</span><span class="sxs-lookup"><span data-stu-id="8fda3-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="8fda3-119">O que é receitas Olá por utilizador, por sessão, por semana e por mês?</span><span class="sxs-lookup"><span data-stu-id="8fda3-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="8fda3-120">Quais são os tipos de compra favorito Olá?</span><span class="sxs-lookup"><span data-stu-id="8fda3-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="8fda3-121">Parte 1 de Olá [guia de introdução](mobile-engagement-getting-started-best-practices.md) explica como toodefine Olá objetivos e KPIs.</span><span class="sxs-lookup"><span data-stu-id="8fda3-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="8fda3-122">Com Olá que KPIs de empresas agora definidas, Olá Mobile produto Manager cria e retenção de tendências de utilizador novo toodetermine KPIs de envolvimento.</span><span class="sxs-lookup"><span data-stu-id="8fda3-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="8fda3-123">Monitorizar a retenção e utilize em Olá intervalos os seguintes: diariamente, a cada 2 dias, semanalmente, mensalmente e todos os 3 meses</span><span class="sxs-lookup"><span data-stu-id="8fda3-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="8fda3-124">Contagens de utilizadores do Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fda3-124">Active user counts</span></span>
* <span data-ttu-id="8fda3-125">classificação da aplicação Olá no Olá armazenar</span><span class="sxs-lookup"><span data-stu-id="8fda3-125">hello app rating in hello store</span></span>

<span data-ttu-id="8fda3-126">Com base na recomendações da equipa de TI de Olá, Olá KPIs técnicos a seguir foram adicionado Olá tooanswer seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="8fda3-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="8fda3-127">O que é o meu caminho de utilizador (visitada, a qual página quanto tempo que o utilizador dedica nela)</span><span class="sxs-lookup"><span data-stu-id="8fda3-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="8fda3-128">Número de falhas ou erros que encontrou por sessão</span><span class="sxs-lookup"><span data-stu-id="8fda3-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="8fda3-129">Quais as versões de SO executam os meus utilizadores?</span><span class="sxs-lookup"><span data-stu-id="8fda3-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="8fda3-130">O que é o tamanho médio de Olá do ecrã para os meus utilizadores?</span><span class="sxs-lookup"><span data-stu-id="8fda3-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="8fda3-131">Que tipo de ligação à internet dispõe os meus utilizadores?</span><span class="sxs-lookup"><span data-stu-id="8fda3-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="8fda3-132">Para cada KPI Olá Mobile produto Manager Especifica dados Olá que precisa e onde está localizado no respetivo manual de comunicação social.</span><span class="sxs-lookup"><span data-stu-id="8fda3-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="8fda3-133">Programa de envolvimento e a integração</span><span class="sxs-lookup"><span data-stu-id="8fda3-133">Engagement program and integration</span></span>
<span data-ttu-id="8fda3-134">Antes de criar um programa de envolvimento avançadas, Olá Director do projeto de Mobile responsável pela projeto Olá deve ter uma compreensão profunda sobre como e quando os produtos são consumidos pelos utilizadores de Olá.</span><span class="sxs-lookup"><span data-stu-id="8fda3-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="8fda3-135">Depois de 3 meses, Olá Director do projeto de Mobile recolheu suficiente tooenhance dados STA vendas de notificação push na aplicação.</span><span class="sxs-lookup"><span data-stu-id="8fda3-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="8fda3-136">Ele aprende que:</span><span class="sxs-lookup"><span data-stu-id="8fda3-136">He learns that:</span></span>

* <span data-ttu-id="8fda3-137">Compra primeiro Olá geralmente ocorre ao nível de Olá 14.</span><span class="sxs-lookup"><span data-stu-id="8fda3-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="8fda3-138">Para 90% nesses casos, compra de Olá destina-se a nova weapons legendary $3.</span><span class="sxs-lookup"><span data-stu-id="8fda3-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="8fda3-139">No 80% nesses casos, os utilizadores que efetuou uma compra, continuar com o produto Olá e tornar mais adquire.</span><span class="sxs-lookup"><span data-stu-id="8fda3-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="8fda3-140">Os utilizadores que passaram a nível de Olá 20, iniciar toospend mais de 10 $/ semana.</span><span class="sxs-lookup"><span data-stu-id="8fda3-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="8fda3-141">Os utilizadores tendem a pacotes de premium toobuy nível 16, 24 e 32.</span><span class="sxs-lookup"><span data-stu-id="8fda3-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="8fda3-142">Obrigado analysis toothis Olá Director do projeto de Mobile decide toocreate push específicos notificação sequências tooincrease no vendas da aplicação.</span><span class="sxs-lookup"><span data-stu-id="8fda3-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="8fda3-143">Ele cria três sequências de push que ele chama: bem-vindo programa, o programa de vendas e o programa inativa.</span><span class="sxs-lookup"><span data-stu-id="8fda3-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="8fda3-144">Para obter mais informações consulte toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="8fda3-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
