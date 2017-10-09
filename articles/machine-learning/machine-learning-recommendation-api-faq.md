---
title: "aaaSet cópias de segurança e a utilização Olá recomendações API do Machine Learning | Microsoft Docs"
description: "Microsoft recomendações de API criada com o Azure Machine Learning FAQ"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a><span data-ttu-id="6ddc6-103">FAQ sobre a configuração e utilização da API de Recomendações do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6ddc6-103">Setting up and using Machine Learning Recommendations API FAQ</span></span>
<span data-ttu-id="6ddc6-104">**O que é recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-104">**What is RECOMMENDATIONS?**</span></span>

> [!NOTE]
> <span data-ttu-id="6ddc6-105">Deve começar a utilizar Olá recomendações API cognitivos serviço em vez de nesta versão.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-105">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="6ddc6-106">Olá serviço cognitivos recomendações irá substituir este serviço e todas as novas funcionalidades de Olá irão ser desenvolvidas não existe.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="6ddc6-107">Tem novas capacidades, como a criação de batches de suporte, melhor Explorador de API, uma experiência de inscrição/faturação superfície, mais consistente de API limpeza, etc.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="6ddc6-108">Saiba mais sobre [migrar toohello novo serviço cognitivos](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="6ddc6-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="6ddc6-109">Para as organizações e empresas que se baseiam em recomendações toocross-vende e vende dos produtos e os serviços tootheir clientes, as recomendações no Azure Machine Learning fornece um motor de recomendações self-service.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-109">For organizations and businesses that rely on recommendations toocross-sell and up-sell products and services tootheir customers, RECOMMENDATIONS in Azure Machine Learning provides a self-service recommendations engine.</span></span> <span data-ttu-id="6ddc6-110">É uma implementação de filtragem de colaboração que utiliza factorization matriz como o algoritmo de núcleos.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-110">It is an implementation of collaborative filtering that uses matrix factorization as its core algorithm.</span></span> <span data-ttu-id="6ddc6-111">Os programadores de aplicações podem aceder recomendações utilizando REST APIs.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-111">Application developers can access RECOMMENDATIONS by using REST APIs.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="6ddc6-112">**O que posso fazer com base em recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-112">**What can I do with RECOMMENDATIONS?**</span></span>

<span data-ttu-id="6ddc6-113">RECOMENDAÇÕES aceita como entrada de um item ou um conjunto de itens e devolve uma lista de recomendações relevantes.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-113">RECOMMENDATIONS takes as input an item or a set of items and returns a list of relevant recommendations.</span></span> <span data-ttu-id="6ddc6-114">Por exemplo: um cliente de um revendedor online clica um produto.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-114">For example: A customer of an online retailer clicks a product.</span></span> <span data-ttu-id="6ddc6-115">revendedor online Olá envia o produto como entrada tooRECOMMENDATIONS, obtém uma lista dos produtos em return e decide que estes produtos serão apresentados toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-115">hello online retailer sends that product as input tooRECOMMENDATIONS, gets a list of products in return, and decides which of these products will be shown toohello customer.</span></span> <span data-ttu-id="6ddc6-116">Pode pretender toouse recomendações toooptimize sua loja online ou mesmo tooinform seu interior center departamento ou chamada de venda.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-116">You may want toouse RECOMMENDATIONS toooptimize your online store or even tooinform your inside sales department or call center.</span></span>

<span data-ttu-id="6ddc6-117">**Existem algumas limitações de utilização?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-117">**Are there any usage limitations?**</span></span>

<span data-ttu-id="6ddc6-118">Recomendações tem Olá seguintes limitações de utilização:</span><span class="sxs-lookup"><span data-stu-id="6ddc6-118">Recommendations has hello following usage limitations:</span></span>

