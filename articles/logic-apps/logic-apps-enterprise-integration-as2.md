---
title: "aaaAS2 mensagens para a integração do enterprise B2B - Azure Logic Apps | Microsoft Docs"
description: "Trocar mensagens AS2 para a integração do enterprise B2B com Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>Trocar mensagens AS2 para a integração empresarial com logic apps

Podem trocar mensagens AS2 para Azure Logic Apps, tem de criar um contrato de AS2 e armazenar esse contrato na sua conta de integração. Seguem-se passos de Olá como contrato toocreate um AS2.

## <a name="before-you-start"></a>Antes de começar

Segue-se itens Olá que precisa de:

* Um [conta integração](../logic-apps/logic-apps-enterprise-integration-accounts.md) que já foi definida e associados à subscrição do Azure
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já estão definidos na sua conta de integração e configurado com qualificador Olá AS2 em **identidades de negócio**

> [!NOTE]
> Quando cria um contrato, conteúdo de Olá no ficheiro de contrato de Olá tem de corresponder ao tipo de contrato de Olá.    

Depois de [criar uma conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md) e [adicionar parceiros](logic-apps-enterprise-integration-partners.md), pode criar um contrato de AS2, seguindo estes passos.

## <a name="create-an-as2-agreement"></a>Crie um contrato de AS2

