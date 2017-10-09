### <a name="create-a-nodejs-application"></a><span data-ttu-id="aed79-101">Criar uma aplicação Node.js</span><span class="sxs-lookup"><span data-stu-id="aed79-101">Create a Node.js application</span></span>

<span data-ttu-id="aed79-102">Criar um novo ficheiro JavaScript denominado `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="aed79-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="aed79-103">Adicionar pacote de reencaminhamento NPM Olá</span><span class="sxs-lookup"><span data-stu-id="aed79-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="aed79-104">Execute `npm install hyco-ws` a partir de uma linha de comandos do Nó na sua pasta do projeto.</span><span class="sxs-lookup"><span data-stu-id="aed79-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="aed79-105">Escrever alguns códigos tooreceive mensagens</span><span class="sxs-lookup"><span data-stu-id="aed79-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="aed79-106">Adicionar Olá seguir superior toohello constante de Olá `listener.js` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="aed79-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="aed79-107">Adicionar Olá seguintes constantes toohello `listener.js` Olá híbrida ligação detalhes no ficheiro.</span><span class="sxs-lookup"><span data-stu-id="aed79-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="aed79-108">Substitua os marcadores de posição de Olá entre parênteses Retos valores Olá que obteve aquando da criação da ligação híbrida Olá.</span><span class="sxs-lookup"><span data-stu-id="aed79-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="aed79-109">`const ns`-Olá espaço de nomes de reencaminhamento.</span><span class="sxs-lookup"><span data-stu-id="aed79-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="aed79-110">Ser toouse se Olá completamente qualificado espaço de nomes; Por exemplo, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="aed79-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="aed79-111">`const path`-nome Olá da ligação híbrida Olá.</span><span class="sxs-lookup"><span data-stu-id="aed79-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="aed79-112">`const keyrule`-nome de Olá da chave SAS do Olá.</span><span class="sxs-lookup"><span data-stu-id="aed79-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="aed79-113">`const key`-Olá valor da chave SAS.</span><span class="sxs-lookup"><span data-stu-id="aed79-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="aed79-114">Adicionar Olá seguinte código toohello `listener.js` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="aed79-114">Add hello following code toohello `listener.js` file:</span></span>
   
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
    <span data-ttu-id="aed79-115">O ficheiro listener.js deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="aed79-115">Here is what your listener.js file should look like:</span></span>
   
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

