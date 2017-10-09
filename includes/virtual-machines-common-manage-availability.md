## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>Compreender os Reinícios da VM - manutenção vs. período de indisponibilidade
Existem três cenários que podem conduzir toovirtual máquina no Azure a ser afetado: manutenção de hardware não planeada, o tempo de inatividade inesperado e, a manutenção planeada.

* **Evento de manutenção não planeada do Hardware** ocorre quando hello esse hardware Olá qualquer plataforma componente tooa associado máquina física ou, é sobre toofail prevê a plataforma do Azure. Quando a plataforma de Olá prevê uma falha, emitirá um hardware não planeada manutenção eventos tooreduce Olá impacto toohello máquinas virtuais alojadas nesse hardware. Azure utiliza a migração em direto tecnologia toomigrate Olá máquinas virtuais de Olá máquina física do hardware tooa bom estado de funcionamento a falhar. Migração em direto é uma VM preservação de operação que só coloca em pausa hello a Máquina Virtual para um curto período de tempo. Memória, ficheiros abertos e ligações de rede são mantidas, mas pode ser reduzido desempenho antes de e/ou após evento de Olá. Nos casos em que não é possível utilizar migração em direto, Olá VM será tempo de inatividade inesperado, conforme descrito abaixo.


* **Um período de inatividade inesperado** raramente ocorre quando o hardware de Olá ou infraestrutura física Olá subjacente a máquina virtual falhou de alguma forma. Isto pode incluir falhas de rede local, falhas de disco local ou outras falhas estruturais. Quando é detetada uma falha de tal, hello plataforma Azure migra automaticamente (heals) a máquina de físico bom estado de funcionamento com tooa de máquina virtual. Durante a Olá autorrecuperação do procedimento, as máquinas virtuais de inatividade (reiniciar) e alguma perda de casos de unidade temporária Olá. Olá ligado SO e discos de dados são sempre mantidos. 

* **Planeada eventos manutenção** atualizações periódicas efetuadas pelo toohello Microsoft subjacente tooimprove da plataforma Azure fiabilidade geral, o desempenho e segurança da infraestrutura de plataforma de Olá executar as máquinas virtuais. A maior parte destas atualizações são realizadas sem exercer qualquer impacto nas suas Máquinas Virtuais ou Serviços Cloud (consulte [Manutenção de Conservação de VMs](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance)). Enquanto Olá plataforma Azure tenta toouse manutenção Preserving VM em todos os ocasiões possíveis, existem instâncias raras quando estas atualizações requerem um reinício da máquina virtual tooapply Olá atualizações necessárias toohello subjacente infraestrutura. Neste caso, pode realizar a manutenção planeada do Azure com a operação de manutenção a implementar iniciando manutenção Olá para as respetivas VMs na janela de tempo adequado Olá. Para obter mais informações, consulte [Manutenção Planeada para Máquinas Virtuais](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/).


impacto de Olá tooreduce período de indisponibilidade devido tooone ou mais destes eventos, recomendamos que Olá seguir as melhores práticas de elevada disponibilidade para as máquinas virtuais:

