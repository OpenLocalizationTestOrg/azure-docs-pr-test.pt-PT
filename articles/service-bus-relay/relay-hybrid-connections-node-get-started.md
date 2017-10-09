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
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="5c9e2-103">Introdução às Ligações Híbridas de Reencaminhamento</span><span class="sxs-lookup"><span data-stu-id="5c9e2-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="5c9e2-104">Este tutorial fornece uma introdução demasiado[Azure reencaminhamento híbrido ligações](relay-what-is-it.md#hybrid-connections)e mostra como toouse Node.js toocreate uma aplicação cliente que envia mensagens tooa aplicação de serviço de escuta correspondente.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="5c9e2-105">O que será efetuado</span><span class="sxs-lookup"><span data-stu-id="5c9e2-105">What will be accomplished</span></span>

<span data-ttu-id="5c9e2-106">Uma vez que as Ligações Híbridas necessitam de um cliente e um componente de servidor, iremos criar duas aplicações de consola neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="5c9e2-107">Eis os passos de Olá:</span><span class="sxs-lookup"><span data-stu-id="5c9e2-107">Here are hello steps:</span></span>

1. <span data-ttu-id="5c9e2-108">Crie um espaço de nomes de reencaminhamento, utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="5c9e2-109">Crie uma ligação híbrida, utilizando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="5c9e2-110">Escreva um servidor de mensagens de tooreceive da aplicação de consola.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="5c9e2-111">Escreva um cliente mensagens de toosend da aplicação de consola.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c9e2-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c9e2-112">Prerequisites</span></span>

1. <span data-ttu-id="5c9e2-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="5c9e2-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="5c9e2-114">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="5c9e2-115">1. Criar um espaço de nomes utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5c9e2-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="5c9e2-116">Se já tiver um espaço de nomes de reencaminhamento criado, avance toohello [criar uma ligação híbrida utilizando o portal do Azure de Olá](#2-create-a-hybrid-connection-using-the-azure-portal) secção.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="5c9e2-117">2. Criar uma ligação híbrida utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5c9e2-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="5c9e2-118">Se já tiver uma ligação híbrida criada, avance toohello [criar uma aplicação de servidor](#3-create-a-server-application-listener) secção.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="5c9e2-119">3. Criar uma aplicação de servidor (serviço de escuta)</span><span class="sxs-lookup"><span data-stu-id="5c9e2-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="5c9e2-120">toolisten e receber mensagens de Olá reencaminhamento, iremos escrever uma aplicação de consola do Node.js.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="5c9e2-121">4. Criar uma aplicação cliente (remetente)</span><span class="sxs-lookup"><span data-stu-id="5c9e2-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="5c9e2-122">toosend mensagens toohello reencaminhamento, iremos escrever uma aplicação de consola do Node.js.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="5c9e2-123">5. Executar aplicações de Olá</span><span class="sxs-lookup"><span data-stu-id="5c9e2-123">5. Run hello applications</span></span>

1. <span data-ttu-id="5c9e2-124">Executar a aplicação de servidor Olá: de um tipo de linha de comandos Node.js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="5c9e2-125">Executar a aplicação de cliente Olá: de um tipo de linha de comandos Node.js `node sender.js`e introduza algum texto.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="5c9e2-126">Certifique-se de que o servidor Olá texto Olá de saídas de consola de aplicação que foi introduzido na aplicação de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="5c9e2-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="5c9e2-128">Parabéns, criou uma aplicação de Ligações Híbridas ponto a ponto com o Node.js!</span><span class="sxs-lookup"><span data-stu-id="5c9e2-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c9e2-129">Passos seguintes:</span><span class="sxs-lookup"><span data-stu-id="5c9e2-129">Next steps:</span></span>

* [<span data-ttu-id="5c9e2-130">FAQ de Reencaminhamento</span><span class="sxs-lookup"><span data-stu-id="5c9e2-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="5c9e2-131">Criar um espaço de nomes</span><span class="sxs-lookup"><span data-stu-id="5c9e2-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="5c9e2-132">Introdução ao .NET</span><span class="sxs-lookup"><span data-stu-id="5c9e2-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="5c9e2-133">Introdução ao Node</span><span class="sxs-lookup"><span data-stu-id="5c9e2-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

