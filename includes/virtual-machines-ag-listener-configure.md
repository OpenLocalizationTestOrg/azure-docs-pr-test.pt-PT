escuta do grupo de disponibilidade de Olá é um nome de rede e endereços IP que hello do SQL Server escuta a grupo de disponibilidade. escuta do grupo de disponibilidade Olá de toocreate, Olá seguintes:

1. <a name="getnet"></a>Obter o nome de Olá Olá rede do recurso do cluster.

    a. Utilize o RDP tooconnect toohello máquina virtual do Azure que aloja a réplica primária Olá. 

    b. Abra o Gestor de clusters de ativação pós-falha.

    c. Selecione Olá **redes** nós e o nome de rede de cluster de Olá nota. Utilize este nome no Olá `$ClusterNetworkName` variável na Olá script do PowerShell. Olá seguir o nome de rede de cluster de Olá de imagem é **rede de Cluster 1**:

   ![Nome de rede de cluster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>Adicione o ponto de acesso de cliente Olá.  
    ponto de acesso de cliente Olá é o nome de rede de Olá que as aplicações utilizar bases de dados do tooconnect toohello num grupo de disponibilidade. Crie ponto de acesso de cliente Olá no Gestor de clusters de ativação pós-falha.

    a. Expanda o nome do cluster Olá e, em seguida, clique em **funções**.

    b. No Olá **funções** painel, o grupo de disponibilidade de Olá contexto nome e, em seguida, selecione **adicionar recursos** > **ponto de acesso de cliente**.

   ![Ponto de acesso de cliente](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. No Olá **nome** caixa, crie um nome para este novo serviço de escuta. 
   nome de Olá para o novo serviço de escuta Olá é o nome de rede de Olá que aplicações utilizam tooconnect toodatabases no grupo de disponibilidade do SQL Server Olá.
   
    d. Clique em toofinish criar Olá serviço de escuta **seguinte** duas vezes e, em seguida, clique em **concluir**. Não coloque o serviço de escuta de Olá ou recurso online neste momento.

3. <a name="congroup"></a>Configure o recurso de IP Olá Olá grupo de disponibilidade.

    a. Clique em Olá **recursos** separador e, em seguida, expanda o ponto de acesso de cliente de Olá que criou.  
    ponto de acesso de cliente Olá está offline.

   ![Ponto de acesso de cliente](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Clique no recurso de IP Olá e, em seguida, clique em propriedades. Anote o nome de Olá do endereço IP de Olá e utilizá-lo em Olá `$IPResourceName` variável na Olá script do PowerShell.

    c. Em **endereço IP**, clique em **endereço IP estático**. Definir o endereço IP de Olá como hello mesmo endereço que utilizou quando definiu o endereço de Balanceador de carga Olá no Olá portal do Azure.

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>Faça com que o recurso do grupo de disponibilidade de SQL Server Olá dependa Olá ponto de acesso de cliente.

    a. No Gestor de clusters de ativação pós-falha, clique em **funções**e, em seguida, clique em seu grupo de disponibilidade.

    b. No Olá **recursos** separador em **outros recursos**, clique no grupo de recursos de disponibilidade de Olá e, em seguida, clique em **propriedades**. 

    c. No separador de dependências de Olá, adicione o nome de Olá do recurso de ponto (serviço de escuta Olá) de acesso de cliente Olá.

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. Clique em **OK**.

5. <a name="listname"></a>Se o acesso de cliente Olá recursos dependentes no endereço IP Olá do ponto.

    a. No Gestor de clusters de ativação pós-falha, clique em **funções**e, em seguida, clique em seu grupo de disponibilidade. 

    b. No Olá **recursos** separador, clique no recurso do ponto de acesso de cliente do Olá sob **nome do servidor**e, em seguida, clique em **propriedades**. 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. Clique em Olá **dependências** separador. Certifique-se de que o endereço IP de Olá é uma dependência. Se não for, defina uma dependência no endereço IP Olá. Se existirem vários recursos listados, certifique-se de que os endereços IP Olá tem ou não e, dependências. Clique em **OK**. 

   ![Recurso de IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Clique no nome do serviço de escuta de Olá e, em seguida, clique em **colocar Online**. 

    >[!TIP]
    >Pode validar que Olá dependências estão corretamente configuradas. No Gestor de clusters de ativação pós-falha, aceda tooRoles, clique no grupo de disponibilidade de Olá, clique em **mais ações**e, em seguida, clique em **Mostrar relatório de dependências**. Quando se encontram corretamente configuradas dependências Olá, grupo de disponibilidade de Olá está dependente de nome de rede Olá e nome de rede Olá está dependente de endereço IP Olá. 


6. <a name="setparam"></a>Definir os parâmetros de cluster de Olá no PowerShell.
    
    a. Copie Olá seguir tooone de script do PowerShell de instâncias do SQL Server. Atualize as variáveis de Olá para o seu ambiente.     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. Definir os parâmetros de cluster de Olá executando Olá script do PowerShell num de nós de cluster Olá.  

    > [!NOTE]
    > Se as instâncias do SQL Server estão em diferentes regiões, terá de script do PowerShell toorun Olá duas vezes. Olá pela primeira vez, utilize Olá `$ILBIP` e `$ProbePort` a região primeiro Olá. Olá segunda vez, utilize Olá `$ILBIP` e `$ProbePort` a região segundo Olá. nome de rede de cluster Olá e nome de recurso IP de cluster Olá são Olá mesmo. 
