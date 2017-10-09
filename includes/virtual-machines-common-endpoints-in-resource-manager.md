pontos finais de tooAzure do Olá abordagem ligeiramente funciona de forma diferente entre os modelos de implementação clássica e Resource Manager Olá. No modelo de implementação do Resource Manager Olá, tem agora Olá flexibilidade toocreate rede filtros Olá fluxo de tráfego que entra e sai as suas VMs do controlo. Estes filtros permitem-lhe os ambientes de rede complexas toocreate para além de um ponto final simple como no modelo de implementação clássica Olá. Este artigo fornece uma descrição geral dos grupos de segurança de rede e de forma diferente de utilizar pontos finais de clássico, criar estas regras, de filtragem e cenários de implementação de exemplo.

## <a name="overview-of-resource-manager-deployments"></a>Descrição geral de implementações do Resource Manager
Pontos finais no modelo de implementação clássica Olá são substituídos pelos grupos de segurança de rede e as regras de lista (ACL) de controlo de acesso. Passos rápidos para implementar as regras de ACL de grupo de segurança de rede são:

* Crie um grupo de segurança de rede.
* tooallow ou negar o tráfego, definir as regras de ACL de grupo de segurança de rede.
* Atribua a interface de rede do grupo de segurança de rede tooa ou a sub-rede da rede virtual.

Se estiver a intenção tooalso efetuar reencaminhamento da porta, o que precisa tooplace um balanceador de carga à frente da sua VM e utiliza regras NAT. Passos rápidos para implementar um balanceador de carga e regras NAT seria o seguinte:

* Crie um balanceador de carga.
* Crie um conjunto de back-end e adicione o conjunto de toohello VMs.
* Defina as regras NAT de reencaminhamento da porta de Olá necessário.
* Atribua as regras NAT tooyour VMs.

