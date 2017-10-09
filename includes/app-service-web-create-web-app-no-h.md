Criar um [aplicação web](../articles/app-service-web/app-service-web-overview.md) no Olá `myAppServicePlan` plano do App Service com Olá [az webapp criar](/cli/azure/webapp#create) comando. 

aplicação web de Olá fornece um espaço de alojamento para o seu código e fornece uma aplicação do URL tooview Olá implementado.

No Olá o seguinte comando, substitua  *\<APP_NAME>.azurewebsites.NET >* com um nome exclusivo (carateres válidos são `a-z`, `0-9`, e `-`). Se `<app_name>` é não exclusivo, obtém a mensagem de erro de Olá "Web site com o nome < APP_NAME>.azurewebsites.NET > especificado já existe." Olá predefinido é o URL da aplicação web de Olá `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Quando tiver sido criada a aplicação web de Olá, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:

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

Procure toohello site toosee a sua aplicação web recentemente criada.

```bash
http://<app_name>.azurewebsites.net
```