1.  Inicie sessão no toohello [portal do Azure](http://portal.azure.com "portal do Azure").  

2.  No menu à esquerda de Olá, selecione **mais serviços**. Na caixa de pesquisa de Olá, introduza **integração** como o filtro. Na lista de resultados de Olá, selecione **contas de automatização**.

    > [!TIP]
    > Se não vir **mais serviços**, poderá ter o menu de Olá tooexpand primeiro. Olá parte superior do menu de Olá fechado, selecione **Mostrar menu**.

    ![Mais serviços, o filtro "integração", selecione "Contas de automatização"](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. No Olá **contas de automatização** painel que abre, conta de integração de Olá selecione onde pretende que o contrato de Olá toocreate.
Se não vir quaisquer contas de automatização, [criar um primeiro](../logic-apps/logic-apps-enterprise-integration-accounts.md "tudo sobre contas de automatização").  

    ![Selecione a conta de integração de olá onde toocreate Olá contrato](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Escolha Olá **contratos** mosaico. Se não tiver um mosaico de contratos, adicione primeiro mosaico Olá.

    ![Escolha o que mosaico "Contratos"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. No painel de contratos de Olá que se abre, escolha **adicionar**.

    ![Escolha "Adicionar"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. Em **adicionar**, introduza um **nome** para o contrato. Para **tipo de contrato**, selecione **AS2**. Selecione Olá **anfitrião parceiro**, **identidade do anfitrião**, **convidado parceiro**, e **identidade de convidado** para o contrato.

    ![Forneça os detalhes do contrato](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | Propriedade | Descrição |
    | --- | --- |
    | Nome |Nome do contrato de Olá |
    | Tipo de contrato | Deve ser AS2 |
    | Parceiro de anfitrião |Um contrato tem de parceiro de um anfitrião e convidado. parceiro de anfitrião Olá representa a organização Olá que configura o contrato de Olá. |
    | Identidade do anfitrião |Um identificador de parceiro de anfitrião Olá |
    | Parceiro de convidado |Um contrato tem de parceiro de um anfitrião e convidado. parceiro de convidado Olá representa a organização Olá que está a decorrer empresas com o parceiro de anfitrião Olá. |
    | Identidade de convidado |Um identificador de parceiro de convidado Olá |
    | Receber definições |Estas propriedades aplicam-se as mensagens de tooall recebidas por um contrato. |
    | Enviar definições |Estas propriedades aplicam-se as mensagens de tooall enviadas por um contrato. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configurar a forma como os identificadores de contrato receberam mensagens

Agora que definiu as propriedades de contrato de Olá, pode configurar como o presente contrato identifica e processa mensagens a receber foi recebidas pelo seu parceiro através deste contrato.

1.  Em **adicionar**, selecione **receber definições**.
Configure estas propriedades com base no seu contrato com o parceiro de Olá trocas de mensagens consigo. Para descrições das propriedades, consulte a tabela de Olá nesta secção.

    ![Configurar "Receber definições"](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. Opcionalmente, pode substituir as propriedades de Olá de mensagens a receber selecionando **substituir as propriedades da mensagem**.

3. toorequire todos os toobe mensagens recebidas assinado, selecione **mensagem deve estar assinada**. De Olá **certificado** lista, selecione um existente [certificado público de parceiro de convidado](../logic-apps/logic-apps-enterprise-integration-certificates.md) para validar a assinatura de Olá nas mensagens hello. Ou criar o certificado de Olá, se não tiver uma.

4.  Selecione de todas as mensagens toobe de entrada encriptados, toorequire **mensagem deve ser encriptada**. De Olá **certificado** lista, selecione um existente [certificado privado de parceiro de anfitrião](../logic-apps/logic-apps-enterprise-integration-certificates.md) para desencriptar mensagens a receber. Ou criar o certificado de Olá, se não tiver uma.

5. Selecione toorequire mensagens toobe comprimido, **mensagem deve ser comprimida**.

6. Selecione toosend uma notificação de disposição mensagem síncrona (MDN) para mensagens recebidas, **enviar MDN**.

7. toosend inscreveu MDNs mensagens recebidas, selecionadas **Send iniciada MDN**.

8. toosend MDNs assíncronas para mensagens recebidas, selecione **enviar MDN assíncrona**.

9. Depois de terminar, certifique-se toosave as suas definições escolhendo **OK**.

Agora, o contrato é toohandle pronto receber mensagens que estão em conformidade com tooyour nas definições selecionadas.

| Propriedade | Descrição |
| --- | --- |
| Substituir as propriedades da mensagem |Indica se as propriedades de mensagens recebidas podem ser substituídas. |
| Mensagem deve estar assinada |Requer toobe mensagens assinado digitalmente. Configure o certificado público do parceiro de convidado de Olá para verificação da assinatura.  |
| Mensagem deve ser encriptada |Requer toobe mensagens encriptada. Mensagens encriptadas não são rejeitadas. Para configurar Olá anfitrião parceiro privada para desencriptar mensagens hello.  |
| Mensagem deve ser comprimida |Requer toobe mensagens comprimido. Mensagens de compressão não são rejeitadas. |
| Texto MDN |Olá predefinido disposição notificação (MDN) toobe toohello enviado mensagem remetente da mensagem. |
| Enviar MDN |Requer toobe MDNs enviada. |
| Enviar MDN assinado |Requer toobe MDNs assinado. |
| Algoritmo de Dinâmicas |Selecione Olá toouse de algoritmo de assinatura de mensagens. |
| Enviar MDN assíncrona | Requer toobe de mensagens enviada de forma assíncrona. |
| URL | Especifique o URL de olá onde toosend Olá MDNs. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configurar como o seu contrato envia mensagens

Pode configurar a forma como este contrato identifica e processa mensagens de saída que enviam tooyour parceiros através deste contrato.

1.  Em **adicionar**, selecione **enviar definições**.
Configure estas propriedades com base no seu contrato com o parceiro de Olá trocas de mensagens consigo. Para descrições das propriedades, consulte a tabela de Olá nesta secção.

    ![Definir as propriedades de "Definições de envio" Olá](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend mensagens assinado tooyour parceiro, selecione **ativar a assinatura das mensagens**. Para assinar mensagens hello, no Olá **MIC algoritmo** lista, selecione de Olá *anfitrião parceiro privada no certificado MIC algoritmo*. E no Olá **certificado** lista, selecione um existente [certificado privado de parceiro de anfitrião](../logic-apps/logic-apps-enterprise-integration-certificates.md).

3. toosend mensagens encriptadas toohello parceiro, selecione **ativar a encriptação de mensagens**. Para encriptar mensagens hello, no Olá **algoritmo de encriptação** lista, selecione de Olá *algoritmos de certificado público de parceiro de convidado*.
E no Olá **certificado** lista, selecione um existente [certificado público de parceiro de convidado](../logic-apps/logic-apps-enterprise-integration-certificates.md).

4. mensagem de saudação toocompress, selecione **ativar a compressão de mensagem**.

5. cabeçalho de tipo de conteúdo de Olá HTTP toounfold numa única linha, selecione **cabeçalhos de Unfold HTTP**.

6. tooreceive MDNs síncronas para Olá enviadas mensagens, selecionadas **pedido MDN**.

7. tooreceive assinado MDNs mensagens hello enviado, selecionadas de **pedido assinado MDN**.

8. tooreceive MDNs assíncronas para Olá enviadas mensagens, selecionadas **pedido assíncrono MDN**. Se selecionar esta opção, introduza o URL de Olá para onde toosend Olá MDNs.

9. não toorequire rejeição de receção, selecione **ativar NRR**.  

10. toospecify algoritmo formato toouse no Olá MIC ou iniciar sessão Olá enviados os cabeçalhos de mensagem de saudação AS2 ou MDN, selecione **formato SHA2 algoritmo**.  

11. Depois de terminar, certifique-se toosave as suas definições escolhendo **OK**.

O contrato está agora pronto toohandle de envio de mensagens que estão em conformidade com as definições de tooyour selecionado.

| Propriedade | Descrição |
| --- | --- |
| Ativar a assinatura das mensagens |Requer que todas as mensagens que são enviadas pelo Olá contrato toobe assinado. |
| Algoritmo de Dinâmicas |Olá toouse de algoritmo de assinatura de mensagens. Configura o certificado privado do Olá anfitrião parceiro algoritmo Dinâmicas para assinar mensagens hello. |
| Certificado |Selecione Olá toouse de certificado para assinar mensagens. Configura Olá anfitrião parceiro privada certificado para assinar mensagens hello. |
| Ativar a encriptação de mensagens |Necessita de encriptação de todas as mensagens que são enviadas do presente contrato. Configura o algoritmo certificado público de parceiro de convidado do Olá para encriptar mensagens hello. |
| Algoritmo de encriptação |Olá toouse de algoritmo de encriptação para encriptação de mensagens. Configura o certificado público do parceiro de convidado de Olá para encriptar mensagens hello. |
| Certificado |mensagens Hello do certificado toouse tooencrypt. Configura o certificado privado do parceiro de convidado de Olá para encriptar mensagens hello. |
| Ativar a compressão de mensagem |Necessita de compressão de todas as mensagens que são enviadas do presente contrato. |
| Unfold cabeçalhos de HTTP |Coloca o cabeçalho content-type HTTP de Olá numa única linha. |
| Pedido MDN |Requer um MDN para todas as mensagens que são enviadas do presente contrato. |
| Pedido assinado MDN |Requer que todos os MDNs que são enviados contrato toothis toobe assinado. |
| MDN assíncrona do pedido |Requer o contrato de toothis de toobe enviado MDNs assíncrono. |
| URL |Especifique o URL de olá onde toosend Olá MDNs. |
| Ativar NRR |Requer a não rejeição de receção (NRR), um atributo de comunicação que fornece provas dados Olá foi recebida como resolvido. |
| Formato de algoritmo de SHA2 |Selecione o algoritmo formato toouse num Olá MIC ou Olá cabeçalhos de mensagem de AS2 Olá ou MDN de envio de início de sessão |

## <a name="find-your-created-agreement"></a>Encontrar o contrato criado

1.  Depois de concluir a definição de todas as propriedades de contrato, em Olá **adicionar** painel, escolha **OK** toofinish criar o seu contrato e o painel de conta de integração de retorno tooyour.

    O contrato recém-adicionado agora aparece na sua **contratos** lista.

2.  Também pode ver os contratos na descrição geral da sua integração conta. No painel da conta de integração, escolha **descrição geral**, em seguida, selecione Olá **contratos** mosaico. 

    ![Escolha "Contratos" mosaico tooview todos os contratos](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Swagger Olá de vista
Consulte Olá [swagger detalhes](/connectors/as2/). 

## <a name="next-steps"></a>Passos seguintes
* [Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")  