## <a name="network-security-group-overview"></a>Descrição geral do grupo de segurança de rede
Grupos de segurança de rede fornecem uma camada de segurança de que portas específicas tooallow e sub-redes tooaccess as suas VMs. Normalmente, terá sempre um grupo de segurança de rede fornecer esta camada de segurança entre as VMs e Olá fora do mundo. Grupos de segurança de rede podem ser aplicados tooa sub-rede da rede virtual ou uma interface de rede específico para uma VM. Em vez de criar regras de ACL de ponto final, pode cria regras de ACL de grupo de segurança de rede. Estas regras ACL fornecem muito maior controlo que simplesmente criar um ponto final tooforward uma porta indicada. Para obter mais informações, consulte [que é um grupo de segurança de rede?](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> Pode atribuir sub-redes toomultiple de grupos de segurança de rede ou as interfaces de rede. Não há nenhum mapeamento 1:1. Pode criar um grupo de segurança de rede com um conjunto comum de regras de ACL e aplicar toomultiple sub-redes ou interfaces de rede. Além disso, o grupo de segurança de rede podem ser aplicados tooresources na sua subscrição (com base no [controlos de acesso baseado em funções](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Descrição geral de balanceadores de carga
No modelo de implementação clássica Olá, Azure iria executar todos os Olá tradução de endereços de rede (NAT) e porta do reencaminhamento de um serviço em nuvem para si. Ao criar um ponto final, tem de especificar Olá porta externa tooexpose juntamente com Olá porta interno toodirect tráfego. Grupos de segurança de rede por si mesmos não execute este mesmo NAT e o reencaminhamento de porta. 

tooallow toocreate regras NAT para essa porta reencaminhamento, cria um balanceador de carga do Azure no seu grupo de recursos. Novamente, o Balanceador de carga Olá é granular suficiente tooonly aplicar toospecific VMs, se necessário. Olá, Azure carregar o trabalho de regras NAT de Balanceador juntamente com tooprovide de regras de ACL de grupo de segurança de rede muito mais flexibilidade e o controlo que era alcançável utilizando pontos finais de serviço em nuvem. Para obter mais informações, consulte Olá [descrição geral do Balanceador de carga](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Regras de ACL de grupo de segurança de rede
Regras de ACL permitem-lhe definir o tráfego flua e para a VM com base em protocolos, portas específicas ou intervalos de portas. As regras são atribuídas tooindividual VMs ou tooa sub-rede. Olá seguinte captura de ecrã é um exemplo de regras de ACL para um servidor Web comuns:

![Regras de ACL de lista do grupo de segurança de rede](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

Regras ACL são aplicadas com base numa métrica de prioridade que especificou - valor de Olá superior Olá, prioridade de Olá Olá inferior. Todos os grupos de segurança de rede tem predefinição três regras que são concebidas de fluxo de Olá toohandle de tráfego de rede do Azure, com explícita `DenyAllInbound` como regra final Olá. Regras ACL predefinidas são fornecido um toonot de baixa prioridade interferir com regras que cria.

## <a name="assigning-network-security-groups"></a>Atribuição de grupos de segurança de rede
Atribuir uma sub-rede de tooa do grupo de segurança de rede ou uma interface de rede. Esta abordagem permite-lhe toobe como granulares, conforme necessário ao aplicar a ACL regras tooonly uma VM específica ou certifique-se de um conjunto comum de ACL as regras são aplicada tooall VMs parte de uma sub-rede:

![Aplicar NSGs toonetwork interfaces ou sub-redes](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

comportamento de Olá de Olá grupo de segurança de rede não irá alterar, dependendo de que está a ser atribuído tooa sub-rede ou de uma interface de rede. Um cenário de implementação comum tem Olá que grupo de segurança de rede atribuído tooa sub-rede tooensure conformidade sub-rede de toothat anexado todas as VMs. Para obter mais informações, consulte [aplicar a segurança de rede grupos tooresources](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Comportamento predefinido de grupos de segurança de rede
Dependendo de como e quando criar o grupo de segurança de rede, as regras predefinidas podem ser criadas para as VMs do Windows do acesso RDP a toopermit na porta TCP 3389. Regras predefinidas para VMs com Linux permitem o acesso SSH na porta TCP 22. Estas regras ACL automáticas são criadas no Olá seguintes condições:

* Se criar uma VM do Windows através do portal Olá e aceitar Olá predefinido ação toocreate um grupo de segurança de rede, é criada uma ACL regra tooallow a porta TCP 3389 (RDP).
* Se criar uma VM com Linux através do portal Olá e aceitar Olá predefinido ação toocreate um grupo de segurança de rede, é criada uma ACL regra tooallow a porta TCP 22 (SSH).

Em todas as outras condições, estas regras ACL predefinidas não são criadas. Não é possível ligar tooyour VM sem criar Olá regras de ACL adequadas. Estas condições incluem Olá seguintes ações comuns:

* Criar um grupo de segurança de rede através do portal Olá como Olá de toocreating uma ação separada VM.
* Criar um grupo de segurança de rede através de programação através do PowerShell, CLI do Azure, as APIs Rest, etc.
* Criar uma VM e atribuição do mesmo tooan existente grupo de segurança de rede que ainda não tiver Olá adequada regra de ACL definida.

Todos os Olá precedente casos, terá de regras de ACL de toocreate para ligações de gestão remota adequado a VM tooallow Olá.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Comportamento predefinido de uma VM sem um grupo de segurança de rede
Pode criar uma VM sem criar um grupo de segurança de rede. Nestas situações, pode ligar tooyour VM através de DRP ou SSH sem criar quaisquer regras ACL. Da mesma forma, se tiver instalado um serviço web na porta 80, que o serviço é automaticamente acessível remotamente. Olá VM tem todas as portas abertas.

> [!NOTE]
> Ainda precisa de toohave um tooa de atribuída de endereço IP de público VM para que quaisquer ligações remotas. Não ter um grupo de segurança de rede para a interface de rede ou de sub-rede Olá não expõe o tráfego de Olá VM tooany externo. ação predefinida de Olá quando criar uma VM através do portal Olá é toocreate um IP público novo. Para todas as outras formas de criar uma VM, tais como o PowerShell, a CLI do Azure ou o modelo do Resource Manager, um IP público não é automaticamente criado, a menos que explicitamente pedida. ação de predefinida Olá através do portal Olá também é toocreate um grupo de segurança de rede. Esta ação de predefinição significa que não deve terminar a cópia de segurança numa situação com uma VM exposta que não tenha a nenhuma rede filtragem no local.

## <a name="understanding-load-balancers-and-nat-rules"></a>Noções sobre balanceadores de carga e regras NAT
No modelo de implementação clássica Olá, pode criar pontos finais que também efetuada reencaminhamento da porta. Quando cria uma VM no modelo de implementação clássica Olá, regras de ACL para RDP ou SSH seriam possível criar automaticamente. Estas regras seriam não expõe a porta TCP 3389 ou a porta TCP 22 respetivamente toohello fora do mundo. Em vez disso, deverá ser exposta uma porta TCP de alto valor que mapeie toohello de porta interna adequada. Pode também criar as suas próprias regras ACL de forma semelhante, tais como expõe um servidor Web em TCP porta toohello 4280 fora do mundo. Pode ver estas regras de ACL e mapeamentos de porta no Olá seguinte captura de ecrã a partir do portal clássico Olá:

![Reencaminhamento de porta com pontos finais de clássico](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Grupos de segurança de rede, essa função de reencaminhamento da porta é processada por um balanceador de carga. Para obter mais informações, consulte [balanceadores no Azure de carga](../articles/load-balancer/load-balancer-overview.md). Olá exemplo seguinte mostra um balanceador de carga com uma NAT regra tooperform reencaminhamento da porta TCP porta 4222 toohello interno porta TCP 22 uma VM:

![Carregar as regras de NAT de Balanceador de reencaminhamento da porta](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Quando implementar um balanceador de carga, normalmente não atribuir Olá um endereço IP público a própria VM. Em vez disso, o Balanceador de carga Olá tem um endereço atribuído tooit público do IP. Ainda precisa de toocreate o grupo de segurança de rede e ACL regras toodefine Olá fluxo de tráfego que entra e sai da VM. Olá as regras de NAT de Balanceador de carga são simplesmente toodefine as portas que são permitidas através do Balanceador de carga Olá e como obter distribuídos back-end de Olá VMs. Como tal, precisa toocreate uma regra NAT para o tráfego tooflow através do Balanceador de carga Olá. Olá do tooallow Olá tráfego tooreach VM, crie uma regra de ACL de grupo de segurança de rede.
