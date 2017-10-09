## <a name="overview-of-azure-resource-manager-templates"></a>Descrição Geral dos Modelos do Azure Resource Manager
Modelos Azure Resource Manager permitem-lhe toodeclaratively especificar infraestrutura do IaaS do Azure de Olá no idioma de Json por definir Olá dependências entre os recursos. Para obter uma descrição detalhada dos modelos do Azure Resource Manager, consulte o artigo toohello abaixo:

[Descrição geral do grupo de recursos](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Fragmento de modelo de exemplo para extensões VM
Implementar extensões VM como parte de um modelo Azure Resource Manager requer que toodeclaratively especificar a configuração de extensão de Olá no modelo de Olá.
Eis o formato de Olá para especificar a configuração da extensão Olá.

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

Como pode ver partir Olá acima, o modelo de extensão de Olá contém duas partes principais:

1. Nome da extensão, publicador e versão
2. Configuração de extensão.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Identificar o publicador de Olá, tipo e typeHandlerVersion para qualquer extensão
Extensões VM do Azure são publicadas pela Microsoft e fidedigno 3rd editores de terceiros e cada extensão é identificado de forma exclusiva pelo respetivo fabricante, o tipo e Olá typeHandlerVersion. Estes podem ser determinados seguinte forma:  

