---
title: "Lista de aplicações B2B de lógica de erros e soluções: App Service do Azure | Microsoft Docs"
description: "Lista de aplicações B2B de lógica de erros e soluções"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="f0043-103">Lista de aplicações B2B de lógica de erros e soluções</span><span class="sxs-lookup"><span data-stu-id="f0043-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="f0043-104">Este artigo ajuda-o a resolver erros que poderão acontecer em Logic Apps B2B cenários e sugere as ações adequadas para corrigir os erros.</span><span class="sxs-lookup"><span data-stu-id="f0043-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="f0043-105">Resolução de contrato</span><span class="sxs-lookup"><span data-stu-id="f0043-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="f0043-106">* Qualquer contrato encontrado</span><span class="sxs-lookup"><span data-stu-id="f0043-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="f0043-107">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-107">Error description</span></span> | <span data-ttu-id="f0043-108">Nenhum contrato encontrado com parâmetros de resolução de contrato</span><span class="sxs-lookup"><span data-stu-id="f0043-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="f0043-109">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-109">User action</span></span> | <span data-ttu-id="f0043-110">contrato de Olá deve ser adicionado a conta de integração toohello com identidades de negócio definido.</span><span class="sxs-lookup"><span data-stu-id="f0043-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="f0043-111">identidades de negócio Olá devem corresponder ao ID de mensagem de entrada toohello</span><span class="sxs-lookup"><span data-stu-id="f0043-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="f0043-112">* Qualquer contrato encontrado com identidades</span><span class="sxs-lookup"><span data-stu-id="f0043-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="f0043-113">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-113">Error description</span></span> | <span data-ttu-id="f0043-114">Nenhum contrato encontrado com identidades: 'AS2Identity':: 'Partner1' e 'AS2Identity':: 'Partner3'</span><span class="sxs-lookup"><span data-stu-id="f0043-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="f0043-115">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-115">User action</span></span> | <span data-ttu-id="f0043-116">AS2 inválido-do ou AS2-tooconfigured contrato.</span><span class="sxs-lookup"><span data-stu-id="f0043-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="f0043-117">Mensagem de AS2 correta AS2-do ou cabeçalhos com configurações de contrato de mensagem de ids de toomatch AS2 AS2 tooheaders ou o contrato no AS2</span><span class="sxs-lookup"><span data-stu-id="f0043-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="f0043-118">AS2</span><span class="sxs-lookup"><span data-stu-id="f0043-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="f0043-119">* Cabeçalhos de mensagens AS2 em falta</span><span class="sxs-lookup"><span data-stu-id="f0043-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="f0043-120">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-120">Error description</span></span>| <span data-ttu-id="f0043-121">Cabeçalhos de AS2 inválidos.</span><span class="sxs-lookup"><span data-stu-id="f0043-121">Invalid AS2 headers.</span></span> <span data-ttu-id="f0043-122">Um dos ' AS2-para ' ou ' AS2-de ' cabeçalhos estão vazios</span><span class="sxs-lookup"><span data-stu-id="f0043-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="f0043-123">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-123">User action</span></span> | <span data-ttu-id="f0043-124">Foi recebida uma mensagem de AS2 que não continha Olá AS2-do ou AS2 tooor ambos os cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="f0043-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="f0043-125">Consulte a mensagem de AS2 AS2-do e AS2 tooheaders e corrija-os com base na configuração de contrato</span><span class="sxs-lookup"><span data-stu-id="f0043-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="f0043-126">* Em falta AS2 corpo da mensagem e os cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="f0043-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="f0043-127">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-127">Error description</span></span>| <span data-ttu-id="f0043-128">conteúdo do pedido Olá é nulo ou está vazio</span><span class="sxs-lookup"><span data-stu-id="f0043-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="f0043-129">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-129">User action</span></span> | <span data-ttu-id="f0043-130">Foi recebida uma mensagem de AS2 que não continha o corpo da mensagem Olá</span><span class="sxs-lookup"><span data-stu-id="f0043-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="f0043-131">* Falha de desencriptação de mensagem AS2</span><span class="sxs-lookup"><span data-stu-id="f0043-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="f0043-132">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-132">Error description</span></span> |  <span data-ttu-id="f0043-133">[processados/erro: falha de desencriptação]</span><span class="sxs-lookup"><span data-stu-id="f0043-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="f0043-134">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-134">User action</span></span> | <span data-ttu-id="f0043-135">Adicionar @base64ToBinary tooAS2Message antes de enviar toopartner</span><span class="sxs-lookup"><span data-stu-id="f0043-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="f0043-136">* Falha de desencriptação MDN</span><span class="sxs-lookup"><span data-stu-id="f0043-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="f0043-137">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-137">Error description</span></span> |  <span data-ttu-id="f0043-138">[processados/erro: falha de desencriptação]</span><span class="sxs-lookup"><span data-stu-id="f0043-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="f0043-139">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-139">User action</span></span> | <span data-ttu-id="f0043-140">Adicionar @base64ToBinary tooMDN antes de enviar toopartner</span><span class="sxs-lookup"><span data-stu-id="f0043-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="f0043-141">* Certificado de assinatura em falta</span><span class="sxs-lookup"><span data-stu-id="f0043-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="f0043-142">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-142">Error description</span></span>| <span data-ttu-id="f0043-143">Olá certificado de assinatura não foi configurado para terceiros AS2.</span><span class="sxs-lookup"><span data-stu-id="f0043-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="f0043-144">AS2-do: partner1 AS2-a: partner2</span><span class="sxs-lookup"><span data-stu-id="f0043-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="f0043-145">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-145">User action</span></span> | <span data-ttu-id="f0043-146">Configurar definições de contratos AS2 com o certificado correto para a assinatura</span><span class="sxs-lookup"><span data-stu-id="f0043-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="f0043-147">X12 e EDIFACT</span><span class="sxs-lookup"><span data-stu-id="f0043-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="f0043-148">* Esquerda ou à direita espaço encontrado</span><span class="sxs-lookup"><span data-stu-id="f0043-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="f0043-149">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-149">Error description</span></span> | <span data-ttu-id="f0043-150">Ocorreu um erro durante a análise.</span><span class="sxs-lookup"><span data-stu-id="f0043-150">Error encountered during parsing.</span></span> <span data-ttu-id="f0043-151">Olá transação Edifact definido com o id ' 123456 'contida no intercâmbio (sem grupo) com o id ' 987654', com o id do remetente 'Partner1', id de recetor 'Partner2' está a ser suspensa com os seguintes erros: separador à esquerda à direita encontrado</span><span class="sxs-lookup"><span data-stu-id="f0043-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="f0043-152">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-152">User action</span></span> | <span data-ttu-id="f0043-153">Olá contrato definições toobe configurado tooallow espaço à direita e à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f0043-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="f0043-154">Editar contrato definições tooallow espaço à direita e à esquerda</span><span class="sxs-lookup"><span data-stu-id="f0043-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![permitir espaço](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="f0043-156">* Ativou a verificação duplicada no contrato de Olá</span><span class="sxs-lookup"><span data-stu-id="f0043-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="f0043-157">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-157">Error description</span></span> | <span data-ttu-id="f0043-158">Número de controlo duplicado</span><span class="sxs-lookup"><span data-stu-id="f0043-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="f0043-159">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-159">User action</span></span> | <span data-ttu-id="f0043-160">Este erro indica a mensagem de saudação recebida tem controlo duplicado números.</span><span class="sxs-lookup"><span data-stu-id="f0043-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="f0043-161">Corrija o número de controlo de Olá e volte a enviar mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="f0043-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="f0043-162">* Esquema em falta no contrato de Olá</span><span class="sxs-lookup"><span data-stu-id="f0043-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="f0043-163">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-163">Error description</span></span> | <span data-ttu-id="f0043-164">Ocorreu um erro durante a análise.</span><span class="sxs-lookup"><span data-stu-id="f0043-164">Error encountered during parsing.</span></span> <span data-ttu-id="f0043-165">conjunto de transação de Olá X12 com o id '564220001' contidos no grupo de funcional com o id '56422', no intercâmbio com o id '000056422', com o id do remetente ' 12345678', id de recetor ' 87654321' está a ser suspensa com os seguintes erros "mensagem de saudação tem um ty de documento desconhecido PE e não foi possível resolver tooany de esquemas existentes Olá configurado no contrato de Olá "</span><span class="sxs-lookup"><span data-stu-id="f0043-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="f0043-166">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-166">User action</span></span> | <span data-ttu-id="f0043-167">Configurar esquema nas definições de contrato de Olá</span><span class="sxs-lookup"><span data-stu-id="f0043-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="f0043-168">* Esquema incorreto no contrato de Olá</span><span class="sxs-lookup"><span data-stu-id="f0043-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="f0043-169">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-169">Error description</span></span> | <span data-ttu-id="f0043-170">mensagem de saudação tem um tipo de documento desconhecido e não foi possível resolver tooany de esquemas existentes Olá configurado no contrato de Olá.</span><span class="sxs-lookup"><span data-stu-id="f0043-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="f0043-171">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-171">User action</span></span> | <span data-ttu-id="f0043-172">Configurar esquema correta nas definições de contrato de Olá</span><span class="sxs-lookup"><span data-stu-id="f0043-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="f0043-173">Ficheiro simples</span><span class="sxs-lookup"><span data-stu-id="f0043-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="f0043-174">* Mensagem de entrada com nenhum corpo</span><span class="sxs-lookup"><span data-stu-id="f0043-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="f0043-175">Descrição de erro</span><span class="sxs-lookup"><span data-stu-id="f0043-175">Error description</span></span> | <span data-ttu-id="f0043-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="f0043-176">InvalidTemplate.</span></span> <span data-ttu-id="f0043-177">Expressões de idioma do modelo não é possível tooprocess em entradas de 'Flat_File_Decoding' de ação na linha '1' e a coluna '1902': ' necessária propriedade 'content' espera um valor, mas obteve nulo.</span><span class="sxs-lookup"><span data-stu-id="f0043-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="f0043-178">Caminho '.'.</span><span class="sxs-lookup"><span data-stu-id="f0043-178">Path ''.'.</span></span> |
| <span data-ttu-id="f0043-179">Ação do utilizador</span><span class="sxs-lookup"><span data-stu-id="f0043-179">User action</span></span> | <span data-ttu-id="f0043-180">Este erro indica a mensagem de saudação entrada não contém um corpo</span><span class="sxs-lookup"><span data-stu-id="f0043-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="f0043-181">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="f0043-181">Learn more</span></span>
[<span data-ttu-id="f0043-182">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="f0043-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
