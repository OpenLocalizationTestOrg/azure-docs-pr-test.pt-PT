# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Regiões e disponibilidade para máquinas virtuais no Azure
Azure funciona em vários centros de dados em torno Olá mundo. Nestes centros de dados estão agrupados em regiões toogeographic, dando-lhe flexibilidade na escolher onde toobuild as suas aplicações. É importante toounderstand como e onde as máquinas virtuais (VMs) operar no Azure, juntamente com as opções toomaximize desempenho, disponibilidade e redundância. Este artigo fornece uma descrição geral da disponibilidade de Olá e funcionalidades de redundância do Azure.

## <a name="what-are-azure-regions"></a>O que são as regiões do Azure?
Criar recursos do Azure em regiões geográficas definidas como 'EUA oeste', 'Europa do Norte' ou 'Sudeste Asiático'. Pode rever Olá [lista de regiões e as respetivas localizações](https://azure.microsoft.com/regions/). Cada região, vários centros de dados existem tooprovide para redundância e disponibilidade. Esta abordagem proporciona flexibilidade quando conceber aplicações toocreate VMs mais próximos tooyour utilizadores e toomeet qualquer legal, compatibilidade, ou fiscais fins.

## <a name="special-azure-regions"></a>Regiões do Azure especiais
O Azure tem algumas regiões especiais que pode ser útil toouse quando a criação de aplicações para fins legais ou de compatibilidade. Estas regiões especiais incluem:

* **Gov (US) - Virginia** e **Gov (US) - Iowa**
  * Uma instância isolada da rede física e lógica do Azure para agências e parceiros do governo dos Estados Unidos da América, operada por pessoas selecionadas dos EUA. Inclui certificações de conformidades adicionais, como [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) e [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). Leia mais sobre o [Azure Government](https://azure.microsoft.com/features/gov/).
* **Leste da China** e **Norte da China**
  * Estas regiões estão disponíveis através de uma única parceria entre a Microsoft e 21Vianet, na qual Microsoft não mantém diretamente Olá centros de dados. Veja mais informações sobre o [Microsoft Azure na China](http://www.windowsazure.cn/).
* **Alemanha Central** e **Nordeste da Alemanha**
  * Estas regiões estão disponíveis através de um modelo de fidedigno de dados em dados de cliente permanecem na Alemanha sob o controlo de T-sistemas, uma empresa Deutsche Telekom, agir como administrador de dados em alemão de Olá.

## <a name="region-pairs"></a>Pares de região
Cada região do Azure se encontra emparelhado com outro região dentro Olá geografia mesma (por exemplo, EUA, Europa ou Ásia). Esta abordagem permite a replicação Olá de recursos, tais como o armazenamento VM, entre uma geografia que deve reduzem a probabilidade de Olá de perante desastres naturais, unrest civis, falhas de energia ou falhas de rede físico que afetam as regiões de uma só vez. As vantagens adicionais de pares de região incluem:

* O evento de Olá de uma vasta falha do Azure, é definida uma região sem cada par toohelp reduzir Olá toorestore de tempo para aplicações. 
* Atualizações do Azure planeadas são implementadas toopaired regiões um um período de indisponibilidade do tempo toominimize e o risco de indisponibilidade de aplicações.
* Dados continuam tooreside dentro Olá mesma geografia como respetivo par (exceto sul do Brasil) para fins de jurisdiction imposição dedução dos impostos e pela lei.

Os exemplos de pares de região incluem:

| Primária | Secundária |
|:--- |:--- |
| EUA Oeste |EUA Leste |
| Europa do Norte |Europa Ocidental |
| Sudeste Asiático |Ásia Oriental |

Pode ver Olá completa [lista de regionais pares aqui](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Disponibilidade de funcionalidades
Alguns serviços ou funcionalidades de VM só estão disponíveis em determinadas regiões, como VMs com tamanhos ou tipos de armazenamento específicos. Existem também alguns serviços do Azure global que não requerem tooselect uma determinada região, tal como [do Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [Gestor de tráfego](../articles/traffic-manager/traffic-manager-overview.md), ou [DNS do Azure](../articles/dns/dns-overview.md). tooassist a conceber o ambiente da aplicação, pode verificar Olá [disponibilidade dos serviços do Azure em cada região](https://azure.microsoft.com/regions/#services). 

## <a name="storage-availability"></a>Disponibilidade de armazenamento
A compreensão das regiões do Azure e localizações geográficas fica importante quando considerar Olá as opções de replicação de armazenamento disponível. Dependendo do tipo de armazenamento Olá, tem opções de replicação diferentes.

**Managed Disks do Azure**
* Armazenamento localmente redundante (LRS)
  * Replica os dados três vezes numa região de Olá no qual criou a conta de armazenamento.

**Discos com base na conta de armazenamento**
* Armazenamento localmente redundante (LRS)
  * Replica os dados três vezes numa região de Olá no qual criou a conta de armazenamento.
* Armazenamento com redundância de zona (ZRS)
  * Replica os dados três vezes em dois instalações de toothree, numa única região ou em duas regiões.
* Armazenamento georredundante (GRS)
  * Replica o dados tooa secundário região centenas de quilómetros região primária Olá.
* Armazenamento georredundante com acesso de leitura (RA-GRS)
  * Replica o dados tooa região secundária, tal como acontece com a GRS, mas também fornece dados de toohello acesso só de leitura na localização secundária Olá.

Olá tabela seguinte fornece uma descrição geral rápida das diferenças de Olá entre tipos de replicação de armazenamento Olá:

| Estratégia de replicação | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Os dados são replicados em vários locais. |Não |Sim |Sim |Sim |
| Podem ser ler dados a partir da localização secundária Olá e de localização primária Olá. |Não |Não |Não |Sim |
| Número de cópias dos dados mantidas em nós separados. |3 |3 |6 |6 |

Pode ler mais sobre as [opções de replicação de Armazenamento do Azure aqui](../articles/storage/common/storage-redundancy.md). Para mais informações sobre discos geridos, veja [Managed Disks Overview (Descrição geral dos Managed Disks)](../articles/virtual-machines/windows/managed-disks-overview.md).

### <a name="storage-costs"></a>Custos de armazenamento
Os preços podem variar consoante o tipo de armazenamento Olá e disponibilidade que selecionar.

**Managed Disks do Azure**
* Os discos geridos Premium são apoiados por unidades de Solid-State (SSDs) e discos geridos padrão são apoiados por discos girar regular. Serem cobrados com base na capacidade de Olá aprovisionado para disco Olá discos geridos Standard e Premium.

**Discos não geridos**
* Armazenamento Premium é copiado por Solid-State unidades (SSDs) e é cobrado com base na capacidade de Olá do disco de Olá.
* Armazenamento Standard é copiado por discos girar regular e é cobrado com base na capacidade do Olá em utilização e pretender a disponibilidade de armazenamento.
  * Para RA-GRS, há um custo de transferência de dados de Georreplicação adicional para Olá largura de banda de replicar esse tooanother dados região do Azure.

Consulte [preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/) para obter informações sobre opções de disponibilidade e Olá diferentes tipos de armazenamentos de preços.

## <a name="availability-sets"></a>Conjuntos de disponibilidade
Um conjunto de disponibilidade é um agrupamento lógico de VMs que lhe permite toounderstand do Azure como a aplicação é criada tooprovide para redundância e disponibilidade. Recomendamos que dois ou mais VMs são criadas dentro de um tooprovide de conjunto de disponibilidade para uma elevada Olá de aplicação e toomeet [99,95% SLA do Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Quando está a utilizar uma única VM [Premium Storage do Azure](../articles/storage/common/storage-premium-storage.md), Olá SLA do Azure aplica-se para eventos de manutenção não planeada. 

Um conjunto de disponibilidade é composto por dois agrupamentos adicionais que protegem contra falhas de hardware e permitem atualizações toosafely ser aplicada - domínios (FDs) de falha e domínios (UDs) de atualização.

![Desenho conceptual de Olá atualização domínio e falhas configuração do domínio](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

Pode ler mais sobre como toomanage Olá disponibilidade dos [VMs com Linux](../articles/virtual-machines/linux/manage-availability.md) ou [VMs do Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Domínios de falha
Um domínio de falhas é um grupo lógico de hardware subjacente que partilham uma fonte de energia comum e um comutador de rede, semelhante tooa bastidor dentro de um datacenter no local. Como criar VMs dentro de um conjunto de disponibilidade, Olá plataforma Azure automaticamente distribui as suas VMs estes domínios de falhas. Esta abordagem limita impacto Olá de potenciais falhas de hardware físico, falhas de rede ou interrupções de energia.

### <a name="update-domains"></a>Domínios de atualização
Um domínio de atualização é um grupo lógico de hardware subjacente, que pode são submetidos a manutenção ou ser reiniciado no Olá mesmo tempo. Como criar VMs dentro de um conjunto de disponibilidade, hello plataforma Azure automaticamente distribui as suas VMs estes domínios de atualização. Esta abordagem garante que, pelo menos, uma instância da sua aplicação permanece sempre em execução como hello plataforma Azure sofre manutenção periódica. ordem de Olá dos domínios de atualização que está a ser reiniciado pode não continuar sequencialmente durante a manutenção planeada, mas o domínio de atualização apenas uma é reiniciado cada vez.

### <a name="managed-disk-fault-domains"></a>Domínios de falhas de disco geridos
Para as VMs que utilizam os [Managed Disks do Azure](../articles/virtual-machines/windows/faq-for-disks.md), as VMs são alinhadas com domínios de falha de discos geridos ao utilizar um conjunto de disponibilidade gerido. Este alinhamento garante que todos os Olá de gerido discos anexado tooa VM respeitam Olá mesmo domínio de falhas de disco gerido. Apenas as VMs com discos geridos podem ser criadas num conjunto de disponibilidade gerido. número de Olá de domínios de falhas de disco gerido varia consoante a região - duas ou três domínios de falhas de disco gerido por região.

![Domínios de Falhas de Discos Geridos](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> número de Olá de domínios de falhas para conjuntos de disponibilidade gerido varia consoante a região - dois ou três por região. Olá tabela seguinte mostra o número de Olá por região

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>Passos seguintes
É agora possível iniciar toouse estes disponibilidade e redundância funcionalidades toobuild do seu ambiente do Azure. Para informações relativas a melhores práticas, veja [Melhores Práticas de Disponibilidade do Azure](../articles/best-practices-availability-checklist.md).

