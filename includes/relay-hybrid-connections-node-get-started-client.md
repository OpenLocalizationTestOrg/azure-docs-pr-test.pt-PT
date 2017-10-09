### <a name="create-a-nodejs-application"></a>Criar uma aplicação Node.js

Criar um novo ficheiro JavaScript denominado `sender.js`.

### <a name="add-hello-relay-npm-package"></a>Adicionar pacote de reencaminhamento NPM Olá

Execute `npm install hyco-ws` a partir de uma linha de comandos do Nó na sua pasta do projeto.

### <a name="write-some-code-toosend-messages"></a>Escrever alguns códigos toosend mensagens

1. Adicione Olá seguinte `constants` toohello superior de Olá `sender.js` ficheiro.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Adicionar Olá seguintes constantes toohello `sender.js` Olá híbrida ligação detalhes no ficheiro. Substitua os marcadores de posição de Olá entre parênteses Retos valores Olá que obteve aquando da criação da ligação híbrida Olá.
   
   1. `const ns`-Olá espaço de nomes de reencaminhamento. Ser toouse se Olá completamente qualificado espaço de nomes; Por exemplo, `{namespace}.servicebus.windows.net`.
   2. `const path`-nome Olá da ligação híbrida Olá.
   3. `const keyrule`-nome de Olá da chave SAS do Olá.
   4. `const key`-Olá valor da chave SAS.

3. Adicionar Olá seguinte código toohello `sender.js` ficheiro:
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    O ficheiro sender.js deve ter o seguinte aspeto:
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

