1. No Gestor de clusters de ativação pós-falha, expanda **funções**e, em seguida, realce o grupo de disponibilidade.  

2. No Olá **recursos** separador, clique no nome do serviço de escuta de Olá e, em seguida, clique em **propriedades**.

3. Clique em Olá **dependências** separador. Se forem apresentados vários recursos, certifique-se de que os endereços IP Olá tem ou não e, dependências.  

4. Clique em **OK**.

5. Clique no nome do serviço de escuta de Olá e, em seguida, clique em **colocar Online**.

6. Depois de Olá escuta está online, no Olá **recursos** separador, clique no grupo de disponibilidade de Olá e, em seguida, clique em **propriedades**.
   
    ![Configurar o recurso do grupo de disponibilidade Olá](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Criar uma dependência no recurso de nome de serviço de escuta de Olá (não Olá recursos nome de endereço IP) e, em seguida, clique em **OK**.
   
    ![Adicione a dependência no nome do serviço de escuta de Olá](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. Inicie o SQL Server Management Studio e, em seguida, ligue toohello de réplica primária.

9. Aceda demasiado**elevada disponibilidade do AlwaysOn** > **grupos de disponibilidade** > **\<AvailabilityGroupName\>**   >  **Serviços de escuta do grupo de disponibilidade**.  
    nome do serviço de escuta de Olá que criou no Gestor de clusters de ativação pós-falha deve ser apresentado.

10. Clique no nome do serviço de escuta de Olá e, em seguida, clique em **propriedades**.

11. No Olá **porta** caixa, especifique o número de porta de escuta do grupo de disponibilidade de Olá Olá utilizando Olá $EndpointPort que utilizou anteriormente (neste tutorial, 1433 foi predefinido Olá) e, em seguida, clique em **OK**.

