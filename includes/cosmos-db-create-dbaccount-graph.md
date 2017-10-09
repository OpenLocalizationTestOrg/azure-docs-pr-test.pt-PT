1. Numa nova janela, inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. No painel esquerdo Olá, clique em **novo**, clique em **bases de dados**e, em **Azure Cosmos DB**, clique em **criar**.
   
   ![Painel da Base de Dados do portal do Azure](./media/cosmos-db-create-dbaccount-graph/create-nosql-db-databases-json-tutorial-1.png)

3. No Olá **nova conta** painel, especificar a configuração de Olá que pretende para esta conta de base de dados do Azure Cosmos. 

    Com o Azure Cosmos DB, pode escolher um de quatro modelos de programação: Gremlin (gráficos), MongoDB, SQL (DocumentDB) e Table (chave-valor), em que cada um requer uma conta separada.
       
    Este artigo de início rápido, iremos programa contra Olá Graph API, por isso, escolha **Gremlin (gráfico)** como preencher o formulário de Olá. Se tiver dados de documentos de aplicações de catálogos, dados de chaves/valores (tabela) ou dados migrados de aplicações MongoDB, tenha em conta que o Azure Cosmos DB pode proporcionar uma plataforma de serviço de bases de dados de elevada disponibilidade e distribuída globalmente para todas as aplicações críticas para a sua atividade.

    Preencha os campos de Olá no Olá **nova conta** painel, utilizando as informações de Olá no Olá seguinte captura de ecrã como um guia - os valores podem ser diferentes de valores de Olá Olá captura de ecrã.
 
    ![Painel de nova conta Olá para Azure Cosmos DB](./media/cosmos-db-create-dbaccount-graph/create-nosql-db-databases-json-tutorial-2.png)

    Definição|Valor sugerido|Descrição
    ---|---|---
    ID|*Valor exclusivo*|Um nome exclusivo que identifica esta conta do Azure Cosmos DB. Porque *documents.azure.com* é anexado toohello ID que forneçam toocreate seu URI, utilize um único, mas identificação ID. Olá ID tem de conter apenas letras minúsculas, números e carateres de hífen (-) Olá e tem de conter de 3 carateres too50.
    API|Gremlin (gráfico)|Iremos programa contra Olá [Graph API](../articles/cosmos-db/graph-introduction.md) posteriormente neste artigo.|
    Subscrição|*A sua subscrição*|Olá subscrição do Azure que pretende que toouse para esta conta de base de dados do Azure Cosmos. 
    Grupo de Recursos|*Olá mesmo valor como ID*|Olá novo nome grupo de recursos para a sua conta. Simplicidade, pode utilizar Olá mesmo nome como o seu ID. 
    Localização|*utilizadores de tooyour do Olá região mais próximos*|Olá localização geográfica na qual toohost a sua conta de base de dados do Azure Cosmos. Escolha a localização de Olá mais próximos tooyour utilizadores toogive Olá-os dados de toohello acesso mais rápidos.

4. Clique em **criar** conta de Olá toocreate.
5. Na barra de ferramentas superior de Olá, clique em Olá **notificações** ícone ![ícone de notificação de Olá](./media/cosmos-db-create-dbaccount-graph/notification-icon.png) processo de implementação de Olá toomonitor.

    ![Olá painel de notificações de portal do Azure](./media/cosmos-db-create-dbaccount-graph/notification.png)

6.  Quando a janela de notificações de Olá indica a janela de notificação do Olá implementação Olá criada com êxito, fechar e nova conta de Olá aberta de Olá **todos os recursos** mosaico Olá Dashboard. 

    ![Conta de DocumentDB no mosaico de todos os recursos de Olá](./media/cosmos-db-create-dbaccount-graph/azure-documentdb-all-resources.png)