* <span data-ttu-id="6ddc6-119">Número máximo de modelos por subscrição: 10</span><span class="sxs-lookup"><span data-stu-id="6ddc6-119">Maximum number of models per subscription: 10</span></span>
* <span data-ttu-id="6ddc6-120">Número máximo de itens que pode conter um catálogo: 100 000</span><span class="sxs-lookup"><span data-stu-id="6ddc6-120">Maximum number of items that a catalog can hold: 100,000</span></span>
* <span data-ttu-id="6ddc6-121">número máximo de Olá de pontos de utilização que são mantidos é ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-121">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="6ddc6-122">Olá mais antigo será eliminado se novos serão carregados ou comunicados.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-122">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="6ddc6-123">Tamanho máximo de dados que podem ser enviados por correio eletrónico (por exemplo, importar dados do catálogo, importar dados de utilização) é 200 MB</span><span class="sxs-lookup"><span data-stu-id="6ddc6-123">Maximum size of data that can be sent in email (for example, import catalog data, import usage data) is 200 MB</span></span>
* <span data-ttu-id="6ddc6-124">Número de transações por segundo (TPS) para uma compilação de modelo de recomendações que não está ativa é TPS ~ 2.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-124">Number of transactions per second (TPS) for a Recommendations model build that is not active is ~2 TPS.</span></span> <span data-ttu-id="6ddc6-125">Uma compilação de modelo de recomendações que Active Directory pode manter cópias de segurança too20 TPS.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-125">A Recommendations model build that is active can hold up too20 TPS.</span></span>

## <a name="purchase-and-billing"></a><span data-ttu-id="6ddc6-126">Compra e Faturação</span><span class="sxs-lookup"><span data-stu-id="6ddc6-126">Purchase and Billing</span></span>
<span data-ttu-id="6ddc6-127">**Quanto custo recomendações durante o período de início de Olá?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-127">**How much does Recommendations cost during hello launch period?**</span></span>

<span data-ttu-id="6ddc6-128">Recomendações é um serviço baseado na subscrição.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-128">Recommendations is a subscription-based service.</span></span> <span data-ttu-id="6ddc6-129">Charging baseia-se no volume de transações por mês.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-129">Charging is based on volume of transactions per month.</span></span> <span data-ttu-id="6ddc6-130">Pode verificar Olá [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations) no Microsoft Azure Marketplace para obter informações sobre preços.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-130">You can check hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) in Microsoft Azure Marketplace for pricing information.</span></span>

<span data-ttu-id="6ddc6-131">**Existem quaisquer custos associados com recomendações a ter controlam e armazenam a atividade do utilizador para mim?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-131">**Are there any costs associated with having Recommendations track and store user activity for me?**</span></span>

<span data-ttu-id="6ddc6-132">Não momento Olá.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-132">Not at hello moment.</span></span>

<span data-ttu-id="6ddc6-133">**A recomendações tem uma versão de avaliação gratuita?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-133">**Does Recommendations have a free trial?**</span></span>

<span data-ttu-id="6ddc6-134">Não há um registo livre que é restrita too10, 000 transações por mês.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-134">There is a free trail which is restricted too10,000 transactions per month.</span></span>

<span data-ttu-id="6ddc6-135">**Quando será posso faturado por recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-135">**When will I be billed for Recommendations?**</span></span>

<span data-ttu-id="6ddc6-136">Uma subscrição paga é nenhuma subscrição para o qual é uma taxa mensal.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-136">A paid subscription is any subscription for which there is a monthly fee.</span></span> <span data-ttu-id="6ddc6-137">Ao adquirir uma subscrição paga, são-lhe imediatamente cobrados para Olá primeiro utilizar do mês.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-137">When you purchase a paid subscription, you are immediately charged for hello first month's use.</span></span> <span data-ttu-id="6ddc6-138">São-lhe cobrados quantidade Olá que está associada a oferta de Olá na página de subscrição de Olá (além de taxas aplicáveis).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-138">You are charged hello amount that is associated with hello offer on hello subscription page (plus applicable taxes).</span></span> <span data-ttu-id="6ddc6-139">Este encargos mensais é efetuado cada mês no Olá mesmo calendário data como compra original até cancelar Olá subscrição.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-139">This monthly charge is made each month on hello same calendar date as your original purchase until you cancel hello subscription.</span></span> 

<span data-ttu-id="6ddc6-140">**Como atualizar o serviço de camada superior tooa?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-140">**How do I upgrade tooa higher tier service?**</span></span>

