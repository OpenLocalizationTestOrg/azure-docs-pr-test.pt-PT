<span data-ttu-id="09854-101">Utilize Olá CLI do Azure tooget Olá implementação remota URL para a sua aplicação API.</span><span class="sxs-lookup"><span data-stu-id="09854-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="09854-102">No Olá o seguinte comando, substitua  *\<APP_NAME>.azurewebsites.NET >* com o nome da sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="09854-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="09854-103">Configure o seu local Git implementação toobe toopush capaz de toohello remoto.</span><span class="sxs-lookup"><span data-stu-id="09854-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="09854-104">Push toohello toodeploy remoto do Azure a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="09854-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="09854-105">Lhe for pedido para a palavra-passe de Olá que criou anteriormente quando criou o utilizador de implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="09854-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="09854-106">Certifique-se de que introduz a palavra-passe de Olá que criou anteriormente no guia de introdução Olá e não Olá palavra-passe que utilize toolog toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="09854-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
