

![Máquinas virtuais no serviço autónomo em nuvem](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

Se colocar as máquinas virtuais numa rede virtual, pode decidir quantos serviços em nuvem que pretende toouse para conjuntos de disponibilidade e balanceamento de carga. Além disso, pode organizar Olá máquinas de virtuais em sub-redes Olá mesma forma como o local de rede e ligar Olá tooyour de rede virtual no local rede. Eis um exemplo:

![Máquinas virtuais numa rede virtual](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

Redes virtuais são Olá recomendado forma tooconnect máquinas virtuais no Azure. Olá melhor prática é tooconfigure cada camada da aplicação no serviço em nuvem separado. No entanto, poderá ser necessário toocombine algumas máquinas virtuais de camadas de aplicações diferentes em Olá mesmo na nuvem tooremain de serviço no máximo, Olá 200 serviços cloud por subscrição. tooreview esta e outros limites, consulte o artigo [subscrição do Azure e limites de serviço, Quotas e restrições](../articles/azure-subscription-service-limits.md).

## <a name="connect-vms-in-a-virtual-network"></a>Ligar as VMs numa rede virtual
máquinas virtuais de tooconnect numa rede virtual:

1. Criar rede virtual Olá no Olá [portal do Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) e especifique 'implementação clássica'.
2. Criar conjunto de Olá de serviços em nuvem para a sua implementação tooreflect o design para conjuntos de disponibilidade e o balanceamento de carga. No portal do Azure Olá, clique em **novo > computação > serviço em nuvem** para cada serviço em nuvem.

  À medida que preencha os detalhes do serviço de nuvem Olá, escolher Olá mesmo _grupo de recursos_ utilizado com a rede virtual Olá.

3. toocreate cada novo virtual máquina, clique em **novo > computação**, em seguida, selecione Olá imagem VM adequada de Olá **aplicações em destaque**.

  No Olá VM **Noções básicas** painel, escolha Olá mesmo _grupo de recursos_ utilizado com a rede virtual Olá.

  ![Painel de noções básicas de VM ao utilizar uma VNet](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. Como preencher Olá VM **definições**, escolha Olá correto _serviço em nuvem_ ou _rede virtual_ para Olá VM.

  Azure selecionará Olá outro item com base na sua seleção.

  ![Painel de definições de VM ao utilizar uma VNet](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>Ligar as VMs num serviço autónomo em nuvem
máquinas virtuais de tooconnect num serviço autónomo em nuvem:

1. Criar o serviço em nuvem Olá no Olá [portal do Azure](http://portal.azure.com). Clique em **novo > computação > serviço em nuvem**. Em alternativa, pode criar o serviço em nuvem Olá para a sua implementação quando criar a sua primeira máquina virtual.
2. Ao criar máquinas virtuais Olá, escolha Olá mesmo grupo de recursos utilizado com o serviço em nuvem Olá.

  ![Adicionar um serviço de nuvem existente do virtual machine tooan](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  Como preencher os detalhes VM Olá, escolha o nome de Olá do serviço em nuvem criado no passo primeiro Olá.

  ![Selecionar um serviço em nuvem para uma máquina virtual](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
