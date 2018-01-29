Quando cria uma máquina virtual (VM) do Azure, tem de criar uma [rede virtual](../articles/virtual-network/virtual-networks-overview.md) (VNet) ou de utilizar uma VNet já existente. Também tem de decidir como pretende que se faça o acesso às VMs na VNet. É importante [planear antes de criar recursos](../articles/virtual-network/virtual-network-vnet-plan-design-arm.md) e ter a certeza de que compreende os [limites dos recursos de rede](../articles/azure-subscription-service-limits.md#networking-limits).

Na figura seguinte, as VMs são representadas como servidores Web e servidores de bases de dados. Cada conjunto de VMs é atribuído a sub-redes separadas na VNet.

![Rede virtual do Azure](./media/virtual-machines-common-network-overview/vnetoverview.png)

Pode criar uma VNet antes de criar uma VM ou pode criar uma VM. Os recursos seguintes são criados para suportar a comunicação com as VMs:

- Interfaces de rede
- Endereços IP
- Rede virtual e sub-redes

Para além destes recursos básicos, também deve considerar estes recursos opcionais:

- Grupos de segurança de rede
- Balanceadores de carga 

## <a name="network-interfaces"></a>Interfaces de rede

Uma [interface de rede (NIC)](../articles/virtual-network/virtual-network-network-interface.md) é a interligação entre uma VM e uma rede virtual (VNet). As VMs têm de ter, pelo menos, uma NIC, mas podem ter mais, dependendo do tamanho da VM que criar. Saiba mais sobre quantas NICs a cada VM tamanho suporta para [Windows](../articles/virtual-machines/windows/sizes.md) ou [Linux](../articles/virtual-machines/linux/sizes.md).

Pode criar uma VM com vários NICs e adicionar ou remover NICs através do ciclo de vida de uma VM. Vários NICs permitir que uma VM ligar a diferentes sub-redes e enviar ou receber tráfego através da interface mais adequada.

Se a VM for adicionada a um conjunto de disponibilidade, todas as VMs dentro desse grupo têm de ter uma ou várias NICs. As VMs que tenham mais de uma NIC não têm, obrigatoriamente, de ter o mesmo número de interfaces, mas todas têm de ter, no mínimo, duas.

Cada NIC ligada a uma VM tem de existir na mesma localização e subscrição que a VM. Cada NIC deve estar ligada a uma VNet que exista na mesma localização e subscrição do Azure que essa NIC. Pode alterar a sub-rede que VM está ligada à depois de criado, mas não é possível alterar a VNet. É atribuído um endereço MAC a cada NIC ligada a uma VM, o qual não muda até a VM ser eliminada.

Esta tabela lista os métodos que pode utilizar para criar uma interface de rede.

| Método | Descrição |
| ------ | ----------- |
| Portal do Azure | Quando cria uma VM no portal do Azure, é criada automaticamente uma interface de rede por si (não pode utilizar uma NIC que tenha criado separadamente). O portal cria uma VM com apenas uma NIC. Se quiser criar uma VM com mais de uma NIC, tem de criá-la com outro método. |
| [Azure PowerShell](../articles/virtual-machines/windows/multiple-nics.md) | Utilize [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) com o parâmetro **-PublicIpAddressId** para fornecer o identificador do endereço IP público que criou anteriormente. |
| [CLI do Azure](../articles/virtual-machines/linux/multiple-nics.md) | Para fornecer o identificador do endereço IP público que criou anteriormente, utilize [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) com o parâmetro **--public-ip-address**. |
| [Modelo](../articles/virtual-network/virtual-network-deploy-multinic-arm-template.md) | Utilize [Network Interface in a Virtual Network with Public IP Address (Interface de Rede numa Rede Virtual com Endereço IP Público)](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) como guia para implementar interfaces de rede através de um modelo. |

## <a name="ip-addresses"></a>Endereços IP 

Pode atribuir estes tipos de [endereços IP](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) a uma NIC no Azure:

- **Endereços IP públicos** - utilizados para comunicação de entrada e saída (sem tradução de endereços de rede [NAT]) com a Internet e outros recursos do Azure não ligados a uma VNet. A atribuição de endereços IP públicos a uma NIC é opcional. Endereços IP públicos têm uma cobrança nominal e existe um número máximo que pode ser utilizado por subscrição.
- **Endereços IP privados** - utilizados para comunicação dentro de VNets, com a sua rede no local e com a Internet (com NAT). Tem de atribuir, pelo menos, um endereço IP privado a uma VM. Para saber mais sobre a NAT no Azure, leia [Understanding outbound connections in Azure (Compreender as ligações de saída no Azure)](../articles/load-balancer/load-balancer-outbound-connections.md).

Pode atribuir endereços IP públicos a VMs ou a balanceadores de carga com acesso à Internet. Pode atribuir endereços IP privados a VMs e a balanceadores de carga internos. Para atribuir endereços IP a uma VM, é utilizada uma interface de rede.

Existem dois métodos através dos quais os endereços IP podem ser alocados a recursos - dinâmico ou estático. O método de alocação predefinido é o dinâmico, no qual o endereço IP não é alocado quando é criado. Em vez disso, é alocado quando cria uma VM ou inicia uma VM parada. O endereço IP é libertado quando para ou elimina a VM. 

Para garantir que o endereço IP da VM fica o mesmo, pode definir o método de alocação explicitamente como estático. Neste caso, é atribuído imediatamente um endereço IP. Só é libertado quando elimina a VM ou altera o método de alocação para dinâmico.
    
Esta tabela lista os métodos que pode utilizar para criar um endereço IP.

| Método | Descrição |
| ------ | ----------- |
| [Portal do Azure](../articles/virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | Por predefinição, os endereços IP públicos são dinâmicos e o endereço associado aos mesmos pode mudar quando a VM é parada ou eliminada. Para garantir que a VM utiliza sempre o mesmo endereço IP público, crie um endereço IP público estático. Por predefinição, o portal atribui um endereço IP privado dinâmico a uma NIC quando é criada uma VM. Pode alterar este endereço IP estático para depois da VM é criada.|
| [Azure PowerShell](../articles/virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Utiliza [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) com o parâmetro **-AllocationMethod** como Dinâmico ou Estático. |
| [CLI do Azure](../articles/virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Utiliza [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) com o parâmetro **--allocation-method** como Dinâmico ou Estático. |
| [Modelo](../articles/virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Utilize [Network Interface in a Virtual Network with Public IP Address (Interface de Rede numa Rede Virtual com Endereço IP Público)](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) como guia para implementar endereços IP públicos através de um modelo. |

Depois de criar um endereço IP público, pode associá-lo a uma VM ao atribuí-lo a uma NIC.

## <a name="virtual-network-and-subnets"></a>Rede virtual e sub-redes

Uma sub-rede é um intervalo de endereços IP na VNet. Pode dividir uma VNet em várias sub-redes por questões de organização e de segurança. Cada NIC numa VM está ligada a uma sub-rede numa VNet. As NICs ligadas a sub-redes (às mesmas ou a diferentes) dentro de uma VNet podem comunicar entre si sem qualquer configuração adicional.

Quando configura uma VNet, especifica a topologia, incluindo os espaços de endereços e as sub-redes disponíveis. Se a VNet for ligada a outras VNets ou a redes no local, tem de selecionar intervalos de endereços que não se sobreponham. Os endereços IP são privados e não podem ser acedidos a partir da Internet, o que era verdade apenas para os endereços IP não endereçáveis, como 10.0.0.0/8, 172.16.0.0/12 ou 192.168.0.0/16. Agora, o Azure trata todos os intervalos de endereços como fazendo parte do espaço de endereços IP privados da VNet que só está acessível dentro da VNet, dentro de VNets interligadas e dentro da sua localização no local. 

Se trabalha numa organização em que outra pessoa é responsável pelas redes internas, deve contactá-la antes de selecionar o espaço de endereços. Confirme que não existem sobreposições e diga a essa pessoa que espaço quer utilizar, para que ela não tente utilizar o mesmo intervalo de endereços IP. 

Por predefinição, não existem limites de segurança entre sub-redes, pelo que as VMs em cada uma dessas sub-redes podem comunicar entre si. No entanto, pode configurar Grupos de Segurança de Rede (NSG), que lhe permitem controlar o fluxo de tráfego de e para as sub-redes e VMs. 

Esta tabela lista os métodos que pode utilizar para criar uma VNet e sub-redes. 

| Método | Descrição |
| ------ | ----------- |
| [Portal do Azure](../articles/virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Se permitir que o Azure crie uma VNet quando cria uma VM, o nome é uma combinação do nome do grupo de recursos que contém a VNet e de **-vnet**. O espaço de endereços é 10.0.0.0/24, o nome da sub-rede obrigatório é **default** e o intervalo de endereços da sub-rede é 10.0.0.0/24. |
| [Azure PowerShell](../articles/virtual-network/virtual-networks-create-vnet-arm-ps.md) | Utiliza [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) e [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) para criar uma sub-rede e uma VNet. Também pode utilizar [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) para adicionar uma sub-rede a uma VNet já existente. |
| [CLI do Azure](../articles/virtual-network/virtual-networks-create-vnet-arm-cli.md) | A sub-rede e a VNet são criadas ao mesmo tempo. Forneça um parâmetro **--subnet-name** para [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) com o nome da sub-rede. |
| [Modelo](../articles/virtual-network/virtual-networks-create-vnet-arm-template-click.md) | A forma mais fácil de criar uma VNet e sub-redes é transferir um modelo já existente, como [Virtual Network with two Subnets (Rede Virtual com Duas Sub-Redes)](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets), e modificá-lo de acordo com as suas necessidades. |

## <a name="network-security-groups"></a>Grupos de segurança de rede

Os [grupo de segurança de rede (NSG)](../articles/virtual-network/virtual-networks-nsg.md) contêm uma lista de regras da Lista de Controlo de Acesso (ACL) que permitem ou negam o tráfego de rede para sub-redes, NICs ou ambas. Os NSGs podem ser associados a sub-redes ou a NICs individuais ligadas a sub-redes. Quando um NSG é associado a uma sub-rede, as regras da ACL são aplicadas a todas as VM nessa sub-rede. Além disso, o tráfego para uma NIC individual pode ser restringido ao associar um NSG diretamente à NIC.

Os NSGs contêm dois conjuntos de regras: de entrada e de saída. A prioridade para uma regra tem de ser exclusiva dentro de cada conjunto. Cada regra tem propriedades de protocolo, de intervalos de portas de origem e destino, de prefixos de endereços, de direção do tráfego, de prioridade e de tipo de acesso. 

Todos os NSGs contêm um conjunto de regras predefinidas. As regras predefinidas não podem ser eliminadas, mas como lhes é atribuída a prioridade mais baixa, podem ser substituídas pelas regras que criar. 

Quando associa um NSG a um NIC, as regras de acesso à rede no NSG só são aplicadas a esse NIC. Se for aplicado um NSG a uma NIC individual numa VM multi-NIC, o tráfego para as outras NIC não é afetado. Pode associar NSGs diferentes a uma NIC (ou VM, consoante o modelo de implementação) e à sub-rede à qual a NIC ou VM está vinculada. A prioridade é atribuída com base na direção do tráfego.

Certifique-se de que [planeia](../articles/virtual-network/virtual-networks-nsg.md#planning) os NSGs quando planear as VMs e a VNet.

Esta tabela lista os métodos que pode utilizar para criar um grupo de segurança de rede.

| Método | Descrição |
| ------ | ----------- |
| [Portal do Azure](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Quando cria uma VM no portal do Azure, é criado automaticamente um NSG e associado à NIC que o portal cria. O nome do NSG é uma combinação do nome da VM e de **-nsg**. Este NSG contém uma regra de entrada com prioridade de 1000, o serviço definido como RDP, o protocolo como TCP, a porta como a 3389 e a ação Permitir. Se quiser permitir outro tráfego de entrada para a VM, tem de adicionar regras ao NSG. |
| [Azure PowerShell](../articles/virtual-network/virtual-networks-create-nsg-arm-ps.md) | Utilize [New-AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) e indique as informações necessárias da regra. Utilize [New-AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) para criar o NSG. Utilize [Set-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) para configurar o NSG para a sub-rede. Utilize [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) para adicionar o NSG à VNet. |
| [CLI do Azure](../articles/virtual-network/virtual-networks-create-nsg-arm-cli.md) | Utilize [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) para criar inicialmente o NSG. Utilize [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) para adicionar regras ao NSG. Utilize [az network vnet subnet update](https://docs.microsoft.com/cli/azure/network/vnet/subnet#update) para adicionar o NSG à sub-rede. |
| [Modelo](../articles/virtual-network/virtual-networks-create-nsg-arm-template.md) | Utilize [Create a Network Security Group (Criar um Grupo de Segurança de Rede)](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) como guia para implementar um grupo de segurança de rede através de um modelo. |

## <a name="load-balancers"></a>Balanceadores de carga

O [Balanceador de Carga do Azure](../articles/load-balancer/load-balancer-overview.md) oferece elevada disponibilidade e elevado desempenho de rede às suas aplicações. Pode ser configurado um balanceador de carga para [balancear o tráfego de entrada da Internet](../articles/load-balancer/load-balancer-internet-overview.md) para VMs ou [balancear o tráfego entre VMs numa VNet](../articles/load-balancer/load-balancer-internal-overview.md). Os balanceadores de carga também podem balancear o tráfego entre computadores no local e VMs numa rede em vários locais ou encaminhar tráfego externo para uma VM específica.

Os balanceadores de carga mapeiam o tráfego de entrada e saída entre o endereço IP público e a porta do balanceador de carga e o endereço IP privado e a porta da VM.

Quando cria um balanceador de carga, tem também de considerar estes elementos de configuração:

- **Configuração de IP de Front-end** – os balanceadores de carga podem incluir um ou mais endereços IP de front-end , também conhecidos como IPs virtuais (VIPs). Estes endereços IP servem como entrada para o tráfego.
- **Conjunto de endereços de back-end** – endereços IP que estão associados à NIC na qual a carga é distribuída.
- **Regras NAT** – definem de que forma é que o tráfego de entrada flui através do IP de front-end e é distribuído para o IP de back-end.
- **Regras de balanceador de carga** -mapeiam uma determinada combinação de IP e porta de front-end para um conjunto de combinação de endereços IP e porta de back-end. Um balanceador de carga individual pode ter várias regras de balanceamento de carga. Cada regra é uma combinação de um IP de front-end e porta e IP de back-end e porta associados a VMs
- **[Sondas](../articles/load-balancer/load-balancer-custom-probe-overview.md)** - monitorizam o estado de funcionamento das VMs. Quando uma sonda não consegue responder, o balanceador de carga deixa de enviar ligações novas para a VM em mau estado de funcionamento. As ligações existentes não são afetadas e as novas são enviadas para as VMs em bom estado de funcionamento.

Esta tabela lista os métodos que pode utilizar para criar um balanceador de carga com acesso à Internet.

| Método | Descrição |
| ------ | ----------- |
| Portal do Azure | Atualmente, não pode criar balanceadores de carga com acesso à Internet através do portal do Azure. |
| [Azure PowerShell](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md) | Para fornecer o identificador do endereço IP público que criou anteriormente, utilize [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) com o parâmetro **-PublicIpAddress**. Utilize [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) para criar a configuração do conjunto de endereços do back-end. Utilize [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) para criar regras NAT de netrada associadas à configuração do IP de front-end que criou. Utilize [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) para criar as sondas de que precisa. Utilize [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) para criar a configuração do balanceador de carga. Utilize [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) para criar o balanceador de carga.|
| [CLI do Azure](../articles/load-balancer/load-balancer-get-started-internet-arm-cli.md) | Utilize [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) para criar a configuração inicial do balanceador de carga. Utilize [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) para adicionar o endereço IP público que criou anteriormente. Utilize [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) para adicionar a configuração do conjunto de endereços do back-end. Utilize [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) para adicionar regras NAT. Utilize [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) para adicionar as regras do balanceador de carga. Utilize [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) para adicionar as sondas. |
| [Modelo](../articles/load-balancer/load-balancer-get-started-internet-arm-template.md) | Utilize [2 VMs in a Load Balancer and configure NAT rules on the LB (Duas VMs num Balanceador de Carga e configurar regras NAT no LB)](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) como guia para implementar um balanceador de carga através de um modelo. |
    
Esta tabela lista os métodos que pode utilizar para criar um balanceador de carga interno.

| Método | Descrição |
| ------ | ----------- |
| Portal do Azure | Atualmente, não pode criar balanceadores de carga internos através do portal do Azure. |
| [Azure PowerShell](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md) | Para fornecer um endereço IP privado na sub-rede da rede, utilize [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) com o parâmetro **-PrivateIpAddress**. Utilize [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) para criar a configuração do conjunto de endereços do back-end. Utilize [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) para criar regras NAT de netrada associadas à configuração do IP de front-end que criou. Utilize [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) para criar as sondas de que precisa. Utilize [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) para criar a configuração do balanceador de carga. Utilize [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) para criar o balanceador de carga.|
| [CLI do Azure](../articles/load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Utilize o comando [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) para criar a configuração inicial do balanceador de carga. Para definir o endereço IP privado, utilize [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) com o parâmetro **--private-ip-address**. Utilize [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) para adicionar a configuração do conjunto de endereços do back-end. Utilize [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) para adicionar regras NAT. Utilize [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) para adicionar as regras do balanceador de carga. Utilize [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) para adicionar as sondas.|
| [Modelo](../articles/load-balancer/load-balancer-get-started-ilb-arm-template.md) | Utilize [2 VMs in a Load Balancer and configure NAT rules on the LB (Duas VMs num Balanceador de Carga e configurar regras NAT no LB)](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) como guia para implementar um balanceador de carga através de um modelo. |

## <a name="vms"></a>VMs

As VMs podem ser criadas na mesma VNet e podem ligar-se entre si através de endereços IP privados. Podem ligar-se mesmo que estejam em sub-redes diferentes sem que seja necessário configurar um gateway ou utilizar endereços IP públicos. Para colocar VMs em VNets, cria primeiro a VNet e, depois, à medida que cria cada VM, vai adicionado-a à VNet e à sub-rede. As VMs adquirem as definições de rede durante a implementação ou o arranque.  

É atribuído um endereço IP às VMs quando são implementadas. Se implementar várias VMs numa VNet ou sub-rede, os endereços IP são-lhes atribuídos quando são arrancadas. O endereço IP dinâmico (DIP) é o endereço IP interno associado a uma VM. Pode alocar um DIP estático a uma VM. Se alocar um DIP estático, deve considerar utilizar uma sub-rede específica para evitar reutilizar, acidentalmente, um DIP estático de outra VM.  

Se criar uma VM e, posteriormente, quiser migrá-la para uma VNet, não é uma alteração de configuração simples. Tem de reimplementar a VM na VNet. A forma mais fácil de reimplementar é eliminar a VM, mas não os discos ligados à mesma, e utilizar os discos originais na VNet para recriá-la. 

Esta tabela lista os métodos que pode utilizar para criar uma VM numa VNet.

| Método | Descrição |
| ------ | ----------- |
| [Portal do Azure](../articles/virtual-machines/windows/quick-create-portal.md) | Utiliza as predefinições de rede que foram mencionadas anteriormente para criar uma VM com uma única NIC. Para criar uma VM com várias NICs, tem de utilizar outro método. |
| [Azure PowerShell](../articles/virtual-machines/windows/tutorial-manage-vm.md) | Inclui a utilização de [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) para adicionar a NIC que criou antes à configuração da VM. |
| [CLI do Azure](../articles/virtual-machines/linux/create-cli-complete.md) | Criar e ligar uma VM para uma Vnet, uma sub-rede e um NIC que criar como passos individuais. |
| [Modelo](../articles/virtual-machines/windows/ps-template.md) | Utilize [Very simple deployment of a Windows VM (Implementação muito simples de uma VM do Windows)](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) como guia para implementar uma VM através de um modelo. |

## <a name="next-steps"></a>Passos seguintes
Para obter os passos de VM específicos sobre como gerir redes virtuais do Azure para as VMs, consulte o [Windows](../articles/virtual-machines/windows/tutorial-virtual-network.md) ou [Linux](../articles/virtual-machines/linux/tutorial-virtual-network.md) tutoriais.

Também existem tutoriais sobre como equilibrar as VMs e criar aplicações elevadas para [Windows](../articles/virtual-machines/windows/tutorial-load-balancer.md) ou [Linux](../articles/virtual-machines/linux/tutorial-load-balancer.md).

- Saiba como configurar [rotas definidas pelo utilizador e encaminhamento de IP](../articles/virtual-network/virtual-networks-udr-overview.md). 
- Saiba como configurar [ligações VNet a VNet](../articles/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Saiba como [Resolver problemas de rotas](../articles/virtual-network/virtual-network-routes-troubleshoot-portal.md).