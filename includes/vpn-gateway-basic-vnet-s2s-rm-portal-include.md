Para criar uma VNet no modelo de implementação do Gestor de Recursos com o Portal do Azure, siga os passos abaixo. Use os [valores de exemplo](#values) se estiver a seguir estes passos como um tutorial. Se não estiver a seguir estes passos como um tutorial, certifique-se de substitui os valores pelos seus próprios. Para obter mais informações sobre como trabalhar com redes virtuais, veja [Descrição Geral da Virtual Network](../articles/virtual-network/virtual-networks-overview.md).

>[!NOTE]
>Para esta VNet ligar a uma localização no local, terá de se coordenar com o administrador da rede no local para extrair um intervalo de endereços IP que possa utilizar especificamente para esta rede virtual. Se existir um intervalo de endereços duplicados em ambos os lados da ligação VPN, o tráfego não será encaminhado da forma esperada. Além disso, se pretender ligar esta VNet a outra VNet, o espaço de endereços não pode sobrepor-se a outra VNet. Tenha o cuidado de planear a configuração da rede em conformidade.
>
>

1. Num browser, navegue para o [Portal do Azure](http://portal.azure.com) e inicie sessão com a sua conta do Azure.
2. Clique em **Novo**. No campo **Procurar no Marketplace**, escreva "rede virtual". Localize a **Rede virtual** na lista devolvida e clique para abrir a página **Rede Virtual**.
3. Perto da parte inferior do painel Virtual Network, na página **Selecionar um modelo de implementação**, selecione **Resource Manager** e clique em **Criar**. É aberta a página "Criar rede virtual".

    ![Página Criar rede virtual](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/vnet.png "Página Criar rede virtual")
4. Na página **Criar rede virtual**, configure as definições da VNet. Depois de preencher os campos, o sinal de exclamação vermelho muda para uma marca de verificação verde se os caracteres introduzidos nos campos forem válidos.

  - **Nome**: Introduza o nome da rede virtual. Neste exemplo, usamos o TestVNet1.
  - **Espaço de endereços**: introduza o espaço de endereços. Se tiver vários espaços de endereços para adicionar, adicione o primeiro. Pode adicionar os outros mais tarde, depois de criar a VNet. Certifique-se de que o espaço de endereço que especificou não se sobrepõe ao espaço de endereço para a sua localização no local.
  - **Subscrição**: Verifique se a subscrição listada é a correta. Pode utilizar o menu pendente para mudar de subscrição.
  - **Grupo de recursos**: selecione um grupo de recursos existente ou crie um novo ao escrever o nome do mesmo. Se estiver a criar um novo grupo, dê-lhe um nome de acordo com os valores de configuração planeados. Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
  - **Localização**: selecione a localização da VNet. A localização determina onde é que os recursos que implementar nesta VNet vão residir.
  - **Sub-rede**: adicione o primeiro nome e o intervalo de endereços da sub-rede. Posteriormente, pode adicionar subredes adicionais e a subrede de gateway depois de criar esta VNet. 

5. Selecione **Afixar ao dashboard** se pretender conseguir localizar mais facilmente as suas VNet no dashboard e clique em **Criar**. Depois de clicar em **Criar**, verá um mosaico no dashboard que irá refletir o progresso da VNet. O mosaico muda enquanto a VNet está a ser criada.