---
title: "aaaLearn como toouse Olá conector SFTP nas suas logic apps | Microsoft Docs"
description: "Crie aplicações lógicas com o App service do Azure. Ligue toosend tooSFTP API e receber ficheiros. Pode realizar várias operações, tais como criar, atualizar, obterem ou eliminar ficheiros."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Introdução ao conector do Olá SFTP
Utilize Olá SFTP conector tooaccess um SFTP conta toosend e receber ficheiros. Pode realizar várias operações, tais como criar, atualizar, obterem ou eliminar ficheiros.  

toouse [qualquer conector](apis-list.md), terá primeiro de toocreate uma aplicação lógica. Pode começar a utilizar pelo [criar uma aplicação lógica agora](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>Ligar tooSFTP
Antes da aplicação lógica pode aceder a qualquer serviço, terá primeiro de toocreate um *ligação* toohello serviço. A [ligação](connectors-overview.md) fornece conectividade entre uma aplicação lógica e outro serviço.  

### <a name="create-a-connection-toosftp"></a>Criar uma ligação tooSFTP
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Utilizar um acionador SFTP
Um acionador é um evento que pode ser o fluxo de trabalho do Olá toostart utilizados definido numa aplicação lógica. [Saiba mais sobre acionadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Neste exemplo, Olá **SFTP - quando um ficheiro é adicionado ou modificado** acionador é um fluxo de trabalho de aplicação de lógica de tooinitiate utilizado quando um ficheiro é adicionado ou modificado num servidor SFTP. Também adicionar uma condição que verifica a existência de conteúdo de Olá do ficheiro de novos ou modificados Olá e faz com que um ficheiro de Olá tooextract decisão se o seu conteúdo indicarem que deve ser extraído antes de utilizar conteúdo Olá. Por fim, adicionar uma ação tooextract Olá do conteúdo de um ficheiro e coloque o conteúdo de Olá extraído numa pasta no servidor SFTP Olá. 

Um exemplo de empresa, pode utilizar este toomonitor acionador uma pasta SFTP para novos ficheiros que representam as ordens de cliente.  Pode, em seguida, utilizar uma ação de conector SFTP, tais como **obter o conteúdo do ficheiro**, conteúdo de Olá tooget da ordem de Olá para armazenamento numa base de dados ordens e processamento adicional.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Adicionar uma condição
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Utilizar uma ação de SFTP
Uma ação é uma operação levada a cabo pelo fluxo de trabalho Olá definido numa aplicação lógica. [Saiba mais sobre as ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Mais conectores
Voltar atrás toohello [lista APIs](apis-list.md).
