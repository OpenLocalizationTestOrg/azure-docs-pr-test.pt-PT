---
title: "Exemplos de aaaQuery de padrões de utilização comuns no Stream Analytics | Microsoft Docs"
description: "Padrões de consulta comuns do Azure Stream Analytics"
keywords: Exemplos de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="54fbc-104">Exemplos de padrões de utilização comuns do Stream Analytics de consulta</span><span class="sxs-lookup"><span data-stu-id="54fbc-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="54fbc-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="54fbc-105">Introduction</span></span>
<span data-ttu-id="54fbc-106">As consultas no Azure Stream Analytics são expressas num idioma de consulta como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="54fbc-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="54fbc-107">Estas consultas estão documentadas na Olá [referência de linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) guia.</span><span class="sxs-lookup"><span data-stu-id="54fbc-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="54fbc-108">Este artigo destaca soluções tooseveral padrões de consulta comuns, com base nos cenários no mundo real.</span><span class="sxs-lookup"><span data-stu-id="54fbc-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="54fbc-109">Este é um trabalho em curso e continua toobe atualizada com novos padrões numa base contínua.</span><span class="sxs-lookup"><span data-stu-id="54fbc-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="54fbc-110">Exemplo de consulta: converter os tipos de dados</span><span class="sxs-lookup"><span data-stu-id="54fbc-110">Query example: Convert data types</span></span>
<span data-ttu-id="54fbc-111">**Descrição**: definir os tipos de Olá das propriedades no fluxo de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="54fbc-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="54fbc-112">Por exemplo, o peso de carro Olá futuras no fluxo de entrada Olá como cadeias e tem de toobe convertido demasiado**INT** tooperform **soma** -cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="54fbc-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="54fbc-113">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-113">**Input**:</span></span>

| <span data-ttu-id="54fbc-114">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-114">Make</span></span> | <span data-ttu-id="54fbc-115">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-115">Time</span></span> | <span data-ttu-id="54fbc-116">Peso</span><span class="sxs-lookup"><span data-stu-id="54fbc-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-117">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-117">Honda</span></span> |<span data-ttu-id="54fbc-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="54fbc-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="54fbc-119">"1000"</span></span> |
| <span data-ttu-id="54fbc-120">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-120">Honda</span></span> |<span data-ttu-id="54fbc-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="54fbc-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="54fbc-122">"2000"</span></span> |

<span data-ttu-id="54fbc-123">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-123">**Output**:</span></span>

| <span data-ttu-id="54fbc-124">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-124">Make</span></span> | <span data-ttu-id="54fbc-125">Peso</span><span class="sxs-lookup"><span data-stu-id="54fbc-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-126">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-126">Honda</span></span> |<span data-ttu-id="54fbc-127">3000</span><span class="sxs-lookup"><span data-stu-id="54fbc-127">3000</span></span> |

<span data-ttu-id="54fbc-128">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="54fbc-129">**EXPLICAÇÃO**: Utilize um **CAST** instrução no Olá **ponderação** campo toospecify respetivo tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="54fbc-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="54fbc-130">Ver lista de Olá dos tipos de dados suportados no [tipos de dados (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="54fbc-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="54fbc-131">Exemplo de consulta: Utilize como/não, como a correspondência de padrões toodo</span><span class="sxs-lookup"><span data-stu-id="54fbc-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="54fbc-132">**Descrição**: verificar se um valor de campo em eventos de Olá corresponde a um determinado padrão.</span><span class="sxs-lookup"><span data-stu-id="54fbc-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="54fbc-133">Por exemplo, verifique que o resultado de Olá devolve plates de licença que começam com um e terminar com 9.</span><span class="sxs-lookup"><span data-stu-id="54fbc-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="54fbc-134">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-134">**Input**:</span></span>

| <span data-ttu-id="54fbc-135">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-135">Make</span></span> | <span data-ttu-id="54fbc-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-136">LicensePlate</span></span> | <span data-ttu-id="54fbc-137">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-138">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-138">Honda</span></span> |<span data-ttu-id="54fbc-139">ABC 123</span><span class="sxs-lookup"><span data-stu-id="54fbc-139">ABC-123</span></span> |<span data-ttu-id="54fbc-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-141">Toyota</span></span> |<span data-ttu-id="54fbc-142">AAA 999</span><span class="sxs-lookup"><span data-stu-id="54fbc-142">AAA-999</span></span> |<span data-ttu-id="54fbc-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="54fbc-144">Nissan</span></span> |<span data-ttu-id="54fbc-145">ABC 369</span><span class="sxs-lookup"><span data-stu-id="54fbc-145">ABC-369</span></span> |<span data-ttu-id="54fbc-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="54fbc-147">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-147">**Output**:</span></span>

