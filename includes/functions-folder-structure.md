
código de Olá para todas as funções de Olá numa aplicação de função especificada se encontra numa pasta raiz que contenha um ficheiro de configuração de anfitrião e uma ou mais subpastas, cada um dos quais contêm código Olá para uma função separada, como no seguinte exemplo de Olá:

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

Olá *host.json* ficheiro contém uma configuração específica do tempo de execução e se encontra na pasta de raiz de Olá da aplicação de função Olá. Para obter informações sobre as definições que estão disponíveis, consulte [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) no wiki do Olá WebJobs.Script repositório.

Cada função tem uma pasta que contém um ou mais ficheiros de código, configuração de function.json Olá e outras dependências.

