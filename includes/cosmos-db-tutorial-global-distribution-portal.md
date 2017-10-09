
<span data-ttu-id="51c25-101">Pode saber sobre a base de dados do Azure Cosmos distribuição global neste Azure sexta-feira vídeo com autoria de Scott Hanselman e o Gestor de engenharia do Principal Karthik Raman.</span><span class="sxs-lookup"><span data-stu-id="51c25-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="51c25-102">Para obter mais informações sobre a replicação de base de dados como global funciona na base de dados do Cosmos, consulte [distribuir dados globalmente com Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="51c25-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="51c25-103"><a id="addregion"></a>Adicionar regiões de base de dados global utilizando Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="51c25-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="51c25-104">BD do Cosmos do Azure está disponível em todos os [regiões do Azure] [ azureregions] em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="51c25-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="51c25-105">Depois de selecionar o nível de consistência Olá predefinido para a sua conta de base de dados, pode associar um ou mais regiões (dependendo da sua escolha de necessidades de distribuição global e nível de consistência predefinida).</span><span class="sxs-lookup"><span data-stu-id="51c25-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="51c25-106">No Olá [portal do Azure](https://portal.azure.com/), no Olá barra à esquerda, clique em **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="51c25-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="51c25-107">No Olá **Azure Cosmos DB** painel, toomodify de conta de base de dados de Olá selecione.</span><span class="sxs-lookup"><span data-stu-id="51c25-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="51c25-108">No painel de conta Olá, clique em **replicar dados globalmente** menu Olá.</span><span class="sxs-lookup"><span data-stu-id="51c25-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="51c25-109">No Olá **replicar dados globalmente** painel, selecione Olá regiões tooadd ou remova ao clicar em regiões no mapa de Olá e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="51c25-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="51c25-110">Há um regiões de tooadding custo, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/documentdb/) ou Olá [distribuir dados globalmente com o DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) artigo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="51c25-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Clique em regiões Olá no Olá mapa tooadd ou removê-las][1]
    
<span data-ttu-id="51c25-112">Depois de adicionar uma segunda região, Olá **ativação pós-falha do Manual** opção está ativada no Olá **replicar dados globalmente** painel no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="51c25-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="51c25-113">Pode utilizar este processo de ativação pós-falha do opção tootest Olá ou alterar a região de escrita primário Olá.</span><span class="sxs-lookup"><span data-stu-id="51c25-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="51c25-114">Depois de adicionar uma região terceira, Olá **prioridades de ativação pós-falha** opção está ativada no Olá mesmo painel para que o pode alterar a ordem de ativação pós-falha de Olá para leituras.</span><span class="sxs-lookup"><span data-stu-id="51c25-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="51c25-115">A seleção de regiões de base de dados globais</span><span class="sxs-lookup"><span data-stu-id="51c25-115">Selecting global database regions</span></span>
<span data-ttu-id="51c25-116">Existem dois cenários comuns para configurar dois ou mais regiões:</span><span class="sxs-lookup"><span data-stu-id="51c25-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="51c25-117">Entrega de acesso de latência baixa toodata tooend utilizadores, independentemente de onde estão localizados em torno globo Olá</span><span class="sxs-lookup"><span data-stu-id="51c25-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="51c25-118">Adicionar regional resiliência de continuidade do negócio e recuperação após desastre (BCDR)</span><span class="sxs-lookup"><span data-stu-id="51c25-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="51c25-119">Para entrega de latência baixa tooend-utilizadores, é recomendado toodeploy ambos Olá aplicação e adicione a BD do Cosmos Azure em regiões Olá que é correspondem utilizadores da aplicação Olá toowhere estão localizados.</span><span class="sxs-lookup"><span data-stu-id="51c25-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="51c25-120">Para BCDR, recomenda-se regiões tooadd com base em pares de região Olá descritos Olá [recuperação de continuidade e desastre de negócio (BCDR): Azure emparelhado regiões] [ bcdr] artigo.</span><span class="sxs-lookup"><span data-stu-id="51c25-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

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
