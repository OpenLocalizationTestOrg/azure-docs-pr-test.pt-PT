## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="1080e-101">Preparar tooauthenticate pedidos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1080e-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="1080e-102">Tem de autenticar todas as operações de Olá efetuar recursos através de Olá [do Azure Resource Manager] [ lnk-authenticate-arm] com o Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="1080e-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="1080e-103">Olá tooconfigure de forma mais fácil é toouse PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1080e-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="1080e-104">Instalar Olá [cmdlets Azure PowerShell] [ lnk-powershell-install] antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="1080e-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="1080e-105">Olá, como os seguintes passos Mostrar tooset configurar a autenticação de palavra-passe para uma aplicação AD utilizando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1080e-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="1080e-106">Pode executar estes comandos numa sessão do PowerShell padrão.</span><span class="sxs-lookup"><span data-stu-id="1080e-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="1080e-107">Inicie sessão no tooyour subscrição do Azure com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="1080e-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="1080e-108">Se tiver várias subscrições do Azure, iniciar sessão tooAzure concede acesso tooall Olá subscrições Azure associadas as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="1080e-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="1080e-109">Utilize Olá toolist Olá subscrições do Azure disponíveis para si toouse de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1080e-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="1080e-110">Utilize Olá seguir subscrição tooselect de comando que pretende que o toouse toorun Olá comandos toomanage seu IoT hub.</span><span class="sxs-lookup"><span data-stu-id="1080e-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="1080e-111">Pode utilizar o nome da subscrição Olá ou o ID da saída de Olá do comando anterior Olá:</span><span class="sxs-lookup"><span data-stu-id="1080e-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="1080e-112">Tome nota do seu **TenantId** e **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="1080e-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="1080e-113">Poderá precisa deles mais tarde.</span><span class="sxs-lookup"><span data-stu-id="1080e-113">You need them later.</span></span>
3. <span data-ttu-id="1080e-114">Crie uma nova aplicação do Azure Active Directory utilizando Olá comando a seguir, substituindo os proprietários de local da Olá:</span><span class="sxs-lookup"><span data-stu-id="1080e-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="1080e-115">**{Nome a apresentar}:** um nome a apresentar para a sua aplicação, tais como **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="1080e-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="1080e-116">**{URL da página inicial}:** Olá, tais como o URL da Olá home page da sua aplicação **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="1080e-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="1080e-117">Este URL não precisa de toopoint tooa real aplicação.</span><span class="sxs-lookup"><span data-stu-id="1080e-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="1080e-118">**{Identificador da aplicação}:** um identificador exclusivo, tais como **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="1080e-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="1080e-119">Este URL não precisa de toopoint tooa real aplicação.</span><span class="sxs-lookup"><span data-stu-id="1080e-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="1080e-120">**{Palavra-passe}:** uma palavra-passe que utiliza tooauthenticate com a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="1080e-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="1080e-121">Tome nota do Olá **ApplicationId** da aplicação Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="1080e-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="1080e-122">Poderá precisa deste mais tarde.</span><span class="sxs-lookup"><span data-stu-id="1080e-122">You need this later.</span></span>
5. <span data-ttu-id="1080e-123">Criar um novo principal de serviço com Olá comando a seguir, substituindo **{MyApplicationId}** com Olá **ApplicationId** do passo anterior Olá:</span><span class="sxs-lookup"><span data-stu-id="1080e-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="1080e-124">Configurar uma atribuição de função utilizando Olá comando a seguir, substituindo **{MyApplicationId}** com seu **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="1080e-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="1080e-125">Terminar agora de criar a aplicação do Azure AD Olá que lhe permite tooauthenticate da sua aplicação c# personalizada.</span><span class="sxs-lookup"><span data-stu-id="1080e-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="1080e-126">É necessário Olá os seguintes valores mais tarde no tutorial:</span><span class="sxs-lookup"><span data-stu-id="1080e-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="1080e-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="1080e-127">TenantId</span></span>
* <span data-ttu-id="1080e-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="1080e-128">SubscriptionId</span></span>
* <span data-ttu-id="1080e-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="1080e-129">ApplicationId</span></span>
* <span data-ttu-id="1080e-130">Palavra-passe</span><span class="sxs-lookup"><span data-stu-id="1080e-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
