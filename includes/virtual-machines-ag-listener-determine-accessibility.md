É importante toorealize que existem duas formas tooconfigure um serviço de escuta do grupo de disponibilidade no Azure. diferem formas de Olá no tipo de Olá do Balanceador de carga do Azure que utilizar quando criar o serviço de escuta de Olá. Olá, a tabela seguinte descreve as diferenças de Olá:

| Tipo de Balanceador de carga | Implementação | Utilize se: |
| --- | --- | --- |
| **Externo** |Utiliza Olá *endereço IP virtual público* do serviço em nuvem Olá que aloja Olá máquinas de virtuais (VMs). |Terá de serviço de escuta do tooaccess Olá a partir da rede virtual externa Olá, incluindo a partir da Internet de Olá. |
| **Interno** |Utiliza um *Balanceador de carga interno* com um endereço para o serviço de escuta de Olá privado. |Olá serviço de escuta apenas a partir de dentro de Olá pode aceder à mesma rede virtual. Este acesso inclui VPN site a site em cenários híbridos. |

> [!IMPORTANT]
> Para um serviço de escuta que Olá, utiliza VIP público do serviço em nuvem Olá (Balanceador de carga externo), desde que o cliente de Olá, serviço de escuta e bases de dados estão na mesma região do Azure, não será cobrado encargos associados à saída. Caso contrário, todos os dados devolvidos através de Olá escuta é considerada saída e é-lhe cobrado às taxas de transferência de dados normal. 
> 
> 

Pode ser configurado um ILB apenas em redes virtuais com um âmbito regional. As redes virtuais existentes que tenham sido configuradas para um grupo de afinidade não é possível utilizar um ILB. Para obter mais informações, consulte [descrição geral do Balanceador de carga interno](../articles/load-balancer/load-balancer-internal-overview.md).

