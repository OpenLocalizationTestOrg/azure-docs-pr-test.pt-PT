### <a name="create-a-nodejs-application"></a><span data-ttu-id="7e07d-101">Criar uma aplicação Node.js</span><span class="sxs-lookup"><span data-stu-id="7e07d-101">Create a Node.js application</span></span>

<span data-ttu-id="7e07d-102">Criar um novo ficheiro JavaScript denominado `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="7e07d-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="7e07d-103">Adicionar pacote de reencaminhamento NPM Olá</span><span class="sxs-lookup"><span data-stu-id="7e07d-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="7e07d-104">Execute `npm install hyco-ws` a partir de uma linha de comandos do Nó na sua pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="7e07d-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="7e07d-105">Escrever alguns códigos toosend mensagens</span><span class="sxs-lookup"><span data-stu-id="7e07d-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="7e07d-106">Adicione Olá seguinte `constants` toohello superior de Olá `sender.js` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7e07d-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="7e07d-107">Adicionar Olá seguintes constantes toohello `sender.js` Olá híbrida ligação detalhes no ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7e07d-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="7e07d-108">Substitua os marcadores de posição de Olá entre parênteses Retos valores Olá que obteve aquando da criação da ligação híbrida Olá.</span><span class="sxs-lookup"><span data-stu-id="7e07d-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="7e07d-109">`const ns`-Olá espaço de nomes de reencaminhamento.</span><span class="sxs-lookup"><span data-stu-id="7e07d-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="7e07d-110">Ser toouse se Olá completamente qualificado espaço de nomes; Por exemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="7e07d-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="7e07d-111">`const path`-nome Olá da ligação híbrida Olá.</span><span class="sxs-lookup"><span data-stu-id="7e07d-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="7e07d-112">`const keyrule`-nome de Olá da chave SAS do Olá.</span><span class="sxs-lookup"><span data-stu-id="7e07d-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="7e07d-113">`const key`-Olá valor da chave SAS.</span><span class="sxs-lookup"><span data-stu-id="7e07d-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="7e07d-114">Adicionar Olá seguinte código toohello `sender.js` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="7e07d-114">Add hello following code toohello `sender.js` file:</span></span>
   
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
    <span data-ttu-id="7e07d-115">O ficheiro sender.js deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="7e07d-115">Here is what your sender.js file should look like:</span></span>
   
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