| <span data-ttu-id="54fbc-148">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-148">Make</span></span> | <span data-ttu-id="54fbc-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-149">LicensePlate</span></span> | <span data-ttu-id="54fbc-150">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-151">Toyota</span></span> |<span data-ttu-id="54fbc-152">AAA 999</span><span class="sxs-lookup"><span data-stu-id="54fbc-152">AAA-999</span></span> |<span data-ttu-id="54fbc-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="54fbc-154">Nissan</span></span> |<span data-ttu-id="54fbc-155">ABC 369</span><span class="sxs-lookup"><span data-stu-id="54fbc-155">ABC-369</span></span> |<span data-ttu-id="54fbc-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="54fbc-157">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="54fbc-158">**EXPLICAÇÃO**: Olá utilize **como** Olá toocheck de instrução **LicensePlate** campo valor.</span><span class="sxs-lookup"><span data-stu-id="54fbc-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="54fbc-159">Deve começar com um um, em seguida, ter qualquer cadeia de zero ou mais carateres e, em seguida, terminar com um 9.</span><span class="sxs-lookup"><span data-stu-id="54fbc-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="54fbc-160">Exemplo de consulta: especificar lógica para casos/valores diferentes (instruções maiúsculas)</span><span class="sxs-lookup"><span data-stu-id="54fbc-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="54fbc-161">**Descrição**: forneça um cálculo diferente de um campo, com base num critério específico.</span><span class="sxs-lookup"><span data-stu-id="54fbc-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="54fbc-162">Por exemplo, indique uma descrição de cadeia para automóveis quantos de Olá, mesmo se passaram, com um caso especial para 1.</span><span class="sxs-lookup"><span data-stu-id="54fbc-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="54fbc-163">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-163">**Input**:</span></span>

| <span data-ttu-id="54fbc-164">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-164">Make</span></span> | <span data-ttu-id="54fbc-165">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-166">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-166">Honda</span></span> |<span data-ttu-id="54fbc-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-168">Toyota</span></span> |<span data-ttu-id="54fbc-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-170">Toyota</span></span> |<span data-ttu-id="54fbc-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="54fbc-172">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-172">**Output**:</span></span>

| <span data-ttu-id="54fbc-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="54fbc-173">CarsPassed</span></span> | <span data-ttu-id="54fbc-174">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-175">1 Honda</span></span> |<span data-ttu-id="54fbc-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="54fbc-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="54fbc-177">2 Toyotas</span></span> |<span data-ttu-id="54fbc-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="54fbc-179">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="54fbc-180">**EXPLICAÇÃO**: Olá **caso** cláusula nos permite tooprovide cálculo diferentes, com base em algumas critérios (no nosso caso, a contagem de Olá de automóveis Olá na janela de agregação Olá).</span><span class="sxs-lookup"><span data-stu-id="54fbc-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="54fbc-181">Exemplo de consulta: enviar dados toomultiple produz</span><span class="sxs-lookup"><span data-stu-id="54fbc-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="54fbc-182">**Descrição**: enviar dados toomultiple saída destinos de uma única tarefa.</span><span class="sxs-lookup"><span data-stu-id="54fbc-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="54fbc-183">Por exemplo, analisar os dados para um alerta baseadas em limiares e todo o armazenamento tooblob eventos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="54fbc-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="54fbc-184">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-184">**Input**:</span></span>

| <span data-ttu-id="54fbc-185">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-185">Make</span></span> | <span data-ttu-id="54fbc-186">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-187">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-187">Honda</span></span> |<span data-ttu-id="54fbc-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-189">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-189">Honda</span></span> |<span data-ttu-id="54fbc-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-191">Toyota</span></span> |<span data-ttu-id="54fbc-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-193">Toyota</span></span> |<span data-ttu-id="54fbc-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-195">Toyota</span></span> |<span data-ttu-id="54fbc-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="54fbc-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-197">**Output1**:</span></span>

| <span data-ttu-id="54fbc-198">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-198">Make</span></span> | <span data-ttu-id="54fbc-199">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-200">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-200">Honda</span></span> |<span data-ttu-id="54fbc-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-202">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-202">Honda</span></span> |<span data-ttu-id="54fbc-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-204">Toyota</span></span> |<span data-ttu-id="54fbc-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-206">Toyota</span></span> |<span data-ttu-id="54fbc-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-208">Toyota</span></span> |<span data-ttu-id="54fbc-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="54fbc-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-210">**Output2**:</span></span>

