---
title: aaaHow toouse Cache de Redis do Azure com o Node.js | Microsoft Docs
description: "Introdução à Cache de Redis do Azure com o Node.js e o node_redis."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Como toouse Azure Redis Cache com o Node.js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [python](cache-python-get-started.md)
> 
> 

Oferece de Cache de Redis do Azure aceder tooa segura, dedicada cache de Redis e gerida pela Microsoft. Pode aceder a uma cache a partir de qualquer aplicação dentro do Microsoft Azure.

Este tópico mostra como tooget à Cache de Redis do Azure com o Node.js. Para obter outro exemplo de utilização da Cache de Redis do Azure com o Node.js, veja [Build a Node.js Chat Application with Socket.IO on an Azure Website (Criar uma Aplicação de Chat do Node.js com Socket.IO num Site do Azure)](../app-service-web/web-sites-nodejs-chat-app-socketio.md).

## <a name="prerequisites"></a>Pré-requisitos
Instale o [node_redis](https://github.com/mranney/node_redis):

    npm install redis

Este tutorial utiliza o [node_redis](https://github.com/mranney/node_redis). Para obter exemplos de utilização de outros clientes de Node.js, consulte a documentação individual de Olá para clientes de Node.js Olá listados em [clientes de Redis do Node.js](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Criar uma cache de Redis no Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Obter chaves de acesso e o nome do anfitrião de Olá
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Ligar a cache de toohello em segurança com SSL
Olá baseia-se mais recente do [node_redis](https://github.com/mranney/node_redis) fornece suporte para ligar tooAzure a Cache de Redis através de SSL. Olá seguinte exemplo mostra como utilizar o tooconnect tooAzure a Cache de Redis Olá SSL ponto final de 6380. Substitua `<name>` com o nome de Olá da cache e `<key>` com a sua chave primária ou secundária conforme descrito em Olá anterior [obter chaves de acesso e o nome do anfitrião de Olá](#retrieve-the-host-name-and-access-keys) secção.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> porta do Olá não SSL está desativada para novas instâncias de Cache de Redis do Azure. Se estiver a utilizar um cliente diferente que não suporta SSL, consulte o artigo [como tooenable Olá porta não SSL](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Adicionar algo toohello colocar em cache e recuperá-lo
Olá seguinte exemplo mostra que como tooconnect tooan Azure Redis Cache instância e armazenar e obter um item da cache de Olá. Para obter mais exemplos de utilização de Redis com Olá [node_redis](https://github.com/mranney/node_redis) cliente, consulte [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Saída:

    OK
    value


## <a name="next-steps"></a>Passos seguintes
* [Ativar o diagnóstico da cache](cache-how-to-monitor.md#enable-cache-diagnostics) para poder [monitor](cache-how-to-monitor.md) Olá estado de funcionamento da cache.
* Leitura Olá oficial [documentação Redis](http://redis.io/documentation).

