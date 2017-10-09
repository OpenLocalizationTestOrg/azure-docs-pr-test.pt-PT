---
title: "aaaEnterprise integração para B2B - Azure Logic Apps | Microsoft Docs"
description: "Criar fluxos de trabalho B2B e suporta cenários de integração do enterprise para aplicações lógicas com Olá Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="79bdc-103">Descrição geral: Cenários B2B e comunicação com Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="79bdc-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="79bdc-104">Para fluxos de trabalho de empresa-empresa (B2B) e a comunicação totalmente integrada com Azure Logic Apps, pode ativar cenários de integração empresarial com a solução da Microsoft baseado na nuvem, Olá Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="79bdc-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="79bdc-105">As organizações podem trocar mensagens eletronicamente, mesmo que utilizem formatos e protocolos diferentes.</span><span class="sxs-lookup"><span data-stu-id="79bdc-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="79bdc-106">pacote de Olá transforma formatos diferentes num formato que sistemas das organizações podem interpretar e processar.</span><span class="sxs-lookup"><span data-stu-id="79bdc-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="79bdc-107">As organizações podem trocar mensagens através de protocolos de norma da indústria, incluindo [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), e [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="79bdc-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="79bdc-108">Também pode proteger as mensagens com a encriptação e assinaturas digitais.</span><span class="sxs-lookup"><span data-stu-id="79bdc-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="79bdc-109">Se estiver familiarizado com o BizTalk Server ou os BizTalk Services do Microsoft Azure, as funcionalidades de integração empresarial com Olá são toouse fácil porque a maioria dos conceitos são semelhantes.</span><span class="sxs-lookup"><span data-stu-id="79bdc-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="79bdc-110">Um principal diferença é que a integração empresarial com utiliza o armazenamento de Olá de toosimplify de contas de integração e a gestão de artefactos utilizado nas comunicações B2B.</span><span class="sxs-lookup"><span data-stu-id="79bdc-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="79bdc-111">Em termos de arquitetura, Olá Enterprise Integration Pack baseia-se no "contas de automatização".</span><span class="sxs-lookup"><span data-stu-id="79bdc-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="79bdc-112">Estas contas são contentores baseado na nuvem que armazenam todos os seus artefactos, como esquemas, parceiros, certificados, mapas e contratos.</span><span class="sxs-lookup"><span data-stu-id="79bdc-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="79bdc-113">Pode utilizar estes toodesign artefactos, implementar e manter as aplicações de B2B e também toobuild B2B fluxos de trabalho para aplicações lógicas.</span><span class="sxs-lookup"><span data-stu-id="79bdc-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="79bdc-114">Mas antes de poder utilizar destes artefactos, tem primeiro de associar a aplicação de lógica de tooyour de conta de integração.</span><span class="sxs-lookup"><span data-stu-id="79bdc-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="79bdc-115">Depois disso, a sua aplicação lógica pode aceder artefactos da sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="79bdc-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="79bdc-116">Por que motivo deve utilizar a integração empresarial?</span><span class="sxs-lookup"><span data-stu-id="79bdc-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="79bdc-117">Com a integração empresarial, pode armazenar todos os seus artefactos num único local – a sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="79bdc-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="79bdc-118">Pode criar fluxos de trabalho B2B e integrar com terceiros software como serviço (SaaS) apps, aplicações no local e aplicações personalizadas utilizando o motor de Azure Logic Apps Olá e todos os respetivos conectores.</span><span class="sxs-lookup"><span data-stu-id="79bdc-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="79bdc-119">Pode criar o código personalizado para as logic apps com as funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="79bdc-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="79bdc-120">Como tooget começar a integração empresarial com?</span><span class="sxs-lookup"><span data-stu-id="79bdc-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="79bdc-121">Pode criar e gerir aplicações de B2B com Olá Enterprise Integration Pack através do Designer de aplicação de lógica de Olá no Olá **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="79bdc-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="79bdc-122">Também pode gerir as logic apps com [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps do PowerShell tópicos").</span><span class="sxs-lookup"><span data-stu-id="79bdc-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="79bdc-123">Eis os passos de alto nível Olá que deve tomar antes de poder criar aplicações no Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="79bdc-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![Imagem de descrição geral](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="79bdc-125">Quais são alguns cenários comuns?</span><span class="sxs-lookup"><span data-stu-id="79bdc-125">What are some common scenarios?</span></span>

<span data-ttu-id="79bdc-126">Suporta a integração empresarial com essas normas da indústria:</span><span class="sxs-lookup"><span data-stu-id="79bdc-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="79bdc-127">EDI - intercâmbio de dados Eletrónicos</span><span class="sxs-lookup"><span data-stu-id="79bdc-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="79bdc-128">EAI - integração de aplicações da empresa</span><span class="sxs-lookup"><span data-stu-id="79bdc-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="79bdc-129">Eis o que precisa de tooget iniciado</span><span class="sxs-lookup"><span data-stu-id="79bdc-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="79bdc-130">Uma subscrição do Azure com uma conta de integração</span><span class="sxs-lookup"><span data-stu-id="79bdc-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="79bdc-131">Visual Studio 2015 toocreate maps e esquemas</span><span class="sxs-lookup"><span data-stu-id="79bdc-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="79bdc-132">Ferramentas de integração do Microsoft Azure lógica empresarial de aplicações para o Visual Studio 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="79bdc-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="79bdc-133">Experimentar agora</span><span class="sxs-lookup"><span data-stu-id="79bdc-133">Try it now</span></span>

<span data-ttu-id="79bdc-134">[Implementar totalmente operacional exemplo AS2 enviar e receber a aplicação lógica](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) que utiliza funcionalidades Olá B2B para Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="79bdc-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="79bdc-135">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="79bdc-135">Learn more</span></span>
* [<span data-ttu-id="79bdc-136">Contratos</span><span class="sxs-lookup"><span data-stu-id="79bdc-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre contratos de integração do enterprise")
* [<span data-ttu-id="79bdc-137">Cenários de tooBusiness (B2B) empresariais</span><span class="sxs-lookup"><span data-stu-id="79bdc-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Saiba como toocreate Logic apps com funcionalidades de B2B")  
* [<span data-ttu-id="79bdc-138">Certificados</span><span class="sxs-lookup"><span data-stu-id="79bdc-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Saiba mais sobre certificados de integração do enterprise")
* [<span data-ttu-id="79bdc-139">Simples de ficheiro codificação/descodificação</span><span class="sxs-lookup"><span data-stu-id="79bdc-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Saiba como tooencode e descodificar o conteúdo do ficheiro simples")  
* [<span data-ttu-id="79bdc-140">Contas de automatização</span><span class="sxs-lookup"><span data-stu-id="79bdc-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Saiba mais sobre contas de automatização")
* [<span data-ttu-id="79bdc-141">Mapeia</span><span class="sxs-lookup"><span data-stu-id="79bdc-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre a maps de integração do enterprise")
* [<span data-ttu-id="79bdc-142">Parceiros</span><span class="sxs-lookup"><span data-stu-id="79bdc-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Saiba mais sobre a parceiros de integração do enterprise")
* [<span data-ttu-id="79bdc-143">Esquemas</span><span class="sxs-lookup"><span data-stu-id="79bdc-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Saiba mais sobre esquemas de integração do enterprise")
* [<span data-ttu-id="79bdc-144">Validação de mensagem XML</span><span class="sxs-lookup"><span data-stu-id="79bdc-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Saiba como toovalidate XML mensagens com as Logic apps")
* [<span data-ttu-id="79bdc-145">Transformação XML</span><span class="sxs-lookup"><span data-stu-id="79bdc-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Saiba mais sobre a maps de integração do enterprise")
* [<span data-ttu-id="79bdc-146">Conectores de integração empresarial</span><span class="sxs-lookup"><span data-stu-id="79bdc-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Saiba mais sobre os conectores de pacote de integração do enterprise")
* [<span data-ttu-id="79bdc-147">Metadados da conta de integração</span><span class="sxs-lookup"><span data-stu-id="79bdc-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Saiba mais sobre metadados da conta de integração")
* [<span data-ttu-id="79bdc-148">Monitorizar as mensagens B2B</span><span class="sxs-lookup"><span data-stu-id="79bdc-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "saber mais sobre a monitorização de mensagens B2B")
* [<span data-ttu-id="79bdc-149">Controlo mensagens B2B no portal do OMS</span><span class="sxs-lookup"><span data-stu-id="79bdc-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Saiba mais sobre o controlo mensagens B2B no portal do OMS")

