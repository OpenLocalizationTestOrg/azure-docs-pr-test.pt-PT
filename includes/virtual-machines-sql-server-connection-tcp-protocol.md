1. Enquanto a máquina virtual de toohello ligado com o ambiente de trabalho remoto, procure **do Configuration Manager**:

    ![Abrir o SSCM](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. No Gestor de configuração de servidor de SQL Server, no painel de consola Olá, expanda **configuração de rede do SQL Server**.

1. No painel de consola Olá, clique em **protocolos para MSSQLSERVER** (Olá nome da instância predefinida.) No painel de detalhes de Olá, faça duplo clique **TCP** e clique em **ativar** caso não ainda esteja ativado.

    ![Ativar TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. No painel de consola Olá, clique em **do SQL Server Services**. No painel de detalhes de Olá, faça duplo clique  **do SQL Server (*nome da instância*) * * (é a instância predefinida de Olá **SQL Server (MSSQLSERVER)**) e, em seguida, clique em **reiniciar** , instância de Olá toostop e reinício do SQL Server.

    ![Reiniciar o Motor de Base de Dados](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Feche o Gestor de Configuração do SQL Server.

Para obter mais informações sobre como ativar protocolos para Olá motor de base de dados do SQL Server, consulte [ativar ou desativar um protocolo de rede do servidor](http://msdn.microsoft.com/library/ms191294.aspx).
