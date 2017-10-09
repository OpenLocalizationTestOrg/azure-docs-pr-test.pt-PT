### <a name="app-service-plan"></a><span data-ttu-id="4ac2e-101">Plano do App Service</span><span class="sxs-lookup"><span data-stu-id="4ac2e-101">App Service plan</span></span>
<span data-ttu-id="4ac2e-102">Cria o plano de serviço Olá para alojar a aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="4ac2e-103">Fornecer Olá nome do plano de Olá através de Olá **hostingPlanName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="4ac2e-104">localização de Olá do plano de Olá está Olá mesma localização utilizada para o grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="4ac2e-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="4ac2e-105">Olá preço camada e de trabalho tamanho estão especificados na Olá **sku** e **workerSize** parâmetros</span><span class="sxs-lookup"><span data-stu-id="4ac2e-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

