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
# <a name="validate-xml-for-enterprise-integration"></a>Validar o XML para a integração do enterprise

Muitas vezes em cenários B2B, parceiros Olá um contrato de tem de se certificar de que as mensagens hello do que Exchange que são válidas antes de iniciar o processamento de dados. Pode validar documentos com um esquema predefinido utilizando o conector do Olá utilize Olá validação XML no Olá Enterprise Integration Pack.

## <a name="validate-a-document-with-hello-xml-validation-connector"></a>Validar um documento com o conector de validação XML Olá

1. Criar uma aplicação lógica, e [ligar Olá aplicação toohello integração conta](../logic-apps/logic-apps-enterprise-integration-accounts.md "saiba toolink uma aplicação de lógica de tooa da conta de integração") que tem o esquema de Olá pretende toouse para validar dados XML.

2. Adicionar um **pedido - pedido de HTTP um quando é recebido** aplicação de lógica de tooyour de Acionador.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. Olá tooadd **validação XML** ação, escolha **adicionar uma ação**.

4. Introduza toofilter Olá todas as ações toohello que quiser, *xml* na caixa de pesquisa de Olá. Escolha **validação XML**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. Selecione toospecify Olá conteúdo XML que pretende que o toovalidate, **conteúdo**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. Selecione a etiqueta body de Olá como Olá conteúdo que pretende que o toovalidate.

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. esquema de Olá toospecify pretende toouse para validar Olá anterior *conteúdo* de entrada, escolha **nome do esquema**.

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. Guarde o trabalho  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

Terminou agora a configuração do seu conector de validação. Uma aplicação do mundo real, pode querer dados de Olá validado toostore numa linha de negócio (LOB) aplicação, como o SalesForce. toosend Olá tooSalesforce saída validados, adicionar uma ação.

tootest a ação de validação, tornar um ponto final toohello HTTP de pedido.

## <a name="next-steps"></a>Passos seguintes
[Saiba mais sobre Olá Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")   

