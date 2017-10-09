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
# <a name="relay-hybrid-connections-node-api-overview"></a>Descrição geral da API de nó de ligações híbridas de reencaminhamento

## <a name="overview"></a>Descrição geral

Olá [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pacote do nó para ligações de híbridas de reencaminhamento do Azure está incorporada no e expande Olá ['ws'](https://www.npmjs.com/package/ws) pacote NPM. Este pacote novamente Exporta todas as exportações esse pacote base e adiciona novas exportações que ativar a integração com a funcionalidade de ligações híbridas de serviço de reencaminhamento do Azure Olá. 

As aplicações existentes que `require('ws')` pode utilizar este pacote com `require('hyco-ws')` em vez disso, que também lhe permite cenários híbridos, em que uma aplicação pode escutar ligações de WebSocket localmente a partir do "no interior da firewall Olá" e através de ligações híbridas, todos num Olá mesmo tempo.
  
## <a name="documentation"></a>Documentação

Olá as APIs são [documentados no pacote de principal 'ws' Olá](https://github.com/websockets/ws/blob/master/doc/ws.md). Este artigo descreve como este pacote difere de acordo com esse linha de base. 

Olá principais diferenças entre o pacote de base de Olá e este 'hyco-ws' é que adiciona uma nova classe de servidor, exportada através de `require('hyco-ws').RelayedServer`e alguns métodos de programa auxiliar.

### <a name="package-helper-methods"></a>Métodos de programa auxiliar do pacote

Existem vários métodos de utilitário disponíveis na exportação do pacote de Olá que pode referenciar da seguinte forma:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

métodos de programa auxiliar de Olá são para utilização com este pacote, mas também podem ser utilizados por um servidor de nó para ativar a escuta de toocreate clientes web ou de dispositivo ou os remetentes. servidor de Olá utiliza estes métodos, transferindo-os URIs incorpore tokens de curta duração. Estes URIs também pode ser utilizado com comuns pilhas de WebSocket não suportam cabeçalhos HTTP de definição de handshake de WebSocket Olá. Ao incorporar tokens de autorização para Olá que URI é suportado principalmente para os cenários de utilização da biblioteca externa. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Cria uma escuta de reencaminhamento do Azure da ligação híbrida URI válida para Olá fornecido espaço de nomes e o caminho. Este URI, em seguida, pode ser utilizado com a versão de reencaminhamento de Olá do Olá WebSocketServer classe.

- `namespaceName`(obrigatório) - Olá nome qualificado do domínio de toouse de espaço de nomes do Olá reencaminhamento do Azure.
- `path`(obrigatório) - Olá o nome de uma ligação híbrida de reencaminhamento do Azure existente nesse espaço de nomes.
- `token`(opcional) - um acesso de reencaminhamento emitido anteriormente token que está incorporada no URI do serviço de escuta do Olá (consulte o seguinte exemplo de Olá).
- `id`(opcional) - um identificador de controlo que permite o controlo de ponto a ponto diagnósticos de pedidos.

Olá `token` valor é opcional e só deve ser utilizado quando não é possível toosend HTTP cabeçalhos, juntamente com o handshake de WebSocket Olá, como é Olá caso com pilha de W3C WebSocket Olá.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Cria um envio de reencaminhamento do Azure da ligação híbrida URI válido para Olá espaço de nome e caminho. Este URI pode ser utilizado com qualquer cliente de WebSocket.

- `namespaceName`(obrigatório) - Olá nome qualificado do domínio de toouse de espaço de nomes do Olá reencaminhamento do Azure.
- `path`(obrigatório) - Olá o nome de uma ligação híbrida de reencaminhamento do Azure existente nesse espaço de nomes.
- `token`(opcional) - um token de acesso de reencaminhamento emitido anteriormente que está incorporado Olá enviar URI (consulte o seguinte exemplo de Olá).
- `id`(opcional) - um identificador de controlo que permite o controlo de ponto a ponto diagnósticos de pedidos.

Olá `token` valor é opcional e só deve ser utilizado quando não é possível toosend HTTP cabeçalhos, juntamente com o handshake de WebSocket Olá, como é Olá caso com pilha de W3C WebSocket Olá.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Cria um token de assinatura de acesso partilhado do Azure reencaminhamento (SAS) para o URI de destino Olá fornecido, a regra SAS e a regra da chave SAS que é válida para Olá desde número de segundos ou para uma hora Olá atual instantânea se o argumento de expiração de Olá for omitido.

- `uri`(obrigatório) - Olá URI para o qual Olá token é toobe emitido. Olá URI é o esquema HTTP de Olá toouse normalizado e as informações da cadeia de consulta são eliminadas.
- `ruleName`(obrigatório) - SAS nome da regra para a entidade de Olá representada pelo Olá fornecido URI ou para Olá espaço de nomes representado pelo Olá parte de anfitrião do URI.
- `key`(obrigatório) - chave válida para a regra SAS Olá. 
- `expirationSeconds`(opcional) - número de Olá de segundos até Olá gerada token deve expirar. Se não for especificado, Olá predefinição é de 1 hora (3600).

token de Olá emitido confers direitos de Olá associados Olá especificado regra SAS para Olá fornecido duração.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Este método é funcionalmente equivalente toohello `createRelayToken` método documentados anteriormente, mas devolve Olá token toohello anexado corretamente entrada URI.

### <a name="class-wsrelayedserver"></a>Classe ws. RelayedServer

Olá `hycows.RelayedServer` classe é uma alternativa toohello `ws.Server` classe que não escutam na rede local Olá, mas delega toohello escuta serviço de reencaminhamento do Azure.

as classes de Olá dois são principalmente contrato compatível, o que significa que uma aplicação existente utilizando Olá `ws.Server` toouse alteradas Olá retransmitida versão facilmente pode ser classe. diferenças principais Olá são no construtor Olá e nas opções disponíveis Olá.

#### <a name="constructor"></a>Construtor  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Olá `RelayedServer` construtor suporta um conjunto diferente de argumentos que Olá `Server`porque não é um serviço de escuta autónomo ou toobe capacidade incorporada para uma arquitetura de serviço de escuta HTTP existente. Também existem menos opções disponíveis, uma vez que Olá gestão WebSocket é amplamente delegado toohello serviço de reencaminhamento.

Argumentos de construtor:

- `server`(obrigatório) - Olá totalmente qualificado URI para um nome da ligação híbrida no qual toolisten, normalmente, construída com Olá método de programa auxiliar de WebSocket.createRelayListenUri().
- `token`Este argumento (obrigatório) - contém uma cadeia de token emitida anteriormente ou uma função de chamada de retorno que pode ser chamada tooobtain essa uma cadeia de token. opção de chamada de retorno de Olá é preferencial, tal como permite-renovação de token.

#### <a name="events"></a>Eventos

`RelayedServer`instâncias emitir três eventos que permitem toohandle pedidos recebidos, estabelecer ligações e, detetar condições de erro. Tem de subscrever toohello `connect` mensagens toohandle de eventos. 

##### <a name="headers"></a>Cabeçalhos

```JavaScript 
function(headers)
```

Olá `headers` evento é desencadeado imediatamente antes de uma ligação recebida é aceite, a ativação da modificação do cliente do Olá cabeçalhos toosend toohello. 

##### <a name="connection"></a>ligação

```JavaScript
function(socket)
```

Emitidos quando uma nova ligação de WebSocket foi aceite. o objeto de Olá é do tipo `ws.WebSocket`, igual ao pacote base Olá.


##### <a name="error"></a>erro

```JavaScript
function(error)
```

Se o servidor subjacente Olá emite um erro, este é reencaminhado aqui.  

#### <a name="helpers"></a>Programas de ajuda

toosimplify a partir de um servidor retransmitido e imediatamente subscrever tooincoming ligações, hello pacote expõe uma função de programa auxiliar simples, que também é utilizada nos exemplos de Olá, da seguinte forma:

##### <a name="createrelayedlistener"></a>createRelayedListener

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

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Este método chama Olá construtor toocreate uma nova instância do Olá RelayedServer e, em seguida, subscreve Olá fornecido chamada de retorno toohello 'ligação' eventos.
 
##### <a name="relayedconnect"></a>relayedConnect

Basta espelhamento Olá `createRelayedServer` auxiliar na função, `relayedConnect` cria uma ligação de cliente e subscreve toohello 'abertura' do evento num socket resultante Olá.

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

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre o reencaminhamento do Azure, visite estas ligações:
* [O que é o Reencaminhamento do Azure?](relay-what-is-it.md)
* [APIs de reencaminhamento disponíveis](relay-api-overview.md)
