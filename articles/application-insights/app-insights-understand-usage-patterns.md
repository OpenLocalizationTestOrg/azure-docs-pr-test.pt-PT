---
title: aaaAzure Funnels do Application Insights
description: "Saiba como pode utilizar Funnels toodiscover como os clientes estão a interagir com a sua aplicação."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 3a90cfd11cb193e303136504df44008ffd04a290
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="bf342-103">Detetar como os clientes estão a utilizar a aplicação com Olá Funnels do Application Insights</span><span class="sxs-lookup"><span data-stu-id="bf342-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="bf342-104">Experiência do cliente de compreender é de negócio de tooyour Olá utmost importância.</span><span class="sxs-lookup"><span data-stu-id="bf342-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="bf342-105">Se a sua aplicação envolve várias fases, terá tooknow se a maioria dos clientes estão a evoluir através do processo completo de Olá ou se está a terminar processo Olá, a determinada altura.</span><span class="sxs-lookup"><span data-stu-id="bf342-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="bf342-106">evolução Olá através de uma série de passos numa aplicação web é conhecida como "funil".</span><span class="sxs-lookup"><span data-stu-id="bf342-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="bf342-107">Pode utilizar Olá Application Insights Funnels toogain aprofundadas dos seus utilizadores e taxas de conversão passo a passo do monitor.</span><span class="sxs-lookup"><span data-stu-id="bf342-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="bf342-108">Introdução ao painel de Funnels Olá</span><span class="sxs-lookup"><span data-stu-id="bf342-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="bf342-109">Olá toolearn de forma mais fácil sobre Funnels é toowalk, embora um exemplo.</span><span class="sxs-lookup"><span data-stu-id="bf342-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="bf342-110">Olá ilustrações seguintes demonstram proprietários de passos Olá de uma empresa de comércio eletrónico demoraria toolearn como os clientes interagem com a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="bf342-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="bf342-111">Criar a sua funil</span><span class="sxs-lookup"><span data-stu-id="bf342-111">Create your funnel</span></span>
<span data-ttu-id="bf342-112">Antes de criar o funil, terá de toodecide em questão Olá pretende tooanswer.</span><span class="sxs-lookup"><span data-stu-id="bf342-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="bf342-113">Por exemplo, poderá tooknow quantos clientes visualizar o página inicial, clique num anúncio.</span><span class="sxs-lookup"><span data-stu-id="bf342-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="bf342-114">Neste exemplo, proprietários de Olá de Olá empresa Fabrikam fibra pretendem percentagem de Olá tooknow dos clientes que efetuam uma compra depois de adicionar tootheir itens compras carrinho durante Olá último mês.</span><span class="sxs-lookup"><span data-stu-id="bf342-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="bf342-115">Seguem-se passos de Olá que efetuar toocreate os respetivos funil.</span><span class="sxs-lookup"><span data-stu-id="bf342-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="bf342-116">Clique no botão de nova Olá no painel de Funnels Olá.</span><span class="sxs-lookup"><span data-stu-id="bf342-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="bf342-117">Selecione intervalo de tempo de Olá do "Mês" Olá **intervalo de tempo** pendente.</span><span class="sxs-lookup"><span data-stu-id="bf342-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="bf342-118">Selecione Olá **página de produto** evento Olá **passo 1** na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="bf342-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="bf342-119">Selecione Olá **adicionar tooshopping carrinho** evento Olá **passo 2** na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="bf342-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="bf342-120">Selecione Olá **clique Compra** evento Olá **passo 3** na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="bf342-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="bf342-121">Adicionar um funil toohello de nome e clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="bf342-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="bf342-122">Olá ilustração seguinte demonstra Olá dados Olá Funnels painel gera.</span><span class="sxs-lookup"><span data-stu-id="bf342-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="bf342-123">De Olá aqui proprietários da Fabrikam podem ver que, durante a última semana Olá, 22.7% dos clientes que adicionados compras de tootheir um item carrinho compra Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="bf342-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="bf342-124">Pode também ver 1% dos clientes Olá clicado um anúncio, antes de visitando a página de produto Olá e 20% dos clientes terminada depois de concluir as respetivas compra.</span><span class="sxs-lookup"><span data-stu-id="bf342-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Painel funnels com dados](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="bf342-126">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bf342-126">Next steps</span></span>
- <span data-ttu-id="bf342-127">Saiba mais sobre [análise de utilização](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bf342-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
