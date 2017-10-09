
<span data-ttu-id="4ab15-101">código de Olá para todas as funções de Olá numa aplicação de função especificada se encontra numa pasta raiz que contenha um ficheiro de configuração de anfitrião e uma ou mais subpastas, cada um dos quais contêm código Olá para uma função separada, como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="4ab15-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

<span data-ttu-id="4ab15-102">Olá *host.json* ficheiro contém uma configuração específica do tempo de execução e se encontra na pasta de raiz de Olá da aplicação de função Olá.</span><span class="sxs-lookup"><span data-stu-id="4ab15-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="4ab15-103">Para obter informações sobre as definições que estão disponíveis, consulte [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) no wiki do Olá WebJobs.Script repositório.</span><span class="sxs-lookup"><span data-stu-id="4ab15-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="4ab15-104">Cada função tem uma pasta que contém um ou mais ficheiros de código, configuração de function.json Olá e outras dependências.</span><span class="sxs-lookup"><span data-stu-id="4ab15-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

