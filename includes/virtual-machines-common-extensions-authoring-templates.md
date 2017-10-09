## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="199a5-101">Descrição Geral dos Modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="199a5-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="199a5-102">Modelos Azure Resource Manager permitem-lhe toodeclaratively especificar infraestrutura do IaaS do Azure de Olá no idioma de Json por definir Olá dependências entre os recursos.</span><span class="sxs-lookup"><span data-stu-id="199a5-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="199a5-103">Para obter uma descrição detalhada dos modelos do Azure Resource Manager, consulte o artigo toohello abaixo:</span><span class="sxs-lookup"><span data-stu-id="199a5-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="199a5-104">Descrição geral do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="199a5-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="199a5-105">Fragmento de modelo de exemplo para extensões VM</span><span class="sxs-lookup"><span data-stu-id="199a5-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="199a5-106">Implementar extensões VM como parte de um modelo Azure Resource Manager requer que toodeclaratively especificar a configuração de extensão de Olá no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="199a5-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="199a5-107">Eis o formato de Olá para especificar a configuração da extensão Olá.</span><span class="sxs-lookup"><span data-stu-id="199a5-107">Here is hello format for specifying hello extension configuration.</span></span>

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

<span data-ttu-id="199a5-108">Como pode ver partir Olá acima, o modelo de extensão de Olá contém duas partes principais:</span><span class="sxs-lookup"><span data-stu-id="199a5-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="199a5-109">Nome da extensão, publicador e versão</span><span class="sxs-lookup"><span data-stu-id="199a5-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="199a5-110">Configuração de extensão.</span><span class="sxs-lookup"><span data-stu-id="199a5-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="199a5-111">Identificar o publicador de Olá, tipo e typeHandlerVersion para qualquer extensão</span><span class="sxs-lookup"><span data-stu-id="199a5-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="199a5-112">Extensões VM do Azure são publicadas pela Microsoft e fidedigno 3rd editores de terceiros e cada extensão é identificado de forma exclusiva pelo respetivo fabricante, o tipo e Olá typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="199a5-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="199a5-113">Estes podem ser determinados seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="199a5-113">These can be determined as following:</span></span>  

