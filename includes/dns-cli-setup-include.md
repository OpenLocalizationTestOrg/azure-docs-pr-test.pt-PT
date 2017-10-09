## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="b73e1-101">Configurar CLI do Azure para o Azure DNS</span><span class="sxs-lookup"><span data-stu-id="b73e1-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="b73e1-102">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="b73e1-102">Before you begin</span></span>

<span data-ttu-id="b73e1-103">Certifique-se de que tem Olá seguintes itens antes de iniciar a configuração.</span><span class="sxs-lookup"><span data-stu-id="b73e1-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="b73e1-104">Uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="b73e1-104">An Azure subscription.</span></span> <span data-ttu-id="b73e1-105">Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b73e1-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b73e1-106">Instale a versão mais recente do Olá do Olá CLI do Azure, disponível para Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="b73e1-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="b73e1-107">Estão disponíveis mais informações no [instalação Olá CLI do Azure](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b73e1-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="b73e1-108">Inicie sessão no tooyour a conta do Azure</span><span class="sxs-lookup"><span data-stu-id="b73e1-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="b73e1-109">Abra uma janela de consola e autentique com as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="b73e1-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="b73e1-110">Para obter mais informações, consulte [tooAzure de Olá CLI do Azure de início de sessão](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="b73e1-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="b73e1-111">Alternar o modo da CLI</span><span class="sxs-lookup"><span data-stu-id="b73e1-111">Switch CLI mode</span></span>

<span data-ttu-id="b73e1-112">O DNS do Azure utiliza o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b73e1-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="b73e1-113">Certifique-se de que alterna comandos da CLI modo toouse do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b73e1-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="b73e1-114">Selecione a subscrição de Olá</span><span class="sxs-lookup"><span data-stu-id="b73e1-114">Select hello subscription</span></span>

<span data-ttu-id="b73e1-115">Verifique Olá subscrições para a conta de Olá.</span><span class="sxs-lookup"><span data-stu-id="b73e1-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="b73e1-116">Escolha qual das suas toouse de subscrições do Azure.</span><span class="sxs-lookup"><span data-stu-id="b73e1-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="b73e1-117">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b73e1-117">Create a resource group</span></span>

<span data-ttu-id="b73e1-118">O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização,</span><span class="sxs-lookup"><span data-stu-id="b73e1-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="b73e1-119">Isto é utilizado como localização predefinida de Olá para recursos nesse grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b73e1-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="b73e1-120">No entanto, uma vez que todos os recursos DNS são globais, não regionais, escolha de Olá de localização do grupo de recursos não tem impacto no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="b73e1-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="b73e1-121">Pode ignorar este passo se estiver a utilizar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="b73e1-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="b73e1-122">Registar o fornecedor de recursos</span><span class="sxs-lookup"><span data-stu-id="b73e1-122">Register resource provider</span></span>

<span data-ttu-id="b73e1-123">Olá serviço DNS do Azure é gerida pelo fornecedor de recursos do Olá Network.</span><span class="sxs-lookup"><span data-stu-id="b73e1-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="b73e1-124">A subscrição do Azure tem de ser registado toouse este fornecedor de recursos antes de poder utilizar o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="b73e1-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="b73e1-125">Esta é uma operação única para cada subscrição.</span><span class="sxs-lookup"><span data-stu-id="b73e1-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

