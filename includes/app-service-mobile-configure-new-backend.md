
1. <span data-ttu-id="0ba5f-101">Clique em Olá **serviços aplicacionais** botão, selecione o seu back-end do Mobile Apps, selecione **início rápido**e, em seguida, selecione a plataforma de cliente (em iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="0ba5f-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Portal do Azure com Início Rápido de Aplicações Móveis realçado][quickstart]

2. <span data-ttu-id="0ba5f-103">Se não estiver configurada uma ligação de base de dados, crie um, Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="0ba5f-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![Portal do Azure com as aplicações de Mobile Connect toodatabase][connect]

    <span data-ttu-id="0ba5f-105">a.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-105">a.</span></span> <span data-ttu-id="0ba5f-106">Crie uma base de dados SQL e o servidor novos.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-106">Create a new SQL database and server.</span></span>

    ![Portal do Azure com Aplicações Móveis criar base de dados e servidor novos][server]

    <span data-ttu-id="0ba5f-108">b.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-108">b.</span></span> <span data-ttu-id="0ba5f-109">Aguarde até que a ligação de dados de Olá é criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-109">Wait until hello data connection is successfully created.</span></span>

    ![Notificação do portal do Azure de criação com êxito de ligação de dados][notification]

    <span data-ttu-id="0ba5f-111">c.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-111">c.</span></span> <span data-ttu-id="0ba5f-112">A ligação de dados tem de ser bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-112">Data connection must be successful.</span></span>

    ![Notificação do portal do Azure, "Já tem uma ligação de dados"][already-connection]

3. <span data-ttu-id="0ba5f-114">Em **2. Criar uma API de tabela**, selecione Node.js em **Linguagem do back-end**.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="0ba5f-115">Aceite a confirmação de Olá e, em seguida, selecione **criar tabela TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="0ba5f-116">Esta ação cria uma nova tabela de itens pendentes na base de dados.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="0ba5f-117">Mudar um tooNode.js de back-end existente substitui todos os conteúdos.</span><span class="sxs-lookup"><span data-stu-id="0ba5f-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="0ba5f-118">toocreate um back-end de .NET em vez disso, consulte [funcione com o servidor de back-end de .NET de Olá SDK para Mobile Apps][instructions].</span><span class="sxs-lookup"><span data-stu-id="0ba5f-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
