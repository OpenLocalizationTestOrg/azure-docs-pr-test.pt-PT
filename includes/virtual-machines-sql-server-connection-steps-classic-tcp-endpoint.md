### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Criar um ponto final TCP para a máquina virtual de Olá
Na ordem tooaccess do SQL Server de Olá internet, Olá deve ter um toolisten de ponto final para comunicação de TCP recebidas. Este passo de configuração do Azure, direciona entrada TCP porta tráfego tooa a porta TCP que seja acessível toohello máquina.

> [!NOTE]
> Se estiver a ligar dentro Olá mesma rede virtual ou serviço de nuvem, não dispõe de toocreate um ponto final acessível publicamente. Nesse caso, pode continuar toohello próximo passo. Para obter mais informações, veja [Cenários de Ligação](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).
> 
> 

1. No Portal do Azure Olá, selecione **máquinas virtuais (clássicas)**.
2. Em seguida, selecione a máquina virtual do SQL Server.
3. Selecione **pontos finais**e, em seguida, clique em Olá **adicionar** botão, Olá parte superior do painel de pontos finais de Olá.
   
    ![Passos do Portal para Criar um Ponto Final](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. No Olá **adicionar ponto final** painel, forneça um **nome** como SQLEndpoint.
5. Selecione **TCP** para Olá **protocolo**.
6. Para **Porta pública**, especifique um número de porta, como **57500**.
7. Para **porta privada**, especifique a porta escuta do SQL Server que está predefinida demasiado**1433**.
8. Clique em **Ok** ponto final de Olá toocreate.

