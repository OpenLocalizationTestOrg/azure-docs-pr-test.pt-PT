1. <span data-ttu-id="f89e9-101">No Gestor de clusters de ativação pós-falha, expanda **funções**e, em seguida, realce o grupo de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="f89e9-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="f89e9-102">No Olá **recursos** separador, clique no nome do serviço de escuta de Olá e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f89e9-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="f89e9-103">Clique em Olá **dependências** separador. Se forem apresentados vários recursos, certifique-se de que os endereços IP Olá tem ou não e, dependências.</span><span class="sxs-lookup"><span data-stu-id="f89e9-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="f89e9-104">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f89e9-104">Click **OK**.</span></span>

5. <span data-ttu-id="f89e9-105">Clique no nome do serviço de escuta de Olá e, em seguida, clique em **colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="f89e9-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="f89e9-106">Depois de Olá escuta está online, no Olá **recursos** separador, clique no grupo de disponibilidade de Olá e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f89e9-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Configurar o recurso do grupo de disponibilidade Olá](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="f89e9-108">Criar uma dependência no recurso de nome de serviço de escuta de Olá (não Olá recursos nome de endereço IP) e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f89e9-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Adicione a dependência no nome do serviço de escuta de Olá](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="f89e9-110">Inicie o SQL Server Management Studio e, em seguida, ligue toohello de réplica primária.</span><span class="sxs-lookup"><span data-stu-id="f89e9-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="f89e9-111">Aceda demasiado**elevada disponibilidade do AlwaysOn** > **grupos de disponibilidade** > **\<AvailabilityGroupName\>**   >  **Serviços de escuta do grupo de disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="f89e9-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="f89e9-112">nome do serviço de escuta de Olá que criou no Gestor de clusters de ativação pós-falha deve ser apresentado.</span><span class="sxs-lookup"><span data-stu-id="f89e9-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="f89e9-113">Clique no nome do serviço de escuta de Olá e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f89e9-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="f89e9-114">No Olá **porta** caixa, especifique o número de porta de escuta do grupo de disponibilidade de Olá Olá utilizando Olá $EndpointPort que utilizou anteriormente (neste tutorial, 1433 foi predefinido Olá) e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f89e9-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

