### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Determinar o nome DNS Olá da máquina virtual de Olá
tooconnect toohello motor de base de dados do SQL Server, de outro computador, tem de saber Olá sistema de nomes de domínio (DNS) nome da máquina virtual de Olá. (Isto é Olá nome Olá internet utiliza tooidentify Olá máquina virtual. Pode utilizar o endereço IP Olá, mas o endereço IP Olá pode mudar quando Azure move os recursos para redundância ou manutenção. nome DNS Olá será estável porque pode ser redirecionado tooa novo endereço IP.)  

1. No Portal do Azure de Olá (ou do passo anterior Olá), selecione **máquinas virtuais (clássicas)**.
2. Selecione a sua VM do SQL.
3. No Olá **Máquina Virtual** painel, Olá cópia **nome DNS** para a máquina virtual de Olá.
   
    ![Nome DNS](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Ligar toohello motor de base de dados a partir de outro computador
1. Num computador ligado toohello internet, abra o SQL Server Management Studio.
2. No Olá **ligar tooServer** ou **ligar tooDatabase motor** Olá caixa de diálogo **nome do servidor** box, introduza o nome DNS Olá da máquina virtual de Olá (determinada na Olá tarefa anterior) e um número de porta do ponto final público no formato de Olá de *DNSName, portnumber* como **mysqlvm.cloudapp.net,57500**.
   
    ![Ligar através do SSMS](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Não se lembra número de porta do ponto final público Olá que criou anteriormente, pode encontrá-lo no Olá **pontos finais** área da Olá **Máquina Virtual** painel.
   
    ![Porta Pública](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. No Olá **autenticação** caixa, selecione **autenticação do SQL Server**.
4. No Olá **início de sessão** caixa, nome de Olá do tipo de início de sessão que criou uma tarefa anterior.
5. No Olá **palavra-passe** caixa, a palavra-passe Olá de tipo de início de sessão de Olá que criar uma tarefa anterior.
6. Clique em **Ligar**.

