### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="db875-101">Criar um novo servidor SQL lógico no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="db875-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="db875-102">Clique em **Novo**, procure **servidor lógico** e prima **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="db875-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![procurar servidor lógico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="db875-104">Selecione **Servidor SQL (servidor lógico)**</span><span class="sxs-lookup"><span data-stu-id="db875-104">Select **SQL server (logical server)**</span></span> 

    ![selecionar servidor lógico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="db875-106">Clique em **criar** tooopen Olá novo SQL Server (servidor lógico) painel.</span><span class="sxs-lookup"><span data-stu-id="db875-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="db875-107"><kbd>![abrir o painel do servidor lógico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![painel do servidor lógico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="db875-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="db875-108">Na caixa de texto nome do servidor do painel do SQL Server (servidor lógico) de Olá, forneça um nome válido para o novo servidor lógico Olá.</span><span class="sxs-lookup"><span data-stu-id="db875-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="db875-109">Uma marca de verificação verde indica que forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="db875-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![novo nome do servidor](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="db875-111">Olá nome completamente qualificado para o novo servidor irá ser < your_server_name >. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="db875-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="db875-112">Na caixa de texto do Olá servidor admin início de sessão, forneça um nome de utilizador para início de sessão de autenticação de SQL de Olá para este servidor.</span><span class="sxs-lookup"><span data-stu-id="db875-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="db875-113">Este início de sessão é conhecido como início de sessão do Olá servidor principal.</span><span class="sxs-lookup"><span data-stu-id="db875-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="db875-114">Uma marca de verificação verde indica que forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="db875-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![início de sessão de administrador SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="db875-116">No Olá **palavra-passe** e **Confirmar palavra-passe** caixas de texto, forneça uma palavra-passe da conta de início de sessão principal do servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="db875-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="db875-117">Uma marca de verificação verde indica que forneceu uma palavra-passe válida.</span><span class="sxs-lookup"><span data-stu-id="db875-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![palavra-passe de administrador SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="db875-119">Selecione uma subscrição na qual tenha objetos toocreate de permissão.</span><span class="sxs-lookup"><span data-stu-id="db875-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![subscrição](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="db875-121">Na caixa de texto do grupo de recursos do Olá, selecione **criar nova** e, em seguida, na caixa de texto do grupo de recursos do Olá, forneça um nome válido para Olá novo grupo de recursos (também pode utilizar um grupo de recursos existente se já tiver criado uma por si).</span><span class="sxs-lookup"><span data-stu-id="db875-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="db875-122">Uma marca de verificação verde indica que forneceu um nome válido.</span><span class="sxs-lookup"><span data-stu-id="db875-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![novo grupo de recursos](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="db875-124">No Olá **localização** caixa de texto, selecione uma data center localização de tooyour apropriado - por exemplo, "Leste da Austrália".</span><span class="sxs-lookup"><span data-stu-id="db875-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![localização do servidor](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="db875-126">Olá caixa de verificação **servidor de tooaccess de serviços do azure permitir** não pode ser alterada neste painel.</span><span class="sxs-lookup"><span data-stu-id="db875-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="db875-127">Pode alterar esta definição no painel de firewall do servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="db875-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="db875-128">Para obter mais informações, veja o artigo [Introdução à segurança](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db875-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="db875-129">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="db875-129">Click **Create**.</span></span>

    ![botão criar](./media/sql-data-warehouse-create-logical-server/create.png)

