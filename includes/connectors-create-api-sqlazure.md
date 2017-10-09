### <a name="prerequisites"></a>Pré-requisitos
* Uma conta do Azure; Pode criar um [conta gratuita](https://azure.microsoft.com/free)
* Um [SQL Database do Azure](../articles/sql-database/sql-database-get-started.md) com as informações da ligação, incluindo o nome do servidor Olá, o nome de base de dados e o nome de utilizador/palavra-passe. Estas informações estão incluídas no Olá cadeia de ligação de base de dados SQL:
  
    Servidor = tcp:*yoursqlservername*. database.windows.net,1433;Initial catálogo =*yourqldbname*; Manter informações de segurança = False; ID de utilizador = {your_username}; Palavra-passe = {your_password}; MultipleActiveResultSets = False; Encriptar = True; TrustServerCertificate = False; Tempo limite da ligação = 30;
  
    Leia mais sobre [bases de dados do Azure SQL](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> Quando cria uma base de dados do SQL do Azure, também pode criar bases de dados do exemplo Olá incluídos com o SQL Server. 
> 
> 

Antes de utilizar a SQL Database do Azure numa aplicação lógica, ligar tooyour base de dados SQL. Pode fazê-facilmente na sua aplicação lógica em Olá portal do Azure.  

Ligar tooyour base de dados do SQL do Azure utilizando Olá os seguintes passos:  

1. Crie uma aplicação lógica. No designer de aplicações lógicas Olá, adicione um acionador e, em seguida, adicionar uma ação. Selecione **Mostrar Microsoft APIs geridas** Olá na lista pendente e, em seguida, introduza "sql" na caixa de pesquisa de Olá. Selecione uma das ações de Olá:  
   
    ![Passo de criação de ligação do SQL Azure](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Se ainda não criou anteriormente qualquer tooSQL de ligações da base de dados, serão apresentadas para detalhes de ligação de Olá:  
   
    ![Passo de criação de ligação do SQL Azure](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Introduza os detalhes de base de dados SQL Olá. Propriedades com um asterisco são necessárias.
   
   | Propriedade | Detalhes |
   | --- | --- |
   | Ligar através do Gateway |Deixe desmarcada. Isto é utilizado quando ligar tooan no local do SQL Server. |
   | Nome da ligação * |Introduza um nome para a sua ligação. |
   | Nome do servidor SQL * |Introduza o nome do servidor Olá; qual é semelhante ao seguinte *servername.database.windows.net*. nome do servidor Olá é apresentado nas propriedades de base de dados SQL Olá na Olá portal do Azure e também na cadeia de ligação de Olá. |
   | Nome da base de dados SQL * |Introduza o nome de Olá deu a sua base de dados do SQL Server. Este é listado nas propriedades de base de dados SQL Olá na cadeia de ligação de Olá: Initial Catalog =*yoursqldbname*. |
   | Nome de utilizador * |Introduza o nome de utilizador de Olá que criou quando Olá base de dados SQL foi criado. Este é listado nas propriedades de base de dados SQL Olá na Olá portal do Azure. |
   | Palavra-passe * |Introduza a palavra-passe de Olá que criou quando Olá base de dados SQL foi criado. |
   
    Estas credenciais são utilizada tooauthorize sua tooconnect de aplicação lógica e aceder aos seus dados do SQL Server. Depois de concluído, os detalhes da sua ligação ter um aspeto semelhante toohello seguinte:  
   
    ![Passo de criação de ligação do SQL Azure](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. Selecione **Criar**. 
5. Tenha em atenção Olá ligação foi criada. Agora, pode continuar com a Olá outro passos seguintes na sua aplicação lógica: 
   
    ![Passo de criação de ligação do SQL Azure](./media/connectors-create-api-sqlazure/table.png)