| <span data-ttu-id="54fbc-211">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-211">Make</span></span> | <span data-ttu-id="54fbc-212">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-212">Time</span></span> | <span data-ttu-id="54fbc-213">Contagem</span><span class="sxs-lookup"><span data-stu-id="54fbc-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-214">Toyota</span></span> |<span data-ttu-id="54fbc-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="54fbc-216">3</span><span class="sxs-lookup"><span data-stu-id="54fbc-216">3</span></span> |

<span data-ttu-id="54fbc-217">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="54fbc-218">**EXPLICAÇÃO**: Olá **INTO** cláusula indica Stream Analytics que Olá produz toowrite Olá dados toofrom esta instrução.</span><span class="sxs-lookup"><span data-stu-id="54fbc-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="54fbc-219">consulta primeiro Olá é um pass-through de dados de Olá recebemos tooan saída que são denominados **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="54fbc-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="54fbc-220">consulta segundo Olá efetua algumas agregação simple e filtragem e envia resultados Olá tooa sistema de alerta a jusante.</span><span class="sxs-lookup"><span data-stu-id="54fbc-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="54fbc-221">Tenha em atenção que também pode reutilizar resultados Olá de expressões de tabela comuns (ctes recursivos) do Olá (tais como **WITH** instruções) em várias instruções de saída.</span><span class="sxs-lookup"><span data-stu-id="54fbc-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="54fbc-222">Esta opção tem Olá benefício adicional de abrir a origem de entrada menos leitores toohello.</span><span class="sxs-lookup"><span data-stu-id="54fbc-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="54fbc-223">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="54fbc-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="54fbc-224">Exemplo de consulta: contagem de valores exclusivos</span><span class="sxs-lookup"><span data-stu-id="54fbc-224">Query example: Count unique values</span></span>
<span data-ttu-id="54fbc-225">**Descrição**: Olá número exclusivo de valores de campos que são apresentados no fluxo de Olá dentro de uma janela de tempo da contagem.</span><span class="sxs-lookup"><span data-stu-id="54fbc-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="54fbc-226">Por exemplo, quantas exclusivo faz com que o de automóveis passadas booth de utilização de Olá numa janela segundo 2?</span><span class="sxs-lookup"><span data-stu-id="54fbc-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="54fbc-227">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-227">**Input**:</span></span>

| <span data-ttu-id="54fbc-228">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-228">Make</span></span> | <span data-ttu-id="54fbc-229">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-230">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-230">Honda</span></span> |<span data-ttu-id="54fbc-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-232">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-232">Honda</span></span> |<span data-ttu-id="54fbc-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-234">Toyota</span></span> |<span data-ttu-id="54fbc-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-236">Toyota</span></span> |<span data-ttu-id="54fbc-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-238">Toyota</span></span> |<span data-ttu-id="54fbc-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="54fbc-240">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="54fbc-240">**Output:**</span></span>

| <span data-ttu-id="54fbc-241">Contagem</span><span class="sxs-lookup"><span data-stu-id="54fbc-241">Count</span></span> | <span data-ttu-id="54fbc-242">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-243">2</span><span class="sxs-lookup"><span data-stu-id="54fbc-243">2</span></span> |<span data-ttu-id="54fbc-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="54fbc-245">1</span><span class="sxs-lookup"><span data-stu-id="54fbc-245">1</span></span> |<span data-ttu-id="54fbc-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="54fbc-247">**Solução:**</span><span class="sxs-lookup"><span data-stu-id="54fbc-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="54fbc-248">**Explicação:**
**CONTAGEM (tornar distintos)** devolve Olá número de valores distintos numa Olá **tornar** coluna dentro de uma janela de tempo.</span><span class="sxs-lookup"><span data-stu-id="54fbc-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="54fbc-249">Exemplo de consulta: determinar se um valor foi alterada</span><span class="sxs-lookup"><span data-stu-id="54fbc-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="54fbc-250">**Descrição**: observar um toodetermine valor anterior, se for diferente do valor atual de Olá.</span><span class="sxs-lookup"><span data-stu-id="54fbc-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="54fbc-251">Por exemplo, é carro anterior Olá no Olá de viagem de utilização de Olá que mesmo tornar mais carro atual Olá?</span><span class="sxs-lookup"><span data-stu-id="54fbc-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="54fbc-252">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-252">**Input**:</span></span>