<span data-ttu-id="6ddc6-141">Pode comprar ou atualizar a sua subscrição do Olá [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations) página no Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-141">You can buy or update your subscription from hello [offer page](https://datamarket.azure.com/dataset/amla/recommendations) page on Microsoft Azure Marketplace.</span></span>

<span data-ttu-id="6ddc6-142">Quando atualiza uma subscrição:</span><span class="sxs-lookup"><span data-stu-id="6ddc6-142">When you upgrade a subscription:</span></span>

* <span data-ttu-id="6ddc6-143">Transações que são restantes na sua subscrição antiga não foram adicionadas tooyour nova subscrição.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-143">Transactions that are remaining on your old subscription are not added tooyour new subscription.</span></span> 
* <span data-ttu-id="6ddc6-144">Paga completo preços nova subscrição de Olá, apesar de a ter transações não utilizadas na sua subscrição antiga.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-144">You pay full price for hello new subscription, even though you have unused transactions on your old subscription.</span></span>

<span data-ttu-id="6ddc6-145">Uma subscrição do processo tooupgrade:</span><span class="sxs-lookup"><span data-stu-id="6ddc6-145">Process tooupgrade a subscription:</span></span>

* <span data-ttu-id="6ddc6-146">Nevigate toohello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-146">Nevigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="6ddc6-147">Inicie sessão no toohello Marketplace se já não são iniciou sessão.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-147">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="6ddc6-148">No painel direito Olá, são listados todos os planos disponíveis de Olá.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-148">In hello right pane, all hello available plans are listed.</span></span> <span data-ttu-id="6ddc6-149">Clique no botão de opção Olá para o plano de Olá que pretende tooupgrade para.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-149">Click hello radio button for hello plan you want tooupgrade to.</span></span>
* <span data-ttu-id="6ddc6-150">Se quiser tooupgrade, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-150">If you want tooupgrade, click **OK**.</span></span> <span data-ttu-id="6ddc6-151">Se não pretender tooupgrade, clique em **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-151">If you do not want tooupgrade, click **Cancel**.</span></span>

<span data-ttu-id="6ddc6-152">**Importante** caixa de diálogo Olá leia cuidadosamente antes de atualizar porque existem implicações de faturação e de utilização.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-152">**Important** Carefully read hello dialog box before you upgrade because there are billing and use implications.</span></span>

<span data-ttu-id="6ddc6-153">**Quando terminará tooRecommendations a minha subscrição?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-153">**When will my subscription tooRecommendations end?**</span></span>

<span data-ttu-id="6ddc6-154">A subscrição terminará quando cancelá-lo.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-154">Your subscription will end when you cancel it.</span></span> <span data-ttu-id="6ddc6-155">Se quiser toocancel as suas subscrições, consulte Olá seguir instruções.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-155">If you would like toocancel your subscriptions, see hello following instructions.</span></span>

<span data-ttu-id="6ddc6-156">**Como cancelar a minha subscrição recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-156">**How do I cancel my Recommendations subscription?**</span></span>