* [Configurar várias máquinas virtuais num conjunto de disponibilidade para redundância]
* [Utilizar discos geridos para VMs num conjunto de disponibilidade]
* [Utilizar eventos agendados tooproactively resposta tooVM afetar eventos] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [Configurar cada camada da aplicação em conjuntos de disponibilidade separados]
* [Combinar um Balanceador de Carga com conjuntos de disponibilidade]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>Configurar várias máquinas virtuais num conjunto de disponibilidade para redundância
aplicação de tooyour de redundância de tooprovide, recomendamos que agrupe duas ou mais máquinas virtuais num conjunto de disponibilidade. Esta configuração assegura que durante a um evento de manutenção planeada ou, pelo menos uma máquina virtual está disponível e de que cumpre os Olá 99,95% SLA do Azure. Para obter mais informações, consulte Olá [SLA para máquinas virtuais](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Evite deixar isolada uma máquina virtual de instância única num conjunto de disponibilidade. As VMs nesta configuração não se qualificam para uma garantia SLA e passam por um período de indisponibilidade durante eventos de manutenção planeada do Azure, exceto quando uma VM única está a utilizar [Armazenamento Premium do Azure](../articles/storage/common/storage-premium-storage.md). Para VMs único utilizar o premium storage, aplicam-se Olá SLA do Azure.

Cada máquina virtual no seu conjunto de disponibilidade é atribuída um **domínio de atualização** e um **domínio de falhas** por Olá subjacente plataforma Azure. Para um conjunto de disponibilidade especificado, os domínios de atualização não configurável utilizador cinco são atribuídos por predefinição (implementações do Resource Manager, em seguida, podem ser tooprovide aumento dos domínios de atualização de too20) tooindicate grupos de máquinas virtuais e o hardware físico subjacente que pode ser reiniciado no Olá mesmo tempo. Quando são configuradas mais de cinco máquinas virtuais dentro de um conjunto de disponibilidade único, Olá sexto máquina de virtual é colocada no Olá mesmo atualizar o domínio como Olá primeira máquina virtual, hello seventh no Olá que mesmo atualizar o domínio como Olá segunda máquina virtual e, de modo no. ordem de Olá dos domínios de atualização que está a ser reiniciado pode não continuar sequencialmente durante a manutenção planeada, mas o domínio de atualização apenas uma é reiniciado cada vez. Um domínio de atualização reinicializada é dado toorecover de 30 minutos antes de manutenção é iniciada a um domínio de atualização diferentes.

Domínios de falhas definem o grupo de Olá de máquinas virtuais que partilham um comutador de rede de origem e de energia comum. Por predefinição, as máquinas de virtuais Olá configuradas no seu conjunto de disponibilidade estiverem separadas através dos domínios de falhas de toothree para implementações do Resource Manager (dois domínios de falha para clássica). Enquanto colocar as máquinas virtuais para um conjunto de disponibilidade não protege a aplicação do sistema operativo ou falhas de aplicação específicos, limitar o impacto Olá de potenciais falhas de hardware físico, falhas de rede ou interrupções de energia.

<!--Image reference-->
   ![Desenho conceptual de Olá atualização domínio e falhas configuração do domínio](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>Utilizar discos geridos para VMs num conjunto de disponibilidade
Se estiver a utilizar atualmente VMs com discos não geridos, recomendamos vivamente [converter VMs no conjunto de disponibilidade toouse geridos discos](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md).

[Discos geridos pelo](../articles/virtual-machines/windows/managed-disks-overview.md) fornece melhor fiabilidade para conjuntos de disponibilidade, garantindo que discos Olá de VMs num conjunto de disponibilidade suficientemente estão isoladas umas das outras tooavoid pontos únicos de falha. Este é automaticamente colocando discos Olá em clusters de armazenamento diferente. Se um cluster de armazenamento falhar devido a falha de toohardware ou de software, apenas instâncias de VM Olá com discos os carimbos de data / falharem.

![Domínios de Falhas de Discos Geridos](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> número de Olá de domínios de falhas para conjuntos de disponibilidade gerido varia consoante a região - dois ou três por região. Olá tabela seguinte mostra o número de Olá por região

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Se planear toouse VMs com [não gerido discos](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), siga abaixo melhores práticas para as contas do Storage onde os discos rígidos virtuais (VHDs) de VMs são armazenados como [blobs de páginas](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs).

1. **Manter todos os discos (SO e dados) associados uma VM no Olá mesma conta de armazenamento**
2. **Olá revisão [limites](../articles/storage/common/storage-scalability-targets.md) no número de Olá de gerido discos numa conta do Storage** antes de adicionar a conta do storage mais tooa de VHDs
3. **Utilize uma conta de armazenamento separada para cada VM num Conjunto de Disponibilidade.** Não deve partilhar contas de armazenamento com várias VMs no Olá mesmo conjunto de disponibilidade. É aceitável para as VMs em diferentes conjuntos de disponibilidade tooshare as contas de armazenamento se forem seguidos acima melhores práticas

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>Configurar cada camada da aplicação em conjuntos de disponibilidade separados
Se as máquinas virtuais são idênticas quase todas as e servir Olá mesmo objetivo para a sua aplicação, recomendamos que configure um conjunto de disponibilidade para cada camada da aplicação.  Se colocar duas diferentes tiers no Olá mesmo conjunto de disponibilidade, todas as máquinas virtuais Olá mesma camada de aplicação pode ser reiniciada em simultâneo. Ao configurar, pelo menos, duas máquinas virtuais num conjunto de disponibilidade para cada camada, garante que, pelo menos, uma máquina virtual em cada camada está disponível.

Por exemplo, pode colocar a todas as máquinas de virtuais Olá no front-end de Olá da sua aplicação que executa o IIS, Apache, Nginx num conjunto de disponibilidade único. Certifique-se de que apenas front-end máquinas virtuais que são colocadas em Olá mesmo conjunto de disponibilidade. Da mesma forma, certifique-se de que apenas as máquinas virtuais de camadas de dados são colocadas no seu próprio conjunto de disponibilidade, como as máquinas virtuais replicadas do SQL Server ou as máquinas virtuais MySQL.

<!--Image reference-->
   ![Camadas da aplicação](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>Combinar um balanceador de carga com conjuntos de disponibilidade
Combinar Olá [Balanceador de carga do Azure](../articles/load-balancer/load-balancer-overview.md) com um disponibilidade definido tooget Olá a maioria das aplicações resilientes. Olá Balanceador de carga do Azure distribui o tráfego entre várias máquinas virtuais. Para máquinas de virtuais nosso escalão Standard, Olá Balanceador de carga do Azure está incluído. Nem todos os escalões de máquina virtual incluem Olá Balanceador de carga do Azure. Para mais informações sobre o balanceamento de carga de máquinas virtuais, veja [Balanceamento de Carga de máquinas virtuais](../articles/virtual-machines/virtual-machines-linux-load-balance.md).

Se o Balanceador de carga Olá não estiver configurado toobalance tráfego em várias máquinas virtuais, em seguida, qualquer evento de manutenção planeada afeta Olá apenas tráfego que máquina virtual, fazendo com que uma camada de aplicação de tooyour de indisponibilidade. Colocação de várias máquinas virtuais de Olá mesmo camada em Olá mesmo carregar balanceador e disponibilidade conjunto permite tráfego toobe continuamente servidos por, pelo menos, uma instância.


<!-- Link references -->
[Configurar várias máquinas virtuais num conjunto de disponibilidade para redundância]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[Configurar cada camada da aplicação em conjuntos de disponibilidade separados]: #configure-each-application-tier-into-separate-availability-sets
[Combinar um Balanceador de Carga com conjuntos de disponibilidade]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[Utilizar discos geridos para VMs num conjunto de disponibilidade]: #use-managed-disks-for-vms-in-an-availability-set
