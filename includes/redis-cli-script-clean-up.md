## <a name="clean-up-deployment"></a><span data-ttu-id="9a46e-101">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="9a46e-101">Clean up deployment</span></span> 

<span data-ttu-id="9a46e-102">Depois de executar o script de exemplo Olá, Olá siga pode ser utilizado tooremove grupo de recursos de Olá, instância da Cache de Redis do Azure e quaisquer recursos relacionados no grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="9a46e-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```