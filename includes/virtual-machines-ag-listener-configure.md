<span data-ttu-id="59c20-101">escuta do grupo de disponibilidade de Olá é um nome de rede e endereços IP que hello do SQL Server escuta a grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="59c20-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="59c20-102">escuta do grupo de disponibilidade Olá de toocreate, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="59c20-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="59c20-103"><a name="getnet"></a>Obter o nome de Olá Olá rede do recurso do cluster.</span><span class="sxs-lookup"><span data-stu-id="59c20-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="59c20-104">a.</span><span class="sxs-lookup"><span data-stu-id="59c20-104">a.</span></span> <span data-ttu-id="59c20-105">Utilize o RDP tooconnect toohello máquina virtual do Azure que aloja a réplica primária Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="59c20-106">b.</span><span class="sxs-lookup"><span data-stu-id="59c20-106">b.</span></span> <span data-ttu-id="59c20-107">Abra o Gestor de clusters de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="59c20-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="59c20-108">c.</span><span class="sxs-lookup"><span data-stu-id="59c20-108">c.</span></span> <span data-ttu-id="59c20-109">Selecione Olá **redes** nós e o nome de rede de cluster de Olá nota.</span><span class="sxs-lookup"><span data-stu-id="59c20-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="59c20-110">Utilize este nome no Olá `$ClusterNetworkName` variável na Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59c20-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="59c20-111">Olá seguir o nome de rede de cluster de Olá de imagem é **rede de Cluster 1**:</span><span class="sxs-lookup"><span data-stu-id="59c20-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![Nome de rede de cluster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="59c20-113"><a name="addcap"></a>Adicione o ponto de acesso de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="59c20-114">ponto de acesso de cliente Olá é o nome de rede de Olá que as aplicações utilizar bases de dados do tooconnect toohello num grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="59c20-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="59c20-115">Crie ponto de acesso de cliente Olá no Gestor de clusters de ativação pós-falha.</span><span class="sxs-lookup"><span data-stu-id="59c20-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="59c20-116">a.</span><span class="sxs-lookup"><span data-stu-id="59c20-116">a.</span></span> <span data-ttu-id="59c20-117">Expanda o nome do cluster Olá e, em seguida, clique em **funções**.</span><span class="sxs-lookup"><span data-stu-id="59c20-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="59c20-118">b.</span><span class="sxs-lookup"><span data-stu-id="59c20-118">b.</span></span> <span data-ttu-id="59c20-119">No Olá **funções** painel, o grupo de disponibilidade de Olá contexto nome e, em seguida, selecione **adicionar recursos** > **ponto de acesso de cliente**.</span><span class="sxs-lookup"><span data-stu-id="59c20-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Ponto de acesso de cliente](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="59c20-121">c.</span><span class="sxs-lookup"><span data-stu-id="59c20-121">c.</span></span> <span data-ttu-id="59c20-122">No Olá **nome** caixa, crie um nome para este novo serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="59c20-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="59c20-123">nome de Olá para o novo serviço de escuta Olá é o nome de rede de Olá que aplicações utilizam tooconnect toodatabases no grupo de disponibilidade do SQL Server Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="59c20-124">d.</span><span class="sxs-lookup"><span data-stu-id="59c20-124">d.</span></span> <span data-ttu-id="59c20-125">Clique em toofinish criar Olá serviço de escuta **seguinte** duas vezes e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="59c20-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="59c20-126">Não coloque o serviço de escuta de Olá ou recurso online neste momento.</span><span class="sxs-lookup"><span data-stu-id="59c20-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="59c20-127"><a name="congroup"></a>Configure o recurso de IP Olá Olá grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="59c20-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="59c20-128">a.</span><span class="sxs-lookup"><span data-stu-id="59c20-128">a.</span></span> <span data-ttu-id="59c20-129">Clique em Olá **recursos** separador e, em seguida, expanda o ponto de acesso de cliente de Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="59c20-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="59c20-130">ponto de acesso de cliente Olá está offline.</span><span class="sxs-lookup"><span data-stu-id="59c20-130">hello client access point is offline.</span></span>

   ![Ponto de acesso de cliente](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="59c20-132">b.</span><span class="sxs-lookup"><span data-stu-id="59c20-132">b.</span></span> <span data-ttu-id="59c20-133">Clique no recurso de IP Olá e, em seguida, clique em propriedades.</span><span class="sxs-lookup"><span data-stu-id="59c20-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="59c20-134">Anote o nome de Olá do endereço IP de Olá e utilizá-lo em Olá `$IPResourceName` variável na Olá script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59c20-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="59c20-135">c.</span><span class="sxs-lookup"><span data-stu-id="59c20-135">c.</span></span> <span data-ttu-id="59c20-136">Em **endereço IP**, clique em **endereço IP estático**.</span><span class="sxs-lookup"><span data-stu-id="59c20-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="59c20-137">Definir o endereço IP de Olá como hello mesmo endereço que utilizou quando definiu o endereço de Balanceador de carga Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="59c20-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="59c20-139"><a name = "dependencyGroup"></a>Faça com que o recurso do grupo de disponibilidade de SQL Server Olá dependa Olá ponto de acesso de cliente.</span><span class="sxs-lookup"><span data-stu-id="59c20-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="59c20-140">a.</span><span class="sxs-lookup"><span data-stu-id="59c20-140">a.</span></span> <span data-ttu-id="59c20-141">No Gestor de clusters de ativação pós-falha, clique em **funções**e, em seguida, clique em seu grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="59c20-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="59c20-142">b.</span><span class="sxs-lookup"><span data-stu-id="59c20-142">b.</span></span> <span data-ttu-id="59c20-143">No Olá **recursos** separador em **outros recursos**, clique no grupo de recursos de disponibilidade de Olá e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="59c20-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="59c20-144">c.</span><span class="sxs-lookup"><span data-stu-id="59c20-144">c.</span></span> <span data-ttu-id="59c20-145">No separador de dependências de Olá, adicione o nome de Olá do recurso de ponto (serviço de escuta Olá) de acesso de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="59c20-147">d.</span><span class="sxs-lookup"><span data-stu-id="59c20-147">d.</span></span> <span data-ttu-id="59c20-148">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="59c20-148">Click **OK**.</span></span>

5. <span data-ttu-id="59c20-149"><a name="listname"></a>Se o acesso de cliente Olá recursos dependentes no endereço IP Olá do ponto.</span><span class="sxs-lookup"><span data-stu-id="59c20-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="59c20-150">a.</span><span class="sxs-lookup"><span data-stu-id="59c20-150">a.</span></span> <span data-ttu-id="59c20-151">No Gestor de clusters de ativação pós-falha, clique em **funções**e, em seguida, clique em seu grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="59c20-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="59c20-152">b.</span><span class="sxs-lookup"><span data-stu-id="59c20-152">b.</span></span> <span data-ttu-id="59c20-153">No Olá **recursos** separador, clique no recurso do ponto de acesso de cliente do Olá sob **nome do servidor**e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="59c20-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="59c20-155">c.</span><span class="sxs-lookup"><span data-stu-id="59c20-155">c.</span></span> <span data-ttu-id="59c20-156">Clique em Olá **dependências** separador. Certifique-se de que o endereço IP de Olá é uma dependência.</span><span class="sxs-lookup"><span data-stu-id="59c20-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="59c20-157">Se não for, defina uma dependência no endereço IP Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="59c20-158">Se existirem vários recursos listados, certifique-se de que os endereços IP Olá tem ou não e, dependências.</span><span class="sxs-lookup"><span data-stu-id="59c20-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="59c20-159">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="59c20-159">Click **OK**.</span></span> 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="59c20-161">d.</span><span class="sxs-lookup"><span data-stu-id="59c20-161">d.</span></span> <span data-ttu-id="59c20-162">Clique no nome do serviço de escuta de Olá e, em seguida, clique em **colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="59c20-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="59c20-163">Pode validar que Olá dependências estão corretamente configuradas.</span><span class="sxs-lookup"><span data-stu-id="59c20-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="59c20-164">No Gestor de clusters de ativação pós-falha, aceda tooRoles, clique no grupo de disponibilidade de Olá, clique em **mais ações**e, em seguida, clique em **Mostrar relatório de dependências**.</span><span class="sxs-lookup"><span data-stu-id="59c20-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="59c20-165">Quando se encontram corretamente configuradas dependências Olá, grupo de disponibilidade de Olá está dependente de nome de rede Olá e nome de rede Olá está dependente de endereço IP Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="59c20-166"><a name="setparam"></a>Definir os parâmetros de cluster de Olá no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59c20-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="59c20-167">a.</span><span class="sxs-lookup"><span data-stu-id="59c20-167">a.</span></span> <span data-ttu-id="59c20-168">Copie Olá seguir tooone de script do PowerShell de instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="59c20-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="59c20-169">Atualize as variáveis de Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="59c20-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="59c20-170">b.</span><span class="sxs-lookup"><span data-stu-id="59c20-170">b.</span></span> <span data-ttu-id="59c20-171">Definir os parâmetros de cluster de Olá executando Olá script do PowerShell num de nós de cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="59c20-172">Se as instâncias do SQL Server estão em diferentes regiões, terá de script do PowerShell toorun Olá duas vezes.</span><span class="sxs-lookup"><span data-stu-id="59c20-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="59c20-173">Olá pela primeira vez, utilize Olá `$ILBIP` e `$ProbePort` a região primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="59c20-174">Olá segunda vez, utilize Olá `$ILBIP` e `$ProbePort` a região segundo Olá.</span><span class="sxs-lookup"><span data-stu-id="59c20-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="59c20-175">nome de rede de cluster Olá e nome de recurso IP de cluster Olá são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="59c20-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
