---
title: "aaaGet começar a utilizar ligações híbridas de reencaminhamento de Azure no nó | Microsoft Docs"
description: "Escreva uma aplicação de consola Node.js para Ligações Híbridas de Reencaminhamento do Azure."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Introdução às Ligações Híbridas de Reencaminhamento

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Este tutorial fornece uma introdução demasiado[Azure reencaminhamento híbrido ligações](relay-what-is-it.md#hybrid-connections)e mostra como toouse Node.js toocreate uma aplicação cliente que envia mensagens tooa aplicação de serviço de escuta correspondente. 

## <a name="what-will-be-accomplished"></a>O que será efetuado

Uma vez que as Ligações Híbridas necessitam de um cliente e um componente de servidor, iremos criar duas aplicações de consola neste tutorial. Eis os passos de Olá:

1. Crie um espaço de nomes de reencaminhamento, utilizando Olá portal do Azure.
2. Crie uma ligação híbrida, utilizando Olá portal do Azure.
3. Escreva um servidor de mensagens de tooreceive da aplicação de consola.
4. Escreva um cliente mensagens de toosend da aplicação de consola.

## <a name="prerequisites"></a>Pré-requisitos

1. [Node.js](https://nodejs.org/en/).
2. Uma subscrição do Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Criar um espaço de nomes utilizando Olá portal do Azure

Se já tiver um espaço de nomes de reencaminhamento criado, avance toohello [criar uma ligação híbrida utilizando o portal do Azure de Olá](#2-create-a-hybrid-connection-using-the-azure-portal) secção.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Criar uma ligação híbrida utilizando Olá portal do Azure

Se já tiver uma ligação híbrida criada, avance toohello [criar uma aplicação de servidor](#3-create-a-server-application-listener) secção.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Criar uma aplicação de servidor (serviço de escuta)

toolisten e receber mensagens de Olá reencaminhamento, iremos escrever uma aplicação de consola do Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Criar uma aplicação cliente (remetente)

toosend mensagens toohello reencaminhamento, iremos escrever uma aplicação de consola do Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Executar aplicações de Olá

1. Executar a aplicação de servidor Olá: de um tipo de linha de comandos Node.js `node listener.js`.
2. Executar a aplicação de cliente Olá: de um tipo de linha de comandos Node.js `node sender.js`e introduza algum texto.
3. Certifique-se de que o servidor Olá texto Olá de saídas de consola de aplicação que foi introduzido na aplicação de cliente Olá.

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Parabéns, criou uma aplicação de Ligações Híbridas ponto a ponto com o Node.js!

## <a name="next-steps"></a>Passos seguintes:

* [FAQ de Reencaminhamento](relay-faq.md)
* [Criar um espaço de nomes](relay-create-namespace-portal.md)
* [Introdução ao .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introdução ao Node](relay-hybrid-connections-node-get-started.md)

