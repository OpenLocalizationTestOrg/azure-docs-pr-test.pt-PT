---
title: sistemas de Azure Logic Apps de ficheiros do local com o aaaConnect tooon | Microsoft Docs
description: "Ligar sistemas de ficheiros tooon local a partir do seu fluxo de trabalho de aplicação lógica através do gateway de dados do Olá no local e conector sistema de ficheiros"
keywords: sistemas de ficheiros
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Ligar sistemas de ficheiros tooon local a partir das logic apps com o conector sistema de ficheiros de Olá

Conectividade de cloud híbrida é aplicações central toologic, os dados de toomanage Sim e em segurança acesso recursos no local, as logic apps podem utilizar o gateway de dados do Olá no local. Neste artigo, mostramos como tooconnect tooan no local o sistema de ficheiros com um cenário básico: copiar um ficheiro tooa de tooDropbox carregado da partilha de ficheiros, em seguida, envie um e-mail.

## <a name="prerequisites"></a>Pré-requisitos

- Instalar e configurar mais recente Olá [gateway de dados no local](https://www.microsoft.com/download/details.aspx?id=53127).
- Instalar o gateway de dados de no local mais recente do Olá, versão 1.15.6150.1 ou superior. [Ligar o gateway de dados no local toohello](http://aka.ms/logicapps-gateway) listas Olá passos. gateway de Olá tem de ser instalado numa máquina no local antes de poder continuar com o resto Olá passos Olá.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>Adicionar acionadores e ações para estabelecer a ligação de sistema de ficheiros tooyour

1. Criar uma aplicação lógica e adicione este acionador Dropbox: **quando é criado um ficheiro** 
2. Em acionador Olá, escolha **passo seguinte** > **adicionar uma ação**. 
3. Na caixa de pesquisa de Olá, introduza `file system` para que possa vê ações todos suportadas para o conector sistema de ficheiros de Olá.

   ![Pesquisa para o conector do ficheiro](media/logic-apps-using-file-connector/search-file-connector.png)

2. Escolha Olá **criar ficheiro** ação e criar um sistema de ficheiros de tooyour de ligação.

   Se não tiver uma ligação existente, é pedido toocreate um.

   1. Escolha **ligar através do gateway de dados no local**. Propriedades são apresentados.
   2. Selecione a pasta de raiz para o seu sistema de ficheiros.
      
       > [!NOTE]
       > pasta de raiz de Olá é a pasta de principal de principais de Olá, que é utilizada para caminhos relativos para todas as ações relacionadas com o ficheiro. Pode especificar uma pasta local na máquina de olá onde está instalado o gateway de dados no local Olá ou pasta Olá pode ser uma partilha de rede que Olá máquina pode aceder.

   3. Introduza Olá nome de utilizador e palavra-passe para o gateway de Olá.
   4. Selecione o gateway de Olá que instalou anteriormente.

       ![Configurar a ligação](media/logic-apps-using-file-connector/create-file.png)

3. Depois de fornecer todos os detalhes de Olá, escolha **criar**. 

   As Logic Apps configura e testa a ligação, certificando-se de que a ligação de Olá funciona corretamente. 
   Se a ligação de Olá está configurado corretamente, consulte as opções para a ação de Olá que selecionou anteriormente. 
   conector de sistema de ficheiros de Olá está agora pronto para ser utilizado.

4. Especifique que pretende que toocopy ficheiros da pasta de raiz de toohello Dropbox para a partilha de ficheiros no local.

   ![Criar a ação de ficheiros](media/logic-apps-using-file-connector/create-file-filled.png)

5. Após a sua lógica cópias Olá de aplicativo, adicione uma ação do Outlook que envia uma mensagem de e-mail para que utilizadores relevantes saber sobre o novo ficheiro de Olá. Introduza destinatários Olá, o título e o corpo da mensagem de e-mail Olá. 

   No Seletor de conteúdo dinâmico de Olá, pode escolher saídas de dados do conector de ficheiro Olá, para poder adicionar o e-mail de toohello mais detalhes.

   ![Enviar correio eletrónico ação](media/logic-apps-using-file-connector/send-email.png)

6. Guarde a sua aplicação lógica. Teste a aplicação através do carregamento tooDropbox um ficheiro. ficheiro de Olá deve obter a partilha de ficheiros copiados toohello no local e deverá receber uma mensagem de e-mail sobre a operação de Olá.

   > [!TIP] 
   > Saiba como demasiado[monitorizar as logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Parabéns, tem agora uma aplicação de lógica de trabalho que pode ligar-se o sistema de ficheiros tooyour no local. Tente explorar outras funcionalidades que Olá ofertas de conector, por exemplo:

- Criar o ficheiro
- Lista de ficheiros na pasta
- Anexar ficheiro
- Eliminar ficheiro
- Obter o conteúdo do ficheiro
- Obter o conteúdo do ficheiro com o caminho
- Obter metadados do ficheiro
- Obter os metadados de ficheiro com o caminho
- Lista de ficheiros na pasta raiz
- Ficheiro de atualização

## <a name="view-hello-swagger"></a>Swagger Olá de vista
Consulte Olá [swagger detalhes](/connectors/fileconnector/). 

## <a name="get-help"></a>Obter ajuda

perguntas tooask, responda às perguntas e saiba que outras Azure Logic Apps os utilizadores estão a fazer, visite Olá [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp melhorar Azure Logic Apps e conectores, votar em ou submeter ideias em Olá [site de comentários do utilizador do Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passos seguintes

- [Ligar a dados local tooon](../logic-apps/logic-apps-gateway-connection.md) partir das logic apps
- Saiba mais sobre [integração empresarial com o](../logic-apps/logic-apps-enterprise-integration-overview.md)
