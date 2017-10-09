---
title: aaaHow toouse Cache de Redis do Azure com o Python | Microsoft Docs
description: "Introdução à Cache de Redis do Azure com o Python"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a><span data-ttu-id="5e560-103">Como toouse Azure Redis Cache com o Python</span><span class="sxs-lookup"><span data-stu-id="5e560-103">How toouse Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e560-104">.NET</span><span class="sxs-lookup"><span data-stu-id="5e560-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="5e560-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5e560-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="5e560-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="5e560-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="5e560-107">Java</span><span class="sxs-lookup"><span data-stu-id="5e560-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="5e560-108">python</span><span class="sxs-lookup"><span data-stu-id="5e560-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="5e560-109">Este tópico mostra como tooget à Cache de Redis do Azure com o Python.</span><span class="sxs-lookup"><span data-stu-id="5e560-109">This topic shows you how tooget started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e560-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5e560-110">Prerequisites</span></span>
<span data-ttu-id="5e560-111">Instale o [redis-py](https://github.com/andymccurdy/redis-py).</span><span class="sxs-lookup"><span data-stu-id="5e560-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="5e560-112">Criar uma cache de Redis no Azure</span><span class="sxs-lookup"><span data-stu-id="5e560-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="5e560-113">Obter chaves de acesso e o nome do anfitrião de Olá</span><span class="sxs-lookup"><span data-stu-id="5e560-113">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a><span data-ttu-id="5e560-114">Ativar o ponto final não SSL de Olá</span><span class="sxs-lookup"><span data-stu-id="5e560-114">Enable hello non-SSL endpoint</span></span>
<span data-ttu-id="5e560-115">Alguns clientes Redis não suportam o SSL e por Olá predefinido [porta não SSL está desativada para novas instâncias de Cache de Redis do Azure](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="5e560-115">Some Redis clients don't support SSL, and by default hello [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="5e560-116">No momento de Olá desta redação, Olá [redis-py](https://github.com/andymccurdy/redis-py) cliente não suporta SSL.</span><span class="sxs-lookup"><span data-stu-id="5e560-116">At hello time of this writing, hello [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="5e560-117">Adicionar algo toohello colocar em cache e recuperá-lo</span><span class="sxs-lookup"><span data-stu-id="5e560-117">Add something toohello cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="5e560-118">Substitua `<name>` pelo nome da sua cache `key` e pela sua chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="5e560-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
