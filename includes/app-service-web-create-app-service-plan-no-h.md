Criar um plano de serviço de aplicações com Olá [criar plano de serviço aplicacional az](/cli/azure/appservice/plan#create) comando.

[!INCLUDE [app-service-plan](app-service-plan.md)]

Olá exemplo seguinte cria um plano de serviço de aplicações com o nome `myAppServicePlan` no Olá **livres** escalão de preço:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Quando tiver sido criado Olá plano do App Service, Olá CLI do Azure mostra informações toohello semelhante seguinte exemplo:

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