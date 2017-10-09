---
title: mensagens de aaaTrack B2B no Operations Management Suite - Azure Logic Apps | Microsoft Docs
description: "Controlar a comunicação de B2B para as suas aplicações de conta e a lógica da integração no Operations Management Suite (OMS) com o Log Analytics do Azure"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>Controlar a comunicação de B2B no Olá Microsoft Operations Management Suite (OMS)

Após configurar a comunicação de B2B entre duas a executar os processos de negócios ou aplicações através da sua conta de integração, estas entidades podem trocar mensagens entre si. toocheck se estas mensagens são processadas corretamente, pode controlar AS2, X12, e EDIFACT mensagens com [Log Analytics do Azure](../log-analytics/log-analytics-overview.md) no Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Por exemplo, pode utilizar estas capacidades de controlo baseada na web para o registo de mensagens:

* Contagem de mensagens e o Estado
* Estado em que as confirmações
* Correlacionar mensagens com em que as confirmações
* Descrições de erro detalhadas para falhas
* Capacidades de pesquisa

## <a name="requirements"></a>Requisitos

* Uma aplicação lógica que esteja configurada com o registo de diagnóstico. Saiba [como toocreate uma aplicação lógica](logic-apps-create-a-logic-app.md) e [como tooset segurança de registo para essa aplicação lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Uma conta de integração que está configurada com a monitorização e registo. Saiba [como toocreate uma conta de integração](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [como tooset cópias de segurança de monitorização e de registo para essa conta](../logic-apps/logic-apps-monitor-b2b-message.md).

* Se ainda não o fez, [publicar dados de diagnóstico tooLog análise](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) no OMS.

> [!NOTE]
> Após cumprir requisitos de anteriores Olá, deve ter uma área de trabalho Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Deve utilizar Olá mesma OMS área de trabalho para controlar a sua comunicação B2B no OMS. 
>  
> Se não tiver uma área de trabalho do OMS, saiba [como toocreate uma área de trabalho do OMS](../log-analytics/log-analytics-get-started.md).

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Adicionar Olá Logic Apps B2B solução toohello Operations Management Suite (OMS)

toohave OMS controlar B2B mensagens para a sua aplicação lógica, tem de adicionar Olá **Logic Apps B2B** portal do OMS solução toohello. Saiba mais sobre [adicionar soluções tooOMS](../log-analytics/log-analytics-get-started.md).

1. No Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**. Procure "análise de registos" e, em seguida, escolha **Log Analytics** conforme mostrado aqui:

   ![Localizar a análise de registos](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. Em **Log Analytics**, localize e selecione a sua área de trabalho do OMS. 

   ![Selecione a sua área de trabalho do OMS](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. Em **gestão**, escolha **Portal do OMS**.

   ![Escolha o portal do OMS](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Depois de abrir a home page do OMS Olá, escolha **soluções galeria**.    

   ![Escolha a Galeria de soluções](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. Em **todas as soluções**, localizar e escolha **Logic Apps B2B**.     

   ![Escolha as Logic Apps B2B](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. Em **Logic Apps B2B**, escolha **adicionar**.

   ![Escolher adicionar](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   Na página inicial do Olá OMS, Olá mosaico para **Logic Apps B2B mensagens** aparece. 
   Este mosaico atualiza a contagem de mensagens hello quando as mensagens B2B são processadas.

   ![Página inicial do OMS, Logic Apps B2B mensagens mosaico](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>Controlar o estado de mensagem e os detalhes na Olá Operations Management Suite

1. Depois das mensagens B2B são processadas, pode ver o estado de Olá e os detalhes para essas mensagens. Na página inicial do Olá OMS, escolha Olá **Logic Apps B2B mensagens** mosaico.

   ![Contagem de mensagens atualizado](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > Por predefinição, Olá **Logic Apps B2B mensagens** mosaico mostra dados com base num único dia. definir o âmbito de dados de Olá toochange tooa de intervalo diferente, escolha o controlo de âmbito de Olá ao hello parte superior da página do OMS Olá:
   > 
   > ![Alterar o âmbito de dados](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Depois de estado de mensagem de Olá dashboard é apresentado, pode ver mais detalhes sobre um tipo de mensagem específico, que mostra os dados com base num único dia. Escolha o mosaico Olá para **AS2**, **X12**, ou **EDIFACT**.

   ![Ver o estado de mensagem](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   É apresentada uma lista de mensagens em fila para o mosaico escolhido. 
   toolearn mais informações sobre as propriedades de Olá para cada tipo de mensagem, consulte estas descrições de propriedade de mensagem:

   * [Propriedades da mensagem AS2](#as2-message-properties)
   * [Propriedades da mensagem X12](#x12-message-properties)
   * [Propriedades da mensagem EDIFACT](#EDIFACT-message-properties)

   Por exemplo, aqui está uma lista de mensagens AS2 poderá aspeto:

   ![Ver mensagens de AS2](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. entradas de Olá tooview ou de exportação e saídas para as mensagens específicas, selecione esses mensagens e escolha **transferir**. Quando lhe for pedido, guarde o computador de tooyour de ficheiro. zip do Olá local e, em seguida, a extrair esse ficheiro. 

   pasta extraída Olá inclui uma pasta para cada mensagem selecionada. 
   Se configurar as confirmações, pasta de mensagem de Olá também inclui ficheiros com detalhes de confirmação. 
   Pasta cada mensagem tem, pelo menos, estes ficheiros: 
   
   * Detalhes de payload payload e de saída de entrada de ficheiros legível por humanos com Olá
   * Ficheiros codificados com Olá entradas e saídas

   Para cada tipo de mensagem, pode encontrar a pasta de Olá e formatos de nome de ficheiro aqui:

   * [Formatos de nome de pasta e ficheiro AS2](#as2-folder-file-names)
   * [X12 formatos de nome de pasta e ficheiro](#x12-folder-file-names)
   * [Formatos de nome de pasta e ficheiro EDIFACT](#edifact-folder-file-names)

   ![Transferir ficheiros de mensagens](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview todas as ações que tenham Olá mesmo executam ID, Olá **pesquisa registo** página, escolha uma mensagem a partir da lista de mensagens hello.

   Pode ordenar estas ações por coluna ou procure resultados específicos.

   ![As ações com Olá mesmo executar o ID](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * resultados de toosearch com consultas prebuilt, escolha **Favoritos**.

   * Saiba [como toobuild consulta adicionando filtros](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md). 
   Ou Saiba mais sobre [como toofind dados com o registo de pesquisa na análise de registos](../log-analytics/log-analytics-log-searches.md).

   * consulta de toochange na caixa de pesquisa de Olá, atualização Olá consulta com Olá colunas e valores que pretende que toouse como filtros.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>Descrições das propriedades e formatos de nome para AS2, X12 e mensagens EDIFACT

Para cada tipo de mensagem, seguem-se descrições de propriedade de Olá e formatos de nome de ficheiros de mensagens transferido.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>Descrições de propriedade de mensagem AS2

Seguem-se descrições de propriedade Olá para cada mensagem AS2.

| Propriedade | Descrição |
| --- | --- |
| Remetente | parceiro de convidado de Olá especificado no **receber definições**, ou o parceiro de anfitrião Olá especificados em **enviar definições** para um contrato de AS2 |
| Recetor | parceiro de anfitrião de Olá especificado no **receber definições**, ou o parceiro de convidado Olá especificados em **enviar definições** para um contrato de AS2 |
| Aplicação Lógica | aplicação de lógica de olá onde são configuradas ações Olá AS2 |
| Estado | Olá estado de mensagem AS2 <br>Êxito = recebidos ou enviados uma mensagem de AS2 válida. Não existem MDN está definida. <br>Êxito = recebidos ou enviados uma mensagem de AS2 válida. MDN está configurado e recebido ou MDN é enviado. <br>Não foi possível = recebida uma mensagem de AS2 inválida. Não existem MDN está definida. <br>Pendente = recebidos ou enviados uma mensagem de AS2 válida. Configurar a MDN e MDN é esperado. |
| Confirmação | Olá estado de mensagem MDN <br>Aceite = recebidos ou enviados um MDN positivo. <br>Pendente = a aguardar tooreceive ou enviar um MDN. <br>Rejeitado = recebidos ou enviados um MDN negativo. <br>Não é necessária = MDN não está definido no contrato de Olá. |
| Direção | Olá direção da mensagem AS2 |
| ID de correlação | ID de Olá está correlacionada com todos os acionadores de Olá e ações numa aplicação lógica |
| ID da mensagem | ID de mensagem de Olá AS2 de cabeçalhos de mensagens hello AS2 |
| Timestamp | tempo de Olá quando Olá AS2 ação processar a mensagem de saudação |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>Formatos de nome de AS2 para ficheiros de mensagens transferido

Seguem-se formatos de nome de Olá para cada pasta de mensagem AS2 transferida e ficheiros.

| Ficheiro ou pasta | Formato de nome |
| :------------- | :---------- |
| Pasta de mensagem | [remetente] \_[recetor]\_AS2\_[ID de correlação]\_[ID de mensagem]\_[timestamp] |
| Entrada, saída e se configurar os ficheiros de confirmação | **Payload de entrada**: [remetente]\_[recetor]\_AS2\_[ID de correlação]\_input_payload.txt </p>**Payload de saída**: [remetente]\_[recetor]\_AS2\_[ID de correlação]\_saída\_payload.txt </p></p>**Entradas**: [remetente]\_[recetor]\_AS2\_[ID de correlação]\_inputs.txt </p></p>**Saídas**: [remetente]\_[recetor]\_AS2\_[ID de correlação]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>Descrições das propriedades da mensagem X12

Seguem-se descrições de propriedade Olá para cada X12 mensagem.

| Propriedade | Descrição |
| --- | --- |
| Remetente | parceiro de convidado de Olá especificado no **receber definições**, ou o parceiro de anfitrião Olá especificados em **enviar definições** para um X12 contrato |
| Recetor | parceiro de anfitrião de Olá especificado no **receber definições**, ou o parceiro de convidado de Olá especificado no **enviar definições** para um X12 contrato |
| Aplicação Lógica | aplicação de lógica de olá onde as ações de Olá X12 estão configuradas |
| Estado | Estado de mensagem de Olá X12 <br>Êxito = recebidos ou enviados um X12 válido mensagem. Nenhum ack funcional está definida. <br>Êxito = recebidos ou enviados um X12 válido mensagem. Ack funcional está configurado e recebido ou uma confirmação funcional é enviada. <br>Não foi possível = recebidos ou enviados um X12 inválido mensagem. <br>Pendente = recebidos ou enviados um X12 válido mensagem. Configurar a confirmação funcional e prevê-se uma confirmação funcional. |
| Confirmação | Estado de confirmação (997) funcional <br>Aceite = recebidos ou enviados uma confirmação funcional positivo <br>Rejeitado = recebidos ou enviados uma confirmação negativa de funcional <br>Pendente = era esperado um ack funcional, mas não foi recebido. <br>Pendente = gerou uma confirmação funcional, mas não é possível enviar toopartner. <br>Não é necessária = funcional ack não está configurado. |
| Direção | direção de mensagem de Olá X12 |
| ID de correlação | ID de Olá está correlacionada com todos os acionadores de Olá e ações numa aplicação lógica |
| Tipo de tarifas de mensagens | Olá, tipo de mensagem 12 EDI X |
| ICN | Olá intercâmbio número de controlo de mensagem de saudação X12 |
| TSCN | Olá transação definida controlo número para a mensagem de saudação X12 |
| Timestamp | tempo de Olá ao processar mensagem de saudação a ação de Olá X12 |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>Formatos de nome de X12 para ficheiros de mensagens transferido

Seguem-se formatos de nome de Olá para cada transferido X12 pastas e ficheiros de mensagens.

| Ficheiro ou pasta | Formato de nome |
| :------------- | :---------- |
| Pasta de mensagem | [remetente] \_[recetor]\_X12\_[número de controlo de intercâmbio]\_[global-controlo-número]\_[transação-set-controlo-número]\_[timestamp] |
| Entrada, saída e se configurar os ficheiros de confirmação | **Payload de entrada**: [remetente]\_[recetor]\_X12\_[número de controlo de intercâmbio]\_input_payload.txt </p>**Payload de saída**: [remetente]\_[recetor]\_X12\_[número de controlo de intercâmbio]\_saída\_payload.txt </p></p>**Entradas**: [remetente]\_[recetor]\_X12\_[número de controlo de intercâmbio]\_inputs.txt </p></p>**Saídas**: [remetente]\_[recetor]\_X12\_[número de controlo de intercâmbio]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>Descrições de propriedade de mensagem EDIFACT

Seguem-se descrições de propriedade Olá para cada mensagem EDIFACT.

| Propriedade | Descrição |
| --- | --- |
| Remetente | parceiro de convidado de Olá especificado no **receber definições**, ou o parceiro de anfitrião Olá especificados em **enviar definições** para um contrato de EDIFACT |
| Recetor | parceiro de anfitrião de Olá especificado no **receber definições**, ou o parceiro de convidado Olá especificados em **enviar definições** para um contrato de EDIFACT |
| Aplicação Lógica | aplicação de lógica de olá onde as ações de EDIFACT Olá estão configuradas |
| Estado | Olá estado de mensagem EDIFACT <br>Êxito = recebidos ou enviados uma mensagem EDIFACT válida. Nenhum ack funcional está definida. <br>Êxito = recebidos ou enviados uma mensagem EDIFACT válida. Ack funcional está configurado e recebido ou uma confirmação funcional é enviada. <br>Não foi possível = recebidos ou enviados uma mensagem EDIFACT inválida <br>Pendente = recebidos ou enviados uma mensagem EDIFACT válida. Configurar a confirmação funcional e prevê-se uma confirmação funcional. |
| Confirmação | Estado de confirmação (997) funcional <br>Aceite = recebidos ou enviados uma confirmação funcional positivo <br>Rejeitado = recebidos ou enviados uma confirmação negativa de funcional <br>Pendente = era esperado um ack funcional, mas não foi recebido. <br>Pendente = gerou uma confirmação funcional, mas não é possível enviar toopartner. <br>Não é necessária = Ack funcional não está configurado. |
| Direção | Olá direção da mensagem EDIFACT |
| ID de correlação | ID de Olá está correlacionada com todos os acionadores de Olá e ações numa aplicação lógica |
| Tipo de tarifas de mensagens | Olá, tipo de mensagem EDIFACT |
| ICN | Olá intercâmbio número de controlo de mensagem EDIFACT Olá |
| TSCN | Olá transação definida controlo número de mensagem EDIFACT Olá |
| Timestamp | tempo de Olá quando Olá ação EDIFACT processar a mensagem de saudação |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>Formatos de nome EDIFACT para ficheiros de mensagens transferido

Seguem-se formatos de nome de Olá para cada pasta de mensagem EDIFACT transferida e ficheiros.

| Ficheiro ou pasta | Formato de nome |
| :------------- | :---------- |
| Pasta de mensagem | [remetente] \_[recetor]\_EDIFACT\_[número de controlo de intercâmbio]\_[global-controlo-número]\_[transação-set-controlo-número]\_[timestamp] |
| Entrada, saída e se configurar os ficheiros de confirmação | **Payload de entrada**: [remetente]\_[recetor]\_EDIFACT\_[número de controlo de intercâmbio]\_input_payload.txt </p>**Payload de saída**: [remetente]\_[recetor]\_EDIFACT\_[número de controlo de intercâmbio]\_saída\_payload.txt </p></p>**Entradas**: [remetente]\_[recetor]\_EDIFACT\_[número de controlo de intercâmbio]\_inputs.txt </p></p>**Saídas**: [remetente]\_[recetor]\_EDIFACT\_[número de controlo de intercâmbio]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>Passos seguintes

* [Consulta para mensagens B2B no Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [Esquemas de controlo de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Esquemas de controlo de X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Esquemas de controlo personalizado](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)