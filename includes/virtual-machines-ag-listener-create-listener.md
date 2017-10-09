Neste passo, cria manualmente escuta do grupo de disponibilidade Olá no Gestor de clusters de ativação pós-falha e o SQL Server Management Studio.

1. Abra o Gestor de clusters de ativação pós-falha a partir do nó de Olá que aloja a réplica primária Olá.

2. Selecione Olá **redes** nós e, em seguida, nome de rede de cluster de Olá nota. Este nome é utilizado na variável de Olá $ClusterNetworkName no Olá script do PowerShell.

3. Expanda o nome do cluster Olá e, em seguida, clique em **funções**.

4. No Olá **funções** painel, o grupo de disponibilidade de Olá contexto nome e, em seguida, selecione **adicionar recursos** > **ponto de acesso de cliente**.
   
    ![Adicionar o ponto de acesso de cliente para o grupo de disponibilidade](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. No Olá **nome** caixa, crie um nome para este novo serviço de escuta, clique em **seguinte** duas vezes e, em seguida, clique em **concluir**.  
    Não coloque o serviço de escuta de Olá ou recurso online neste momento.

6. Clique em Olá **recursos** separador e, em seguida, expanda o ponto de acesso de cliente de Olá que acabou de criar. 
    recurso de endereço IP Olá para cada rede de cluster do cluster é apresentado. Se se tratar de uma solução apenas de Azure, é apresentado apenas um recurso de endereço IP.

7. Efetue um dos seguintes Olá:
   
   * tooconfigure uma solução híbrida:
     
        a. Clique no recurso de endereço IP do Olá que corresponde à sub-rede do tooyour no local e, em seguida, selecione **propriedades**. Tenha em atenção o nome do endereço IP Olá e o nome de rede.
   
        b. Selecione **endereço IP estático**, atribua um endereço IP não utilizado e, em seguida, clique em **OK**.
 
   * tooconfigure uma solução apenas de Azure:

        a. Clique no recurso de endereço IP Olá corresponde tooyour sub-rede do Azure e, em seguida, selecione **propriedades**.
       
       > [!NOTE]
       > Se o serviço de escuta de Olá falhar posteriormente toocome online devido a um endereço IP em conflito selecionado por DHCP, pode configurar um endereço IP estático válido nesta janela de propriedades.
       > 
       > 

       b. No Olá mesmo **endereço IP** janela Propriedades, alteração Olá **nome de endereço IP**.  
        Este nome é utilizado na variável Olá $IPResourceName de Olá script do PowerShell. Se a solução abranger várias redes virtuais do Azure, repita este passo para cada recurso IP.

