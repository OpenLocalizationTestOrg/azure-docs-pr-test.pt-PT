---
title: "aaaCustom esquemas de controlo para B2B monitorização - Azure Logic Apps | Microsoft Docs"
description: "Crie controlo personalizado esquemas toomonitor B2B mensagens de transações na sua conta de integração do Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="83c1d-103">Ativar toomonitor de controlo de fluxo de trabalho completado, ponto a ponto</span><span class="sxs-lookup"><span data-stu-id="83c1d-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="83c1d-104">Não há incorporadas que pode ativar para diferentes partes da sua empresa-empresa de fluxo de trabalho, tais como controlo AS2 ou X12 mensagens de controlo.</span><span class="sxs-lookup"><span data-stu-id="83c1d-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="83c1d-105">Quando criar fluxos de trabalho que inclui uma aplicação lógica, BizTalk Server, SQL Server ou qualquer outra camada, em seguida, pode ativar o controlo personalizado que regista eventos a partir da extremidade de toohello Olá início do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="83c1d-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="83c1d-106">Este tópico fornece código personalizado que pode utilizar camadas de Olá fora da sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="83c1d-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="83c1d-107">Esquema de controlo personalizado</span><span class="sxs-lookup"><span data-stu-id="83c1d-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="83c1d-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="83c1d-108">Property</span></span> | <span data-ttu-id="83c1d-109">Tipo</span><span class="sxs-lookup"><span data-stu-id="83c1d-109">Type</span></span> | <span data-ttu-id="83c1d-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="83c1d-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83c1d-111">SourceType</span><span class="sxs-lookup"><span data-stu-id="83c1d-111">sourceType</span></span> |   | <span data-ttu-id="83c1d-112">Tipo de origem Olá executar.</span><span class="sxs-lookup"><span data-stu-id="83c1d-112">Type of hello run source.</span></span> <span data-ttu-id="83c1d-113">Valores permitidos são **Microsoft.Logic/workflows** e **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="83c1d-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="83c1d-114">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-114">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-115">Origem</span><span class="sxs-lookup"><span data-stu-id="83c1d-115">Source</span></span> |   | <span data-ttu-id="83c1d-116">Se for de tipo de origem Olá **Microsoft.Logic/workflows**, precisam de informações da origem Olá toofollow neste esquema.</span><span class="sxs-lookup"><span data-stu-id="83c1d-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="83c1d-117">Se for de tipo de origem Olá **personalizado**, esquema de Olá é um JToken.</span><span class="sxs-lookup"><span data-stu-id="83c1d-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="83c1d-118">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-118">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-119">systemId</span><span class="sxs-lookup"><span data-stu-id="83c1d-119">systemId</span></span> | <span data-ttu-id="83c1d-120">Cadeia</span><span class="sxs-lookup"><span data-stu-id="83c1d-120">String</span></span> | <span data-ttu-id="83c1d-121">ID de sistema da aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="83c1d-121">Logic app system ID.</span></span> <span data-ttu-id="83c1d-122">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-122">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-123">runId</span><span class="sxs-lookup"><span data-stu-id="83c1d-123">runId</span></span> | <span data-ttu-id="83c1d-124">Cadeia</span><span class="sxs-lookup"><span data-stu-id="83c1d-124">String</span></span> | <span data-ttu-id="83c1d-125">Aplicação de lógica executar ID.</span><span class="sxs-lookup"><span data-stu-id="83c1d-125">Logic app run ID.</span></span> <span data-ttu-id="83c1d-126">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-126">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-127">operationName</span><span class="sxs-lookup"><span data-stu-id="83c1d-127">operationName</span></span> | <span data-ttu-id="83c1d-128">Cadeia</span><span class="sxs-lookup"><span data-stu-id="83c1d-128">String</span></span> | <span data-ttu-id="83c1d-129">Nome da operação de Olá (por exemplo, ação ou acionador).</span><span class="sxs-lookup"><span data-stu-id="83c1d-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="83c1d-130">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-130">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="83c1d-131">repeatItemScopeName</span></span> | <span data-ttu-id="83c1d-132">Cadeia</span><span class="sxs-lookup"><span data-stu-id="83c1d-132">String</span></span> | <span data-ttu-id="83c1d-133">Repita o nome do item se ação Olá está dentro de um `foreach` / `until` ciclo.</span><span class="sxs-lookup"><span data-stu-id="83c1d-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="83c1d-134">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-134">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="83c1d-135">repeatItemIndex</span></span> | <span data-ttu-id="83c1d-136">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="83c1d-136">Integer</span></span> | <span data-ttu-id="83c1d-137">Se a ação de Olá está dentro de um `foreach` / `until` ciclo.</span><span class="sxs-lookup"><span data-stu-id="83c1d-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="83c1d-138">Indica o índice de itens repetido de Olá.</span><span class="sxs-lookup"><span data-stu-id="83c1d-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="83c1d-139">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-139">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="83c1d-140">trackingId</span></span> | <span data-ttu-id="83c1d-141">Cadeia</span><span class="sxs-lookup"><span data-stu-id="83c1d-141">String</span></span> | <span data-ttu-id="83c1d-142">ID de controlo, mensagens hello do toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="83c1d-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="83c1d-143">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="83c1d-143">(Optional)</span></span> |
| <span data-ttu-id="83c1d-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="83c1d-144">correlationId</span></span> | <span data-ttu-id="83c1d-145">Cadeia</span><span class="sxs-lookup"><span data-stu-id="83c1d-145">String</span></span> | <span data-ttu-id="83c1d-146">ID de correlação, mensagens hello do toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="83c1d-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="83c1d-147">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="83c1d-147">(Optional)</span></span> |
| <span data-ttu-id="83c1d-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="83c1d-148">clientRequestId</span></span> | <span data-ttu-id="83c1d-149">Cadeia</span><span class="sxs-lookup"><span data-stu-id="83c1d-149">String</span></span> | <span data-ttu-id="83c1d-150">Cliente pode preenchê-lo toocorrelate mensagens.</span><span class="sxs-lookup"><span data-stu-id="83c1d-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="83c1d-151">(Opcional)</span><span class="sxs-lookup"><span data-stu-id="83c1d-151">(Optional)</span></span> |
| <span data-ttu-id="83c1d-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="83c1d-152">eventLevel</span></span> |   | <span data-ttu-id="83c1d-153">Nível de evento Olá.</span><span class="sxs-lookup"><span data-stu-id="83c1d-153">Level of hello event.</span></span> <span data-ttu-id="83c1d-154">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-154">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="83c1d-155">eventTime</span></span> |   | <span data-ttu-id="83c1d-156">Hora do evento de Olá, em formato UTC aaaa-MM-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="83c1d-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="83c1d-157">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-157">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-158">recordType</span><span class="sxs-lookup"><span data-stu-id="83c1d-158">recordType</span></span> |   | <span data-ttu-id="83c1d-159">Tipo de registo de controlar Olá.</span><span class="sxs-lookup"><span data-stu-id="83c1d-159">Type of hello track record.</span></span> <span data-ttu-id="83c1d-160">Permitido é de valor **personalizado**.</span><span class="sxs-lookup"><span data-stu-id="83c1d-160">Allowed value is **custom**.</span></span> <span data-ttu-id="83c1d-161">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-161">(Mandatory)</span></span> |
| <span data-ttu-id="83c1d-162">registo</span><span class="sxs-lookup"><span data-stu-id="83c1d-162">record</span></span> |   | <span data-ttu-id="83c1d-163">Tipo de registo personalizado.</span><span class="sxs-lookup"><span data-stu-id="83c1d-163">Custom record type.</span></span> <span data-ttu-id="83c1d-164">O formato permitido é JToken.</span><span class="sxs-lookup"><span data-stu-id="83c1d-164">Allowed format is JToken.</span></span> <span data-ttu-id="83c1d-165">(Obrigatório)</span><span class="sxs-lookup"><span data-stu-id="83c1d-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="83c1d-166">Esquemas de controlo de protocolo de B2B</span><span class="sxs-lookup"><span data-stu-id="83c1d-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="83c1d-167">Para obter informações sobre o protocolo de B2B esquemas de controlo, consulte:</span><span class="sxs-lookup"><span data-stu-id="83c1d-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="83c1d-168">Esquemas de controlo de AS2</span><span class="sxs-lookup"><span data-stu-id="83c1d-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="83c1d-169">Esquemas de controlo de X12</span><span class="sxs-lookup"><span data-stu-id="83c1d-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="83c1d-170">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="83c1d-170">Next steps</span></span>
* <span data-ttu-id="83c1d-171">Saiba mais sobre [monitorização mensagens B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="83c1d-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="83c1d-172">Saiba mais sobre [controlo mensagens B2B no portal de Operations Management Suite Olá](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="83c1d-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="83c1d-173">Saiba mais sobre Olá [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="83c1d-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
