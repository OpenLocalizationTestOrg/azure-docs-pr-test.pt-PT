<span data-ttu-id="d9f3b-101">Criar um [aplicação web](../articles/app-service-web/app-service-web-overview.md) no Olá `myAppServicePlan` plano do App Service com Olá [az webapp criar](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="d9f3b-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="d9f3b-102">aplicação web de Olá fornece um espaço de alojamento para o seu código e fornece uma aplicação do URL tooview Olá implementado.</span><span class="sxs-lookup"><span data-stu-id="d9f3b-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="d9f3b-103">No Olá o seguinte comando, substitua  *\<APP_NAME>.azurewebsites.NET >* com um nome exclusivo (carateres válidos são `a-z`, `0-9`, e `-`).</span><span class="sxs-lookup"><span data-stu-id="d9f3b-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="d9f3b-104">Se `<app_name>` é não exclusivo, obtém a mensagem de erro de Olá "Web site com o nome < APP_NAME>.azurewebsites.NET > especificado já existe."</span><span class="sxs-lookup"><span data-stu-id="d9f3b-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="d9f3b-105">Olá predefinido é o URL da aplicação web de Olá `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d9f3b-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="d9f3b-106">Quando tiver sido criada a aplicação web de Olá, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="d9f3b-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```

<span data-ttu-id="d9f3b-107">Procure toohello site toosee a sua aplicação web recentemente criada.</span><span class="sxs-lookup"><span data-stu-id="d9f3b-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
