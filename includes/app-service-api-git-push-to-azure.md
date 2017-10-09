Utilize Olá CLI do Azure tooget Olá implementação remota URL para a sua aplicação API. No Olá o seguinte comando, substitua  *\<APP_NAME>.azurewebsites.NET >* com o nome da sua aplicação web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Configure o seu local Git implementação toobe toopush capaz de toohello remoto.

```bash
git remote add azure <URI from previous step>
```

Push toohello toodeploy remoto do Azure a sua aplicação. Lhe for pedido para a palavra-passe de Olá que criou anteriormente quando criou o utilizador de implementação de Olá. Certifique-se de que introduz a palavra-passe de Olá que criou anteriormente no guia de introdução Olá e não Olá palavra-passe que utilize toolog toohello portal do Azure.

```bash
git push azure master
```
