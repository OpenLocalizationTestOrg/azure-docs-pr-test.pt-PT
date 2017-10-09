---
title: "recuperação de aaaDisaster para a conta de integração de B2B - Azure Logic Apps | Microsoft Docs"
description: "Recuperação de desastres do Logic Apps B2B"
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
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Recuperação de desastre por várias regiões lógica B2B de aplicações

B2B cargas de trabalho envolvem transações dinheiro como encomendas pendentes e faturas. Durante um evento de desastre, é essencial para uma Olá toomeet do negócio tooquickly recuperar que SLAs de nível empresarial acordadas com os respetivos parceiros. Este artigo demonstra como planear a toobuild continuidade do negócio para cargas de trabalho B2B. 

* Preparação de recuperação de desastre 
* Efetuar a ativação pós-falha toosecondary região durante um evento de desastre 
* Reverter tooprimary região após um evento de desastre

## <a name="disaster-recovery-readiness"></a>Preparação de recuperação de desastre  

1. Identifique uma região secundária e crie um [conta integração](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) na região secundária Olá.

2. Adicione parceiros, esquemas e contratos para fluxos de mensagens hello necessário onde Olá executar estado tem de toobe replicado toosecondary região integração conta.

   > [!TIP]
   > Certifique-se de que existe consistência na Convenção de nomenclatura do artefacto de Olá, integração conta em regiões. 

3. Olá toopull executar o estado da região primária Olá, criar uma aplicação lógica na região secundária Olá. 

   Esta aplicação lógica deve ter um *acionador* e um *ação*. 
   acionador Olá deve estabelecer ligação a conta de integração de região tooprimary e ação de Olá deve estabelecer ligação a conta de integração do toosecondary região. 
   Com base num intervalo de tempo de Olá, o acionador Olá consulta a tabela de estado de região primária executar Olá e obtém novos registos de Olá, se aplicável. ação de Olá atualiza-los a conta de integração de região toosecondary. 
   Isto ajuda-o estado de incremental runtime tooget da região de toosecondary região primária.

4. Continuidade do negócio em Logic Apps é a conta de integração concebidos toosupport com base em protocolos de B2B - X12, AS2 e EDIFACT. passos de detalhado toofind, selecione Olá as respetivas ligações.

5. Olá recomendação é toodeploy todos os recursos de região primária numa região secundária demasiado. 

   Recursos de região primária incluem a SQL Database do Azure ou do Azure Cosmos DB, Service Bus do Azure e utilizado para as mensagens, a API Management do Azure e a funcionalidade de Azure Logic Apps Olá no App Service do Azure de Event Hubs do Azure.   

6. Estabelece uma ligação a uma região secundária de tooa região primária. Olá toopull executar estado a partir de uma região primária, criar uma aplicação lógica numa região secundária. 

   aplicação de lógica de Olá deve ter um acionador e uma ação. 
   acionador Olá deve ligar a conta de integração de região primária tooa. 
   ação de Olá deve estabelecer ligação a conta de integração do tooa região secundária. 
   Com base num intervalo de tempo de Olá, o acionador Olá consulta a tabela de estado de região primária executar Olá e obtém novos registos de Olá, se aplicável. 
   ação de Olá atualiza-los a conta de integração de região secundária tooa. 
   Este processo ajuda-o estado de incremental runtime tooget da região secundária do Olá região primária toohello.

Continuidade do negócio numa conta integração Logic Apps fornece suporte com base em protocolos de B2B Olá X12, AS2 e EDIFACT. Para obter passos detalhados sobre como utilizar X12 e AS2, consulte [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) e [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) neste artigo.

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>Efetuar a ativação pós-falha região secundária tooa durante um evento de desastre

Durante um evento de desastre, quando a região primária Olá não está disponível para a continuidade do negócio, região secundária do tráfego direta toohello. Uma ajuda a região secundária toorecover um negócio rapidamente funciona toomeet Olá RPO/RTO acordada pelos respetivos parceiros. Também minimiza os esforços toofail através da região de tooanother uma região. 

