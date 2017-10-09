toocreate uma VNet no modelo de implementação do Resource Manager Olá utilizando Olá portal do Azure, siga os passos de Olá abaixo. Olá utilize [valores de exemplo](#values) se estiver a utilizar estes passos como um tutorial. Se não estão a fazer estes passos como um tutorial, ser se valores de Olá tooreplace com os seus próprios. Para obter mais informações sobre como trabalhar com redes virtuais, consulte Olá [descrição geral de rede Virtual](../articles/virtual-network/virtual-networks-overview.md).

1. Num browser, navegue toohello [portal do Azure](http://portal.azure.com) e inicie sessão com a sua conta do Azure.
2. Clique em **Novo**. No Olá **marketplace Olá de pesquisa** campo, escreva 'Rede Virtual'. Localizar **rede Virtual** de Olá devolvido lista e clique em tooopen Olá **rede Virtual** painel.
3. Perto Olá parte inferior do painel de rede Virtual Olá, de Olá **selecionar um modelo de implementação** lista, selecione **Resource Manager**e, em seguida, clique em **criar**. Esta ação abre o painel do Olá 'Criar rede virtual'.

    ![Painel Criar rede virtual](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "Painel Criar rede virtual")
4. No Olá **criar rede virtual** painel, configurar definições da VNet Olá. Quando preencha os campos de Olá, hello de exclamação vermelho torna-se uma marca de verificação verde quando caracteres Olá introduzidos no campo Olá são válidos.

  - **Nome**: introduza o nome de Olá na sua rede virtual. Neste exemplo, usamos o TestVNet1.
  - **Espaço de endereços**: introduza o espaço de endereços de Olá. Se tiver vários tooadd de espaços de endereços, adicione o seu primeiro espaço de endereços. Pode adicionar mais tarde, espaços de endereços adicionais depois de criar Olá VNet. Certifique-se de que esse espaço de endereço Olá que especificou não se sobreponha a com o espaço de endereços de Olá para a sua localização no local.
  - **Nome da sub-rede**: Adicionar Olá primeira sub-rede nome e a sub-rede intervalo de endereços. Pode adicionar sub-redes adicionais e a sub-rede do gateway Olá mais tarde, depois de criar nesta VNet. 
  - **Subscrição**: Certifique-se de que subscrição Olá listada é Olá correto. Pode alterar as subscrições utilizando Olá lista pendente.
  - **Grupo de recursos**: selecione um grupo de recursos existente ou crie um novo ao escrever o nome do mesmo. Se estiver a criar um novo grupo, o grupo de recursos nome Olá tooyour de acordo com planeada valores de configuração. Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
  - **Localização**: selecione a localização de Olá para a sua VNet. localização de Olá determina onde os recursos de Olá que implemente toothis VNet irão residir.

5. Selecione **Pin toodashboard** se pretende toofind capaz de toobe a VNet facilmente no dashboard de Olá e, em seguida, clique em **criar**. Depois de clicar em **criar**, verá um mosaico no dashboard que irá refletir o progresso de Olá da VNet. alterações de mosaico Olá como Olá VNet está a ser criado.
