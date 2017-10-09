## <a name="scenario"></a>Cenário
Este documento irá guiá-lo através de uma implementação que utiliza vários NICs nas VMs num cenário específico. Neste cenário, tem uma duas camadas IaaS carga de trabalho alojada no Azure. Cada camada está implementada na sua própria sub-rede numa rede virtual (VNet). camada de front-end Olá é composta por vários servidores web, agrupados num Balanceador de carga definido para elevada disponibilidade. camada de back-end Olá é composta por vários servidores de base de dados. Estes servidores de base de dados será implementado com dois NICs cada, um para acesso de base de dados, hello outros para gestão. cenário de Olá também inclui toocontrol de grupos de segurança de rede (NSGs) que o tráfego é permitido tooeach sub-rede e NIC na implementação de Olá. figura Olá abaixo mostra a arquitetura básica do Olá deste cenário.  

![Cenário de MultiNIC](./media/virtual-network-deploy-multinic-scenario-include/Figure1.png)