| <span data-ttu-id="54fbc-253">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-253">Make</span></span> | <span data-ttu-id="54fbc-254">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-255">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-255">Honda</span></span> |<span data-ttu-id="54fbc-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-257">Toyota</span></span> |<span data-ttu-id="54fbc-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="54fbc-259">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-259">**Output**:</span></span>

| <span data-ttu-id="54fbc-260">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-260">Make</span></span> | <span data-ttu-id="54fbc-261">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-262">Toyota</span></span> |<span data-ttu-id="54fbc-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="54fbc-264">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="54fbc-265">**EXPLICAÇÃO**: Utilize **desfasamento** toopeek para Olá fluxo um evento volta de entrada e obter Olá **tornar** valor.</span><span class="sxs-lookup"><span data-stu-id="54fbc-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="54fbc-266">Em seguida, compare toohello **tornar** valor num evento Olá de saída e de evento atual de Olá se forem diferentes.</span><span class="sxs-lookup"><span data-stu-id="54fbc-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="54fbc-267">Exemplo de consulta: o primeiro evento a localizar Olá numa janela</span><span class="sxs-lookup"><span data-stu-id="54fbc-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="54fbc-268">**Descrição**: localizar carro primeiro de Olá em cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="54fbc-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="54fbc-269">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-269">**Input**:</span></span>

| <span data-ttu-id="54fbc-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-270">LicensePlate</span></span> | <span data-ttu-id="54fbc-271">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-271">Make</span></span> | <span data-ttu-id="54fbc-272">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="54fbc-273">DXE 5291</span></span> |<span data-ttu-id="54fbc-274">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-274">Honda</span></span> |<span data-ttu-id="54fbc-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="54fbc-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="54fbc-276">YZK 5704</span></span> |<span data-ttu-id="54fbc-277">Ford</span><span class="sxs-lookup"><span data-stu-id="54fbc-277">Ford</span></span> |<span data-ttu-id="54fbc-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="54fbc-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="54fbc-279">RMV 8282</span></span> |<span data-ttu-id="54fbc-280">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-280">Honda</span></span> |<span data-ttu-id="54fbc-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="54fbc-282">YHN 6970</span></span> |<span data-ttu-id="54fbc-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-283">Toyota</span></span> |<span data-ttu-id="54fbc-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="54fbc-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="54fbc-285">VFE 1616</span></span> |<span data-ttu-id="54fbc-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-286">Toyota</span></span> |<span data-ttu-id="54fbc-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="54fbc-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="54fbc-288">QYF 9358</span></span> |<span data-ttu-id="54fbc-289">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-289">Honda</span></span> |<span data-ttu-id="54fbc-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="54fbc-291">MDR 6128</span></span> |<span data-ttu-id="54fbc-292">BMW</span><span class="sxs-lookup"><span data-stu-id="54fbc-292">BMW</span></span> |<span data-ttu-id="54fbc-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="54fbc-294">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-294">**Output**:</span></span>

| <span data-ttu-id="54fbc-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-295">LicensePlate</span></span> | <span data-ttu-id="54fbc-296">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-296">Make</span></span> | <span data-ttu-id="54fbc-297">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="54fbc-298">DXE 5291</span></span> |<span data-ttu-id="54fbc-299">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-299">Honda</span></span> |<span data-ttu-id="54fbc-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="54fbc-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="54fbc-301">QYF 9358</span></span> |<span data-ttu-id="54fbc-302">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-302">Honda</span></span> |<span data-ttu-id="54fbc-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="54fbc-304">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="54fbc-305">Agora vamos alterar Olá problema e localizar Olá primeiro carro de uma determinada efetuar em cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="54fbc-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="54fbc-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-306">LicensePlate</span></span> | <span data-ttu-id="54fbc-307">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-307">Make</span></span> | <span data-ttu-id="54fbc-308">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="54fbc-309">DXE 5291</span></span> |<span data-ttu-id="54fbc-310">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-310">Honda</span></span> |<span data-ttu-id="54fbc-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="54fbc-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="54fbc-312">YZK 5704</span></span> |<span data-ttu-id="54fbc-313">Ford</span><span class="sxs-lookup"><span data-stu-id="54fbc-313">Ford</span></span> |<span data-ttu-id="54fbc-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="54fbc-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="54fbc-315">YHN 6970</span></span> |<span data-ttu-id="54fbc-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-316">Toyota</span></span> |<span data-ttu-id="54fbc-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="54fbc-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="54fbc-318">QYF 9358</span></span> |<span data-ttu-id="54fbc-319">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-319">Honda</span></span> |<span data-ttu-id="54fbc-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="54fbc-321">MDR 6128</span></span> |<span data-ttu-id="54fbc-322">BMW</span><span class="sxs-lookup"><span data-stu-id="54fbc-322">BMW</span></span> |<span data-ttu-id="54fbc-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="54fbc-324">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="54fbc-325">Exemplo de consulta: último evento de localizar Olá numa janela</span><span class="sxs-lookup"><span data-stu-id="54fbc-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="54fbc-326">**Descrição**: carro de último Olá localizar em cada intervalo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="54fbc-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="54fbc-327">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-327">**Input**:</span></span>

