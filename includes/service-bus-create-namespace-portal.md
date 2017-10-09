<span data-ttu-id="be135-101">filas toobegin utilizando o Service Bus no Azure, primeiro tem de criar um espaço de nomes com um nome que seja exclusivo em todo o Azure.</span><span class="sxs-lookup"><span data-stu-id="be135-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="be135-102">Um espaço de nomes fornece um contentor de âmbito para abordar os recursos do Service Bus na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="be135-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="be135-103">toocreate um espaço de nomes:</span><span class="sxs-lookup"><span data-stu-id="be135-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="be135-104">Inicie sessão no toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="be135-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="be135-105">No painel de navegação esquerdo Olá do portal de Olá, clique em **novo**, em seguida, clique em **integração empresarial com**e, em seguida, clique em **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="be135-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="be135-106">No Olá **criar espaço de nomes** caixa de diálogo, introduza um nome de espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="be135-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="be135-107">sistema de Olá verifica imediatamente toosee se o nome de Olá está disponível.</span><span class="sxs-lookup"><span data-stu-id="be135-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="be135-108">Depois de efetuar o nome de espaço de nomes de Olá se estiver disponível, escolha Olá (básica, Standard ou Premium) de escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="be135-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="be135-109">No Olá **subscrição** campo, escolha uma subscrição do Azure no espaço de nomes de Olá que toocreate.</span><span class="sxs-lookup"><span data-stu-id="be135-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="be135-110">No Olá **grupo de recursos** campo, escolha um grupo de recursos existente na qual Olá espaço de nomes em direto ou, crie um novo.</span><span class="sxs-lookup"><span data-stu-id="be135-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="be135-111">No **localização**, escolha o país Olá ou região onde será alojado o espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="be135-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Create namespace][create-namespace]
8. <span data-ttu-id="be135-113">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="be135-113">Click **Create**.</span></span> <span data-ttu-id="be135-114">Agora, o sistema Olá cria o seu espaço de nomes e ativa-o.</span><span class="sxs-lookup"><span data-stu-id="be135-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="be135-115">Poderá ter toowait alguns minutos enquanto Olá sistema Aprovisiona recursos para a sua conta.</span><span class="sxs-lookup"><span data-stu-id="be135-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="be135-116">Obter credenciais de gestão de Olá</span><span class="sxs-lookup"><span data-stu-id="be135-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="be135-117">Na lista de Olá dos espaços de nomes, clique em Olá recém-criado espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="be135-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="be135-118">No painel de espaço de nomes de Olá, clique em **políticas de acesso partilhado**.</span><span class="sxs-lookup"><span data-stu-id="be135-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="be135-119">No Olá **políticas de acesso partilhado** painel, clique em **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="be135-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="be135-121">No Olá **política: RootManageSharedAccessKey** painel, clique no botão de cópia de Olá junto demasiado**chave de cadeia – primária da ligação**, toocopy Olá ligação cadeia tooyour área de transferência para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="be135-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="be135-122">Cole este valor no Bloco de Notas ou noutra localização temporária.</span><span class="sxs-lookup"><span data-stu-id="be135-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="be135-124">Passo anterior repetida Olá, copiar e colar o valor Olá **chave primária** tooa localização temporária para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="be135-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
