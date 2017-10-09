---
title: aaaValidate XML - Azure Logic Apps | Microsoft Docs
description: "Validar o XML com esquemas para o Azure Logic Apps e cenários B2B utilizando Olá Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="78fe7-103">Validar o XML para a integração do enterprise</span><span class="sxs-lookup"><span data-stu-id="78fe7-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="78fe7-104">Muitas vezes em cenários B2B, parceiros Olá um contrato de tem de se certificar de que as mensagens hello do que Exchange que são válidas antes de iniciar o processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="78fe7-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="78fe7-105">Pode validar documentos com um esquema predefinido utilizando o conector do Olá utilize Olá validação XML no Olá Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="78fe7-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="78fe7-106">Validar um documento com o conector de validação XML Olá</span><span class="sxs-lookup"><span data-stu-id="78fe7-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="78fe7-107">Criar uma aplicação lógica, e [ligar Olá aplicação toohello integração conta](../logic-apps/logic-apps-enterprise-integration-accounts.md "saiba toolink uma aplicação de lógica de tooa da conta de integração") que tem o esquema de Olá pretende toouse para validar dados XML.</span><span class="sxs-lookup"><span data-stu-id="78fe7-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="78fe7-108">Adicionar um **pedido - pedido de HTTP um quando é recebido** aplicação de lógica de tooyour de Acionador.</span><span class="sxs-lookup"><span data-stu-id="78fe7-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="78fe7-109">Olá tooadd **validação XML** ação, escolha **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="78fe7-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="78fe7-110">Introduza toofilter Olá todas as ações toohello que quiser, *xml* na caixa de pesquisa de Olá.</span><span class="sxs-lookup"><span data-stu-id="78fe7-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="78fe7-111">Escolha **validação XML**.</span><span class="sxs-lookup"><span data-stu-id="78fe7-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="78fe7-112">Selecione toospecify Olá conteúdo XML que pretende que o toovalidate, **conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="78fe7-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="78fe7-113">Selecione a etiqueta body de Olá como Olá conteúdo que pretende que o toovalidate.</span><span class="sxs-lookup"><span data-stu-id="78fe7-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="78fe7-114">esquema de Olá toospecify pretende toouse para validar Olá anterior *conteúdo* de entrada, escolha **nome do esquema**.</span><span class="sxs-lookup"><span data-stu-id="78fe7-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="78fe7-115">Guarde o trabalho</span><span class="sxs-lookup"><span data-stu-id="78fe7-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="78fe7-116">Terminou agora a configuração do seu conector de validação.</span><span class="sxs-lookup"><span data-stu-id="78fe7-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="78fe7-117">Uma aplicação do mundo real, pode querer dados de Olá validado toostore numa linha de negócio (LOB) aplicação, como o SalesForce.</span><span class="sxs-lookup"><span data-stu-id="78fe7-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="78fe7-118">toosend Olá tooSalesforce saída validados, adicionar uma ação.</span><span class="sxs-lookup"><span data-stu-id="78fe7-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="78fe7-119">tootest a ação de validação, tornar um ponto final toohello HTTP de pedido.</span><span class="sxs-lookup"><span data-stu-id="78fe7-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78fe7-120">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="78fe7-120">Next steps</span></span>
[<span data-ttu-id="78fe7-121">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="78fe7-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")   

