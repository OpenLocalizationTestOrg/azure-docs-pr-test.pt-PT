### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Criar um novo servidor SQL lógico no Olá portal do Azure

1. Clique em **Novo**, procure **servidor lógico** e prima **ENTER**.

    ![procurar servidor lógico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. Selecione **Servidor SQL (servidor lógico)** 

    ![selecionar servidor lógico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Clique em **criar** tooopen Olá novo SQL Server (servidor lógico) painel.

   <kbd>![abrir o painel do servidor lógico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![painel do servidor lógico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. Na caixa de texto nome do servidor do painel do SQL Server (servidor lógico) de Olá, forneça um nome válido para o novo servidor lógico Olá. Uma marca de verificação verde indica que forneceu um nome válido.
    
    ![novo nome do servidor](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Olá nome completamente qualificado para o novo servidor irá ser < your_server_name >. database.windows.net.
    >
    
4. Na caixa de texto do Olá servidor admin início de sessão, forneça um nome de utilizador para início de sessão de autenticação de SQL de Olá para este servidor. Este início de sessão é conhecido como início de sessão do Olá servidor principal. Uma marca de verificação verde indica que forneceu um nome válido.
    
    ![início de sessão de administrador SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. No Olá **palavra-passe** e **Confirmar palavra-passe** caixas de texto, forneça uma palavra-passe da conta de início de sessão principal do servidor de Olá. Uma marca de verificação verde indica que forneceu uma palavra-passe válida.
    
    ![palavra-passe de administrador SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. Selecione uma subscrição na qual tenha objetos toocreate de permissão.

    ![subscrição](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. Na caixa de texto do grupo de recursos do Olá, selecione **criar nova** e, em seguida, na caixa de texto do grupo de recursos do Olá, forneça um nome válido para Olá novo grupo de recursos (também pode utilizar um grupo de recursos existente se já tiver criado uma por si). Uma marca de verificação verde indica que forneceu um nome válido.

    ![novo grupo de recursos](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. No Olá **localização** caixa de texto, selecione uma data center localização de tooyour apropriado - por exemplo, "Leste da Austrália".
    
    ![localização do servidor](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > Olá caixa de verificação **servidor de tooaccess de serviços do azure permitir** não pode ser alterada neste painel. Pode alterar esta definição no painel de firewall do servidor de Olá. Para obter mais informações, veja o artigo [Introdução à segurança](../articles/sql-database/sql-database-manage-servers-portal.md).
    >
    
9. Clique em **Criar**.

    ![botão criar](./media/sql-data-warehouse-create-logical-server/create.png)

