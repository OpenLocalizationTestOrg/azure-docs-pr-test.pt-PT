## <a name="set-up-hello-development-environment"></a><span data-ttu-id="1b7bf-101">Configurar o ambiente de desenvolvimento de Olá</span><span class="sxs-lookup"><span data-stu-id="1b7bf-101">Set up hello development environment</span></span>

<span data-ttu-id="1b7bf-102">Esta secção explica-lhe como configurar o ambiente de desenvolvimento, incluindo a criação de uma aplicação ASP.NET MVC, adicionar uma ligação a serviços ligados, adicionar um controlador, e Olá especificação necessária diretivas de espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying hello required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="1b7bf-103">Criar um projeto de aplicação de ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="1b7bf-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="1b7bf-104">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="1b7bf-105">Selecione **ficheiro -> novo -> projeto** menu principal Olá</span><span class="sxs-lookup"><span data-stu-id="1b7bf-105">Select **File->New->Project** from hello main menu</span></span>

1. <span data-ttu-id="1b7bf-106">No Olá **novo projeto** caixa de diálogo, especifique as opções de Olá como Olá realçado na figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-106">On hello **New Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Criar projeto ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="1b7bf-108">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-108">Select **OK**.</span></span>

1. <span data-ttu-id="1b7bf-109">No Olá **novo projeto ASP.NET** caixa de diálogo, especifique as opções de Olá como Olá realçado na figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-109">On hello **New ASP.NET Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Especifique o MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="1b7bf-111">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-111">Select **OK**.</span></span>

### <a name="use-connected-services-tooconnect-tooan-azure-storage-account"></a><span data-ttu-id="1b7bf-112">Utilizar a conta de armazenamento do Azure ligado serviços tooconnect tooan</span><span class="sxs-lookup"><span data-stu-id="1b7bf-112">Use Connected Services tooconnect tooan Azure storage account</span></span>

1. <span data-ttu-id="1b7bf-113">No Olá **Explorador de soluções**, clique no projeto Olá e, no menu de contexto de Olá, selecione **adicionar -> serviço ligado**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-113">In hello **Solution Explorer**, right-click hello project, and from hello context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="1b7bf-114">No Olá **adicionar o serviço ligado** caixa de diálogo, selecione **Storage do Azure**e, em seguida, selecione **configurar**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-114">On hello **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Caixa de diálogo de serviço ligada](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="1b7bf-116">No Olá **Storage do Azure** caixa de diálogo, selecione Olá conta de armazenamento do Azure pretendido com a qual pretende toowork e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-116">On hello **Azure Storage** dialog, select hello desired Azure storage account with which you want toowork, and select **Add**.</span></span>
