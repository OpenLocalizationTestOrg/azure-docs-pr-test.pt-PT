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
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>Descrição geral: Cenários B2B e comunicação com Olá Enterprise Integration Pack

Para fluxos de trabalho de empresa-empresa (B2B) e a comunicação totalmente integrada com Azure Logic Apps, pode ativar cenários de integração empresarial com a solução da Microsoft baseado na nuvem, Olá Enterprise Integration Pack. As organizações podem trocar mensagens eletronicamente, mesmo que utilizem formatos e protocolos diferentes. pacote de Olá transforma formatos diferentes num formato que sistemas das organizações podem interpretar e processar. As organizações podem trocar mensagens através de protocolos de norma da indústria, incluindo [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), e [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md). Também pode proteger as mensagens com a encriptação e assinaturas digitais.

Se estiver familiarizado com o BizTalk Server ou os BizTalk Services do Microsoft Azure, as funcionalidades de integração empresarial com Olá são toouse fácil porque a maioria dos conceitos são semelhantes. Um principal diferença é que a integração empresarial com utiliza o armazenamento de Olá de toosimplify de contas de integração e a gestão de artefactos utilizado nas comunicações B2B. 

Em termos de arquitetura, Olá Enterprise Integration Pack baseia-se no "contas de automatização". Estas contas são contentores baseado na nuvem que armazenam todos os seus artefactos, como esquemas, parceiros, certificados, mapas e contratos. Pode utilizar estes toodesign artefactos, implementar e manter as aplicações de B2B e também toobuild B2B fluxos de trabalho para aplicações lógicas. Mas antes de poder utilizar destes artefactos, tem primeiro de associar a aplicação de lógica de tooyour de conta de integração. Depois disso, a sua aplicação lógica pode aceder artefactos da sua conta de integração.

## <a name="why-should-you-use-enterprise-integration"></a>Por que motivo deve utilizar a integração empresarial?

* Com a integração empresarial, pode armazenar todos os seus artefactos num único local – a sua conta de integração.
* Pode criar fluxos de trabalho B2B e integrar com terceiros software como serviço (SaaS) apps, aplicações no local e aplicações personalizadas utilizando o motor de Azure Logic Apps Olá e todos os respetivos conectores.
* Pode criar o código personalizado para as logic apps com as funções do Azure.

## <a name="how-tooget-started-with-enterprise-integration"></a>Como tooget começar a integração empresarial com?

Pode criar e gerir aplicações de B2B com Olá Enterprise Integration Pack através do Designer de aplicação de lógica de Olá no Olá **portal do Azure**. Também pode gerir as logic apps com [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps do PowerShell tópicos").

Eis os passos de alto nível Olá que deve tomar antes de poder criar aplicações no Olá portal do Azure:

![Imagem de descrição geral](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>Quais são alguns cenários comuns?

Suporta a integração empresarial com essas normas da indústria:

* EDI - intercâmbio de dados Eletrónicos
* EAI - integração de aplicações da empresa

## <a name="heres-what-you-need-tooget-started"></a>Eis o que precisa de tooget iniciado

* Uma subscrição do Azure com uma conta de integração
* Visual Studio 2015 toocreate maps e esquemas
* [Ferramentas de integração do Microsoft Azure lógica empresarial de aplicações para o Visual Studio 2015 2.0](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>Experimentar agora

[Implementar totalmente operacional exemplo AS2 enviar e receber a aplicação lógica](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) que utiliza funcionalidades Olá B2B para Azure Logic Apps.

## <a name="learn-more"></a>Saiba mais
* [Contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre contratos de integração do enterprise")
* [Cenários de tooBusiness (B2B) empresariais](../logic-apps/logic-apps-enterprise-integration-b2b.md "Saiba como toocreate Logic apps com funcionalidades de B2B")  
* [Certificados](logic-apps-enterprise-integration-certificates.md "Saiba mais sobre certificados de integração do enterprise")
* [Simples de ficheiro codificação/descodificação](logic-apps-enterprise-integration-flatfile.md "Saiba como tooencode e descodificar o conteúdo do ficheiro simples")  
* [Contas de automatização](../logic-apps/logic-apps-enterprise-integration-accounts.md "Saiba mais sobre contas de automatização")
* [Mapeia](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre a maps de integração do enterprise")
* [Parceiros](logic-apps-enterprise-integration-partners.md "Saiba mais sobre a parceiros de integração do enterprise")
* [Esquemas](logic-apps-enterprise-integration-schemas.md "Saiba mais sobre esquemas de integração do enterprise")
* [Validação de mensagem XML](logic-apps-enterprise-integration-xml.md "Saiba como toovalidate XML mensagens com as Logic apps")
* [Transformação XML](logic-apps-enterprise-integration-transform.md "Saiba mais sobre a maps de integração do enterprise")
* [Conectores de integração empresarial](../connectors/apis-list.md "Saiba mais sobre os conectores de pacote de integração do enterprise")
* [Metadados da conta de integração](../logic-apps/logic-apps-enterprise-integration-metadata.md "Saiba mais sobre metadados da conta de integração")
* [Monitorizar as mensagens B2B](logic-apps-monitor-b2b-message.md "saber mais sobre a monitorização de mensagens B2B")
* [Controlo mensagens B2B no portal do OMS](logic-apps-track-b2b-messages-omsportal.md "Saiba mais sobre o controlo mensagens B2B no portal do OMS")