| <span data-ttu-id="54fbc-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-328">LicensePlate</span></span> | <span data-ttu-id="54fbc-329">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-329">Make</span></span> | <span data-ttu-id="54fbc-330">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="54fbc-331">DXE 5291</span></span> |<span data-ttu-id="54fbc-332">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-332">Honda</span></span> |<span data-ttu-id="54fbc-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="54fbc-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="54fbc-334">YZK 5704</span></span> |<span data-ttu-id="54fbc-335">Ford</span><span class="sxs-lookup"><span data-stu-id="54fbc-335">Ford</span></span> |<span data-ttu-id="54fbc-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="54fbc-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="54fbc-337">RMV 8282</span></span> |<span data-ttu-id="54fbc-338">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-338">Honda</span></span> |<span data-ttu-id="54fbc-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="54fbc-340">YHN 6970</span></span> |<span data-ttu-id="54fbc-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-341">Toyota</span></span> |<span data-ttu-id="54fbc-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="54fbc-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="54fbc-343">VFE 1616</span></span> |<span data-ttu-id="54fbc-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-344">Toyota</span></span> |<span data-ttu-id="54fbc-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="54fbc-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="54fbc-346">QYF 9358</span></span> |<span data-ttu-id="54fbc-347">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-347">Honda</span></span> |<span data-ttu-id="54fbc-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="54fbc-349">MDR 6128</span></span> |<span data-ttu-id="54fbc-350">BMW</span><span class="sxs-lookup"><span data-stu-id="54fbc-350">BMW</span></span> |<span data-ttu-id="54fbc-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="54fbc-352">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-352">**Output**:</span></span>

| <span data-ttu-id="54fbc-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-353">LicensePlate</span></span> | <span data-ttu-id="54fbc-354">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-354">Make</span></span> | <span data-ttu-id="54fbc-355">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="54fbc-356">VFE 1616</span></span> |<span data-ttu-id="54fbc-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-357">Toyota</span></span> |<span data-ttu-id="54fbc-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="54fbc-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="54fbc-359">MDR 6128</span></span> |<span data-ttu-id="54fbc-360">BMW</span><span class="sxs-lookup"><span data-stu-id="54fbc-360">BMW</span></span> |<span data-ttu-id="54fbc-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="54fbc-362">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="54fbc-363">**EXPLICAÇÃO**: Existem dois passos numa consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="54fbc-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="54fbc-364">Olá primeiro encontra um Olá mais recente carimbo de hora do windows 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="54fbc-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="54fbc-365">associações de passo segundo Olá Olá resultados de consulta de primeiro Olá com Olá original fluxo toofind Olá eventos que correspondem ao hello último tempo carimbos de cada janela.</span><span class="sxs-lookup"><span data-stu-id="54fbc-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="54fbc-366">Exemplo de consulta: detetar ausência de Olá de eventos</span><span class="sxs-lookup"><span data-stu-id="54fbc-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="54fbc-367">**Descrição**: verificar se uma sequência não tem um valor que corresponde a um determinado critério.</span><span class="sxs-lookup"><span data-stu-id="54fbc-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="54fbc-368">Por exemplo, 2 carros consecutivos de Olá, que mesmo se introduziu viagem de utilização de Olá dentro Olá últimos 90 segundos?</span><span class="sxs-lookup"><span data-stu-id="54fbc-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="54fbc-369">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-369">**Input**:</span></span>

| <span data-ttu-id="54fbc-370">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-370">Make</span></span> | <span data-ttu-id="54fbc-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-371">LicensePlate</span></span> | <span data-ttu-id="54fbc-372">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-373">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-373">Honda</span></span> |<span data-ttu-id="54fbc-374">ABC 123</span><span class="sxs-lookup"><span data-stu-id="54fbc-374">ABC-123</span></span> |<span data-ttu-id="54fbc-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="54fbc-376">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-376">Honda</span></span> |<span data-ttu-id="54fbc-377">AAA 999</span><span class="sxs-lookup"><span data-stu-id="54fbc-377">AAA-999</span></span> |<span data-ttu-id="54fbc-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="54fbc-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-379">Toyota</span></span> |<span data-ttu-id="54fbc-380">DEF 987</span><span class="sxs-lookup"><span data-stu-id="54fbc-380">DEF-987</span></span> |<span data-ttu-id="54fbc-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="54fbc-382">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-382">Honda</span></span> |<span data-ttu-id="54fbc-383">GHI 345</span><span class="sxs-lookup"><span data-stu-id="54fbc-383">GHI-345</span></span> |<span data-ttu-id="54fbc-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="54fbc-385">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-385">**Output**:</span></span>

