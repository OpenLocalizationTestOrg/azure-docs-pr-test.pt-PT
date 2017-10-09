## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a>Como toocreate uma VNet clássica no Olá portal do Azure
toocreate uma VNet clássica com base no cenário de Olá acima, siga os passos de Olá abaixo.

1. Num browser, navegue toohttp://portal.azure.com e, se necessário, inicie sessão com a sua conta do Azure.
2. Clique em **novo** > **redes** > **rede Virtual**, tenha em atenção que Olá **selecionar um modelo de implementação** já lista mostra **clássico**e, em seguida, clique em **criar**, como mostrado na figura Olá abaixo.
   
    ![Criar a VNet no Portal do Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. No Olá **rede Virtual** painel, Olá tipo **nome** de Olá VNet e clique em **espaço de endereços**. Configure as definições de espaço de endereço para Olá VNet e a primeira sub-rede, em seguida, clique em **OK**. a figura Olá abaixo mostra as definições do bloco CIDR Olá para o nosso cenário.
   
    ![Painel de espaço de endereço](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. Clique em **grupo de recursos** e selecione um tooadd do grupo de recursos Olá VNet ou clique em **criar novo grupo de recursos** tooadd Olá VNet tooa novo grupo de recursos. Olá ilustração abaixo mostra Olá recursos definições de grupo para um novo grupo de recursos chamado **TestRG**. Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
   
    ![Criar painel do grupo de recursos](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. Se necessário, altere Olá **subscrição** e **localização** definições para a sua VNet. 
6. Se não quiser toosee Olá VNet como um mosaico no Olá **Startboard**, desativar **Pin tooStartboard**. 
7. Clique em **criar** e o aviso Olá mosaico com o nome **criar rede Virtual** conforme mostrado na figura Olá abaixo.
   
    ![Criar a VNet no portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. Aguarde Olá toobe VNet criada e quando for apresentada Olá mosaico abaixo, clique nela tooadd mais sub-redes.
   
    ![Criar a VNet no portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. Deverá ver Olá **configuração** para a sua VNet, como mostrado abaixo. 
   
    ![Criar a VNet no portal](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. Clique em **sub-redes** > **adicionar**, em seguida, escreva um **nome** e especifique um **(bloco CIDR) do intervalo de endereços** para a sub-rede e, em seguida, Clique em **OK**. a figura Olá abaixo mostra as definições de Olá para o nosso cenário atual.
    
    ![Criar a VNet no Portal do Azure](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

