Agora, pode utilizar a ferramenta Explorador de dados de Olá no Olá toocreate do portal do Azure, uma base de dados do gráfico. 

1. No Olá portal do Azure, no menu de navegação esquerdo Olá, clique em **Explorador de dados (pré-visualização)**. 
2. No Olá **Explorador de dados (pré-visualização)** painel, clique em **gráfico novo**, em seguida, preencha a página Olá utilizando Olá informações a seguir.

    ![Explorador de dados no Olá portal do Azure](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    Definição|Valor sugerido|Descrição
    ---|---|---
    Id da base de dados|base de dados de exemplo|Olá ID para a sua nova base de dados. Os nomes das bases de dados têm de ter entre um e 255 carateres e não podem conter `/ \ # ?` nem espaços à direita.
    ID do gráfico|gráfico de exemplo|ID de Olá para o novo gráfico. Os nomes de gráfico têm Olá requisitos mesmo caráter como ids de base de dados.
    Capacidade de Armazenamento| 10 GB|Deixe o valor predefinido de Olá. Esta é a capacidade de armazenamento Olá da base de dados de Olá.
    Débito|400 RUs|Deixe o valor predefinido de Olá. Pode dimensionar débito hello mais tarde se quiser tooreduce latência.
    Chave de partição|/userid|Uma chave de partição que será a distribuir uniformemente dados tooeach partição. Selecionar Olá correto de chave de partição é importante criar uma performant graph, leia mais acerca do mesmo no [estruturar para criação de partições](../articles/cosmos-db/partition-data.md#designing-for-partitioning).

3. Depois do formulário de Olá é preenchido, clique em **OK**.