<span data-ttu-id="6ddc6-157">toocancel a sua subscrição, Olá utilize os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-157">toocancel your subscription, use hello following steps.</span></span> <span data-ttu-id="6ddc6-158">Se a sua subscrição atual é uma subscrição paga, a subscrição continua em vigor até fim Olá Olá atual de período de faturação.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-158">If your current subscription is a paid subscription, your subscription continues in effect until hello end of hello current billing period.</span></span> <span data-ttu-id="6ddc6-159">Se precisar de hello cancelamento toobe em vigor imediatamente, contacte-nos [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-159">If you need hello cancellation toobe effective immediately, contact us at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

<span data-ttu-id="6ddc6-160">**Tenha em atenção** não reembolso é dado se cancelar antes do final de Olá de um período de faturação ou de transações não utilizadas num período de faturação.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-160">**Note** No refund is given if you cancel before hello end of a billing period or for unused transactions in a billing period.</span></span>

* <span data-ttu-id="6ddc6-161">Navegue toohello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-161">Navigate toohello [offer page](https://datamarket.azure.com/dataset/amla/recommendations).</span></span>
* <span data-ttu-id="6ddc6-162">Inicie sessão no toohello Marketplace se já não são iniciou sessão.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-162">Sign in toohello Marketplace if you aren't already Signed in.</span></span>
* <span data-ttu-id="6ddc6-163">Clique em **Cancelar** toohello direita do nome do conjunto de dados de Olá e o estado.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-163">Click **Cancel** toohello right of hello dataset name and status.</span></span> <span data-ttu-id="6ddc6-164">Pode utilizar esta subscrição até Olá de Olá atual período ou o limite de transação de faturação é foi atingido um fim (que ocorrer primeiro).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-164">You can use this subscription until hello end of hello current billing period or your transaction limit is reached (whichever occurs first).</span></span>

<span data-ttu-id="6ddc6-165">Se quiser toocancel a sua subscrição imediatamente, por isso, pode comprar uma nova subscrição, um ticket ao [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-165">If you would like toocancel your subscription immediately so you can purchase a new subscription, file a ticket at [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).</span></span>

## <a name="getting-started-with-recommendations"></a><span data-ttu-id="6ddc6-166">Introdução ao recomendações</span><span class="sxs-lookup"><span data-stu-id="6ddc6-166">Getting started with Recommendations</span></span>
<span data-ttu-id="6ddc6-167">**É recomendações para mim?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-167">**Is Recommendations for me?**</span></span> 

<span data-ttu-id="6ddc6-168">Recomendações no Machine Learning é para as organizações e empresas que se baseiam em recomendações toocross vende e cópia de segurança vende produtos ou serviços tootheir clientes.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-168">Recommendations in Machine Learning is for organizations and businesses that rely on recommendations toocross-sell and up-sell products or services tootheir customers.</span></span> <span data-ttu-id="6ddc6-169">Se tiver um Web site orientado para o cliente, uma força de venda, um interior vendedores ou de um centro de atendimento telefónico, e se oferecer um catálogo de mais do que alguns dozen produtos ou serviços, a linha na parte inferior pode beneficiar da utilização recomendações.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-169">If you have a customer-facing website, a sales force, an inside sales force, or a call center, and if you offer a catalog of more than a few dozen products or services, your bottom line may benefit from using Recommendations.</span></span> 

<span data-ttu-id="6ddc6-170">Conseguirmos uma com base em recomendações é concebida toobe bastante simples.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-170">Experimenting with Recommendations is designed toobe fairly simple.</span></span> <span data-ttu-id="6ddc6-171">versão de API com base em atual Olá requer competências de programação básicas.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-171">hello current API-based version requires basic programming skills.</span></span> <span data-ttu-id="6ddc6-172">Se necessitar de assistência, contacte o fornecedor de Olá que desenvolveu o seu Web site.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-172">If you need assistance, contact hello vendor who developed your website.</span></span> <span data-ttu-id="6ddc6-173">Se tiver um departamento de TI interno ou um programador interna, devem ser capaz de tooget recomendações toowork por si.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-173">If you have an internal IT department or an in-house developer, they should be able tooget Recommendations toowork for you.</span></span> 

<span data-ttu-id="6ddc6-174">**Quais são Olá pré-requisitos para configurar as recomendações?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-174">**What are hello prerequisites for setting up Recommendations?**</span></span>

<span data-ttu-id="6ddc6-175">Recomendações requer que tem um registo das opções de utilizador no que respeita tooyour catálogo.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-175">Recommendations requires that you have a log of user choices as it relates tooyour catalog.</span></span> <span data-ttu-id="6ddc6-176">Se não tiver um registo de tal e tiver um Web site com acesso de cliente, recomendações podem recolher a atividade do utilizador para si.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-176">If you don't have such a log and you do have a customer facing website, Recommendations can collect user activity for you.</span></span> 

<span data-ttu-id="6ddc6-177">Recomendações também requer um catálogo dos seus produtos ou serviços.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-177">Recommendations also requires a catalog of your products or services.</span></span> <span data-ttu-id="6ddc6-178">Se não tiver catálogo Olá, recomendações podem utilizar dados de utilização do cliente real Olá e distill um catálogo.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-178">If you don't have hello catalog, Recommendations can use hello actual customer usage data and distill a catalog.</span></span> <span data-ttu-id="6ddc6-179">Um catálogo implícito não irá incluir itens que não foram reportados como parte de transações de utilizador.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-179">An implied catalog will not include items that were not reported as part of user transactions.</span></span>

<span data-ttu-id="6ddc6-180">**Como posso configurar recomendações para Olá pela primeira vez?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-180">**How do I set up Recommendations for hello first time?**</span></span>

<span data-ttu-id="6ddc6-181">Depois de [subscrição](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, deve utilizar documentação Olá API no Olá [recomendações no Azure Machine Learning - Guia Rápido](machine-learning-recommendation-api-quick-start-guide.md) tooset serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-181">After [subscribing](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, you should use hello API documentation in hello [Azure Machine Learning Recommendations - Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md) tooset up hello service.</span></span>

<span data-ttu-id="6ddc6-182">**Onde posso encontrar a documentação da API?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-182">**Where can I find API documentation?**</span></span> 

<span data-ttu-id="6ddc6-183">Olá documentação da API é [Azure Machine Learning recomendações-Guia Rápido](machine-learning-recommendation-api-quick-start-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-183">hello API documentation is [Azure Machine Learning Recommendations -Quick Start Guide](machine-learning-recommendation-api-quick-start-guide.md).</span></span>

<span data-ttu-id="6ddc6-184">**O que fazem opções tenho tooRecommendations de dados de utilização e de catálogo tooupload?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-184">**What options do I have tooupload catalog and usage data tooRecommendations?**</span></span>

<span data-ttu-id="6ddc6-185">Tem duas opções para carregar os dados de utilização e de catálogo: pode exportar os dados de Olá do seu sistema CRM ou outros registos e carregá-la tooRecommendations ou pode adicionar Web site do tooyour etiquetas que irá monitorizar atividades de utilizador.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-185">You have two options for uploading your catalog and usage data: You can export hello data from your CRM system or other logs and upload it tooRecommendations, or you can add tags tooyour website that will track user activities.</span></span> <span data-ttu-id="6ddc6-186">Se utilizar o método última Olá, Olá dados serão armazenados no Azure.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-186">If you use hello latter method, hello data will be stored in Azure.</span></span>

## <a name="maintenance-and-support"></a><span data-ttu-id="6ddc6-187">Suporte e manutenção</span><span class="sxs-lookup"><span data-stu-id="6ddc6-187">Maintenance and support</span></span>
<span data-ttu-id="6ddc6-188">**Grande como podem os meus conjunto de dados ser?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-188">**How large can my data set be?**</span></span>

<span data-ttu-id="6ddc6-189">Cada conjunto de dados pode conter segurança too100, 000 itens de catálogo e cópia de segurança too2048 MB de dados de utilização.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-189">Each data set can contain up too100,000 catalog items and up too2048 MB of usage data.</span></span>
<span data-ttu-id="6ddc6-190">Além disso, pode conter uma subscrição de cópia de segurança too10 conjuntos de dados (modelos).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-190">In addition, a subscription can contain up too10 data sets (models).</span></span>

<span data-ttu-id="6ddc6-191">**Onde posso obter suporte técnico para obter recomendações de?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-191">**Where can I get technical support for Recommendations?**</span></span>

<span data-ttu-id="6ddc6-192">O suporte técnico está disponível no Olá [suporte do Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span><span class="sxs-lookup"><span data-stu-id="6ddc6-192">Technical support is available on hello [Microsoft Azure Support](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.</span></span>

<span data-ttu-id="6ddc6-193">**Onde posso encontrar termos Olá de utilização?**</span><span class="sxs-lookup"><span data-stu-id="6ddc6-193">**Where can I find hello terms of use?**</span></span>

<span data-ttu-id="6ddc6-194">[Microsoft Azure Machine Learning recomendações API termos de serviço](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span><span class="sxs-lookup"><span data-stu-id="6ddc6-194">[Microsoft Azure Machine Learning Recommendations API Terms of Service](https://datamarket.azure.com/dataset/amla/recommendations#terms).</span></span>