Há uma latência esperada ao copiar os números de controlo de uma região secundária de tooa região primária. tooavoid enviar duplicado controlo gerado números toopartners durante um evento de desastre, recomendação Olá seja tooincrement Olá controlo composto por números nos contratos de região secundária Olá utilizando [cmdlets do PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>Reverter eventos de pós-desastre tooa região primária

toofall tooa anterior a região primária quando estiver disponível, siga estes passos:

1. Pare a aceitação das mensagens de parceiros na região secundária Olá.  

2. Incrementar números de controlo de Olá gerado para todos os contratos de região primária Olá utilizando [cmdlets do PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).  

3. Tráfego direto de região primária do Olá região secundária toohello.

4. Certifique-se de que aplicação de lógica de Olá criada numa região secundária de Olá para extrair a executar o estado da região primária Olá está ativada.

## <a name="x12"></a>X12 

Continuidade do negócio para EDI X 12 documentos baseia-se em números de controlo:

> [!TIP]
> Também pode utilizar Olá [X12 rápido iniciar modelo](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps. Criar contas de automatização primária e secundária são modelo de Olá toouse de pré-requisitos. Olá modelo ajuda as logic apps de dois toocreate, para números de controlo recebido e outra para números de controlo gerado. Respetivos acionadores e ações são criadas no Olá as logic apps, ligar Olá acionador toohello integração primário contas e Olá ação toohello integração secundário.

**Pré-requisitos**

recuperação de desastres tooenable para mensagens de entrada, selecione Olá duplicado Verifique as definições do receber definições do contrato de Olá X12.

![Selecione as definições de verificação duplicado](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. Criar um [aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md) numa região secundária.    

2. Pesquisar nos **X12**e selecione **X12-quando um número de controlo é modificado**.   

   ![Procure o X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   acionador Olá solicita tooestablish uma conta de integração de tooan de ligação. 
   acionador Olá deve ser ligado a conta de integração do tooa região primária.

3. Introduza um nome de ligação, selecione o *conta de integração de região primária* de Olá lista e escolha **criar**.   

   ![Nome de conta de integração de região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. Olá **sincronização de número de controlo do DateTime toostart** definição é opcional. Olá **frequência** pode ser definido demasiado**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.   

   ![DateTime e a frequência](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. Selecione **novo passo** > **adicionar uma ação**.

   ![Novo passo, adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. Pesquisar nos **X12**e selecione **X12-adicionar ou atualizar os números de controlo**.   

   ![Adicionar ou atualizar os números de controlo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. Selecione tooconnect uma conta de integração do ação tooa região secundária, **Alterar ligação** > **Adicionar nova ligação** para obter uma lista de contas de integração disponível Olá. Introduza um nome de ligação, selecione o *conta de integração de região secundária* de Olá lista e escolha **criar**. 

   ![Nome de conta de integração de região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. Mudar tooraw entradas clicando no ícone de Olá no canto superior direito.

   ![Comutador tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Selecione o corpo do Seletor de conteúdo dinâmico Olá e guardar a aplicação de lógica de Olá.

   ![Campos de conteúdo dinâmicos](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   Com base num intervalo de tempo de Olá, o acionador de Olá consulta a tabela de número de controlo do Olá região primária recebido e obtém novos registos de Olá. 
   ação de Olá atualiza os registos de Olá na conta de integração do Olá região secundária. 
   Se não existirem não existem atualizações, o estado de Acionador de Olá aparece como **ignorados**.   

   ![Tabela de número de controlo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Com base num intervalo de tempo de Olá, estado de incremental runtime Olá replica a partir de uma região secundária de tooa região primária. Durante um evento de desastre, quando a região primária Olá não é a região secundária de toohello tráfego disponível, direta para a continuidade do negócio. 

## <a name="edifact"></a>EDIFACT 

Continuidade do negócio para documentos EDI EDIFACT baseia-se em números de controlo.

**Pré-requisitos**

tooenable recuperação de desastres para as mensagens de entrada, selecione Olá duplicado Verifique as definições do receber definições seu contrato EDIFACT.

![Selecione as definições de verificação duplicado](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. Criar um [aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md) numa região secundária.    

2. Pesquisar nos **EDIFACT**e selecione **EDIFACT - quando um número de controlo é modificado**.

   ![Procure EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   acionador Olá solicita tooestablish uma conta de integração de tooan de ligação. 
   acionador Olá deve ser ligado a conta de integração do tooa região primária. 

3. Introduza um nome de ligação, selecione o *conta de integração de região primária* de Olá lista e escolha **criar**.    

   ![Nome de conta de integração de região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. Olá **sincronização de número de controlo do DateTime toostart** definição é opcional. Olá **frequência** pode ser definido demasiado**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.    

   ![DateTime e a frequência](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. Selecione **novo passo** > **adicionar uma ação**.    

   ![Novo passo, adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. Pesquisar nos **EDIFACT**e selecione **EDIFACT - adicionar ou atualizar os números de controlo**.   

   ![Adicionar ou atualizar os números de controlo](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. Selecione tooconnect uma conta de integração do ação tooa região secundária, **Alterar ligação** > **Adicionar nova ligação** para obter uma lista de contas de integração disponível Olá. Introduza um nome de ligação, selecione o *conta de integração de região secundária* de Olá lista e escolha **criar**.

   ![Nome de conta de integração de região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. Mudar tooraw entradas clicando no ícone de Olá no canto superior direito.

   ![Comutador tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Selecione o corpo do Seletor de conteúdo dinâmico Olá e guardar a aplicação de lógica de Olá.   

   ![Campos de conteúdo dinâmicos](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   Com base num intervalo de tempo de Olá, o acionador de Olá consulta a tabela de número de controlo do Olá região primária recebido e obtém novos registos de Olá.
   ação de Olá atualiza a conta de integração do Olá registos toohello região secundária. 
   Se não existirem não existem atualizações, o estado de Acionador de Olá aparece como **ignorados**.

   ![Tabela de número de controlo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Com base num intervalo de tempo de Olá, estado de incremental runtime Olá replica a partir de uma região secundária de tooa região primária. Durante um evento de desastre, quando a região primária Olá não é a região secundária de toohello tráfego disponível, direta para a continuidade do negócio. 

## <a name="as2"></a>AS2 

Continuidade do negócio para documentos que utilizam o protocolo de AS2 Olá baseia-se no ID de mensagem de Olá e valor MIC Olá.

> [!TIP]
> Também pode utilizar Olá [AS2 início rápido modelo](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps. Criar contas de automatização primária e secundária são modelo de Olá toouse de pré-requisitos. modelo de Olá ajuda a criar uma aplicação lógica que tem um acionador e uma ação. aplicação de lógica de Olá cria uma ligação a partir de uma conta do acionador tooa integração primária e uma conta de ação de integração secundário tooa.

1. Criar um [aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md) na região secundária Olá.  

2. Pesquisar nos **AS2**e selecione **AS2 - valor MIC de quando é criado**.   

   ![Procure AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   Um acionador pede-lhe tooestablish uma conta de integração de tooan de ligação. 
   acionador Olá deve ser ligado a conta de integração do tooa região primária. 
   
3. Introduza um nome de ligação, selecione o *conta de integração de região primária* de Olá lista e escolha **criar**.

   ![Nome de conta de integração de região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. Olá **sincronização de valor DateTime toostart MIC** definição é opcional. Olá **frequência** pode ser definido demasiado**dia**, **hora**, **minuto**, ou **segundo** com um intervalo.   

   ![DateTime e a frequência](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. Selecione **novo passo** > **adicionar uma ação**.  

   ![Novo passo, adicionar uma ação](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. Pesquisar nos **AS2**e selecione **AS2 - adicionar ou atualizar o conteúdo do MIC**.  

   ![Adição de MIC ou atualização](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. Selecione tooconnect conta de ação tooa integração secundária, **Alterar ligação** > **Adicionar nova ligação** para obter uma lista de contas de integração disponível Olá. Introduza um nome de ligação, selecione o *conta de integração de região secundária* de Olá lista e escolha **criar**.

   ![Nome de conta de integração de região secundária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. Mudar tooraw entradas clicando no ícone de Olá no canto superior direito.

   ![Comutador tooraw entradas](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Selecione o corpo do Seletor de conteúdo dinâmico Olá e guardar a aplicação de lógica de Olá.   

   ![Conteúdo dinâmico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   Com base num intervalo de tempo de Olá, o acionador de Olá consulta a tabela de região primária Olá e obtém novos registos de Olá. ação de Olá atualiza-los a conta de integração de região secundária toohello. 
   Se não existirem não existem atualizações, o estado de Acionador de Olá aparece como **ignorados**.  

   ![Tabela de região primária](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

Estado de incremental runtime Olá com base num intervalo de tempo de Olá, replica a região secundária do Olá região primária toohello. Durante um evento de desastre, quando a região primária Olá não é a região secundária de toohello tráfego disponível, direta para a continuidade do negócio. 

## <a name="next-steps"></a>Passos seguintes

[Monitorizar mensagens B2B](logic-apps-monitor-b2b-message.md)

