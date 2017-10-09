## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="35b11-101">Configurar o Azure PowerShell para o DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="35b11-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="35b11-102">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="35b11-102">Before you begin</span></span>

<span data-ttu-id="35b11-103">Certifique-se de que tem Olá seguintes itens antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="35b11-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="35b11-104">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="35b11-104">An Azure subscription.</span></span> <span data-ttu-id="35b11-105">Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35b11-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="35b11-106">Tem a versão mais recente de Olá tooinstall de Olá cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="35b11-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="35b11-107">Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="35b11-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="35b11-108">Inicie sessão no tooyour a conta do Azure</span><span class="sxs-lookup"><span data-stu-id="35b11-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="35b11-109">Abra a consola do PowerShell e ligue tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="35b11-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="35b11-110">Para obter mais informações, consulte [utilizando o PowerShell com o Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="35b11-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="35b11-111">Selecione a subscrição de Olá</span><span class="sxs-lookup"><span data-stu-id="35b11-111">Select hello subscription</span></span>
 
<span data-ttu-id="35b11-112">Verifique Olá subscrições para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="35b11-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="35b11-113">Escolha qual das suas toouse de subscrições do Azure.</span><span class="sxs-lookup"><span data-stu-id="35b11-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="35b11-114">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="35b11-114">Create a resource group</span></span>

<span data-ttu-id="35b11-115">O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização,</span><span class="sxs-lookup"><span data-stu-id="35b11-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="35b11-116">Esta localização é utilizada como localização predefinida de Olá para recursos nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="35b11-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="35b11-117">No entanto, uma vez que todos os recursos DNS são globais, não regionais, escolha de Olá de localização do grupo de recursos não tem impacto no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="35b11-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="35b11-118">Pode ignorar este passo se estiver a utilizar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="35b11-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="35b11-119">Registar o fornecedor de recursos</span><span class="sxs-lookup"><span data-stu-id="35b11-119">Register resource provider</span></span>

<span data-ttu-id="35b11-120">Olá serviço DNS do Azure é gerida pelo fornecedor de recursos do Olá Network.</span><span class="sxs-lookup"><span data-stu-id="35b11-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="35b11-121">A subscrição do Azure tem de ser registado toouse este fornecedor de recursos antes de poder utilizar o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="35b11-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="35b11-122">Esta é uma operação única para cada subscrição.</span><span class="sxs-lookup"><span data-stu-id="35b11-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```