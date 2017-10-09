<span data-ttu-id="afc32-101">Criar um plano de serviço de aplicações com Olá [criar plano de serviço aplicacional az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="afc32-101">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="afc32-102">Olá exemplo seguinte cria um plano de serviço de aplicações com o nome `myAppServicePlan` no Olá **livres** escalão de preço:</span><span class="sxs-lookup"><span data-stu-id="afc32-102">hello following example creates an App Service plan named `myAppServicePlan` in hello **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="afc32-103">Quando tiver sido criado Olá plano do App Service, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="afc32-103">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```