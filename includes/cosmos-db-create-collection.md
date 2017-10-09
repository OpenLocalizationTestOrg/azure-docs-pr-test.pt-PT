Agora pode utilizar a ferramenta Explorador de dados de Olá no Olá toocreate do portal do Azure, uma base de dados e coleção. 

1. No Olá portal do Azure, no menu de navegação esquerdo Olá, clique em **Explorador de dados (pré-visualização)**. 

2. No Olá **Explorador de dados (pré-visualização)** painel, clique em **nova coleção**e, em seguida, fornecer Olá seguintes informações:

    ![Olá painel do Explorador de dados portal do Azure](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    Definição|Valor sugerido|Descrição
    ---|---|---
    Id da base de dados|Tarefas|nome de Olá para a sua nova base de dados. Os nomes das bases de dados devem conter de 1 a 255 carateres e não podem conter /, \\, #, ?, ou um espaço à direita.
    ID da coleção|Itens|nome de Olá para a coleção de novo. Nomes de colecção tem Olá mesmo caráter os requisitos de como os IDs de base de dados.
    Capacidade de armazenamento| Fixa (10 GB)|Utilize o valor predefinido de Olá. Este valor é a capacidade de armazenamento Olá da base de dados de Olá.
    Débito|400 RU|Utilize o valor predefinido de Olá. Se quiser tooreduce latência, pode dimensionar a débito hello mais tarde.
    Chave de partição|/categoria|Uma chave de partição que distribui dados uniformemente tooeach partição. Chave de partição correto de Olá selecionar é importante criar uma coleção de performant. toolearn mais, consulte [estruturar para criação de partições](../articles/cosmos-db/partition-data.md#designing-for-partitioning).    
3. Após concluir formulário Olá, clique em **OK**.

Mostra do Explorador de dados Olá nova base de dados e coleção. 
