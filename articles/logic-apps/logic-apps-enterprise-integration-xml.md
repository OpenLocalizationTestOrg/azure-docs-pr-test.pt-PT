---
title: mensagens de aaaWorking com XML em fluxos de trabalho - Azure Logic Apps | Microsoft Docs
description: "Processar, validação, transformação e enriqueça XML mensagens as logic apps e a utilização de negócio tooscenarios Olá Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="374a6-103">Validar transformação XML, codificar e descodificar ficheiros simples e enriquecer a funcionalidades de mensagens nas logic apps</span><span class="sxs-lookup"><span data-stu-id="374a6-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="374a6-104">Utilizar as logic apps, terá de mensagens hello do capacidade tooprocess XML que enviar e receber.</span><span class="sxs-lookup"><span data-stu-id="374a6-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="374a6-105">Esta funcionalidade está incluída no Olá Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="374a6-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="374a6-106">Para os utilizadores com um fundo do BizTalk Server, Olá Enterprise Integration Pack dá-lhe semelhante tootransform de capacidades e validar mensagens, trabalhar com ficheiros simples e mesmo utilize XPath tooenrich ou extrair propriedades específicas de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="374a6-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="374a6-107">Para os utilizadores que são o novo espaço de toothis, estas funcionalidades expanda como processar mensagens dentro do seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="374a6-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="374a6-108">Por exemplo, se estiver num cenário de empresa-empresa e a trabalhar com esquemas XML específicas, em seguida, pode utilizar Olá Enterprise Integration Pack tooenhance como da sua empresa processa estas mensagens.</span><span class="sxs-lookup"><span data-stu-id="374a6-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="374a6-109">Olá Enterprise Integration Pack inclui:</span><span class="sxs-lookup"><span data-stu-id="374a6-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="374a6-110">[Validação XML](logic-apps-enterprise-integration-xml-validation.md "Saiba mais sobre a validação de mensagem XML") -validar uma mensagem XML de entrada ou saída com um esquema específico.</span><span class="sxs-lookup"><span data-stu-id="374a6-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="374a6-111">[Transformação XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Saiba mais sobre transformações de mensagem XML e mapas") - converter ou personalizar uma mensagem XML com base nos seus requisitos Olá requisitos ou de um parceiro.</span><span class="sxs-lookup"><span data-stu-id="374a6-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="374a6-112">[Simples e ficheiro codificação e descodificação de ficheiro simples](logic-apps-enterprise-integration-flatfile.md "Saiba mais sobre o ficheiro simples codificação/descodificação") - codificar ou descodificar um ficheiro simples.</span><span class="sxs-lookup"><span data-stu-id="374a6-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="374a6-113">Por exemplo, SAP aceita e envia ficheiros IDOC no formato de ficheiro simples.</span><span class="sxs-lookup"><span data-stu-id="374a6-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="374a6-114">Muitas plataformas de integração criar mensagens XML, incluindo as Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="374a6-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="374a6-115">Por isso, pode criar uma aplicação lógica que utiliza Olá ficheiro simples codificador demasiado "converter" XML ficheiros tooflat ficheiros.</span><span class="sxs-lookup"><span data-stu-id="374a6-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="374a6-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - enriquecer a uma mensagem e extrair propriedades específicas de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="374a6-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="374a6-117">Pode, em seguida, utilize Olá extraídos propriedades tooroute Olá mensagem tooa, ou de destino um ponto de final intermediário.</span><span class="sxs-lookup"><span data-stu-id="374a6-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="374a6-118">Experimentar</span><span class="sxs-lookup"><span data-stu-id="374a6-118">Try it out</span></span>
<span data-ttu-id="374a6-119">[Implementar uma aplicação lógica totalmente operacional ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (exemplo de GitHub) com funcionalidades XML Olá in Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="374a6-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="374a6-120">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="374a6-120">Learn more</span></span>
[<span data-ttu-id="374a6-121">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="374a6-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")
