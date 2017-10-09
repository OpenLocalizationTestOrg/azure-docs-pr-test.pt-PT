---
title: "aaaOverview de Olá APIs de nó de reencaminhamento do Azure | Microsoft Docs"
description: "Descrição geral da API de nó de reencaminhamento"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="f9c45-103">Descrição geral da API de nó de ligações híbridas de reencaminhamento</span><span class="sxs-lookup"><span data-stu-id="f9c45-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="f9c45-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="f9c45-104">Overview</span></span>

<span data-ttu-id="f9c45-105">Olá [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pacote do nó para ligações de híbridas de reencaminhamento do Azure está incorporada no e expande Olá ['ws'](https://www.npmjs.com/package/ws) pacote NPM.</span><span class="sxs-lookup"><span data-stu-id="f9c45-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="f9c45-106">Este pacote novamente Exporta todas as exportações esse pacote base e adiciona novas exportações que ativar a integração com a funcionalidade de ligações híbridas de serviço de reencaminhamento do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="f9c45-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="f9c45-107">As aplicações existentes que `require('ws')` pode utilizar este pacote com `require('hyco-ws')` em vez disso, que também lhe permite cenários híbridos, em que uma aplicação pode escutar ligações de WebSocket localmente a partir do "no interior da firewall Olá" e através de ligações híbridas, todos num Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="f9c45-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="f9c45-108">Documentação</span><span class="sxs-lookup"><span data-stu-id="f9c45-108">Documentation</span></span>

<span data-ttu-id="f9c45-109">Olá as APIs são [documentados no pacote de principal 'ws' Olá](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="f9c45-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="f9c45-110">Este artigo descreve como este pacote difere de acordo com esse linha de base.</span><span class="sxs-lookup"><span data-stu-id="f9c45-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="f9c45-111">Olá principais diferenças entre o pacote de base de Olá e este 'hyco-ws' é que adiciona uma nova classe de servidor, exportada através de `require('hyco-ws').RelayedServer`e alguns métodos de programa auxiliar.</span><span class="sxs-lookup"><span data-stu-id="f9c45-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="f9c45-112">Métodos de programa auxiliar do pacote</span><span class="sxs-lookup"><span data-stu-id="f9c45-112">Package helper methods</span></span>

<span data-ttu-id="f9c45-113">Existem vários métodos de utilitário disponíveis na exportação do pacote de Olá que pode referenciar da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f9c45-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="f9c45-114">métodos de programa auxiliar de Olá são para utilização com este pacote, mas também podem ser utilizados por um servidor de nó para ativar a escuta de toocreate clientes web ou de dispositivo ou os remetentes.</span><span class="sxs-lookup"><span data-stu-id="f9c45-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="f9c45-115">servidor de Olá utiliza estes métodos, transferindo-os URIs incorpore tokens de curta duração.</span><span class="sxs-lookup"><span data-stu-id="f9c45-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="f9c45-116">Estes URIs também pode ser utilizado com comuns pilhas de WebSocket não suportam cabeçalhos HTTP de definição de handshake de WebSocket Olá.</span><span class="sxs-lookup"><span data-stu-id="f9c45-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="f9c45-117">Ao incorporar tokens de autorização para Olá que URI é suportado principalmente para os cenários de utilização da biblioteca externa.</span><span class="sxs-lookup"><span data-stu-id="f9c45-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="f9c45-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="f9c45-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="f9c45-119">Cria uma escuta de reencaminhamento do Azure da ligação híbrida URI válida para Olá fornecido espaço de nomes e o caminho.</span><span class="sxs-lookup"><span data-stu-id="f9c45-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="f9c45-120">Este URI, em seguida, pode ser utilizado com a versão de reencaminhamento de Olá do Olá WebSocketServer classe.</span><span class="sxs-lookup"><span data-stu-id="f9c45-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="f9c45-121">`namespaceName`(obrigatório) - Olá nome qualificado do domínio de toouse de espaço de nomes do Olá reencaminhamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c45-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="f9c45-122">`path`(obrigatório) - Olá o nome de uma ligação híbrida de reencaminhamento do Azure existente nesse espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="f9c45-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="f9c45-123">`token`(opcional) - um acesso de reencaminhamento emitido anteriormente token que está incorporada no URI do serviço de escuta do Olá (consulte o seguinte exemplo de Olá).</span><span class="sxs-lookup"><span data-stu-id="f9c45-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="f9c45-124">`id`(opcional) - um identificador de controlo que permite o controlo de ponto a ponto diagnósticos de pedidos.</span><span class="sxs-lookup"><span data-stu-id="f9c45-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="f9c45-125">Olá `token` valor é opcional e só deve ser utilizado quando não é possível toosend HTTP cabeçalhos, juntamente com o handshake de WebSocket Olá, como é Olá caso com pilha de W3C WebSocket Olá.</span><span class="sxs-lookup"><span data-stu-id="f9c45-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="f9c45-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="f9c45-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="f9c45-127">Cria um envio de reencaminhamento do Azure da ligação híbrida URI válido para Olá espaço de nome e caminho.</span><span class="sxs-lookup"><span data-stu-id="f9c45-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="f9c45-128">Este URI pode ser utilizado com qualquer cliente de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="f9c45-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="f9c45-129">`namespaceName`(obrigatório) - Olá nome qualificado do domínio de toouse de espaço de nomes do Olá reencaminhamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c45-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="f9c45-130">`path`(obrigatório) - Olá o nome de uma ligação híbrida de reencaminhamento do Azure existente nesse espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="f9c45-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="f9c45-131">`token`(opcional) - um token de acesso de reencaminhamento emitido anteriormente que está incorporado Olá enviar URI (consulte o seguinte exemplo de Olá).</span><span class="sxs-lookup"><span data-stu-id="f9c45-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="f9c45-132">`id`(opcional) - um identificador de controlo que permite o controlo de ponto a ponto diagnósticos de pedidos.</span><span class="sxs-lookup"><span data-stu-id="f9c45-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="f9c45-133">Olá `token` valor é opcional e só deve ser utilizado quando não é possível toosend HTTP cabeçalhos, juntamente com o handshake de WebSocket Olá, como é Olá caso com pilha de W3C WebSocket Olá.</span><span class="sxs-lookup"><span data-stu-id="f9c45-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="f9c45-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="f9c45-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="f9c45-135">Cria um token de assinatura de acesso partilhado do Azure reencaminhamento (SAS) para o URI de destino Olá fornecido, a regra SAS e a regra da chave SAS que é válida para Olá desde número de segundos ou para uma hora Olá atual instantânea se o argumento de expiração de Olá for omitido.</span><span class="sxs-lookup"><span data-stu-id="f9c45-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="f9c45-136">`uri`(obrigatório) - Olá URI para o qual Olá token é toobe emitido.</span><span class="sxs-lookup"><span data-stu-id="f9c45-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="f9c45-137">Olá URI é o esquema HTTP de Olá toouse normalizado e as informações da cadeia de consulta são eliminadas.</span><span class="sxs-lookup"><span data-stu-id="f9c45-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="f9c45-138">`ruleName`(obrigatório) - SAS nome da regra para a entidade de Olá representada pelo Olá fornecido URI ou para Olá espaço de nomes representado pelo Olá parte de anfitrião do URI.</span><span class="sxs-lookup"><span data-stu-id="f9c45-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="f9c45-139">`key`(obrigatório) - chave válida para a regra SAS Olá.</span><span class="sxs-lookup"><span data-stu-id="f9c45-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="f9c45-140">`expirationSeconds`(opcional) - número de Olá de segundos até Olá gerada token deve expirar.</span><span class="sxs-lookup"><span data-stu-id="f9c45-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="f9c45-141">Se não for especificado, Olá predefinição é de 1 hora (3600).</span><span class="sxs-lookup"><span data-stu-id="f9c45-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="f9c45-142">token de Olá emitido confers direitos de Olá associados Olá especificado regra SAS para Olá fornecido duração.</span><span class="sxs-lookup"><span data-stu-id="f9c45-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="f9c45-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="f9c45-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="f9c45-144">Este método é funcionalmente equivalente toohello `createRelayToken` método documentados anteriormente, mas devolve Olá token toohello anexado corretamente entrada URI.</span><span class="sxs-lookup"><span data-stu-id="f9c45-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="f9c45-145">Classe ws. RelayedServer</span><span class="sxs-lookup"><span data-stu-id="f9c45-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="f9c45-146">Olá `hycows.RelayedServer` classe é uma alternativa toohello `ws.Server` classe que não escutam na rede local Olá, mas delega toohello escuta serviço de reencaminhamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c45-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="f9c45-147">as classes de Olá dois são principalmente contrato compatível, o que significa que uma aplicação existente utilizando Olá `ws.Server` toouse alteradas Olá retransmitida versão facilmente pode ser classe.</span><span class="sxs-lookup"><span data-stu-id="f9c45-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="f9c45-148">diferenças principais Olá são no construtor Olá e nas opções disponíveis Olá.</span><span class="sxs-lookup"><span data-stu-id="f9c45-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="f9c45-149">Construtor</span><span class="sxs-lookup"><span data-stu-id="f9c45-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="f9c45-150">Olá `RelayedServer` construtor suporta um conjunto diferente de argumentos que Olá `Server`porque não é um serviço de escuta autónomo ou toobe capacidade incorporada para uma arquitetura de serviço de escuta HTTP existente.</span><span class="sxs-lookup"><span data-stu-id="f9c45-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="f9c45-151">Também existem menos opções disponíveis, uma vez que Olá gestão WebSocket é amplamente delegado toohello serviço de reencaminhamento.</span><span class="sxs-lookup"><span data-stu-id="f9c45-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="f9c45-152">Argumentos de construtor:</span><span class="sxs-lookup"><span data-stu-id="f9c45-152">Constructor arguments:</span></span>

- <span data-ttu-id="f9c45-153">`server`(obrigatório) - Olá totalmente qualificado URI para um nome da ligação híbrida no qual toolisten, normalmente, construída com Olá método de programa auxiliar de WebSocket.createRelayListenUri().</span><span class="sxs-lookup"><span data-stu-id="f9c45-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="f9c45-154">`token`Este argumento (obrigatório) - contém uma cadeia de token emitida anteriormente ou uma função de chamada de retorno que pode ser chamada tooobtain essa uma cadeia de token.</span><span class="sxs-lookup"><span data-stu-id="f9c45-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="f9c45-155">opção de chamada de retorno de Olá é preferencial, tal como permite-renovação de token.</span><span class="sxs-lookup"><span data-stu-id="f9c45-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="f9c45-156">Eventos</span><span class="sxs-lookup"><span data-stu-id="f9c45-156">Events</span></span>

<span data-ttu-id="f9c45-157">`RelayedServer`instâncias emitir três eventos que permitem toohandle pedidos recebidos, estabelecer ligações e, detetar condições de erro.</span><span class="sxs-lookup"><span data-stu-id="f9c45-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="f9c45-158">Tem de subscrever toohello `connect` mensagens toohandle de eventos.</span><span class="sxs-lookup"><span data-stu-id="f9c45-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="f9c45-159">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="f9c45-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="f9c45-160">Olá `headers` evento é desencadeado imediatamente antes de uma ligação recebida é aceite, a ativação da modificação do cliente do Olá cabeçalhos toosend toohello.</span><span class="sxs-lookup"><span data-stu-id="f9c45-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="f9c45-161">ligação</span><span class="sxs-lookup"><span data-stu-id="f9c45-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="f9c45-162">Emitidos quando uma nova ligação de WebSocket foi aceite.</span><span class="sxs-lookup"><span data-stu-id="f9c45-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="f9c45-163">o objeto de Olá é do tipo `ws.WebSocket`, igual ao pacote base Olá.</span><span class="sxs-lookup"><span data-stu-id="f9c45-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="f9c45-164">erro</span><span class="sxs-lookup"><span data-stu-id="f9c45-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="f9c45-165">Se o servidor subjacente Olá emite um erro, este é reencaminhado aqui.</span><span class="sxs-lookup"><span data-stu-id="f9c45-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="f9c45-166">Programas de ajuda</span><span class="sxs-lookup"><span data-stu-id="f9c45-166">Helpers</span></span>

<span data-ttu-id="f9c45-167">toosimplify a partir de um servidor retransmitido e imediatamente subscrever tooincoming ligações, hello pacote expõe uma função de programa auxiliar simples, que também é utilizada nos exemplos de Olá, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="f9c45-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="f9c45-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="f9c45-168">createRelayedListener</span></span>

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a><span data-ttu-id="f9c45-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="f9c45-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="f9c45-170">Este método chama Olá construtor toocreate uma nova instância do Olá RelayedServer e, em seguida, subscreve Olá fornecido chamada de retorno toohello 'ligação' eventos.</span><span class="sxs-lookup"><span data-stu-id="f9c45-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="f9c45-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="f9c45-171">relayedConnect</span></span>

<span data-ttu-id="f9c45-172">Basta espelhamento Olá `createRelayedServer` auxiliar na função, `relayedConnect` cria uma ligação de cliente e subscreve toohello 'abertura' do evento num socket resultante Olá.</span><span class="sxs-lookup"><span data-stu-id="f9c45-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a><span data-ttu-id="f9c45-173">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f9c45-173">Next steps</span></span>
<span data-ttu-id="f9c45-174">toolearn mais informações sobre o reencaminhamento do Azure, visite estas ligações:</span><span class="sxs-lookup"><span data-stu-id="f9c45-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="f9c45-175">O que é o Reencaminhamento do Azure?</span><span class="sxs-lookup"><span data-stu-id="f9c45-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="f9c45-176">APIs de reencaminhamento disponíveis</span><span class="sxs-lookup"><span data-stu-id="f9c45-176">Available Relay APIs</span></span>](relay-api-overview.md)
