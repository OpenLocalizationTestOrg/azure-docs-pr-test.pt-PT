Configurar local aplicação de web de toohello a implementação de Git com Olá [origem de implementação webapp com az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando.

App Service suporte várias formas toodeploy tooa conteúdo aplicação web, tal como FTP, o local Git, o GitHub, o Visual Studio Team Services e o Bitbucket. Para este início rápido, pode implementar com o Git local. Isto significa que implementar utilizando um toopush de comandos de Git do repositório de tooa repositório local no Azure. 

No Olá o seguinte comando, substitua  *\<APP_NAME>.azurewebsites.NET >* com o nome da sua aplicação web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

saída de Olá tem Olá seguinte formato:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Olá `<username>` é Olá [utilizador implementação](#configure-a-deployment-user) que criou no passo anterior.

Copiar Olá URI mostrado; irá utilizá-lo no passo seguinte Olá.