| <span data-ttu-id="54fbc-386">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-386">Make</span></span> | <span data-ttu-id="54fbc-387">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-387">Time</span></span> | <span data-ttu-id="54fbc-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="54fbc-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="54fbc-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="54fbc-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="54fbc-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="54fbc-391">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-391">Honda</span></span> |<span data-ttu-id="54fbc-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="54fbc-393">AAA 999</span><span class="sxs-lookup"><span data-stu-id="54fbc-393">AAA-999</span></span> |<span data-ttu-id="54fbc-394">ABC 123</span><span class="sxs-lookup"><span data-stu-id="54fbc-394">ABC-123</span></span> |<span data-ttu-id="54fbc-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="54fbc-396">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="54fbc-397">**EXPLICAÇÃO**: Utilize **desfasamento** toopeek para Olá fluxo um evento volta de entrada e obter Olá **tornar** valor.</span><span class="sxs-lookup"><span data-stu-id="54fbc-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="54fbc-398">Compare-toohello **tornar** valor Olá atual de eventos e, em seguida, eventos de Olá de saída se estes estão Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="54fbc-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="54fbc-399">Também pode utilizar **desfasamento** tooget dados sobre carro anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="54fbc-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="54fbc-400">Exemplo de consulta: detetar duração Olá entre eventos</span><span class="sxs-lookup"><span data-stu-id="54fbc-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="54fbc-401">**Descrição**: localizar duração Olá de um evento específico.</span><span class="sxs-lookup"><span data-stu-id="54fbc-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="54fbc-402">Por exemplo, tendo em conta um clickstream da web, determine o tempo de Olá gasto numa funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="54fbc-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="54fbc-403">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-403">**Input**:</span></span>  

| <span data-ttu-id="54fbc-404">Utilizador</span><span class="sxs-lookup"><span data-stu-id="54fbc-404">User</span></span> | <span data-ttu-id="54fbc-405">Funcionalidade</span><span class="sxs-lookup"><span data-stu-id="54fbc-405">Feature</span></span> | <span data-ttu-id="54fbc-406">Evento</span><span class="sxs-lookup"><span data-stu-id="54fbc-406">Event</span></span> | <span data-ttu-id="54fbc-407">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="54fbc-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="54fbc-408">RightMenu</span></span> |<span data-ttu-id="54fbc-409">Iniciar</span><span class="sxs-lookup"><span data-stu-id="54fbc-409">Start</span></span> |<span data-ttu-id="54fbc-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="54fbc-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="54fbc-411">RightMenu</span></span> |<span data-ttu-id="54fbc-412">Fim</span><span class="sxs-lookup"><span data-stu-id="54fbc-412">End</span></span> |<span data-ttu-id="54fbc-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="54fbc-414">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-414">**Output**:</span></span>  

| <span data-ttu-id="54fbc-415">Utilizador</span><span class="sxs-lookup"><span data-stu-id="54fbc-415">User</span></span> | <span data-ttu-id="54fbc-416">Funcionalidade</span><span class="sxs-lookup"><span data-stu-id="54fbc-416">Feature</span></span> | <span data-ttu-id="54fbc-417">Duração</span><span class="sxs-lookup"><span data-stu-id="54fbc-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="54fbc-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="54fbc-418">RightMenu</span></span> |<span data-ttu-id="54fbc-419">7</span><span class="sxs-lookup"><span data-stu-id="54fbc-419">7</span></span> |

