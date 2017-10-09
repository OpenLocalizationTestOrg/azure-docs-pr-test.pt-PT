toocreate uma VNet no modelo de implementação do Resource Manager Olá utilizando Olá portal do Azure, siga os passos de Olá abaixo. Olá capturas de ecrã são fornecidas como exemplos. Ser se valores de Olá tooreplace com os seus próprios. Para obter mais informações sobre como trabalhar com redes virtuais, consulte Olá [descrição geral de rede Virtual](../articles/virtual-network/virtual-networks-overview.md).

1. Num browser, navegue toohello [portal do Azure](http://portal.azure.com) e, se necessário, inicie sessão com a sua conta do Azure.
2. Clique em **+**. No Olá **marketplace Olá de pesquisa** campo, escreva "Rede Virtual". Localizar **rede Virtual** de Olá devolvido lista e clique em tooopen Olá **rede Virtual** página.

  ![Localizar página de recursos da Rede Virtual](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/newvnetportal700.png "Localizar página de recursos da Rede Virtual")
3. Perto Olá parte inferior da página Olá da rede Virtual, do Olá **selecionar um modelo de implementação** lista, selecione **Resource Manager**e, em seguida, clique em **criar**.

  ![Selecionar o Resource Manager](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/resourcemanager250.png "Selecionar o Resource Manager")
4. No Olá **criar rede virtual** página, configurar definições da VNet Olá. Quando preencha os campos de Olá, hello de exclamação vermelho torna-se uma marca de verificação verde quando caracteres Olá introduzidos no campo Olá são válidos. Poderá haver valores preenchidos automaticamente. Se assim for, substitua os valores de Olá com os seus próprios. Olá **criar rede virtual** página procura toohello semelhante seguinte exemplo:

  ![Validação de campo](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/createp2sgvnet.png "Validação de campo")
5. **Nome**: introduza o nome de Olá na sua rede Virtual.
6. **Espaço de endereços**: introduza o espaço de endereços de Olá. Se tiver vários tooadd de espaços de endereços, adicione o seu primeiro espaço de endereços. Pode adicionar mais tarde, espaços de endereços adicionais depois de criar Olá VNet.
7. **Nome da sub-rede**: Adicionar Olá sub-rede nome e a sub-rede intervalo de endereços. Pode adicionar sub-redes adicionais mais tarde, depois de criar Olá VNet.
8. **Subscrição**: Certifique-se de que Olá listada de subscrição é Olá correto. Pode alterar as subscrições utilizando Olá lista pendente.
9. **Grupo de recursos**: selecione um grupo de recursos existente ou crie um novo ao escrever o nome do mesmo. Se estiver a criar um novo grupo, o grupo de recursos nome Olá tooyour de acordo com planeada valores de configuração. Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
10. **Localização**: selecione a localização de Olá para a sua VNet. localização de Olá determina onde os recursos de Olá que implemente toothis VNet irão residir.
11. Selecione **Pin toodashboard** se pretende toofind capaz de toobe a VNet facilmente no dashboard de Olá e, em seguida, clique em **criar**.

 ![PIN toodashboard](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/pintodashboard150.png "toodashboard de pin")
12. Depois de clicar em **criar**, verá um mosaico no dashboard que irá refletir o progresso de Olá da VNet. alterações de mosaico Olá como Olá VNet está a ser criado.

  ![Mosaico Criar rede virtual](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/deploying150.png "Mosaico Criar rede virtual")