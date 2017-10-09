## <a name="set-up-hello-development-environment"></a>Configurar o ambiente de desenvolvimento de Olá

Esta secção explica-lhe como configurar o ambiente de desenvolvimento, incluindo a criação de uma aplicação ASP.NET MVC, adicionar uma ligação a serviços ligados, adicionar um controlador, e Olá especificação necessária diretivas de espaço de nomes.

### <a name="create-an-aspnet-mvc-app-project"></a>Criar um projeto de aplicação de ASP.NET MVC

1. Abra o Visual Studio.

1. Selecione **ficheiro -> novo -> projeto** menu principal Olá

1. No Olá **novo projeto** caixa de diálogo, especifique as opções de Olá como Olá realçado na figura a seguir:

    ![Criar projeto ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. Selecione **OK**.

1. No Olá **novo projeto ASP.NET** caixa de diálogo, especifique as opções de Olá como Olá realçado na figura a seguir:

    ![Especifique o MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. Selecione **OK**.

### <a name="use-connected-services-tooconnect-tooan-azure-storage-account"></a>Utilizar a conta de armazenamento do Azure ligado serviços tooconnect tooan

1. No Olá **Explorador de soluções**, clique no projeto Olá e, no menu de contexto de Olá, selecione **adicionar -> serviço ligado**.

1. No Olá **adicionar o serviço ligado** caixa de diálogo, selecione **Storage do Azure**e, em seguida, selecione **configurar**.

    ![Caixa de diálogo de serviço ligada](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. No Olá **Storage do Azure** caixa de diálogo, selecione Olá conta de armazenamento do Azure pretendido com a qual pretende toowork e selecione **adicionar**.
