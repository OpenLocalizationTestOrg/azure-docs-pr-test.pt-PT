---
title: "comportamento de aaaOverride HTTP utilizando o motor de regras do Olá CDN do Azure | Microsoft Docs"
description: "o motor de regras de Olá permite-lhe toocustomize como os pedidos de HTTP são processados pela CDN do Azure, tal como está a bloquear Olá entrega de determinados tipos de conteúdo, definir uma política de colocação em cache e modificar os cabeçalhos de HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="22431-103">Substituir o comportamento HTTP utilizando o motor de regras do Olá CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="22431-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="22431-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="22431-104">Overview</span></span>
<span data-ttu-id="22431-105">o motor de regras de Olá permite-lhe toocustomize como pedidos de HTTP são processados, por exemplo, entrega de Olá de determinados tipos de conteúdo a bloquear, definir uma política de colocação em cache e modificar os cabeçalhos de HTTP.</span><span class="sxs-lookup"><span data-stu-id="22431-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="22431-106">Este tutorial demonstrar criar uma regra que irá alterar Olá comportamento de ativos CDN a colocação em cache.</span><span class="sxs-lookup"><span data-stu-id="22431-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="22431-107">Há também conteúdo de vídeo disponível no Olá "[Consulte também](#see-also)" secção.</span><span class="sxs-lookup"><span data-stu-id="22431-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="22431-108">Para uma sintaxe de toohello de referência em detalhe, consulte [regras motor referência](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="22431-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="22431-109">Tutorial</span><span class="sxs-lookup"><span data-stu-id="22431-109">Tutorial</span></span>
1. <span data-ttu-id="22431-110">No painel do perfil da CDN Olá, clique em Olá **gerir** botão.</span><span class="sxs-lookup"><span data-stu-id="22431-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Botão de gerir do painel do perfil da CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="22431-112">portal de gestão de CDN Olá abre.</span><span class="sxs-lookup"><span data-stu-id="22431-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="22431-113">Clique em Olá **HTTP grande** separador, seguido de **motor de regras**.</span><span class="sxs-lookup"><span data-stu-id="22431-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="22431-114">São apresentadas as opções para uma nova regra.</span><span class="sxs-lookup"><span data-stu-id="22431-114">Options for a new rule are displayed.</span></span>
   
    ![Novas opções de regra CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="22431-116">ordem de Olá em que várias regras estão listadas afeta a forma como são processadas.</span><span class="sxs-lookup"><span data-stu-id="22431-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="22431-117">Uma regra subsequente pode substituir as ações de Olá especificadas por uma regra de anterior.</span><span class="sxs-lookup"><span data-stu-id="22431-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="22431-118">Introduza um nome na Olá **nome / descrição** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="22431-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="22431-119">Identifique o tipo de Olá de pedidos Olá regra será aplicada a.</span><span class="sxs-lookup"><span data-stu-id="22431-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="22431-120">Por predefinição, Olá **sempre** está selecionada condição de correspondência.</span><span class="sxs-lookup"><span data-stu-id="22431-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="22431-121">Irá utilizar **sempre** para este tutorial, por isso deixe que selecionou.</span><span class="sxs-lookup"><span data-stu-id="22431-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condição de correspondência CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="22431-123">Existem muitos tipos de correspondência de condições disponíveis no menu pendente de Olá.</span><span class="sxs-lookup"><span data-stu-id="22431-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="22431-124">Clicar no Olá azul ícone informativa toohello esquerda da condição de correspondência de Olá explicar condição Olá atualmente selecionado em detalhe.</span><span class="sxs-lookup"><span data-stu-id="22431-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="22431-125">Para Olá a lista completa de expressões condicionais com detalhes, consulte [expressões condicionais do motor de regras](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="22431-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="22431-126">Para Olá obter uma lista completa das condições de correspondência em detalhe, consulte [condições de corresponder ao motor de regras](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="22431-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="22431-127">Clique em Olá  **+**  no botão seguinte demasiado**funcionalidades** tooadd uma nova funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="22431-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="22431-128">Na lista pendente de Olá Olá esquerda, selecione **idade de máxima de interno Force**.</span><span class="sxs-lookup"><span data-stu-id="22431-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="22431-129">Olá caixa de texto que aparece, introduza **300**.</span><span class="sxs-lookup"><span data-stu-id="22431-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="22431-130">Deixe Olá restantes valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="22431-130">Leave hello remaining default values.</span></span>
   
   ![Funcionalidade CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="22431-132">Como com condições de correspondência, clicando em Olá azul ícone informativa toohello esquerda do Olá nova funcionalidade apresentará detalhes sobre esta funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="22431-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="22431-133">No caso de Olá de **idade de máxima de interno Force**, iremos são a substituir o recurso de Olá **Cache-Control** e **expira** cabeçalhos toocontrol quando o nó de extremidade CDN Olá atualizará Olá recurso de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="22431-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="22431-134">Nosso exemplo de 300 segundos significa nó de extremidade CDN Olá irão colocar em cache asset Olá 5 minutos antes de atualizar o recurso de Olá de origem.</span><span class="sxs-lookup"><span data-stu-id="22431-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="22431-135">Para Olá obter uma lista completa das funcionalidades em detalhe, consulte [detalhes de funcionalidade do motor de regras](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="22431-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="22431-136">Clique em Olá **adicionar** nova regra do botão toosave Olá.</span><span class="sxs-lookup"><span data-stu-id="22431-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="22431-137">nova regra de Olá agora está a aguardar aprovação.</span><span class="sxs-lookup"><span data-stu-id="22431-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="22431-138">Quando for aprovado, o estado de Olá deixará de **XML pendente** demasiado**XML Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="22431-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="22431-139">Alterações de regras podem demorar até too90 minutos toopropagate através de Olá CDN.</span><span class="sxs-lookup"><span data-stu-id="22431-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="22431-140">Consultar também</span><span class="sxs-lookup"><span data-stu-id="22431-140">See also</span></span>
* [<span data-ttu-id="22431-141">Descrição geral da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="22431-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="22431-142">Referência do motor de regras</span><span class="sxs-lookup"><span data-stu-id="22431-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="22431-143">Condições de correspondência do motor de regras</span><span class="sxs-lookup"><span data-stu-id="22431-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="22431-144">Expressões condicionais de motor de regras</span><span class="sxs-lookup"><span data-stu-id="22431-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="22431-145">Funcionalidades do motor de regras</span><span class="sxs-lookup"><span data-stu-id="22431-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="22431-146">Substituir o comportamento HTTP predefinido utilizando o motor de regras de Olá</span><span class="sxs-lookup"><span data-stu-id="22431-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="22431-147">[Azure sextas: Poderosas novo as funcionalidades Azure CDN Premium](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (vídeo)</span><span class="sxs-lookup"><span data-stu-id="22431-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>