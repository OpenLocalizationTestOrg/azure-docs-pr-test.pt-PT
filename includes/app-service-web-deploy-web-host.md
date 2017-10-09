### <a name="app-service-plan"></a>Plano do App Service
Cria o plano de serviço Olá para alojar a aplicação web de Olá. Fornecer Olá nome do plano de Olá através de Olá **hostingPlanName** parâmetro. localização de Olá do plano de Olá está Olá mesma localização utilizada para o grupo de recursos de Olá. Olá preço camada e de trabalho tamanho estão especificados na Olá **sku** e **workerSize** parâmetros

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

