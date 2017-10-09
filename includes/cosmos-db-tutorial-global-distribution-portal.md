
Pode saber sobre a base de dados do Azure Cosmos distribuição global neste Azure sexta-feira vídeo com autoria de Scott Hanselman e o Gestor de engenharia do Principal Karthik Raman.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Para obter mais informações sobre a replicação de base de dados como global funciona na base de dados do Cosmos, consulte [distribuir dados globalmente com Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Adicionar regiões de base de dados global utilizando Olá Portal do Azure
BD do Cosmos do Azure está disponível em todos os [regiões do Azure] [ azureregions] em todo o mundo. Depois de selecionar o nível de consistência Olá predefinido para a sua conta de base de dados, pode associar um ou mais regiões (dependendo da sua escolha de necessidades de distribuição global e nível de consistência predefinida).

1. No Olá [portal do Azure](https://portal.azure.com/), no Olá barra à esquerda, clique em **Azure Cosmos DB**.
2. No Olá **Azure Cosmos DB** painel, toomodify de conta de base de dados de Olá selecione.
3. No painel de conta Olá, clique em **replicar dados globalmente** menu Olá.
4. No Olá **replicar dados globalmente** painel, selecione Olá regiões tooadd ou remova ao clicar em regiões no mapa de Olá e, em seguida, clique em **guardar**. Há um regiões de tooadding custo, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/documentdb/) ou Olá [distribuir dados globalmente com o DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) artigo para obter mais informações.
   
    ![Clique em regiões Olá no Olá mapa tooadd ou removê-las][1]
    
Depois de adicionar uma segunda região, Olá **ativação pós-falha do Manual** opção está ativada no Olá **replicar dados globalmente** painel no portal de Olá. Pode utilizar este processo de ativação pós-falha do opção tootest Olá ou alterar a região de escrita primário Olá. Depois de adicionar uma região terceira, Olá **prioridades de ativação pós-falha** opção está ativada no Olá mesmo painel para que o pode alterar a ordem de ativação pós-falha de Olá para leituras.  

### <a name="selecting-global-database-regions"></a>A seleção de regiões de base de dados globais
Existem dois cenários comuns para configurar dois ou mais regiões:

1. Entrega de acesso de latência baixa toodata tooend utilizadores, independentemente de onde estão localizados em torno globo Olá
2. Adicionar regional resiliência de continuidade do negócio e recuperação após desastre (BCDR)

Para entrega de latência baixa tooend-utilizadores, é recomendado toodeploy ambos Olá aplicação e adicione a BD do Cosmos Azure em regiões Olá que é correspondem utilizadores da aplicação Olá toowhere estão localizados.

Para BCDR, recomenda-se regiões tooadd com base em pares de região Olá descritos Olá [recuperação de continuidade e desastre de negócio (BCDR): Azure emparelhado regiões] [ bcdr] artigo.

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
