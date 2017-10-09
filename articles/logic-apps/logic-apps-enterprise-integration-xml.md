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
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a>Validar transformação XML, codificar e descodificar ficheiros simples e enriquecer a funcionalidades de mensagens nas logic apps

Utilizar as logic apps, terá de mensagens hello do capacidade tooprocess XML que enviar e receber. Esta funcionalidade está incluída no Olá Enterprise Integration Pack. Para os utilizadores com um fundo do BizTalk Server, Olá Enterprise Integration Pack dá-lhe semelhante tootransform de capacidades e validar mensagens, trabalhar com ficheiros simples e mesmo utilize XPath tooenrich ou extrair propriedades específicas de uma mensagem. 

Para os utilizadores que são o novo espaço de toothis, estas funcionalidades expanda como processar mensagens dentro do seu fluxo de trabalho. Por exemplo, se estiver num cenário de empresa-empresa e a trabalhar com esquemas XML específicas, em seguida, pode utilizar Olá Enterprise Integration Pack tooenhance como da sua empresa processa estas mensagens. 

Olá Enterprise Integration Pack inclui: 

* [Validação XML](logic-apps-enterprise-integration-xml-validation.md "Saiba mais sobre a validação de mensagem XML") -validar uma mensagem XML de entrada ou saída com um esquema específico.
* [Transformação XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Saiba mais sobre transformações de mensagem XML e mapas") - converter ou personalizar uma mensagem XML com base nos seus requisitos Olá requisitos ou de um parceiro.
* [Simples e ficheiro codificação e descodificação de ficheiro simples](logic-apps-enterprise-integration-flatfile.md "Saiba mais sobre o ficheiro simples codificação/descodificação") - codificar ou descodificar um ficheiro simples. Por exemplo, SAP aceita e envia ficheiros IDOC no formato de ficheiro simples. Muitas plataformas de integração criar mensagens XML, incluindo as Logic Apps. Por isso, pode criar uma aplicação lógica que utiliza Olá ficheiro simples codificador demasiado "converter" XML ficheiros tooflat ficheiros. 
* [XPath](https://msdn.microsoft.com/library/mt643789.aspx) - enriquecer a uma mensagem e extrair propriedades específicas de mensagem de saudação. Pode, em seguida, utilize Olá extraídos propriedades tooroute Olá mensagem tooa, ou de destino um ponto de final intermediário.

## <a name="try-it-out"></a>Experimentar
[Implementar uma aplicação lógica totalmente operacional ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (exemplo de GitHub) com funcionalidades XML Olá in Azure Logic Apps.

## <a name="learn-more"></a>Saiba mais
[Saiba mais sobre Olá Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")