<span data-ttu-id="54fbc-420">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="54fbc-421">**EXPLICAÇÃO**: Olá utilize **último** funcionar tooretrieve Olá pela última vez **tempo** valor quando o tipo de evento Olá foi **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="54fbc-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="54fbc-422">Olá **último** funcionar utiliza **PARTITION BY [user]** tooindicate Olá resultado é calculada por utilizador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="54fbc-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="54fbc-423">consulta de Olá tem um limiar máximo de 1 hora de diferença de tempo de Olá entre **iniciar** e **parar** eventos, mas é configurável conforme necessário **(limite DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="54fbc-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="54fbc-424">Exemplo de consulta: detetar duração Olá de uma condição</span><span class="sxs-lookup"><span data-stu-id="54fbc-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="54fbc-425">**Descrição**: localizar fora quanto Ocorreu uma condição.</span><span class="sxs-lookup"><span data-stu-id="54fbc-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="54fbc-426">Por exemplo, suponha que um erro resultou em todos os carros ter uma ponderação incorreta (acima pounds 20.000).</span><span class="sxs-lookup"><span data-stu-id="54fbc-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="54fbc-427">Queremos toocompute duração Olá erros Olá.</span><span class="sxs-lookup"><span data-stu-id="54fbc-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="54fbc-428">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-428">**Input**:</span></span>

| <span data-ttu-id="54fbc-429">Certifique-</span><span class="sxs-lookup"><span data-stu-id="54fbc-429">Make</span></span> | <span data-ttu-id="54fbc-430">Hora</span><span class="sxs-lookup"><span data-stu-id="54fbc-430">Time</span></span> | <span data-ttu-id="54fbc-431">Peso</span><span class="sxs-lookup"><span data-stu-id="54fbc-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-432">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-432">Honda</span></span> |<span data-ttu-id="54fbc-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="54fbc-434">2000</span><span class="sxs-lookup"><span data-stu-id="54fbc-434">2000</span></span> |
| <span data-ttu-id="54fbc-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-435">Toyota</span></span> |<span data-ttu-id="54fbc-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="54fbc-437">25000</span><span class="sxs-lookup"><span data-stu-id="54fbc-437">25000</span></span> |
| <span data-ttu-id="54fbc-438">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-438">Honda</span></span> |<span data-ttu-id="54fbc-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="54fbc-440">26000</span><span class="sxs-lookup"><span data-stu-id="54fbc-440">26000</span></span> |
| <span data-ttu-id="54fbc-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-441">Toyota</span></span> |<span data-ttu-id="54fbc-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="54fbc-443">25000</span><span class="sxs-lookup"><span data-stu-id="54fbc-443">25000</span></span> |
| <span data-ttu-id="54fbc-444">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-444">Honda</span></span> |<span data-ttu-id="54fbc-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="54fbc-446">26000</span><span class="sxs-lookup"><span data-stu-id="54fbc-446">26000</span></span> |
| <span data-ttu-id="54fbc-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-447">Toyota</span></span> |<span data-ttu-id="54fbc-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="54fbc-449">25000</span><span class="sxs-lookup"><span data-stu-id="54fbc-449">25000</span></span> |
| <span data-ttu-id="54fbc-450">Honda</span><span class="sxs-lookup"><span data-stu-id="54fbc-450">Honda</span></span> |<span data-ttu-id="54fbc-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="54fbc-452">26000</span><span class="sxs-lookup"><span data-stu-id="54fbc-452">26000</span></span> |
| <span data-ttu-id="54fbc-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="54fbc-453">Toyota</span></span> |<span data-ttu-id="54fbc-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="54fbc-455">2000</span><span class="sxs-lookup"><span data-stu-id="54fbc-455">2000</span></span> |

<span data-ttu-id="54fbc-456">**Saída**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-456">**Output**:</span></span>

| <span data-ttu-id="54fbc-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="54fbc-457">StartFault</span></span> | <span data-ttu-id="54fbc-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="54fbc-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="54fbc-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="54fbc-461">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="54fbc-462">**EXPLICAÇÃO**: Utilize **desfasamento** tooview Olá o fluxo de entrada para 24 horas e procure instâncias onde **StartFault** e **StopFault** são abrangido pelo Olá < 20000 de importância.</span><span class="sxs-lookup"><span data-stu-id="54fbc-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="54fbc-463">Exemplo de consulta: preencher os valores em falta</span><span class="sxs-lookup"><span data-stu-id="54fbc-463">Query example: Fill missing values</span></span>
<span data-ttu-id="54fbc-464">**Descrição**: para o fluxo de Olá dos eventos que têm valores em falta, produzir um fluxo de eventos com intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="54fbc-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="54fbc-465">Por exemplo, gere um evento a cada cinco segundos, que comunica o ponto de dados de Olá visto mais recentemente.</span><span class="sxs-lookup"><span data-stu-id="54fbc-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="54fbc-466">**Entrada**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-466">**Input**:</span></span>

| <span data-ttu-id="54fbc-467">T</span><span class="sxs-lookup"><span data-stu-id="54fbc-467">t</span></span> | <span data-ttu-id="54fbc-468">valor</span><span class="sxs-lookup"><span data-stu-id="54fbc-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="54fbc-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="54fbc-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="54fbc-470">1</span><span class="sxs-lookup"><span data-stu-id="54fbc-470">1</span></span> |
| <span data-ttu-id="54fbc-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="54fbc-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="54fbc-472">2</span><span class="sxs-lookup"><span data-stu-id="54fbc-472">2</span></span> |
| <span data-ttu-id="54fbc-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="54fbc-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="54fbc-474">3</span><span class="sxs-lookup"><span data-stu-id="54fbc-474">3</span></span> |
| <span data-ttu-id="54fbc-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="54fbc-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="54fbc-476">4</span><span class="sxs-lookup"><span data-stu-id="54fbc-476">4</span></span> |
| <span data-ttu-id="54fbc-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="54fbc-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="54fbc-478">5</span><span class="sxs-lookup"><span data-stu-id="54fbc-478">5</span></span> |
| <span data-ttu-id="54fbc-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="54fbc-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="54fbc-480">6</span><span class="sxs-lookup"><span data-stu-id="54fbc-480">6</span></span> |

<span data-ttu-id="54fbc-481">**Saída (primeiras 10 linhas)**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="54fbc-482">windowend</span><span class="sxs-lookup"><span data-stu-id="54fbc-482">windowend</span></span> | <span data-ttu-id="54fbc-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="54fbc-483">lastevent.t</span></span> | <span data-ttu-id="54fbc-484">lastevent.Value</span><span class="sxs-lookup"><span data-stu-id="54fbc-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54fbc-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="54fbc-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="54fbc-487">1</span><span class="sxs-lookup"><span data-stu-id="54fbc-487">1</span></span> |
| <span data-ttu-id="54fbc-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="54fbc-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="54fbc-490">2</span><span class="sxs-lookup"><span data-stu-id="54fbc-490">2</span></span> |
| <span data-ttu-id="54fbc-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="54fbc-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="54fbc-493">3</span><span class="sxs-lookup"><span data-stu-id="54fbc-493">3</span></span> |
| <span data-ttu-id="54fbc-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="54fbc-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="54fbc-496">4</span><span class="sxs-lookup"><span data-stu-id="54fbc-496">4</span></span> |
| <span data-ttu-id="54fbc-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="54fbc-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="54fbc-499">4</span><span class="sxs-lookup"><span data-stu-id="54fbc-499">4</span></span> |
| <span data-ttu-id="54fbc-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="54fbc-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="54fbc-502">4</span><span class="sxs-lookup"><span data-stu-id="54fbc-502">4</span></span> |
| <span data-ttu-id="54fbc-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="54fbc-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="54fbc-505">5</span><span class="sxs-lookup"><span data-stu-id="54fbc-505">5</span></span> |
| <span data-ttu-id="54fbc-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="54fbc-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="54fbc-508">6</span><span class="sxs-lookup"><span data-stu-id="54fbc-508">6</span></span> |
| <span data-ttu-id="54fbc-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="54fbc-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="54fbc-511">6</span><span class="sxs-lookup"><span data-stu-id="54fbc-511">6</span></span> |
| <span data-ttu-id="54fbc-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="54fbc-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="54fbc-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="54fbc-514">6</span><span class="sxs-lookup"><span data-stu-id="54fbc-514">6</span></span> |

<span data-ttu-id="54fbc-515">**Solução**:</span><span class="sxs-lookup"><span data-stu-id="54fbc-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="54fbc-516">**EXPLICAÇÃO**: esta consulta gera eventos a cada cinco segundos e saídas Olá último evento que foi recebido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="54fbc-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="54fbc-517">Olá [Hopping janela](https://msdn.microsoft.com/library/dn835041.aspx "Hopping janela – Azure Stream Analytics") duração determina até que ponto a consulta de back-Olá procura eventos mais recentes do toofind Olá (300 segundos neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="54fbc-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="54fbc-518">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="54fbc-518">Get help</span></span>
<span data-ttu-id="54fbc-519">Para obter mais assistência, experimente a nossa [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="54fbc-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54fbc-520">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="54fbc-520">Next steps</span></span>
* [<span data-ttu-id="54fbc-521">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54fbc-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="54fbc-522">Começar a utilizar o Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54fbc-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="54fbc-523">Tarefas de escala do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54fbc-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="54fbc-524">Referência do idioma de consulta do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54fbc-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="54fbc-525">Referência de API do REST de gestão do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="54fbc-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

