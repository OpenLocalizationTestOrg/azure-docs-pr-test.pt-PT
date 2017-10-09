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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="30413-103">Como toouse Azure Redis Cache com o Node.js</span><span class="sxs-lookup"><span data-stu-id="30413-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="30413-104">.NET</span><span class="sxs-lookup"><span data-stu-id="30413-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="30413-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="30413-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="30413-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="30413-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="30413-107">Java</span><span class="sxs-lookup"><span data-stu-id="30413-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="30413-108">python</span><span class="sxs-lookup"><span data-stu-id="30413-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="30413-109">Oferece de Cache de Redis do Azure aceder tooa segura, dedicada cache de Redis e gerida pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="30413-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="30413-110">Pode aceder a uma cache a partir de qualquer aplicação dentro do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="30413-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="30413-111">Este tópico mostra como tooget à Cache de Redis do Azure com o Node.js.</span><span class="sxs-lookup"><span data-stu-id="30413-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="30413-112">Para obter outro exemplo de utilização da Cache de Redis do Azure com o Node.js, veja [Build a Node.js Chat Application with Socket.IO on an Azure Website (Criar uma Aplicação de Chat do Node.js com Socket.IO num Site do Azure)](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="30413-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30413-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="30413-113">Prerequisites</span></span>
<span data-ttu-id="30413-114">Instale o [node_redis](https://github.com/mranney/node_redis):</span><span class="sxs-lookup"><span data-stu-id="30413-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="30413-115">Este tutorial utiliza o [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="30413-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="30413-116">Para obter exemplos de utilização de outros clientes de Node.js, consulte a documentação individual de Olá para clientes de Node.js Olá listados em [clientes de Redis do Node.js](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="30413-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="30413-117">Criar uma cache de Redis no Azure</span><span class="sxs-lookup"><span data-stu-id="30413-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="30413-118">Obter chaves de acesso e o nome do anfitrião de Olá</span><span class="sxs-lookup"><span data-stu-id="30413-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="30413-119">Ligar a cache de toohello em segurança com SSL</span><span class="sxs-lookup"><span data-stu-id="30413-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="30413-120">Olá baseia-se mais recente do [node_redis](https://github.com/mranney/node_redis) fornece suporte para ligar tooAzure a Cache de Redis através de SSL.</span><span class="sxs-lookup"><span data-stu-id="30413-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="30413-121">Olá seguinte exemplo mostra como utilizar o tooconnect tooAzure a Cache de Redis Olá SSL ponto final de 6380.</span><span class="sxs-lookup"><span data-stu-id="30413-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="30413-122">Substitua `<name>` com o nome de Olá da cache e `<key>` com a sua chave primária ou secundária conforme descrito em Olá anterior [obter chaves de acesso e o nome do anfitrião de Olá](#retrieve-the-host-name-and-access-keys) secção.</span><span class="sxs-lookup"><span data-stu-id="30413-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="30413-123">porta do Olá não SSL está desativada para novas instâncias de Cache de Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="30413-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="30413-124">Se estiver a utilizar um cliente diferente que não suporta SSL, consulte o artigo [como tooenable Olá porta não SSL](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="30413-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="30413-125">Adicionar algo toohello colocar em cache e recuperá-lo</span><span class="sxs-lookup"><span data-stu-id="30413-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="30413-126">Olá seguinte exemplo mostra que como tooconnect tooan Azure Redis Cache instância e armazenar e obter um item da cache de Olá.</span><span class="sxs-lookup"><span data-stu-id="30413-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="30413-127">Para obter mais exemplos de utilização de Redis com Olá [node_redis](https://github.com/mranney/node_redis) cliente, consulte [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="30413-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="30413-128">Saída:</span><span class="sxs-lookup"><span data-stu-id="30413-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="30413-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="30413-129">Next steps</span></span>
* <span data-ttu-id="30413-130">[Ativar o diagnóstico da cache](cache-how-to-monitor.md#enable-cache-diagnostics) para poder [monitor](cache-how-to-monitor.md) Olá estado de funcionamento da cache.</span><span class="sxs-lookup"><span data-stu-id="30413-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="30413-131">Leitura Olá oficial [documentação Redis](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="30413-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

