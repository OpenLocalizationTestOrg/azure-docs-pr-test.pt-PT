### <a name="create-a-nodejs-application"></a>Criar uma aplicação Node.js

Criar um novo ficheiro JavaScript denominado `listener.js`.

### <a name="add-hello-relay-npm-package"></a>Adicionar pacote de reencaminhamento NPM Olá

Execute `npm install hyco-ws` a partir de uma linha de comandos do Nó na sua pasta do projeto.

### <a name="write-some-code-tooreceive-messages"></a>Escrever alguns códigos tooreceive mensagens

1. Adicionar Olá seguir superior toohello constante de Olá `listener.js` ficheiro.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Adicionar Olá seguintes constantes toohello `listener.js` Olá híbrida ligação detalhes no ficheiro. Substitua os marcadores de posição de Olá entre parênteses Retos valores Olá que obteve aquando da criação da ligação híbrida Olá.
   
   1. `const ns`-Olá espaço de nomes de reencaminhamento. Ser toouse se Olá completamente qualificado espaço de nomes; Por exemplo, `{namespace}.servicebus.windows.net`.
   2. `const path`-nome Olá da ligação híbrida Olá.
   3. `const keyrule`-nome de Olá da chave SAS do Olá.
   4. `const key`-Olá valor da chave SAS.

3. Adicionar Olá seguinte código toohello `listener.js` ficheiro:
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    O ficheiro listener.js deve ter o seguinte aspeto:
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

