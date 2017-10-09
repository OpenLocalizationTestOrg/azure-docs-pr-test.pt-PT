<span data-ttu-id="e6df0-101">Configurar local aplicação de web de toohello a implementação de Git com Olá [origem de implementação webapp com az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando.</span><span class="sxs-lookup"><span data-stu-id="e6df0-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="e6df0-102">App Service suporte várias formas toodeploy tooa conteúdo aplicação web, tal como FTP, o local Git, o GitHub, o Visual Studio Team Services e o Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="e6df0-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="e6df0-103">Para este início rápido, pode implementar com o Git local.</span><span class="sxs-lookup"><span data-stu-id="e6df0-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="e6df0-104">Isto significa que implementar utilizando um toopush de comandos de Git do repositório de tooa repositório local no Azure.</span><span class="sxs-lookup"><span data-stu-id="e6df0-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="e6df0-105">No Olá o seguinte comando, substitua  *\<APP_NAME>.azurewebsites.NET >* com o nome da sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="e6df0-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="e6df0-106">saída de Olá tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="e6df0-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="e6df0-107">Olá `<username>` é Olá [utilizador implementação](#configure-a-deployment-user) que criou no passo anterior.</span><span class="sxs-lookup"><span data-stu-id="e6df0-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="e6df0-108">Copiar Olá URI mostrado; irá utilizá-lo no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="e6df0-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
