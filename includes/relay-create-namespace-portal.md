1. <span data-ttu-id="c2c49-101">Inicie sessão no toohello [portal do Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="c2c49-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="c2c49-102">No painel de navegação esquerdo Olá do portal de Olá, clique em **novo**, em seguida, clique em **integração empresarial com**e, em seguida, clique em **reencaminhamento**.</span><span class="sxs-lookup"><span data-stu-id="c2c49-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="c2c49-103">No Olá **criar espaço de nomes** caixa de diálogo, introduza um nome de espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="c2c49-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="c2c49-104">sistema de Olá verifica imediatamente toosee se o nome de Olá está disponível.</span><span class="sxs-lookup"><span data-stu-id="c2c49-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="c2c49-105">No Olá **subscrição** campo, escolha uma subscrição do Azure no espaço de nomes de Olá que toocreate.</span><span class="sxs-lookup"><span data-stu-id="c2c49-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="c2c49-106">No Olá  **[grupo de recursos](../articles/azure-resource-manager/resource-group-portal.md)**  campo, escolha um grupo de recursos existente na qual Olá espaço de nomes em direto ou, crie um novo.</span><span class="sxs-lookup"><span data-stu-id="c2c49-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="c2c49-107">No **localização**, escolha o país Olá ou região onde será alojado o espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="c2c49-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Create namespace][create-namespace]
7. <span data-ttu-id="c2c49-109">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c2c49-109">Click **Create**.</span></span> <span data-ttu-id="c2c49-110">Agora, o sistema Olá cria o seu espaço de nomes e ativa-o.</span><span class="sxs-lookup"><span data-stu-id="c2c49-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="c2c49-111">Após alguns minutos, Olá sistema Aprovisiona recursos para a sua conta.</span><span class="sxs-lookup"><span data-stu-id="c2c49-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="c2c49-112">Obter credenciais de gestão de Olá</span><span class="sxs-lookup"><span data-stu-id="c2c49-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="c2c49-113">Na lista de Olá dos espaços de nomes, clique em Olá recém-criado espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="c2c49-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="c2c49-114">No painel de espaço de nomes de Olá, clique em **políticas de acesso partilhado**.</span><span class="sxs-lookup"><span data-stu-id="c2c49-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="c2c49-115">No Olá **políticas de acesso partilhado** painel, clique em **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="c2c49-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="c2c49-117">No Olá **política: RootManageSharedAccessKey** painel, clique no botão de cópia de Olá junto demasiado**chave de cadeia – primária da ligação**, toocopy Olá ligação cadeia tooyour área de transferência para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="c2c49-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="c2c49-118">Cole este valor no Bloco de Notas ou noutra localização temporária.</span><span class="sxs-lookup"><span data-stu-id="c2c49-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="c2c49-120">Passo anterior repetida Olá, copiar e colar o valor Olá **chave primária** tooa localização temporária para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="c2c49-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
