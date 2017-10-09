---
title: "aaaCreate, ligar, eliminar ou mover uma conta de integração em aplicações lógicas do Azure | Microsoft Docs"
description: "Como toocreate uma integração conta e ligá-lo tooyour logic apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="d93ac-103">O que é uma conta de integração?</span><span class="sxs-lookup"><span data-stu-id="d93ac-103">What is an integration account?</span></span>

<span data-ttu-id="d93ac-104">Uma conta de integração permite que aplicações de integração do enterprise toomanage artefactos, incluindo esquemas, mapas, certificados, parceiros e contratos.</span><span class="sxs-lookup"><span data-stu-id="d93ac-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="d93ac-105">Qualquer aplicação de integração que criar utiliza um tooaccess de conta de integração estes esquemas, mapas, certificados e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="d93ac-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="d93ac-106">Criar uma conta de integração</span><span class="sxs-lookup"><span data-stu-id="d93ac-106">Create an integration account</span></span>

1.  <span data-ttu-id="d93ac-107">Inicie sessão no toohello [portal do Azure](http://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="d93ac-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="d93ac-108">No menu à esquerda de Olá, selecione **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-108">From hello left menu, select **More services**.</span></span>

    ![Selecione "Mais serviços"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="d93ac-110">Na caixa de pesquisa de Olá, escreva "" integração para o filtro.</span><span class="sxs-lookup"><span data-stu-id="d93ac-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="d93ac-111">Na lista de resultados de Olá, selecione **contas de automatização**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtrar por "integração", selecione "Contas de automatização"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="d93ac-113">Em Olá parte superior da página Olá, escolha **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-113">At hello top of hello page, choose **Add**.</span></span>

    ![Escolher adicionar](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="d93ac-115">A conta de integração e selecione Olá subscrição do Azure que pretende que o toouse de nomes.</span><span class="sxs-lookup"><span data-stu-id="d93ac-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="d93ac-116">Pode criar um novo **grupo de recursos** ou selecione um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="d93ac-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="d93ac-117">Em seguida, selecione um **localização** para alojar a sua conta de integração e um **escalão de preço**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="d93ac-118">Quando estiver pronto, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-118">When you're ready, choose **Create**.</span></span>

    ![Forneça detalhes para a sua conta de integração](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="d93ac-120">Azure Aprovisiona a sua conta de integração na localização de Olá selecionado, o que deve ser concluído dentro de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="d93ac-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="d93ac-121">Atualize a página Olá.</span><span class="sxs-lookup"><span data-stu-id="d93ac-121">Refresh hello page.</span></span> <span data-ttu-id="d93ac-122">Consulte a nova conta de integração listada.</span><span class="sxs-lookup"><span data-stu-id="d93ac-122">You see your new integration account listed.</span></span>

    ![É apresentada a sua nova conta de integração](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="d93ac-124">Em seguida, associe a Olá integração conta que é criado tooyour aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="d93ac-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="d93ac-125">Ligar uma aplicação de lógica de tooa da conta de integração</span><span class="sxs-lookup"><span data-stu-id="d93ac-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="d93ac-126">toogive aceder às suas logic apps toomaps, esquemas, contratos e outros objetos na sua conta de integração, a aplicação de lógica de tooyour integração conta ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="d93ac-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d93ac-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d93ac-127">Prerequisites</span></span>

* <span data-ttu-id="d93ac-128">Uma conta de integração</span><span class="sxs-lookup"><span data-stu-id="d93ac-128">An integration account</span></span>
* <span data-ttu-id="d93ac-129">Uma aplicação lógica</span><span class="sxs-lookup"><span data-stu-id="d93ac-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="d93ac-130">Certifique-se a aplicação de conta e a lógica de integração Olá *mesma localização do Azure* antes de começar.</span><span class="sxs-lookup"><span data-stu-id="d93ac-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="d93ac-131">Olá portal do Azure, selecione a sua aplicação lógica e verifique a localização da sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="d93ac-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Selecione a sua aplicação lógica, verifique a localização](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="d93ac-133">Em **definições**, selecione **Integration Account**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Selecione "Conta de integração"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="d93ac-135">De Olá **selecionar uma conta de integração** lista, a conta de integração de Olá selecione pretende que a aplicação de lógica de tooyour toolink.</span><span class="sxs-lookup"><span data-stu-id="d93ac-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="d93ac-136">toofinish da ligação, escolha **guardar**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-136">toofinish linking, choose **Save**.</span></span>

    ![Selecione a sua conta de integração](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="d93ac-138">Receberá uma notificação que apresenta a integração de conta é a aplicação de lógica de tooyour ligado e que todos os artefactos na sua conta de integração estão agora disponíveis tooyour aplicação de lógica.</span><span class="sxs-lookup"><span data-stu-id="d93ac-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Está ligada a sua aplicação lógica tooyour conta de integração](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="d93ac-140">Agora que a sua conta de integração é a aplicação de lógica de tooyour ligado, pode utilizar os conectores de Olá B2B nas suas logic apps.</span><span class="sxs-lookup"><span data-stu-id="d93ac-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="d93ac-141">Alguns conectores B2B comuns incluem validação XML e Codificar/descodificar com ficheiros simples.</span><span class="sxs-lookup"><span data-stu-id="d93ac-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="d93ac-142">Eliminar a conta de integração</span><span class="sxs-lookup"><span data-stu-id="d93ac-142">Delete your integration account</span></span>

1. <span data-ttu-id="d93ac-143">Selecione **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-143">Select **More services**.</span></span>

    ![Selecione "Mais serviços"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="d93ac-145">Na caixa de pesquisa de Olá, escreva "" integração para o filtro.</span><span class="sxs-lookup"><span data-stu-id="d93ac-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="d93ac-146">Na lista de resultados de Olá, selecione **contas de automatização**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtrar por "integração", selecione "Contas de automatização"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="d93ac-148">Selecione a conta de integração de Olá que pretende que o toodelete.</span><span class="sxs-lookup"><span data-stu-id="d93ac-148">Select hello integration account that you want toodelete.</span></span>

    ![Selecione toodelete de conta de integração](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="d93ac-150">No menu de Olá, escolha **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-150">On hello menu, choose **Delete**.</span></span>

    ![Escolha "Eliminar"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="d93ac-152">Confirme a sua conta de integração de Olá choice toodelete.</span><span class="sxs-lookup"><span data-stu-id="d93ac-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="d93ac-153">Mover a sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="d93ac-153">Move your integration account</span></span>

<span data-ttu-id="d93ac-154">toomove um tooanother de conta de integração do Azure subscrição ou grupo de recursos, siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="d93ac-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d93ac-155">Tem de atualizar todos os scripts toouse Olá novos IDs de recurso depois de mover uma conta de integração.</span><span class="sxs-lookup"><span data-stu-id="d93ac-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="d93ac-156">Selecione **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-156">Select **More services**.</span></span>

    ![Selecione "Mais serviços"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="d93ac-158">Na caixa de pesquisa de Olá, escreva "" integração para o filtro.</span><span class="sxs-lookup"><span data-stu-id="d93ac-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="d93ac-159">Na lista de resultados de Olá, selecione **contas de automatização**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtrar por "integração", selecione "Contas de automatização"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="d93ac-161">Selecione a conta de integração de Olá que pretende que o toomove.</span><span class="sxs-lookup"><span data-stu-id="d93ac-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="d93ac-162">Em **definições**, escolha **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d93ac-162">Under **Settings**, choose **Properties**.</span></span>

    ![Selecione toomove de conta de integração.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="d93ac-165">Alterar o grupo de recursos de Olá ou de subscrição do Azure associado à sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="d93ac-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Escolha o grupo de recursos de alteração ou de subscrição de alteração](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="d93ac-167">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="d93ac-167">Next Steps</span></span>
* [<span data-ttu-id="d93ac-168">Saiba mais sobre contratos</span><span class="sxs-lookup"><span data-stu-id="d93ac-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre contratos de integração do enterprise")  

