<span data-ttu-id="d7906-101">Neste passo, cria manualmente escuta do grupo de disponibilidade Olá no Gestor de clusters de ativação pós-falha e o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="d7906-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="d7906-102">Abra o Gestor de clusters de ativação pós-falha a partir do nó de Olá que aloja a réplica primária Olá.</span><span class="sxs-lookup"><span data-stu-id="d7906-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="d7906-103">Selecione Olá **redes** nós e, em seguida, nome de rede de cluster de Olá nota.</span><span class="sxs-lookup"><span data-stu-id="d7906-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="d7906-104">Este nome é utilizado na variável de Olá $ClusterNetworkName no Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7906-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="d7906-105">Expanda o nome do cluster Olá e, em seguida, clique em **funções**.</span><span class="sxs-lookup"><span data-stu-id="d7906-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="d7906-106">No Olá **funções** painel, o grupo de disponibilidade de Olá contexto nome e, em seguida, selecione **adicionar recursos** > **ponto de acesso de cliente**.</span><span class="sxs-lookup"><span data-stu-id="d7906-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Adicionar o ponto de acesso de cliente para o grupo de disponibilidade](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="d7906-108">No Olá **nome** caixa, crie um nome para este novo serviço de escuta, clique em **seguinte** duas vezes e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="d7906-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="d7906-109">Não coloque o serviço de escuta de Olá ou recurso online neste momento.</span><span class="sxs-lookup"><span data-stu-id="d7906-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="d7906-110">Clique em Olá **recursos** separador e, em seguida, expanda o ponto de acesso de cliente de Olá que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="d7906-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="d7906-111">recurso de endereço IP Olá para cada rede de cluster do cluster é apresentado.</span><span class="sxs-lookup"><span data-stu-id="d7906-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="d7906-112">Se se tratar de uma solução apenas de Azure, é apresentado apenas um recurso de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="d7906-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="d7906-113">Efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="d7906-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="d7906-114">tooconfigure uma solução híbrida:</span><span class="sxs-lookup"><span data-stu-id="d7906-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="d7906-115">a.</span><span class="sxs-lookup"><span data-stu-id="d7906-115">a.</span></span> <span data-ttu-id="d7906-116">Clique no recurso de endereço IP do Olá que corresponde à sub-rede do tooyour no local e, em seguida, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d7906-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="d7906-117">Tenha em atenção o nome do endereço IP Olá e o nome de rede.</span><span class="sxs-lookup"><span data-stu-id="d7906-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="d7906-118">b.</span><span class="sxs-lookup"><span data-stu-id="d7906-118">b.</span></span> <span data-ttu-id="d7906-119">Selecione **endereço IP estático**, atribua um endereço IP não utilizado e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7906-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="d7906-120">tooconfigure uma solução apenas de Azure:</span><span class="sxs-lookup"><span data-stu-id="d7906-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="d7906-121">a.</span><span class="sxs-lookup"><span data-stu-id="d7906-121">a.</span></span> <span data-ttu-id="d7906-122">Clique no recurso de endereço IP Olá corresponde tooyour sub-rede do Azure e, em seguida, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d7906-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="d7906-123">Se o serviço de escuta de Olá falhar posteriormente toocome online devido a um endereço IP em conflito selecionado por DHCP, pode configurar um endereço IP estático válido nesta janela de propriedades.</span><span class="sxs-lookup"><span data-stu-id="d7906-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="d7906-124">b.</span><span class="sxs-lookup"><span data-stu-id="d7906-124">b.</span></span> <span data-ttu-id="d7906-125">No Olá mesmo **endereço IP** janela Propriedades, alteração Olá **nome de endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="d7906-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="d7906-126">Este nome é utilizado na variável Olá $IPResourceName de Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7906-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="d7906-127">Se a solução abranger várias redes virtuais do Azure, repita este passo para cada recurso IP.</span><span class="sxs-lookup"><span data-stu-id="d7906-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

